# Site Redesign — Design Spec
_2026-05-15_

## Overview

Full redesign of akarshsingh.com from a minimal "Coming Soon" placeholder into a professional personal site for Akarsh Singh, a Cybersecurity Engineer. Direction: Warm & Structured — same amber/zinc/warm-surface palette, significantly more depth and content. No additional dependencies beyond what already exists (Tailwind CDN, Plus Jakarta Sans).

---

## Design System (unchanged tokens)

```js
colors: { surface: "#f9f8f6", elevated: "#f2f0ec", card: "#ffffff", border: "#e6e2db" }
```
Accent: `amber-600` (#b45309). Body: `text-zinc-700`. Headings: `text-zinc-900`. All hard rules from CLAUDE.md apply: no emoji, no copyright symbol, no dark theme.

---

## Pages to Build / Update

### 1. `/` — Homepage (full rebuild)

**Header (sticky):**
- Left: "Akarsh Singh" — larger than current, `font-size: ~18px`, `font-weight: 800`
- Right: amber "Contact" button only — no nav links

**Hero section:**
- Left: circular photo (`assets/photo.jpg` — placeholder SVG avatar until real photo provided)
- Right column:
  - Green dot badge: "Cybersecurity Engineer · Raleigh-Durham, NC"
  - H1 (scaled, ~26–28px): "Threat detection. Vulnerability management. Security that scales." — amber accent on last line
  - Tagline paragraph (~13px): 4+ years, cloud infra, SaaS, endpoints, detection coverage, vulnerability programs, automation
  - Cert/tool badges: CompTIA Security+, CCSK v5, ITIL 4, CrowdStrike · Okta · AWS

**About section (labeled divider → two-column cards):**
- Left card: "Background" — prose paragraph covering 4+ years, endpoint → cloud → programs, SIEM/pentest/AI governance
- Right card: "Core Disciplines" — amber dot list:
  - SIEM & Threat Detection
  - Endpoint Detection & Response
  - Vulnerability Management
  - Penetration Testing
  - Workstation & Device Management
  - Compliance & Security Frameworks
  - Third-Party Risk Management
  - Cloud & SaaS Security
  - AI Governance & Automation

**Footer (minimal, centered):**
- "Akarsh Singh · Raleigh-Durham, NC"
- Small faint "Sitemap" link below

---

### 2. `/worky` — Worky v3 App Page (NEW)

Consumer-focused marketing page.

**Header:** "Akarsh Singh" left, back arrow right

**App hero (flex row):**
- Orange gradient icon (bar chart SVG), box-shadow glow
- Name: "Worky v3", sub: "The no-nonsense workout tracker", label: "iOS App · Free"
- CTA: "Download on App Store →" (amber button) — links to App Store (URL TBD, use `#` for now)

**Tagline:** "Track your lifts. Beat your records." + consumer description paragraph

**Features (3-col grid):**
1. Personal Records — auto-tracks best lifts per exercise
2. iCloud Sync — private CloudKit sync, no account needed
3. Built-in Timer — rest timer without leaving app

**Screenshots strip:** worky-1.png (Workout Days), worky-2.png (Dashboard/PRs), worky-3.png (Exercise Detail)
- Images stored in `assets/screenshots/`
- Displayed as rounded phone frames with shadow

**Privacy callout bar:** "Your data stays on your device — no servers, no tracking, no ads." + "Privacy Policy →" link to `/worky/privacy`

**Footer:** same minimal pattern

---

### 3. `/peony` — Peony App Page (NEW)

Consumer-focused marketing page. Same structure as Worky, adapted.

**App hero:**
- Rose/red gradient icon (moon+stars SVG matching app branding)
- Name: "Peony", sub: "A simple period tracker", label: "iOS App · Free"
- CTAs: "Download on App Store →" (amber) + "Privacy Policy" (ghost) — privacy links to `/peony/privacy`

**Tagline:** "Your cycle. Your data. Always." + consumer description

**Features:**
1. Cycle Calendar — color-coded, period/fertile/prediction days
2. Mood & Symptoms — flow intensity, symptoms, mood logging
3. 100% Private — no account, no ads, local + iCloud only

**Screenshots:** peony-1.png (Today/home), peony-2.png (Calendar), peony-3.png (Mood picker)

**Privacy callout:** "Health data is sensitive. Peony is built with privacy at the core." + Privacy Policy link

---

### 4. `/tprm` — TPRM SaaS Tool Page (NEW)

Business-focused SaaS landing page. Slightly longer than app pages.

**App hero:**
- Amber/brown gradient shield icon
- Name: "TPRM", sub: "Third-Party Risk Management, simplified", label: "SaaS · Live"
- CTAs: "View Live Platform →" (links to tprm.akarshsingh.com) + "Contact for Access" (ghost, links to /contact)

**Tagline:** "Vendor risk without the spreadsheet." + business-focused pitch: compliance teams, security-driven vendor reviews, AI-assisted questionnaire auto-fill

**Features (3-col):**
1. AI-Assisted Research — auto-fills vendor questionnaires from public sources using Claude AI
2. Risk Scoring — 0–100 risk score with low/medium/high/critical thresholds, automatic on submission
3. Integrations — Jira and Slack built in; notifications on review dates, flags, completed research

**Why it exists section (full-width card):**
Short paragraph: "Most TPRM programs live in spreadsheets and get reviewed once a year. This platform turns vendor risk into a living, auditable program — assessments, scoring, AI research, and integrations in one place."

**Tech callout strip (4 items):**
- React + Node.js — modern full-stack
- PostgreSQL + Prisma — structured, auditable data
- Role-based access — admin / standard / viewer
- DigitalOcean — self-hosted, production-ready

**Footer:** same minimal pattern

---

### 5. `/worky/privacy` — Keep URL, update theming

Already at correct URL (submitted to Apple). Update to match new site header style:
- Header: "SD Solutions NC" left (links to akarshsingh.com), "Worky v3 — Privacy Policy" right
- Content: existing prose (unchanged)
- Footer: "2026 Akarsh Singh, SD Solutions NC · Worky v3"

---

### 6. `/peony/privacy` — Already updated

Theming already matches site. No changes needed.

---

### 7. `/contact` — Restyle to match new header/footer

- Header: "Akarsh Singh" left (larger, matching homepage), back arrow right
- Form: unchanged (Formspree endpoint stays)
- Footer: matching minimal style

---

### 8. `/sitemap` — Add new pages

Add to Apps section:
- Peony — Privacy Policy (already added)
- Worky v3 → `/worky`
- Peony → `/peony`
- TPRM → `/tprm`

---

## Assets

Screenshots copied to `assets/screenshots/`:
- `worky-1.png` — Workout Days home screen
- `worky-2.png` — Dashboard with Personal Records
- `worky-3.png` — Exercise detail (Chest & Triceps)
- `peony-1.png` — Today/home with cycle wheel
- `peony-2.png` — Calendar with color-coded dots
- `peony-3.png` — Mood picker grid

Photo: `assets/photo.jpg` — placeholder SVG circle avatar until user provides real photo.

---

## Build Sequence

1. Create `assets/screenshots/` and copy all 6 images
2. Build `index.html` (homepage)
3. Build `worky/index.html`
4. Build `peony/index.html`
5. Build `tprm/index.html`
6. Update `worky/privacy/index.html` (header/footer only)
7. Update `contact/index.html` (header/footer)
8. Update `sitemap/index.html` (add new pages)
9. Update `CLAUDE.md` and `WEBSITE_CONTEXT.md`
10. Commit and push
