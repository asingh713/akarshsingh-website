# Homepage Redesign — Dark Split-Screen

**Date:** 2026-05-19
**Status:** Approved
**File:** `index.html`

---

## Goal

Redesign the homepage from a warm light theme to a dark, sophisticated split-screen layout. Make the photo more prominent, replace the marketing-copy headline with a direct biographical statement, and retheme to charcoal dark.

---

## Layout

**Desktop — two-column split (50/50):**
- Left panel: full-height fixed photo, `object-cover`, blends into right panel via a right-edge gradient vignette (`from-transparent to-#111111`)
- Right panel: scrollable content column, constrained width, comfortable padding

**Mobile — stacked:**
- Photo collapses to a full-width top banner (~40vh), `object-cover object-top`
- Content stacks below as a single column

No sticky header — name lives inside the right panel content.

---

## Colors

| Token | Value | Use |
|-------|-------|-----|
| `surface` | `#111111` | Page + right panel background |
| `card` | `#1e1e1e` | Cards, badge backgrounds |
| `border` | `#2a2a2a` | All borders, dividers |
| `accent` | `#d97706` (amber-600) | Buttons, highlights, dots |
| Text primary | `#f0f0f0` | Headings, name |
| Text muted | `#888888` | Secondary text, badge labels |

Left-edge vignette on photo: `linear-gradient(to right, transparent 60%, #111111 100%)`

---

## Right Panel Content (top to bottom)

1. **Name** — `"Akarsh Singh"`, large (`text-3xl font-extrabold`), `#f0f0f0`
2. **Headline** — `"Cybersecurity engineer with 4+ years protecting workstations, cloud infrastructure, and SaaS environments."` — single sentence, `text-base`, muted (`#888`)
3. **Status badge** — green dot + `"Raleigh-Durham, NC"` — dark card background
4. **Cert/tool badges** — `Security+`, `CCSK v5`, `ITIL 4`, `CrowdStrike · Okta · AWS` — dark card style
5. **Divider** — labeled `"Background"`, hairline `#2a2a2a`
6. **Background prose** — existing copy, `text-sm #888`
7. **Divider** — labeled `"Core Disciplines"`
8. **Disciplines list** — 9 items, amber dot bullets, `text-sm #f0f0f0`
9. **Footer** — `"Akarsh Singh · Raleigh-Durham, NC"` + sitemap link, bottom of scroll

---

## Contact Button

Amber pill in the right panel below the headline (not in a header). Same amber style as rest of site.

---

## Photo

`/assets/photo.jpg` — full-bleed left panel on desktop, banner on mobile. No border-radius on desktop panel (edge-to-edge). `object-position: top` to favor face framing.

---

## What Does NOT Change

- Font: Plus Jakarta Sans, same weights
- Amber accent color: `#d97706` / `bg-amber-600`
- Content copy (background prose, disciplines list)
- Cert/tool badge content
- `/contact` link destination
- Footer text

---

## Hard Rules (carried forward)

- No copyright symbol
- No emoji
- Tailwind CDN only — no build step
- Dark theme is now the design — do not revert to light
