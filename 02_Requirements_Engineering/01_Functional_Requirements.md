# Rasid National Platform: Requirements Engineering

This document outlines the functional and non-functional requirements for the Rasid National Platform, a comprehensive digital ecosystem for managing and disseminating official information. It details user roles, system features, and technical specifications to guide the development and implementation process.

## 1. User Roles and Personas

The platform is designed to serve a diverse user base with distinct roles and permissions. These roles ensure a structured and secure environment for content management, administration, and public access.

| Role                | Description                                                                                                                            | Key Responsibilities                                                                                                                                      |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Administrator**   | Has full control over the system, including user management, system settings, and content oversight.                                 | - Manage user accounts and roles<br>- Configure system-wide settings (e.g., SMTP)<br>- Monitor system activity and analytics<br>- Oversee all content         |
| **Content Moderator** | Reviews and approves content submitted by editors and other users to ensure it meets quality and compliance standards.                 | - Review and approve/reject news, videos, and other content<br>- Ensure content adheres to platform guidelines<br>- Manage content scheduling and publishing |
| **Editor**          | Creates, edits, and manages various types of content, such as news articles, videos, and guides.                                       | - Create and edit content<br>- Submit content for approval<br>- Manage tags and categories                                                              |
| **Member**          | A registered user with access to exclusive content and features not available to the general public.                                   | - Access member-only content and services<br>- Manage personal profile and bookmarks<br>- Interact with community features (e.g., comments, likes)         |
| **User**            | A registered user with basic access to the platform's features.                                                                        | - Access public content<br>- Manage personal profile and bookmarks<br>- Interact with community features                                                      |
| **Viewer**          | A guest user who can browse and view public content without needing to register an account.                                            | - View public news, videos, and other content                                                                                                             |

## 2. Functional Requirements

Functional requirements define the specific behaviors and features of the system. They are categorized into public-facing features, user-specific functionalities, and administrative capabilities.

### 2.1. Public-Facing and Core Features

These features are accessible to all users, including unregistered guests, and form the core of the public-facing portal.

- **Homepage:** A dynamic landing page (`/`) showcasing the latest news, featured content, and key announcements.
- **News Portal:** A dedicated section for news articles (`/news`), with a listing page and detailed view (`/news/:id`) for each article.
- **Media Galleries:** Separate sections for video (`/videos`) and image (`/gallery`) galleries, allowing users to browse and view multimedia content.
- **Resource Libraries:** Centralized repositories for official documents, guides (`/guides`), presentations (`/presentations`), and external links (`/links`).
- **Search Functionality:** A global search feature (`/search`) enabling users to find content across the entire platform.
- **User Authentication:** Secure user login (`/login`) and password reset (`/reset-password`) functionalities.

### 2.2. Registered User and Member Features

These features are available to authenticated users and provide personalized experiences and community engagement tools.

- **Personalized Dashboard (`/my-dashboard`):** A customizable dashboard for users to access their content, bookmarks, and notifications.
- **Profile Management (`/profile`):** Allows users to update their personal information, change their password, and manage their avatar.
- **Bookmarking (`/bookmarks`):** Enables users to save their favorite content for easy access later.
- **Interactive Features:**
    - **Comments Section:** Allows users to engage in discussions on news articles and other content.
    - **Like Button:** Provides a simple mechanism for users to express their appreciation for content.
- **Member-Exclusive Services (`/member`):** Access to special content and services reserved for registered members.

### 2.3. Content Management and Administration

These features are restricted to authorized administrative roles (Administrator, Content Moderator, Editor) and are managed through a dedicated admin dashboard (`/dashboard`).

- **Content Creation and Editing:** A rich text editor for creating and formatting articles, with support for multimedia embedding.
- **Content Approval Workflow (`/approval`):** A multi-step approval process for news and videos, allowing editors to submit content and moderators to review, approve, or reject it.
- **Content Scheduling (`/scheduling`):** The ability to schedule the publication of news and videos for a future date and time.
- **User and Role Management (`/users`, `/roles`):** Tools for administrators to create, edit, and manage user accounts and their assigned roles.
- **Analytics and Reporting (`/analytics`):** A comprehensive analytics dashboard providing insights into user engagement, content performance, and system activity.
- **System Settings (`/smtp-settings`):** A secure interface for administrators to configure system-wide settings, such as email server configurations.

## 3. Non-Functional Requirements

Non-functional requirements define the system's operational characteristics and quality attributes.

- **Performance:** The platform must be highly responsive, with fast page load times and smooth user interactions, supported by a modern tech stack (React, Vite, Node.js) and efficient data fetching (tRPC, React Query).
- **Security:** Robust security measures are essential, including secure authentication (JWT), role-based access control, and protection against common web vulnerabilities.
- **Usability:** The user interface must be intuitive, accessible, and easy to navigate for all user groups, with a clean design and consistent layout.
- **Scalability:** The architecture must be scalable to handle a growing user base and increasing content volume, leveraging a robust database solution (MySQL/TiDB) and efficient backend services.
- **Maintainability:** The codebase must be well-structured, documented, and easy to maintain, following best practices for both frontend (TypeScript, Radix UI) and backend (tRPC, Drizzle ORM) development.

