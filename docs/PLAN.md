# Trippr - Project Plan

## Vision

A mobile-first web application that helps families and groups of friends organize trips with hyper-personalized recommendations drawn from Google Maps saved lists, social media posts, and independent research. Inspired by Airbnb's clean, inviting design language.

---

## Phase 1: Foundation

**Goal**: Bootable application with auth, basic UI shell, and database.

### 1.1 Project Initialization
- Initialize Next.js 14+ with TypeScript and App Router
- Configure Tailwind CSS with mobile-first breakpoints
- Set up ESLint, Prettier, and Vitest
- Configure Prisma with PostgreSQL connection
- Set up GitHub Actions CI (lint, type-check, test)

### 1.2 Authentication
- Integrate NextAuth.js with Google OAuth and email/password providers
- User table and session management in PostgreSQL
- Protected route middleware
- Login / sign-up pages (mobile-first, Airbnb-inspired)

### 1.3 UI Shell & Design System
- Global layout: bottom navigation (mobile), sidebar (desktop)
- Base UI components: Button, Input, Card, Avatar, Modal, Toast
- Typography and color tokens via Tailwind theme extension
- Loading skeletons and error boundary components

**PRDs to write**: Auth PRD, Design System PRD

---

## Phase 2: Core Trip Management

**Goal**: Users can create, view, edit, and delete trips. Multiple users can collaborate.

### 2.1 Trip CRUD
- Trip creation flow (destination, dates, cover image)
- Trip list/dashboard view
- Trip detail view with overview card
- Edit and delete functionality

### 2.2 Trip Members & Roles
- Invite members via link or email
- Roles: Owner, Editor, Viewer
- Member management UI within trip settings
- Real-time presence indicators (stretch)

### 2.3 Itinerary Builder
- Day-by-day itinerary view
- Add/remove/reorder activities within a day
- Activity detail: name, place, time, notes, links
- Drag-and-drop reordering (mobile-friendly)

**PRDs to write**: Trip Management PRD, Collaboration PRD, Itinerary Builder PRD

---

## Phase 3: Personalization Engine

**Goal**: Import user data sources and generate personalized recommendations.

### 3.1 Google Maps Integration
- OAuth connection to Google account
- Import saved lists (Favorites, Want to Go, custom lists)
- Display saved places on trip map and as suggestion cards
- Sync and refresh saved lists

### 3.2 Social Media Ingestion
- Connect social media accounts (Instagram, TikTok - scope TBD)
- Parse posts/saves for location and travel-related content
- Extract place names, tags, and sentiment
- Store as recommendation candidates

### 3.3 Research & Recommendation Pipeline
- Aggregate data from Google Maps saves, social media, and web research
- Score and rank recommendations by relevance to trip destination
- Present personalized suggestion feed within trip context
- Allow users to add suggestions directly to itinerary

**PRDs to write**: Google Maps Integration PRD, Social Ingestion PRD, Recommendation Engine PRD

---

## Phase 4: Enhanced Experience

**Goal**: Polish the product with rich features that increase engagement and utility.

### 4.1 Expense Splitting
- Add expenses to activities or trip-level
- Split by equal, percentage, or custom amounts
- Running balance per member
- Settlement suggestions

### 4.2 Polls & Voting
- Create polls for group decisions (restaurant, activity, date)
- Vote and view results in real-time
- Resolve polls and auto-add winning option to itinerary

### 4.3 Maps & Navigation
- Interactive map view per trip showing all activities
- Routing/directions between activities in a day
- Proximity-based suggestions ("you're near this saved place")

### 4.4 Notifications & Reminders
- Trip departure reminders
- Itinerary change notifications for collaborators
- Upcoming activity reminders
- Push notification support (PWA)

**PRDs to write**: Expenses PRD, Polls PRD, Maps View PRD, Notifications PRD

---

## Phase 5: Offline & PWA

**Goal**: Make the app installable and usable without connectivity.

### 5.1 Service Worker & Caching
- Cache trip data and itineraries for offline access
- Queue mutations and sync when back online
- Offline indicator UI

### 5.2 PWA Manifest
- App manifest for install-to-homescreen
- Splash screen and app icons
- Full-screen standalone mode

**PRDs to write**: Offline & PWA PRD

---

## Phase 6: Growth & Iteration

**Goal**: Feedback-driven improvements, performance tuning, and scaling.

### 6.1 Analytics & Monitoring
- Event tracking for key user flows
- Error monitoring (Sentry or equivalent)
- Performance monitoring (Core Web Vitals)

### 6.2 User Feedback Loop
- In-app feedback mechanism
- Usage analytics to inform roadmap
- A/B testing framework for UI experiments

### 6.3 Performance Optimization
- Image optimization pipeline (next/image, CDN)
- Bundle analysis and code splitting
- Database query optimization and indexing

---

## Development Process (Applied to Every Feature)

1. **PRD**: Write a Product Requirement Document in `docs/prds/`
2. **Tickets**: Break PRD into discrete tickets in `docs/tickets/`
3. **Implement**: Build on a feature branch per ticket
4. **Test**: Write unit, component, and e2e tests; run regression suite
5. **Review**: PR with CI checks passing
6. **Merge & Validate**: Merge to main; validate no regressions
7. **Update Memory**: Record patterns and learnings in `/memory/` files

---

## Immediate Next Steps

1. **Write Phase 1.1 PRD** - Project initialization and tooling setup
2. **Initialize Next.js project** - `npx create-next-app@latest` with TypeScript + App Router
3. **Set up Prisma** - Schema with User table, PostgreSQL connection
4. **Build auth flow** - NextAuth.js Google OAuth + email/password
5. **Create base UI components** - Button, Input, Card following Airbnb design patterns
