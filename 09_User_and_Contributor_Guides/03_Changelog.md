# Changelog

All notable changes to the Rasid National Platform will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2026-02-13

### Added

#### Core Platform
- Full-stack TypeScript application built with React 19, Vite 6, TailwindCSS, and tRPC 11
- Right-to-left (RTL) Arabic language support with Tajawal font family
- Dark/light theme toggle with localStorage persistence
- Responsive design for desktop, tablet, and mobile devices
- Guided onboarding tour for new users
- Global search functionality across all content types
- Scroll progress bar for long-form content reading

#### Authentication and Authorization
- JWT-based authentication with HTTP-only cookie storage
- Local login with username and password
- Password strength meter with five assessment levels
- Account lockout after 5 failed login attempts (15-minute duration)
- Password reset via email with secure token
- Profile management with avatar upload
- Role-based access control (RBAC) with 7 distinct roles: admin, content_moderator, editor, viewer, user, moderator, member
- Role-specific dashboard views

#### Content Management — News
- News article creation with Tiptap rich text editor
- Cover image upload to Manus CDN
- Article categories and tagging
- Draft, published, and archived status lifecycle
- Content approval workflow (submit → review → approve/reject)
- Scheduled publication with future date/time
- Manual sort order control
- Visibility controls (public, members-only, restricted to specific users)

#### Content Management — Videos
- Video content management with multiple quality tiers (standard, HD, preview)
- Thumbnail image support
- Duration and file size metadata
- Playback and download permission controls (standard and HD)
- Content approval workflow (same as news)
- Scheduled publication support

#### Content Management — Images
- Image gallery with album organization
- Multiple resolution support (standard, HD, preview)
- Image metadata (dimensions, file size, MIME type)
- Download permission controls (standard and HD)
- Visibility controls

#### Content Management — Guides
- Document and guide repository
- Support for multiple file types (PDF, DOCX, etc.)
- Guide type classification
- Category organization
- Download permission controls

#### Content Management — Presentations
- Presentation file management with slide count metadata
- Thumbnail generation for cover slides
- Fullscreen presentation viewer with keyboard navigation
- Presentation toolbar with slide counter
- Member-only access option
- Download permission controls

#### Content Management — Links
- Curated external link directory
- Icon support for visual identification
- Category organization
- Manual sort order control

#### Community Features
- Public guestbook with moderation (submit → approve)
- Content bookmarking system with toggle functionality
- Like button for content engagement
- Comments section on content items
- Tag-based content organization with color-coded tags

#### Internal Communication
- Direct messaging between users
- Broadcast messaging from administrators to all users
- Message inbox and sent folders
- Read/unread status tracking
- Real-time notification system with bell indicator
- Unread notification count badge

#### Administration
- Admin dashboard with content statistics (news, videos, images, guides, presentations, guestbook, users, links, member files)
- User management (create, edit roles, activate/deactivate)
- Comprehensive analytics dashboard with Recharts visualizations:
  - Content overview statistics
  - Activity by day
  - User registrations by month
  - Content creation by month
  - Top liked content
  - Bookmarks by type
  - Comments by month
  - Likes by type
  - Recent activity feed
- PDF report generation from analytics data
- SMTP email configuration with test email functionality
- Content scheduling management (view scheduled, publish now, change status)
- Content display order management (drag-and-drop reordering)
- Weekly report configuration (day, time, recipients)
- Activity logging and audit trail

#### UI/UX
- 19 shadcn/ui components built on Radix UI primitives (Avatar, Badge, Button, Card, Checkbox, Dialog, DropdownMenu, Input, Label, Popover, ScrollArea, Select, Separator, Sheet, Sonner, Switch, Tabs, Textarea, Tooltip)
- 5 animation components (AnimatedCounter, KineticText, MicroInteractions, ParticleBackground, ScrollReveal)
- Page transition animations with Framer Motion
- Floating particle decorative backgrounds
- Toast notifications via Sonner
- Media viewer modal with zoom and navigation
- Error boundary for graceful error handling

#### Technical Infrastructure
- tRPC API with 22 routers, 48 query procedures, and 47 mutation procedures
- Drizzle ORM with MySQL/TiDB database
- SuperJSON serialization for type-safe data transfer
- React Query (TanStack Query) for server state management
- Wouter for lightweight client-side routing
- Manus CDN integration for file storage
- Zod schema validation on all API inputs
- bcrypt password hashing
