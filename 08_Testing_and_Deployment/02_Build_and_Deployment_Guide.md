# Build and Deployment Guide

This document provides comprehensive instructions for building, configuring, and deploying the Rasid National Platform. The guide is based on reverse engineering of the deployed application and its runtime configuration.

## 1. Prerequisites

### 1.1. Required Software

| Software | Version | Purpose |
|:---|:---|:---|
| **Node.js** | 22.x or later | JavaScript runtime for server and build tools |
| **npm** or **pnpm** | Latest | Package manager for dependency installation |
| **MySQL** or **TiDB** | 8.x / 7.x | Relational database engine |
| **Git** | Latest | Version control |

### 1.2. Required Accounts and Services

| Service | Purpose |
|:---|:---|
| **Manus Platform** | Cloud hosting and deployment (primary deployment target) |
| **Manus CDN** | File storage for media uploads (images, videos, documents) |
| **SMTP Server** | Email delivery for password resets and weekly reports |

## 2. Local Development Setup

### 2.1. Clone the Repository

```bash
git clone <repository-url>
cd rasid-platform
```

### 2.2. Install Dependencies

```bash
npm install
# or
pnpm install
```

### 2.3. Configure Environment Variables

Create a `.env` file in the project root with the following variables:

```env
# Database Configuration
DATABASE_URL=mysql://username:password@localhost:3306/rasid_db

# Authentication
JWT_SECRET=your-secure-jwt-secret-key-minimum-32-characters
SESSION_SECRET=your-secure-session-secret-key

# Application Settings
APP_TITLE=منصة راصد الوطنية
APP_LOCALE=ar-SA
APP_DIRECTION=rtl

# File Storage (Manus CDN)
MANUS_CDN_URL=https://files.manuscdn.com

# SMTP Configuration (optional for local development)
SMTP_HOST=smtp.example.com
SMTP_PORT=587
SMTP_USER=noreply@example.com
SMTP_PASS=smtp-password
SMTP_FROM=noreply@example.com
SMTP_SECURE=false
```

### 2.4. Initialize the Database

```bash
# Generate database migrations from Drizzle schema
npx drizzle-kit generate

# Apply migrations to the database
npx drizzle-kit push

# (Optional) Seed the database with initial data
npm run db:seed
```

### 2.5. Create the Admin User

After database initialization, create the root administrator account:

```bash
npm run create-admin -- \
  --username MRUHAILY \
  --password 15001500 \
  --name "Muhammed ALRuhaily" \
  --email prog.muhammed@gmail.com \
  --mobile +966553445533 \
  --displayName "Admin Rasid System"
```

Alternatively, the admin user can be created directly in the database:

```sql
INSERT INTO users (openId, name, email, role, username, displayName, mobile, loginMethod, isActive)
VALUES ('local_MRUHAILY', 'Muhammed ALRuhaily', 'prog.muhammed@gmail.com', 'admin', 'MRUHAILY', 'Admin Rasid System', '+966553445533', 'local', true);
```

### 2.6. Start the Development Server

```bash
npm run dev
```

This starts both the Vite development server (frontend) and the tRPC server (backend) with hot module replacement enabled. The application will be available at `http://localhost:5000`.

## 3. Production Build

### 3.1. Build the Application

```bash
npm run build
```

This command:
1. Compiles TypeScript source files
2. Bundles the React frontend with Vite (output to `dist/public/`)
3. Bundles the Node.js backend (output to `dist/`)
4. Generates optimized production assets with content hashing

### 3.2. Build Output Structure

```
dist/
├── public/
│   ├── assets/
│   │   ├── index-CCVI1ym-.js      # Main application bundle (~2.1 MB)
│   │   └── index-BxPuHNBZ.css     # Compiled TailwindCSS styles
│   └── index.html                  # Entry HTML with runtime config
└── server.js                       # Compiled backend server
```

### 3.3. Verify the Build

```bash
npm run preview
```

