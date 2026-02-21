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

## Deployment

- **Platform**: Vercel (Hobby for dev/prototyping, Pro for commercial launch)
- **Why Vercel**: Native Next.js support, zero-config deployment, day-one feature support for App Router, Server Components, ISR, middleware, and image optimization
- **Hobby limits**: 100 GB bandwidth, 6,000 build minutes/mo, 150K serverless invocations/mo, 60-300s function timeout
- **Commercial use**: Not allowed on Hobby — must upgrade to Pro ($20/user/mo) before launch
- **Image optimization**: `next/image` works natively on Vercel (no adapter needed, unlike Netlify/Cloudflare)

## Learnings

- **Vercel has best-in-class Next.js DX** — zero-config deploys, preview deployments per PR, instant rollbacks
- **6,000 build minutes/mo on Hobby** is very generous for active development (Netlify only offers 300)
- **Function timeout of 60-300s** is critical — Netlify's 10s limit would have been a real risk for SSR + Prisma + NextAuth flows
- **Netlify middleware execution order differs** from Next.js docs — would have required platform-specific workarounds. Vercel matches Next.js behavior exactly.
- **Cloudflare's 3 MiB worker bundle limit** is incompatible with Prisma Client — eliminated as an option
- **Render free tier sleeps after 15 min inactivity** — poor UX for a consumer-facing app
- **Railway ($5/mo)** is the best budget option if we ever need to move off Vercel — PostgreSQL included, no timeout issues

## Decisions Log

| Date | Decision | Rationale |
|------|----------|-----------|
| 2026-02-21 | Next.js App Router with Tailwind CSS | Mobile-first SSR with utility-first styling matches Airbnb-inspired design goals |
| 2026-02-21 | Zustand + TanStack Query | Lightweight client state + robust server-state caching for collaborative features |
| 2026-02-21 | Deploy to Vercel | Native Next.js support, best DX, generous Hobby tier for development. Upgrade to Pro before commercial launch. |
