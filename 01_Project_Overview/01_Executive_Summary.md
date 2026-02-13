# 1. Project Overview

## 1.1. Introduction

The Rasid National Platform is a comprehensive, modern web application designed to serve as a central hub for news, media, and internal communication. It provides a rich user experience with a wide range of features for both public users and internal administrators. The platform is built on a modern technology stack, emphasizing performance, scalability, and maintainability.

## 1.2. Purpose and Scope

The primary purpose of the Rasid National Platform is to disseminate information effectively and engage with its audience through various content types, including news articles, videos, image galleries, and presentations. It also serves as a collaboration and content management tool for internal teams, with features for content creation, approval workflows, and user management.

The scope of the project encompasses the following key areas:

*   **Public-facing portal:** A feature-rich website for consuming content.
*   **Administrative dashboard:** A comprehensive backend for managing content, users, and system settings.
*   **Content management:** A robust system for creating, editing, and publishing various types of content.
*   **User engagement:** Features like comments, bookmarks, and social sharing to foster user interaction.
*   **Media delivery:** Efficient delivery of images, videos, and documents.

## 1.3. Key Features

The platform includes a wide array of features, which can be broadly categorized as follows:

| Category | Features |
| :--- | :--- |
| **Content Consumption** | News feed, video player, image gallery, presentation viewer, guides, and links. |
| **User Interaction** | Bookmarking, liking, commenting, and guestbook. |
| **Personalization** | User profiles, personal dashboards, and role-based dashboards. |
| **Administration** | User management, role management, content approval workflows, content scheduling, and analytics. |
| **Communication** | Internal messaging system and real-time notifications. |
| **Settings** | SMTP settings and other system configurations. |

## 1.4. Technology Stack

The platform is built using a modern, robust technology stack, ensuring a high-quality user experience and a scalable architecture.

### 1.4.1. Frontend

| Technology | Description |
| :--- | :--- |
| **Framework** | React 19 |
| **Language** | TypeScript |
| **Build Tool** | Vite |
| **Styling** | TailwindCSS |
| **UI Library** | Radix UI (shadcn/ui) |
| **State Management** | React Query (TanStack Query) |
| **Routing** | Wouter |
| **Animations** | Framer Motion |
| **Rich Text Editor** | Tiptap |
| **Charts** | Recharts |
| **Notifications** | Sonner |
| **Font** | Tajawal (Arabic) |
| **Icons** | Lucide React |

### 1.4.2. Backend

| Technology | Description |
| :--- | :--- |
| **Runtime** | Node.js |
| **API Framework** | tRPC |
| **Database** | MySQL/TiDB (via Drizzle ORM) |
| **Authentication** | JWT (JSON Web Tokens) |
| **File Storage** | Manus CDN (manuscdn.com) |
| **Hosting** | Manus Platform |
