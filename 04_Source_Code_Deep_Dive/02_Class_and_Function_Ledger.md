# Class and Function Ledger

This document provides a comprehensive inventory of all React components (which serve as the primary class-like constructs in this functional React codebase) and their key functions, hooks, and state management patterns. Since the Rasid National Platform is built entirely with React functional components and hooks, this ledger is organized by component rather than by traditional class hierarchy.

## 1. Page Components

### 1.1. Home (`client/src/pages/Home.tsx`)

| Property | Description |
|:---|:---|
| **Purpose** | Main landing page displaying featured content, latest news, and platform highlights |
| **State** | Server state via React Query: `news.latest`, `videos.list`, `presentations.list` |
| **Key Functions** | Content rendering, animated counters for statistics, particle background effects |
| **Dependencies** | `AnimatedCounter`, `FloatingParticles`, `SectionHeader`, `PageTransition` |

### 1.2. LoginPage (`client/src/pages/LoginPage.tsx`)

| Property | Description |
|:---|:---|
| **Purpose** | User authentication with username/password login |
| **State** | Local state: `username`, `password`, `error`, `passwordStrength` |
| **Key Functions** | `handleSubmit` — validates inputs, calls `auth.localLogin` mutation; `calculatePasswordStrength` — real-time password strength assessment (5 levels) |
| **Mutations** | `auth.localLogin` — authenticates user and sets JWT cookie |
| **Error Handling** | Displays error messages from server; handles account lockout notifications |

### 1.3. DashboardPage (`client/src/pages/DashboardPage.tsx`)

| Property | Description |
|:---|:---|
| **Purpose** | Admin dashboard with content statistics and quick actions |
| **State** | Server state: `dashboard.stats` query |
| **Key Functions** | Renders stat cards for news, videos, images, guides, presentations, guestbook, users, links, member files |
| **Access Control** | Admin role required |

### 1.4. NewsPage (`client/src/pages/NewsPage.tsx`)

| Property | Description |
|:---|:---|
| **Purpose** | News listing page with filtering and search |
| **State** | Server state: `news.list` (public) or `news.all` (admin); Local state: filter, search, pagination |
| **Key Functions** | Content filtering by category, search functionality, pagination |
| **Dependencies** | `SectionHeader`, `BookmarkButton`, `LikeButton`, `PageTransition` |

### 1.5. NewsDetailPage (`client/src/pages/NewsDetailPage.tsx`)

| Property | Description |
|:---|:---|
| **Purpose** | Full article view with rich content rendering |
| **State** | Server state: `news.getById`; `bookmarks.isBookmarked` |
| **Key Functions** | HTML content rendering, social sharing, bookmark toggling, comment display |
| **Dependencies** | `ScrollProgressBar`, `CommentsSection`, `BookmarkButton`, `LikeButton`, `MediaViewer` |

### 1.6. AnalyticsPage (`client/src/pages/AnalyticsPage.tsx`)

| Property | Description |
|:---|:---|
| **Purpose** | Comprehensive analytics dashboard with charts and metrics |
| **State** | Server state: `analytics.overview`, `analytics.activityByDay`, `analytics.contentByMonth`, `analytics.userRegistrations`, `analytics.topLiked`, `analytics.recentActivity` |
| **Key Functions** | Chart rendering via Recharts, report generation, data aggregation |
| **Dependencies** | `PdfReportButton`, Recharts components |
| **Access Control** | Admin role required |

### 1.7. ApprovalPage (`client/src/pages/ApprovalPage.tsx`)

| Property | Description |
|:---|:---|
| **Purpose** | Content approval workflow management |
| **State** | Server state: `approval.pendingNews`, `approval.pendingVideos`, `approval.mySubmissions` |
| **Key Functions** | `handleApprove` — calls `approval.reviewNews`/`approval.reviewVideo` with approved status; `handleReject` — calls with rejected status and review note |
| **Mutations** | `approval.reviewNews`, `approval.reviewVideo` |
| **Access Control** | Content Moderator or Admin role required |

