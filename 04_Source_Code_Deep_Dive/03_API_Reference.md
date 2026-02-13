# API Reference

The Rasid National Platform exposes its API through tRPC (TypeScript Remote Procedure Call), which provides end-to-end type safety between the client and server. Unlike traditional REST APIs, tRPC procedures are invoked as typed function calls rather than HTTP endpoints. However, they are accessible via HTTP at the base path `/api/trpc/{router}.{procedure}`.

## 1. API Overview

| Property | Value |
|:---|:---|
| **Base URL** | `https://www.rasid.vip/api/trpc` |
| **Protocol** | tRPC over HTTP |
| **Serialization** | SuperJSON (preserves Date, Map, Set types) |
| **Authentication** | JWT via HTTP-only cookies |
| **Query Method** | `GET /api/trpc/{procedure}?input={encoded_json}` |
| **Mutation Method** | `POST /api/trpc/{procedure}` with JSON body `{"json": {...}}` |

## 2. Authentication Router (`auth`)

### 2.1. auth.me (Query)

| Property | Value |
|:---|:---|
| **Description** | Returns the currently authenticated user's profile |
| **Authentication** | Required (JWT cookie) |
| **Input** | None |
| **Success Response (200)** | `{ id, openId, name, email, role, username, displayName, mobile, title, avatarUrl, loginMethod, createdAt, updatedAt, lastSignedIn }` |
| **Error Response (401)** | `{ code: "UNAUTHORIZED", message: "Not authenticated" }` |

### 2.2. auth.localLogin (Mutation)

| Property | Value |
|:---|:---|
| **Description** | Authenticates a user with username and password |
| **Authentication** | Not required |
| **Input** | `{ username: string, password: string }` |
| **Success Response (200)** | `{ success: true, user: { id, name, displayName, role, username } }` + Set-Cookie header |
| **Error Responses** | `UNAUTHORIZED` (invalid credentials), `FORBIDDEN` (account locked), `BAD_REQUEST` (missing fields) |

### 2.3. auth.logout (Mutation)

| Property | Value |
|:---|:---|
| **Description** | Logs out the current user by clearing the JWT cookie |
| **Authentication** | Required |
| **Input** | None |
| **Success Response (200)** | `{ success: true }` |

### 2.4. auth.changePassword (Mutation)

| Property | Value |
|:---|:---|
| **Description** | Changes the authenticated user's password |
| **Authentication** | Required |
| **Input** | `{ currentPassword: string, newPassword: string }` |
| **Success Response (200)** | `{ success: true }` |
| **Error Responses** | `UNAUTHORIZED` (wrong current password), `BAD_REQUEST` (weak password) |

### 2.5. auth.requestPasswordReset (Mutation)

| Property | Value |
|:---|:---|
| **Description** | Sends a password reset email to the specified address |
| **Authentication** | Not required |
| **Input** | `{ email: string }` |
| **Success Response (200)** | `{ success: true }` |

### 2.6. auth.resetPassword (Mutation)

| Property | Value |
|:---|:---|
| **Description** | Resets a user's password using a reset token |
| **Authentication** | Not required |
| **Input** | `{ token: string, newPassword: string }` |
| **Success Response (200)** | `{ success: true }` |

### 2.7. auth.updateProfile (Mutation)

| Property | Value |
|:---|:---|
| **Description** | Updates the authenticated user's profile information |
| **Authentication** | Required |
| **Input** | `{ name?: string, displayName?: string, mobile?: string, title?: string }` |
| **Success Response (200)** | Updated user object |

### 2.8. auth.uploadAvatar (Mutation)

| Property | Value |
|:---|:---|
| **Description** | Uploads a new avatar image for the authenticated user |
| **Authentication** | Required |
| **Input** | `{ imageData: string }` (base64 encoded) |
| **Success Response (200)** | `{ avatarUrl: string }` |

## 3. News Router (`news`)

### 3.1. news.list (Query)

| Property | Value |
|:---|:---|
| **Description** | Returns published news articles, ordered by sortOrder |
| **Authentication** | Not required |
| **Input** | None |
| **Success Response (200)** | Array of news objects (published only, 15 items observed) |
| **Permissions** | Public access; only `isPublished=true` articles returned |

### 3.2. news.all (Query)

| Property | Value |
|:---|:---|
| **Description** | Returns all news articles including drafts and unpublished |
| **Authentication** | Required (Admin/Editor) |
| **Input** | None |
| **Success Response (200)** | Array of all news objects (18 items observed) |
| **Permissions** | Admin or Editor role required |

### 3.3. news.latest (Query)

| Property | Value |
|:---|:---|
| **Description** | Returns the most recently published news article |
| **Authentication** | Not required |
| **Input** | None |
| **Success Response (200)** | Array with single news object |

### 3.4. news.getById (Query)

| Property | Value |
|:---|:---|
| **Description** | Returns a specific news article by ID |
| **Authentication** | Not required (public articles); Required (unpublished) |
| **Input** | `{ id: number }` |
| **Success Response (200)** | Single news object |
| **Error Response (404)** | `{ code: "NOT_FOUND" }` |

