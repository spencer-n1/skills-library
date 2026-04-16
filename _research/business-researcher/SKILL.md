---
name: business-researcher
description: Research web design leads and compile standardized business intelligence. Handles variable input (name+location, website URL, or partial info). Extracts ALL reviews found. Universal approach - no niche-specific paths. Outputs structured research file with emphasis on integration opportunities (booking apps, platforms) for closing meetings.
type: procedural
---

# Business Research Skill

**Purpose:** Research web design leads and compile standardized business intelligence  
**Input:** Variable — can be any of:
- Business name + location (most common)
- Website URL only
- Partial information (social media handle, rough location, etc.)
- Warm lead with relationship context
  
**Output:** `scratch/YYYY-MM-DD/research-[business-slug].md` — structured research file (dated folder auto-created)  
**Scope:** Research ONLY. Extract ALL reviews, ALL services, ALL platforms found.  
**Version:** 2.1 — March 29, 2026 (Variable input handling, all reviews extraction)

---

## Input Handling

**You may receive ANY level of information. Adapt:**

| Input Type | Your Approach |
|------------|---------------|
| **Name + Location** | Standard search: `"[name]" [location]` |
| **Website URL only** | Start with site analysis → backfill with search for reviews/social |
| **Social media handle** | Search handle → find connected business → expand |
| **Partial info** | Search what you have → document gaps for the user to fill |
| **Warm lead context** | Use relationship info to guide search priorities |

**Never say "I need more info."** Work with what you have and document what's missing.

---

## Pre-Flight: Check Mulch

Query mulch for known patterns before starting:

```
Read mulch/expertise/client-research.jsonl for patterns
Check mulch/db/mx-*.jsonl for failure modes
```

**What to look for in the results:**

| Pattern Type | Why It Helps | Example |
|--------------|--------------|---------|
| **Discovery methods** | Find hidden social/profiles faster | `"Found salon's IG via individual stylist pages"` |
| **Platform shortcuts** | Know where to look for booking tools | `"Check staff IG bios for Booksy links"` |
| **Search queries** | Better search terms that worked | `"'[business] + [city] + reviews' found GMB faster"` |
| **Dead ends** | Don't waste time on what doesn't work | `"Yelp 403 errors — use search instead of direct"` |

**If you find a relevant pattern, use it.** If you discover something new, record it before finishing.

---

## Research Process

### Step 1: Identify Information Sources (Adaptive)

**If you have a website URL:**
1. **Start there** — visit the site first
2. Extract: Name, services, contact, about info, any social links
3. **Then search** for reviews and additional presence

**If you have name + location:**
1. **Start with search** — `"[business name]" [location]`
2. Follow where results lead (GMB, Yelp, social, website)

**If you have partial info:**
1. Search what you have
2. Document what you couldn't find
3. Note: "[Field] not found — may need the user to provide"

**Sources to check (all that apply):**
- Google Business Profile (reviews + services often listed here)
- Yelp
- Facebook Business Page
- Instagram Business Profile
- Existing website
- LinkedIn Company Page
- Industry directories
- Booking platform directories (Booksy, StyleSeat, etc.)

---

### Step 2: Gather Core Business Information

**Extract everything available — leave blank if not found:**

```markdown
**Business Name:** [Exact legal/trade name]
**Tagline/Slogan:** [If available]
**Industry:** [Specific category - infer if needed]
**Years in Business:** [If known]
**Owner/Contact Name:** [Decision maker if found]

**Contact Information:**
- **Phone:** [Primary number]
- **Email:** [Business email]
- **Website:** [Current URL or "NONE - Clean slate opportunity"]
- **Social Media:** [All profiles found with @handles]

**Location:**
- **Address:** [Full street address]
- **City/State/ZIP:** 
- **Neighborhood/Area:** [Local context]
- **Service Area:** [Radius or specific areas served]

**Hours of Operation:**
- **Monday:** through **Sunday:** [Fill all found]

**Services/Products:** [Extract ALL services found - list every single one]

**Pricing:** [Any ranges mentioned - even "starting at $X"]

**Target Audience:** [Who they serve - inferred from services/reviews]
```

---

### Step 3: Extract ALL Reviews

**CRITICAL: Extract EVERY review you find.** Don't limit to 3-5.

