# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

A personal site and portfolio for Akarsh Singh, Cybersecurity Engineer. Hosted on GitHub Pages at **akarshsingh.com**. No build step, no framework, no package manager — files are served as-is. Deployment is automatic on push to `main` (live within ~2 minutes).

- **Git remote:** `https://github.com/asingh713/akarshsingh-website.git` (HTTPS — SSH keys not configured)
- **Branch:** `main` (GitHub Pages serves from this branch)
- **Custom domain:** Configured via `CNAME` file — do not modify it

## Deployment

```bash
git add <files>
git commit -m "message"
git push
# If rejected: git pull --rebase && git push
```

GitHub enforces branch protection but direct pushes to `main` work. Committer name warnings about auto-configured identity are cosmetic only.

## Site Structure

Each route is a directory with an `index.html` inside it, so `akarshsingh.com/foo` maps to `foo/index.html`.

| Path | URL |
|------|-----|
| `index.html` | `/` — Homepage (hero + about) |
| `contact/index.html` | `/contact` — Contact form (Formspree) |
| `sitemap/index.html` | `/sitemap` |
| `worky/index.html` | `/worky` — Worky v3 app marketing page |
| `worky/privacy/index.html` | `/worky/privacy` — Worky v3 App Store privacy policy |
| `peony/index.html` | `/peony` — Peony app marketing page |
| `peony/privacy/index.html` | `/peony/privacy` — Peony App Store privacy policy |
| `tprm/index.html` | `/tprm` — TPRM SaaS landing page |
| `sds-consulting/index.html` | `/sds-consulting` — SD Solutions NC (not in sitemap, not launched) |
| `assets/screenshots/` | Static screenshot images for app pages |

## Design System

**All pages must use the same tokens and color scheme.** Do not introduce per-page custom palettes.

**Stack:** Tailwind CSS via CDN (`https://cdn.tailwindcss.com`) + Plus Jakarta Sans from Google Fonts (weights 400, 500, 600, 700, 800). No other dependencies.

**Custom color tokens** (defined inline in each page's `<script>` block):
```js
colors: {
  surface:  "#f9f8f6",  // page background
  elevated: "#f2f0ec",  // subtle section backgrounds
  card:     "#ffffff",  // card/panel backgrounds
  border:   "#e6e2db",  // borders
}
```

**Body:** `class="min-h-dvh bg-surface text-zinc-700 antialiased font-sans flex flex-col"` + `style="background-color: #f9f8f6;"` (flat, no gradient)

**Key recurring patterns:**

Sticky header:
```html
<header class="sticky top-0 z-50 border-b border-border bg-surface/95 backdrop-blur-md">
  <div class="max-w-3xl mx-auto px-4 sm:px-6 h-14 flex items-center justify-between">
```

Primary button: `bg-amber-600 hover:bg-amber-500 text-white`
Secondary/ghost button: `border border-border bg-card hover:border-amber-400`
Accent text/labels: `text-amber-600`
Links: `text-amber-600 hover:text-amber-500 underline underline-offset-2`
Card container: `rounded-xl border border-border bg-card`

Footer:
```html
<footer class="border-t border-border py-8 mt-auto">
  <div class="max-w-3xl mx-auto px-4 sm:px-6 ...">
```

## Page-Specific Notes

**Privacy pages** (`/worky/privacy`, `/peony/privacy`):
- Header left: **"SD Solutions NC"** (links to `https://akarshsingh.com`) — not "Akarsh Singh"
- Worky uses one continuous prose block inside a single card
- Peony uses numbered sections (1–10) with `<div class="h-px bg-border">` dividers inside a single card
- Footer: `"2026 Akarsh Singh, SD Solutions NC · [App Name]"`
- These URLs are submitted to App Store Connect — do not change the paths
  - Worky: `https://akarshsingh.com/worky/privacy`
  - Peony: `https://akarshsingh.com/peony/privacy`

**App pages** (`/worky`, `/peony`, `/tprm`):
- Header: "Akarsh Singh" (text-base font-extrabold) left, back arrow right
- Consumer-focused: app hero with gradient icon, tagline, 3 feature cards, screenshot strip, privacy/CTA callout
- App Store links currently placeholder (`href="#"`) — update when apps are published
- TPRM links to `https://tprm.akarshsingh.com` (live)
- Screenshots served from `assets/screenshots/` — worky-1/2/3.png and peony-1/2/3.png

**Contact form** (`/contact`):
- Formspree endpoint: `https://formspree.io/f/mjgpebkg` — do not change without confirming
- JS intercepts submit and shows an inline success banner (no page reload)

**sds-consulting:** intentionally not in the sitemap and intentionally vague in copy — do not add it to the sitemap or make the copy more specific without explicit instruction.

## Hard Rules

- **No copyright symbol** — user preference
- **No emoji** in any page content
- **No dark theme** — was deliberately removed, do not revert
- **No per-page custom color palettes** — all pages share the amber/zinc/warm-surface theme
- **Tailwind via CDN only** — no npm, no PostCSS, no build pipeline
- When adding a new app's privacy policy, use `/<appname>/privacy/index.html`, publish under "SD Solutions NC" branding, and add it to the sitemap
- **Photo placeholder** — homepage uses an SVG avatar circle at `assets/photo.jpg` path; swap in `<img src="/assets/photo.jpg">` when a real photo is provided
