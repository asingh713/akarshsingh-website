# Website Project Context
**Last updated:** April 2026
**Repo:** github.com/asingh713/akarshsingh-website
**Live site:** https://akarshsingh.com
**Hosting:** GitHub Pages (custom domain via CNAME file)
**Deployment:** Auto-deploys on push to `main`. Pages typically go live within 1–2 minutes.

---

## Site Structure

```
website/
├── index.html                    → akarshsingh.com/            (Coming Soon homepage)
├── contact/
│   └── index.html                → akarshsingh.com/contact      (Contact form)
├── sitemap/
│   └── index.html                → akarshsingh.com/sitemap      (Sitemap)
├── worky/
│   └── privacy/
│       └── index.html            → akarshsingh.com/worky/privacy (Worky v3 privacy policy)
├── sds-consulting/
│   └── index.html                → akarshsingh.com/sds-consulting (SD Solutions NC landing page)
├── CNAME                         → akarshsingh.com (custom domain config)
├── README.md
└── WEBSITE_CONTEXT.md            (this file)
```

---

## Design System

All pages share the same design system. Do not deviate from these without updating all pages.

**Framework:** Tailwind CSS (CDN — `https://cdn.tailwindcss.com`)
**Font:** Plus Jakarta Sans (Google Fonts) — weights 400, 500, 600, 700, 800
**Theme:** Light/warm

