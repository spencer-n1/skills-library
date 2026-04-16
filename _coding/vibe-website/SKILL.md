---
name: vibe-website
description: Build production-ready Next.js client websites from research and the shared design library. Direct code generation — no Base44 prompts.
type: procedural
keywords: ["build website", "client website", "next.js website", "web design agency", "vibe code website"]
category: coding
---

# Vibe Website Builder

**Purpose:** Build complete, production-ready Next.js client websites directly from research files and design direction.

**Input:**
1. Full build prompt from Spencer
2. `scratch/research-[slug].md` (if it does not exist, STOP and ask Spencer: "I don't see a research file at `scratch/research-[slug].md`. Is there one? If so, where is it located?")

**Output:** Complete Next.js project written to `websites/[business-slug]/`

**Stack:** Next.js 14+ (App Router), React, TypeScript, Tailwind CSS

---

## Pre-Flight (Read First)

Before writing any code, read these files in order:
1. `skills/_coding/base44-wisdom.md`
2. `skills/_design/library/taste-profile.md`
3. `skills/_design/reasoning-engine/business-types.json`
4. `skills/_design/reasoning-engine/style-matching.json`
5. `skills/_design/reasoning-engine/pattern-selection.json`
6. The research file (`scratch/research-[slug].md`)

**Hard stop:** If any of files 1–5 is missing or unreadable, STOP and tell Spencer before proceeding.

**Hard stop:** If the research file does not exist, STOP and ask Spencer: "I don't see a research file at `scratch/research-[slug].md`. Is there one? If so, where is it located?"

---

## Procedural Steps

### Step 0: Determine Business Slug and Project Path
- Extract business name from research file or prompt
- Create slug: lowercase, hyphenated (e.g., `the-locals-barbershop`)
- Project root: `websites/[business-slug]/`

### Step 1: Run Design Reasoning Engine
- Match business type in `business-types.json`
- Select **primary aesthetic** from `skills/_design/library/aesthetics/`
- Select **nav pattern**, **hero pattern**, **section patterns**, **CTA pattern**, **footer pattern** from `skills/_design/library/patterns/`
- Apply taste-profile overrides (preferred → use, avoid → skip)

### Step 2: Lock Design System
- Read the chosen aesthetic folder for exact colors, fonts, and component styles
- Read chosen pattern files for layout specs
- Build a design-system manifest (used for `lib/design-system.ts`)

### Step 3: Extract Business Intelligence
From the research file, extract:
- Business name, location, contact info, hours
- Top 3 services (homepage only gets 3 max)
- Best 2-3 review quotes with attribution
- Differentiators and brand vibe
- Photo URLs or specific shot list from GMB
- Any personal notes / design direction from Spencer

### Step 4: Plan Site Architecture

**Required pages for every client site:**
1. `app/page.tsx` — Home
2. `app/services/page.tsx` — Services detail
3. `app/about/page.tsx` — About
4. `app/contact/page.tsx` — Contact / Location
5. `app/sitemap/page.tsx` — Visual sitemap
6. `app/privacy-policy/page.tsx` — Privacy policy
7. `app/thank-you/page.tsx` — Post-form submission
8. `app/services-deep-dive/page.tsx` — Comprehensive services page (included in sitemap)

**Navigation structure:**
- Logo (left)
- Links: Home, Services, About, Location/Contact
- CTA button (right)
- Mobile: hamburger menu
- Behavior: transparent on hero → solid background on scroll (300ms transition)

### Step 5: Typed Content Structures
Before writing any page component, define typed content structures in `lib/content.ts` for:
- Services array
- Reviews array
- Business info object
- Navigation links

**Rule:** All business info flows from a single source (research file → typed constants → components). No hardcoded business text inside reusable components.

### Step 6: Foundation Pass or Full Generate?

**Foundation Pass (always recommended):**
1. Generate `lib/design-system.ts`
2. Generate `lib/content.ts` with typed structures
3. Generate root layout, global styles, and navigation shell
4. Generate empty page shells with correct metadata
5. Generate shared components (Nav, Footer, ContactForm) with prop interfaces

**UI Pass:**
Fill in one route at a time: Hero → Services Preview → Trust → Reviews → Location → CTA Banner.

### Step 7: Generate Code

Write these files into `websites/[business-slug]/`:

#### `app/layout.tsx`
- Root layout with HTML metadata
- Import Google Fonts if needed
- Global Tailwind classes
- Navigation component
- Footer component
- JSON-LD LocalBusiness schema

#### `app/page.tsx`
- Home page assembling all sections
- Sections in order: Hero → Services Preview → Trust/Why Choose Us → Social Proof → Location → CTA Banner

#### `app/services/page.tsx`
- Full services detail page
- Can use alternating layout or clean card grid

#### `app/about/page.tsx`
- Story section, values, team/atmosphere if relevant

#### `app/contact/page.tsx`
- Map embed, contact form, hours, click-to-call phone
- "Book Online" button if external booking URL exists

#### `app/sitemap/page.tsx`
- Visual list of all pages

#### `app/privacy-policy/page.tsx`
- Standard privacy policy text

#### `app/thank-you/page.tsx`
- Simple confirmation message

#### `app/services-deep-dive/page.tsx`
- **Not** a hidden spam page. This is a comprehensive, human-readable services page.
- Content requirements:
  - Full service descriptions (more thorough than homepage)
  - Process explanations
  - Area coverage / service regions
  - FAQs with full Q&A
  - Semantic HTML hierarchy (H1 + H2s)
  - Internal links to `/services`, `/contact`, `/about`
- **Include in sitemap** — removing it doesn't hide it from Google
- Link from footer and/or `/services` page
- Must read like it was written for a human who wants detail
- **Out:** keyword lists, repetition spam, "written for bots" tone

