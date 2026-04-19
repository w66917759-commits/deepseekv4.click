# DeepSeek V4 — AI Video & Image Workflow Toolkit

A multi-model AI video and image workflow toolkit built around a DeepSeek V4-style interface. Run text-to-video, image-to-video, and image generation on Sora 2, Kling V3, Seedance, Nano Banana, See Dream, and GPT Image today, with DeepSeek V4 slotting into the same canvas when it ships.

**Live site:** [deepseekv4.click](https://deepseekv4.click)

## Featured SEO Entry Points

These public landing pages are the main long-tail SEO targets for the AI video workflow:

| Page | Search intent |
|------|---------------|
| [Free AI Video Generator](https://deepseekv4.click/deepseek-v4-free-ai-video-generator) | Compare free online AI video tools and starter-credit workflows |
| [AI Video Generator](https://deepseekv4.click/deepseek-v4-video-generator) | Create AI videos online from text, images, and references |
| [Text to Video](https://deepseekv4.click/deepseek-v4-text-to-video) | Turn prompts and scripts into AI video drafts |
| [Image / Photo to Video](https://deepseekv4.click/deepseek-v4-image-to-video) | Animate photos, product shots, and still images |
| [AI Video Editing](https://deepseekv4.click/deepseek-v4-ai-video-editing) | Transform, extend, and refine existing clips with AI-assisted workflows |

### Social backlink copy

```text
Testing a browser-based AI video generator for text-to-video, image-to-video, and fast creative drafts.

Good starting point if you want to compare online AI video tools with free starter credits.

Try it here:
https://deepseekv4.click/deepseek-v4-free-ai-video-generator

#AIVideo #TextToVideo #AICreators
```


## Tech Stack

| Layer | Technology |
|-------|-----------|
| Framework | Next.js 16 (App Router) |
| Language | TypeScript 5.9 |
| UI | React 19, Tailwind CSS 4, Lucide icons |
| Auth | Clerk |
| Database | Supabase (PostgreSQL + Storage) |
| Payments | Stripe, PayPal |
| State | Zustand |
| AI Chat | MiniMax (streaming) |







## Features

- **Multi-model video generation** — submit jobs to 7 different video AI models with configurable resolution, duration, and aspect ratio
- **Multi-model image generation** — generate images via 5 AI models with various styles and sizes
- **AI prompt assistant** — chat-based prompt refinement powered by MiniMax with streaming responses
- **Showcase gallery** — public video wall with staggered waterfall layout
- **Credits & billing** — subscription plans (Stripe) and one-time credit packs (PayPal) with atomic deduction
- **SEO system** — SSR landing pages, JSON-LD structured data, sitemap, Open Graph metadata
- **Job queue** — real-time polling UI for both video and image generation jobs



## SEO Content System

Landing pages are driven by typed content objects — no CMS, no duplication across routes. Adding a new long-tail keyword page is three steps.

### Content sources

| File | Purpose |
|------|---------|
| `src/lib/content/landing-pages.ts` | Core DeepSeek V4 / Delphin workflow pages and the root `landingPages` aggregate |
| `src/lib/content/keyword-pages.ts` | Long-tail keyword pages (free AI video generator, AI video editing, etc.) |
| `src/lib/content/deepseek-keyword-pages.ts` | DeepSeek long-tail cluster (prompt library, photo generator, paid version, etc.) |
| `src/lib/content/shorts-pages.ts` | Platform-specific Shorts pages (TikTok, YouTube Shorts, Instagram Reels) |
| `src/lib/content/model-pages.ts` | Model comparison and showcase pages |
| `src/lib/content/sora-pages.ts` | Sora 2 / alternative-to-Sora pages |
| `src/lib/content/types.ts` | `LandingPageContent`, `GuideContent`, `UseCaseContent`, and related types |

All `*-pages.ts` files are merged into the `landingPages` export consumed by the sitemap and the localized `[lang]/[slug]` route.

### LandingPageContent shape

```ts
type LandingPageContent = {
  slug: string;
  title: string;
  h1: string;
  description: string;
  mainKeyword: string;
  keywords?: string[];
  intro: string;
  heroImage: { src: string; alt: string; prompt?: string };
  ctaLabel: string;
  ctaHref: string;
  sections: ContentSection[]; // 3–4 recommended
  faqs: FaqItem[];            // 3–5 recommended
  related: RelatedLink[];     // 3–4 internal links
};
```

### Add a new SEO page

1. **Append a content object** to the most appropriate `src/lib/content/*-pages.ts` file. At least one FAQ should literally contain the primary keyword so People-Also-Ask can pick it up.
2. **Create a route** at `src/app/<slug>/page.tsx` that imports `getLandingPage("<slug>")`, wires `createMetadata`, `createSoftwareApplicationSchema`, and `createFaqSchema` from `@/lib/seo`, and renders `<ContentPageTemplate {...pageData} />`.
3. **Register in the footer** (optional but recommended) at `src/components/layout/Footer.tsx` under the category that matches the search intent.

The sitemap auto-picks up anything exported via `landingPages` — see `src/app/sitemap.ts` for the aggregation. Localized versions (`/zh/<slug>`, `/fr/<slug>`, etc.) are opt-in through `src/lib/content/translations.ts`.

### Target Keyword Map

DeepSeek long-tail cluster (English):

| Slug | Primary keyword | Intent |
|------|-----------------|--------|
| `/deepseek-v4-video-generator` | ai video creator | Flagship video workflow |
| `/deepseek-v4-image-generator` | Delphin image generator | Flagship image workflow |
| `/deepseek-v4-text-to-video` | ai text to video generator free | Prompt-led video |
| `/deepseek-v4-image-to-video` | photo to video ai | Reference-led motion |
| `/deepseek-v4-prompt-generator` | ai video script generator | Prompt-building workflow |
| `/deepseek-v4-free-ai-video-generator` | best free ai video generator | Free-tier intent |
| `/deepseek-v4-ai-video-editing` | ai video editing | Edit-style workflow |
| `/deepseek-prompt` | deepseek prompt | Prompt library and structure |
| `/deepseek-v4-image-generation` | deepseek v4 image generation | V4-specific image workflow |
| `/deepseek-ai-video-generator` | deepseek ai video generator | Tool intent (no "v4") |
| `/deepseek-photo-generator` | deepseek photo generator | Photo-first image generation |
| `/deepseek-image-generator` | deepseek image generator | Tool intent (no "v4") |
| `/does-deepseek-have-a-paid-version` | does deepseek have a paid version | Question intent, pricing answer |

Platform / comparison clusters:

| Slug | Primary keyword |
|------|-----------------|
| `/ai-tiktok-video-generator` | AI TikTok video generator |
| `/ai-youtube-shorts-generator` | AI YouTube Shorts generator |
| `/ai-instagram-reels-generator` | AI Instagram Reels generator |
| `/sora-2-vs-deepseek-v4` | Sora 2 vs DeepSeek V4 |
| `/sora-2-vs-seedance` | Sora 2 vs Seedance |
| `/seedance-2-0` | Seedance 2.0 |
| `/wan-2-7-video-generator` | Wan 2.7 video generator |



## Supported AI Models

### Video Models

| Model ID | Display Name | Status | Audio | Notes |
|----------|-------------|--------|-------|-------|
| `deepseek-v4` | DeepSeek V4-Omni | Coming Soon | — | Flagship model |
| `sora-2` | Sora 2 Pro | Active | No | High quality |
| `sora-2-standard` | Sora 2 | Active | No | Cost-effective |
| `kling-v3-omni` | Kling V3 Omni | Active | Yes | Video & audio |
| `kling-v3` | Kling V3 | Active | Yes | Fast |
| `seedance-1.5-pro` | Seedance 1.5 Pro | Active | Yes | Fast |
| `seedance-2.0` | Seedance 2.0 | Active | Yes | Next-gen |

### Image Models

| Model ID | Display Name | Status |
|----------|-------------|--------|
| `deepseek-v4` | DeepSeek V4 | Coming Soon |
| `nano-banana-pro` | Nano Banana Pro | Active (Hot) |
| `nano-banana` | Nano Banana | Active (Fast) |
| `see-dream-5.0` | See Dream 5.0 | Active (New) |
| `gpt-image` | GPT Image | Active (Popular) |

## Project Structure

```
├── docs/                        # API & payment documentation
├── public/                      # Static assets (videos, images, icons)
├── scripts/                     # Build & utility scripts
├── src/
│   ├── app/                     # Next.js App Router
│   │   ├── api/                 # API routes (generate, ai-image, checkout, webhooks, etc.)
│   │   ├── auth/                # Clerk sign-in / sign-up
│   │   ├── generate/            # Video generation page
│   │   ├── ai-image/            # Image generation page
│   │   ├── chat/                # Prompt assistant page
│   │   ├── showcase/            # Video showcase gallery
│   │   ├── pricing/             # Pricing & plans
│   │   ├── guides/[slug]/       # Dynamic guide pages
│   │   ├── contact/             # Contact page
│   │   ├── privacy/             # Privacy policy
│   │   ├── terms/               # Terms of service
│   │   ├── refund/              # Refund policy
│   │   └── deepseek-v4-*/       # SEO landing pages
│   ├── components/              # React components
│   │   ├── layout/              # Header, Footer
│   │   ├── home/                # Landing page sections
│   │   ├── chat/                # Chat UI components
│   │   ├── ui/                  # Generation canvas, video cards, job queues
│   │   ├── content/             # Showcase, guides, landing page templates
│   │   ├── providers/           # Context providers (auth, job queues)
│   │   └── seo/                 # JSON-LD structured data
│   ├── hooks/                   # Custom React hooks
│   ├── lib/                     # Business logic & utilities
│   │   ├── generate/            # Video generation (adapters, validation, types)
│   │   │   └── adapters/        # Per-model adapters (Sora, Kling, Seedance, etc.)
│   │   ├── ai-image/            # Image generation (adapters, validation, types)
│   │   │   └── adapters/        # Per-model adapters (Gemini, CometAPI)
│   │   ├── content/             # Static content (guides, showcase, landing pages)
│   │   ├── constants.ts         # Models, pricing plans, features, FAQs
│   │   ├── credits.ts           # Credit calculation & management
│   │   ├── stripe.ts            # Stripe client & price mapping
│   │   ├── paypal.ts            # PayPal API functions
│   │   ├── supabase.ts          # Client-side Supabase
│   │   ├── supabase-server.ts   # Server-side Supabase (service role)
│   │   ├── seo.ts               # SEO utilities
│   │   ├── site.ts              # Site URL & metadata
│   │   ├── rate-limit.ts        # Rate limiting
│   │   └── video-pricing.ts     # CSV-based video pricing
│   └── stores/                  # Zustand stores
├── supabase-migration.sql       # Database schema & RPC functions
├── next.config.ts
├── package.json
└── tsconfig.json
```

## Getting Started

### Prerequisites

- **Node.js** 20+ (24 LTS recommended — matches the current Vercel default)
- **npm** or **pnpm**
- A [Clerk](https://clerk.com) account (authentication)
- A [Supabase](https://supabase.com) project (database & storage)
- AI model API keys (see Environment Variables below)
- Stripe and/or PayPal accounts (payments)

### Install & Run

```bash
git clone <repo-url>
cd DS-V4-VIDEO
npm install
```

Copy `.env.local.example` (or create `.env.local`) and fill in the required values (see below).

```bash
npm run dev      # Start development server
npm run build    # Production build
npm run start    # Start production server
```

## Environment Variables

Create a `.env.local` file with the following variables:

### Site

| Variable | Description |
|----------|-------------|
| `NEXT_PUBLIC_SITE_URL` | Public site URL (default: `https://deepseekv4.click`) |

### Analytics (Google Analytics 4)

| Variable | Description |
|----------|-------------|
| `NEXT_PUBLIC_GA_MEASUREMENT_ID` | GA4 Measurement ID (e.g. `G-XXXX`). Optional — if unset, the site does not load gtag.js. |

### Authentication (Clerk)

| Variable | Description |
|----------|-------------|
| `NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY` | Clerk publishable key |
| `CLERK_SECRET_KEY` | Clerk secret key |
| `NEXT_PUBLIC_CLERK_SIGN_IN_URL` | Sign-in route (default: `/auth/signin`) |
| `NEXT_PUBLIC_CLERK_SIGN_UP_URL` | Sign-up route (default: `/auth/signup`) |
| `NEXT_PUBLIC_CLERK_AFTER_SIGN_IN_URL` | Post sign-in redirect (default: `/generate`) |
| `NEXT_PUBLIC_CLERK_AFTER_SIGN_UP_URL` | Post sign-up redirect (default: `/generate`) |

### Database (Supabase)

| Variable | Description |
|----------|-------------|
| `NEXT_PUBLIC_SUPABASE_URL` | Supabase project URL |
| `NEXT_PUBLIC_SUPABASE_ANON_KEY` | Supabase anonymous/public key |
| `SUPABASE_SERVICE_ROLE_KEY` | Supabase service role key (server-side only) |

### AI Model APIs

| Variable | Description |
|----------|-------------|
| `DEEPSEEK_V4_API_KEY` | DeepSeek V4 API key |
| `DEEPSEEK_V4_API_URL` | DeepSeek V4 API endpoint |
| `SORA_2_API_KEY` | Sora 2 API key |
| `SEEDANCE_1_5_PRO_API_KEY` | Seedance 1.5 Pro API key |
| `SEEDANCE_2_0_API_KEY` | Seedance 2.0 API key |
| `SEEDANCE_2_0_API_URL` | Seedance 2.0 API endpoint |
| `KLING_ACCESS_KEY` | Kling access key |
| `KLING_secret_KEY` | Kling secret key |
| `kling3o_key` | Kling V3 Omni API key |
| `SEEDREAM_5_API_KEY` | See Dream 5.0 API key |
| `GPT_IMAGE_API_KEY` | GPT Image API key |
| `AI_IMAGE_API_KEY` | Shared image model API key |
| `nanobanana_api_key` | Nano Banana (Google Gemini) API key |
| `VEO3_API_KEY` | Veo 3 API key |
| `MINIMAX_API_KEY` | MiniMax chat API key |

### Payments (Stripe)

| Variable | Description |
|----------|-------------|
| `NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY` | Stripe publishable key |
| `STRIPE_SECRET_KEY` | Stripe secret key |
| `STRIPE_WEBHOOK_SECRET` | Stripe webhook signing secret |
| `STRIPE_PRICE_BASIC_MONTHLY` | Stripe Price ID — Basic monthly |
| `STRIPE_PRICE_BASIC_ANNUAL` | Stripe Price ID — Basic annual |
| `STRIPE_PRICE_STANDARD_MONTHLY` | Stripe Price ID — Standard monthly |
| `STRIPE_PRICE_STANDARD_ANNUAL` | Stripe Price ID — Standard annual |
| `STRIPE_PRICE_PRO_MONTHLY` | Stripe Price ID — Pro monthly |
| `STRIPE_PRICE_PRO_ANNUAL` | Stripe Price ID — Pro annual |
| `STRIPE_PRICE_CREDITS_800` | Stripe Price ID — 800 credit pack |
| `STRIPE_PRICE_CREDITS_2000` | Stripe Price ID — 2000 credit pack |
| `STRIPE_PRICE_CREDITS_5000` | Stripe Price ID — 5000 credit pack |

### Payments (PayPal)

| Variable | Description |
|----------|-------------|
| `NEXT_PUBLIC_PAYPAL_CLIENT_ID` | PayPal client ID |
| `PAYPAL_CLIENT_SECRET` | PayPal client secret |
| `PAYPAL_WEBHOOK_ID` | PayPal webhook ID |

## Database Setup

The project uses Supabase PostgreSQL. Run the migration to create all required tables, functions, and storage:

```bash
# Apply via Supabase SQL Editor or CLI
psql <connection-string> -f supabase-migration.sql
```

### Tables

| Table | Purpose |
|-------|---------|
| `user_credits` | Per-user credit balance (default: 50 credits for new users) |
| `generation_jobs` | Video & image generation job tracking |
| `billing_payments` | Idempotent payment record tracking |

### RPC Functions

| Function | Purpose |
|----------|---------|
| `deduct_credits(p_user_id, p_amount)` | Atomic credit deduction (returns false if insufficient) |
| `refund_credits(p_user_id, p_amount)` | Refund credits back to user |
| `sync_subscription_credits(p_user_id)` | Sync subscription-based credit allocation |

### Storage

- **`user-uploads`** bucket — public read access for user-uploaded media

See [`supabase-migration.sql`](./supabase-migration.sql) for the full schema.

## API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/generate` | Submit video generation job |
| `GET` | `/api/generate/[jobId]` | Poll video job status |
| `GET` | `/api/generate/jobs` | List user's video jobs |
| `POST` | `/api/ai-image` | Submit image generation job |
| `GET` | `/api/ai-image/[jobId]` | Poll image job status |
| `GET` | `/api/ai-image/jobs` | List user's image jobs |
| `POST` | `/api/chat` | Chat with AI prompt assistant (streaming) |
| `POST` | `/api/upload` | Upload media to Supabase storage |
| `GET` | `/api/credits` | Get current user credit balance |
| `GET` | `/api/video-pricing` | Get video pricing data |
| `POST` | `/api/checkout/stripe` | Create Stripe checkout session |
| `POST` | `/api/checkout/paypal` | Create PayPal order |
| `POST` | `/api/webhooks/stripe` | Handle Stripe webhook events |
| `POST` | `/api/webhooks/paypal` | Handle PayPal webhook events |

See [`docs/api.md`](./docs/api.md) for full request/response documentation.

## Credits & Pricing

### How Credits Work

- New users receive **50 free credits**
- Credits are deducted atomically when a generation job is submitted
- If a job fails to submit, credits are automatically refunded

### Credit Costs

**Video generation** — priced by model, resolution, and duration:

| Resolution | Credits per second (fallback) |
|-----------|-------------------------------|
| 480p | 1 credit/s |
| 720p | 2 credits/s |
| 1080p | 4 credits/s |

> Exact pricing is defined per model/mode/resolution/duration in CSV pricing tables. The per-second rates above are the fallback when no CSV entry matches.

**Image generation** — **5 credits** per output image.

### Subscription Plans

| Plan | Monthly | Annual (per month) | Credits/month |
|------|---------|-------------------|---------------|
| Basic | $19.90 | $9.90 | 800 |
| Standard | $34.90 | $16.90 | 2,000 |
| Pro | $99.90 | $49.90 | 6,000 |

One-time credit packs are also available (800 / 2,000 / 5,000 credits).

## Deployment

1. Set all environment variables on your hosting platform
2. Run `npm run build` to create a production build
3. Deploy to Vercel, or any Node.js-compatible host with `npm run start`
4. Configure Stripe and PayPal webhook endpoints to point to your deployed URL
5. Submit your sitemap to Google Search Console

## Documentation

- [API Reference](./docs/api.md) — full endpoint documentation with request/response examples
- [Payment Gateway & Credits](./docs/payment-gateway-and-credits.md) — billing system architecture and credit rules
- [Database Schema](./supabase-migration.sql) — complete Supabase migration with tables, RPC functions, and RLS policies
