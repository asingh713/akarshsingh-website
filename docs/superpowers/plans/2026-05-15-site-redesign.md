# Site Redesign Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Rebuild akarshsingh.com from a minimal placeholder into a professional personal site with a redesigned homepage, three new app/project pages, and updated supporting pages — all sharing the same warm amber/zinc theme.

**Architecture:** Pure static HTML, no build step. Each route is a directory with `index.html`. All pages share the same Tailwind CDN config, Plus Jakarta Sans font, and four custom color tokens. Screenshots are served from `assets/screenshots/`. No JavaScript beyond the existing contact form handler.

**Tech Stack:** HTML, Tailwind CSS (CDN), Plus Jakarta Sans (Google Fonts), Git + GitHub Pages

**Spec:** `docs/superpowers/specs/2026-05-15-site-redesign-design.md`

---

## File Map

| Action | Path | Purpose |
|--------|------|---------|
| Create dir | `assets/screenshots/` | Screenshot images for app pages |
| Copy ×6 | `assets/screenshots/worky-{1,2,3}.png` | Worky simulator screenshots |
| Copy ×6 | `assets/screenshots/peony-{1,2,3}.png` | Peony simulator screenshots |
| Rewrite | `index.html` | Homepage — hero + about |
| Create | `worky/index.html` | Worky app marketing page |
| Create | `peony/index.html` | Peony app marketing page |
| Create | `tprm/index.html` | TPRM SaaS landing page |
| Modify | `worky/privacy/index.html` | Update header/footer only |
| Modify | `contact/index.html` | Update header/footer only |
| Modify | `sitemap/index.html` | Add new pages to Apps section |
| Modify | `CLAUDE.md` | Update site structure + new pages |
| Modify | `WEBSITE_CONTEXT.md` | Update to reflect redesign |

---

## Shared HTML Boilerplate

Every page uses this exact head/body opening. Do not deviate.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>PAGE TITLE</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
  <script>
    tailwind.config = {
      theme: {
        extend: {
          fontFamily: { sans: ["Plus Jakarta Sans", "system-ui", "sans-serif"] },
          colors: {
            surface:  "#f9f8f6",
            elevated: "#f2f0ec",
            card:     "#ffffff",
            border:   "#e6e2db",
          },
        },
      },
    };
  </script>
</head>
<body class="min-h-dvh bg-surface text-zinc-700 antialiased font-sans flex flex-col" style="background-color:#f9f8f6;">
```

---

## Shared Components (copy exactly)

### Standard sticky header (homepage + inner pages with back arrow)

Homepage header (no back arrow):
```html
<header class="sticky top-0 z-50 border-b border-border bg-surface/95 backdrop-blur-md">
  <div class="max-w-3xl mx-auto px-4 sm:px-6 h-14 flex items-center justify-between">
    <a href="/" class="text-base font-extrabold text-zinc-900 tracking-tight hover:text-amber-600 transition-colors duration-200">
      Akarsh Singh
    </a>
    <a href="/contact" class="inline-flex items-center px-4 py-2 rounded-lg bg-amber-600 hover:bg-amber-500 text-white text-xs font-semibold transition-all duration-200">
      Contact
    </a>
  </div>
</header>
```

Inner page header (with back arrow, name links to `/`):
```html
<header class="sticky top-0 z-50 border-b border-border bg-surface/95 backdrop-blur-md">
  <div class="max-w-3xl mx-auto px-4 sm:px-6 h-14 flex items-center justify-between">
    <a href="/" class="text-base font-extrabold text-zinc-900 tracking-tight hover:text-amber-600 transition-colors duration-200">
      Akarsh Singh
    </a>
    <a href="/" class="inline-flex items-center gap-1.5 text-xs text-zinc-400 hover:text-zinc-700 transition-colors duration-200">
      <svg xmlns="http://www.w3.org/2000/svg" class="w-3.5 h-3.5" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="m12 19-7-7 7-7"/><path d="M19 12H5"/></svg>
      Back
    </a>
  </div>
</header>
```

SD Solutions NC header (privacy pages only — keep existing):
```html
<header class="sticky top-0 z-50 border-b border-border bg-surface/95 backdrop-blur-md">
  <div class="max-w-3xl mx-auto px-4 sm:px-6 h-14 flex items-center justify-between">
    <a href="https://akarshsingh.com" class="text-sm font-bold text-zinc-900 tracking-tight hover:text-amber-600 transition-colors duration-200">
      SD Solutions NC
    </a>
    <span class="text-xs text-zinc-400 font-medium">APP NAME — Privacy Policy</span>
  </div>
</header>
```

### Standard minimal footer (all pages)
```html
<footer class="border-t border-border py-8 mt-auto">
  <div class="max-w-3xl mx-auto px-4 sm:px-6 text-center">
    <p class="text-xs text-zinc-400">Akarsh Singh · Raleigh-Durham, NC</p>
    <a href="/sitemap" class="text-[10px] text-zinc-300 hover:text-zinc-500 transition-colors mt-1 inline-block">Sitemap</a>
  </div>
</footer>
```

Privacy page footer variant:
```html
<footer class="border-t border-border py-8 mt-auto">
  <div class="max-w-3xl mx-auto px-4 sm:px-6 flex flex-col sm:flex-row items-center justify-between gap-3 text-sm text-zinc-400">
    <span>2026 Akarsh Singh, SD Solutions NC · APP NAME</span>
    <a href="https://akarshsingh.com" class="hover:text-amber-600 transition-colors">akarshsingh.com</a>
  </div>
</footer>
```

### Section divider with label
```html
<div class="flex items-center gap-3 mb-8">
  <div class="h-px flex-1 bg-border"></div>
  <span class="text-[10px] font-semibold text-zinc-400 uppercase tracking-[0.2em]">LABEL</span>
  <div class="h-px flex-1 bg-border"></div>
</div>
```

### Photo placeholder (use until real photo provided)
```html
<div class="w-24 h-24 sm:w-28 sm:h-28 rounded-full bg-elevated border-4 border-card shadow-sm flex items-center justify-center flex-shrink-0">
  <svg class="w-10 h-10 text-zinc-300" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/></svg>
