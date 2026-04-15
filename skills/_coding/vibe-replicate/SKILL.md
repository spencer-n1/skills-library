---
name: vibe-replicate
description: Replicate an existing vibe-coded website or app from scratch using source code, live URL screenshots, and the original prompt.
type: procedural
keywords: ["replicate", "clone", "duplicate", "recreate", "copy website", "rebuild", "vibe replicate"]
category: coding
---

# Vibe Replicate

**Purpose:** Rebuild an existing vibe-coded project from scratch by combining source-code analysis, live-site screenshots, and the original build prompt.

**Inputs:**
1. **Source code** — Base44 export or existing Next.js/React project (highest authority)
2. **Live URL** — For visual validation via Playwright screenshots
3. **Original prompt** — For intent, business context, and design direction

**Output:** A rebuilt project using `vibe-website` or `vibe-app`, written to the standard output directory.

---

## Pre-Flight: Gather Inputs

Spencer will typically provide all three. If any are missing, proceed with what you have using this priority:

**Source code > Live URL screenshots > Original prompt**

### Step 0: Accept Inputs

Ask for or confirm:
- Path to source code directory
- Live URL (if deployed)
- Original prompt / build spec

---

## Phase 1: Source Code Archaeology

If source code is provided, read it thoroughly before doing anything else.

### 1.1 Determine Stack

Read `package.json`:
- Next.js App Router → use **vibe-website**
- React + Vite → use **vibe-app**
- Base44 export (often Next.js or React) → treat as **reference material**, not copy-paste source

### 1.2 Extract Design System

Find and read:
- `lib/design-system.ts` or `src/lib/design-system.ts`
- `tailwind.config.ts` / `tailwind.config.js`
- `globals.css` / `index.css`

Extract:
- Color palette (primary, secondary, accent, background, text)
- Typography (font families, sizes, weights, tracking)
- Spacing (section padding, container max-width, gaps)
- Border radius, shadows, transitions

### 1.3 Map Architecture

List all pages/routes:
- `app/**/page.tsx` (Next.js)
- `src/pages/**/*.tsx` (Vite/React Router)
- `src/App.tsx` sections (single-page apps)

List all shared components:
- `components/` or `src/components/`
- Note which are UI primitives (Button, Card, Input) vs section components (Hero, ServicesGrid, Nav)

### 1.4 Extract Content Structures

Find the content source:
- `lib/content.ts`
- `src/data/` or constants inside components

Extract:
- Business name, tagline, location, contact info
- Services list (titles, descriptions, icons)
- Reviews/quotes with attribution
- Navigation links
- Any SEO metadata

### 1.5 Build Replication Manifest (Source)

Write a concise summary:
```markdown
## Replication Manifest — Source Truth

**Stack:** Next.js 14 App Router
**Target Skill:** vibe-website
**Pages:** /, /services, /about, /contact, /sitemap, /privacy-policy, /thank-you, /services-deep-dive
**Colors:** Primary #1E5F8E, Background #FFFFFF, Accent #4A90B8
**Fonts:** DM Sans
**Key Components:** Nav (transparent→solid scroll), Hero (100vh), ServicesGrid (max 3), Reviews, CTABanner, Footer
**Content Notes:** [any anomalies or missing pieces]
```

---

## Phase 2: Live Site Visual Capture

If a live URL is provided, use **playwright-cli** to screenshot and inspect.

### 2.1 Full-Page Screenshots

Capture at **desktop (1280x800)** and **mobile (390x844)**:
- `/` — Home
- `/services` — Services
- `/about` — About
- `/contact` — Contact

Save screenshots to `scratch/replicate-screenshots/[project-slug]/`

### 2.2 Component Close-Ups

Use Playwright to screenshot specific viewport regions or scroll-to-capture:
- Hero section
- Navigation (top and scrolled state if possible)
- Services grid / cards
- Reviews section
- CTA banner
- Footer

### 2.3 Motion & Behavior Notes

Document anything not obvious in code:
- Scroll-triggered animations
- Hover states
- Mobile menu open/close transition
- Any video, carousel, or interactive element

### 2.4 Update Replication Manifest

Append visual findings:
```markdown
## Visual Findings
- Nav has blurred glass background on scroll
- Hero has subtle gradient overlay on background image
- Service cards lift on hover with shadow increase
- Mobile menu slides from right
```

---

## Phase 3: Prompt Analysis

Read the original prompt for:
- Business type and industry
- Brand vibe / tone
- Specific Spencer requests that may not be in the code
- Design direction or references

If the prompt conflicts with the source code, **ask Spencer which wins** before proceeding.

---

## Phase 4: Build

### 4.1 Choose Builder Skill

| Stack Detected | Use Skill |
|----------------|-----------|
| Next.js (App Router) | `vibe-website` |
| React + Vite | `vibe-app` |
| Unclear / mixed | Ask Spencer |

### 4.2 Lock Constraints Before Writing Code

From the replication manifest, define:
1. Exact data model / content structures
2. Design tokens (one source of truth)
3. Component boundaries (props vs internal state)
4. Page architecture and routing

### 4.3 Foundation Pass

Generate in order:
1. `lib/design-system.ts` (or equivalent)
2. `lib/content.ts` with typed structures
3. Root layout, global styles, font imports
4. Navigation + Footer shells
5. Empty page shells with correct metadata

### 4.4 UI Pass

Fill pages one at a time, cross-referencing screenshots:
1. Hero
2. Services / Features
3. Trust / Social Proof
4. Reviews
5. CTA Banner
6. Footer details

**Rule:** Do not copy boilerplate from Base44 exports. Rebuild using your own clean patterns from `vibe-website` or `vibe-app`.

---

## Phase 5: Validation Checklist

Before declaring done, verify:

- [ ] **Structural match:** All pages/routes from source are present
- [ ] **Design token match:** Colors, fonts, and spacing align with source
- [ ] **Visual match:** Rebuilt sections look equivalent to screenshots
- [ ] **Hero height:** Exactly 100vh (if website)
- [ ] **Mobile match:** Mobile screenshots look equivalent
- [ ] **Content complete:** All business info, services, and reviews present
- [ ] **Animations captured:** Scroll, hover, and menu behaviors replicated
- [ ] **No hardcoded hexes:** All colors reference the design system file
- [ ] **Click-to-call / links:** Phone numbers and external links work
- [ ] **No Base44 boilerplate:** Code is clean, not bloated with generated cruft

---

## Phase 6: Output Summary

Tell Spencer:
1. Project location
2. Builder skill used
3. What was replicated from source vs interpreted from screenshots
4. Any anomalies, missing assets, or areas that needed guesswork
5. How to run: `npm install && npm run dev`
6. How to deploy: `npm run build`

---

## Universal Rules

### Rule 1: Source Code Wins on Structure
If the source has 8 pages, the rebuild has 8 pages. No shortcuts.

### Rule 2: Screenshots Win on Visuals
If the live site has a blurred nav on scroll but the code doesn't show it clearly, replicate the visual behavior.

### Rule 3: Prompt Wins on Intent
If Spencer explicitly asked for something in the prompt that got lost in the source code, ask which to follow — but default to honoring the original request.

### Rule 4: Clean Rebuild Only
Base44 exports are noisy. Extract the intent, then rewrite it cleanly. Do not copy generated junk.

### Rule 5: Surgical Fixes
If something is slightly off after the build, fix the specific file/line. Do not rewrite entire sections.
