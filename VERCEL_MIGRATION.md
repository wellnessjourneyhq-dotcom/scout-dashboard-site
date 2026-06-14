# Scout Dashboard Website — Vercel Migration Guide

The site is now a static site + a client-side interactive tool. It's ready for Vercel.
The final "connect" step happens in your Vercel account (2 minutes) — everything else is prepped.

---

## What's in this folder
- `index.html` — the full landing page + interactive "Try it with your export" tool
- `img/` — WebP product images (optimized; ~2.2 MB total, down from ~25 MB) + `logo.png`
- `vercel.json` — caching + security headers (images cached 1 year, immutable)
- `VERCEL_MIGRATION.md` — this file

No build step. No dependencies. No server. The CSV tool runs 100% in the visitor's browser —
files are never uploaded or stored anywhere.

---

## Deploy to Vercel (one-time, ~2 min)

1. Go to https://vercel.com → sign in with GitHub.
2. **Add New… → Project**.
3. Import the **scout-dashboard-site** repo (the public one).
4. Framework Preset: **Other** (it's static — Vercel auto-detects).
   - Root Directory: leave as `/`
   - Build Command: leave empty
   - Output Directory: leave empty
5. Click **Deploy**. Done — you'll get a `*.vercel.app` URL in ~20 seconds.

Every future `git push` to that repo auto-deploys. Pull requests get preview URLs.

---

## Turn on Web Analytics (do this before paid traffic)
1. In the Vercel project → **Analytics** tab → **Enable**.
2. That's it — the `/_vercel/insights/script.js` tag is already in `index.html`.
   You'll see visitors, top pages, referrers, and devices. (Free tier is plenty to start.)

Note: because checkout is on Etsy, Vercel Analytics shows landing-page behavior and
**outbound clicks to Etsy**, not completed purchases. Full purchase tracking only
becomes possible if you move checkout to Payhip/Gumroad/Shopify (the page is wired
for that — change the single `BUY_URL` constant near the bottom of index.html).

---

## Custom domain (recommended for ads)
1. Buy a domain (see CLAUDE-side shortlist; `scoutdashboard.com` or `dugoutdata.com`).
2. Vercel project → **Settings → Domains → Add** → enter the domain.
3. Follow Vercel's DNS instructions at your registrar (usually one A record or a CNAME).
   HTTPS is automatic.

---

## Updating images later
Images are referenced as **.webp**. To replace a proof screenshot:
- Save your screenshot, then convert it to webp keeping the same filename, e.g.
  `proof_03_team_dashboard.webp`, and drop it in `img/`.
- Quick convert (any PNG/JPG → webp), run from this folder:
  ```
  python -c "from PIL import Image,sys; im=Image.open('shot.png').convert('RGB'); im.save('img/proof_03_team_dashboard.webp','WEBP',quality=82,method=6)"
  ```
- Or just send me the raw screenshot and I'll convert + place it.

## Adding the demo video later
Record ~20–30s of paste → dashboard filling in, save as `img/demo.mp4`.
(The interactive tool already covers "see it work," so the video is now optional —
nice-to-have for social ads, not required.)

---

## GitHub Pages
The site is still live on GitHub Pages too. Once Vercel + a custom domain are running,
you can point all ads at the Vercel/custom-domain URL and leave Pages as a backup,
or disable it in the repo settings. No rush.