### 1.8. MessagesPage (`client/src/pages/MessagesPage.tsx`)

| Property | Description |
|:---|:---|
| **Purpose** | Internal messaging system with inbox, sent, and compose views |
| **State** | Server state: `messages.inbox`, `messages.sent`, `messages.unreadCount`, `messages.users` |
| **Key Functions** | `handleSend` — sends message via `messages.send` mutation; `handleBroadcast` — sends to all users via `messages.broadcast`; `handleMarkRead`/`handleMarkUnread` — toggles read status |
| **Mutations** | `messages.send`, `messages.broadcast`, `messages.delete`, `messages.markRead`, `messages.markUnread` |

### 1.9. SchedulingPage (`client/src/pages/SchedulingPage.tsx`)

| Property | Description |
|:---|:---|
| **Purpose** | Content scheduling and publication management |
| **State** | Server state: `scheduling.allNewsWithStatus`, `scheduling.allVideosWithStatus`, `scheduling.scheduledNews`, `scheduling.scheduledVideos` |
| **Key Functions** | `handlePublishNow` — immediately publishes content; `handleUpdateStatus` — changes publication status; `handleSchedule` — sets future publication date |
| **Mutations** | `scheduling.updateNewsStatus`, `scheduling.updateVideoStatus`, `scheduling.publishNow` |

### 1.10. RoleDashboardPage (`client/src/pages/RoleDashboardPage.tsx`)

| Property | Description |
|:---|:---|
| **Purpose** | Dynamic dashboard that renders different content based on user role |
| **State** | Server state: `auth.me` for role detection |
| **Key Functions** | Role-based component selection: `admin` → full dashboard; `content_moderator` → approval queue; `editor` → content creation; `viewer` → read-only content |
| **Role Mapping** | `{ admin: AdminDashboard, content_moderator: ModeratorDashboard, editor: EditorDashboard, viewer: ViewerDashboard, user: UserDashboard }` |

## 2. Reusable Components

### 2.1. Layout (`client/src/components/Layout.tsx`)

| Property | Description |
|:---|:---|
| **Purpose** | Main application layout wrapper providing consistent structure |
| **Props** | `children: ReactNode` |
| **Structure** | `Navbar` → `main content` → `Footer` |
| **Features** | Responsive layout, RTL support, theme-aware styling |

### 2.2. Navbar (`client/src/components/Navbar.tsx`)

| Property | Description |
|:---|:---|
| **Purpose** | Primary navigation bar with responsive menu |
| **State** | Server state: `auth.me` for user info; Local state: `isMenuOpen`, `isScrolled` |
| **Key Functions** | Scroll-based style changes, responsive hamburger menu, role-based navigation items |
| **Dependencies** | `NotificationBell`, `ThemeContext` |

### 2.3. RichTextEditor (`client/src/components/RichTextEditor.tsx`)

| Property | Description |
|:---|:---|
| **Purpose** | Full-featured rich text editor for content creation |
| **Props** | `content: string`, `onChange: (html: string) => void`, `placeholder?: string` |
| **State** | Tiptap editor instance |
| **Features** | Bold, italic, headings, lists, links, images, code blocks, blockquotes |
| **Dependencies** | `@tiptap/react`, `@tiptap/starter-kit` |

### 2.4. BookmarkButton (`client/src/components/BookmarkButton.tsx`)

| Property | Description |
|:---|:---|
| **Purpose** | Toggle button for bookmarking content items |
| **Props** | `contentType: string`, `contentId: number` |
| **State** | Server state: `bookmarks.isBookmarked` |
| **Mutations** | `bookmarks.toggle` — adds or removes bookmark |
| **Behavior** | Optimistic UI update with server reconciliation |

### 2.5. CommentsSection (`client/src/components/CommentsSection.tsx`)

