# Component Library

This document catalogs all reusable UI components in the Rasid National Platform, organized by category. Each entry includes the component's purpose, props interface, state management, and emitted events.

## 1. Custom Application Components

### 1.1. AnimatedCounter

| Property | Value |
|:---|:---|
| **File Path** | `client/src/components/AnimatedCounter.tsx` |
| **Description** | Displays a number that animates from 0 to a target value when scrolled into view |

| Prop | Type | Required | Description |
|:---|:---|:---|:---|
| `end` | `number` | Yes | Target number to count up to |
| `duration` | `number` | No | Animation duration in milliseconds (default: 2000) |
| `prefix` | `string` | No | Text displayed before the number |
| `suffix` | `string` | No | Text displayed after the number |

**State:** Internal `count` state animated via `requestAnimationFrame`. Uses Intersection Observer to trigger animation when visible.

### 1.2. BookmarkButton

| Property | Value |
|:---|:---|
| **File Path** | `client/src/components/BookmarkButton.tsx` |
| **Description** | Toggle button that allows authenticated users to bookmark content items |

| Prop | Type | Required | Description |
|:---|:---|:---|:---|
| `contentType` | `string` | Yes | Type of content (e.g., "news", "video") |
| `contentId` | `number` | Yes | ID of the content item |
| `size` | `"sm" \| "md" \| "lg"` | No | Button size variant |

**State:** Server state via `bookmarks.isBookmarked` query. Optimistic update on toggle.
**Events:** Triggers `bookmarks.toggle` mutation and invalidates `bookmarks.myBookmarks` cache.

### 1.3. CommentsSection

| Property | Value |
|:---|:---|
| **File Path** | `client/src/components/CommentsSection.tsx` |
| **Description** | Displays a list of comments and provides a form for adding new comments |

| Prop | Type | Required | Description |
|:---|:---|:---|:---|
| `contentType` | `string` | Yes | Type of content being commented on |
| `contentId` | `number` | Yes | ID of the content item |

**State:** Local state for new comment text; Server state for comments list.

### 1.4. ErrorBoundary

| Property | Value |
|:---|:---|
| **File Path** | `client/src/components/ErrorBoundary.tsx` |
| **Description** | React error boundary that catches rendering errors and displays a fallback UI |

| Prop | Type | Required | Description |
|:---|:---|:---|:---|
| `children` | `ReactNode` | Yes | Child components to wrap |
| `fallback` | `ReactNode` | No | Custom fallback UI |

**State:** `hasError: boolean`, `error: Error | null`.

### 1.5. FloatingParticles

| Property | Value |
|:---|:---|
| **File Path** | `client/src/components/FloatingParticles.tsx` |
| **Description** | Renders floating particle effects as a decorative background |

| Prop | Type | Required | Description |
|:---|:---|:---|:---|
| `count` | `number` | No | Number of particles (default: 50) |
| `color` | `string` | No | Particle color |

### 1.6. Footer

| Property | Value |
|:---|:---|
| **File Path** | `client/src/components/Footer.tsx` |
| **Description** | Application footer with copyright notice and navigation links |

No props. Renders static content with current year and platform branding.

### 1.7. GuidedTour

| Property | Value |
|:---|:---|
| **File Path** | `client/src/components/GuidedTour.tsx` |
| **Description** | Interactive onboarding tour that highlights key platform features |

| Prop | Type | Required | Description |
|:---|:---|:---|:---|
| `steps` | `TourStep[]` | Yes | Array of tour step definitions |
| `isOpen` | `boolean` | Yes | Whether the tour is active |
| `onComplete` | `() => void` | Yes | Callback when tour is completed |

**State:** `currentStep: number`.

### 1.8. Layout

| Property | Value |
|:---|:---|
| **File Path** | `client/src/components/Layout.tsx` |
| **Description** | Main layout wrapper providing Navbar, content area, and Footer |