This starts a local preview server serving the production build.

## 4. Deployment

### 4.1. Manus Platform Deployment (Primary)

The Rasid National Platform is designed for deployment on the Manus Platform, which provides:

- Automatic SSL/TLS certificate management
- CDN-based static asset serving
- Managed database connections
- Environment variable management
- Zero-downtime deployments

**Deployment Steps:**

1. Connect the Git repository to the Manus Platform
2. Configure environment variables in the Manus dashboard
3. Set the build command: `npm run build`
4. Set the start command: `node dist/server.js`
5. Configure the custom domain: `www.rasid.vip`
6. Deploy

### 4.2. Docker Deployment (Alternative)

Create a `Dockerfile` for containerized deployment:

```dockerfile
FROM node:22-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

FROM node:22-alpine AS runner
WORKDIR /app
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/package.json ./

EXPOSE 5000
ENV NODE_ENV=production
CMD ["node", "dist/server.js"]
```

Build and run:

```bash
docker build -t rasid-platform .
docker run -p 5000:5000 --env-file .env rasid-platform
```

### 4.3. Reverse Proxy Configuration (Nginx)

For production deployments behind Nginx:

```nginx
server {
    listen 80;
    server_name www.rasid.vip rasid.vip;
    return 301 https://$server_name$request_uri;
}

server {
    listen 443 ssl http2;
    server_name www.rasid.vip;

    ssl_certificate /etc/ssl/certs/rasid.vip.crt;
    ssl_certificate_key /etc/ssl/private/rasid.vip.key;

    location / {
        proxy_pass http://localhost:5000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_cache_bypass $http_upgrade;
    }

    location /assets/ {
        proxy_pass http://localhost:5000;
        expires 1y;
        add_header Cache-Control "public, immutable";
    }
}
```

## 5. Database Management

### 5.1. Migrations

```bash
# Generate a new migration after schema changes
npx drizzle-kit generate

# Apply pending migrations
npx drizzle-kit push

# View migration status
npx drizzle-kit status

# Open Drizzle Studio for database inspection
npx drizzle-kit studio
```

### 5.2. Backup and Restore

```bash
# Backup
mysqldump -u username -p rasid_db > backup_$(date +%Y%m%d).sql

# Restore
mysql -u username -p rasid_db < backup_20260213.sql
```

## 6. Post-Deployment Verification

After deployment, verify the following:

| Check | Method | Expected Result |
|:---|:---|:---|
| Homepage loads | Visit `https://www.rasid.vip/` | Landing page with latest content |
| API responds | `curl https://www.rasid.vip/api/trpc/news.list` | JSON response with news data |
| Authentication works | Login with admin credentials | Redirect to admin dashboard |
| CDN files accessible | Check image URLs in news articles | Images load from manuscdn.com |
| SMTP configured | Send test email from `/smtp-settings` | Email received at test address |
| SSL certificate valid | Check browser padlock icon | Valid certificate for rasid.vip |

## 7. Monitoring and Maintenance

### 7.1. Health Checks

Monitor the following endpoints:

- `GET /api/trpc/news.list` — Verifies API and database connectivity
- `GET /` — Verifies frontend serving

### 7.2. Log Management

Application logs are output to stdout/stderr and can be captured by the hosting platform's log management system. Key log events to monitor:

- Authentication failures (potential brute-force attacks)
- Database connection errors
- SMTP delivery failures
- Unhandled exceptions

### 7.3. Regular Maintenance Tasks

| Task | Frequency | Description |
|:---|:---|:---|
| Database backup | Daily | Automated backup of MySQL/TiDB database |
| Dependency updates | Monthly | Review and update npm dependencies |
| Security audit | Quarterly | Run `npm audit` and review findings |
| Performance review | Quarterly | Review analytics and identify bottlenecks |
| SSL certificate renewal | Before expiry | Renew SSL certificate (automated with Let's Encrypt) |
