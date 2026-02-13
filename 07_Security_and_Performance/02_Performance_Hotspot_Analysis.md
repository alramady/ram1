# Performance Hotspot Analysis

This document identifies potential performance bottlenecks in the Rasid National Platform, based on analysis of the application's architecture, API design, and client-side rendering patterns. Each hotspot is categorized by severity and accompanied by recommendations for mitigation.

## 1. Client-Side Performance Hotspots

### 1.1. Large Initial Bundle Size

**Severity:** Medium

The production JavaScript bundle is approximately 2.1 MB (minified). While Vite performs code splitting, the initial bundle still includes several heavy libraries that are loaded on every page visit.

| Library | Estimated Size | Used On |
|:---|:---|:---|
| Framer Motion | ~150 KB | All pages (PageTransition, animations) |
| Tiptap (Rich Text Editor) | ~200 KB | Content creation pages only |
| Recharts | ~180 KB | Analytics page only |
| Radix UI (all primitives) | ~120 KB | Various components |

**Recommendation:** Implement route-based code splitting with `React.lazy()` and `Suspense` to defer loading of Tiptap and Recharts until their respective pages are navigated to. Consider replacing Framer Motion with CSS animations for simple transitions.

### 1.2. Particle Animation Performance

**Severity:** Medium

The `FloatingParticles` and `ParticleBackground` components use HTML5 Canvas with `requestAnimationFrame` loops to render continuous particle animations. These animations run on the main thread and can cause frame drops on lower-powered devices, particularly mobile phones.

**Recommendation:** Implement a performance check on component mount (e.g., checking `navigator.hardwareConcurrency`) and reduce particle count or disable animations on low-powered devices. Consider using `OffscreenCanvas` with a Web Worker for the particle simulation.

### 1.3. Unoptimized Image Loading

**Severity:** Medium-High

The image gallery (`GalleryPage`) loads all 29+ images simultaneously without virtualization or lazy loading. Each image card triggers a network request for the standard-resolution image, which can result in significant bandwidth consumption and slow initial rendering.

**Recommendation:** Implement intersection-observer-based lazy loading for gallery images. Use the `imageUrlPreview` field (which exists in the schema but appears underutilized) to load low-resolution placeholders first. Consider implementing virtual scrolling for galleries with more than 50 images.

### 1.4. React Query Polling for Notifications

**Severity:** Low-Medium

The `NotificationBell` component polls the `notifications.unreadCount` endpoint at regular intervals to check for new notifications. This creates continuous network traffic even when the user is idle.

**Recommendation:** Replace polling with WebSocket-based push notifications (the `RealtimeNotifications` component suggests this may already be partially implemented). Alternatively, increase the polling interval when the browser tab is not focused using the `visibilitychange` event.

## 2. Backend Performance Hotspots

### 2.1. Unfiltered List Queries

**Severity:** Medium

Several tRPC query procedures (`news.all`, `videos.all`, `images.all`, `guides.all`, `links.all`) return all records without pagination. As the content library grows, these queries will return increasingly large payloads.

| Procedure | Current Count | Growth Risk |
|:---|:---|:---|
| `news.all` | 18 items | High (news is frequently added) |
| `images.all` | 32 items | High (gallery grows over time) |
| `guides.all` | 34 items | Medium |
| `links.all` | 34 items | Medium |
| `presentations.all` | 19 items | Medium |

**Recommendation:** Implement cursor-based or offset pagination for all list queries. Add server-side filtering and sorting parameters. Consider implementing infinite scroll on the frontend to load content incrementally.

### 2.2. Analytics Aggregation Queries

**Severity:** Medium

The analytics dashboard (`AnalyticsPage`) dispatches 6-9 parallel queries on page load, each of which likely performs aggregate SQL operations (COUNT, GROUP BY) across the entire dataset. As the database grows, these queries will become increasingly expensive.

