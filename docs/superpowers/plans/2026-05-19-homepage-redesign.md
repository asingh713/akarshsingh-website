# Homepage Redesign — Dark Split-Screen Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Rebuild `index.html` as a dark charcoal split-screen layout with a full-height left photo panel and scrollable right content panel.

**Architecture:** Single HTML file, no build step. Tailwind CSS via CDN with inline config for custom dark tokens. Left panel is `position: fixed` on desktop, collapses to a `40vh` top banner on mobile. Right panel contains all content and scrolls independently.

**Tech Stack:** HTML5, Tailwind CSS (CDN), Plus Jakarta Sans (Google Fonts), no JS changes required.

---

### Task 1: Update Tailwind config and body for dark theme

**Files:**
- Modify: `index.html` (lines 12–27 — `<script>` Tailwind config block and `<body>` tag)

- [ ] **Step 1: Replace Tailwind color tokens and body class**

Replace the existing `tailwind.config` script block and `<body>` tag with:

```html
  <script>
    tailwind.config = {
      theme: {
        extend: {
          fontFamily: { sans: ["Plus Jakarta Sans", "system-ui", "sans-serif"] },
          colors: {
            surface:  "#111111",
            card:     "#1e1e1e",
            border:   "#2a2a2a",
          },
        },
      },
    };
  </script>
```

And update the `<body>` tag to:

```html
<body class="min-h-dvh bg-surface text-[#f0f0f0] antialiased font-sans" style="background-color:#111111;">
```

- [ ] **Step 2: Open `index.html` in a browser and verify**

The page should now have a near-black `#111111` background. Existing text will appear light-coloured. Layout will be broken — that's expected, structure changes come next.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "style: switch to dark charcoal theme tokens"
```

---

### Task 2: Build the split-screen shell

**Files:**
- Modify: `index.html` — replace everything inside `<body>` with the two-panel shell

- [ ] **Step 1: Replace body content with split-screen shell**

Remove the existing `<header>`, `<main>`, and `<footer>` tags entirely. Replace with:

```html
<!-- Split layout wrapper -->
<div class="flex min-h-dvh">

  <!-- LEFT PANEL — fixed photo (desktop) / top banner (mobile) -->
  <div class="hidden md:block md:w-1/2 lg:w-5/12 fixed top-0 left-0 h-full">
    <img
      src="/assets/photo.jpg"
      alt="Akarsh Singh"
      class="w-full h-full object-cover object-top"
    >
    <!-- right-edge vignette to blend into content panel -->
    <div class="absolute inset-0" style="background: linear-gradient(to right, transparent 55%, #111111 100%);"></div>
  </div>

  <!-- Mobile photo banner (hidden on md+) -->
  <div class="md:hidden w-full h-[40vh] relative flex-shrink-0">
    <img
      src="/assets/photo.jpg"
      alt="Akarsh Singh"
      class="w-full h-full object-cover object-top"
    >
    <div class="absolute inset-0" style="background: linear-gradient(to bottom, transparent 50%, #111111 100%);"></div>
  </div>

  <!-- RIGHT PANEL — scrollable content -->
  <div class="w-full md:w-1/2 lg:w-7/12 md:ml-auto flex flex-col min-h-dvh">
    <!-- content goes here in Task 3 -->
  </div>