</div>
```

When real photo is provided, replace with:
```html
<img src="/assets/photo.jpg" alt="Akarsh Singh" class="w-24 h-24 sm:w-28 sm:h-28 rounded-full object-cover border-4 border-card shadow-sm flex-shrink-0">
```

---

## Task 1: Copy screenshot assets

**Files:**
- Create: `assets/screenshots/` (directory)
- Copy: 6 screenshots from Desktop

- [ ] **Step 1: Create assets directory and copy screenshots**

```bash
mkdir -p /Users/akarshsingh/Documents/Engineering_Tools/website/assets/screenshots

SS="/Users/akarshsingh/Desktop/Worky and Peony SS"
DEST="/Users/akarshsingh/Documents/Engineering_Tools/website/assets/screenshots"

cp "$SS/Simulator Screenshot - iPhone 17 Pro Max - 2026-05-15 at 18.04.23.png" "$DEST/worky-1.png"
cp "$SS/Simulator Screenshot - iPhone 17 Pro Max - 2026-05-15 at 18.04.54.png" "$DEST/worky-2.png"
cp "$SS/Simulator Screenshot - iPhone 17 Pro Max - 2026-05-15 at 18.05.03.png" "$DEST/worky-3.png"
cp "$SS/Simulator Screenshot - iPhone 17 Pro Max - 2026-05-11 at 23.17.26.png" "$DEST/peony-1.png"
cp "$SS/Simulator Screenshot - iPhone 17 Pro Max - 2026-05-11 at 23.17.43.png" "$DEST/peony-2.png"
cp "$SS/Simulator Screenshot - iPhone 17 Pro Max - 2026-05-11 at 23.17.37.png" "$DEST/peony-3.png"

ls "$DEST"
```

Expected output: 6 files listed (worky-1.png through peony-3.png)

- [ ] **Step 2: Commit**

```bash
git add assets/
git commit -m "Add app screenshot assets for Worky and Peony"
```

---

## Task 2: Rebuild `index.html` (Homepage)

**Files:**
- Rewrite: `index.html`

- [ ] **Step 1: Write the full homepage**

Write `index.html` with the complete content below. This replaces the existing "Coming Soon" page entirely.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Akarsh Singh — Cybersecurity Engineer</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
  <script>
    tailwind.config = {
      theme: {
        extend: {
          fontFamily: { sans: ["Plus Jakarta Sans", "system-ui", "sans-serif"] },
          colors: {
            surface:  "#f9f8f6",
            elevated: "#f2f0ec",
            card:     "#ffffff",
            border:   "#e6e2db",
          },
        },
      },
    };
  </script>
</head>
<body class="min-h-dvh bg-surface text-zinc-700 antialiased font-sans flex flex-col" style="background-color:#f9f8f6;">

  <header class="sticky top-0 z-50 border-b border-border bg-surface/95 backdrop-blur-md">
    <div class="max-w-3xl mx-auto px-4 sm:px-6 h-14 flex items-center justify-between">
      <a href="/" class="text-base font-extrabold text-zinc-900 tracking-tight hover:text-amber-600 transition-colors duration-200">
        Akarsh Singh
      </a>
      <a href="/contact" class="inline-flex items-center px-4 py-2 rounded-lg bg-amber-600 hover:bg-amber-500 text-white text-xs font-semibold transition-all duration-200">
        Contact
      </a>
    </div>
  </header>

  <main class="max-w-3xl mx-auto px-4 sm:px-6 py-14 flex-1 w-full">

    <!-- Hero -->
    <div class="flex items-start gap-6 sm:gap-8 mb-14">
      <!-- Photo placeholder -->
      <div class="w-24 h-24 sm:w-28 sm:h-28 rounded-full bg-elevated border-4 border-card shadow-sm flex items-center justify-center flex-shrink-0">
        <svg class="w-10 h-10 text-zinc-300" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/></svg>
      </div>

      <div class="flex-1 pt-1">
        <!-- Status badge -->
        <div class="inline-flex items-center gap-2 bg-card border border-border rounded-full px-3 py-1 mb-4">
          <span class="w-2 h-2 rounded-full bg-green-500 flex-shrink-0"></span>
          <span class="text-[10px] font-semibold text-zinc-500 uppercase tracking-widest">Cybersecurity Engineer · Raleigh-Durham, NC</span>
        </div>

        <!-- Headline -->
        <h1 class="text-2xl sm:text-3xl font-extrabold text-zinc-900 leading-tight tracking-tight mb-3">
          Threat detection.<br>
          Vulnerability management.<br>
          <span class="text-amber-600">Security that scales.</span>
        </h1>

        <!-- Tagline -->
        <p class="text-sm text-zinc-500 leading-relaxed mb-5 max-w-lg">
          4+ years securing cloud infrastructure, SaaS environments, and endpoints. I build detection coverage, run vulnerability programs, and automate the operational work that slows security teams down.
        </p>

        <!-- Cert badges -->
        <div class="flex flex-wrap gap-2">
          <span class="bg-card border border-border text-zinc-600 text-[11px] font-medium px-2.5 py-1 rounded-md">CompTIA Security+</span>
          <span class="bg-card border border-border text-zinc-600 text-[11px] font-medium px-2.5 py-1 rounded-md">CCSK v5</span>
          <span class="bg-card border border-border text-zinc-600 text-[11px] font-medium px-2.5 py-1 rounded-md">ITIL 4</span>
          <span class="bg-card border border-border text-zinc-600 text-[11px] font-medium px-2.5 py-1 rounded-md">CrowdStrike · Okta · AWS</span>
        </div>
      </div>
    </div>

    <!-- About divider -->
    <div class="flex items-center gap-3 mb-8">
      <div class="h-px flex-1 bg-border"></div>
      <span class="text-[10px] font-semibold text-zinc-400 uppercase tracking-[0.2em]">About</span>
      <div class="h-px flex-1 bg-border"></div>
    </div>

    <!-- About cards -->
    <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
      <!-- Background -->
      <div class="rounded-xl border border-border bg-card p-6">
        <p class="text-[10px] font-bold text-zinc-400 uppercase tracking-[0.14em] mb-3">Background</p>
        <p class="text-sm text-zinc-600 leading-relaxed">
          Security professional with 4+ years across endpoint security, cloud infrastructure, and compliance-driven environments. Started in device lifecycle and systems administration, grew into owning security programs end-to-end — from SIEM deployment to penetration test coordination to AI governance.
        </p>
      </div>

      <!-- Core Disciplines -->
      <div class="rounded-xl border border-border bg-card p-6">
        <p class="text-[10px] font-bold text-zinc-400 uppercase tracking-[0.14em] mb-3">Core Disciplines</p>
        <ul class="space-y-2">
          <li class="flex items-center gap-2 text-sm text-zinc-600">
            <span class="w-1.5 h-1.5 rounded-full bg-amber-500 flex-shrink-0"></span>SIEM &amp; Threat Detection
          </li>
          <li class="flex items-center gap-2 text-sm text-zinc-600">
            <span class="w-1.5 h-1.5 rounded-full bg-amber-500 flex-shrink-0"></span>Endpoint Detection &amp; Response
          </li>
          <li class="flex items-center gap-2 text-sm text-zinc-600">
            <span class="w-1.5 h-1.5 rounded-full bg-amber-500 flex-shrink-0"></span>Vulnerability Management
          </li>
          <li class="flex items-center gap-2 text-sm text-zinc-600">
            <span class="w-1.5 h-1.5 rounded-full bg-amber-500 flex-shrink-0"></span>Penetration Testing
          </li>
          <li class="flex items-center gap-2 text-sm text-zinc-600">
            <span class="w-1.5 h-1.5 rounded-full bg-amber-500 flex-shrink-0"></span>Workstation &amp; Device Management
          </li>
          <li class="flex items-center gap-2 text-sm text-zinc-600">
            <span class="w-1.5 h-1.5 rounded-full bg-amber-500 flex-shrink-0"></span>Compliance &amp; Security Frameworks
          </li>
          <li class="flex items-center gap-2 text-sm text-zinc-600">
            <span class="w-1.5 h-1.5 rounded-full bg-amber-500 flex-shrink-0"></span>Third-Party Risk Management
          </li>
          <li class="flex items-center gap-2 text-sm text-zinc-600">
            <span class="w-1.5 h-1.5 rounded-full bg-amber-500 flex-shrink-0"></span>Cloud &amp; SaaS Security
          </li>
          <li class="flex items-center gap-2 text-sm text-zinc-600">
            <span class="w-1.5 h-1.5 rounded-full bg-amber-500 flex-shrink-0"></span>AI Governance &amp; Automation
          </li>
        </ul>
      </div>
    </div>

  </main>

  <footer class="border-t border-border py-8 mt-auto">
    <div class="max-w-3xl mx-auto px-4 sm:px-6 text-center">
      <p class="text-xs text-zinc-400">Akarsh Singh · Raleigh-Durham, NC</p>
      <a href="/sitemap" class="text-[10px] text-zinc-300 hover:text-zinc-500 transition-colors mt-1 inline-block">Sitemap</a>
    </div>
  </footer>

</body>
</html>
```