**Recommendation:** Implement materialized views or pre-computed analytics tables that are updated periodically (e.g., via a cron job). Cache analytics results with a longer TTL since they don't need real-time accuracy. Consider implementing date range filters to limit the scope of aggregation queries.

### 2.3. Content Order Updates

**Severity:** Low

The `contentOrder.updateNewsOrder` and `contentOrder.updateVideosOrder` mutations accept an array of all content IDs in the desired order. This requires updating the `sortOrder` column for every record in the table, even if only one item's position changed.

**Recommendation:** Implement a more efficient ordering algorithm that only updates the affected records. Consider using a fractional ordering system (e.g., storing sort order as a float) to allow insertions without reordering all items.

### 2.4. Broadcast Messaging

**Severity:** Low-Medium

The `messages.broadcast` mutation sends a message to all registered users. This likely creates N database records (one per recipient) in a single transaction, which can be slow and may cause database lock contention as the user base grows.

**Recommendation:** Implement broadcast messages as a single record with a "broadcast" flag, rather than creating individual copies for each recipient. Alternatively, process broadcast delivery asynchronously using a background job queue.

## 3. Database Performance Hotspots

### 3.1. JSON Column Queries

**Severity:** Medium

Several tables use JSON columns (`allowedUserIds`) for storing arrays of user IDs. Querying these columns for access control checks (e.g., "does user X have access to this content?") requires JSON parsing at query time, which is significantly slower than indexed column lookups.

**Recommendation:** For frequently queried access control patterns, consider creating a separate junction table (e.g., `content_user_access`) with indexed foreign keys. This enables efficient JOIN-based access control queries.

### 3.2. Missing Indexes (Inferred)

**Severity:** Medium

Based on the query patterns observed, the following indexes are likely needed but may not be present:

| Table | Suggested Index | Reason |
|:---|:---|:---|
| `news` | `(isPublished, sortOrder)` | Public listing query optimization |
| `news` | `(approvalStatus)` | Approval queue filtering |
| `news` | `(authorId)` | Author-based content filtering |
| `videos` | `(isPublished, sortOrder)` | Public listing query optimization |
| `images` | `(isPublished, album)` | Gallery filtering by album |
| `users` | `(role)` | Role-based user queries |
| `users` | `(username)` | Login lookup optimization |

**Recommendation:** Review the Drizzle ORM schema definitions and add composite indexes for the most common query patterns. Use `EXPLAIN ANALYZE` on production queries to identify missing indexes.

## 4. Network Performance

### 4.1. CDN File Serving

**Severity:** Low

All media files are served from `files.manuscdn.com`, which provides CDN-level caching and distribution. However, there is no evidence of client-side caching headers being set for API responses, which means that tRPC query results may not be cached by the browser's HTTP cache.

**Recommendation:** Configure appropriate `Cache-Control` headers for public API responses (e.g., `news.list` could be cached for 60 seconds). Ensure that CDN-served files include proper `ETag` and `Last-Modified` headers for conditional requests.

### 4.2. SuperJSON Serialization Overhead

**Severity:** Low

The use of SuperJSON for tRPC serialization adds a small overhead to every API response, as it includes a `meta` object describing type transformations (e.g., Date objects). For large list responses, this metadata can add noticeable payload size.

**Recommendation:** For performance-critical endpoints, consider using standard JSON serialization with explicit date string formatting, eliminating the need for SuperJSON's type metadata.

## 5. Summary

| Hotspot | Severity | Impact | Effort to Fix |
|:---|:---|:---|:---|
| Large initial bundle | Medium | Slower first load | Medium |
| Particle animations | Medium | Frame drops on mobile | Low |
| Unoptimized image loading | Medium-High | Bandwidth waste, slow gallery | Low |
| Notification polling | Low-Medium | Unnecessary network traffic | Medium |
| Unfiltered list queries | Medium | Slow admin pages as data grows | Medium |
| Analytics aggregation | Medium | Slow analytics page | High |
| JSON column queries | Medium | Slow access control checks | High |
| Missing database indexes | Medium | Suboptimal query performance | Low |