</div>
```

- [ ] **Step 2: Verify in browser**

On desktop (≥768px): left half should show the photo, right half should be dark `#111111`. On mobile: photo banner at top, dark content area below.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add split-screen shell with fixed photo panel"
```

---

### Task 3: Build right panel — hero section

**Files:**
- Modify: `index.html` — fill in the right panel content area (replace the `<!-- content goes here -->` comment)

- [ ] **Step 1: Add hero content inside the right panel**

Replace `<!-- content goes here in Task 3 -->` with:

```html
    <main class="flex-1 px-8 sm:px-12 pt-16 pb-12">

      <!-- Name -->
      <h1 class="text-3xl sm:text-4xl font-extrabold text-[#f0f0f0] tracking-tight mb-3">
        Akarsh Singh
      </h1>

      <!-- Headline -->
      <p class="text-base text-[#888888] leading-relaxed mb-6 max-w-md">
        Cybersecurity engineer with 4+ years protecting workstations, cloud infrastructure, and SaaS environments.
      </p>

      <!-- Status badge -->
      <div class="inline-flex items-center gap-2 bg-card border border-border rounded-full px-3 py-1 mb-5">
        <span class="w-2 h-2 rounded-full bg-green-500 flex-shrink-0"></span>
        <span class="text-[10px] font-semibold text-[#888888] uppercase tracking-widest">Raleigh-Durham, NC</span>
      </div>

      <!-- Contact button -->
      <div class="mb-6">
        <a href="/contact" class="inline-flex items-center px-5 py-2.5 rounded-lg bg-amber-600 hover:bg-amber-500 text-white text-sm font-semibold transition-all duration-200">
          Contact
        </a>
      </div>

      <!-- Cert / tool badges -->
      <div class="flex flex-wrap gap-2 mb-12">
        <span class="bg-card border border-border text-[#888888] text-[11px] font-medium px-2.5 py-1 rounded-md">CompTIA Security+</span>
        <span class="bg-card border border-border text-[#888888] text-[11px] font-medium px-2.5 py-1 rounded-md">CCSK v5</span>
        <span class="bg-card border border-border text-[#888888] text-[11px] font-medium px-2.5 py-1 rounded-md">ITIL 4</span>
        <span class="bg-card border border-border text-[#888888] text-[11px] font-medium px-2.5 py-1 rounded-md">CrowdStrike &middot; Okta &middot; AWS</span>
      </div>

    </main>
```

- [ ] **Step 2: Verify in browser**

Right panel should show: name in large white text, muted headline, green dot badge, amber Contact button, dark cert badges. No layout breakage on mobile.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add right panel hero — name, headline, badge, contact, certs"
```

---

### Task 4: Build right panel — about sections and footer

**Files:**
- Modify: `index.html` — add background + disciplines sections inside `<main>`, and footer below `<main>`

- [ ] **Step 1: Add about sections inside `<main>` after the cert badges div (before the closing `</main>`)**

```html
      <!-- Background divider -->
      <div class="flex items-center gap-3 mb-6">
        <div class="h-px flex-1 bg-border"></div>
        <span class="text-[10px] font-semibold text-[#555555] uppercase tracking-[0.2em]">Background</span>
        <div class="h-px flex-1 bg-border"></div>
      </div>

      <!-- Background prose -->
      <p class="text-sm text-[#888888] leading-relaxed mb-10 max-w-md">
        Security professional with 4+ years across endpoint security, cloud infrastructure, and compliance-driven environments. Started in device lifecycle and systems administration, grew into owning security programs end-to-end &mdash; from SIEM deployment to penetration test coordination to AI governance.
      </p>

      <!-- Core Disciplines divider -->
      <div class="flex items-center gap-3 mb-6">
        <div class="h-px flex-1 bg-border"></div>
        <span class="text-[10px] font-semibold text-[#555555] uppercase tracking-[0.2em]">Core Disciplines</span>
        <div class="h-px flex-1 bg-border"></div>
      </div>

      <!-- Disciplines list -->
      <ul class="space-y-2.5 max-w-md">
        <li class="flex items-center gap-2.5 text-sm text-[#f0f0f0]">
          <span class="w-1.5 h-1.5 rounded-full bg-amber-500 flex-shrink-0"></span>SIEM &amp; Threat Detection
        </li>
        <li class="flex items-center gap-2.5 text-sm text-[#f0f0f0]">
          <span class="w-1.5 h-1.5 rounded-full bg-amber-500 flex-shrink-0"></span>Endpoint Detection &amp; Response
        </li>
        <li class="flex items-center gap-2.5 text-sm text-[#f0f0f0]">
          <span class="w-1.5 h-1.5 rounded-full bg-amber-500 flex-shrink-0"></span>Vulnerability Management
        </li>
        <li class="flex items-center gap-2.5 text-sm text-[#f0f0f0]">
          <span class="w-1.5 h-1.5 rounded-full bg-amber-500 flex-shrink-0"></span>Penetration Testing
        </li>
        <li class="flex items-center gap-2.5 text-sm text-[#f0f0f0]">
          <span class="w-1.5 h-1.5 rounded-full bg-amber-500 flex-shrink-0"></span>Workstation &amp; Device Management
        </li>
        <li class="flex items-center gap-2.5 text-sm text-[#f0f0f0]">
          <span class="w-1.5 h-1.5 rounded-full bg-amber-500 flex-shrink-0"></span>Compliance &amp; Security Frameworks
        </li>
        <li class="flex items-center gap-2.5 text-sm text-[#f0f0f0]">
          <span class="w-1.5 h-1.5 rounded-full bg-amber-500 flex-shrink-0"></span>Third-Party Risk Management
        </li>
        <li class="flex items-center gap-2.5 text-sm text-[#f0f0f0]">
          <span class="w-1.5 h-1.5 rounded-full bg-amber-500 flex-shrink-0"></span>Cloud &amp; SaaS Security
        </li>
        <li class="flex items-center gap-2.5 text-sm text-[#f0f0f0]">
          <span class="w-1.5 h-1.5 rounded-full bg-amber-500 flex-shrink-0"></span>AI Governance &amp; Automation
        </li>
      </ul>
```

