# Implementation Plan — E‑commerce cookies & snacks

## Tech stack
- Frontend: Next.js (App Router), TypeScript, CSS modules / Tailwind (project uses globals.css)
- Auth: NextAuth (email + Google sign-in optional)
- DB: Prisma + SQLite for development (easy setup); production can use PostgreSQL
- Payments: Google Pay JS on client + server-side validation webhook
- Notifications: Email (SMTP) + in-app order status UI; optional push/WebSocket later
- Hosting: Vercel or other Next.js host (serverless API routes)

## High-level phases
1. Setup: create feature specs, add dependency list, env samples, Prisma schema.
2. Foundational: product model, product API, database seed, cart state.
3. User stories (priority order): implement browse/select (US1), auth (US2), shipping/checkout (US3), Google Pay integration (US4), order confirmation & shipment tracking (US5).
4. Polish: accessibility, responsive design, error handling, logging, docs.

## Key integrations
- Google Pay: client-only JS + server verification endpoint. Use Merchant ID in `.env`.
- NextAuth: store sessions in JWT or DB; link orders to user ID.
- Prisma: `Product`, `Order`, `OrderItem`, `User`, `Address`, `Notification` models.

## Risk & mitigations
- Payment testing: use Google Pay test environment and sandbox merchant IDs.
- Shipment notifications: initially simulated webhook updates; integrate carrier APIs later.

## Deliverables
- `specs/001-ecom-cookies/tasks.md` — execution tasks (generated).
- Minimal seed data and working checkout flow with Google Pay sandbox.
