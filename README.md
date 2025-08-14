
# CoConsult (coco)

Next.js App Router + Neon (Postgres) + Auth.js + Prisma + Stripe/PayPal + OpenRouter + Resend + R2/S3.

## Tech Stack
- **Frontend**: Next.js (TS, Tailwind, shadcn/ui, Framer Motion)
- **Backend**: Next.js API routes
- **DB**: Neon (serverless Postgres, pooled)
- **Auth**: Auth.js (email/password + Google + 2FA for staff)
- **ORM**: Prisma
- **Payments**: Stripe, PayPal, Wise (manual proof)
- **AI**: OpenRouter
- **Email**: Resend
- **Storage**: Cloudflare R2 / S3

## Monorepo? 
Single app for now (`/app`).

## Environments
- Vercel (prod/preview)
- Neon pooled `DATABASE_URL` in runtime.

## Getting Started (local)
```bash
npm i
cp .env.example .env.local   # fill keys
npm run dev
