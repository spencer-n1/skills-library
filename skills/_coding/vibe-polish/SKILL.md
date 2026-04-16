---
name: vibe-polish
description: Polish existing vibe-website and vibe-app projects with critical fixes, subtle purposeful animations, and portfolio-ready refinements. Surgical edits only — no full rebuilds.
type: procedural
keywords: ["polish", "refine", "cleanup", "fix bugs", "add animations", "portfolio polish", "micro-interactions", "hover effects", "scroll animations"]
category: coding
---

# Vibe Polish

**Purpose:** Take an existing built project and elevate it with critical fixes, subtle purposeful animations, and portfolio-ready cleanliness. This is the direct-code equivalent of the Base44 "redesign prompt" — but applied surgically instead of regenerated from scratch.

**Input:**
1. Path to built project (`websites/[slug]/` or `Kimi Code Apps/[slug]/`)
2. Optional live URL for visual comparison
3. Optional notes from Spencer on specific concerns

**Output:** Same project, polished. No new directory.

**Tooling:** Delegates all actual edits to `vibe-editor` (surgical, additive, or structural as needed).

---

## Core Philosophy

**Fix first, polish second.** A broken nav with fancy animations is still broken.

**Purposeful, not flashy.** Animations should feel like they *belong* — not like they're showing off.

**Surgical only.** Never rewrite an entire page to fix one section. Touch the minimum files necessary.

---

## Step 0: Input Clarification & Confirmation

Before auditing or polishing anything, convert the user's request into a **discrete, numbered list of polish items**.

**Protocol:**
1. Parse the user's input. Break it into individual, specific changes or concerns.
2. Present the list to Spencer exactly like this:
   ```
   Here's what I understood you want polished:

   1. [specific item 1]
   2. [specific item 2]
   3. [specific item 3]

   Does this look right? (yes / no / add or remove items)
   ```
3. **WAIT for explicit confirmation.** Do not proceed until Spencer says yes or approves the list.
4. If Spencer says no or adds items, revise the list and confirm again.
5. Only after confirmation, begin Phase 1 (Critical Fixes Audit).

**Why this matters:** Prevents misinterpretation, scope creep, and wasted edits.

---

## Polish Tier: "Slight + Purposeful"

This skill operates at a fixed tier between "barely any animation" and "premium wow factor":

| What We Add | What We Avoid |
|-------------|---------------|
| Staggered fade-in + slide-up on scroll (translateY 20-30px, 400-600ms) | Pulsing/breathing animations |
| Subtle hover lifts (translateY -2px to -4px) with shadow increase | Dramatic parallax |
| Nav underline or color shift on hover | Floating independent elements |
| Button press feedback (scale 0.98 on click) | Excessive shadow layers |
| Hero content staggered load sequence | Animations that delay content access |
| Very subtle image zoom on hover (scale 1→1.02) | Ken Burns effects |
| Icon scale-in on scroll (0.8→1 with fade) | "SCROLL" indicator text |

**Rule:** If an animation draws attention to *itself* instead of the *content*, it's too much.

---

## Phase 1: Critical Fixes Audit

Inspect the project for structural and conversion issues. Check every item:

### Navigation
- [ ] Nav links are correct and match the sitemap
- [ ] No duplicate or missing links
- [ ] Nav text has sufficient contrast on ALL backgrounds (hero transparent + scrolled solid)
- [ ] Transparent → solid background transition works on scroll
- [ ] Mobile hamburger menu exists and functions
- [ ] **Cross-page links land at TOP of destination page first**

### Hero
- [ ] Exactly 100vh height (websites)
- [ ] Background image has appropriate overlay for text contrast
- [ ] Headline and CTAs are readable
- [ ] No layout breakage on mobile

### Services
- [ ] Homepage shows **maximum 3 service cards only**
- [ ] Cards have consistent spacing and alignment
- [ ] "See All Services" or equivalent link works

### Content & Conversion
- [ ] Phone numbers are `tel:` links
- [ ] "Get Directions" links to actual map/address
- [ ] Contact form has all required fields
- [ ] Reviews section displays correctly with attribution
- [ ] Footer has correct links and social icons

### Responsive
- [ ] All grids collapse to single column on mobile
- [ ] Touch targets are minimum 44px
- [ ] No horizontal overflow

### Code Quality
- [ ] No hardcoded hex codes outside `lib/design-system.ts`
- [ ] All images have descriptive `alt` text
- [ ] No broken imports or TypeScript errors

---

## Phase 2: Subtle Animation Pass

After critical fixes are complete, add animations in this order of priority:

### 1. Page Load Sequence (Hero Only)
```
Stage 1 (0ms):     Background/image fades in (opacity 0→1, 600ms ease-out)
Stage 2 (400ms):   Headline fades + slides up (translateY 30px→0, 500ms)
Stage 3 (700ms):   Subheadline fades + slides up (translateY 20px→0, 400ms)
Stage 4 (900ms):   Key elements (message bar, CTAs) fade in (400ms)
```

