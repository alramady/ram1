# Rasid National Platform — منصة راصد الوطنية

## Comprehensive Technical Documentation Repository

This repository contains the complete technical documentation for the **Rasid National Platform** (منصة راصد الوطنية), generated through exhaustive reverse engineering and analysis of the deployed application at [www.rasid.vip](https://www.rasid.vip). It serves as the **single source of truth** for all technical, functional, and architectural aspects of the project.

---

## Executive Summary

The Rasid National Platform is a comprehensive digital content management and communication system built for government and national organizations in the Kingdom of Saudi Arabia. The platform consolidates six content types — news articles, videos, images, guides/documents, presentations, and curated links — into a unified, Arabic-first portal with full RTL support.

The platform is built on a modern full-stack TypeScript architecture featuring **React 19** with **Vite 6** on the frontend, **tRPC 11** for end-to-end type-safe API communication, **Drizzle ORM** with **MySQL/TiDB** for data persistence, and **TailwindCSS** with **shadcn/ui** for a polished, accessible user interface. The system implements a robust role-based access control model with seven user roles, a multi-step content approval workflow, internal messaging, comprehensive analytics, and automated weekly reporting.

| Metric | Value |
|:---|:---|
| **Source Files** | 80 (client-side) |
| **Page Components** | 32 |
| **Reusable Components** | 45 (21 custom + 19 shadcn/ui + 5 animation) |
| **tRPC Routers** | 22 |
| **API Procedures** | 95 (48 queries + 47 mutations) |
| **Database Tables** | 10+ |
| **User Roles** | 7 |
| **Production Bundle** | ~2.1 MB (minified) |

For the complete executive summary, see [01_Project_Overview/01_Executive_Summary.md](01_Project_Overview/01_Executive_Summary.md).

For the detailed technology inventory, see [01_Project_Overview/02_Project_Footprint.md](01_Project_Overview/02_Project_Footprint.md).

---

## Table of Contents

### 1. Project Overview

| Document | Description |
|:---|:---|
| [01_Executive_Summary.md](01_Project_Overview/01_Executive_Summary.md) | High-level overview of the platform's purpose, technology stack, and key capabilities |
| [02_Project_Footprint.md](01_Project_Overview/02_Project_Footprint.md) | Complete inventory of languages, frameworks, dependencies, configuration parameters, and file structure |
| [03_Inferred_Vision.md](01_Project_Overview/03_Inferred_Vision.md) | Analysis of the problem being solved, the solution approach, and the target audience |

### 2. Requirements Engineering

| Document | Description |
|:---|:---|
| [01_Functional_Requirements.md](02_Requirements_Engineering/01_Functional_Requirements.md) | Comprehensive catalog of all functional requirements, organized by user role and feature area |
| [02_Non_Functional_Requirements.md](02_Requirements_Engineering/02_Non_Functional_Requirements.md) | Performance, security, scalability, maintainability, usability, and reliability requirements with supporting evidence |

### 3. Architectural Design

| Document | Description |
|:---|:---|
| [01_Architectural_Blueprint.md](03_Architectural_Design/01_Architectural_Blueprint.md) | System architecture overview with Mermaid.js diagrams showing the N-tier architecture and component interactions |
| [02_Data_Flow_and_Interaction_Diagrams.md](03_Architectural_Design/02_Data_Flow_and_Interaction_Diagrams.md) | Sequence diagrams for 5 core use cases: authentication, content creation/approval, content browsing, analytics, and messaging |
| [03_Database_Schema_and_Design.md](03_Architectural_Design/03_Database_Schema_and_Design.md) | Complete database schema with ERD, table specifications, column details, and design pattern analysis |

### 4. Source Code Deep Dive

| Document | Description |
|:---|:---|
| [01_File_by_File_Analysis.md](04_Source_Code_Deep_Dive/01_File_by_File_Analysis.md) | Detailed analysis of every source file, including purpose, key components, and dependencies |
| [02_Class_and_Function_Ledger.md](04_Source_Code_Deep_Dive/02_Class_and_Function_Ledger.md) | Comprehensive inventory of all React components, their props, state management, and key functions |
| [03_API_Reference.md](04_Source_Code_Deep_Dive/03_API_Reference.md) | Complete tRPC API reference with all 95 procedures, input schemas, response formats, and error codes |

### 5. UI/UX Component Analysis

| Document | Description |
|:---|:---|
| [01_Page_and_Screen_Breakdown.md](05_UI_Component_Analysis/01_Page_and_Screen_Breakdown.md) | Analysis of all 32 pages with routes, purpose, component trees, and user workflows |
| [02_Component_Library.md](05_UI_Component_Analysis/02_Component_Library.md) | Catalog of all 45 reusable components with props tables, state management, and events |

### 6. Quality and Compliance

| Document | Description |
|:---|:---|
| [01_Code_Standards_Compliance_Report.md](06_Quality_and_Compliance/01_Code_Standards_Compliance_Report.md) | Code quality assessment including compliance score, major violations, and code smells |
| [02_Inline_Documentation_Audit.md](06_Quality_and_Compliance/02_Inline_Documentation_Audit.md) | Documentation coverage analysis with undocumented components list and improvement recommendations |

### 7. Security and Performance

| Document | Description |
|:---|:---|
| [01_Security_Vulnerability_Assessment.md](07_Security_and_Performance/01_Security_Vulnerability_Assessment.md) | Security analysis covering authentication, authorization, input validation, and OWASP Top 10 assessment |
| [02_Performance_Hotspot_Analysis.md](07_Security_and_Performance/02_Performance_Hotspot_Analysis.md) | Performance bottleneck identification in client-side rendering, API design, and database queries |

### 8. Testing and Deployment

| Document | Description |
|:---|:---|
| [01_Inferred_Testing_Strategy.md](08_Testing_and_Deployment/01_Inferred_Testing_Strategy.md) | Analysis of testing frameworks, test coverage, and recommended testing approach |
| [02_Build_and_Deployment_Guide.md](08_Testing_and_Deployment/02_Build_and_Deployment_Guide.md) | Step-by-step guide for local setup, production build, deployment, and maintenance |

### 9. User and Contributor Guides

| Document | Description |
|:---|:---|
| [01_End_User_Manual.md](09_User_and_Contributor_Guides/01_End_User_Manual.md) | Non-technical user guide with step-by-step instructions for all platform features |
| [02_Contributor_Guide.md](09_User_and_Contributor_Guides/02_Contributor_Guide.md) | Developer onboarding guide with coding standards, project structure, and PR process |
| [03_Changelog.md](09_User_and_Contributor_Guides/03_Changelog.md) | Version 1.0.0 changelog listing all features in Keep a Changelog format |

---

## Technology Stack

| Layer | Technology |
|:---|:---|
| **Frontend** | React 19, TypeScript, Vite 6, TailwindCSS, shadcn/ui (Radix UI) |
| **State Management** | React Query (TanStack Query), React Context |
| **API Layer** | tRPC 11 with SuperJSON serialization |
| **Backend** | Node.js 22, Express |
| **Database** | MySQL / TiDB with Drizzle ORM |
| **Authentication** | JWT (HTTP-only cookies), bcrypt |
| **File Storage** | Manus CDN (manuscdn.com) |
| **Hosting** | Manus Platform |
| **Rich Text** | Tiptap |
| **Charts** | Recharts |
| **Animations** | Framer Motion |
| **Routing** | Wouter |
| **Validation** | Zod |

---

## Analysis Methodology

This documentation was generated through a multi-phase reverse engineering process.

**Phase 1 — Reconnaissance.** The deployed application at `www.rasid.vip` was accessed and its HTML source, JavaScript bundles, and runtime configuration were extracted and analyzed.

**Phase 2 — Bundle Analysis.** The production JavaScript bundle (~2.1 MB) was decompiled and analyzed to extract source file paths, component names, route definitions, tRPC procedure names, and library dependencies.

**Phase 3 — API Discovery.** All 95 tRPC procedures were systematically discovered and probed. Authenticated sessions were established to access admin-only endpoints, and response schemas were documented from live API responses.

**Phase 4 — Data Analysis.** Live data from all API endpoints was collected and analyzed to infer database schema, content structures, user roles, and business rules.

**Phase 5 — Documentation Generation.** The collected intelligence was synthesized into this comprehensive documentation repository following the 9-phase analysis framework.

---

## Document Information

| Property | Value |
|:---|:---|
| **Generated** | February 13, 2026 |
| **Platform Version** | 1.0.0 (inferred) |
| **Analysis Target** | https://www.rasid.vip |
| **Total Documents** | 22 |
| **Total Sections** | 9 |

---

*This documentation repository was generated through automated reverse engineering analysis. While every effort has been made to ensure accuracy, some implementation details may differ from the actual source code due to the limitations of analyzing minified production bundles.*
