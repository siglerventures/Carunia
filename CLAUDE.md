# Carunia — conventions for Claude Code (read before editing)

Public website for **Carunia Children's Home** (Visakhapatnam, India), a
nonprofit mission of The Living Church, Boise, Idaho. Single static
`index.html` (no build step, no backend), hosted on GitHub Pages from
`main` / root at https://siglerventures.github.io/Carunia/.

## Versioning — SINGLE SOURCE OF TRUTH
- The version is defined ONCE: `<meta name="app-rev" content="X.Y">` near the
  top of `index.html`. The footer version is filled from it at runtime.
  NEVER hard-code the version anywhere else.
- The cache-bust bootstrap reads the same meta tag (localStorage key
  `carunia_lastRev`) and forces a one-time `?v={rev}` reload.
- **Every change to `index.html` MUST bump the meta tag** (e.g. 1.7 → 1.8).
  Bumping it is how we confirm the new page is actually live.

## Multi-agent coordination (IMPORTANT — more than one bot works here)
- Several Claude Code sessions may push to `main` concurrently.
- ALWAYS `git pull --rebase origin main` immediately before every push.
  If the push is rejected, rebase again — never force-push `main`.
- After a rebase, re-check the `app-rev` meta tag: if the other session
  already took your intended number, bump to the next one.
- Deploys go straight from `main` — every push publishes. Keep commits
  self-contained and working.

## Content & assets
- Photos live in `images/` as web-optimized JPEGs (~200 KB, max ~1600px
  wide). Never commit multi-MB originals — resize/compress first.
  Current set: `ChildrensHome.jpg` (hero — has the site title baked into
  the photo, so don't overlay duplicate title text), `food.jpg`,
  `School.jpg`, `play.jpg`, `schoolforgirls.jpg` (unused so far).
- Filenames are case-sensitive on GitHub Pages.
- SEO matters: keep the meta description, canonical URL, Open Graph /
  Twitter tags, and the NGO JSON-LD block in sync with content changes,
  and update `sitemap.xml` (lastmod + image entries) when pages/images
  change.
- Contact email: `thelivingchurchboise@gmail.com`.

## Pull-request hygiene
- This repo deploys from `main`; small fixes may be committed directly.
- Never create a PR unless asked; flag any force-push of a shared branch.