### 2. Scroll-Triggered Reveals (All Sections Below Hero)
```
Standard Section Entry:
- Headline: fade + slide up (translateY 30px→0, opacity 0→1, 500ms ease-out)
- Content blocks: staggered fade + slide (translateY 20px→0)
- Delay between staggered items: 80-100ms
- Trigger: when element enters viewport (typically 20% from bottom)
```

### 3. Navigation Micro-interactions
```
On Scroll (past ~100px):
- Background: transparent → solid (250ms ease)
- Optional subtle shadow appears: 0 2px 10px rgba(0,0,0,0.1)

Nav Link Hover:
- Underline slides in from left (width 0→100%, 200ms)
- OR color shift to accent color (200ms)
```

### 4. Card Hover States
```
Default: clean, no lift, subtle shadow
Hover (250ms ease-out):
- Lift: translateY -4px
- Shadow intensifies slightly
- Optional: border color shifts subtly toward accent
```

### 5. Button Micro-interactions
```
Primary Button Hover:
- Background darkens slightly
- Subtle lift: translateY -2px

Primary Button Click:
- Scale 0.98 (quick press feedback, 100ms)

Secondary Button Hover:
- Background fills with accent color or border darkens
- Smooth 200ms transition
```

### 6. Image Treatments
```
Scroll Reveal:
- Fade in (400ms)

Hover:
- Very subtle zoom: scale 1→1.02 (300ms)
```

---

## Phase 3: Section-by-Section Polish

Walk through each major section and apply targeted improvements:

### Hero
- Ensure strong visual impact
- Verify text contrast
- Add subtle load sequence
- Optional: very slow background parallax (0.3x scroll speed) — only if it doesn't complicate the implementation

### Services
- Staggered scroll reveal on cards (100ms delay)
- Subtle hover lift + shadow
- Ensure icons are crisp and well-sized

### Why Choose Us / Trust Section
- Pure white text (#ffffff) on dark backgrounds for max contrast
- Subtle icon scale-in on scroll (0.8→1 with fade)
- Even spacing, balanced grid

### Reviews
- Clean card layout
- Subtle hover lift
- Star ratings visually clear

### CTA / Closing Section
- Section height feels impactful but not excessive
- CTAs have clear hover states
- Optional subtle background texture/gradient only if it fits the brand

### Footer
- Clean multi-column layout
- All links work
- Social icons have hover states

---

## Phase 4: Execution via Vibe-Editor

All changes must route through `vibe-editor` tiers:

| Change Type | Editor Tier | Example |
|-------------|-------------|---------|
| Copy fix, color tweak, broken link | Surgical | Fix CTA text, adjust contrast |
| New animation hook, new hover component | Additive | Add `useScrollReveal` hook, `FadeIn` wrapper component |
| Update design tokens affecting multiple files | Structural | Add animation timing tokens to `design-system.ts` |

**Before any structural animation changes:**
1. Check if the project already has an animation approach (Framer Motion, CSS keyframes, Intersection Observer, etc.)
2. Match the existing approach if it's clean
3. If no approach exists, introduce the minimal viable solution (usually CSS transitions + Intersection Observer, or Framer Motion if already in dependencies)

**Never introduce new heavy dependencies** (like GSAP) just for subtle animations.

---

## Phase 5: Quality Checklist

Before declaring done:

- [ ] Nav is clearly visible on all backgrounds
- [ ] Cross-page navigation starts at TOP every time
- [ ] Hero is exactly 100vh (if website)
- [ ] Homepage services capped at 3 cards
- [ ] All `tel:` links work
- [ ] Mobile menu functions
- [ ] No horizontal scroll on mobile
- [ ] Animations feel intentional and smooth
- [ ] No animations block content access
- [ ] No hardcoded hex codes outside design-system file
- [ ] All images have `alt` text
- [ ] No TypeScript errors
- [ ] Sitemap matches actual pages

---

## Output Format

Report to Spencer:

```
Polish complete for [project-name].

Critical fixes applied:
- [fix 1]
- [fix 2]

Animations added:
- [animation 1]
- [animation 2]

Files changed:
- [file] — [change]
- [file] — [change]

Files created:
- [file] — [what it is]
```

If anything was too broken to fix surgically, flag it:
> "The nav component has structural issues that go beyond polish — recommend a partial rebuild. Want me to do that?"

---

## What Never to Do

- **Never add flashy effects** just to look impressive
- **Never fix one thing by rewriting an entire page**
- **Never introduce new dependencies** for simple CSS animations
- **Never skip the critical fixes** to get to the fun animation stuff
- **Never polish a broken foundation** — if the core structure is wrong, stop and tell Spencer
