# Feature: E‑commerce cookies & snacks storefront

## Goal
Build a professional e-commerce storefront for cookies and snacks supporting sign-in, multi-item selection, shipping address entry, Google Pay checkout, and shipment-status notifications.

## User stories
- US1 (P1): As a customer I can browse product listings, view product details, add one or more items to a cart, and change quantities.
- US2 (P1): As a customer I can sign in and sign out so my cart and orders are associated with my account.
- US3 (P1): As a customer I can enter and save a shipping address during checkout.
- US4 (P1): As a customer I can pay with Google Pay to complete the order.
- US5 (P2): As a customer I receive order confirmation and shipment-status notifications and can view tracking status.

## Acceptance criteria (high level)
- Browsing: product list and detail pages show product data and allow adding quantities to cart.
- Auth: users can sign in; secure pages redirect to sign-in when required.
- Checkout: captures shipping address, calculates totals, invokes Google Pay, and records payment result.
- Notifications: user receives a confirmation and sees shipment updates in the UI.

## Notes
- Use the repository's existing Next.js `app/` layout and TypeScript.
- Prefer serverless API routes (Next.js App Router `app/api/.../route.ts`).
- For persistent data use Prisma with SQLite (simple local dev).