- [ ] **Step 2: Add footer after the closing `</main>` tag (still inside the right panel `<div>`)**

```html
    <footer class="px-8 sm:px-12 py-8 border-t border-border">
      <p class="text-xs text-[#555555]">Akarsh Singh &middot; Raleigh-Durham, NC</p>
      <a href="/sitemap" class="text-[10px] text-[#444444] hover:text-[#888888] transition-colors mt-1 inline-block">Sitemap</a>
    </footer>
```

- [ ] **Step 3: Verify full page in browser**

Scroll down the right panel — Background prose, Core Disciplines list, footer should all appear. Left photo stays fixed on desktop. Mobile stacks correctly.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add background, disciplines, and footer to right panel"
```

---

### Task 5: Update CLAUDE.md and WEBSITE_CONTEXT.md to reflect dark theme

**Files:**
- Modify: `CLAUDE.md`
- Modify: `WEBSITE_CONTEXT.md`

- [ ] **Step 1: Update the Hard Rules section in `CLAUDE.md`**

Change:
```
- **No dark theme** — was deliberately removed, do not revert
```
To:
```
- **Dark theme** — site uses charcoal dark (`#111111` surface, `#1e1e1e` cards, `#2a2a2a` borders). Do not revert to light theme.
```

Update the Design System color tokens block:
```js
colors: {
  surface:  "#111111",  // page background
  card:     "#1e1e1e",  // card/panel backgrounds
  border:   "#2a2a2a",  // borders
}
```

- [ ] **Step 2: Update Design System section in `WEBSITE_CONTEXT.md`**

Replace the colors block:
```js
colors: {
  surface:  "#111111",   // page background
  card:     "#1e1e1e",   // card/panel backgrounds
  border:   "#2a2a2a",   // borders
}
```

Update body background note:
```
**Body background:** `background-color: #111111;` (flat dark charcoal)
**Body text color:** `text-[#f0f0f0]`
**Secondary/muted text:** `text-[#888888]` or `text-[#555555]`
```

Update the Homepage section to reflect split-screen layout and new heading.

Update Key Decisions to remove the "dark theme deliberately removed" note and replace with "site is dark charcoal — do not revert to light."

- [ ] **Step 3: Commit**

```bash
git add CLAUDE.md WEBSITE_CONTEXT.md
git commit -m "docs: update design system docs to reflect dark charcoal theme"
```

---

### Task 6: Push and verify live

**Files:** none

- [ ] **Step 1: Push to GitHub**

```bash
git push
```

Expected output: `main -> main` with no errors.

- [ ] **Step 2: Wait ~2 minutes, then verify at https://akarshsingh.com**

Check:
- Dark charcoal background on both panels
- Photo fills left half on desktop, top banner on mobile
- Name, headline, badge, contact button, certs all render correctly
- Background + disciplines sections visible on scroll
- Footer at bottom of right panel
- No layout breakage on mobile (test by resizing browser to <768px)
