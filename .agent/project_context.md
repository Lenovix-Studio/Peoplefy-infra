# Peoplefy Project Context

## Overview
Peoplefy is a full-stack web application. Based on the name, it is likely a human resources (HR) or people management system. The project is structured as a monorepo with separate directories for `backend`, `frontend`, and `infra`.

## Tech Stack

### Backend (`/backend`)
- **Framework:** NestJS (v12)
- **Runtime:** Bun
- **Language:** TypeScript
- **Database ORM:** Prisma (v7)
- **Key Features:** Uses Bun's native environment variables handling (`--env-file`) and execution. Prisma is used for database schema management and queries.

### Frontend (`/frontend`)
- **Framework:** Next.js (v16)
- **UI Library:** React (v19)
- **Language:** TypeScript
- **Styling & Components:** 
  - Tailwind CSS (v4)
  - shadcn/ui
  - @base-ui/react
  - Icons via `lucide-react` and `react-icons`
- **Other:** Uses modern date formatting (`date-fns`) and UI elements like `react-day-picker`.

### Infrastructure (`/infra`)
- **Containerization:** Docker Compose
- **Database:** PostgreSQL 17 (Alpine image)
- **Environments:** The `docker-compose.yml` defines two database services:
  - `postgres-dev` (port 6040)
  - `postgres-prod` (port 6041)
- **Data Persistence:** Database volumes are mounted locally to `infra/data/postgres-dev` and `infra/data/postgres-prod`.

## Frontend Coding Conventions
- **Component Architecture:**
  - Pages (`app/**/page.tsx`) should primarily act as **Server Components**, handling initial data fetching (e.g., `async function SettingsPage()`).
  - Interactive UI elements must be extracted into **Client Components** (`"use client"`) and placed in the `components/` directory (e.g., `components/settings/common-codes-manager.tsx`).
- **Types Extraction:** Shared interfaces and types (like `CommonCodeType`) must be placed in a dedicated `types/` folder (e.g., `types/common-code.ts`) instead of keeping them tightly coupled inside component files.
- **Environment Variables:** Must be defined in `.env` with the `NEXT_PUBLIC_` prefix if they need to be accessed by Client Components, and usually exported via a centralized constant file (like `constant/variable.ts`).
