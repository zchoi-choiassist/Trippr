# Database Memory

> Patterns, preferences, and learnings for the Trippr database.
> This file is a living document updated as the project evolves.

## Stack

- **Database**: PostgreSQL
- **ORM**: Prisma
- **Migrations**: Prisma Migrate (committed to version control)

## Schema Conventions

- UUID primary keys on all tables
- `created_at` and `updated_at` timestamps on every table
- Soft deletes via `deleted_at` column where appropriate
- Snake_case column names in the database; Prisma maps to camelCase in TypeScript

## Core Entities (Planned)

- **User** - accounts, profiles, preferences
- **Trip** - trip metadata, dates, destination
- **TripMember** - many-to-many user-trip relationship with roles (owner, editor, viewer)
- **Itinerary** - day-by-day plans within a trip
- **Activity** - individual items within an itinerary day
- **Place** - cached place data from Google Maps
- **SavedList** - imported Google Maps saved lists
- **Recommendation** - personalized suggestions from various data sources

## Hosting & Connectivity

- **Database hosting**: External provider required — Vercel Postgres (Neon-powered) offers 60 free compute hours, or use Neon/Supabase free tier directly
- **Recommended**: Neon free tier (serverless PostgreSQL, generous free limits, connection pooling built-in) or Supabase free tier (PostgreSQL + extras)
- **Connection pooling**: Critical for serverless environments — each Vercel function invocation opens a new connection. Use Prisma's connection pooling or Neon's built-in pooler.
- **Region co-location**: Deploy database in the same region as Vercel functions to minimize query latency
- **Prisma Client singleton**: Use a singleton pattern to avoid creating multiple Prisma Client instances in serverless (standard Next.js pattern)

## Query Patterns

_To be populated as queries are written._

## Learnings

- **Serverless + PostgreSQL requires connection pooling** — without it, you'll hit connection limits quickly under load. Neon's pooler or PgBouncer are standard solutions.
- **Prisma Client bundle size matters on Cloudflare Workers** (3 MiB limit) — this was a factor in choosing Vercel over Cloudflare. Not an issue on Vercel.
- **Vercel Postgres is Neon under the hood** — if using Vercel's offering, you get the same serverless PostgreSQL with auto-scaling and branching
- **Railway includes PostgreSQL at ~$0.55/mo** — viable fallback if we need to self-host the database outside of Vercel's ecosystem
- **Database branching (Neon feature)**: Each PR preview deployment can have its own database branch — powerful for testing schema migrations without affecting production data

## Decisions Log

| Date | Decision | Rationale |
|------|----------|-----------|
| 2026-02-21 | PostgreSQL with Prisma | Relational data model fits trip/itinerary structure; Prisma provides type-safe queries |
| 2026-02-21 | UUID primary keys | Safer for distributed systems and URL exposure than sequential IDs |
| 2026-02-21 | Soft deletes for trips/activities | Users may want to recover deleted trip data; hard deletes for truly ephemeral data only |
| 2026-02-21 | External PostgreSQL hosting (Neon or Supabase free tier) | Vercel doesn't include PostgreSQL on Hobby; Neon offers serverless pooling ideal for Vercel functions |
