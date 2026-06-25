# akarshsingh-website

Personal portfolio and app showcase site for Akarsh Singh, hosted on GitHub Pages at **akarshsingh.com**. No build step — static HTML + Tailwind CSS via CDN, deployed automatically on push to `main`.

## Structure

```
website/
├── index.html              # Homepage (hero + about)
├── CNAME                   # Custom domain config — do not modify
├── assets/
│   └── screenshots/        # App screenshots (worky-1/2/3.png, peony-1/2/3.png)
├── contact/index.html      # Contact form (Formspree)
├── peony/
│   ├── index.html          # Peony app marketing page
│   └── privacy/index.html  # Peony App Store privacy policy
├── worky/
│   ├── index.html          # Worky app marketing page
│   └── privacy/index.html  # Worky Privacy Policy + Terms of Service
├── budgy/
│   ├── index.html          # Budgy app marketing page
│   └── privacy/index.html  # Budgy Privacy Policy + Terms of Service
├── vetta/                  # Vetta SaaS landing page (formerly TPRM) + legal pages
├── tprm/index.html         # Redirect stub → /vetta (old links)
├── sds-consulting/         # SD Solutions NC page (not in sitemap)
├── sitemap/index.html      # Sitemap
└── docs/                   # Supporting docs
```

## Version History (branches)

| Branch | Description |
|--------|-------------|
| `main` | Current site — full portfolio, app pages, Tailwind design system |
| `dev-update` | Active development branch |
| `v0` | Original "Coming soon" placeholder (Oct 2025) |

## Deploy

```bash
git add <files>
git commit -m "message"
git push
```

Live within ~2 minutes of push. If rejected: `git pull --rebase && git push`.
