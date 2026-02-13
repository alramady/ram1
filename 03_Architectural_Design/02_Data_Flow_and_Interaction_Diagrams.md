# Data Flow and Interaction Diagrams

This document traces the execution paths and data flows for five core use cases of the Rasid National Platform. Each use case is illustrated with a Mermaid.js sequence diagram and accompanied by a detailed explanation of the interaction between system components.

## 1. User Authentication (Login)

The login flow demonstrates the JWT-based authentication mechanism, including account lockout protection after failed attempts.

```mermaid
sequenceDiagram
    participant U as User (Browser)
    participant R as React App
    participant T as tRPC Client
    participant S as tRPC Server
    participant M as Auth Middleware
    participant DB as MySQL/TiDB

    U->>R: Enter credentials (userId, password)
    R->>R: Client-side validation (non-empty fields)
    R->>T: auth.localLogin mutation
    T->>S: POST /api/trpc/auth.localLogin
    S->>M: Check account lockout status
    M->>DB: SELECT failed_attempts, locked_until FROM users
    DB-->>M: Account status
    alt Account is locked
        M-->>S: Error: Account locked (15 min)
        S-->>T: TRPCError (FORBIDDEN)
        T-->>R: Error response
        R-->>U: Display lockout message
    else Account is active
        M->>DB: SELECT user WHERE username = ?
        DB-->>M: User record
        M->>M: bcrypt.compare(password, hashedPassword)
        alt Password matches
            M->>M: Generate JWT token
            M->>DB: UPDATE lastSignedIn, reset failed_attempts
            M-->>S: { success: true, user: {...} }
            S-->>T: Set-Cookie: jwt=token (HttpOnly)
            T-->>R: Success response with user data
            R->>R: Update React Query cache (auth.me)
            R-->>U: Redirect to dashboard
        else Password incorrect
            M->>DB: INCREMENT failed_attempts
            alt failed_attempts >= 5
                M->>DB: SET locked_until = NOW() + 15min
            end
            M-->>S: Error: Invalid credentials
            S-->>T: TRPCError (UNAUTHORIZED)
            T-->>R: Error response
            R-->>U: Display error message
        end
    end
```

The authentication flow begins when the user submits their credentials through the `LoginPage` component. The React application performs basic client-side validation before dispatching the `auth.localLogin` tRPC mutation. On the server side, the auth middleware first checks whether the account is currently locked due to excessive failed attempts. If the account is active, the middleware retrieves the user record from the database and compares the submitted password against the stored bcrypt hash. Upon successful authentication, a JWT token is generated and set as an HTTP-only cookie, and the user is redirected to their role-appropriate dashboard.

## 2. Content Creation and Approval Workflow

This use case illustrates the complete lifecycle of a news article, from creation by an Editor through approval by a Content Moderator to publication.

```mermaid
sequenceDiagram
    participant E as Editor
    participant R as React App
    participant T as tRPC Client
    participant S as tRPC Server
    participant DB as MySQL/TiDB
    participant CDN as Manus CDN
    participant CM as Content Moderator
    participant N as Notification System

    E->>R: Create news article (RichTextEditor)
    E->>R: Upload cover image
    R->>CDN: Upload image file
    CDN-->>R: Image URL (manuscdn.com/...)
    R->>T: news.create mutation
    T->>S: POST /api/trpc/news.create
    S->>S: Validate input (Zod schema)
    S->>S: Check user role (editor+)
    S->>DB: INSERT INTO news (status='draft', approvalStatus='pending')
    DB-->>S: New article ID
    S->>T: approval.submitNews mutation
    T->>S: POST /api/trpc/approval.submitNews
    S->>DB: UPDATE news SET submittedBy = editorId
    S->>N: Create notification for moderators
    N->>DB: INSERT INTO notifications
    S-->>R: Success response
    R-->>E: "Article submitted for approval"

    Note over CM: Content Moderator receives notification

    CM->>R: Open Approval Queue (/approval)
    R->>T: approval.pendingNews query
    T->>S: GET /api/trpc/approval.pendingNews
    S->>DB: SELECT * FROM news WHERE approvalStatus='pending'
    DB-->>S: Pending articles list
    S-->>R: Pending articles data
    R-->>CM: Display pending articles

    CM->>R: Review and approve article
    R->>T: approval.reviewNews mutation
    T->>S: POST /api/trpc/approval.reviewNews
    S->>DB: UPDATE news SET approvalStatus='approved', reviewedBy=moderatorId, isPublished=true
    S->>N: Notify editor of approval
    S-->>R: Success response
    R-->>CM: "Article approved and published"
```

