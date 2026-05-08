# Unskooling.day — Build Walkthrough

## Summary

Built a complete, high-conversion Hugo static site for Unskooling.day — a community-based experiential learning platform targeting parents in Bangalore's gated communities. The site uses Hugo v0.161 with Tailwind CSS v4, features a warm/playful "Modern Education" design aesthetic, and is fully data-driven via markdown content files.

## Screenshots

### Hero Section
![Hero section with headline, CTAs, and watercolor illustration](/Users/plotkai/.gemini/antigravity/brain/02288acf-ac8c-4343-890e-913d973c261c/screenshot_hero.png)

### Clarity Section & How It Works
![Two-column rote vs unskooling comparison and 3-step timeline](/Users/plotkai/.gemini/antigravity/brain/02288acf-ac8c-4343-890e-913d973c261c/screenshot_clarity.png)

### Sessions Directory with Filters
![Session cards with category filter tabs and AI-generated images](/Users/plotkai/.gemini/antigravity/brain/02288acf-ac8c-4343-890e-913d973c261c/screenshot_sessions.png)

### Society CTA & Footer
![Dark society CTA section and 3-column footer](/Users/plotkai/.gemini/antigravity/brain/02288acf-ac8c-4343-890e-913d973c261c/screenshot_footer.png)

---

## Architecture

### Tech Stack
- **Hugo v0.161.1** (extended) — Static site generator
- **Tailwind CSS v4** — Utility-first CSS via Hugo's `css.TailwindCSS` pipe
- **Google Fonts** — Quicksand (display) + Outfit (body)

### File Structure

| Directory | Purpose |
|---|---|
| `hugo.toml` | Site config, Tailwind build, security, menus |
| `assets/css/main.css` | Design system (theme tokens, components, animations) |
| `layouts/_default/baseof.html` | Base template with deferred CSS rendering |
| `layouts/index.html` | Homepage with all 8 sections |
| `layouts/partials/` | Nav, footer, head, CSS processing |
| `layouts/sessions/` | Session list + single page templates |
| `layouts/mentors/` | Mentor list + single page templates |
| `layouts/societies/` | Society listing template |
| `content/sessions/` | 3 sample sessions (Guitar, Swimming, Business) |
| `content/mentors/` | 3 sample mentors (Priya, Rahul, Anita) |
| `content/societies/` | 3 sample societies (Prestige, Brigade, Sobha) |
| `static/images/` | AI-generated placeholder images |

### CTA Integration
All CTAs link to the provided Google Forms:
- **Join the Circle** → `forms.gle/ZZxzmyht9kSb8Zv46`
- **Bring to My Society** → `forms.gle/hL4BetHe43yCFm1c8`
- **Become a Mentor / Express Interest** → `forms.gle/4YHumKyhqc3r6paeA`

### Adding New Content
To add a new session, mentor, or society, just create a new `.md` file:

```bash
# New session
hugo new content sessions/yoga-for-kids.md

# New mentor  
hugo new content mentors/vikram-patel.md

# New society
hugo new content societies/embassy-springs.md
```

Each file uses frontmatter like:
```yaml
---
title: "Yoga for Kids"
category: "Wellness"
status: "Upcoming"
price_model: "₹300/session"
schedule: "Wednesdays, 5 PM"
society: "Embassy Springs"
description: "Mindful movement for young bodies..."
image: "/images/sessions/yoga.webp"
---
```

## What Was Tested
- ✅ Hugo build succeeds without errors
- ✅ All 8 homepage sections render correctly
- ✅ Sticky navigation with scroll effect works
- ✅ Session category filters work (All/Music/Swimming/Business)
- ✅ Content loops populate from markdown files
- ✅ All AI-generated images display correctly
- ✅ Google Fonts (Quicksand + Outfit) load properly
- ✅ Gradient text effects render
- ✅ Glass card hover animations work
- ✅ Footer with 3-column layout renders properly

## Next Steps
- [ ] **GitHub Actions**: Update workflow to Hugo v0.161.1 + Node.js (deferred per your request)
- [ ] Replace AI-generated images with real photos as they become available
- [ ] Add more sessions/mentors/societies as content grows
- [ ] Consider adding a blog section for SEO content marketing
