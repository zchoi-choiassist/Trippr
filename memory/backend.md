# Backend Memory

> Patterns, preferences, and learnings for the Trippr backend.
> This file is a living document updated as the project evolves.

## Architecture

- **Runtime**: Next.js API Routes / Route Handlers (TypeScript)
- **Validation**: Zod schemas for all request/response payloads
- **Auth**: NextAuth.js (Google OAuth, email/password)
- **Response Shape**: `{ data, error, meta }` on all endpoints

## API Patterns

_To be populated as endpoints are built._

## External Integrations

- **Google Maps API**: Saved lists import, place details, geocoding
- **Social Media APIs**: Post ingestion for trip inspiration (platforms TBD)
- **Research/Recommendation Engine**: Personalized suggestion pipeline (design TBD)

## Conventions

- RESTful endpoint naming
- Standard HTTP status codes for errors
- Input validation at the boundary; trust internal code
- Service layer pattern: Route Handler -> Service -> Repository/Prisma

## Learnings

_To be populated as the project progresses._

## Decisions Log

| Date | Decision | Rationale |
|------|----------|-----------|
| 2026-02-21 | Next.js Route Handlers for API | Unified deployment, shared types between frontend and backend |
| 2026-02-21 | Zod for validation | Runtime type safety at API boundaries; pairs well with TypeScript |
