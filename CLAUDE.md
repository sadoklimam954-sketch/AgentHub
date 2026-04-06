# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**AgentHub** is a white-label AI customer support SaaS targeted at French web agencies. The concept: agencies deploy an AI agent (powered by Claude API + RAG) for their clients, branded as their own, and sell it at 49–199€/month per client.

This repo is currently a **static HTML proof-of-concept** — two self-contained files with no build system, no dependencies, and no backend.

## Files

- `agent-support-whitelabel.html` — Marketing landing page for agencies
- `index.html` — 4-step pricing funnel + signup flow (plan selection → account creation → payment → dashboard)

## Running

Open either `.html` file directly in a browser. No server, build, or install step required.

## Design System

Both files share an embedded CSS design system:

- **Colors:** dark background (`#0a0d0a`), green accent (`#4ade80`), orange secondary (`#f97316`)
- **Typography:** "Playfair Display" (headings) + "Outfit" (body), loaded from Google Fonts
- **Animations:** `fadeUp`, `popIn`, `bounce`, `spin` keyframes; scroll-reveal via `IntersectionObserver`

## Architecture of `index.html` (Funnel)

Client-side multi-page flow driven by a single `state` object:

```js
const state = { plan, price, prenom, agence }
```

Navigation between pages (`#page1` through `#page4`) is done by toggling CSS visibility — no routing library. Key JS behaviors:
- Plan selection updates state and syncs the right-side summary card
- Real-time form validation on the signup and payment pages
- Card number formatting (groups of 4) + brand detection (Visa/MC/Amex by first digit)
- 14-day trial end-date calculation displayed before payment
- Mock payment processing with loading state, then reveal of `#page4`
- Bar chart built from hardcoded conversation data on the dashboard
- Setup wizard tracks 3 steps (import docs → branding → deploy) with progress bar

## Planned Full Stack (documented in the landing page)

| Layer | Technologies |
|-------|-------------|
| Frontend | Next.js 14, React, TailwindCSS, Vercel |
| AI/RAG | Claude API, Pinecone, LangChain, OpenAI Embeddings |
| Backend | Node.js, Prisma, PostgreSQL, Redis |
| Infra/Auth | Supabase, AWS S3, Cloudflare, Railway |
| Payments | Stripe Subscriptions |

## Pricing Tiers

| Plan | Price | Agents | Conv/month |
|------|-------|--------|------------|
| Starter | 49€ | 1 | 500 |
| Pro | 99€ | 3 | 2,000 |
| Agence+ | 199€ | Unlimited | 5,000 |

## Language

All user-facing content is in **French**.
