# CoConsult Platform Blueprint

## Architecture Overview
- **Framework**: Next.js 15 with App Router
- **Language**: TypeScript
- **Styling**: Tailwind CSS + shadcn/ui; glassmorphism and vibrant gradients
- **Database**: Postgres (Neon) accessed via Prisma
- **Authentication**: Auth.js (email/password, Google, optional 2FA)
- **Storage**: R2/S3 for user uploads
- **Payments**: Stripe, PayPal, Wise (manual proof)
- **Messaging & Notifications**: internal chat and email (Resend)
- **Blockchain**: optional for document hashes and transaction logs
- **Deployment**: Vercel + Neon

## Feature Modules
### 1. Public Pages
- Dynamic homepage with hero slider, service cards, country highlights, testimonials and live chat
- Content pages (about, services, destinations) editable only by admins

### 2. User Panel
- Dashboard with profile completion tracker
- Document center with status tags and blockchain hash
- Service marketplace: choose services, submit requests, view invoices
- Payment portal supporting Stripe/PayPal/Wise
- Application tracker for each service request
- Messaging center for support tickets
- Booking system for counseling sessions
- Notifications & downloadable PDF summaries

### 3. Admin Panel
- User and request management with search/filter/export
- Role assignment (admin, moderator, financial manager, virtual assistant)
- Document verification and feedback
- Financial management: view, approve, reject transactions; filter by date range; daily totals
- Content management: create/update pages, sliders, testimonials
- Bulk email to all users or segments
- Analytics dashboard for registrations, revenue, service usage
- Audit log with IP, user, role, action; exportable and verifiable via blockchain hash + QR code

### 4. Advanced Features
- AI recommendations for missing docs, scholarships, next steps
- Gamified progress with badges and rewards
- PWA with offline support and dark mode
- Localization and accessibility (WCAG 2.2+)

## Design Guidelines
- **Color Palette**: Deep navy background (`#0a0f1f`) with neon accents (`#00e0ff`, `#ff00a8`) and gradient overlays
- **Typography**: Inter for body, Poppins for headings
- **Glassmorphism**: frosted cards with 30% opacity, subtle shadows
- **Imagery**: high‑resolution photos for study/work/travel themes
- **Interaction**: smooth Framer Motion transitions, micro‑animations for status changes

## Database Schema (Prisma)
See `prisma/schema.prisma` for full definitions. Key tables:
- `User`, `Role`
- `Service`, `UserService`
- `Document`, `DocumentType`
- `Transaction`, `Purpose`
- `Message`, `Conversation`
- `Booking`
- `Notification`
- `AuditLog`

## Development Steps
1. Initialize Next.js project with Tailwind and shadcn/ui
2. Configure Prisma and generate migrations
3. Implement authentication and role-based access
4. Build public pages with CMS controls
5. Implement user dashboard modules (documents, services, payments)
6. Build admin dashboard with financial management and content tools
7. Integrate messaging, notifications, and booking
8. Add AI recommendations and gamification
9. Write tests, run accessibility and performance checks

## Notes
This blueprint covers core functionality; individual features should be implemented iteratively with proper testing and security reviews.