The content creation workflow demonstrates the platform's multi-step approval process. An Editor uses the Tiptap-based `RichTextEditor` to compose an article, uploads a cover image to Manus CDN, and submits the article for review. The article is stored in the database with a `draft` status and `pending` approval status. A notification is sent to Content Moderators, who can review the article through the dedicated Approval Queue page. Upon approval, the article's status is updated to `approved` and `isPublished` is set to `true`, making it visible on the public news listing.

## 3. Content Browsing and Interaction

This use case shows how a public user browses news content and interacts with it through bookmarking and commenting.

```mermaid
sequenceDiagram
    participant U as User (Browser)
    participant R as React App
    participant RQ as React Query Cache
    participant T as tRPC Client
    participant S as tRPC Server
    participant DB as MySQL/TiDB

    U->>R: Navigate to /news
    R->>RQ: Check cache for news.list
    alt Cache miss or stale
        RQ->>T: news.list query
        T->>S: GET /api/trpc/news.list
        S->>DB: SELECT * FROM news WHERE isPublished=true ORDER BY sortOrder
        DB-->>S: Published news list
        S-->>T: News data (with superjson dates)
        T-->>RQ: Store in cache
    end
    RQ-->>R: News list data
    R-->>U: Render news cards with animations

    U->>R: Click on news article
    R->>R: Navigate to /news/:id (Wouter)
    R->>T: news.getById query
    T->>S: GET /api/trpc/news.getById?input={id}
    S->>DB: SELECT * FROM news WHERE id=? AND isPublished=true
    DB-->>S: Article data
    S-->>R: Article with full content
    R-->>U: Render article with ScrollProgressBar

    U->>R: Click bookmark button
    R->>T: bookmarks.toggle mutation
    T->>S: POST /api/trpc/bookmarks.toggle
    S->>DB: INSERT/DELETE FROM bookmarks
    DB-->>S: Updated bookmark status
    S-->>R: { isBookmarked: true }
    R->>RQ: Invalidate bookmarks.myBookmarks
    R-->>U: Update BookmarkButton state (filled icon)
```

The content browsing flow leverages React Query's caching mechanism for optimal performance. When a user navigates to the news listing, the application first checks the local cache for existing data. If the cache is empty or stale, a fresh query is dispatched to the tRPC server. The server retrieves only published articles, ordered by their configured sort order. When the user clicks on an article, the detail view is loaded with the full content, and the `ScrollProgressBar` component tracks reading progress. User interactions such as bookmarking trigger optimistic UI updates followed by server-side persistence.

## 4. Administrative Analytics Review

This use case demonstrates how an administrator accesses and reviews platform analytics.

