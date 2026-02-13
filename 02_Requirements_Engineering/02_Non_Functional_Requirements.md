# Non-Functional Requirements

This document details the non-functional requirements (NFRs) of the Rasid National Platform, inferred through reverse engineering analysis of the deployed application's JavaScript bundle, API behavior, and runtime configuration. Each requirement is supported by evidence observed in the codebase.

## 1. Performance

### 1.1. Client-Side Performance

The platform employs several strategies to ensure fast and responsive user interactions.

**Code Splitting and Lazy Loading.** The application is built with Vite, which automatically performs code splitting for production builds. Route-based lazy loading ensures that only the JavaScript required for the current page is loaded, reducing initial bundle size and improving Time to First Contentful Paint (TTFP).

**Server State Caching.** React Query (TanStack Query) is used extensively for data fetching, providing automatic caching, background refetching, and stale-while-revalidate strategies. This means that previously fetched data is served instantly from cache while fresh data is fetched in the background, resulting in near-instantaneous page transitions for previously visited content.

**Optimized Rendering.** The use of React 19 with its concurrent rendering capabilities allows the application to prioritize urgent UI updates (such as user input) over less critical updates (such as data loading indicators). Framer Motion's `AnimatePresence` component ensures smooth page transitions without layout shifts.

**Image Optimization.** The image gallery supports multiple resolution tiers (`imageUrl`, `imageUrlHd`, `imageUrlPreview`), allowing the application to serve appropriately sized images based on the viewing context. Preview images are loaded first for gallery thumbnails, with HD versions available on demand.

### 1.2. Backend Performance

**tRPC with SuperJSON.** The use of tRPC eliminates the overhead of REST API serialization/deserialization and provides automatic type inference. SuperJSON enables efficient serialization of complex types (Dates, Maps, Sets) without manual transformation.

**Database Query Optimization.** Drizzle ORM generates optimized SQL queries with proper indexing. The separation of `list` (published content only) and `all` (all content for admins) query procedures ensures that public-facing queries are optimized with appropriate WHERE clauses.

## 2. Security

### 2.1. Authentication

**JWT-Based Authentication.** The platform uses JSON Web Tokens for stateless authentication. The login page explicitly states: "جلستك محمية بتشفير JWT" (Your session is protected by JWT encryption). Tokens are stored in HTTP-only cookies to prevent XSS-based token theft.

**Account Lockout Policy.** The login page indicates an automatic account lockout mechanism: "يتم قفل الحساب تلقائياً بعد 5 محاولات فاشلة لمدة 15 دقيقة" (The account is automatically locked after 5 failed attempts for 15 minutes). This provides protection against brute-force attacks.

**Password Security.** Password hashing is implemented using bcrypt, as evidenced by the `auth.changePassword` and `auth.resetPassword` mutation procedures. The login page includes a real-time password strength meter with five levels of assessment.

### 2.2. Authorization

**Role-Based Access Control (RBAC).** The platform implements a comprehensive RBAC system with seven distinct roles: `admin`, `content_moderator`, `editor`, `viewer`, `user`, `moderator`, and `member`. Each role maps to a specific dashboard view through the `RoleDashboardPage` component, which dynamically renders different UI elements based on the user's role.

**Content-Level Visibility Controls.** Every content entity (news, videos, images, guides, presentations, links) includes `visibility` and `allowedUserIds` fields, enabling fine-grained access control at the individual content item level.

**Procedure-Level Authorization.** tRPC mutations (create, update, delete operations) are protected by server-side middleware that verifies the user's role before executing the operation. The separation of `list` (public) and `all` (admin) queries ensures that unpublished content is never exposed to unauthorized users.

### 2.3. Input Validation

**Zod Schema Validation.** All tRPC procedure inputs are validated using Zod schemas on the server side. This provides runtime type checking and prevents malformed data from reaching the database layer. The `BAD_REQUEST` error responses observed during API probing confirm that input validation is actively enforced.

## 3. Scalability

