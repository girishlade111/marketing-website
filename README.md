# Marketing Website (BaseHub Template)

A fully-featured, production-ready **marketing website** for startups and SaaS products, built on the [BaseHub](https://basehub.com) CMS. It ships with a homepage, blog, changelog, documentation-style dynamic pages, text search, newsletter forms, dark/light mode, analytics, and SEO best practices — with all content editable visually from BaseHub.

> Based on the official BaseHub marketing-website template.

## What it does

- **Landing page** — hero, logos, features, testimonials, pricing, FAQ sections, all CMS-driven
- **Blog** — list + detail pages with RSS feed (`/blog/rss.xml`)
- **Changelog** — release-notes listing with RSS feed (`/changelog/rss.xml`)
- **Dynamic pages** — catch-all `[[...slug]]` routes render any CMS page type
- **Text search** — full-text search powered by BaseHub
- **Newsletter & contact forms** — server-action-backed forms
- **Dark/light mode** toggle, analytics integrations, social links
- SEO-ready: Open Graph/Twitter metadata, sitemap-friendly structure

## Features

- All copy, images, and page structure editable in the BaseHub dashboard — no redeploys for content changes
- Draft mode support (preview unpublished CMS content)
- Responsive, mobile-first design
- Modular `_sections` components (each homepage section is a self-contained component)
- shadcn/ui-based design system with Tailwind CSS

## Tech stack

- **Next.js** 15 (App Router, SSR/ISR)
- **React** 19
- **TypeScript**
- **BaseHub CMS** (`basehub` SDK + `basehub.config.ts` schema)
- **Tailwind CSS** + **shadcn/ui** (Radix UI primitives)
- **lucide-react** icons
- **Vercel Analytics** integration points

## Quick start

Prerequisites: Node.js 18+ and npm; a free [BaseHub](https://basehub.com) account.

```bash
npm install
```

Create `.env.local` and add your BaseHub token:

```txt
# .env.local
BASEHUB_TOKEN=<your-basehub-token>
```

Start the dev server:

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000).

### Production build

```bash
npm run build
npm run start
```

## Project structure

```
├── app/
│   ├── [[...slug]]/       # CMS-driven dynamic pages
│   ├── blog/              # Blog list, [slug] detail, rss.xml route
│   ├── changelog/         # Changelog list, [slug] detail, rss.xml route
│   ├── _sections/         # Homepage building blocks (hero, pricing, FAQ, forms, ...)
│   └── layout.tsx         # Root layout, metadata, BaseHub draft-mode toolbar
├── basehub.config.ts      # BaseHub schema (pages, blog, changelog collections)
├── components/            # Shared + shadcn/ui components
├── context/               # React context providers
├── hooks/                 # React hooks
├── lib/                   # Utilities
└── public/                # Static assets
```

## Environment variables

| Variable        | Required | Description                                   |
|-----------------|----------|-----------------------------------------------|
| `BASEHUB_TOKEN` | Yes      | BaseHub API token (create one in your BaseHub project dashboard). Keeps the site connected to its CMS content. |

The token is used server-side only; never expose it in client code.

## Deployment notes

- This is a **dynamic SSR app** — it needs a Node.js host (Vercel, Netlify, or a VPS), not a static host.
- It requires the `BASEHUB_TOKEN` secret at build/run time (the CMS is fetched at build time for static pages and at request time for drafts).
- Static export (`output: 'export'`) is **not supported** for this template: it relies on server actions (forms/newsletter), draft mode/cookies, and dynamic search.
- Recommended: one-click deploy to Vercel with the BaseHub integration, or any platform that supports Next.js SSR.

---

Built by Girish Lade — https://ladestack.in