```mermaid
sequenceDiagram
    participant A as Admin
    participant R as React App
    participant T as tRPC Client
    participant S as tRPC Server
    participant DB as MySQL/TiDB

    A->>R: Navigate to /analytics
    R->>R: Verify admin role (RBAC check)
    
    par Parallel Data Fetching
        R->>T: analytics.overview query
        T->>S: GET /api/trpc/analytics.overview
        S->>DB: SELECT COUNT(*) FROM news, videos, images, ...
        DB-->>S: Content counts
        S-->>R: { news: 18, videos: 6, images: 32, ... }
    and
        R->>T: analytics.activityByDay query
        T->>S: GET /api/trpc/analytics.activityByDay
        S->>DB: SELECT date, COUNT(*) GROUP BY date
        DB-->>S: Activity data
        S-->>R: Daily activity array
    and
        R->>T: analytics.userRegistrations query
        T->>S: GET /api/trpc/analytics.userRegistrations
        S->>DB: SELECT month, COUNT(*) FROM users GROUP BY month
        DB-->>S: Registration data
        S-->>R: Monthly registration array
    and
        R->>T: analytics.topLiked query
        T->>S: GET /api/trpc/analytics.topLiked
        S->>DB: SELECT content, like_count ORDER BY like_count DESC
        DB-->>S: Top liked content
        S-->>R: Top liked items
    end

    R->>R: Render Recharts visualizations
    R-->>A: Display analytics dashboard

    A->>R: Click "Generate Report"
    R->>T: analytics.generateReport mutation
    T->>S: POST /api/trpc/analytics.generateReport
    S->>S: Compile analytics data into report
    S-->>R: Report data
    R->>R: Generate PDF (PdfReportButton)
    R-->>A: Download PDF report
```

The analytics dashboard demonstrates parallel data fetching, where multiple tRPC queries are dispatched simultaneously to populate different sections of the dashboard. React Query manages these parallel requests efficiently, rendering each chart as its data becomes available. The `Recharts` library renders the data as interactive visualizations. Administrators can generate comprehensive PDF reports using the `PdfReportButton` component.

## 5. Internal Messaging

This use case illustrates the internal messaging system, including direct messaging and broadcast functionality.

```mermaid
sequenceDiagram
    participant S as Sender (Admin)
    participant R as React App
    participant T as tRPC Client
    participant SV as tRPC Server
    participant DB as MySQL/TiDB
    participant NS as Notification System
    participant RC as Recipient

    S->>R: Navigate to /messages
    R->>T: messages.users query
    T->>SV: GET /api/trpc/messages.users
    SV->>DB: SELECT id, name, displayName FROM users
    DB-->>SV: User list
    SV-->>R: Available recipients
    R-->>S: Display compose form with user list

    S->>R: Compose and send message
    R->>T: messages.send mutation
    T->>SV: POST /api/trpc/messages.send
    SV->>SV: Validate input (Zod)
    SV->>DB: INSERT INTO messages (senderId, recipientId, content)
    SV->>NS: Create notification for recipient
    NS->>DB: INSERT INTO notifications (userId=recipientId, type='message')
    SV-->>R: Success response
    R->>R: Invalidate messages.sent cache
    R-->>S: "Message sent successfully" (Sonner toast)

    Note over RC: Recipient receives real-time notification

    RC->>R: NotificationBell shows unread count
    R->>T: notifications.unreadCount query (polling)
    T->>SV: GET /api/trpc/notifications.unreadCount
    SV->>DB: SELECT COUNT(*) FROM notifications WHERE read=false
    SV-->>R: Unread count
    R-->>RC: Update NotificationBell badge

    RC->>R: Navigate to /messages
    R->>T: messages.inbox query
    T->>SV: GET /api/trpc/messages.inbox
    SV->>DB: SELECT * FROM messages WHERE recipientId=?
    SV-->>R: Inbox messages
    R-->>RC: Display inbox with new message

    RC->>R: Open and read message
    R->>T: messages.markRead mutation
    T->>SV: POST /api/trpc/messages.markRead
    SV->>DB: UPDATE messages SET read=true WHERE id=?
    R->>R: Invalidate messages.unreadCount cache
```

The messaging system provides both direct and broadcast communication capabilities. When an administrator composes a message, the `messages.users` query populates the recipient selector with all registered users. Upon sending, the message is persisted in the database and a notification is created for the recipient. The `NotificationBell` component polls for unread notification counts, providing near-real-time awareness of new messages. The `RealtimeNotifications` component may also provide WebSocket-based instant notifications, though this could not be fully confirmed through static analysis alone.