| Property | Description |
|:---|:---|
| **Purpose** | Displays and manages comments on content items |
| **Props** | `contentType: string`, `contentId: number` |
| **State** | Local state: `newComment`; Server state: comments list |
| **Key Functions** | `handleSubmitComment` — posts new comment; `handleDeleteComment` — removes comment |

### 2.6. NotificationBell (`client/src/components/NotificationBell.tsx`)

| Property | Description |
|:---|:---|
| **Purpose** | Notification indicator with unread count badge |
| **State** | Server state: `notifications.unreadCount` (polled) |
| **Key Functions** | Polling for unread count, dropdown notification list, mark as read |
| **Dependencies** | `notifications.list`, `notifications.markRead`, `notifications.markAllRead` |

### 2.7. PdfReportButton (`client/src/components/PdfReportButton.tsx`)

| Property | Description |
|:---|:---|
| **Purpose** | Generates and downloads PDF reports from analytics data |
| **Props** | `data: AnalyticsData`, `title?: string` |
| **Key Functions** | `handleGenerateReport` — compiles data into PDF format and triggers download |

### 2.8. MediaViewer (`client/src/components/MediaViewer.tsx`)

| Property | Description |
|:---|:---|
| **Purpose** | Modal viewer for images and videos with zoom and navigation |
| **Props** | `media: MediaItem`, `isOpen: boolean`, `onClose: () => void` |
| **Features** | Fullscreen mode, zoom controls, keyboard navigation, download option |

### 2.9. PresentationMode (`client/src/components/PresentationMode.tsx`)

| Property | Description |
|:---|:---|
| **Purpose** | Fullscreen presentation viewer with slide navigation |
| **Props** | `slides: Slide[]`, `currentSlide: number` |
| **Key Functions** | Keyboard navigation (arrow keys), fullscreen toggle, slide counter |
| **Dependencies** | `PresentationToolbar` |

## 3. Animation Components

### 3.1. ParticleBackground (`client/src/components/animations/ParticleBackground.tsx`)

| Property | Description |
|:---|:---|
| **Purpose** | Canvas-based particle animation for visual backgrounds |
| **Props** | `particleCount?: number`, `color?: string`, `speed?: number` |
| **Implementation** | HTML5 Canvas with requestAnimationFrame loop |

### 3.2. ScrollReveal (`client/src/components/animations/ScrollReveal.tsx`)

| Property | Description |
|:---|:---|
| **Purpose** | Reveals child elements with animation as they scroll into view |
| **Props** | `children: ReactNode`, `direction?: 'up' | 'down' | 'left' | 'right'` |
| **Implementation** | Intersection Observer API + Framer Motion |

### 3.3. KineticText (`client/src/components/animations/KineticText.tsx`)

| Property | Description |
|:---|:---|
| **Purpose** | Animated text effects for headings and hero sections |
| **Props** | `text: string`, `animation?: 'typewriter' | 'wave' | 'bounce'` |
| **Implementation** | Framer Motion character-by-character animation |

## 4. Context Providers

### 4.1. ThemeContext (`client/src/contexts/ThemeContext.tsx`)

| Property | Description |
|:---|:---|
| **Purpose** | Manages dark/light theme state across the application |
| **Provided Values** | `theme: 'dark' | 'light'`, `toggleTheme: () => void` |
| **Persistence** | Theme preference stored in `localStorage` |
| **Implementation** | Toggles `dark` class on `document.documentElement` for TailwindCSS dark mode |

## 5. tRPC Hook Patterns

All data fetching in the application follows a consistent pattern using tRPC's React Query integration.

**Query Pattern:**
```typescript
const { data, isLoading, error } = trpc.{router}.{procedure}.useQuery(input);
```

**Mutation Pattern:**
```typescript
const mutation = trpc.{router}.{procedure}.useMutation({
  onSuccess: () => {
    utils.{router}.{relatedQuery}.invalidate();
    toast.success("Operation successful");
  },
  onError: (error) => {
    toast.error(error.message || "Operation failed");
  }
});
```

This pattern ensures consistent error handling, cache invalidation, and user feedback across all data operations in the application.
