# Rasid National Platform: User and Contributor Guides

This document provides comprehensive guides for both end-users and contributors of the Rasid National Platform. It covers the platform's functionalities from a user perspective and offers detailed instructions for developers who wish to contribute to the project.

## 1. User Guides

This section outlines the various features and functionalities available to different user roles within the Rasid National Platform.

### 1.1. User Roles and Permissions

The platform employs a role-based access control (RBAC) system to manage user permissions. The following roles are defined:

| Role                | Description                                                                                                                                      |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Admin**           | Has full access to all platform features, including user management, system settings, and content administration.                                |
| **Content Moderator** | Can review and approve content submitted by editors and other users.                                                                             |
| **Editor**          | Can create, edit, and submit content for review and publication.                                                                                 |
| **Viewer**          | Has read-only access to public content on the platform.                                                                                          |
| **User**            | A general registered user with access to basic features like commenting, bookmarking, and personalized dashboards.                                |
| **Moderator**       | Can manage user-generated content such as comments and guestbook entries.                                                                        |
| **Member**          | A special user role with access to exclusive member-only content and services.                                                                   |

### 1.2. Core Platform Features

#### 1.2.1. Content Consumption

- **News:** Stay updated with the latest articles and announcements.
- **Videos:** Watch a variety of video content.
- **Image Gallery:** Browse through albums of images.
- **Guides:** Access instructional and informational guides.
- **Presentations:** View and download presentations.
- **Links:** Discover a curated list of useful links.

#### 1.2.2. Interactive Features

- **Comments:** Engage in discussions on news articles and other content.
- **Likes:** Show appreciation for content.
- **Bookmarks:** Save content for later viewing.
- **Guestbook:** Leave messages and feedback for the platform administrators.

#### 1.2.3. Personalization

- **My Dashboard:** A personalized dashboard with relevant information and quick access to features.
- **Profile:** Manage your user profile and preferences.
- **Notifications:** Receive real-time notifications for important events.

### 1.3. Administrative Features

Administrators and other privileged roles have access to a powerful control panel to manage the platform:

- **User Management:** Manage user accounts, roles, and permissions.
- **Content Management:** Create, edit, approve, and publish content.
- **Content Ordering:** Organize the display order of news and videos.
- **Scheduling:** Schedule content for future publication.
- **Analytics:** View detailed analytics and generate reports on platform usage.
- **Settings:** Configure various system settings, including SMTP for email notifications.

## 2. Contributor Guides

This section is for developers and contributors who want to help build and improve the Rasid National Platform.

### 2.1. Getting Started

#### 2.1.1. Prerequisites

- **Node.js:** Required for both frontend and backend development.
- **Git:** For version control.

#### 2.1.2. Installation

1.  **Clone the repository:**

    ```bash
    git clone https://github.com/alramady/alqasem.git
    cd alqasem
    ```

2.  **Install dependencies:**

    The project is a monorepo. To install dependencies for both the client and server, you will need to navigate to the respective directories and run the package manager's install command.

### 2.2. Development Workflow

#### 2.2.1. Frontend

The frontend is a React application built with Vite and TypeScript. It uses TailwindCSS for styling and Radix UI for UI components.

- **Running the development server:**

  ```bash
  cd client
  pnpm dev
  ```

#### 2.2.2. Backend

The backend is a Node.js application using tRPC for API communication and Drizzle ORM for database interaction.

- **Running the development server:**

  ```bash
  cd server
  pnpm dev
  ```

### 2.3. Coding Standards

- **TypeScript:** All code should be written in TypeScript with strict type checking.
- **Linting and Formatting:** The project uses ESLint and Prettier to enforce a consistent code style. Please ensure your code adheres to these standards before submitting a pull request.

### 2.4. Submitting Contributions

1.  **Fork the repository.**
2.  **Create a new branch for your feature or bug fix.**
3.  **Make your changes and commit them with clear and descriptive messages.**
4.  **Push your changes to your fork.**
5.  **Open a pull request to the main repository.**

Your contribution will be reviewed by the project maintainers, and once approved, it will be merged into the main branch.