#### `components/Nav.tsx`
- Responsive nav with scroll-state background transition
- Logo, links, CTA
- Mobile hamburger menu

#### `components/Hero.tsx`
- 100vh height (non-negotiable)
- Follows selected hero pattern from design library
- Headline, subheadline, CTAs

#### `components/ServicesGrid.tsx`
- Max 3 cards on homepage
- Icon + title + 1-line description
- "See All Services" link

#### `components/Reviews.tsx`
- Review cards with quotes, attribution, star ratings

#### `components/CTABanner.tsx`
- High-contrast closing section

#### `components/Footer.tsx`
- Multi-column footer with links, social icons, copyright
- Include link to `/services-deep-dive`

#### `components/ContactForm.tsx`
- Name, email, message, submit

#### `lib/design-system.ts`
- Exported color tokens
- Exported typography classes / sizes
- Exported spacing values
- Exported border-radius / shadow tokens

#### `lib/content.ts`
- Typed constants for all business content
- Services, reviews, business info, nav links

#### `lib/utils.ts`
- Simple helpers (cn() for class merging if needed)

#### `next.config.js` (or `.mjs`)
- `output: 'export'` for static deployment
- `distDir: 'dist'`

#### `package.json`
- Next.js, React, Tailwind dependencies
- Build scripts

#### `tailwind.config.ts`
- Extend theme with design system colors
- Add custom font families

#### `tsconfig.json`
- Standard Next.js TypeScript config

#### `README.md`
- How to run locally
- Deployment notes
- Missing info / placeholders to fill

### Step 8: Validation Checklist
Before declaring done, verify:
- [ ] Hero is exactly 100vh
- [ ] Homepage has MAXIMUM 3 service cards only
- [ ] Navigation includes: Logo, Home, Services, About, Location/Contact, CTA
- [ ] Mobile menu exists and works
- [ ] All cross-page links scroll to TOP of destination first
- [ ] Click-to-call phone links use `tel:`
- [ ] Every color references `lib/design-system.ts` — no hardcoded hexes in components
- [ ] services-deep-dive page has thorough, human-readable content with full descriptions, process, area coverage, and FAQs
- [ ] services-deep-dive is included in the sitemap and linked from the footer
- [ ] LocalBusiness JSON-LD schema in layout
- [ ] All images have descriptive `alt` text
- [ ] Responsive at mobile breakpoint

### Step 9: Output Summary
Tell Spencer:
1. Project location (`websites/[business-slug]/`)
2. Design system chosen (aesthetic + patterns)
3. Any missing info that needs to be filled (phone numbers, exact hours, photos)
4. How to run it: `npm install && npm run dev`
5. How to deploy: `npm run build` → static files in `dist/`

---

## Universal Rules (Non-Negotiable)

### Rule 0: Taste Profile Overrides Everything
If `taste-profile.md` says "avoid" a pattern, do not use it.
If it says "preferred," bump it to top choice.

### Rule 1: Hero Height
**Every hero must be 100vh.** No exceptions.

### Rule 2: Homepage Services
**Maximum 3 service cards only.**

### Rule 3: Solid Backgrounds by Default
Decorative patterns, textures, and geometric shapes are OPTIONAL.
Default to clean solid backgrounds.

### Rule 4: No Inter as Primary
Inter is banned as the primary font per taste profile. Use alternatives.

### Rule 5: Cross-Page Navigation
Cross-page links MUST navigate to the top of the destination page first.
Never start a page scrolled to a section.

### Rule 6: Color Token Discipline
Every color in every component MUST reference `lib/design-system.ts`.
No rogue hex codes in TSX files.

### Rule 7: Mobile-First
All layouts must collapse gracefully to single column on mobile.
Touch targets minimum 44px.

### Rule 8: Component Data Boundaries
Every reusable section component receives its data via props.
No hardcoded business text inside components.

---

## Design System Token Format

`lib/design-system.ts` should export:

```typescript
export const colors = {
  primary: '#1E5F8E',
  secondary: '#2A7CB5',
  accent: '#4A90B8',
  background: '#FFFFFF',
  backgroundAlt: '#E8F4F8',
  textPrimary: '#1E5F8E',
  textSecondary: '#5A6B7A',
  textLight: '#FFFFFF',
} as const;

export const typography = {
  fontFamily: '"DM Sans", sans-serif',
  h1: 'text-5xl md:text-6xl font-bold tracking-tight',
  h2: 'text-3xl md:text-4xl font-semibold tracking-tight',
  h3: 'text-xl md:text-2xl font-semibold',
  body: 'text-base md:text-lg leading-relaxed',
  small: 'text-sm font-medium uppercase tracking-wider',
} as const;

export const spacing = {
  section: 'py-20 md:py-32',
  container: 'max-w-7xl mx-auto px-4 sm:px-6 lg:px-8',
} as const;
```

---

## Example Component Pattern

Hero component using design system:

```tsx
// components/Hero.tsx
import { colors, spacing, typography } from '@/lib/design-system';

export function Hero() {
  return (
    <section
      className="min-h-screen flex items-center justify-center relative"
      style={{ backgroundColor: colors.background }}
    >
      <div className={spacing.container}>
        <h1 className={typography.h1} style={{ color: colors.textPrimary }}>
          {businessName}
        </h1>
        {/* ... */}
      </div>
    </section>
  );
}
```

---

## Feedback Integration

After building, ask: "Want me to log any feedback on patterns or aesthetic?"

If Spencer gives feedback:
1. Identify the pattern/aesthetic used
2. Update `skills/_design/library/taste-profile.md`
3. Note for future builds