### 3.5. news.create (Mutation)

| Property | Value |
|:---|:---|
| **Description** | Creates a new news article |
| **Authentication** | Required (Editor+) |
| **Input** | `{ title: string, content: string, summary?: string, imageUrl?: string, category?: string, visibility?: string, allowedUserIds?: number[] }` |
| **Success Response (200)** | Created news object with generated ID |

### 3.6. news.update (Mutation)

| Property | Value |
|:---|:---|
| **Description** | Updates an existing news article |
| **Authentication** | Required (Editor+ or author) |
| **Input** | `{ id: number, title?: string, content?: string, summary?: string, imageUrl?: string, category?: string, isPublished?: boolean, visibility?: string }` |
| **Success Response (200)** | Updated news object |

### 3.7. news.delete (Mutation)

| Property | Value |
|:---|:---|
| **Description** | Deletes a news article |
| **Authentication** | Required (Admin) |
| **Input** | `{ id: number }` |
| **Success Response (200)** | `{ success: true }` |

## 4. Videos Router (`videos`)

### 4.1. videos.list / videos.all (Queries)

Follow the same pattern as `news.list` / `news.all` with video-specific fields.

### 4.2. videos.create (Mutation)

| Property | Value |
|:---|:---|
| **Input** | `{ title: string, description?: string, videoUrl: string, videoUrlHd?: string, thumbnailUrl?: string, duration?: string, category?: string, visibility?: string, allowDownload?: boolean, allowPlay?: boolean, allowHdDownload?: boolean }` |

### 4.3. videos.update / videos.delete (Mutations)

Follow the same pattern as news mutations.

## 5. Images Router (`images`)

### 5.1. images.list / images.all (Queries)

| Property | Value |
|:---|:---|
| **Description** | Returns published/all images with gallery metadata |
| **Response Fields** | `id, title, description, imageUrl, imageUrlHd, imageUrlPreview, album, fileSize, mimeType, width, height, isPublished, visibility, allowedUserIds, allowDownload, allowHdDownload, authorId, createdAt` |

### 5.2. images.create / images.update / images.delete (Mutations)

Follow standard CRUD patterns with image-specific fields.

## 6. Guides Router (`guides`)

### 6.1. guides.list / guides.all (Queries)

| Property | Value |
|:---|:---|
| **Response Fields** | `id, title, description, fileUrl, fileType, guideType, category, isPublished, visibility, allowedUserIds, allowDownload, authorId, createdAt` |

## 7. Presentations Router (`presentations`)

### 7.1. presentations.list / presentations.all / presentations.getById (Queries)

| Property | Value |
|:---|:---|
| **Response Fields** | `id, title, description, fileUrl, thumbnailUrl, slideCount, category, isPublished, isMemberOnly, visibility, allowedUserIds, allowDownload, authorId, createdAt` |

## 8. Links Router (`links`)

### 8.1. links.list / links.all (Queries)

| Property | Value |
|:---|:---|
| **Response Fields** | `id, title, description, url, icon, category, sortOrder, isPublished, visibility, allowedUserIds, createdAt` |

## 9. Guestbook Router (`guestbook`)

### 9.1. guestbook.list (Query) — Public approved entries
### 9.2. guestbook.all (Query) — All entries including unapproved (Admin)
### 9.3. guestbook.create (Mutation)

| Property | Value |
|:---|:---|
| **Input** | `{ name: string, email?: string, message: string, organization?: string }` |

### 9.4. guestbook.approve (Mutation)

| Property | Value |
|:---|:---|
| **Input** | `{ id: number }` |
| **Permissions** | Admin role required |

## 10. Tags Router (`tags`)

### 10.1. tags.list (Query) — Returns all tags
### 10.2. tags.getContentByTag (Query)

| Property | Value |
|:---|:---|
| **Input** | `{ tagId: number }` or `{ tagName: string }` |
| **Response** | Content items associated with the specified tag |

### 10.3. tags.create / tags.update / tags.delete (Mutations)

Standard CRUD with `{ name: string, color?: string }` input.

## 11. Users Router (`users`)

### 11.1. users.list (Query)

| Property | Value |
|:---|:---|
| **Description** | Returns all registered users |
| **Authentication** | Required (Admin) |
| **Response Fields** | `id, name, email, role, username, displayName, mobile, title, avatarUrl, isActive, createdAt, lastSignedIn` |

### 11.2. users.update (Mutation)

| Property | Value |
|:---|:---|
| **Input** | `{ id: number, role?: string, isActive?: boolean, displayName?: string }` |
| **Permissions** | Admin role required |

## 12. Analytics Router (`analytics`)

### 12.1. analytics.overview (Query)

| Property | Value |
|:---|:---|
| **Response** | `{ news: number, videos: number, images: number, guides: number, presentations: number, links: number, users: number, comments: number, likes: number, messages: number }` |

### 12.2. analytics.activityByDay (Query)

Returns daily activity counts as an array of `{ date: string, count: number }`.

### 12.3. analytics.userRegistrations (Query)

Returns monthly registration counts.

