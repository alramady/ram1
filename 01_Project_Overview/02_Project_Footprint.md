# Project Footprint

## 1. Languages and Frameworks

The Rasid National Platform is built using a modern full-stack JavaScript/TypeScript ecosystem. The following table provides a comprehensive inventory of all programming languages, frameworks, and runtime environments identified through reverse engineering of the deployed application bundle.

| Category | Technology | Version | Purpose |
|:---|:---|:---|:---|
| **Primary Language** | TypeScript | 5.x | Type-safe development across frontend and backend |
| **Frontend Framework** | React | 19.x | Component-based UI rendering |
| **Build Tool** | Vite | 6.x | Fast development server and production bundling |
| **CSS Framework** | TailwindCSS | 3.x | Utility-first CSS styling |
| **UI Primitives** | Radix UI | Latest | Accessible, unstyled UI component primitives |
| **Component Library** | shadcn/ui | Latest | Pre-styled components built on Radix UI |
| **Backend Runtime** | Node.js | 22.x | Server-side JavaScript execution |
| **API Framework** | tRPC | 11.x | End-to-end typesafe API layer |
| **ORM** | Drizzle ORM | Latest | Type-safe SQL query builder and ORM |
| **Database** | MySQL / TiDB | 8.x / 7.x | Relational data storage |
| **Hosting Platform** | Manus Platform | N/A | Cloud hosting and deployment |

## 2. Dependency Graph

### 2.1. Frontend Dependencies

The frontend application relies on a rich ecosystem of React-compatible libraries. The following dependencies were identified through analysis of the production JavaScript bundle.

| Dependency | Category | Purpose |
|:---|:---|:---|
| `react` / `react-dom` | Core | React rendering engine |
| `wouter` | Routing | Lightweight client-side routing |
| `@tanstack/react-query` | Data Fetching | Server state management, caching, and synchronization |
| `@trpc/client` / `@trpc/react-query` | API Client | Type-safe tRPC client integration with React Query |
| `framer-motion` | Animation | Declarative animations and gestures |
| `@tiptap/react` / `@tiptap/starter-kit` | Rich Text | Rich text editor for content creation |
| `recharts` | Charting | Data visualization and chart rendering |
| `sonner` | Notifications | Toast notification system |
| `lucide-react` | Icons | SVG icon library |
| `@radix-ui/react-*` | UI Primitives | Dialog, Dropdown, Popover, Select, Tabs, Tooltip, etc. |
| `class-variance-authority` | Styling | Variant-based component styling |
| `clsx` / `tailwind-merge` | Styling | Conditional class name utilities |
| `date-fns` | Utilities | Date formatting and manipulation |
| `superjson` | Serialization | JSON serialization with type preservation for tRPC |

### 2.2. Backend Dependencies

| Dependency | Category | Purpose |
|:---|:---|:---|
| `@trpc/server` | API Server | tRPC server-side procedure definitions |
| `drizzle-orm` | ORM | Database schema definition and query building |
| `drizzle-kit` | ORM Tooling | Database migration management |
| `jsonwebtoken` | Authentication | JWT token generation and verification |
| `bcrypt` / `bcryptjs` | Security | Password hashing |
| `express` | HTTP Server | HTTP server framework (inferred) |
| `zod` | Validation | Schema validation for tRPC inputs |
| `nodemailer` | Email | SMTP email sending |

## 3. Configuration Parameters

The application utilizes environment-based configuration managed through the Manus Platform runtime. The following configuration parameters were identified from the application's runtime initialization script and bundle analysis.

| Parameter | Purpose | Source |
|:---|:---|:---|
| `DATABASE_URL` | MySQL/TiDB connection string | Environment variable |
| `JWT_SECRET` | Secret key for JWT token signing | Environment variable |
| `SESSION_SECRET` | Secret for session management | Environment variable |
| `MANUS_CDN_URL` | Base URL for file storage CDN | Runtime config (`manuscdn.com`) |
| `SMTP_HOST` | SMTP server hostname | Database settings table |
| `SMTP_PORT` | SMTP server port | Database settings table |
| `SMTP_USER` | SMTP authentication username | Database settings table |
| `SMTP_PASS` | SMTP authentication password | Database settings table |
| `APP_TITLE` | Application display title | Runtime config ("منصة راصد الوطنية") |
| `APP_LOCALE` | Application locale | Runtime config (`ar-SA`) |
| `APP_DIRECTION` | Text direction | Runtime config (`rtl`) |

## 4. File Structure Summary

The application follows a standard full-stack TypeScript project structure with clear separation between client and server code.

```
project-root/
├── client/
│   └── src/
│       ├── App.tsx                    # Main application with routing
│       ├── main.tsx                   # Entry point
│       ├── components/               # 21 reusable components
│       │   ├── animations/           # 5 animation components
│       │   └── ui/                   # 19 shadcn/ui components
│       ├── contexts/                 # 1 context provider (Theme)
│       └── pages/                    # 32 page components
├── server/
│   ├── routes/                       # tRPC router definitions
│   ├── db/                           # Drizzle ORM schema & migrations
│   └── middleware/                   # Auth & validation middleware
├── shared/
│   └── types/                        # Shared TypeScript types
├── package.json
├── vite.config.ts
├── tailwind.config.ts
├── tsconfig.json
└── drizzle.config.ts
```

## 5. Statistics

| Metric | Value |
|:---|:---|
| **Total Source Files (Client)** | 80 |
| **Page Components** | 32 |
| **Reusable UI Components** | 19 (shadcn/ui) |
| **Custom Components** | 21 |
| **Animation Components** | 5 |
| **Context Providers** | 1 |
| **tRPC Routers** | 22 |
| **tRPC Query Procedures** | 48 |
| **tRPC Mutation Procedures** | 47 |
| **Database Tables** | 10 |
| **User Roles** | 7 |
| **Client-Side Routes** | 33 |
| **Production Bundle Size** | ~2.1 MB (minified) |
