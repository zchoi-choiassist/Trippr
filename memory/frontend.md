# Frontend Memory

> Patterns, preferences, and learnings for the Trippr frontend.
> This file is a living document updated as the project evolves.

## UI Framework & Styling

- **Framework**: Next.js 14+ with App Router, React 18+, TypeScript
- **Styling**: Tailwind CSS, mobile-first breakpoints
- **Design Reference**: Airbnb - clean, spacious layouts, high-quality imagery, smooth micro-interactions

## Component Patterns

_To be populated as components are built._

## State Management

- **Client state**: Zustand
- **Server state**: TanStack Query (React Query)

## Conventions

- Server Components by default; `'use client'` only when interactivity requires it
- PascalCase for component files and exports
- Co-locate tests alongside components (`Component.test.tsx`)

## Learnings

_To be populated as the project progresses._

## Decisions Log

| Date | Decision | Rationale |
|------|----------|-----------|
| 2026-02-21 | Next.js App Router with Tailwind CSS | Mobile-first SSR with utility-first styling matches Airbnb-inspired design goals |
| 2026-02-21 | Zustand + TanStack Query | Lightweight client state + robust server-state caching for collaborative features |