```markdown
**Google Business Profile:**
- Status: [Claimed/Unclaimed/Not found]
- Rating: [X.X/5 stars (X reviews)]
- **ALL Review Quotes:**
  - "[Full quote 1 — include emotion/specifics]"
  - "[Full quote 2 — include emotion/specifics]"
  - "[Full quote 3 — include emotion/specifics]"
  - "[Continue for ALL reviews found...]"
  - "[Quote 7...]"
  - "[Quote 8...]"
  - "[Keep going until you've captured them all]"

**Common Review Themes:** [What do people mention most? e.g., "fast service", "friendly staff", "fair pricing"]

**Yelp:**
- Status: [Active/Inactive/Not found]
- Rating: [X.X/5 stars]
- **Review Quotes:**
  - "[Full quote 1...]"
  - "[Full quote 2...]"
  - "[ALL reviews found...]"

**Facebook:**
- Rating/Reviews if available
- **Review Quotes:** [ALL found]

**Other Platforms:** [Industry-specific review sites]
```

**Why extract all:** The prompt builder may want 5 specific ones. Having 12 gives options for emotional hooks, trust builders, and variety.

---

### Step 4: Identify ALL Platforms & Tools

**Document EVERY platform, tool, or system found:**

```markdown
**Booking/Scheduling Platforms:**
- **Booksy:** [URL if found — check staff IG bios]
- **StyleSeat:** [URL if found]
- **Vagaro:** [URL if found]
- **Square Appointments:** [URL if found]
- **Calendly:** [URL if found]
- **Acuity:** [URL if found]
- **Housecall Pro:** [If home services]
- **Mindbody:** [If wellness/fitness]
- **Other:** [Any custom booking system]
- **None Found:** [Note if no booking system — major opportunity]

**E-Commerce Platforms:**
- **Shopify:** [If selling products online]
- **Etsy:** [If craft/handmade business]
- **Square Online:** [If using Square for sales]
- **Other:** [WooCommerce, BigCommerce, etc.]

**Communication Tools:**
- **WhatsApp Business:** [If found]
- **Facebook Messenger:** [If active]
- **Text/SMS system:** [If mentioned]

**Payment Processors:**
- **Square:** [If mentioned/seen]
- **Stripe:** [If custom site]
- **PayPal:** [If found]
- **Cash/Venmo/Zelle:** [If mentioned in reviews/social]

**Other Tools:**
- **CRM:** [HubSpot, Salesforce, etc.]
- **Email Marketing:** [Mailchimp, Constant Contact, etc.]
- **Review Management:** [Podium, BirdEye, etc.]
```

---

### Step 5: Online Presence Audit

```markdown
**Social Media:**
- **Facebook:** [Active/Inactive — follower count if available — link]
- **Instagram:** [Active/Inactive — follower count — @handle — how found]
- **TikTok:** [If relevant and found]
- **LinkedIn:** [If B2B and found]
- **YouTube:** [If found]

**Directories & Listings:**
- **Google Business Profile:** [Link]
- **Yelp:** [Link]
- **MapQuest:** [If found]
- **Yellow Pages:** [If found]
- **Industry Directories:** [Specific to their niche]
- **Nextdoor:** [If local business found there]

**Website Analysis (if exists):**
- **Platform:** [WordPress, Wix, Squarespace, custom, etc. — infer if possible]
- **Age/Style:** [Looks modern/dated]
- **Mobile-friendly:** [Yes/No]
- **Key Issues:** [Slow, broken links, poor design, etc.]
- **What's Working:** [Good copy, clear services, etc.]
```

---

### Step 6: Extract Brand Intelligence

```markdown
**Atmosphere/Vibe:** [e.g., "laid-back traditional barbershop with modern touches"]

**Key Differentiators:** [3-5 bullet points on what makes them unique]
- 
- 
- 

**Brand Voice:** [Professional, casual, luxury, friendly, technical, etc.]

**Visual Direction Notes:** [Colors seen, style in photos, aesthetic]

**Customer Pain Points They Solve:** [What problems do they fix?]

**Community/Story Elements:** [Local connections, owner story, heritage, mission]
```

---

### Step 7: Write Personal Notes (Synthesis)

One paragraph (3-5 sentences):
- Essence of the business
- Why they need a website
- Design direction that feels right
- Any relationship context

---

## Output Format

**CRITICAL:** Save to dated folder structure:

```bash
# Create today's folder automatically
TODAY=$(date +%Y-%m-%d)
mkdir -p "workspace/scratch/$TODAY"

# Save research file here
workspace/scratch/$TODAY/research-[business-slug].md
```

