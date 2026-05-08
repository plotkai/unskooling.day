# Unskooling.day — Hugo Static Site Build

A high-conversion, modern Hugo site for a community-based experiential learning platform in Bangalore. Serves as a smoke test to validate interest from parents in gated communities.

## User Review Required

> [!IMPORTANT]
> **Node.js is not installed** on your system. Hugo v0.161+ requires Node.js v22+ to use the built-in `css.TailwindCSS` pipe with Tailwind CSS v4. I'll install it via Homebrew as the first step. Please confirm this is acceptable.

> [!IMPORTANT]
> **GitHub Actions workflow** currently uses Hugo v0.145.0. I'll update it to v0.161.1 and add the Node.js setup step to match your local environment.

## Open Questions

1. **Form backend**: The CTAs ("Join the Circle", "Bring Unskooling to My Society", "Express Interest") need a form submission endpoint. Options:
   - **Formspree** (free tier, zero backend) — recommended for a smoke test
   - **Google Forms embed**
   - **Netlify Forms** (if you move off GitHub Pages later)
   - Should I integrate one of these, or just link to an external form for now?

2. **Gallery images**: Should I generate placeholder images with AI for the "Previous Classes" gallery, or leave them as empty slots to be filled with real photos?

3. **Color palette**: The brief says "warm, playful, modern education." I'm proposing:
   - Primary: `#F97316` (warm orange)
   - Accent: `#6366F1` (indigo)
   - Background: `#FFFBF5` (warm white)
   - Dark: `#1E1B2E` (deep purple-black)
   - Is this direction acceptable, or do you have brand colors?

---

## Proposed Changes

### Phase 0 — Prerequisites & Project Initialization

#### Install Node.js v22+ via Homebrew
```bash
brew install node
```

#### Initialize npm & install Tailwind CSS
```bash
npm init -y
npm install --save-dev tailwindcss @tailwindcss/cli @tailwindcss/typography
```

#### Initialize Hugo project structure
```bash
hugo new site . --force  # --force since CNAME/.github already exist
```

---

### Phase 1 — Hugo Configuration

#### [NEW] [hugo.toml](file:///Users/plotkai/products/unskooling-day/unskooling.day/hugo.toml)

Complete site configuration including:
- Site metadata (title, baseURL, language)
- Tailwind CSS build integration (`build.buildStats`, `cachebusters`, `module.mounts`)
- Node security permissions for Tailwind CLI
- Site params: tagline, description, social links, CTA URLs
- Menu configuration for sticky nav

---

### Phase 2 — Tailwind CSS & Design System

#### [NEW] [assets/css/main.css](file:///Users/plotkai/products/unskooling-day/unskooling.day/assets/css/main.css)

Tailwind v4 entry point with:
- `@import "tailwindcss"`
- `@source "hugo_stats.json"` for class detection
- `@theme` block with custom colors, fonts (Quicksand/Outfit), border-radius tokens
- Custom component styles for cards, buttons, badges

---

### Phase 3 — Layout Templates

#### [NEW] [layouts/_default/baseof.html](file:///Users/plotkai/products/unskooling-day/unskooling.day/layouts/_default/baseof.html)

Base template with:
- `<head>`: Google Fonts (Quicksand + Outfit), meta tags, OG tags, Tailwind CSS pipe using `css.TailwindCSS` with deferred rendering
- Sticky navigation bar partial
- `{{ block "main" . }}` content block
- Footer partial
- Smooth scroll behavior

#### [NEW] [layouts/index.html](file:///Users/plotkai/products/unskooling-day/unskooling.day/layouts/index.html)

Homepage template with all sections in order:
1. **Hero Section** — Full-width gradient background, headline, sub-copy, dual CTAs
2. **"So What" Clarity Section** — Two-column comparing rote learning vs curiosity-led unschooling
3. **How It Works** — 3-step horizontal timeline with icons
4. **Session Directory** — Grid pulling from `content/sessions/*.md` with category filters
5. **Mentor Profiles** — Card grid pulling from `content/mentors/*.md`
6. **Safety & Quality Trust Block** — Icon-based trust signals
7. **Gallery** — CSS grid for previous class photos
8. **Society CTA** — "Bring Unskooling to My Society" section for society presidents

#### [NEW] [layouts/partials/nav.html](file:///Users/plotkai/products/unskooling-day/unskooling.day/layouts/partials/nav.html)

Sticky nav with:
- Logo/brand name
- Nav links (How It Works, Sessions, Mentors, Societies)
- "Join the Circle" CTA button
- Mobile hamburger menu with slide-in drawer
- Scroll-triggered background change (transparent → solid)

#### [NEW] [layouts/partials/footer.html](file:///Users/plotkai/products/unskooling-day/unskooling.day/layouts/partials/footer.html)

Footer with:
- Quick links
- Contact info
- Social links
- "Made with ❤️ in India"

#### [NEW] [layouts/partials/css.html](file:///Users/plotkai/products/unskooling-day/unskooling.day/layouts/partials/css.html)

Tailwind CSS processing partial using `css.TailwindCSS` with fingerprinting for production.

#### [NEW] [layouts/partials/head.html](file:///Users/plotkai/products/unskooling-day/unskooling.day/layouts/partials/head.html)

