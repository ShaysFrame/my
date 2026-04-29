---
name: shay-portfolio
description: |
  Personal portfolio and brand system for Shay (ShaysFrame). Use this skill when building,
  designing, or improving any part of Shay's personal portfolio website, blog, project pages,
  resume page, or any self-promotional web content. Trigger on: "portfolio", "my site",
  "project page", "about me", "resume page", "hero section", "personal brand", "shay.pub".
allowed-tools: Read, Write, Grep, Glob, WebFetch
---

# M. MAHAFUJ RAHMAN's Portfolio — Brand & Build System

You are building the personal portfolio of M. Mahafuj Rahman, a full-stack developer with a wide
range of shipped projects across mobile, web, backend, IoT, and ML. The portfolio must
communicate depth, range, and craft — not just list technologies.

---

## Identity

**Name**: M. MAHAFUJ RAHMAN (goes by Shay online)
**GitHub**: ShaysFrame
**Site**: shay.pub  
**Stack identity**: Full-stack generalist — Flutter, Vue, Astro, React, Django, PHP, Docker, YOLO/CV  
**Career goal**: Land a role at a top-tier tech company by demonstrating real, shipped work

---

## Design Philosophy

**Aesthetic**: Editorial. High-contrast. Typography-led. Instantly attention-grabbing.  
**Mood**: Clean and elegant — like a magazine cover, not a SaaS landing page.  
**Guiding principle**: Every element either grabs attention or gets removed.

### Color Palette

```
--color-bg:        #0a0a0a   /* near-black background */
--color-surface:   #111111   /* cards, panels */
--color-border:    #222222   /* subtle dividers */
--color-text:      #f5f5f5   /* primary text — off-white, not harsh pure white */
--color-muted:     #777777   /* secondary/metadata text */
--color-accent:    #ffffff   /* pure white — used sparingly for maximum contrast */
--color-highlight: #e8e8e8   /* hover states, selected items */
```

No color accents. No gradients. Black, white, and contrast do all the work.

### Typography

- **Display / Hero**: A single bold serif or high-contrast grotesque display font.
  Suggestions: `Playfair Display`, `Editorial New`, `PP Neue Montreal`, `Instrument Serif`
- **Body / UI**: Clean geometric sans-serif. `Inter`, `DM Sans`, or `Geist`
- **Code**: `JetBrains Mono` or `Geist Mono`
- **Rule**: Fewer font weights, more intentional sizing. Use scale, not color, to create hierarchy.

### Motion & Interaction

**Philosophy**: Motion should feel inevitable, not decorative. Every animation answers
"why does this move?" — to direct attention, signal state, or reward a scroll.

**Layer 1 — CSS (always, no dependencies)**

- Page transitions: use Astro's built-in `<ViewTransitions />` — zero JS cost
- Hover states: opacity shifts, underline reveals, subtle scale (1.0 → 1.02)
- Focus states: visible ring using `--color-accent`
- Entrance: CSS `@keyframes` fadeUp for above-the-fold content

**Layer 2 — Scroll-driven animation (CSS-first)**

- Use native CSS `animation-timeline: scroll()` where browser support allows
- Fallback: `IntersectionObserver` in a small `.ts` utility — no library needed
- Project cards: staggered `fade + translateY(24px → 0)` as they enter the viewport
- Section headings: slide in from left on scroll

**Layer 3 — Hero "wow" element (one, and only one)**

- The hero gets ONE signature motion effect. Options in order of preference:
  1. **Staggered letter/word reveal** — hero name animates in character by character (CSS only)
  2. **Noise/grain overlay** — animated CSS grain texture over the dark background (CSS only)
  3. **Subtle 3D tilt** — project cards tilt slightly on mouse move (Vanilla JS, ~15 lines)
  4. **Three.js / React Three Fiber** — only if a specific 3D asset is needed (e.g. a rotating
     geometric logo). Use the `3D-Animation-Creator` or `3D-Website-Asset-Generator` skills to
     generate the asset separately, then embed as a single isolated component.

**What to never do**

- Full-page Three.js backgrounds (kills performance, distracts from content)
- Looping animations anywhere except the hero
- Bouncy spring physics (wrong tone for editorial aesthetic)
- Parallax scrolling on text
- Motion just because a tutorial used it

---

## Site Structure

```
/                  → Hero + featured projects teaser + brief intro
/about             → Who Shay is, background, philosophy, skills overview
/projects          → Grid of all projects with stack tags and short descriptions
/projects/[slug]   → Individual project deep-dive (problem, solution, stack, links, screenshots)
/resume            → Inline resume view + downloadable PDF link
/blog              → List of blog posts (already exists in Astro)
/blog/[slug]       → Individual post (already exists)
```

---

## Tech Stack

- **Framework**: Astro (SSG, markdown-first, zero JS by default, excellent SEO)
- **Component language**: Astro components + React/Preact (`.tsx`) for interactive islands
- **Language**: TypeScript everywhere — `.ts`, `.tsx`, `.astro` with typed frontmatter. Never `.js` or `.jsx`
- **Styling**: CSS custom properties (no Tailwind unless user specifically requests it)
- **Deployment**: Vercel
- **Content**: Astro Content Collections for blog posts and projects

---

## Project Showcase Priority

When building project pages, prioritize these projects in this order (most impressive first):

1. **Qifa** — multi-app ecosystem (client, shop, office, Docker, custom logging dashboard, ChatWoot)
2. **Open RTMS** — real-time system with YOLO v8n face detection (ML angle is rare and impressive)
3. **XueHanYu** — full-stack (Vue + Django), Chinese language learning platform
4. **NoorConnect** — app + backend + firmware (IoT/embedded is rare for web devs)
5. **Jidian Daojia** — Flutter + PHP + uniapp, multi-platform
6. **LittleLemon** — Meta Professional Certificate capstone (credentialed work)

For each project page, structure the content as:

1. One-line hook (what problem it solves, not what tech it uses)
2. Stack badges
3. The challenge / what made it interesting
4. Key decisions made
5. Links (GitHub, live demo if available)

---

## Writing Tone

- Direct. Confident. No fluff.
- First person where appropriate ("I built...", "I chose... because...")
- Avoid: "passionate about", "self-motivated", "results-driven", "leveraged synergies"
- Technical specifics > vague claims. Say "built a real-time face detection pipeline using YOLO v8n" not "worked on computer vision projects"

---

## Component Guidelines

When generating Astro components for this portfolio:

- Default export style: `.astro` files with `---` frontmatter
- Use CSS custom properties from the palette above
- Mobile-first responsive design
- Semantic HTML (proper use of `<article>`, `<section>`, `<nav>`, `<main>`)
- No inline styles except dynamic values
- Animations via CSS — keyframes in `global.css` or scoped `<style>` blocks
- Interactive islands: use `client:visible` directive so JS only loads when needed

---

## What to Avoid

- Generic hero text like "Hi, I'm a developer who loves to code"
- Purple gradients, rounded-everything, blue CTA buttons
- Cluttered layouts — embrace white (or black) space
- Listing every technology you've touched without context
- Copy that reads like a CV; this is a narrative, not a list
