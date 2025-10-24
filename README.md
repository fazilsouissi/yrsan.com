# Mariya Mehraban Books

Localized e-commerce experience for two poetry books by Mariya Mehraban. Built with Next.js App Router, Prisma, Supabase, Stripe Checkout, and next-intl.

## Features

- Four-language storefront (EN/FR/DE/FA) with localized copy and RTL support for Persian.
- Bundle-aware cart with client persistence and server-side validation.
- Stripe Checkout integration with webhook confirmation, localized order success, and email notifications (customer + store owner).
- Order lookup page secured by email + order ID.
- Admin dashboard (credentials auth) covering order management, status updates, email resend, books CRUD, and shipping/settings management.
- Prisma schema for books, orders, order items, shipping rates, settings, and admin seed user.

## Requirements

- Node.js 18+
- npm (bundled with Node) or your preferred package manager
- Supabase PostgreSQL instance (or any PostgreSQL URL for `DATABASE_URL`)
- Stripe test keys
- Gmail App Password or SMTP provider for transactional email

## Getting Started

1. **Install dependencies**

   ```bash
   npm install
   ```

2. **Environment variables**

   Copy `.env.example` to `.env` and supply real credentials:

   ```bash
   cp .env.example .env
   ```

   Required variables:

   - `DATABASE_URL` – Supabase/PostgreSQL connection string
   - `SUPABASE_URL`, `SUPABASE_SERVICE_ROLE_KEY` – for Supabase adapter usage
   - `STRIPE_SECRET_KEY`, `STRIPE_PUBLISHABLE_KEY`, `STRIPE_WEBHOOK_SECRET`
   - `NEXTAUTH_SECRET`
   - `GMAIL_USER`, `GMAIL_APP_PASS`
   - `STORE_EMAIL_TO`, `SITE_URL`, `ADMIN_EMAIL`, `ADMIN_PASSWORD`

3. **Prisma setup**

   ```bash
   npx prisma migrate deploy
   npx prisma db seed
   ```

4. **Run development server**

   ```bash
   npm run dev
   ```

   Visit `http://localhost:3000` (root landing) or `http://localhost:3000/en` for the storefront.

5. **Admin dashboard**

   - Navigate to `http://localhost:3000/admin/login`
   - Sign in using the seeded credentials (`ADMIN_EMAIL` / `ADMIN_PASSWORD`)

## Stripe Webhooks

Expose your dev server to Stripe and register the webhook endpoint:

```bash
stripe listen --forward-to localhost:3000/api/stripe/webhook
```

Use the provided signing secret as `STRIPE_WEBHOOK_SECRET`.

## Useful Scripts

| Command              | Description                    |
|----------------------|--------------------------------|
| `npm run dev`        | Start Next.js dev server       |
| `npm run build`      | Create production build        |
| `npm run start`      | Run built application          |
| `npm run lint`       | TypeScript + ESLint checks     |
| `npm test`           | Run unit tests                 |
| `npm run test:watch` | Run tests in watch mode        |
| `npm run test:coverage` | Run tests with coverage     |

## Technologies

- Next.js 15 (App Router, React 19)
- next-intl for i18n and middleware routing
- Prisma ORM targeting Supabase PostgreSQL
- Stripe Checkout + Nodemailer (Gmail SMTP)
- Tailwind CSS v4
- Jest + Testing Library for unit testing

## Testing

The project includes a comprehensive test suite with **42 passing tests** covering:

- ✅ Cart calculations and validation (100% coverage)
- ✅ Authentication and authorization (100% coverage)
- ✅ Rate limiting (100% coverage)
- ✅ Email notifications (97.75% coverage)
- ✅ Checkout API (83.68% coverage)

```bash
npm test              # Run all tests
npm run test:watch    # Watch mode for development
npm run test:coverage # Generate coverage report
```

See [TESTING.md](./TESTING.md) for comprehensive testing documentation or [TEST_SUMMARY.md](./TEST_SUMMARY.md) for a quick reference.

## Documentation

- **[TESTING.md](./TESTING.md)** - Complete testing guide
- **[TEST_SUMMARY.md](./TEST_SUMMARY.md)** - Quick testing reference
- **[TESTING_IMPLEMENTATION.md](./TESTING_IMPLEMENTATION.md)** - Implementation details
- **[README_BACKEND.md](./README_BACKEND.md)** - Backend documentation index
- **[QUICK_START.md](./QUICK_START.md)** - 5-minute setup guide
- **[STATUS.md](./STATUS.md)** - Project status and deployment checklist

## Notes

- Cart persists in `localStorage` but is revalidated server-side during checkout.
- Shipping rates and store email are editable from the admin Settings tab and stored in the database.
- `STORE_EMAIL_TO` is also persisted in the `settings` table for runtime updates.
# yrsan.com
