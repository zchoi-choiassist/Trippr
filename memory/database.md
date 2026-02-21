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

## Query Patterns

_To be populated as queries are written._

## Learnings

_To be populated as the project progresses._

## Decisions Log

| Date | Decision | Rationale |
|------|----------|-----------|
| 2026-02-21 | PostgreSQL with Prisma | Relational data model fits trip/itinerary structure; Prisma provides type-safe queries |
| 2026-02-21 | UUID primary keys | Safer for distributed systems and URL exposure than sequential IDs |
| 2026-02-21 | Soft deletes for trips/activities | Users may want to recover deleted trip data; hard deletes for truly ephemeral data only |