## 4. Data Requirements

The platform's data model is designed to support its diverse content types and functionalities. The following table provides an overview of the key database tables and their purpose.

| Table           | Description                                                                                                  |
| --------------- | ------------------------------------------------------------------------------------------------------------ |
| `news`          | Stores news articles, including their content, metadata, and publication status.                             |
| `videos`        | Manages video content, including URLs, thumbnails, descriptions, and playback permissions.                     |
| `images`        | Contains information about images in the gallery, including their URLs, metadata, and download permissions.   |
| `guides`        | Stores official documents and guides, including file paths, types, and access restrictions.                    |
| `presentations` | Manages presentation files, including slide counts, thumbnails, and member-only access flags.                |
| `links`         | A collection of curated external links with descriptions and categorization.                                 |
| `guestbook`     | Stores entries from the public guestbook, including messages and approval status.                            |
| `tags`          | Manages the tags used to categorize content across the platform.                                              |
| `users`         | Contains user account information, including authentication details, roles, and profile data.                  |
| `settings`      | A key-value store for system-wide configuration settings.                                                    |

## 5. API and Integration Requirements

The platform exposes a comprehensive set of API endpoints via tRPC for client-server communication. These endpoints are organized by feature and provide the necessary operations for all user interactions and administrative tasks.

### 5.1. Authentication (`auth`)
- **Queries:** `me`
- **Mutations:** `localLogin`, `logout`, `changePassword`, `requestPasswordReset`, `resetPassword`, `updateProfile`, `uploadAvatar`

### 5.2. Content Management
- **News (`news`):**
  - **Queries:** `list`, `all`, `latest`, `getById`
  - **Mutations:** `create`, `update`, `delete`
- **Videos (`videos`):**
  - **Queries:** `list`, `all`
  - **Mutations:** `create`, `update`, `delete`
- **Images (`images`):**
  - **Queries:** `list`, `all`
  - **Mutations:** `create`, `update`, `delete`
- **Guides (`guides`):**
  - **Queries:** `list`, `all`
  - **Mutations:** `create`, `update`, `delete`
- **Presentations (`presentations`):**
  - **Queries:** `list`, `all`, `getById`
  - **Mutations:** `create`, `update`, `delete`
- **Links (`links`):**
  - **Queries:** `list`, `all`
  - **Mutations:** `create`, `update`, `delete`

### 5.3. Community and Engagement
- **Guestbook (`guestbook`):**
  - **Queries:** `list`, `all`
  - **Mutations:** `create`, `approve`, `delete`
- **Tags (`tags`):**
  - **Queries:** `list`, `getContentByTag`
  - **Mutations:** `create`, `update`, `delete`
- **Bookmarks (`bookmarks`):**
  - **Queries:** `myBookmarks`, `isBookmarked`
  - **Mutations:** `toggle`
- **Notifications (`notifications`):**
  - **Queries:** `list`, `unreadCount`
  - **Mutations:** `markRead`, `markAllRead`

### 5.4. Administration and Management
- **Users (`users`):**
  - **Queries:** `list`
  - **Mutations:** `update`
- **Analytics (`analytics`):**
  - **Queries:** `overview`, `activityByDay`, `bookmarksByType`, `commentsByMonth`, `contentByMonth`, `likesByType`, `recentActivity`, `topLiked`, `userRegistrations`
  - **Mutations:** `generateReport`
- **Dashboard (`dashboard`):**
  - **Queries:** `stats`
- **Approval Workflow (`approval`):**
  - **Queries:** `mySubmissions`, `pendingNews`, `pendingVideos`
  - **Mutations:** `submitNews`, `submitVideo`, `reviewNews`, `reviewVideo`
- **Messaging (`messages`):**
  - **Queries:** `inbox`, `sent`, `unreadCount`, `users`
  - **Mutations:** `send`, `broadcast`, `delete`, `markRead`, `markUnread`
- **System Settings (`settings`, `smtp`):**
  - **Queries:** `getAll`, `getConfig`
  - **Mutations:** `set`, `saveConfig`, `testEmail`
- **Content Organization (`scheduling`, `contentOrder`):**
  - **Queries:** `allNewsWithStatus`, `allVideosWithStatus`, `scheduledNews`, `scheduledVideos`, `getNews`, `getVideos`
  - **Mutations:** `updateNewsStatus`, `updateVideoStatus`, `publishNow`, `updateNewsOrder`, `updateVideosOrder`
- **Weekly Reports (`weeklyReport`):**
  - **Queries:** `getData`, `getSettings`
  - **Mutations:** `saveSettings`, `sendNow`

### 5.5. General
- **Search (`search`):**
  - **Queries:** `query`