- [ ] **Step 2: Verify in browser**

Open `index.html` directly in a browser (file://) or via a local server. Confirm:
- Photo placeholder circle renders
- Green dot badge shows correctly
- Hero headline has amber accent on last line
- Two about cards side-by-side on desktop, stacked on mobile
- Footer shows name + city + small Sitemap link

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "Redesign homepage with hero, about section, and professional copy"
```

---

## Task 3: Create `worky/index.html` (Worky App Page)

**Files:**
- Create: `worky/index.html`

- [ ] **Step 1: Create the directory and file**

`worky/` directory already exists (contains `privacy/`). Create `worky/index.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Worky v3 — Workout Tracker for iPhone</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
  <script>
    tailwind.config = {
      theme: {
        extend: {
          fontFamily: { sans: ["Plus Jakarta Sans", "system-ui", "sans-serif"] },
          colors: {
            surface:  "#f9f8f6",
            elevated: "#f2f0ec",
            card:     "#ffffff",
            border:   "#e6e2db",
          },
        },
      },
    };
  </script>
</head>
<body class="min-h-dvh bg-surface text-zinc-700 antialiased font-sans flex flex-col" style="background-color:#f9f8f6;">

  <header class="sticky top-0 z-50 border-b border-border bg-surface/95 backdrop-blur-md">
    <div class="max-w-3xl mx-auto px-4 sm:px-6 h-14 flex items-center justify-between">
      <a href="/" class="text-base font-extrabold text-zinc-900 tracking-tight hover:text-amber-600 transition-colors duration-200">
        Akarsh Singh
      </a>
      <a href="/" class="inline-flex items-center gap-1.5 text-xs text-zinc-400 hover:text-zinc-700 transition-colors duration-200">
        <svg xmlns="http://www.w3.org/2000/svg" class="w-3.5 h-3.5" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="m12 19-7-7 7-7"/><path d="M19 12H5"/></svg>
        Back
      </a>
    </div>
  </header>

  <main class="max-w-3xl mx-auto px-4 sm:px-6 py-14 flex-1 w-full">

    <!-- App Hero -->
    <div class="flex flex-col sm:flex-row sm:items-center gap-6 mb-10 pb-10 border-b border-border">
      <!-- Icon -->
      <div class="w-20 h-20 rounded-2xl flex items-center justify-center flex-shrink-0" style="background:linear-gradient(135deg,#f97316,#c2410c);box-shadow:0 8px 24px rgba(249,115,22,0.3);">
        <svg class="w-9 h-9" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><path d="M18 20V10"/><path d="M12 20V4"/><path d="M6 20v-6"/></svg>
      </div>
      <!-- Meta -->
      <div class="flex-1">
        <p class="text-[10px] font-bold text-amber-600 uppercase tracking-[0.16em] mb-1">iOS App · Free</p>
        <h1 class="text-3xl font-extrabold text-zinc-900 tracking-tight mb-1">Worky v3</h1>
        <p class="text-sm text-zinc-500">The no-nonsense workout tracker</p>
      </div>
      <!-- CTA -->
      <div class="flex-shrink-0">
        <a href="#" class="inline-flex items-center gap-2 px-5 py-3 rounded-xl bg-amber-600 hover:bg-amber-500 text-white text-sm font-semibold shadow-md shadow-amber-100 transition-all duration-200">
          <svg class="w-4 h-4" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 17V3"/><path d="m6 11 6 6 6-6"/><path d="M19 21H5"/></svg>
          App Store
        </a>
      </div>
    </div>

    <!-- Tagline -->
    <div class="mb-10">
      <h2 class="text-2xl font-extrabold text-zinc-900 tracking-tight leading-snug mb-3">
        Track your lifts.<br>Beat your records.
      </h2>
      <p class="text-sm text-zinc-500 leading-relaxed max-w-xl">
        Worky keeps your training data exactly where it belongs — on your device. Log workout days, track exercises by sets, reps, and weight, watch your personal records climb, and sync privately across all your Apple devices. No account. No subscription. No nonsense.
      </p>
    </div>

    <!-- Features -->
    <div class="grid grid-cols-1 sm:grid-cols-3 gap-4 mb-10">
      <div class="rounded-xl border border-border bg-card p-5">
        <div class="w-9 h-9 rounded-lg bg-amber-50 flex items-center justify-center mb-3">
          <svg class="w-4 h-4 text-amber-600" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z"/></svg>
        </div>
        <h3 class="text-sm font-bold text-zinc-900 mb-1">Personal Records</h3>
        <p class="text-xs text-zinc-500 leading-relaxed">Automatically tracks your best lifts across every exercise. See exactly when you hit a new PR.</p>
      </div>
      <div class="rounded-xl border border-border bg-card p-5">
        <div class="w-9 h-9 rounded-lg bg-amber-50 flex items-center justify-center mb-3">
          <svg class="w-4 h-4 text-amber-600" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="2" y="3" width="20" height="14" rx="2"/><path d="M8 21h8M12 17v4"/></svg>
        </div>
        <h3 class="text-sm font-bold text-zinc-900 mb-1">iCloud Sync</h3>
        <p class="text-xs text-zinc-500 leading-relaxed">Your data syncs privately across iPhone and iPad via CloudKit. No account needed.</p>
      </div>
      <div class="rounded-xl border border-border bg-card p-5">
        <div class="w-9 h-9 rounded-lg bg-amber-50 flex items-center justify-center mb-3">
          <svg class="w-4 h-4 text-amber-600" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></svg>
        </div>
        <h3 class="text-sm font-bold text-zinc-900 mb-1">Built-in Timer</h3>
        <p class="text-xs text-zinc-500 leading-relaxed">Rest timer keeps your sets on pace without leaving the app or picking up your phone.</p>
      </div>
    </div>

    <!-- Screenshots -->
    <div class="rounded-xl border border-border bg-elevated p-6 mb-6">
      <p class="text-[10px] font-bold text-zinc-400 uppercase tracking-[0.16em] mb-5">Screenshots</p>
      <div class="flex gap-4 overflow-x-auto pb-2">
        <div class="flex-shrink-0 w-36 rounded-2xl overflow-hidden border border-border shadow-sm">
          <img src="/assets/screenshots/worky-1.png" alt="Workout Days" class="w-full block">
        </div>
        <div class="flex-shrink-0 w-36 rounded-2xl overflow-hidden border border-border shadow-sm">
          <img src="/assets/screenshots/worky-2.png" alt="Dashboard" class="w-full block">
        </div>
        <div class="flex-shrink-0 w-36 rounded-2xl overflow-hidden border border-border shadow-sm">
          <img src="/assets/screenshots/worky-3.png" alt="Exercise Detail" class="w-full block">
        </div>
      </div>
    </div>

    <!-- Privacy callout -->
    <div class="rounded-xl border border-border bg-card px-6 py-4 flex flex-col sm:flex-row sm:items-center justify-between gap-3">
      <p class="text-xs text-zinc-500">Your data stays on your device — no servers, no tracking, no ads.</p>
      <a href="/worky/privacy" class="text-xs font-semibold text-amber-600 hover:text-amber-500 transition-colors whitespace-nowrap">Privacy Policy →</a>
    </div>

  </main>

  <footer class="border-t border-border py-8 mt-auto">
    <div class="max-w-3xl mx-auto px-4 sm:px-6 text-center">
      <p class="text-xs text-zinc-400">Akarsh Singh · Raleigh-Durham, NC</p>
      <a href="/sitemap" class="text-[10px] text-zinc-300 hover:text-zinc-500 transition-colors mt-1 inline-block">Sitemap</a>
    </div>
  </footer>

</body>
</html>
```

- [ ] **Step 2: Verify**

Open `worky/index.html`. Confirm:
- Orange gradient icon renders with glow shadow
- App Store button present (links to `#` for now)
- 3 feature cards in a row (stack on mobile)
- 3 screenshots visible in horizontal scroll strip
- Privacy Policy link points to `/worky/privacy`

- [ ] **Step 3: Commit**

```bash
git add worky/index.html
git commit -m "Add Worky v3 consumer app marketing page"
```

---

## Task 4: Create `peony/index.html` (Peony App Page)

**Files:**
- Create: `peony/index.html`

- [ ] **Step 1: Create the file**

`peony/` directory already exists (contains `privacy/`). Create `peony/index.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Peony — A Simple Period Tracker for iPhone</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
  <script>
    tailwind.config = {
      theme: {
        extend: {
          fontFamily: { sans: ["Plus Jakarta Sans", "system-ui", "sans-serif"] },
          colors: {
            surface:  "#f9f8f6",
            elevated: "#f2f0ec",
            card:     "#ffffff",
            border:   "#e6e2db",
          },
        },
      },
    };
  </script>
</head>
<body class="min-h-dvh bg-surface text-zinc-700 antialiased font-sans flex flex-col" style="background-color:#f9f8f6;">

  <header class="sticky top-0 z-50 border-b border-border bg-surface/95 backdrop-blur-md">
    <div class="max-w-3xl mx-auto px-4 sm:px-6 h-14 flex items-center justify-between">
      <a href="/" class="text-base font-extrabold text-zinc-900 tracking-tight hover:text-amber-600 transition-colors duration-200">
        Akarsh Singh
      </a>
      <a href="/" class="inline-flex items-center gap-1.5 text-xs text-zinc-400 hover:text-zinc-700 transition-colors duration-200">
        <svg xmlns="http://www.w3.org/2000/svg" class="w-3.5 h-3.5" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="m12 19-7-7 7-7"/><path d="M19 12H5"/></svg>
        Back
      </a>
    </div>
  </header>

  <main class="max-w-3xl mx-auto px-4 sm:px-6 py-14 flex-1 w-full">

    <!-- App Hero -->
    <div class="flex flex-col sm:flex-row sm:items-center gap-6 mb-10 pb-10 border-b border-border">
      <div class="w-20 h-20 rounded-2xl flex items-center justify-center flex-shrink-0" style="background:linear-gradient(135deg,#f43f5e,#be123c);box-shadow:0 8px 24px rgba(244,63,94,0.3);">
        <svg class="w-9 h-9" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 3a6 6 0 0 0 9 9 9 9 0 1 1-9-9Z"/></svg>
      </div>
      <div class="flex-1">
        <p class="text-[10px] font-bold text-rose-600 uppercase tracking-[0.16em] mb-1">iOS App · Free</p>
        <h1 class="text-3xl font-extrabold text-zinc-900 tracking-tight mb-1">Peony</h1>
        <p class="text-sm text-zinc-500">A simple period tracker</p>
      </div>
      <div class="flex flex-shrink-0 gap-3">
        <a href="#" class="inline-flex items-center gap-2 px-5 py-3 rounded-xl bg-amber-600 hover:bg-amber-500 text-white text-sm font-semibold shadow-md shadow-amber-100 transition-all duration-200">
          <svg class="w-4 h-4" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 17V3"/><path d="m6 11 6 6 6-6"/><path d="M19 21H5"/></svg>
          App Store
        </a>
        <a href="/peony/privacy" class="inline-flex items-center px-5 py-3 rounded-xl border border-border bg-card hover:border-amber-400 text-zinc-600 text-sm font-semibold transition-all duration-200">
          Privacy
        </a>
      </div>
    </div>

    <!-- Tagline -->
    <div class="mb-10">
      <h2 class="text-2xl font-extrabold text-zinc-900 tracking-tight leading-snug mb-3">
        Your cycle.<br>Your data. Always.
      </h2>
      <p class="text-sm text-zinc-500 leading-relaxed max-w-xl">
        Peony is a clean, private period tracker built for simplicity. Log your cycle, track symptoms and mood, get fertile window predictions, and see your full cycle history on a color-coded calendar — all stored privately on your device. No account required. Your health data never leaves your phone.
      </p>
    </div>

    <!-- Features -->
    <div class="grid grid-cols-1 sm:grid-cols-3 gap-4 mb-10">
      <div class="rounded-xl border border-border bg-card p-5">
        <div class="w-9 h-9 rounded-lg bg-rose-50 flex items-center justify-center mb-3">
          <svg class="w-4 h-4 text-rose-500" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="4" width="18" height="18" rx="2"/><path d="M16 2v4M8 2v4M3 10h18"/></svg>
        </div>
        <h3 class="text-sm font-bold text-zinc-900 mb-1">Cycle Calendar</h3>
        <p class="text-xs text-zinc-500 leading-relaxed">Color-coded calendar shows your full cycle at a glance — period days, fertile windows, and predictions.</p>
      </div>
      <div class="rounded-xl border border-border bg-card p-5">
        <div class="w-9 h-9 rounded-lg bg-rose-50 flex items-center justify-center mb-3">
          <svg class="w-4 h-4 text-rose-500" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M20.84 4.61a5.5 5.5 0 0 0-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 0 0-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 0 0 0-7.78z"/></svg>
        </div>
        <h3 class="text-sm font-bold text-zinc-900 mb-1">Mood &amp; Symptoms</h3>
        <p class="text-xs text-zinc-500 leading-relaxed">Log how you're feeling each day. Track flow intensity, symptoms, and mood in a few taps.</p>
      </div>
      <div class="rounded-xl border border-border bg-card p-5">
        <div class="w-9 h-9 rounded-lg bg-rose-50 flex items-center justify-center mb-3">
          <svg class="w-4 h-4 text-rose-500" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="11" width="18" height="11" rx="2"/><path d="M7 11V7a5 5 0 0 1 10 0v4"/></svg>
        </div>
        <h3 class="text-sm font-bold text-zinc-900 mb-1">100% Private</h3>
        <p class="text-xs text-zinc-500 leading-relaxed">No account. No ads. No tracking. Data stored locally and synced via your personal iCloud only.</p>
      </div>
    </div>

    <!-- Screenshots -->
    <div class="rounded-xl border border-border bg-elevated p-6 mb-6">
      <p class="text-[10px] font-bold text-zinc-400 uppercase tracking-[0.16em] mb-5">Screenshots</p>
      <div class="flex gap-4 overflow-x-auto pb-2">
        <div class="flex-shrink-0 w-36 rounded-2xl overflow-hidden border border-border shadow-sm">
          <img src="/assets/screenshots/peony-1.png" alt="Today View" class="w-full block">
        </div>
        <div class="flex-shrink-0 w-36 rounded-2xl overflow-hidden border border-border shadow-sm">
          <img src="/assets/screenshots/peony-2.png" alt="Calendar" class="w-full block">
        </div>
        <div class="flex-shrink-0 w-36 rounded-2xl overflow-hidden border border-border shadow-sm">
          <img src="/assets/screenshots/peony-3.png" alt="Mood Tracker" class="w-full block">
        </div>
      </div>
    </div>

    <!-- Privacy callout -->
    <div class="rounded-xl border border-border bg-card px-6 py-4 flex flex-col sm:flex-row sm:items-center justify-between gap-3">
      <p class="text-xs text-zinc-500">Health data is sensitive. Peony is built with privacy at the core.</p>
      <a href="/peony/privacy" class="text-xs font-semibold text-amber-600 hover:text-amber-500 transition-colors whitespace-nowrap">Privacy Policy →</a>
    </div>

  </main>

  <footer class="border-t border-border py-8 mt-auto">
    <div class="max-w-3xl mx-auto px-4 sm:px-6 text-center">
      <p class="text-xs text-zinc-400">Akarsh Singh · Raleigh-Durham, NC</p>
      <a href="/sitemap" class="text-[10px] text-zinc-300 hover:text-zinc-500 transition-colors mt-1 inline-block">Sitemap</a>
    </div>
  </footer>

</body>
</html>
```

- [ ] **Step 2: Verify**

Open `peony/index.html`. Confirm:
- Rose/red gradient icon with glow
- App Store + Privacy ghost button both present
- Feature icons are rose-colored (distinct from Worky's amber)
- Screenshots strip shows peony-1/2/3.png
- Privacy callout links to `/peony/privacy`

- [ ] **Step 3: Commit**

```bash
git add peony/index.html
git commit -m "Add Peony consumer app marketing page"
```

---

## Task 5: Create `tprm/index.html` (TPRM SaaS Page)

**Files:**
- Create: `tprm/index.html`
- Create: `tprm/` directory

- [ ] **Step 1: Create directory and file**

```bash
mkdir -p /Users/akarshsingh/Documents/Engineering_Tools/website/tprm
```

Then create `tprm/index.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>TPRM — Third-Party Risk Management Platform</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
  <script>
    tailwind.config = {
      theme: {
        extend: {
          fontFamily: { sans: ["Plus Jakarta Sans", "system-ui", "sans-serif"] },
          colors: {
            surface:  "#f9f8f6",
            elevated: "#f2f0ec",
            card:     "#ffffff",
            border:   "#e6e2db",
          },
        },
      },
    };
  </script>
</head>
<body class="min-h-dvh bg-surface text-zinc-700 antialiased font-sans flex flex-col" style="background-color:#f9f8f6;">

  <header class="sticky top-0 z-50 border-b border-border bg-surface/95 backdrop-blur-md">
    <div class="max-w-3xl mx-auto px-4 sm:px-6 h-14 flex items-center justify-between">
      <a href="/" class="text-base font-extrabold text-zinc-900 tracking-tight hover:text-amber-600 transition-colors duration-200">
        Akarsh Singh
      </a>
      <a href="/" class="inline-flex items-center gap-1.5 text-xs text-zinc-400 hover:text-zinc-700 transition-colors duration-200">
        <svg xmlns="http://www.w3.org/2000/svg" class="w-3.5 h-3.5" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="m12 19-7-7 7-7"/><path d="M19 12H5"/></svg>
        Back
      </a>
    </div>
  </header>

  <main class="max-w-3xl mx-auto px-4 sm:px-6 py-14 flex-1 w-full">

    <!-- App Hero -->
    <div class="flex flex-col sm:flex-row sm:items-center gap-6 mb-10 pb-10 border-b border-border">
      <div class="w-20 h-20 rounded-2xl flex items-center justify-center flex-shrink-0" style="background:linear-gradient(135deg,#b45309,#92400e);box-shadow:0 8px 24px rgba(180,83,9,0.3);">
        <svg class="w-9 h-9" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></svg>
      </div>
      <div class="flex-1">
        <p class="text-[10px] font-bold text-amber-600 uppercase tracking-[0.16em] mb-1">SaaS Platform · Live</p>
        <h1 class="text-3xl font-extrabold text-zinc-900 tracking-tight mb-1">TPRM</h1>
        <p class="text-sm text-zinc-500">Third-party risk management, simplified</p>
      </div>
      <div class="flex flex-shrink-0 gap-3">
        <a href="https://tprm.akarshsingh.com" target="_blank" rel="noopener noreferrer" class="inline-flex items-center gap-2 px-5 py-3 rounded-xl bg-amber-600 hover:bg-amber-500 text-white text-sm font-semibold shadow-md shadow-amber-100 transition-all duration-200">
          View Platform →
        </a>
        <a href="/contact" class="inline-flex items-center px-5 py-3 rounded-xl border border-border bg-card hover:border-amber-400 text-zinc-600 text-sm font-semibold transition-all duration-200">
          Get in Touch
        </a>
      </div>
    </div>

    <!-- Tagline -->
    <div class="mb-10">
      <h2 class="text-2xl font-extrabold text-zinc-900 tracking-tight leading-snug mb-3">
        Vendor risk without<br>the spreadsheet.
      </h2>
      <p class="text-sm text-zinc-500 leading-relaxed max-w-xl">
        Most TPRM programs live in spreadsheets and get reviewed once a year. This platform turns vendor risk into a living, auditable program — standardized assessments, automatic risk scoring, AI-assisted questionnaire research, and integrations that push findings where your team already works.
      </p>
    </div>

    <!-- Features -->
    <div class="grid grid-cols-1 sm:grid-cols-3 gap-4 mb-8">
      <div class="rounded-xl border border-border bg-card p-5">
        <div class="w-9 h-9 rounded-lg bg-amber-50 flex items-center justify-center mb-3">
          <svg class="w-4 h-4 text-amber-600" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="10"/><path d="M12 8v4l3 3"/></svg>
        </div>
        <h3 class="text-sm font-bold text-zinc-900 mb-1">AI-Assisted Research</h3>
        <p class="text-xs text-zinc-500 leading-relaxed">Automatically researches vendors from public sources and pre-fills assessment questionnaires using Claude AI. Cut review time dramatically.</p>
      </div>
      <div class="rounded-xl border border-border bg-card p-5">
        <div class="w-9 h-9 rounded-lg bg-amber-50 flex items-center justify-center mb-3">
          <svg class="w-4 h-4 text-amber-600" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M18 20V10"/><path d="M12 20V4"/><path d="M6 20v-6"/></svg>
        </div>
        <h3 class="text-sm font-bold text-zinc-900 mb-1">Automatic Risk Scoring</h3>
        <p class="text-xs text-zinc-500 leading-relaxed">Every submitted assessment produces a 0–100 risk score with low, medium, high, and critical thresholds — no manual calculation.</p>
      </div>
      <div class="rounded-xl border border-border bg-card p-5">
        <div class="w-9 h-9 rounded-lg bg-amber-50 flex items-center justify-center mb-3">
          <svg class="w-4 h-4 text-amber-600" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M15 17h5l-1.405-1.405A2.032 2.032 0 0 1 18 14.158V11a6.002 6.002 0 0 0-4-5.659V5a2 2 0 1 0-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 1 1-6 0v-1m6 0H9"/></svg>
        </div>
        <h3 class="text-sm font-bold text-zinc-900 mb-1">Integrations &amp; Alerts</h3>
        <p class="text-xs text-zinc-500 leading-relaxed">Jira and Slack integrations built in. Automatic notifications for upcoming review dates, high-risk findings, and completed AI research.</p>
      </div>
    </div>

    <!-- Why it exists -->
    <div class="rounded-xl border border-border bg-card p-6 mb-8">
      <p class="text-[10px] font-bold text-zinc-400 uppercase tracking-[0.14em] mb-3">Built from real experience</p>
      <p class="text-sm text-zinc-600 leading-relaxed">
        This platform came from running TPRM programs in production — the kind where vendors pile up in a spreadsheet, review dates slip, and nobody knows which ones are actually high-risk until something goes wrong. TPRM centralizes vendor assessments, enforces consistent evaluation criteria, and uses AI to do the research legwork so your team can focus on decisions, not data entry.
      </p>
    </div>

    <!-- Tech strip -->
    <div class="grid grid-cols-2 sm:grid-cols-4 gap-3">
      <div class="rounded-lg border border-border bg-card px-4 py-3 text-center">
        <p class="text-xs font-bold text-zinc-900 mb-0.5">React + Node.js</p>
        <p class="text-[10px] text-zinc-400">Full-stack</p>
      </div>
      <div class="rounded-lg border border-border bg-card px-4 py-3 text-center">
        <p class="text-xs font-bold text-zinc-900 mb-0.5">PostgreSQL</p>
        <p class="text-[10px] text-zinc-400">Structured data</p>
      </div>
      <div class="rounded-lg border border-border bg-card px-4 py-3 text-center">
        <p class="text-xs font-bold text-zinc-900 mb-0.5">Role-Based Access</p>
        <p class="text-[10px] text-zinc-400">Admin / Standard / Viewer</p>
      </div>
      <div class="rounded-lg border border-border bg-card px-4 py-3 text-center">
        <p class="text-xs font-bold text-zinc-900 mb-0.5">Self-Hosted</p>
        <p class="text-[10px] text-zinc-400">DigitalOcean + Docker</p>
      </div>
    </div>

  </main>

  <footer class="border-t border-border py-8 mt-auto">
    <div class="max-w-3xl mx-auto px-4 sm:px-6 text-center">
      <p class="text-xs text-zinc-400">Akarsh Singh · Raleigh-Durham, NC</p>
      <a href="/sitemap" class="text-[10px] text-zinc-300 hover:text-zinc-500 transition-colors mt-1 inline-block">Sitemap</a>
    </div>
  </footer>

</body>
</html>
```

- [ ] **Step 2: Verify**

Open `tprm/index.html`. Confirm:
- Amber/brown gradient shield icon
- "View Platform →" links to `https://tprm.akarshsingh.com`
- "Get in Touch" links to `/contact`
- 3 feature cards present
- "Built from real experience" card renders
- Tech strip shows 4 items in 2x2 grid on mobile, 4-col on desktop

- [ ] **Step 3: Commit**

```bash
git add tprm/
git commit -m "Add TPRM SaaS landing page"
```

---

## Task 6: Update `worky/privacy/index.html` (Header/Footer only)

**Files:**
- Modify: `worky/privacy/index.html`

The privacy policy content (prose) does NOT change. Only update the header to match the new name size, and ensure the footer matches the standard privacy footer pattern. The URL `/worky/privacy` must not change.

- [ ] **Step 1: Update the header `<a>` name size**

In `worky/privacy/index.html`, find the header name link and update the font size to match new site style:

Old:
```html
<a href="https://akarshsingh.com" class="text-sm font-bold text-zinc-900 tracking-tight hover:text-amber-600 transition-colors duration-200">
  SD Solutions NC
</a>
```

New:
```html
<a href="https://akarshsingh.com" class="text-base font-extrabold text-zinc-900 tracking-tight hover:text-amber-600 transition-colors duration-200">
  SD Solutions NC
</a>
```

- [ ] **Step 2: Ensure footer matches privacy footer pattern**

Footer should be:
```html
<footer class="border-t border-border py-8 mt-auto">
  <div class="max-w-3xl mx-auto px-4 sm:px-6 flex flex-col sm:flex-row items-center justify-between gap-3 text-sm text-zinc-400">
    <span>2026 Akarsh Singh, SD Solutions NC &middot; Worky v3</span>
    <a href="https://akarshsingh.com" class="hover:text-amber-600 transition-colors">akarshsingh.com</a>
  </div>
</footer>
```

- [ ] **Step 3: Commit**

```bash
git add worky/privacy/index.html
git commit -m "Update Worky privacy page header to match site redesign"
```

---

## Task 7: Update `contact/index.html` (Header/Footer)

**Files:**
- Modify: `contact/index.html`

Form, fields, and Formspree endpoint (`https://formspree.io/f/mjgpebkg`) do NOT change.

- [ ] **Step 1: Update header name size**

Find the header `<a>` with "Akarsh Singh" and update class to match:

```html
<a href="/" class="text-base font-extrabold text-zinc-900 tracking-tight hover:text-amber-600 transition-colors duration-200">
  Akarsh Singh
</a>
```

- [ ] **Step 2: Update footer to use standard minimal footer with sitemap link**

Replace existing footer with:
```html
<footer class="border-t border-border py-8 mt-auto">
  <div class="max-w-3xl mx-auto px-4 sm:px-6 text-center">
    <p class="text-xs text-zinc-400">Akarsh Singh · Raleigh-Durham, NC</p>
    <a href="/sitemap" class="text-[10px] text-zinc-300 hover:text-zinc-500 transition-colors mt-1 inline-block">Sitemap</a>
  </div>
</footer>
```

- [ ] **Step 3: Commit**

```bash
git add contact/index.html
git commit -m "Update contact page header/footer to match site redesign"
```

---

## Task 8: Update `sitemap/index.html`

**Files:**
- Modify: `sitemap/index.html`

- [ ] **Step 1: Update header name size**

Same as contact — update the `<a>` with "Akarsh Singh" in the header:
```html
<a href="/" class="text-base font-extrabold text-zinc-900 tracking-tight hover:text-amber-600 transition-colors duration-200">
  Akarsh Singh
</a>
```

- [ ] **Step 2: Add new pages to the Apps section**

Find the Apps `<ul>` block and replace it with:
```html
<ul class="space-y-3">
  <li>
    <a href="/worky" class="group flex items-center justify-between">
      <span class="text-sm text-zinc-700 group-hover:text-amber-600 transition-colors">Worky v3</span>
      <span class="text-xs text-zinc-400 group-hover:text-zinc-600 transition-colors">akarshsingh.com/worky</span>
    </a>
  </li>
  <li class="border-t border-border pt-3">
    <a href="/worky/privacy" class="group flex items-center justify-between">
      <span class="text-sm text-zinc-700 group-hover:text-amber-600 transition-colors">Worky v3 — Privacy Policy</span>
      <span class="text-xs text-zinc-400 group-hover:text-zinc-600 transition-colors">akarshsingh.com/worky/privacy</span>
    </a>
  </li>
  <li class="border-t border-border pt-3">
    <a href="/peony" class="group flex items-center justify-between">
      <span class="text-sm text-zinc-700 group-hover:text-amber-600 transition-colors">Peony</span>
      <span class="text-xs text-zinc-400 group-hover:text-zinc-600 transition-colors">akarshsingh.com/peony</span>
    </a>
  </li>
  <li class="border-t border-border pt-3">
    <a href="/peony/privacy" class="group flex items-center justify-between">
      <span class="text-sm text-zinc-700 group-hover:text-amber-600 transition-colors">Peony — Privacy Policy</span>
      <span class="text-xs text-zinc-400 group-hover:text-zinc-600 transition-colors">akarshsingh.com/peony/privacy</span>
    </a>
  </li>
  <li class="border-t border-border pt-3">
    <a href="/tprm" class="group flex items-center justify-between">
      <span class="text-sm text-zinc-700 group-hover:text-amber-600 transition-colors">TPRM</span>
      <span class="text-xs text-zinc-400 group-hover:text-zinc-600 transition-colors">akarshsingh.com/tprm</span>
    </a>
  </li>
</ul>
```

- [ ] **Step 3: Update footer to standard minimal footer**

```html
<footer class="border-t border-border py-8 mt-auto">
  <div class="max-w-3xl mx-auto px-4 sm:px-6 text-center">
    <p class="text-xs text-zinc-400">Akarsh Singh · Raleigh-Durham, NC</p>
    <a href="/sitemap" class="text-[10px] text-zinc-300 hover:text-zinc-500 transition-colors mt-1 inline-block">Sitemap</a>
  </div>
</footer>
```

- [ ] **Step 4: Commit**

```bash
git add sitemap/index.html
git commit -m "Update sitemap with new app pages and consistent header/footer"
```

---

## Task 9: Update CLAUDE.md and WEBSITE_CONTEXT.md

**Files:**
- Modify: `CLAUDE.md`
- Modify: `WEBSITE_CONTEXT.md`

- [ ] **Step 1: Update CLAUDE.md site structure table**

Replace the existing site structure table with:

```markdown
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
```

Also update the header note to reflect the homepage is no longer "Coming Soon":
```markdown
A personal site and portfolio for Akarsh Singh, Cybersecurity Engineer. Hosted on GitHub Pages at **akarshsingh.com**.
```

- [ ] **Step 2: Update WEBSITE_CONTEXT.md**

Update the following sections:
- Site tree: add `worky/index.html`, `peony/index.html`, `tprm/index.html`, `assets/screenshots/`
- Pages: update `/` description from "Coming Soon" to full homepage spec
- Pages: add `/worky`, `/peony`, `/tprm` entries
- Pending work: remove "Full personal site" item (done), add "Add real photo to homepage when provided"
- Last updated: May 2026

- [ ] **Step 3: Commit**

```bash
git add CLAUDE.md WEBSITE_CONTEXT.md
git commit -m "Update CLAUDE.md and WEBSITE_CONTEXT.md to reflect full site redesign"
```

---

## Task 10: Final push and verify live

- [ ] **Step 1: Push to GitHub**

```bash
git push
```

Expected: GitHub Pages deploys within ~2 minutes.

- [ ] **Step 2: Verify live pages**

Check each URL in a browser after ~2 minutes:
- `https://akarshsingh.com` — homepage hero + about
- `https://akarshsingh.com/worky` — Worky app page with screenshots
- `https://akarshsingh.com/peony` — Peony app page with screenshots
- `https://akarshsingh.com/tprm` — TPRM SaaS page
- `https://akarshsingh.com/worky/privacy` — unchanged prose, updated header
- `https://akarshsingh.com/peony/privacy` — unchanged
- `https://akarshsingh.com/contact` — form still works
- `https://akarshsingh.com/sitemap` — all new pages listed

- [ ] **Step 3: Smoke test contact form**

Submit the contact form with a test message. Verify it routes to Formspree without errors and shows the inline success banner.

- [ ] **Step 4: Check screenshot images load**

On `/worky` and `/peony`, confirm all 3 screenshot images load (not broken). If any 404, re-check paths — images must be at `/assets/screenshots/worky-1.png` etc.