```markdown
# Business Research: [Business Name]

## Core Information
[All fields from Step 2]

## Services & Offerings
[Complete list of ALL services found]

## Review Analysis
[ALL reviews from Step 3 — organized by platform]

## Platforms & Tools Inventory
[ALL platforms from Step 4 — booking, e-commerce, communication, payment]

## Online Presence Audit
[Social, directories, website analysis from Step 5]

## Brand Intelligence
[Vibe, differentiators, voice, visual notes from Step 6]

## Lead Context
**Source:** [How the user found them]
**Warmth:** [Cold/Warm/Hot lead]
**Pain Point:** [Why they need a website]
**Opportunity:** [What's exciting about this project]

## Personal Notes
[Synthesis paragraph from Step 7]

---

## Important Details for Closing Meeting

**Integration Opportunities (PRIORITY):**
- [ ] Booking platform: [Which one + URL if found — TALK ABOUT THIS]
- [ ] E-commerce: [Platform if found — TALK ABOUT THIS]
- [ ] Payment processor: [If found — integration opportunity]
- [ ] Existing tools: [CRM, email marketing — mention migration/integration]

**Key Discussion Points:**
- [ ] [Something important about their current setup]
- [ ] [A pain point mentioned in reviews]
- [ ] [Opportunity you spotted]

**Questions to Clarify:**
- [ ] [What you couldn't find that matters for the website]
- [ ] [Integration preferences — keep existing tool or migrate?]
- [ ] [Service details that were unclear]

---

## For Prompt Builder

**Key Info Summary:**
- Business: [Name] — [Industry] in [Location]
- Services: [Top 3-5 services for homepage focus]
- Differentiators: [Top 2-3 unique points]
- Design Direction: [Brief style note]
- Lead Context: [Warm/cold, relationship if applicable]
- **IMPORTANT:** [Any booking/platforms they use — critical for contact section]
```

---

## Report Back to the user

After saving the file, report ONLY the most important information:

### Template:

> **Research complete for [Business Name].**
> 
> **File:** `scratch/research-[business-slug].md`
> 
> **Critical for Closing Meeting:**
> - **Booking Platform:** [Booksy/Square/etc. — currently paying $X/month — discuss integration vs. replacement]
> - **E-commerce:** [If found — Shopify/etc. — major integration discussion]
> - **Current Website:** [If exists — platform, issues, migration complexity]
> - **Decision Maker:** [Name if found — for outreach]
> 
> **Key Intel:**
> - [Important finding 1 — e.g., "43 reviews, 4.9 stars — strong social proof to leverage"]
> - [Important finding 2 — e.g., "Using Housecall Pro — discuss embedded booking vs. link out"]
> - [Important finding 3 — e.g., "No Instagram — opportunity to suggest social integration"]
> 
> **Questions to Ask:**
> - [What you need clarified before building prompt]
> - [Integration preference — keep tool or migrate?]

**Prioritize:** Booking apps, platforms, tools, decision maker name, and anything that affects pricing or scope.

---

## Post-Flight: Record to Mulch

**Record what worked (for future you/other agents):**

```bash
# If you found a clever way to discover something
Manually append pattern to JSONL \
  --name "[What you found and how]" \
  --description "[Brief: searched X, found Y via Z]"

# If you hit a dead end or something was hard to find
Manually append failure to JSONL \
  --description "[What didn't work]" \
  --resolution "[What worked instead]"

# Record the outcome
Manually append outcome to JSONL \
  --description "Research for [business] — [input type]" \
  --status success
```

**Record patterns like:**
- `"Found barbershop IG via searching '[barber name] + [city]'"`
- `"Booksy link always in Instagram bio for salons"`
- `"Service lists more complete on website than GMB"`
- `"Couldn't find email — only contact form on site"`

---

## Research Tools

### Primary: `kimi_search`
- `"[business name]" [location]`
- `[business name] reviews`
- `[business name] booking`
- `[business name] instagram`
- `[staff name] [location] barber` (for staff page discovery)

### Secondary: `web_fetch`
- For extracting details from specific URLs

### Adapt to Input
- **Got website?** → Start there, then search for reviews
- **Got name only?** → Search broad, narrow down
- **Got social handle?** → Start there, find connected business

---

## Incremental Updates

When the user says *"Add this to the research..."*:

1. Read existing file
2. Integrate new info cleanly
3. Rewrite complete file (no timestamps)
4. Re-save

---

## What This Skill Does NOT Do

- ❌ Build prompts
- ❌ Make design decisions  
- ❌ Competitor analysis (future skill)
- ❌ Judge lead quality (report findings, let the user decide)
- ❌ Limit review extraction (GET THEM ALL)

---

*Version 2.1 — March 29, 2026 — Variable input handling, all reviews extraction, platforms inventory, closing meeting intel*
