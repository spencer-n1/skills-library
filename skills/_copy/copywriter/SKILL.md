---
name: copywriter
description: On-demand copywriter. Clean, effective, persuasive writing for any medium — SEO content, blogs, emails, landing pages, sales pages, ads, social posts.
type: procedural
keywords: ["write copy", "SEO content", "blog post", "email copy", "landing page copy", "ad copy", "sales copy", "conversion copy"]
auto_detect: true
agent_type: sub
input_schema:
  what: string
  who: string
  goal: string
  tone: string
output_schema:
  content: string
quality_metrics:
  success_rate: 0.40
  avg_tokens: 6000
evolution:
  parent: null
  version: "3.0"
  lineage: []
status: active
---

# Copywriter

**Version:** 3.0  
Your on-demand copywriter. Clean, effective, persuasive writing for any medium.

---

## When to Use

- Website copy (home, about, services, product pages)
- Landing pages and sales pages
- Email sequences and newsletters
- Blog posts and articles
- Cold outreach messages
- Social media posts
- Ad copy (Google, Meta, LinkedIn)
- Meta descriptions and SEO content
- Text messages or DMs
- Any words that need to persuade or convert

## Don't Use When

- Goal is pure education (not conversion)
- You haven't researched your audience
- You need technical/legal documentation
- The content is internal-only (use simpler tone)

---

## Input

| Field | Description |
|-------|-------------|
| **What** | What are we writing? (blog, email, landing page, etc.) |
| **Who** | Who's the audience? (specific persona) |
| **Goal** | What should this achieve? (click, buy, sign up, reply) |
| **Context** | Business info, offer, pain points, proof points |
| **Length** | Short, medium, long — or word count |
| **Tone** | How should it sound? |

---

## The Copywriting Process

### Step 1: Research & Strategy

**Voice of Customer:**
- What words do customers use to describe their pain?
- What outcomes do they actually want?
- What objections do they have?

**Key Questions:**
- Who is the reader? (one specific persona)
- What's their current state (pain)?
- What's their desired state (outcome)?
- What's the one thing they must believe?
- What's the primary action they should take?

### Step 2: Choose Your Framework

**AIDA:**
- **Attention:** Hook that stops the scroll
- **Interest:** Why keep reading?
- **Desire:** Show the transformation
- **Action:** Clear CTA

**PAS (Problem-Agitation-Solution):**
- **Problem:** Agitate the pain
- **Agitation:** Make it hurt more
- **Solution:** Your product as relief

**Before-After-Bridge:**
- **Before:** Current painful state
- **After:** Desired state
- **Bridge:** How to get there (your solution)

### Step 3: Write First Draft

**Headline Formulas:**
- How to [achieve outcome] without [common pain]
- The [adjective] way to [outcome] in [timeframe]
- [Number] ways to [outcome] (even if [objection])
- Are you making these [topic] mistakes?

**Body Copy Principles:**
- Write like you talk (conversational)
- One idea per sentence, one idea per paragraph
- Short paragraphs (1-3 sentences)
- Use "you" more than "we"
- Lead with benefits, support with features
- Specifics beat generalities ("$199 tune-up" vs "affordable")

### Step 4: Add Proof

- Testimonials (with photos, names, specifics)
- Case studies (before/after numbers)
- Statistics and data
- User numbers / social proof
- "As seen in" logos

### Step 5: Edit Ruthlessly

- Cut 10% of words (minimum)
- Replace jargon with simple words
- Check for passive voice
- Ensure one clear CTA
- Read aloud — does it flow?

---

## Page-Specific Structures

### Homepage
1. Headline: What you do + who for
2. Subhead: Key benefit or differentiator
3. Social proof: Logos, numbers, testimonials
4. Features/benefits: 3 key value props
5. CTA: Primary action
6. Secondary proof: Case studies

### Landing Page
1. Hook: Problem or bold promise
2. Agitation: Why current solutions fail
3. Solution: Your unique approach
4. Benefits: What's in it for them
5. Proof: Testimonials, results
6. Offer: What they get
7. Guarantee: Risk reversal
8. CTA: Strong, specific action

### Product Page
1. Headline: Product name + key benefit
2. Subhead: What it does
3. Benefits: 3-5 key outcomes
4. Features: What makes it possible
5. Social proof: Reviews, testimonials
6. Pricing/CTA
7. FAQ

### Email
1. Subject line: Compelling, specific
2. Hook: First line grabs attention
3. Value: The useful content
4. CTA: What to do next
5. Sign-off: Human, warm

---

## Tone Options

| Tone | Use When |
|------|----------|
| **Direct** | Cold outreach, sales, urgency |
| **Friendly** | Most business writing, blogs, emails |
| **Professional** | B2B, legal, medical, high-ticket |
| **Casual** | Social, younger audiences, personal brands |
| **Authoritative** | Expert content, thought leadership |
| **Empathetic** | Healthcare, sensitive topics |

---

## Writing Principles

### Always
- Write like a human — conversational, not robotic
- Lead with value — why should they keep reading?
- Active voice — "We fix leaks" not "Leaks are fixed"
- Specific over vague — "$199 tune-up" beats "affordable"
- Clear CTA — tell them exactly what to do
- One idea per paragraph

### Never
- Keyword stuffing (integrate naturally)
- Generic fluff ("quality service since 1995")
- Overly formal unless requested
- Walls of text — use breaks, bullets, whitespace

---

## Headline Power Words

Free, New, Proven, Easy, Quick, Guaranteed, Secret, Discover, Exclusive, Limited, Instant, You, Your, Now, Today, Results, Transform

---

## Output Formats by Request Type

| Request | Output Style |
|---------|--------------|
| Blog post | Full article with headline, sections, conclusion |
| Email | Subject line + body (ready to send) |
| Landing page | Section-by-section copy (hero, benefits, CTA) |
| Text/DM | Short, punchy message |
| SEO content | Optimized copy with meta data |
| Ad copy | Headline options + body + CTA variations |

---

## File Saving

Save to: `scratch/copy/[type]-[topic]-YYYY-MM-DD.md`

Examples:
- `scratch/copy/blog-roof-maintenance-2026-03-30.md`
- `scratch/copy/email-follow-up-2026-03-30.md`
- `scratch/copy/landing-plumber-2026-03-30.md`

---

## Quality Standards

### 95/5 Rule
- 95% of quality comes from clear direction upfront
- 5% comes from editing
- Better brief = better first draft

### Time-Box
- Maximum 10 minutes writing + reviewing
- Good copy doesn't need endless tweaking
- When in doubt, ship it

### When to Iterate
| Situation | Action |
|-----------|--------|
| Minor tweaks | Fix and send |
| Wrong direction | Tell me what's off, I'll rewrite |
| Missing context | Ask me questions |

---

## Related Skills

- **customer-research** — Voice of customer data
- **copy-editing** — Refinement with Seven Sweeps
- **humanizer** — Remove AI patterns from copy
- **marketing-psychology** — Persuasion principles
- **email-sequence** — Multi-email campaigns
- **cold-email** — B2B outreach specifically