**Custom Tailwind colors (defined inline in each page's `<script>` block):**
```js
colors: {
  surface:  "#f9f8f6",   // page background
  elevated: "#f2f0ec",   // subtle section backgrounds
  card:     "#ffffff",   // card/panel backgrounds
  border:   "#e6e2db",   // borders
}
```

**Body background:** `background-color: #f9f8f6;` (flat, no gradient — clean light look)
**Body text color:** `text-zinc-700`
**Heading color:** `text-zinc-900`
**Secondary/muted text:** `text-zinc-500` or `text-zinc-400`
**Accent color:** Amber — buttons use `bg-amber-600 hover:bg-amber-500`, labels use `text-amber-600`
**Card borders:** `border border-border bg-card` — white cards on the warm background
**Left-border accent on service cards:** `border-l-4 border-l-amber-500/60`

**Sticky header pattern:**
```html
<header class="sticky top-0 z-50 border-b border-border bg-surface/95 backdrop-blur-md">
  <div class="max-w-[3xl or 4xl] mx-auto px-4 sm:px-6 h-14 flex items-center justify-between">
```

**Primary button:**
```html
class="inline-flex items-center gap-2 px-6 py-3 rounded-lg bg-amber-600 hover:bg-amber-500 text-white text-sm font-semibold shadow-md shadow-amber-100 transition-all duration-200"
```

**Secondary/ghost button:**
```html
class="inline-flex items-center gap-2 px-6 py-3 rounded-lg border border-border bg-card hover:border-amber-400 hover:text-zinc-900 text-zinc-600 text-sm font-semibold transition-all duration-200"
```

**Section divider with label:**
```html
<div class="flex items-center gap-3 mb-8">
  <div class="h-px flex-1 bg-border"></div>
  <span class="text-[10px] font-semibold text-zinc-400 uppercase tracking-[0.2em]">Label</span>
  <div class="h-px flex-1 bg-border"></div>
</div>
```

**Footer pattern (minimal):**
```html
<footer class="py-8 mt-auto text-center border-t border-border">
  <p class="text-xs text-zinc-400">Name · Raleigh-Durham, NC</p>
</footer>
```

---

## Pages — Current State

### `/` — Homepage (`index.html`)
- "Coming Soon" page — the main personal site is not built out yet
- Shows: name, tagline ("Something new is on the way"), three buttons: LinkedIn, GitHub, Contact
- Footer: minimal — "Akarsh Singh · Raleigh-Durham, NC" + small Sitemap link
- Header: none (no sticky nav on this page)
- **Status:** Placeholder. Full personal site to be built at a later date.

### `/contact` — Contact Page
- Contact form with Name, Email, Message fields
- Form submits to Formspree: `https://formspree.io/f/mjgpebkg`
- Subject line hidden field: `Contact — akarshsingh.com`
- JS intercepts submit, shows green success banner inline (no page reload)
- Social links below form: LinkedIn, GitHub
- Header left: "Akarsh Singh" (links to `/`), right: Back arrow

### `/sitemap` — Sitemap
- Three sections: Pages (Home, Contact, Sitemap), Apps (Worky v3 Privacy Policy), Elsewhere (LinkedIn, GitHub)
- Each row: page name left, full URL right, amber hover on both
- Header left: "Akarsh Singh", right: Back arrow

### `/worky/privacy` — Worky v3 Privacy Policy
- Written as **one continuous block of prose** (not separate card sections)
- All content in a single `rounded-xl border border-border bg-card` container
- Branding throughout: **Worky v3**, creator: **Akarsh Singh, SD Solutions NC**
- Header left: **"SD Solutions NC"** (links to akarshsingh.com), right: "Worky v3 — Privacy Policy"
- Footer: "2026 Akarsh Singh, SD Solutions NC · Worky v3"
- Required by App Store Connect for Sign in with Apple / Sign in with Google
- **Privacy policy covers:**
  - Data stored locally via SwiftData; iCloud sync via CloudKit (private, end-to-end)
  - Sign in with Apple: anonymized identifier only, stored in Keychain
  - Sign in with Google: display name + email only, stored locally/iCloud, never on Worky servers
  - One outbound network request: exercise name search to wger.de (no personal info included)
  - No tracking, no IDFA, no analytics SDKs, no third-party data sharing
  - Data deletion: Settings → Sign Out removes all data
  - Not directed at children under 13
  - Changes posted at this URL with updated date

### `/sds-consulting` — SD Solutions NC Consulting Page
- **NOT in the sitemap** (intentional — not officially launched yet)
- Separate business identity: **SD Solutions NC** — small business IT consulting
- Header: "SD Solutions NC" on left, "Get in Touch" button on right (links to `/contact`)
- Footer: "SD Solutions NC · Raleigh-Durham, NC"
- **Target audience:** Small businesses under 15 employees (restaurants, retail, salons, medical/dental, law/accounting, startups)
- **Tone:** Professional, brief, welcoming — intentionally vague to not filter out potential clients
- CTA box uses `bg-amber-50 border-amber-200` (amber-tinted light background) to stand out
- **Four service cards** (left amber border accent):
  1. Setup & Installation — networking, devices, POS, configured from day one
  2. Staff Training — hands-on, plain language, stay until questions are done
  3. AI & Workflow Optimization — smart tools that fit how the business actually runs
  4. Ongoing Support — direct access, no ticket systems
- **CTA section:** "Not sure if this is a fit? Reach out anyway." — explicitly lowers the barrier to contact
- **When ready to launch:** Add to sitemap, optionally push to a separate domain

---

## Key Decisions & Conventions

- **No copyright symbol** — user preference, do not add `©`
- **No emoji** in any page content
- **Formspree endpoint:** `https://formspree.io/f/mjgpebkg` — do not change without confirming with user
- **Privacy page header says "SD Solutions NC"** — not "Akarsh Singh" — because Worky v3 is published under SD Solutions NC
- **Consulting page is intentionally vague** — prior versions were too specific about pain points and industries, which the user felt would deter people who didn't match exactly. Keep copy high-level and encouraging.
- **sds-consulting is NOT in the sitemap** — keep it this way until user decides it's ready to promote
- **Dark theme was deliberately removed** — user found it "depressing." Do not revert to dark.
- **Light theme CTA section** on consulting page uses `bg-amber-50 border border-amber-200` instead of a dark gradient

---

## Deployment Notes

- **Git remote:** `git@github.com:asingh713/akarshsingh-website.git`
- **Branch:** `main` (GitHub Pages serves from this branch)
- **Workflow:** Edit files → `git add` → `git commit` → `git push`
- **Custom domain:** Configured via `CNAME` file containing `akarshsingh.com`
- **DNS:** Managed externally — do not touch CNAME file
- If push is rejected (remote ahead), run: `git pull --rebase && git push`
- GitHub enforces branch protection ("Changes must be made through a pull request") but it is bypassed — pushes to main work directly.

---

## Pending / Future Work

- **Full personal site** — `index.html` is still a "Coming Soon" placeholder. The full personal portfolio/site has not been designed or built yet. This is the main outstanding item for the website.
- **sds-consulting launch** — once user is ready, add the page to the sitemap and decide if it gets its own domain or stays as a sub-path
- **Worky v3 App Store privacy policy URL** — already submitted as `https://akarshsingh.com/worky/privacy` in App Store Connect
- **Contact form testing** — verify Formspree endpoint (`mjgpebkg`) is receiving submissions correctly

---

## Related Projects

- **Worky v3** — iOS workout tracking app. Context file at `/Users/akarshsingh/Engineering_Tools/Worky_V3/WORKY_CONTEXT.md`. The website hosts the app's required privacy policy at `/worky/privacy`.
- **SD Solutions NC** — small business IT consulting. No separate site/domain yet. Currently lives at `akarshsingh.com/sds-consulting`.
