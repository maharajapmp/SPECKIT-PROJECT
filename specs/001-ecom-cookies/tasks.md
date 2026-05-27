# Tasks — E‑commerce cookies & snacks

Phase 1: Setup
- [ ] T001 Create feature spec file at specs/001-ecom-cookies/spec.md
- [ ] T002 Update `package.json` with dependencies: `next-auth`, `prisma`, `@prisma/client`, `sqlite3`, and `nodemailer` (if sending emails). Path: package.json
- [ ] T003 Add Prisma schema and config at prisma/schema.prisma
- [ ] T004 Add environment sample `.env.example` with placeholders for `DATABASE_URL`, `NEXTAUTH_URL`, `GOOGLE_PAY_MERCHANT_ID`, `SMTP_*`.

Phase 2: Foundational
- [ ] T005 [P] Create `Product` and `Order` models in `prisma/schema.prisma` and generate Prisma client. Path: prisma/schema.prisma
- [ ] T006 [P] Add seed script to insert sample products (prisma/seed.ts) and document how to run it. Path: prisma/seed.ts
- [ ] T007 [P] Implement products API route at `app/api/products/route.ts` returning product list and detail. Path: app/api/products/route.ts
- [ ] T008 [P] Create basic global styles and layout adjustments in `app/globals.css` and `app/layout.tsx` to accommodate storefront header/cart. Paths: app/globals.css, app/layout.tsx

Phase 3: User Stories (Priority order)

US1 — Browse & Select Products (P1)
- [ ] T009 [US1] Create `ProductList` component to render product grid and `Add to Cart` controls. Path: app/components/ProductList.tsx
- [ ] T010 [US1] Create product detail page at `app/product/[id]/page.tsx` showing images, price, and quantity selector. Path: app/product/[id]/page.tsx
- [ ] T011 [US1] Implement `Cart` context and UI at `app/context/cart.tsx` and `app/components/Cart.tsx` (supports multiple items and quantity updates). Path: app/context/cart.tsx, app/components/Cart.tsx
- [ ] T012 [P] [US1] Ensure cart persists in `localStorage` for anonymous users. Path: app/context/cart.tsx

US2 — Authentication (P1)
- [ ] T013 [US2] Configure NextAuth at `app/api/auth/[...nextauth]/route.ts` with email provider (and Google optional). Path: app/api/auth/[...nextauth]/route.ts
- [ ] T014 [US2] Add `SignInButton` and `UserMenu` components and wire auth state to header. Path: app/components/SignInButton.tsx, app/components/UserMenu.tsx
- [ ] T015 [US2] Link anonymous cart to user after sign-in (merge local cart into DB cart). Path: app/context/cart.tsx, app/api/cart/route.ts

US3 — Shipping Address & Checkout (P1)
- [ ] T016 [US3] Create `ShippingForm` component to collect name, address lines, city, postal code, country. Path: app/components/ShippingForm.tsx
- [ ] T017 [US3] Create checkout page at `app/checkout/page.tsx` showing cart summary, shipping form, and payment options. Path: app/checkout/page.tsx
- [ ] T018 [US3] Implement `Order` creation API at `app/api/orders/route.ts` that accepts cart, shipping, and user info. Path: app/api/orders/route.ts
- [ ] T019 [US3] Add server-side validation for shipping address and order totals. Path: app/api/orders/route.ts

US4 — Google Pay Integration (P1)
- [ ] T020 [US4] Add Google Pay client integration to checkout page and render the Google Pay button (use test environment). Path: app/checkout/page.tsx
- [ ] T021 [US4] Implement server-side payment endpoint at `app/api/payments/gpay/route.ts` to validate and record payment. Path: app/api/payments/gpay/route.ts
- [ ] T022 [US4] Update `Order` record with payment status and transaction reference after successful payment. Path: app/api/orders/route.ts

US1 supplemental — Cart actions (P1)
- [ ] T023 [US1] Implement increase/decrease quantity and remove-item actions in `app/components/Cart.tsx`. Path: app/components/Cart.tsx

US5 — Order confirmation & Shipment notifications (P2)
- [ ] T024 [US5] Create `Notification` model in `prisma/schema.prisma` and API route `app/api/notifications/route.ts` for in-app notifications. Path: prisma/schema.prisma, app/api/notifications/route.ts
- [ ] T025 [US5] Send order-confirmation email (or in-app notification) after order placement (use `nodemailer` or a mocked email provider). Path: app/api/orders/route.ts
- [ ] T026 [US5] Create order status page at `app/orders/[id]/page.tsx` showing shipment tracking and notification history. Path: app/orders/[id]/page.tsx
- [ ] T027 [US5] Implement a simple background job/script to simulate shipment status updates and push notifications (scripts/update-shipment-status.ts). Path: scripts/update-shipment-status.ts

Phase: Polish & Cross-cutting
- [ ] T028 Accessibility: run axe checks and fix high-impact issues. Path: app/
- [ ] T029 Responsive: verify mobile/tablet layouts and adjust CSS. Path: app/globals.css, app/components/*
- [ ] T030 Logging & error handling: add basic request logging in API routes and error UI. Path: app/api/*
- [ ] T031 Documentation: update README with environment variables and how to run in sandbox (Google Pay test). Path: README.md

Dependencies & Ordering
- Run: `prisma migrate dev --name init` and `pnpm/ npm/ yarn prisma db seed` after T005–T007.
- MVP suggestion: implement through T022 (US1–US4) to have a fully working checkout with Google Pay sandbox; T024–T027 are enhancements for shipment notifications.

Estimated total tasks: 31

Parallel opportunities: T005–T007 (DB + seed + product API) can be done in parallel; UI components (T009–T012) can be implemented alongside auth (T013–T015).

Independent test criteria (per story)
- US1: Add item to cart, change quantity, checkout flow reaches payment screen.
- US2: Sign-in redirects and session persists; cart merges after login.
- US3: Shipping form validates and order creation succeeds with address saved.
- US4: Google Pay button renders and server validates test payment (sandbox).
- US5: Order confirmation sent and order status page shows simulated shipment updates.
