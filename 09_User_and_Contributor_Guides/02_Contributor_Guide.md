# Contributor Guide

This guide provides instructions for developers who wish to contribute to the Rasid National Platform. It covers development environment setup, coding standards, and the process for submitting changes.

## 1. Development Environment Setup

### 1.1. Prerequisites

Ensure the following software is installed on your development machine:

- **Node.js** 22.x or later (download from [nodejs.org](https://nodejs.org/))
- **npm** (included with Node.js) or **pnpm** (recommended for faster installs)
- **MySQL** 8.x or **TiDB** 7.x (for local database)
- **Git** (for version control)
- **VS Code** (recommended IDE with the following extensions):
  - ESLint
  - Prettier
  - Tailwind CSS IntelliSense
  - TypeScript and JavaScript Language Features

### 1.2. Initial Setup

```bash
# 1. Clone the repository
git clone <repository-url>
cd rasid-platform

# 2. Install dependencies
npm install

# 3. Copy the environment template
cp .env.example .env

# 4. Configure your local .env file (see Build and Deployment Guide)

# 5. Initialize the database
npx drizzle-kit push

# 6. Start the development server
npm run dev
```

The application will be available at `http://localhost:5000` with hot module replacement enabled for both frontend and backend changes.

## 2. Project Structure

Understanding the project structure is essential for effective contribution. The codebase follows a monorepo structure with clear separation between client and server code.

```
project-root/
├── client/                    # Frontend application
│   └── src/
│       ├── App.tsx            # Main app with routing definitions
│       ├── main.tsx           # React entry point
│       ├── components/        # Reusable components
│       │   ├── animations/    # Animation components
│       │   └── ui/            # shadcn/ui components
│       ├── contexts/          # React context providers
│       ├── hooks/             # Custom React hooks
│       ├── lib/               # Utility functions
│       └── pages/             # Page components (one per route)
├── server/                    # Backend application
│   ├── routes/                # tRPC router definitions
│   ├── db/                    # Database schema and migrations
│   │   ├── schema.ts          # Drizzle ORM schema definitions
│   │   └── migrations/        # SQL migration files
│   └── middleware/            # Authentication and validation
├── shared/                    # Shared types and utilities
│   └── types/                 # TypeScript type definitions
├── package.json
├── vite.config.ts             # Vite build configuration
├── tailwind.config.ts         # TailwindCSS configuration
├── tsconfig.json              # TypeScript configuration
└── drizzle.config.ts          # Drizzle ORM configuration
```

## 3. Coding Standards

### 3.1. TypeScript

- **Strict mode** is enabled. All code must pass TypeScript strict type checking.
- Use **explicit return types** for all exported functions.
- Prefer **interfaces** over type aliases for object shapes.
- Use **enums** sparingly; prefer union types (e.g., `'draft' | 'published' | 'archived'`).
- Never use `any` type. Use `unknown` when the type is truly unknown.

### 3.2. React Components

- Use **functional components** with hooks. Class components are not used in this project.
- Follow the **single responsibility principle**: each component should do one thing well.
- Place page components in `client/src/pages/` and reusable components in `client/src/components/`.
- Use **PascalCase** for component file names (e.g., `BookmarkButton.tsx`).
- Export components as **named exports** (not default exports).

### 3.3. Styling

- Use **TailwindCSS utility classes** for all styling. Avoid custom CSS files.
- Use the `cn()` utility (from `clsx` + `tailwind-merge`) for conditional class names.
- Follow the existing **RTL-first** approach: use logical properties (`ms-`, `me-`, `ps-`, `pe-`) instead of directional ones (`ml-`, `mr-`, `pl-`, `pr-`).
- Use **shadcn/ui components** for common UI elements. Do not create custom implementations of buttons, inputs, dialogs, etc.

### 3.4. API Development

- Define all API procedures in the appropriate **tRPC router** under `server/routes/`.
- Use **Zod schemas** for input validation on all mutations and parameterized queries.
- Follow the naming convention: `router.action` (e.g., `news.create`, `approval.reviewNews`).
- Separate **public queries** (`list`) from **admin queries** (`all`).
- Always check **user permissions** in mutation procedures.

### 3.5. Database

- Define all schema changes in `server/db/schema.ts` using **Drizzle ORM**.
- Generate migrations with `npx drizzle-kit generate` after schema changes.
- Never modify migration files after they have been committed.
- Include **appropriate indexes** for columns used in WHERE clauses and JOIN conditions.

### 3.6. Naming Conventions

| Element | Convention | Example |
|:---|:---|:---|
| Components | PascalCase | `BookmarkButton` |
| Files (components) | PascalCase.tsx | `BookmarkButton.tsx` |
| Files (utilities) | camelCase.ts | `formatDate.ts` |
| Functions | camelCase | `handleSubmit` |
| Variables | camelCase | `isLoading` |
| Constants | UPPER_SNAKE_CASE | `MAX_RETRY_ATTEMPTS` |
| tRPC Routers | camelCase | `weeklyReport` |
| tRPC Procedures | camelCase | `getById` |
| Database Tables | snake_case | `weekly_report_settings` |
| Database Columns | camelCase | `isPublished` |
| CSS Classes | kebab-case (Tailwind) | `bg-primary text-white` |

## 4. Development Workflow

### 4.1. Branching Strategy

The project follows a simplified Git Flow model:

- `main` — Production-ready code. Direct commits are not allowed.
- `develop` — Integration branch for features. Merges to `main` for releases.
- `feature/{name}` — Feature branches created from `develop`.
- `fix/{name}` — Bug fix branches created from `develop` or `main` (for hotfixes).

### 4.2. Creating a Feature Branch

```bash
git checkout develop
git pull origin develop
git checkout -b feature/add-comment-reactions
```

### 4.3. Making Changes

1. Write your code following the coding standards above.
2. Ensure TypeScript compilation passes: `npx tsc --noEmit`.
3. Test your changes locally by running the development server.
4. Verify that existing functionality is not broken.

### 4.4. Committing Changes

Follow the **Conventional Commits** specification:

```
<type>(<scope>): <description>

[optional body]
[optional footer]
```

Types: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `chore`.

Examples:
```
feat(news): add comment reactions feature
fix(auth): resolve account lockout timing issue
docs(api): update API reference for new endpoints
refactor(components): extract shared media viewer logic
```

### 4.5. Submitting a Pull Request

1. Push your branch to the remote repository.
2. Create a Pull Request targeting the `develop` branch.
3. Fill in the PR template with:
   - Description of changes
   - Screenshots (for UI changes)
   - Testing steps
   - Related issues
4. Request review from at least one team member.
5. Address review feedback and update the PR.
6. Once approved, the PR will be merged by a maintainer.

## 5. Adding New Features

### 5.1. Adding a New Content Type

To add a new content type (e.g., "podcasts"):

1. **Database Schema:** Add the table definition in `server/db/schema.ts`.
2. **tRPC Router:** Create `server/routes/podcasts.ts` with `list`, `all`, `create`, `update`, `delete` procedures.
3. **Register Router:** Add the new router to the main tRPC app router.
4. **Page Components:** Create `PodcastsPage.tsx` and `PodcastDetailPage.tsx` in `client/src/pages/`.
5. **Routing:** Add routes in `App.tsx`.
6. **Navigation:** Add menu items in `Navbar.tsx`.
7. **Dashboard:** Update `DashboardPage.tsx` with the new content count.

### 5.2. Adding a New UI Component

1. Check if **shadcn/ui** provides the component: `npx shadcn-ui add <component>`.
2. If custom, create the component in `client/src/components/`.
3. Define a clear **props interface** with TypeScript.
4. Use **TailwindCSS** for styling with `cn()` for conditional classes.
5. Ensure **RTL compatibility** using logical properties.

## 6. Troubleshooting

| Issue | Solution |
|:---|:---|
| Database connection error | Verify `DATABASE_URL` in `.env` and ensure MySQL is running |
| TypeScript compilation errors | Run `npx tsc --noEmit` and fix reported issues |
| Vite HMR not working | Clear browser cache and restart dev server |
| tRPC type errors | Run `npm run build` to regenerate type definitions |
| TailwindCSS classes not applying | Ensure the file path is included in `tailwind.config.ts` content array |
