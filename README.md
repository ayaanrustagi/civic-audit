# Civic Audit — GitHub Pages bundle (DRAFT, NOT PUBLISHED)

Static site for "Citizen Portal and the public record" by Ayaan Rustagi.
Built 18 Nov 2026 from the latest repo copy (`latest/site/`, generated from `data/parsed/results.json`, 10:26 AM CST).

**Status:** findings are AI reference labels awaiting Ayaan's confirmation. A red "Draft — findings pending author
confirmation; not yet published" banner is pinned to the top, the title starts with [DRAFT], and the page carries
`noindex, nofollow`. Citizen Portal's reply window runs through 30 Nov 2026; do not publish before 1 Dec 2026.

## What's here
- `index.html` — the whole site (CSS/JS inline)
- `data.json` — study data (the "Download study data" link); names of members of the public and students are already withheld
- `assets/fonts/` — self-hosted fonts (OFL licences included)
- `assets/media/` — EMPTY: the five decorative photos (`church.webp`, `leander.webp`, `depot.webp`, `log-house.webp`,
  `lake-cover-enhanced.webp`) live in `site/media/` on Ayaan's Mac and were not copied. The page hides them if missing.
- `.nojekyll` — tells GitHub Pages to serve files as-is

## Before publishing (Ayaan)
1. Confirm or reject the flagged facts in `review/index.html`; rerun `python3 -m civicaudit.pipeline report` so numbers reflect your decisions, and rebuild this bundle from the new `site/`.
2. Copy `site/media/*.webp` into `assets/media/`.
3. Remove the draft banner: delete the `<div class="draft-banner" ...>...</div>` right after `<body>`, the
   `<meta name="robots" content="noindex, nofollow">` line, and `[DRAFT] ` from `<title>`.
4. Wait until 1 Dec 2026 and fold in any Citizen Portal reply.

## Publish steps (only after the above)
```bash
cd pages
git init -b main
git add -A
git commit -m "Civic audit site"
gh repo create civic-audit --public --source=. --remote=origin --push   # or create the repo on github.com and:
# git remote add origin https://github.com/<user>/civic-audit.git && git push -u origin main
```
Then on GitHub: repo → Settings → Pages → Build and deployment → Source: "Deploy from a branch" →
Branch: `main`, folder `/ (root)` → Save. The site appears at `https://<user>.github.io/civic-audit/` within a few minutes.

Preview locally: `cd pages && python3 -m http.server 8000` → http://localhost:8000
