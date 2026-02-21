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

## Deployment & Runtime

- **Platform**: Vercel — API routes run as serverless functions
- **Function timeout**: 60-300 seconds on Vercel Hobby (generous for SSR + Prisma + NextAuth)
- **Cold starts**: Serverless functions have cold starts; keep Prisma Client instantiation efficient (singleton pattern)
- **Middleware**: Runs on Vercel Edge Runtime — execution order matches Next.js docs exactly (unlike Netlify)
- **Environment variables**: Managed via Vercel dashboard; secrets never committed to repo
- **Preview deployments**: Every PR gets its own deployment URL — useful for testing API changes in isolation

## Learnings

- **10-second function timeout (Netlify free) was a dealbreaker** — SSR pages with Prisma queries + NextAuth session checks can easily exceed that during cold starts
- **Vercel's 60-300s timeout gives breathing room** for chained API calls (e.g., Google Maps API -> process -> Prisma write)
- **NextAuth.js session strategy matters for serverless**: JWT strategy avoids database hits on every request; database strategy requires connection pooling. Evaluate during auth implementation.
- **Service layer pattern is important for serverless**: Route Handler -> Service -> Prisma. Keeps handlers thin and testable; services can be reused across routes.
- **Vercel Functions run in a single region by default** — choose a region close to the database to minimize latency

## Decisions Log

| Date | Decision | Rationale |
|------|----------|-----------|
| 2026-02-21 | Next.js Route Handlers for API | Unified deployment, shared types between frontend and backend |
| 2026-02-21 | Zod for validation | Runtime type safety at API boundaries; pairs well with TypeScript |
| 2026-02-21 | Vercel for serverless deployment | 60-300s function timeout supports Prisma + NextAuth flows; native Next.js middleware support |
