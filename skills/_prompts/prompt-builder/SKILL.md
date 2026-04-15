---
name: prompt-builder
description: Generate professional, detailed Base44 website prompts from research input. Uses the shared design library and reasoning engine to make smart pattern and aesthetic choices. This is a STANDALONE task.
type: procedural
---

# Prompt Builder Skill

**Purpose:** Generate professional, detailed Base44 website prompts from research input
**Input:** `scratch/research-[business-slug].md` (MUST read this first)
**Output:** `prompts/client/[business-slug].md` — complete Base44 prompt
**Scope:** Prompt building ONLY. Uses reasoning engine + design library.

---

## Pre-Flight

Read these BEFORE building:
1. `skills/_design/reasoning-engine/business-types.json`
2. `skills/_design/reasoning-engine/style-matching.json`
3. `skills/_design/reasoning-engine/pattern-selection.json`
4. `skills/_design/library/taste-profile.md`

---

## Procedural Steps

### Step 0: Get Input

**Read the research file completely.** Extract:
- Business name, location, contact info
- Services (top 3 for homepage)
- Review quotes (best 2-3)
- Brand vibe and differentiators
- Photos from Google Business Profile
- Personal notes (design direction)

### Step 1: Run Reasoning Engine

Match business type in `business-types.json`.
- If exact match: Use that category
- If no exact match: Use closest category or fallback

Get recommendations for:
- **Aesthetic** (primary + alternatives)
- **Style keywords**
- **Color mood**
- **Typography mood**
- **Key sections**
- **Anti-patterns to avoid**

### Step 2: Query Library

Read specific patterns from `skills/_design/library/patterns/`:
- Nav pattern
- Hero pattern
- Section patterns
- CTA pattern
- Footer pattern

Read the chosen **aesthetic folder** from `skills/_design/library/aesthetics/` for exact colors/fonts.

### Step 3: Apply Taste Profile

Check `taste-profile.md` for overrides:
- Skip patterns marked "avoid" for this context
- Bump "preferred" patterns to top recommendation
- Apply "Always" and "Never" rules

### Step 4: Build the Prompt

Assemble into the structured prompt template (see below).

### Step 5: Output

Save directly to:
```
prompts/client/[business-slug].md
```

---

## Prompt Structure Template

```markdown
# [Business Name] — Website Build Prompt

**Business:** [Name]
**Location:** [City, State]
**Industry:** [Industry]
**Services:** [List from research]
**Current Website:** [URL] (reference for copy/logo ONLY, NOT structure)

**Design Direction:** [From reasoning engine]
- Aesthetic: [Chosen aesthetic]
- Style: [Keywords]
- Color Mood: [From aesthetic folder]
- Typography: [Font pairing]

**Copywriting Note:** Use existing website as source material. Adapt and optimize for clarity and SEO while maintaining core messaging.

---

## Universal Rules

[Logo extraction, website reference, animation level]

---

## Design System

**Color Palette:**
[Exact colors from aesthetic folder]

**Typography:**
[Exact fonts from aesthetic folder]

**Spacing:**
[From library foundations]

**Components:**
[From chosen patterns]

---

## Page-by-Page Breakdown

### Required Pages
Every site must have:
1. **Sitemap** (`/sitemap`)
2. **Privacy Policy** (`/privacy-policy`)
3. **Services Deep-Dive** (`/services-deep-dive`) — included in sitemap, linked from footer/services page. This page must have thorough, human-readable content: full service descriptions, process explanations, area coverage, FAQs with full Q&A, semantic HTML hierarchy (H1 + H2s), and internal links to `/services`, `/contact`, and `/about`. Must read like it was written for a human who wants detail. No keyword stuffing or bot-only tone.
4. **Thank You Page** (`/thank-you`) — separate page after form submission

### Navigation
[Specific pattern from library]

### Page 1: Home
**Section 1: Hero**
[Hero pattern specs]

**Section 2: About/Trust**
[Pattern specs]

**Section 3: Services Preview**
- MAX 3 service cards
- Icon + Title + 1-line description
- "See All Services" button

**Section 4: Social Proof**
[Review pattern specs]

**Section 5: CTA Banner**
[CTA pattern specs]

### Page 2: Services
[Full service details]

### Page 3: About
[Structure from pattern library]

### Page 4: Contact/Location
[Structure from pattern library]

### Footer
[Footer pattern specs]

---

## Global Elements
- Chat widget (bottom right)
- Smooth scroll navigation
- Mobile-responsive
- Navigation Behavior: Cross-page links MUST reset to top first

---

## Company Information (From Research)
[All verified details from research file]
```

---

## Universal Rules (Always Apply)

### Rule 0: Decorative Elements (CRITICAL)
**Background patterns, geometric shapes, and textures are OPTIONAL — not default.**
**Default:** Clean solid backgrounds.
**Only add patterns if:** The design feels flat without them, OR the pattern fits the brand.

### Rule 1: Logo Extraction
- Extract logo from existing website if available
- Use `filter: invert` for dark/light compatibility

### Rule 2: Website Reference Usage
- **USE existing site FOR:** Copy, business info, services, contact details, logo
- **DO NOT USE existing site FOR:** Structure, layout, design patterns, colors

### Rule 3: Image Handling
- Use specific photo URLs from Google Business Profile when available
- Otherwise provide specific shot list

### Rule 4: Two-Prompt System
**Initial Prompt:** Light animations, solid foundation, clean and functional
**Redesign Prompt:** Heavy animations, premium polish

### Rule 5: Hero Section — Full Viewport (CRITICAL)
**Every hero must be 100vh.** No exceptions.

### Rule 6: Navigation Structure
**Nav must include:** Logo, Home, Services, About, Location OR Contact, CTA Button
**NO duplicate links.** Cross-page links MUST start at TOP of destination page.

### Rule 7: Homepage Services (CRITICAL)
**MAXIMUM 3 service cards only.**

---

## Feedback Integration

After building, ask Spencer: "Want me to log any feedback on patterns or aesthetic?"

If he gives feedback:
1. Identify the pattern/aesthetic used
2. Update `skills/_design/library/taste-profile.md`
3. Note for future builds
