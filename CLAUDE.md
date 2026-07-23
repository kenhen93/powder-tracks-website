# CLAUDE.md — powder-tracks-website

Marketing site for PowderTracks (Android ski-tracking app). Static
HTML/CSS/JS on Cloudflare Pages at https://powdertracks.com, deployed by
GitHub Actions on push to `main`. This repo is SEPARATE from the app
repo (`powder-tracks`) — never assume app code is present here.

## Non-negotiable facts (source of truth for all copy)

- Premium is a **ONE-TIME purchase — $19.99, yours for life. There is
  no subscription and never will be.** Never write "/year", "/month",
  "trial", or "plan". This is the product's core differentiator vs
  Ski Tracks and Slopes; say it plainly and often.
- Cloud backup cap: **1 GB** (a decade of skiing ≈ 33 MB). Additional
  storage will be sellable later — also one-time. Don't invent tiers.
- The invariant still holds internally — **all local data stays free
  forever; premium gates delighters, not data; we never hold user data
  hostage** — but DO NOT print that sentence verbatim on the site. Express
  it in plain words instead. And the site MUST always carry the "free
  means local / lost phone" warning near the free-vs-premium comparison:
  on the free app history lives only on the phone, so if the phone is lost
  or broken the data goes with it — export a GPX copy now and then, or let
  premium's cloud backup keep an encrypted copy safe. (Currently a
  `.callout` at the bottom of index.html's #whats-included and in
  pricing.html's "Your data, your rules" section.)
- **Free forever:** live GPS tracking, full session/run history and
  stats, GPX + Ski Tracks (.skiz) import, and GPX export. (No .skiz
  export exists; batch import and full-fidelity GPX export are premium.)
- **Premium ($19.99 once):** cloud backup (1 GB) + restore on a new
  phone, run scores / Top Runs / Records / season recaps, live stats on
  Wear OS watches, heart rate & calories (Health Connect), pass value
  tracking, Strava upload, batch import.
- Purchases happen **in-app via Google Play only**. The website is
  informational — no checkout, no payment forms, ever.
- Platform: **Android (Google Play)**. An iOS/Apple Watch version is in
  development — do not promise it, link it, or give dates. App Store
  badges stay commented out until it ships.

## Brand

- Dark theme to match the app: near-black surfaces (#121212–#1d1d1d),
  cards #2C2C2C-ish, light text.
- **Brand orange is `#E07028`** (extracted from the logo master). The
  old `#FF6B35` in early files is wrong — replace on sight.
- Assets come from the app repo's `assets/images/` (snowflake mark with
  transparency, `wordmark_white.png` / `wordmark_orange.png`). Copy
  them into `images/` here; never hotlink, never restyle or recolor the
  marks.
- Strava assets: only official brand-kit files, unmodified ("Powered by
  Strava" / "Compatible with Strava"). Never the bare Strava glyph,
  never Strava in our own branding.
- Screenshots are real app captures (Pixel, ~1179×2556). No mockups
  passed off as screenshots, no fabricated data in shots.

## Voice

- Plain, confident, skier-to-skier. No growth-hack tone, no urgency, no
  countdowns, no dark patterns, no fake testimonials, no invented
  ratings or user counts.
- Positive framing only (mirrors the app rule): describe what free
  includes and what premium adds — never "free users can't…".
- The origin story is fair game and effective: built because the
  incumbent apps moved a skier's own history behind subscriptions.
  State it without naming-and-shaming beyond facts.

## Privacy & terms pages (launch requirement — Google Play listing
links to privacy.html)

privacy.html must stay ACCURATE to the real architecture; when in doubt
understate:
- Local-first: tracking data lives on the device; no account needed to
  use the app.
- Premium only: email (Supabase auth), an entitlement record, and the
  user's encrypted backup file stored in Backblaze B2 keyed by account
  id. That is the complete server-side data inventory.
- Strava: optional; only sessions the user explicitly uploads.
- Health Connect: heart-rate/calorie data stays on device (required
  disclosure for Play's Health Connect policy).
- **No ads, no analytics, no trackers, no cookies, no data sale** — on
  the site AND in the app. This repo must contain zero analytics
  snippets; the "add analytics" TODO is rejected permanently.
- Account deletion removes entitlement record and backup blob.
- Include a contact email and a "last updated" date; bump the date on
  any material change.
  terms.html: one-time license, refunds per Google Play policy, plain
  no-warranty language, Colorado/US governing-law placeholder.

## Tech rules

- Pure static: hand-written HTML/CSS/JS. **No frameworks, no npm
  dependencies, no build step.** If a page needs a build tool, the
  design is wrong.
- Mobile-first, fast: no webfonts beyond system stack or one
  self-hosted file; images compressed; decorative JS (snow animation)
  must be `prefers-reduced-motion`-aware and never block content.
- Every page: proper title/meta description, OpenGraph tags with a real
  preview image, working footer links (Privacy · Terms · Contact).
- Relative links only (site must work on *.pages.dev previews and the
  custom domain).

## Deploy

- GitHub Actions → `wrangler pages deploy . --project-name=powdertracks`
  on push to `main`. Secrets: `CLOUDFLARE_API_TOKEN`,
  `CLOUDFLARE_ACCOUNT_ID`. No other CI.
- Custom domain powdertracks.com is attached in the Cloudflare Pages
  dashboard (this also owns the apex DNS records — don't add
  conflicting records for `@` or `www` elsewhere in the zone).
- Verify locally by opening index.html in a browser before pushing;
  there is no staging beyond Pages preview deployments.

## Working agreements

- Small, reviewable commits; one concern per commit.
- Never invent product facts, prices, dates, or platform promises not
  listed above — if copy needs a fact this file doesn't have, ASK
  instead of guessing.
- When app facts change (price, roster, cap), update THIS file in the
  same commit as the copy change so it stays the source of truth.