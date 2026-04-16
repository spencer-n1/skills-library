---
name: prompt-redesign
description: Create redesign prompts for existing websites. Use when the user asks you to redesign a current website. This is a STANDALONE task — analyze the URL, build redesign prompt, save file. Never do external research beyond the website itself.
type: procedural
---

# Prompt Redesign Skill

**Purpose:** Create redesign prompts for existing websites  
**Input:** Three entry paths (see below)  
**Output:** `prompts/redesign/YYYY-MM-DD/[business-slug].md` — complete redesign prompt (dated folder auto-created)  
**Scope:** Redesign ONLY. Analyze inputs, build prompt.  
**Version:** 2.2 — April 5, 2026 (Added three-path input system, cross-reference analysis)

---

## When to Use

Use this skill when the user asks you to redesign an existing site:
- "Build a redesign prompt for [URL]"
- "Update this prompt: [path]"
- "Compare this site to the original prompt"
- Client has current site that needs improvement
- Creating "before/after" concept

**This is a standalone task.** Analyze inputs → build prompt → save file → report.

---

## Three Input Paths

the user can provide inputs in three ways. Detect which path based on what he gives you:

### Path A: URL Only
**Input:** Website URL  
**Approach:** Analyze live site, reverse-engineer structure, identify weaknesses  
**Best for:** 
- Old sites built by others
- Competitor analysis
- Sites built without prompts (including your own builds where prompt wasn't provided)
- When you need to start fresh with no reference
**Output:** Standard redesign prompt  
**Filename:** `[business-slug]-redesign.md`

### Path B: Original Prompt Only
**Input:** Path to original prompt file  
**Approach:** Review design intent, identify what failed to execute, build "do it right" prompt  
**Best for:**
- Site isn't live yet or is broken/inaccessible
- Major scope changes needed
- When you want to iterate on a concept before building
**Output:** Revised/updated prompt (v2 build, not redesign)  
**Filename:** `[business-slug]-v2.md`

### Path C: URL + Original Prompt
**Input:** Both website URL and original prompt path  
**Approach:** Cross-reference analysis — compare intent vs. reality  
**Best for:**
- Sites you built that drifted from spec
- When execution didn't match design
- Detailed gap analysis and fixes
**Output:** "Gap Analysis + Redesign" — shows what drifted and how to fix it  
**Filename:** `[business-slug]-gap-analysis.md`  
**Special:** Includes "Intent vs. Reality" comparison table

---

## Pre-Flight: Check Mulch

Before starting, query mulch:

```
Read mulch/expertise/prompt-redesign.jsonl for patterns
Check mulch/db/mx-*.jsonl for failure modes
```

---

## Procedure

### Step 0: Determine Input Path

Based on what the user provided, identify the path:

| If the user gives... | Path | Output filename |
|---------------------|------|-----------------|
| URL only | Path A | `[business-slug]-redesign.md` |
| Prompt file path only | Path B | `[business-slug]-v2.md` |
| URL + Prompt file path | Path C | `[business-slug]-gap-analysis.md` |

### Path A: URL Only

#### Step A1: Site Structure Extraction
Visit the existing site. Document:

```
CURRENT STRUCTURE:
├── Header: [logo, nav items, CTA]
├── Hero: [headline, subhead, imagery, CTA]
├── Section 2: [content type]
├── Section 3: [content type]
├── ...
└── Footer: [links, contact, social]
```

#### Step A2: Weakness Analysis
For each section, identify problems and opportunities:

| Element | Current State | Problem | Opportunity |
|---------|---------------|---------|-------------|
| Headline | "Welcome to Our Site" | Generic | Specific outcome-focused |
| Hero Image | Stock photo | Not authentic | Real project photos |
| CTA | "Contact Us" | Weak | "Get Free Quote" with urgency |
| Social Proof | None | No trust | Add reviews, certifications |

Common weaknesses to check:
- [ ] No clear value proposition above fold
- [ ] Weak/no CTAs
- [ ] Missing trust signals
- [ ] Poor visual hierarchy
- [ ] No location/SEO optimization
- [ ] Outdated design
- [ ] Walls of text
- [ ] No service differentiation

#### Step A3: Content Strategy
**Keep:** Specific services, strong copy, good brand colors, contact structure  
**Change:** Headlines → outcome-focused, Imagery → authentic, Layout → clear hierarchy  
**Add:** Social proof, Service differentiation, Location signals

Proceed to Step 4 (Build Redesign Prompt).

---

### Path B: Original Prompt Only

#### Step B1: Prompt Review
Read the original prompt file completely. Extract:
- Design system (colors, fonts, spacing)
- Intended structure (sections, layout)
- Content plan (copy, images, CTAs)
- Business information

#### Step B2: Execution Gap Analysis
Identify what likely failed or needs updating:
- Design system issues (colors that won't work, bad contrast)
- Structure problems (too many/few sections)
- Content gaps (missing copy, weak CTAs)
- Technical issues (animations too heavy, not mobile-friendly)

#### Step B3: Revision Strategy
**Keep:** Core design direction, business info, what's working  
**Change:** Design system fixes, structure improvements, stronger copy  
**Add:** Missing sections, better CTAs, current trends

Proceed to Step 4 (Build Revised Prompt).

---

### Path C: URL + Original Prompt

#### Step C1: Dual Extraction
**From URL:** Document actual site structure and content  
**From Prompt:** Extract intended design and structure

#### Step C2: Cross-Reference Analysis (Intent vs. Reality)
Create comparison table:

| Element | Original Intent (Prompt) | Current Reality (Site) | Gap |
|---------|--------------------------|------------------------|-----|
| Hero headline | "Built to Last" | "Welcome to Our Site" | Generic replacement |
| Primary color | #D97706 orange | #FF6B35 reddish | Color drift |
| Services section | 3 cards with icons | Text list | Structure failed |
| CTA button | "Get Free Estimate" | "Contact Us" | Weak CTA |

#### Step C3: Gap Resolution Strategy
For each gap, determine fix:
- **Drift (execution failed):** Restore to original spec
- **Improvement needed:** Enhance beyond original
- **New requirement:** Add what's missing
- **Remove bloat:** Cut what doesn't serve the goal

Proceed to Step 4 (Build Gap Analysis + Redesign Prompt).

---

### Step 4: Build Prompt

### Step 5: Output

**CRITICAL:** Save to dated folder structure with path-specific filename:

```bash
# Create today's folder automatically
TODAY=$(date +%Y-%m-%d)
mkdir -p "workspace/prompts/redesign/$TODAY"
```

**Path A (URL Only):**
```
workspace/prompts/redesign/$TODAY/[business-slug]-redesign.md
```

**Path B (Prompt Only):**
```
workspace/prompts/redesign/$TODAY/[business-slug]-v2.md
```

**Path C (URL + Prompt):**
```
workspace/prompts/redesign/$TODAY/[business-slug]-gap-analysis.md
```

### Step 6: Record to Mulch

Document patterns/failures.

---

## Redesign Prompt Template

```markdown
# [Business Name] — Website Redesign

## Current Site Analysis

**URL:** [original URL]
**Niche:** [industry]
**Location:** [city, state]

### Existing Structure
[Documented structure from Step 1]

### Key Weaknesses
1. [Weakness 1 - impact]
2. [Weakness 2 - impact]
3. [Weakness 3 - impact]

### What's Working
1. [Keep this]
2. [Keep this]

### Intent vs. Reality (Path C Only)
**Note:** If using Path C (URL + Original Prompt), add this section:

| Element | Original Intent (Prompt) | Current Reality (Site) | Gap |
|---------|--------------------------|------------------------|-----|
| Hero headline | "Built to Last" | "Welcome" | Generic replacement |
| Primary color | #D97706 orange | #FF6B35 | Color drift |
| Services layout | 3 icon cards | Text list | Structure failed |
| CTA button | "Get Free Estimate" | "Contact Us" | Weak CTA |

## Redesign Strategy

### Primary Goal
[One sentence: e.g., "Increase quote requests by making trust signals prominent"]

### Target Audience
[Who: e.g., "Homeowners in [city] needing [service]"]
[Their pain points]
[What they want]

### Design Direction
- **Style:** [modern/classic/bold/clean]
- **Colors:** [primary, secondary, accent]
- **Typography:** [font choices]
- **Mood:** [professional/friendly/urgent/trustworthy]

## Base44 Prompt — Full Structure

### Design System
```yaml
colors:
  primary: "#[color]"
  secondary: "#[color]"
  accent: "#[color]"
  background: "#[color]"
  text: "#[color]"

fonts:
  heading: "[font]"
  body: "[font]"

effects:
  - "Subtle shadow on cards"
  - "Smooth transitions on hover"
```

### Section 1: Header/Navigation
[Layout, components, CTA button]

### Section 2: Hero
[Full 100vh, headline, subhead, CTAs, visual]

### Section 3-7: Content Sections
[Section-by-section breakdown]

### Section 8: Social Proof/Trust
[Grid of trust signals]

### Footer
[3-column structure]

## Copy Guidelines

### Tone
[Professional but approachable / etc]

### Key Messages
1. [Message 1]
2. [Message 2]
3. [Message 3]

### Words to Use/Avoid
[Trust, expert, fast] / [Cheap, try, maybe]

## SEO Requirements

### Title Tag
"[Service] in [City] | [Business Name] — [Differentiator]"

### Meta Description
"[Compelling description with keywords]"

### Header Structure
- H1: [Primary keyword]
- H2: [Secondary sections]
- H3: [Subsections]

### Local SEO
- City name in headlines
- Service area mention
- NAP consistent

## Deliverables Checklist

- [ ] 7-8 sections total
- [ ] 2-3 CTAs minimum
- [ ] Trust signals in first 2 sections
- [ ] Location optimization
- [ ] Mobile-responsive design
- [ ] Clear service differentiation
```

---

## Quality Checklist

Before delivering:

- [ ] Site structure fully documented
- [ ] At least 3 specific weaknesses identified
- [ ] Redesign strategy is clear
- [ ] Every section has specific copy direction
- [ ] Design system is complete
- [ ] SEO elements are specific
- [ ] Tone is consistent
- [ ] CTAs are action-oriented with value

---

## Redesign Tiers (Choose Appropriately)

| Tier | Best For | Animation | Visual Polish | When to Use |
|------|----------|-----------|---------------|-------------|
| **Tier 1: Polish Pass** | Local service businesses | Fade-ins only | Clean spacing, fix buttons, better hierarchy | **DEFAULT** — most clients |
| **Tier 2: Premium** | Agencies, premium services | Soft scroll effects, hover states | Cards with depth, gradients, subtle textures | When they want to stand out |
| **Tier 3: Full** | Creative brands only | Full motion (if appropriate) | Immersive, "wow" factor | When they specifically ask for it |

**The "No Cornball" Rule:** Default to Tier 1. Most HVACs, plumbers, landscapers need trust, not circuses.

---

## Background Texture Library (Optional)

Use subtle textures to add depth without visual noise. Not every section needs texture — default to clean solid backgrounds.

| Texture | Description | Best For | Opacity |
|---------|-------------|----------|---------|
| **Subtle Dot Grid** | Small dots, evenly spaced | Professional, healthcare, agency | 3-5% |
| **Plus/Cross Pattern** | Small + symbols, scattered | Modern tech, creative, construction | 4-6% |
| **Geometric Lines** | Thin lines forming subtle grid | Corporate, legal, financial | 2-4% |
| **Subtle Noise/Grain** | Film grain texture | Dark themes, premium feel | 3-5% |
| **Diagonal Stripes** | Very faint diagonal lines | Energy, fitness, dynamic brands | 2-3% |
| **Gradient Mesh** | Soft color shifts, no hard edges | Creative agencies, modern brands | 5-8% |

**Usage Rules:**
- Never use same texture on adjacent sections
- Dark sections: slightly more visible (5-8%)
- Light sections: very subtle (2-4%)
- Mix textures for variety
- When in doubt, skip it (clean is better than busy)

---

## Business Type Color Quick Reference

| Business Type | Primary | Accent | Notes |
|---------------|---------|--------|-------|
| Electrician | Deep navy, midnight blue | Electric blue, cobalt | Urgency, technical, 24/7 trust |
| HVAC | Navy foundation, charcoal | Vibrant orange | Heating/cooling duality |
| Landscaping | Sand, beige, sage, cream | Natural green | Earthy, premium outdoor living |
| Web Agency | Deep black, near-black | Cyan, white | Modern, premium, tech-forward |
| Health/Beauty | Soft white, light gray | Calming blue, soft pink | Clean, safe, professional |
| Professional Services | Navy, charcoal | Gold, deep blue | Authoritative, refined |

---

## Post-Flight: Record to Mulch

```bash
# Record patterns
Manually append pattern to JSONL \
  --name "[Industry] redesign approach" \
  --description "[What worked]"

# Record common weaknesses
Manually append pattern to JSONL \
  --name "Common [industry] website weaknesses" \
  --description "[List of issues to check for]"

# Record outcome
Manually append outcome to JSONL \
  --description "Redesign prompt for [URL]" \
  --status success
```

---

## Reminder: This is a STANDALONE Task

**Three entry paths:**
- **Path A:** URL only → reverse-engineer and redesign
- **Path B:** Prompt only → revise and improve
- **Path C:** URL + Prompt → gap analysis and fix

No external research beyond the inputs provided. the user will provide URL and/or prompt path — use what's given.

---

*Version 2.2 — April 5, 2026 — Added three-path input system (URL only, Prompt only, URL + Prompt)*
