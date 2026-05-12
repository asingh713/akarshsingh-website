# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

A personal static HTML website hosted on GitHub Pages at **akarshsingh.com**. No build step, no framework, no package manager — files are served as-is. Deployment is automatic on push to `main` (live within ~2 minutes).

- **Git remote:** `git@github.com:asingh713/akarshsingh-website.git`
- **Branch:** `main` (GitHub Pages serves from this branch)
- **Custom domain:** Configured via `CNAME` file — do not modify it

## Deployment

```bash
git add <files>
git commit -m "message"
git push
# If rejected: git pull --rebase && git push
```

GitHub enforces branch protection but direct pushes to `main` work.

## Site Structure

Each route is a directory with an `index.html` inside it, so `akarshsingh.com/foo` maps to `foo/index.html`.

| Path | URL |
|------|-----|
| `index.html` | `/` — Coming Soon placeholder |
| `contact/index.html` | `/contact` — Contact form (Formspree) |
| `sitemap/index.html` | `/sitemap` |
| `worky/privacy/index.html` | `/worky/privacy` — Worky v3 App Store privacy policy |
| `poppy/privacy/index.html` | `/poppy/privacy` — Poppy App Store privacy policy |
| `sds-consulting/index.html` | `/sds-consulting` — SD Solutions NC (not in sitemap, not launched) |

## Design System

All pages share the exact same stack and tokens — do not deviate.

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
Card container: `rounded-xl border border-border bg-card`

Footer:
```html
<footer class="border-t border-border py-8 mt-auto">
  <div class="max-w-3xl mx-auto px-4 sm:px-6 ...">
```

## Page-Specific Notes

**Privacy pages** (`/worky/privacy`, `/poppy/privacy`):
- Header left: **"SD Solutions NC"** (links to `https://akarshsingh.com`) — not "Akarsh Singh"
- Worky uses one continuous prose block inside a single card. Poppy uses numbered sections with `<div class="h-px bg-border">` dividers inside a single card.
- Footer: `"2026 Akarsh Singh, SD Solutions NC · [App Name]"`
- These URLs are submitted to App Store Connect — do not change the paths

**Contact form** (`/contact`):
- Formspree endpoint: `https://formspree.io/f/mjgpebkg` — do not change without confirming
- JS intercepts submit and shows an inline success banner (no page reload)

**sds-consulting:** intentionally not in the sitemap and intentionally vague in copy — do not add it to the sitemap or make the copy more specific without explicit instruction.

## Hard Rules

- **No copyright symbol** — user preference
- **No emoji** in any page content
- **No dark theme** — was deliberately removed
- **Tailwind via CDN only** — no npm, no PostCSS, no build pipeline
- When adding a new app's privacy policy, use `/<appname>/privacy/index.html` and publish under "SD Solutions NC" branding
