# Cloudflare Workers SaaS Template

[![.github/workflows/deploy.yml](https://github.com/LubomirGeorgiev/cloudflare-workers-nextjs-saas-template/actions/workflows/deploy.yml/badge.svg)](https://github.com/LubomirGeorgiev/cloudflare-workers-nextjs-saas-template/actions/workflows/deploy.yml)

# [Live Demo](https://saas-stack.startupstudio.dev/sign-up)
# [Github Repo](https://github.com/LubomirGeorgiev/cloudflare-workers-nextjs-saas-template)

This is a SaaS template for Cloudflare Workers. It uses the [OpenNext](https://opennext.js.org/cloudflare) framework to build a SaaS application.

Have a look at the [project plan](./cursor-docs/project-plan.md) to get an overview of the project.

# Supported Features:

- ✅ Authentication with Lucia Auth
  - ✅ Email/Password Sign In
  - ✅ Email/Password Sign Up
  - ✅ Forgot Password Flow
  - ✅ Change Password
  - ✅ Session Management with Cloudflare KV
  - ✅ Turnstile Captcha Integration
  - ✅ Rate Limiting for Auth Endpoints
- ✅ Database with Drizzle and Cloudflare D1
  - ✅ Type-safe Database Operations
  - ✅ Automatic Migration Generation
  - ✅ SQLite for Local Development
- ✅ Email Service with React Email and Resend
  - ✅ Beautiful Email Templates
  - ✅ Email Preview Mode
  - ✅ Local Email Development Server
- ✅ Deployment with Github Actions
  - ✅ Automatic Deployments
  - ✅ Environment Variables Management
  - ✅ Database Migrations
- ✅ Modern UI
  - ✅ Tailwind CSS
  - ✅ Shadcn UI Components
  - ✅ Dark/Light Mode
  - ✅ Responsive Design
  - ✅ Loading States and Animations
  - ✅ Toast Notifications
  - ✅ Settings Dashboard
  - ✅ Landing Page
- ✅ Validations with Zod and React Hook Form
  - ✅ Type-safe Form Validations
  - ✅ Server-side Validations
  - ✅ Client-side Validations
- ✅ Developer Experience
  - ✅ TypeScript Support
  - ✅ ESLint Configuration
  - ✅ Prettier Configuration
  - ✅ Type-safe Environment Variables
  - ✅ Cloudflare Types Generation
  - ✅ AI-powered Development with Cursor

## Planned features (TODO):

- [ ] Update Meta SEO tags
- [ ] Multi-language support (i18n)
- [ ] Billing
- [ ] Admin dashboard
- [ ] Email verification on sign up
- [ ] Notifications
- [ ] Payments
- [ ] Webhooks
- [ ] Track bundle size with https://www.npmjs.com/package/webpack-bundle-analyzer

# Running it locally

1. `pnpm install`
2.  Copy `.env.development.example` to `.env.development` and fill in the values
3. `pnpm db:migrate:dev` - Creates a local SQLite database and applies migrations
4. `pnpm dev`
5.  Open http://localhost:3000

## Changes to wrangler.toml

After making a change to wrangler.toml, you need to run `pnpm cf-typegen` to generate the new types.

## Things to change and customize before deploying to production
1. Go to `src/constants.ts` and update it with your project details
2. Update the documentation in `./cursor-docs` with your project details so that Cursor AI can give you better suggestions
3. Update the footer in `src/components/footer.tsx` with your project details and links
4. Optional: Update the color palette in `src/app/globals.css`
5. Update the metadata in `src/app/layout.tsx` with your project details

## Deploying to Cloudflare with Github Actions

1. Create D1 and KV namespaces
2. Create a Resend account, and set the `RESEND_API_KEY` as a secret in your Cloudflare Worker.
3. Create a Turnstile catcha in your Cloudflare account, and set the `NEXT_PUBLIC_TURNSTILE_SITE_KEY` as a Github Actions variable.
4. Set `TURNSTILE_SECRET_KEY` as a secret in your Cloudflare Worker.
5. Update the `wrangler.toml` file with the new database and KV namespaces and env variables.
6. Create a Cloudflare API token with the following permissions:
    - Workers Builds Configuration:Edit
    - AI Gateway:Edit
    - Workers AI:Edit
    - Queues:Edit
    - Vectorize:Edit
    - D1:Edit
    - Workers R2 Storage:Edit
    - Cloudflare Images:Edit
    - Workers Tail:Read
    - Workers KV Storage:Edit
    - Workers Scripts:Edit
7. Add the API token to the Github repository secrets as `CLOUDFLARE_API_TOKEN`
8. Add the Cloudflare account id to the Github repository variables as `CLOUDFLARE_ACCOUNT_ID`
9. Add the database name to the Github repository variables as `DATABASE_ID`. This should match the database name in the `wrangler.toml` file.
10. Push to the main branch

## Email templates
If you want to preview and edit the email templates you can:
1. `pnpm email:dev`
2. Open http://localhost:3001
3. Edit the email templates in the `src/react-email` folder
4. For inspiration you can checkout https://react.email/templates


### How to upgrade this template
Since this template is based on the [OpenNext](https://opennext.js.org/cloudflare) framework we need to make sure that we are following the changes they are making and update this template accordingly.

Go [here](https://github.com/cloudflare/workers-sdk/tree/main/packages/create-cloudflare/templates-experimental/next/templates) and check which have have recent commits.

[This](https://github.com/cloudflare/workers-sdk/tree/a5725bdb32f0b1c67063b988d09e1b76266aa19e/packages/create-cloudflare/templates-experimental/next/templates) is the git commit we are using
