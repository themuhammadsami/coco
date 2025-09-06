# CoConsult Platform — Full Build Prompt

This document consolidates the project requirements for building the production-ready CoConsult platform.

## 0. Tech Stack & Architecture
- **Monorepo:** Turborepo (pnpm)
- **Frontend:** Next.js 15 (App Router, RSC), React 18, TypeScript, Tailwind CSS, shadcn/ui, Framer Motion, Lucide icons, React Hook Form + Zod.
- **Backend:** NestJS (TypeScript) with REST and GraphQL APIs, Swagger docs, class-validator, CQRS for critical domains.
- **Database:** PostgreSQL 15 with Prisma ORM; Redis for caching/queues/rate limiting; optional Elasticsearch for search.
- **Auth:** NextAuth.js (email/password, Google OAuth) with 2FA (TOTP) and optional Web3 signature. Passwords hashed with Argon2id.
- **Storage:** S3-compatible (Cloudflare R2); file virus scanning (ClamAV) pipeline; image optimization.
- **Payments:** Stripe, PayPal, Wise, and manual bank transfer (receipt upload + review). Webhooks with signature verification.
- **Email:** Resend/SendGrid for transactional, bulk campaigns with unsubscribe and list management.
- **Realtime:** WebSockets or Pusher/Ably for chat, notifications, and admin events.
- **Blockchain Notarization:** SHA-256 hash anchors to Polygon/Ethereum, storing tx hash and block number.
- **PDF/QR:** pdf-lib for stamping, qrcode for verification links.
- **Observability:** OpenTelemetry, Prometheus metrics, pino logging, Sentry.
- **DevOps:** Docker Compose for local; GitHub Actions CI/CD; deployment presets for Vercel (frontend) and Fly.io/Render (API); Neon/PlanetScalePG (DB); Cloudflare R2 (files).

## 1. Information Architecture
### Main Menu
1. Home
2. Services ▾ (Study Abroad, Work Abroad, Immigration, Pre‑Arrival, Post‑Arrival, Travel Insurance, Accommodation, Visa Organization, Tax Returns, Scholarships, Career Counseling)
3. Countries ▾ (Europe, Canada, USA, Australia, UK, Malta, Spain, China, …)
4. Success Stories
5. Resources ▾ (Articles, Templates, FAQs)
6. Pricing
7. Contact / Book Session
8. Dashboard (contextual when signed in)

### Footer
Company info, legal pages, social links, newsletter signup, sitemap. All public pages editable via admin CMS.

## 2. UX/UI Design System
- Glassmorphism accents with vibrant gradients.
- **Colors:** Primary `#6C5CE7 → #8E2DE2`, Secondary `#00C2A8`, Accents `#FF6B6B`, `#FDBA74`, `#22D3EE`, neutral surfaces with 8–12% blur.
- Typography: Inter/Manrope, heading weight 700, body 400–500, base size 16px, line-height ≥1.6.
- Components: shadcn primitives, motion on hover/press, visible focus rings, 8‑pt spacing.
- Accessibility: WCAG 2.2 AA, keyboard navigation, skip links, ARIA landmarks.

### Homepage Hero & Slider
Glassmorphic CTA card over animated gradient background with high-impact imagery. Primary CTA “Get Your Profile Reviewed”, secondary “Book a Session”. Trust badges and testimonials link.

## 3. Core Features
### 3.1 Registration & Onboarding
Email/password or Google OAuth, optional Web3 wallet bind. Guided onboarding with intent selection, document upload, and profile completion meter.

### 3.2 User Dashboard
Profile management, document center with virus scan and status flow, service requests, payments and invoices, application tracker, messaging, booking, notifications, and downloadable PDF report with QR verification.

### 3.3 Admin Dashboard
User management, role-based permissions (admin, moderator, financial_manager, content_editor, virtual_assistant, auditor), document review, payment/transaction oversight with purposes and daily totals, bulk email campaigns, CMS for pages/blocks/media, messaging center, analytics, security controls, audit logging with blockchain anchoring.

### 3.4 Moderators & Roles
Moderators handle content/doc review; virtual assistants have limited actions; financial managers perform transaction tasks; auditors access logs read-only. All actions logged with IP, username, role.

## 4. Data Model
See `prisma/schema.prisma` for detailed Prisma schema covering users, roles, permissions, profiles, documents, services, service requests, transactions, invoices, email campaigns, pages, messaging, appointments, notifications, audit logs, and verifications.

## 5. API Overview
Representative REST endpoints:
- Auth: `POST /auth/register`, `POST /auth/login`, `POST /auth/2fa/enable`, `POST /auth/2fa/verify`, `GET /me`.
- Documents: `POST /documents`, `GET /documents`, `PATCH /documents/:id/status`.
- Services: `GET /services`, `POST /service-requests`, `PATCH /service-requests/:id`.
- Payments: `POST /checkout`, `POST /bank-transfer`, webhooks, admin review endpoints.
- CMS: CRUD for pages/blocks/media with publish flow.
- Messaging: `POST /threads`, `GET /threads`, `POST /threads/:id/messages`.
- Email Campaigns: `POST /email/campaigns`, `POST /email/send`, `GET /email/stats`.
- Verification: `GET /verify/:id` returning record snapshot and chain link.

## 6. Feature Workflows
- **Transaction Review:** user payment → webhook/record → admin approve/reject → invoice PDF with QR → audit log and optional chain anchor.
- **Document Verification:** upload → virus scan → moderator verification → public verification page with QR and optional chain anchor.
- **Email Campaign:** segment users, compose template, preview, send/schedule, track opens/clicks/unsubscribes.
- **CMS Publishing:** content editor drafts → preview → admin publishes → cache invalidation and versioning.

## 7. Security & Compliance
Rate limiting, CSRF protection, 2FA, secure cookies, encryption at rest/in transit, PII minimization, data export/deletion, audit log tamper evidence with hashes and optional blockchain anchoring.

## 8. Testing Strategy
Unit tests (Jest), e2e tests (Playwright), accessibility tests (axe), performance budgets (Lighthouse CI), webhook contract tests.

## 9. Deployment & Ops
Environments for local, staging, production. GitHub Actions CI/CD pipelines: lint → typecheck → test → build → migrate → deploy. Daily backups, cron jobs for digest and finance rollup.

## 10. Developer Checklist
1. Setup monorepo with linting and formatting.
2. Implement Prisma schema, migrations, and seed data (roles, permissions, services, purposes).
3. Build auth flows with RBAC guards.
4. Implement file storage with virus scanning and document status logic.
5. Integrate payments and transaction management.
6. Generate invoices with QR verification links.
7. Build messaging and booking modules.
8. Implement CMS with preview and versioning.
9. Add email campaign system with list management.
10. Create analytics dashboards.
11. Add audit logging with blockchain anchoring and verification endpoints.
12. Ensure accessibility, performance, and PWA support.
13. Configure CI/CD and deployment manifests.
14. Provide `.env.example`, README, and sample content/images.

---
This prompt serves as the blueprint for developing the full CoConsult platform from frontend to backend with all specified features.