| Prop | Type | Required | Description |
|:---|:---|:---|:---|
| `children` | `ReactNode` | Yes | Page content |

### 1.9. LikeButton

| Property | Value |
|:---|:---|
| **File Path** | `client/src/components/LikeButton.tsx` |
| **Description** | Heart-shaped toggle button for liking content items |

| Prop | Type | Required | Description |
|:---|:---|:---|:---|
| `contentType` | `string` | Yes | Type of content |
| `contentId` | `number` | Yes | ID of the content item |
| `initialCount` | `number` | No | Initial like count |

### 1.10. MediaViewer

| Property | Value |
|:---|:---|
| **File Path** | `client/src/components/MediaViewer.tsx` |
| **Description** | Modal overlay for viewing images and videos with zoom and download controls |

| Prop | Type | Required | Description |
|:---|:---|:---|:---|
| `media` | `MediaItem` | Yes | Media item to display |
| `isOpen` | `boolean` | Yes | Modal visibility state |
| `onClose` | `() => void` | Yes | Close handler |
| `onNext` | `() => void` | No | Navigate to next item |
| `onPrevious` | `() => void` | No | Navigate to previous item |

### 1.11. Navbar

| Property | Value |
|:---|:---|
| **File Path** | `client/src/components/Navbar.tsx` |
| **Description** | Primary navigation bar with responsive menu, user info, and theme toggle |

No external props. Consumes `auth.me` query and `ThemeContext`.

### 1.12. NotificationBell

| Property | Value |
|:---|:---|
| **File Path** | `client/src/components/NotificationBell.tsx` |
| **Description** | Bell icon with unread notification count badge and dropdown list |

No external props. Consumes `notifications.unreadCount` and `notifications.list` queries.

### 1.13. PageTransition

| Property | Value |
|:---|:---|
| **File Path** | `client/src/components/PageTransition.tsx` |
| **Description** | Wraps page content with Framer Motion enter/exit animations |

| Prop | Type | Required | Description |
|:---|:---|:---|:---|
| `children` | `ReactNode` | Yes | Page content to animate |

### 1.14. PdfReportButton

| Property | Value |
|:---|:---|
| **File Path** | `client/src/components/PdfReportButton.tsx` |
| **Description** | Button that generates and downloads a PDF report from provided data |

| Prop | Type | Required | Description |
|:---|:---|:---|:---|
| `data` | `object` | Yes | Report data to compile |
| `title` | `string` | No | Report title |
| `filename` | `string` | No | Downloaded file name |

### 1.15. PresentationMode / PresentationToolbar

| Property | Value |
|:---|:---|
| **File Path** | `client/src/components/PresentationMode.tsx`, `PresentationToolbar.tsx` |
| **Description** | Fullscreen presentation viewer with navigation toolbar |

| Prop | Type | Required | Description |
|:---|:---|:---|:---|
| `slides` | `Slide[]` | Yes | Array of slide data |
| `currentSlide` | `number` | Yes | Current slide index |
| `onNavigate` | `(index: number) => void` | Yes | Slide navigation handler |
| `onExit` | `() => void` | Yes | Exit fullscreen handler |

### 1.16. RichTextEditor

| Property | Value |
|:---|:---|
| **File Path** | `client/src/components/RichTextEditor.tsx` |
| **Description** | Full-featured WYSIWYG editor built on Tiptap for content creation |

| Prop | Type | Required | Description |
|:---|:---|:---|:---|
| `content` | `string` | Yes | Initial HTML content |
| `onChange` | `(html: string) => void` | Yes | Content change handler |
| `placeholder` | `string` | No | Placeholder text |
| `editable` | `boolean` | No | Whether editing is enabled |

### 1.17. ScrollProgressBar

| Property | Value |
|:---|:---|
| **File Path** | `client/src/components/ScrollProgressBar.tsx` |
| **Description** | Fixed progress bar at the top of the page indicating scroll position |

