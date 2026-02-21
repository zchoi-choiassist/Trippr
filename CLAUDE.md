# Trippr - Project Guide

## Project Overview

Trippr is a mobile-first web application that helps families and groups of friends organize trips. It provides hyper-personalized trip planning by integrating saved lists from Google Maps, social media posts, and independent research. Design cues are drawn from Airbnb's UI/UX patterns.

## Tech Stack

- **Frontend**: Next.js 14+ (App Router), React 18+, TypeScript, Tailwind CSS
- **Backend**: Next.js API Routes / Route Handlers, TypeScript
- **Database**: PostgreSQL with Prisma ORM
- **Authentication**: NextAuth.js (Google OAuth, email/password)
- **State Management**: Zustand for client state, React Query (TanStack Query) for server state
- **Testing**: Vitest (unit), Playwright (e2e), React Testing Library (component)
- **Deployment**: Vercel
- **CI/CD**: GitHub Actions

## Project Structure

```
/src
  /app              # Next.js App Router pages and layouts
  /components        # Reusable React components
    /ui              # Base UI primitives (buttons, inputs, cards)
    /features        # Feature-specific components
    /layouts         # Layout components (navigation, sidebars)
  /lib               # Shared utilities, helpers, constants
  /hooks             # Custom React hooks
  /services          # API client functions and external service integrations
  /types             # TypeScript type definitions and interfaces
  /styles            # Global styles and Tailwind config extensions
/prisma              # Prisma schema and migrations
/public              # Static assets (images, icons, fonts)
/docs                # Project documentation, PRDs, and plans
  /prds              # Product Requirement Documents
  /tickets           # Feature tickets
/memory              # Component memory files for patterns and learnings
/tests
  /unit              # Unit tests
  /e2e               # End-to-end tests
  /integration       # Integration tests
```

## Development Workflow

### Process
1. Every feature starts with a PRD in `/docs/prds/`
2. PRDs are broken into tickets in `/docs/tickets/`
3. Each ticket is implemented on a feature branch
4. All changes require tests before merging
5. Regression testing is performed after each feature merge

### Commands
```bash
npm run dev          # Start development server
npm run build        # Production build
npm run test         # Run all tests
npm run test:unit    # Run unit tests only
npm run test:e2e     # Run e2e tests only
npm run lint         # Lint the codebase
npm run db:migrate   # Run database migrations
npm run db:seed      # Seed the database
npm run db:studio    # Open Prisma Studio
```

## Code Conventions

### TypeScript
- Strict mode enabled; no `any` types unless absolutely necessary
- Use interfaces for object shapes, types for unions/intersections
- All function parameters and return types must be explicitly typed

### React / Next.js
- Functional components only; no class components
- Use Server Components by default; add `'use client'` only when needed
- Co-locate component-specific styles, tests, and types
- Naming: PascalCase for components, camelCase for hooks and utilities

### API Routes
- RESTful naming conventions
- All endpoints return consistent response shapes: `{ data, error, meta }`
- Input validation with Zod schemas
- Error responses use standard HTTP status codes

### Database
- All tables use UUID primary keys
- Timestamps: `created_at`, `updated_at` on every table
- Soft deletes where appropriate (`deleted_at` column)
- Prisma migrations committed to version control

### Testing
- Unit tests for all utility functions and hooks
- Component tests for interactive UI elements
- E2E tests for critical user flows (trip creation, itinerary management, sharing)
- Test files live alongside source files: `Component.test.tsx`

### Git
- Branch naming: `feature/<ticket-id>-short-description`
- Commit messages: conventional commits format (`feat:`, `fix:`, `chore:`, `docs:`, `test:`)
- PRs require passing CI checks before merge

## Memory Files

Component-specific patterns, preferences, and learnings are stored in `/memory/`:
- `frontend.md` - Frontend patterns, component conventions, UI decisions
- `backend.md` - API patterns, service architecture, integration notes
- `database.md` - Schema decisions, query patterns, migration notes

These files are living documents updated as the project evolves. A dedicated skill will define the write protocol for these files.

## Key Design Principles

1. **Mobile-first**: All UI designed for mobile viewports first, then scaled up
2. **Personalization**: Every recommendation and suggestion draws from user-connected data sources
3. **Collaborative**: Multi-user trip editing and decision-making are core to every feature
4. **Offline-capable**: Key trip data should be accessible without connectivity
5. **Airbnb-inspired**: Clean, spacious layouts with high-quality imagery and smooth interactions
