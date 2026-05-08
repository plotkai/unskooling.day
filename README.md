# 🌻 Unskooling.day

A community-based experiential learning platform connecting kids in Bangalore's gated communities with passionate neighbor-mentors. Built with **Hugo v0.161** and **Tailwind CSS v4**.

> Real-world skills, taught by neighbors, in your community hall.

---

## 🚀 Quick Start

### Prerequisites

- [Hugo Extended v0.161+](https://gohugo.io/installation/) (`brew install hugo`)
- [Node.js v22+](https://nodejs.org/) (`brew install node`)

### Local Development

```bash
# Install dependencies
npm install

# Start dev server (with drafts)
hugo server --buildDrafts

# Site is live at http://localhost:1313/
```

### Production Build

```bash
hugo --minify
# Output goes to ./public/
```

---

## 📁 Project Structure

```
unskooling.day/
├── hugo.toml                  # Site configuration & Tailwind build settings
├── package.json               # Node dependencies (Tailwind CSS)
├── CNAME                      # Custom domain for GitHub Pages
│
├── assets/
│   └── css/
│       └── main.css           # Tailwind v4 entry + design system tokens
│
├── content/                   # ✏️ ALL CONTENT LIVES HERE (Markdown files)
│   ├── sessions/              # Learning sessions
│   ├── mentors/               # Mentor profiles
│   └── societies/             # Partner societies
│
├── layouts/
│   ├── _default/
│   │   └── baseof.html        # Base HTML template (head, nav, footer)
│   ├── index.html             # Homepage (all sections)
│   ├── partials/              # Reusable template fragments
│   │   ├── nav.html           # Sticky navigation bar
│   │   ├── footer.html        # Footer
│   │   ├── head.html          # SEO meta tags, fonts, favicon
│   │   └── css.html           # Tailwind CSS processing pipe
│   ├── sessions/              # Session list & detail templates
│   ├── mentors/               # Mentor list & detail templates
│   └── societies/             # Society listing template
│
├── static/
│   ├── favicon.svg            # Sunflower emoji favicon
│   └── images/
│       ├── hero/              # Hero section illustration
│       ├── sessions/          # Session card images
│       ├── mentors/           # Mentor profile photos
│       └── gallery/           # Gallery section photos
│
└── .github/
    └── workflows/
        └── gh-pages.yml       # GitHub Pages deployment
```

---

## ✏️ Content Management

All content is managed through **Markdown files** in the `content/` directory. The site automatically rebuilds when files are added, edited, or removed.

### Adding a New Session

Create a new file in `content/sessions/`:

```bash
# Example: content/sessions/yoga-for-kids.md
```

```yaml
---
title: "Yoga for Kids"
category: "Wellness"          # Used for filter tabs (Music, Swimming, Business, etc.)
mentor: "vikram-patel"        # Slug of the mentor
price_model: "₹300/session"
status: "Active"              # "Active" or "Upcoming"
description: "Mindful movement and breathing exercises for ages 6-12."
schedule: "Wednesdays, 5 PM"
society: "Embassy Springs"
image: "/images/sessions/yoga.webp"   # Optional — falls back to emoji
---

Detailed content about the session goes here.
Supports full **Markdown** formatting.
```

**Required frontmatter fields:**
| Field | Description | Example |
|---|---|---|
| `title` | Session name | `"Guitar Basics"` |
| `category` | Filter category | `"Music"`, `"Swimming"`, `"Business"` |
| `status` | Current status | `"Active"` or `"Upcoming"` |
| `price_model` | Pricing display | `"₹500/session"` |
| `description` | Short summary (shown on cards) | One-liner |
| `schedule` | When it happens | `"Saturdays, 10 AM"` |

**Optional fields:** `mentor`, `society`, `image`

---

### Adding a New Mentor

Create a new file in `content/mentors/`:

```bash
# Example: content/mentors/vikram-patel.md
```

```yaml
---
title: "Vikram Patel"
skill: "Yoga & Mindfulness"
bio: "A certified yoga instructor with 10 years of experience..."
photo: "/images/mentors/vikram.webp"   # Optional — falls back to avatar icon
society: "Embassy Springs"
experience: "10 years teaching"
---
```

**Required frontmatter fields:**
| Field | Description |
|---|---|
| `title` | Mentor's full name |
| `skill` | What they teach |
| `bio` | Short biography (2-3 sentences) |
| `society` | Which society they belong to |

**Optional fields:** `photo`, `experience`

---

### Adding a New Society

Create a new file in `content/societies/`:

```bash
# Example: content/societies/embassy-springs.md
```

```yaml
---
title: "Embassy Springs"
location: "Devanahalli, North Bangalore"
status: "Upcoming"               # "Active" or "Upcoming"
resident_count: "4000+ families"
---

Optional description about the society goes here.
```

---

## 🖼️ Adding Images & Assets

All static assets go in the `static/` directory. They are served from the site root.

```
static/images/sessions/yoga.webp  →  https://unskooling.day/images/sessions/yoga.webp
static/images/mentors/vikram.webp →  https://unskooling.day/images/mentors/vikram.webp
```

### Image Guidelines

| Type | Recommended Size | Location |
|---|---|---|
| Session card | 800×500px | `static/images/sessions/` |
| Mentor photo | 600×600px | `static/images/mentors/` |
| Gallery photo | 800×800px | `static/images/gallery/` |
| Hero illustration | 1000×1000px | `static/images/hero/` |

**Formats:** Use `.webp` for best performance. `.jpg` and `.png` also work.

---

## 🎨 Design System

The design system is defined in `assets/css/main.css` using Tailwind CSS v4's `@theme` block.

### Brand Colors

| Token | Hex | Usage |
|---|---|---|
| `--color-brand-orange` | `#F97316` | Primary CTA, highlights |
| `--color-brand-indigo` | `#6366F1` | Secondary accents, links |
| `--color-warm-white` | `#FFFBF5` | Page background |
| `--color-deep` | `#1E1B2E` | Text, dark sections |
| `--color-trust-green` | `#10B981` | Trust/safety indicators |

### Fonts

- **Display** (headings): [Quicksand](https://fonts.google.com/specimen/Quicksand)
- **Body** (paragraphs): [Outfit](https://fonts.google.com/specimen/Outfit)

### Reusable CSS Classes

| Class | Usage |
|---|---|
| `.btn-primary` | Orange gradient CTA button |
| `.btn-secondary` | Indigo outline button |
| `.glass-card` | Frosted glass card with hover lift |
| `.badge` | Small status/category pill |
| `.badge-active` | Green "Active" badge |
| `.badge-upcoming` | Pink "Upcoming" badge |
| `.gradient-text` | Orange-to-indigo gradient text |
| `.reveal` | Fade-in-up on scroll (IntersectionObserver) |

---

## 🔗 CTA Links (Google Forms)

All call-to-action buttons link to Google Forms. These URLs are configured centrally in `hugo.toml`:

```toml
[params]
  joinFormURL = "https://forms.gle/ZZxzmyht9kSb8Zv46"       # Join the Circle
  societyFormURL = "https://forms.gle/hL4BetHe43yCFm1c8"     # Bring to My Society
  mentorFormURL = "https://forms.gle/4YHumKyhqc3r6paeA"       # Become a Mentor
```

To update a form link, just edit `hugo.toml` — all buttons across the site update automatically.

---

## 🏗️ Adding New Sections to the Homepage

The homepage is a single-file template at `layouts/index.html`. Each section is wrapped in a `<section>` tag with an `id`. To add a new section:

1. Add the HTML block in `layouts/index.html` between existing sections
2. Add a nav link in `hugo.toml` under `[menus]`:

```toml
[[menus.main]]
  name = 'New Section'
  url = '#new-section'
  weight = 5
```

---

## 📝 Adding New Category Filter Tabs

Session categories are filtered client-side. To add a new category (e.g., "Wellness"):

1. Add sessions with `category: "Wellness"` in their frontmatter
2. Add a filter button in `layouts/index.html` inside `#session-filters`:

```html
<button class="filter-tab" data-filter="wellness" onclick="filterSessions('wellness', this)">🧘 Wellness</button>
```

3. Add a badge style in `assets/css/main.css`:

```css
.badge-wellness {
  background: #ECFDF5;
  color: #065F46;
}
```

---

## 🚢 Deployment

The site auto-deploys to GitHub Pages via `.github/workflows/gh-pages.yml` on push to `main`.

> ⚠️ **Note:** The GitHub Actions workflow currently uses Hugo v0.145.0 and does not have a Node.js setup step. This needs to be updated to Hugo v0.161.1 with Node.js v22 for Tailwind CSS to work in CI. Until then, you can build locally and push the `public/` folder manually if needed.

### Manual Deploy

```bash
hugo --minify
# Push the contents of ./public/ to your hosting
```

---

## 📋 Common Tasks Cheat Sheet

| Task | How |
|---|---|
| Add a session | Create `content/sessions/my-session.md` with frontmatter |
| Add a mentor | Create `content/mentors/name.md` with frontmatter |
| Add a society | Create `content/societies/name.md` with frontmatter |
| Add an image | Drop file in `static/images/<category>/` |
| Change CTA links | Edit `hugo.toml` → `[params]` section |
| Change nav items | Edit `hugo.toml` → `[menus]` section |
| Change colors/fonts | Edit `assets/css/main.css` → `@theme` block |
| Edit homepage sections | Edit `layouts/index.html` |
| Edit nav/footer | Edit `layouts/partials/nav.html` or `footer.html` |
| Run locally | `hugo server --buildDrafts` |
| Build for prod | `hugo --minify` |

---

*Made with 🌻 in India*
