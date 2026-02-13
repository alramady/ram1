
> This document provides a detailed walkthrough of the Rasid National Platform's source code, offering insights into the structure, purpose, and implementation of key files and components. The analysis is based on the master analysis file and aims to give developers a comprehensive understanding of the codebase.

## 1. Key Directories and Files

The following table outlines the key directories and files in the Rasid National Platform's codebase, along with their primary functions:

| Path | Description |
| --- | --- |
| `client/src/` | Main source code directory for the frontend application. |
| `client/src/App.tsx` | Main application component responsible for routing and layout. |
| `client/src/main.tsx` | The entry point of the React application. |
| `client/src/components/` | Contains reusable React components used throughout the application. |
| `client/src/pages/` | Contains the main page components for different routes. |
| `client/src/contexts/` | Holds React context providers for state management. |
| `server/` | Main source code directory for the backend application. |

## 2. Component Analysis

This section provides a detailed breakdown of the React components that form the building blocks of the user interface.

### 2.1. Core Components

| Component | Description |
| --- | --- |
| `AnimatedCounter.tsx` | An animated counter that increments from a starting value to a target value. |
| `BookmarkButton.tsx` | A button that allows users to bookmark content. |
| `CommentsSection.tsx` | A component that displays a list of comments and allows users to add new ones. |
| `ErrorBoundary.tsx` | A React error boundary to catch and handle errors in its component tree. |
| `FloatingParticles.tsx` | A component that renders floating particles for visual effect. |
| `Footer.tsx` | The standard footer for the application. |
| `GuidedTour.tsx` | A component that provides a guided tour for new users. |
| `Layout.tsx` | The main layout component that wraps the page content. |
| `LikeButton.tsx` | A button that allows users to like content. |
| `MediaViewer.tsx` | A modal component for viewing media such as images and videos. |
| `Navbar.tsx` | The main navigation bar for the application. |
| `NotificationBell.tsx` | A component that displays a notification bell with a count of unread notifications. |
| `PageTransition.tsx` | A component that provides an animated transition between pages. |
| `PdfReportButton.tsx` | A button that generates and downloads a PDF report. |
| `PresentationMode.tsx` | A component that enables a fullscreen presentation mode. |
| `PresentationToolbar.tsx` | The toolbar for the presentation mode. |
| `RealtimeNotifications.tsx` | A component that handles real-time notifications. |
| `RichTextEditor.tsx` | A rich text editor based on Tiptap for creating and editing content. |
| `ScrollProgressBar.tsx` | A progress bar that indicates the user's scroll position on the page. |
| `SectionHeader.tsx` | A header component for sections of a page. |

### 2.2. UI Components (shadcn/ui)

The application utilizes a set of UI components from `shadcn/ui`, which are built on top of Radix UI.

| Component | Description |
| --- | --- |
| `avatar.tsx` | An avatar component. |
| `badge.tsx` | A badge component for displaying status or labels. |
| `button.tsx` | A standard button component. |
| `card.tsx` | A card component for grouping content. |
| `checkbox.tsx` | A checkbox component. |
| `dialog.tsx` | A dialog or modal component. |
| `dropdown-menu.tsx` | A dropdown menu component. |
| `input.tsx` | A standard input field. |
| `label.tsx` | A label for form elements. |
| `popover.tsx` | A popover component. |
| `scroll-area.tsx` | A component with a scrollable area. |
| `select.tsx` | A select or dropdown list component. |
| `separator.tsx` | A separator line. |
| `sheet.tsx` | A sheet or drawer component that slides in from the side. |
| `sonner.tsx` | A toast notification component. |
| `switch.tsx` | A switch toggle component. |
| `tabs.tsx` | A tabs component for organizing content. |
| `textarea.tsx` | A textarea component for multi-line text input. |
| `tooltip.tsx` | A tooltip component. |

## 3. State Management

The application uses **React Query (TanStack Query)** for managing server state. This library simplifies data fetching, caching, and synchronization with the backend.

- **`ThemeContext.tsx`**: This context is used for managing the application's theme (dark/light mode).

## 4. Routing

The application uses **Wouter** for routing. The main routes are defined in `App.tsx`, which maps URL paths to their corresponding page components.

| Route | Page Component | Description |
| --- | --- | --- |
| `/` | `Home.tsx` | The homepage of the application. |
| `/news` | `NewsPage.tsx` | Displays a list of news articles. |
| `/news/:id` | `NewsDetailPage.tsx` | Displays the details of a single news article. |
| `/videos` | `VideosPage.tsx` | Displays a list of videos. |
| `/gallery` | `GalleryPage.tsx` | Displays a gallery of images. |
| `/login` | `LoginPage.tsx` | The user login page. |
| `/dashboard` | `DashboardPage.tsx` | The admin dashboard. |

## 5. Backend (tRPC) API

The backend is built using **tRPC**, which allows for typesafe API routes. The tRPC procedures are organized by feature.

### 5.1. Authentication (`auth`)

- **Queries**: `me`
- **Mutations**: `localLogin`, `logout`, `changePassword`, `requestPasswordReset`, `resetPassword`, `updateProfile`, `uploadAvatar`

### 5.2. News (`news`)

- **Queries**: `list`, `all`, `latest`, `getById`
- **Mutations**: `create`, `update`, `delete`

### 5.3. Videos (`videos`)

- **Queries**: `list`, `all`
- **Mutations**: `create`, `update`, `delete`