SEO meta tags, Open Graph, Twitter Card, favicon references.

---

### Phase 4 — Content Type Templates

#### [NEW] [layouts/sessions/list.html](file:///Users/plotkai/products/unskooling-day/unskooling.day/layouts/sessions/list.html)

Session listing page with category filter tabs (Music, Swimming, Business, All).

#### [NEW] [layouts/sessions/single.html](file:///Users/plotkai/products/unskooling-day/unskooling.day/layouts/sessions/single.html)

Individual session detail page with mentor link, schedule, pricing, and CTA.

#### [NEW] [layouts/mentors/list.html](file:///Users/plotkai/products/unskooling-day/unskooling.day/layouts/mentors/list.html)

Mentor directory with profile cards.

#### [NEW] [layouts/mentors/single.html](file:///Users/plotkai/products/unskooling-day/unskooling.day/layouts/mentors/single.html)

Individual mentor profile with bio, skills, and "Express Interest" form.

#### [NEW] [layouts/societies/list.html](file:///Users/plotkai/products/unskooling-day/unskooling.day/layouts/societies/list.html)

Society directory showing upcoming sessions per society.

---

### Phase 5 — Sample Content (Data-Driven)

#### [NEW] content/sessions/_index.md
Section index for sessions.

#### [NEW] content/sessions/guitar-basics.md
```yaml
---
title: "Guitar Basics"
category: "Music"
mentor: "priya-sharma"
price_model: "₹500/session"
status: "Active"
description: "Learn acoustic guitar from scratch..."
schedule: "Every Saturday, 10 AM"
society: "prestige-lakeside"
image: "/images/sessions/guitar.jpg"
---
```

#### [NEW] content/sessions/swimming-101.md
#### [NEW] content/sessions/young-entrepreneurs.md

*(3 sample session markdown files)*

#### [NEW] content/mentors/_index.md
#### [NEW] content/mentors/priya-sharma.md
```yaml
---
title: "Priya Sharma"
skill: "Music (Guitar, Ukulele)"
bio: "A software engineer by day and musician by passion..."
photo: "/images/mentors/priya.jpg"
society: "Prestige Lakeside Habitat"
experience: "5 years teaching"
---
```

#### [NEW] content/mentors/rahul-menon.md
#### [NEW] content/mentors/anita-krishnan.md

*(3 sample mentor markdown files)*

#### [NEW] content/societies/_index.md
#### [NEW] content/societies/prestige-lakeside.md
```yaml
---
title: "Prestige Lakeside Habitat"
location: "Varthur, Bangalore"
status: "Active"
resident_count: "2000+ families"
---
```

#### [NEW] content/societies/brigade-gateway.md
#### [NEW] content/societies/sobha-dream-acres.md

*(3 sample society markdown files)*

---

### Phase 6 — Static Assets

#### [NEW] static/images/
- Generate placeholder hero illustration (AI-generated)
- Generate mentor avatar placeholders
- Generate session/gallery images

#### [NEW] static/favicon.ico
Basic favicon

---

### Phase 7 — GitHub Actions Update

#### [MODIFY] [gh-pages.yml](file:///Users/plotkai/products/unskooling-day/unskooling.day/.github/workflows/gh-pages.yml)

- Update Hugo version to `0.161.1`
- Add Node.js v22 setup step
- Add `npm ci` step before build
- Keep existing CNAME configuration

---

## File Tree (Final)

```
unskooling.day/
├── hugo.toml
├── package.json
├── package-lock.json
├── CNAME
├── .github/workflows/gh-pages.yml
├── assets/
│   └── css/
│       └── main.css              # Tailwind v4 entry
├── content/
│   ├── sessions/
│   │   ├── _index.md
│   │   ├── guitar-basics.md
│   │   ├── swimming-101.md
│   │   └── young-entrepreneurs.md
│   ├── mentors/
│   │   ├── _index.md
│   │   ├── priya-sharma.md
│   │   ├── rahul-menon.md
│   │   └── anita-krishnan.md
│   └── societies/
│       ├── _index.md
│       ├── prestige-lakeside.md
│       ├── brigade-gateway.md
│       └── sobha-dream-acres.md
├── layouts/
│   ├── _default/
│   │   └── baseof.html
│   ├── index.html                # Homepage
│   ├── partials/
│   │   ├── nav.html
│   │   ├── footer.html
│   │   ├── css.html
│   │   └── head.html
│   ├── sessions/
│   │   ├── list.html
│   │   └── single.html
│   ├── mentors/
│   │   ├── list.html
│   │   └── single.html
│   └── societies/
│       └── list.html
├── static/
│   └── images/
│       ├── hero/
│       ├── mentors/
│       ├── sessions/
│       └── gallery/
└── data/                         # (optional future use)
```

## Verification Plan

### Automated Tests
1. `hugo server` — verify site builds without errors and serves locally
2. `hugo --minify` — verify production build succeeds
3. Browser test — navigate all sections, check responsiveness, verify content loops work

### Manual Verification
- Visual review of all sections in browser
- Mobile responsiveness check
- Verify session/mentor/society content populates from markdown files
- Test sticky nav behavior on scroll
- Confirm CTAs are prominent and accessible
