# PowderTracks Website

Marketing site for **PowderTracks** — the ski & snowboard tracking app you
buy once and own for life. No subscription, no ads, no trackers.

🌐 **Live:** https://powdertracks.com

Pure static HTML/CSS. No framework, no build step, no dependencies, no
JavaScript. Deploys to Cloudflare Pages via GitHub Actions on every push
to `main`.

## Pages

| File           | Purpose                                                            |
| -------------- | ----------------------------------------------------------------- |
| `index.html`   | Landing page — hero, the free story, free vs premium, download    |
| `premium.html` | Every premium feature, all inside the one-time $19.99             |
| `pricing.html` | One-time purchase explained + the data-freedom promise            |
| `privacy.html` | Real privacy policy, accurate to the app architecture             |
| `terms.html`   | One-time license, refunds, no-warranty terms                      |
| `styles.css`   | Shared stylesheet (dark theme, brand orange `#E07028`)            |
| `favicon.svg`  | Inline snowflake favicon (no external request)                    |
| `images/`      | Brand marks + app icon; `images/screens/` holds app screenshots   |

## Local preview

No tooling required — just open the file:

```bash
open index.html      # macOS
xdg-open index.html  # Linux
```

Links are relative, so it works from the filesystem, on `*.pages.dev`
preview URLs, and on the custom domain alike.

## Screenshots

The feature sections reference real app captures (Pixel, ~1179×2556).

Home (`index.html`) — the free story:

```
images/screens/live-tracking.png
images/screens/history.png
images/screens/import-export.png
```

Premium (`premium.html`):

```
images/screens/run-score.png
images/screens/wear-os.png
images/screens/heart-rate.png
images/screens/pass-value.png
images/screens/cloud-backup.png
images/screens/strava.png
```

Until those PNGs are added, the slots show a labelled placeholder frame.
Drop in the real files with those exact names and they appear
automatically — the layout already reserves the correct aspect ratio, so
there's no layout shift.

## Deployment

Every push to `main` runs `.github/workflows/deploy-website.yml`, which
publishes the repo root to Cloudflare Pages:

```
wrangler pages deploy . --project-name=powdertracks --branch=main
```

### One-time setup

**1. Create the Pages project** (once)

- Cloudflare dashboard → **Workers & Pages → Create → Pages**.
- Create a project named **`powdertracks`** (Direct Upload is fine — the
  GitHub Action does the uploading; you don't need to connect the repo in
  the dashboard).

**2. Add the GitHub secrets**

In the repo: **Settings → Secrets and variables → Actions → New repository
secret**. Add both:

| Secret                  | Where to find it                                                         |
| ----------------------- | ------------------------------------------------------------------------ |
| `CLOUDFLARE_API_TOKEN`  | Cloudflare → **My Profile → API Tokens → Create Token**. Use the **Cloudflare Pages → Edit** permission (Account scope). |
| `CLOUDFLARE_ACCOUNT_ID` | Cloudflare dashboard → **Workers & Pages** → right sidebar → **Account ID**. |

**3. Push to `main`**

```bash
git add .
git commit -m "Publish PowderTracks site"
git push origin main
```

The Action deploys in ~30 seconds. You can also trigger it manually from
the **Actions** tab (**Run workflow**).

### Manual deploy (optional)

```bash
npm install -g wrangler
wrangler login
wrangler pages deploy . --project-name=powdertracks
```

## Custom domain — powdertracks.com

Attach the domain in the Pages dashboard (this also manages the apex DNS,
so **don't** add conflicting `@`/`www` records elsewhere in the zone):

1. Cloudflare dashboard → **Workers & Pages → `powdertracks` → Custom
   domains → Set up a custom domain**.
2. Enter **`powdertracks.com`** and follow the prompt. If the domain is on
   Cloudflare, the DNS records are created for you automatically.
3. (Optional) Add **`www.powdertracks.com`** the same way if you want
   `www` to resolve too.
4. Wait for the domain status to show **Active** and TLS to provision
   (usually a minute or two). Cloudflare issues the certificate.

If the domain's registrar/DNS is elsewhere, point its nameservers to
Cloudflare (or add the `CNAME` target Pages shows you) before step 2.

## Ground rules

- **No subscription language, ever.** Premium is one-time — $19.99, yours
  for life. Never write "/month", "/year", "trial", or "plan".
- **No analytics, trackers, cookies, or ad snippets** — on the site or in
  the app. This is permanent; don't add them.
- Keep `privacy.html` accurate to the real architecture (see `CLAUDE.md`
  for the source-of-truth facts).
- Relative links only; system fonts only; images compressed.

---

© 2026 PowderTracks · Built for skiers & riders 🏔️