No props. Uses `window.scrollY` and `document.documentElement.scrollHeight` for calculation.

### 1.18. SectionHeader

| Property | Value |
|:---|:---|
| **File Path** | `client/src/components/SectionHeader.tsx` |
| **Description** | Styled header component for page sections with optional subtitle |

| Prop | Type | Required | Description |
|:---|:---|:---|:---|
| `title` | `string` | Yes | Section title |
| `subtitle` | `string` | No | Section subtitle |
| `icon` | `LucideIcon` | No | Icon component |

## 2. shadcn/ui Components

The following components are from the shadcn/ui library, built on Radix UI primitives. They provide accessible, customizable, and theme-aware UI elements.

| Component | File | Base Primitive | Description |
|:---|:---|:---|:---|
| **Avatar** | `ui/avatar.tsx` | `@radix-ui/react-avatar` | User avatar with image and fallback initials |
| **Badge** | `ui/badge.tsx` | Native | Status badge with variant styling (default, secondary, destructive, outline) |
| **Button** | `ui/button.tsx` | Native | Button with variants (default, destructive, outline, secondary, ghost, link) and sizes (default, sm, lg, icon) |
| **Card** | `ui/card.tsx` | Native | Content card with Header, Title, Description, Content, and Footer sub-components |
| **Checkbox** | `ui/checkbox.tsx` | `@radix-ui/react-checkbox` | Accessible checkbox with indeterminate state support |
| **Dialog** | `ui/dialog.tsx` | `@radix-ui/react-dialog` | Modal dialog with overlay, title, description, and close button |
| **DropdownMenu** | `ui/dropdown-menu.tsx` | `@radix-ui/react-dropdown-menu` | Dropdown menu with items, separators, and sub-menus |
| **Input** | `ui/input.tsx` | Native | Styled text input with consistent sizing and focus states |
| **Label** | `ui/label.tsx` | `@radix-ui/react-label` | Form label with proper accessibility attributes |
| **Popover** | `ui/popover.tsx` | `@radix-ui/react-popover` | Floating popover panel anchored to a trigger element |
| **ScrollArea** | `ui/scroll-area.tsx` | `@radix-ui/react-scroll-area` | Custom scrollbar container with cross-browser consistency |
| **Select** | `ui/select.tsx` | `@radix-ui/react-select` | Dropdown select with search, groups, and custom rendering |
| **Separator** | `ui/separator.tsx` | `@radix-ui/react-separator` | Horizontal or vertical divider line |
| **Sheet** | `ui/sheet.tsx` | `@radix-ui/react-dialog` | Side panel (drawer) that slides in from left, right, top, or bottom |
| **Sonner** | `ui/sonner.tsx` | `sonner` | Toast notification container with stacking and auto-dismiss |
| **Switch** | `ui/switch.tsx` | `@radix-ui/react-switch` | Toggle switch for boolean settings |
| **Tabs** | `ui/tabs.tsx` | `@radix-ui/react-tabs` | Tab navigation with content panels |
| **Textarea** | `ui/textarea.tsx` | Native | Multi-line text input with auto-resize capability |
| **Tooltip** | `ui/tooltip.tsx` | `@radix-ui/react-tooltip` | Hover tooltip with configurable delay and positioning |

## 3. Animation Components

| Component | File | Description |
|:---|:---|:---|
| **AnimatedCounter** | `animations/AnimatedCounter.tsx` | Number counter with easing animation |
| **KineticText** | `animations/KineticText.tsx` | Character-by-character text animation effects |
| **MicroInteractions** | `animations/MicroInteractions.tsx` | Small-scale hover and click feedback animations |
| **ParticleBackground** | `animations/ParticleBackground.tsx` | Canvas-based floating particle system |
| **ScrollReveal** | `animations/ScrollReveal.tsx` | Intersection Observer-based reveal-on-scroll animation |