### 12.4. analytics.topLiked / analytics.recentActivity / analytics.bookmarksByType / analytics.commentsByMonth / analytics.contentByMonth / analytics.likesByType (Queries)

Each returns aggregated analytics data in their respective formats.

### 12.5. analytics.generateReport (Mutation)

Generates a comprehensive analytics report for download.

## 13. Dashboard Router (`dashboard`)

### 13.1. dashboard.stats (Query)

| Property | Value |
|:---|:---|
| **Response** | `{ newsCount: 18, videosCount: 6, imagesCount: 32, guidesCount: 34, presentationsCount: 19, guestbookCount: 5, usersCount: 9, linksCount: 34, memberFilesCount: 5 }` |

## 14. Approval Router (`approval`)

### 14.1. approval.pendingNews / approval.pendingVideos (Queries)

Returns content items with `approvalStatus='pending'`.

### 14.2. approval.mySubmissions (Query)

| Property | Value |
|:---|:---|
| **Response** | `{ news: NewsItem[], videos: VideoItem[] }` |

### 14.3. approval.submitNews / approval.submitVideo (Mutations)

| Property | Value |
|:---|:---|
| **Input** | `{ id: number }` |

### 14.4. approval.reviewNews / approval.reviewVideo (Mutations)

| Property | Value |
|:---|:---|
| **Input** | `{ id: number, status: 'approved' | 'rejected', reviewNote?: string }` |

## 15. Messages Router (`messages`)

### 15.1. messages.inbox / messages.sent (Queries)

Returns message arrays for the authenticated user.

### 15.2. messages.unreadCount (Query)

Returns integer count of unread messages.

### 15.3. messages.users (Query)

Returns list of users available as message recipients.

### 15.4. messages.send (Mutation)

| Property | Value |
|:---|:---|
| **Input** | `{ recipientId: number, subject?: string, content: string }` |

### 15.5. messages.broadcast (Mutation)

| Property | Value |
|:---|:---|
| **Input** | `{ subject?: string, content: string }` |
| **Permissions** | Admin role required |

### 15.6. messages.markRead / messages.markUnread / messages.delete (Mutations)

| Property | Value |
|:---|:---|
| **Input** | `{ id: number }` |

## 16. Remaining Routers

### 16.1. Bookmarks (`bookmarks`)

- `myBookmarks` (Query) — Returns user's bookmarked items
- `isBookmarked` (Query) — `{ contentType: string, contentId: number }` → `boolean`
- `toggle` (Mutation) — `{ contentType: string, contentId: number }` → toggles bookmark

### 16.2. Notifications (`notifications`)

- `list` (Query) — Returns notification list
- `unreadCount` (Query) — Returns unread count
- `markRead` (Mutation) — `{ id: number }`
- `markAllRead` (Mutation) — No input

### 16.3. Settings (`settings`)

- `getAll` (Query) — Returns all settings as key-value pairs
- `set` (Mutation) — `{ key: string, value: string }`

### 16.4. SMTP (`smtp`)

- `getConfig` (Query) — Returns SMTP configuration
- `saveConfig` (Mutation) — `{ host, port, user, pass, from, secure }`
- `testEmail` (Mutation) — `{ to: string }`

### 16.5. Scheduling (`scheduling`)

- `allNewsWithStatus` / `allVideosWithStatus` (Queries) — Returns content with scheduling info
- `scheduledNews` / `scheduledVideos` (Queries) — Returns only scheduled items
- `updateNewsStatus` / `updateVideoStatus` (Mutations) — `{ id, status }`
- `publishNow` (Mutation) — `{ id, type: 'news' | 'video' }`

### 16.6. Content Order (`contentOrder`)

- `getNews` / `getVideos` (Queries) — Returns ordered content lists
- `updateNewsOrder` / `updateVideosOrder` (Mutations) — `{ orderedIds: number[] }`

### 16.7. Weekly Report (`weeklyReport`)

- `getData` (Query) — Returns weekly report data
- `getSettings` (Query) — `{ enabled: boolean, dayOfWeek: number, hour: number, recipients: string[] }`
- `saveSettings` (Mutation) — Same shape as getSettings response
- `sendNow` (Mutation) — Triggers immediate report delivery

### 16.8. Search (`search`)

- `query` (Query) — `{ q: string }` → Returns search results across all content types

## 17. Error Response Format

All tRPC errors follow a consistent format:

```json
{
  "error": {
    "json": {
      "message": "Error description",
      "code": -32004,
      "data": {
        "code": "NOT_FOUND | UNAUTHORIZED | FORBIDDEN | BAD_REQUEST | METHOD_NOT_SUPPORTED",
        "httpStatus": 404,
        "path": "router.procedure"
      }
    }
  }
}
```

| Error Code | HTTP Status | Description |
|:---|:---|:---|
| `NOT_FOUND` | 404 | Procedure or resource not found |
| `UNAUTHORIZED` | 401 | Authentication required or invalid |
| `FORBIDDEN` | 403 | Insufficient permissions |
| `BAD_REQUEST` | 400 | Invalid input parameters |
| `METHOD_NOT_SUPPORTED` | 405 | Wrong HTTP method (GET for mutation or POST for query) |