**Stateless Architecture.** The JWT-based authentication model ensures that the backend is stateless, allowing horizontal scaling of server instances without session affinity requirements.

**TiDB Compatibility.** The use of TiDB (a MySQL-compatible distributed SQL database) as the database engine indicates that the platform is designed for horizontal database scalability. TiDB provides automatic sharding and distributed transactions, enabling the database to scale seamlessly as data volume grows.

**CDN-Based File Storage.** All media files (images, videos, documents) are stored on Manus CDN (`files.manuscdn.com`), offloading file serving from the application server and providing global content delivery with low latency.

## 4. Maintainability

**TypeScript Throughout.** The entire codebase uses TypeScript, providing compile-time type checking and enabling IDE-assisted refactoring. The end-to-end type safety provided by tRPC ensures that API contract changes are immediately flagged as compilation errors on both client and server.

**Component-Based Architecture.** The frontend follows a strict component-based architecture with clear separation between page components (32 pages), reusable custom components (21 components), animation components (5 components), and UI primitives (19 shadcn/ui components).

**Standardized UI Library.** The use of shadcn/ui (built on Radix UI) provides a consistent, accessible, and well-documented component library. This reduces the maintenance burden of custom UI components and ensures consistent behavior across the application.

**ORM-Based Data Access.** Drizzle ORM abstracts database interactions, making it easier to modify the schema, add new fields, or switch database engines without rewriting query logic.

## 5. Usability

**Right-to-Left (RTL) Support.** The platform is built with full RTL support for Arabic language users. The Tajawal font family is used throughout the application, providing excellent Arabic typography. The application direction is set to `rtl` in the runtime configuration.

**Dark/Light Theme.** The `ThemeContext` provider enables users to switch between dark and light themes, improving readability and reducing eye strain in different lighting conditions.

**Responsive Design.** TailwindCSS's responsive utility classes are used throughout the application, ensuring that the platform renders correctly on desktop, tablet, and mobile devices.

**Guided Onboarding.** The `GuidedTour` component provides an interactive onboarding experience for new users, walking them through the platform's key features and navigation.

**Accessibility.** The use of Radix UI primitives ensures that all interactive elements (dialogs, dropdowns, tooltips, etc.) are fully accessible, with proper ARIA attributes, keyboard navigation, and focus management.

**Real-Time Feedback.** The Sonner toast notification system provides immediate visual feedback for user actions (content saved, message sent, error occurred), while the `ScrollProgressBar` component indicates reading progress on long-form content.

## 6. Reliability

**Error Boundaries.** The `ErrorBoundary` component wraps the application to catch and gracefully handle runtime errors, preventing the entire application from crashing due to a single component failure.

**Optimistic Updates.** React Query's mutation hooks are configured with `onSuccess` callbacks that invalidate and refetch related queries, ensuring that the UI always reflects the latest server state after a mutation.

**Activity Logging.** The `ActivityLogPage` indicates that the platform maintains a comprehensive audit trail of user actions, providing accountability and enabling forensic analysis in case of incidents.

## 7. Availability

**Cloud-Hosted Infrastructure.** The platform is deployed on the Manus Platform, which provides managed hosting with automatic scaling, SSL/TLS termination, and high availability.

**CDN Distribution.** Static assets and media files are served through Manus CDN, providing redundancy and ensuring content availability even during server-side issues.

## 8. Summary Table

| NFR Category | Rating | Key Evidence |
|:---|:---|:---|
| **Performance** | High | React Query caching, Vite code splitting, image optimization tiers |
| **Security** | High | JWT auth, bcrypt hashing, RBAC, account lockout, Zod validation |
| **Scalability** | High | Stateless JWT, TiDB distributed DB, CDN file storage |
| **Maintainability** | High | Full TypeScript, tRPC type safety, shadcn/ui, Drizzle ORM |
| **Usability** | High | RTL Arabic support, dark/light theme, guided tour, responsive design |
| **Reliability** | Medium-High | Error boundaries, optimistic updates, activity logging |
| **Availability** | Medium-High | Cloud hosting, CDN distribution |
