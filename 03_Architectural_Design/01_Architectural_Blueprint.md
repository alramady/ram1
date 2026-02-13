'''
# Architectural Design

This section provides a detailed overview of the architectural design of the Rasid National Platform, covering the frontend and backend technologies, data models, and API structure.

## 1. Technology Stack

The platform is built on a modern, robust technology stack, ensuring scalability, performance, and maintainability.

### 1.1. Frontend

The frontend is a single-page application (SPA) developed using the following technologies:

| Category             | Technology                               |
| -------------------- | ---------------------------------------- |
| **Framework**        | React 19                                 |
| **Language**         | TypeScript                               |
| **Build Tool**       | Vite                                     |
| **Styling**          | TailwindCSS                              |
| **UI Library**       | Radix UI (via shadcn/ui)                 |
| **State Management** | React Query (TanStack Query)             |
| **Routing**          | Wouter                                   |
| **Animations**       | Framer Motion                            |
| **Rich Text Editor** | Tiptap                                   |
| **Charts**           | Recharts                                 |
| **Notifications**    | Sonner                                   |
| **Font**             | Tajawal (for Arabic script)              |
| **Icons**            | Lucide React                             |

### 1.2. Backend

The backend is powered by a Node.js runtime and leverages the following technologies:

| Category           | Technology                       |
| ------------------ | -------------------------------- |
| **Runtime**        | Node.js                          |
| **API Framework**  | tRPC                             |
| **Database**       | MySQL/TiDB (via Drizzle ORM)     |
| **Authentication** | JWT (JSON Web Tokens)            |
| **File Storage**   | Manus CDN (manuscdn.com)         |
| **Hosting**        | Manus Platform                   |

## 2. Data Model

The application's data is organized into several tables, each representing a core entity within the system. The following table outlines the database schema:

| Table           | Description                                      |
| --------------- | ------------------------------------------------ |
| `news`          | Stores news articles and related metadata.       |
| `videos`        | Manages video content and associated details.    |
| `images`        | Contains image gallery information.              |
| `guides`        | Stores downloadable guides and documents.        |
| `presentations` | Manages presentation files and metadata.         |
| `links`         | Stores a collection of external and internal links. |
| `guestbook`     | Collects entries from the visitor guestbook.     |
| `tags`          | Manages tags for content categorization.         |
| `users`         | Stores user account information and roles.       |
| `settings`      | Contains application-wide configuration settings.|

## 3. API Endpoints

The platform uses tRPC for type-safe API communication between the frontend and backend. The API is structured into logical namespaces, each with a set of queries (for data retrieval) and mutations (for data modification).

### 3.1. Authentication (`auth`)

- **Queries**: `me`
- **Mutations**: `localLogin`, `logout`, `changePassword`, `requestPasswordReset`, `resetPassword`, `updateProfile`, `uploadAvatar`

### 3.2. Content Management

- **News (`news`)**: `list`, `all`, `latest`, `getById`, `create`, `update`, `delete`
- **Videos (`videos`)**: `list`, `all`, `create`, `update`, `delete`
- **Images (`images`)**: `list`, `all`, `create`, `update`, `delete`
- **Guides (`guides`)**: `list`, `all`, `create`, `update`, `delete`
- **Presentations (`presentations`)**: `list`, `all`, `getById`, `create`, `update`, `delete`
- **Links (`links`)**: `list`, `all`, `create`, `update`, `delete`

### 3.3. User Interaction

- **Guestbook (`guestbook`)**: `list`, `all`, `create`, `approve`, `delete`
- **Tags (`tags`)**: `list`, `getContentByTag`, `create`, `update`, `delete`
- **Bookmarks (`bookmarks`)**: `myBookmarks`, `isBookmarked`, `toggle`
- **Notifications (`notifications`)**: `list`, `unreadCount`, `markRead`, `markAllRead`
- **Messages (`messages`)**: `inbox`, `sent`, `unreadCount`, `users`, `send`, `broadcast`, `delete`, `markRead`, `markUnread`

### 3.4. Administration & Analytics

- **Users (`users`)**: `list`, `update`
- **Analytics (`analytics`)**: `overview`, `activityByDay`, `bookmarksByType`, `commentsByMonth`, `contentByMonth`, `likesByType`, `recentActivity`, `topLiked`, `userRegistrations`, `generateReport`
- **Dashboard (`dashboard`)**: `stats`
- **Approval (`approval`)**: `mySubmissions`, `pendingNews`, `pendingVideos`, `submitNews`, `submitVideo`, `reviewNews`, `reviewVideo`
- **Settings (`settings`)**: `getAll`, `set`
- **SMTP (`smtp`)**: `getConfig`, `saveConfig`, `testEmail`
- **Scheduling (`scheduling`)**: `allNewsWithStatus`, `allVideosWithStatus`, `scheduledNews`, `scheduledVideos`, `updateNewsStatus`, `updateVideoStatus`, `publishNow`
- **Content Order (`contentOrder`)**: `getNews`, `getVideos`, `updateNewsOrder`, `updateVideosOrder`
- **Weekly Report (`weeklyReport`)**: `getData`, `getSettings`, `saveSettings`, `sendNow`

### 3.5. Search

- **Search (`search`)**: `query`

## 4. Client-Side Routing

The frontend uses `wouter` for client-side routing. The following table maps URL paths to their corresponding pages or features:

| Path                     | Page/Feature                     |
| ------------------------ | -------------------------------- |
| `/`                      | Home                             |
| `/news`                  | News listing                     |
| `/news/:id`              | News detail                      |
| `/videos`                | Videos listing                   |
| `/gallery`               | Image gallery                    |
| `/links`                 | Links listing                    |
| `/guides`                | Guides listing                   |
| `/presentations`         | Presentations listing            |
| `/presentations/:id`     | Presentation viewer              |
| `/guestbook`             | Guestbook/Visitor log            |
| `/about`                 | About page                       |
| `/help-center`           | Help center                      |
| `/login`                 | Login page                       |
| `/reset-password`        | Password reset                   |
| `/member`                | Member services                  |
| `/members`               | Members management (admin)       |
| `/profile`               | User profile                     |
| `/dashboard`             | Admin dashboard                  |
| `/my-dashboard`          | Personal dashboard               |
| `/role-dashboard`        | Role-based dashboard             |
| `/analytics`             | Analytics (admin)                |
| `/approval`              | Content approval (admin)         |
| `/bookmarks`             | User bookmarks                   |
| `/content-order`         | Content ordering (admin)         |
| `/messages`              | Messages/Inbox                   |
| `/roles`                 | Roles management (admin)         |
| `/scheduling`            | Content scheduling (admin)       |
| `/search`                | Search results                   |
| `/smtp-settings`         | SMTP settings (admin)            |
| `/tags`                  | Tags management (admin)          |
| `/weekly-reports`        | Weekly reports (admin)           |
| `/activity-log`          | Activity log (admin)             |
| `/404`                   | Not Found page                   |
'''
