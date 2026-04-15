---
name: deep-research-audit
description: Run intensive, comprehensive research on any business, market, or existing asset. Creates detailed audit report, executive summary PDF, and closing notes.
type: procedural
keywords: ["deep research", "audit", "comprehensive research", "market research", "competitive analysis"]
auto_detect: true
agent_type: sub
input_schema:
  subject: string
  context: string
  industry: string
output_schema:
  audit_file: scratch/audits/[subject]-audit-YYYY-MM-DD.md
  summary_file: scratch/audits/[subject]-executive-summary-YYYY-MM-DD.md
quality_metrics:
  success_rate: 0.60
  avg_tokens: 25000
evolution:
  parent: null
  version: "2.0"
  lineage: []
status: active
---

# deep-research-audit — SKILL.md

**Version:** 2.0  
**Last Updated:** 2026-03-30  
**Type:** Procedural / Optional Deep-Dive

---

## Purpose

Run intensive, comprehensive research on any business, market, or existing asset. Creates three outputs: detailed audit report, 1-2 page executive summary PDF, and closing notes for immediate use on calls.

**Use this when:**
- You need ammunition for a high-stakes pitch or closing call
- You want to identify specific gaps, opportunities, or competitive advantages
- You're entering a new market and need deep intelligence
- You want data-driven insights beyond surface-level research
- You're preparing strategic recommendations for a client

**Don't use when:**
- You need quick turnaround (this is depth over speed)
- Budget doesn't justify intensive research
- Surface-level research is sufficient for the task

---

## Input

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `subject` | string | Yes | What to research (business name, website URL, market, competitor, etc.) |
| `context` | string | Yes | Why you're researching — redesign, competitive analysis, market entry, etc. |
| `industry` | string | Yes | Industry/niche for benchmarking |
| `depth` | enum | No | `standard` or `deep` — default: `deep` |
| `focus_areas` | array | No | Specific areas to emphasize (e.g., ["digital presence", "competitive positioning", "customer journey"]) |

---

## Output

### 1. Detailed Audit Report (Comprehensive)

**Saved to:** `scratch/audits/[subject-name]-audit-YYYY-MM-DD.md`

Full deep-dive with all findings, data, competitive analysis, and detailed recommendations. Use this when you need to reference specifics or dig deeper into any section.

### 2. Executive Summary PDF (1-2 Pages)

**Saved to:** `scratch/audits/[subject-name]-executive-summary-YYYY-MM-DD.md`

Nicely formatted key points for quick reference. Formatted for PDF conversion via md-to-pdf skill.

**Sections:**
- The Bottom Line (one-sentence summary)
- Critical Issues (top 3-5 with impact)
- Competitive Position (who's winning, why)
- High-Leverage Opportunities (actionable wins)
- Strategic Recommendations (how to pitch/position)
- Key Takeaways (bullet summary)

### 3. Chat Output — Closing Notes (Conversation-Ready)

**Displayed in chat** for immediate use on closing calls.

Format: Conversational bullets you can reference naturally while talking.

---

## Research Framework

The audit adapts to the subject and context, but generally covers:

### 1. Current State Assessment

**Digital Presence** (if applicable)
- Website performance, UX, conversion optimization
- SEO fundamentals and content gaps
- Social media presence and engagement
- Online reputation and reviews

**Business Fundamentals**
- Service offerings and positioning
- Target audience clarity
- Value proposition strength
- Pricing and packaging

**Trust & Credibility Signals**
- Social proof (testimonials, case studies, reviews)
- Credentials and authority markers
- Professional presentation
- Consistency across touchpoints

### 2. Market & Competitive Analysis

**Direct Competitors**
- 2-4 key competitors analyzed
- Their strengths and weaknesses
- Feature/offer comparison
- Market positioning gaps

**Industry Benchmarks**
- Best-in-class examples
- Emerging trends and standards
- Common customer expectations
- Table stakes vs differentiators

**Whitespace Opportunities**
- What competitors aren't doing
- Underserved segments
- Unexploited channels or messaging

### 3. Customer/Audience Intelligence

**Target Audience Profile**
- Demographics and psychographics
- Pain points and motivations
- Decision-making criteria
- Common objections

**Customer Journey**
- Awareness → consideration → decision → retention
- Touchpoints and friction points
- Content gaps at each stage
- Conversion optimization opportunities

### 4. Strategic Opportunities

**Quick Wins**
- Low effort, high impact changes
- Immediate improvements
- Easy differentiators

**Medium-Term Initiatives**
- Strategic shifts requiring investment
- Capability building
- Positioning evolution

**Long-Term Plays**
- Market expansion
- Category creation
- Competitive moats

---

## Modular Usage

The audit is designed to be **modular and flexible**:

**For Building Initial Prompts**
Use audit findings to inform strategy, positioning, and key elements in your creative briefs.

**For Redesign or Refresh Projects**
Identify specific gaps, competitor advantages, and improvement opportunities to address.

**For Closing Calls & Pitches**
Reference closing notes in chat or executive summary PDF during the call. Use findings as proof of your strategic thinking.

**For Strategic Planning**
Use detailed report as foundation for recommendations, roadmap development, or business case justification.

**Standalone Research**
Sometimes you just need deep intelligence on a market, competitor, or opportunity.

---

## Process

### Step 1: Define Scope
- Clarify the subject and context
- Identify focus areas
- Set depth parameters

### Step 2: Gather Intelligence
- Analyze digital presence (if applicable)
- Research competitors and benchmarks
- Review customer feedback and market signals
- Identify patterns and gaps

### Step 3: Synthesize Findings
- Categorize by severity/impact
- Connect dots between findings
- Identify strategic themes
- Prioritize opportunities

### Step 4: Generate Detailed Report
- Write comprehensive audit to markdown file
- Structure for readability and reference
- Include specific examples and data points
- Add actionable recommendations

### Step 5: Generate Executive Summary
- Extract key points only
- Format for quick scanning
- Structure as 1-2 pages
- Make PDF-ready

### Step 6: Generate Closing Notes
- Format for conversational use
- Extract talking points
- Prioritize what to lead with
- Make immediately actionable

---

## Output Formats

### 1. Detailed Audit Report Structure

```markdown
# Deep Research Audit: [Subject]

**Context:** [Why this research was conducted]  
**Industry:** [Industry/Niche]  
**Audit Date:** [Date]  
**Auditor:** SolidState Studio

---

## Executive Summary

**Key Finding:** [One-sentence bottom line]

**Critical Issues:** [Count]  
**High-Priority Opportunities:** [Count]  
**Quick Wins:** [Count]

---

## 1. Current State Assessment

### Digital Presence (if applicable)
| Dimension | Assessment | Impact |
|-----------|------------|--------|
| [Area] | [Status] | [Business effect] |
| [Area] | [Status] | [Business effect] |

**Critical Findings:**
- **[Finding]** — [Business impact]
- **[Finding]** — [Business impact]

### Business Fundamentals
- **Positioning:** [Assessment]
- **Offerings:** [Assessment]
- **Audience Clarity:** [Assessment]

### Trust & Credibility
- **[Element]:** [Status/Assessment]
- **[Element]:** [Status/Assessment]

---

## 2. Competitive Landscape

### Competitor: [Name]
**Strengths:**
- [Advantage]
- [Advantage]

**Weaknesses (Your Opportunities):**
- [Gap]
- [Gap]

### Benchmark Comparison
| Element | Subject | Competitor 1 | Competitor 2 | Best Practice |
|---------|---------|--------------|--------------|---------------|
| [Feature] | [Status] | [Status] | [Status] | [Status] |

### Whitespace Opportunities
- [Opportunity] — [Why it matters]
- [Opportunity] — [Why it matters]

---

## 3. Audience Intelligence

### Target Profile
- **Demographics:** [Details]
- **Psychographics:** [Details]
- **Pain Points:** [List]

### Customer Journey Gaps
- **[Stage]:** [Gap] — [Impact]
- **[Stage]:** [Gap] — [Impact]

---

## 4. Strategic Opportunities

### Quick Wins (Do Now)
| Opportunity | Impact | Effort |
|-------------|--------|--------|
| [Action] | [Result] | [Low/Med/High] |

### High-Leverage Initiatives
| Initiative | Expected Outcome | Timeline |
|------------|------------------|----------|
| [Action] | [Result] | [Duration] |

### Long-Term Strategic Plays
- [Initiative] — [Outcome] — [Timeline]

---

## 5. Recommendations

### Critical (Immediate)
1. **[Problem]** → **[Solution]** → **[Expected Result]**
2. **[Problem]** → **[Solution]** → **[Expected Result]**

### High Priority (Next Phase)
1. **[Problem]** → **[Solution]** → **[Expected Result]**
2. **[Problem]** → **[Solution]** → **[Expected Result]**

### Strategic Positioning
[How to position recommendations for maximum impact]

---

## Appendix

[Additional data, screenshots, detailed notes]
```

---

### 2. Executive Summary PDF Structure

```markdown
# Executive Summary: [Business Name]

**Audit Date:** [Date]  
**Industry:** [Industry]  
**Focus:** [Context]

---

## The Bottom Line

[One powerful sentence summarizing the biggest opportunity or problem]

---

## Critical Issues

| Issue | Impact | Solution |
|-------|--------|----------|
| [Problem 1] | [Business cost] | [Fix] |
| [Problem 2] | [Business cost] | [Fix] |
| [Problem 3] | [Business cost] | [Fix] |

---

## Competitive Position

**Market Leaders:**
- [Competitor 1]: [What they do well]
- [Competitor 2]: [What they do well]

**Your Advantages:**
- [Whitespace opportunity 1]
- [Whitespace opportunity 2]

---

## High-Leverage Opportunities

✅ **[Opportunity]**  
**Current:** [What exists now]  
**Opportunity:** [What's possible]  
**Action:** [What to do]  
**Result:** [Expected outcome]

✅ **[Opportunity]**  
**Current:** [What exists now]  
**Opportunity:** [What's possible]  
**Action:** [What to do]  
**Result:** [Expected outcome]

---

## Strategic Recommendations

**Lead With:** [Key finding that grabs attention]

**Address This Objection:** [Common concern + your counter]

**Frame The Value:** [ROI or outcome projection]

**Position As:** [Strategic angle]

---

## Key Takeaways

- [Bullet 1]
- [Bullet 2]
- [Bullet 3]

---

**Full detailed audit:** `scratch/audits/[filename]`
```

**To convert to PDF:** Use md-to-pdf skill with this file.

---

### 3. Closing Notes (Chat Format)

**Purpose:** Conversation-ready bullets for use during closing calls.

**Format:**

```
CLOSING NOTES: [Business Name]

OPEN WITH THIS:
"I analyzed your current setup and found [specific finding]. Here's what that means for you..."

KEY TALKING POINTS:

1. [Specific problem] → [Business impact]
   "When I looked at your [element], I saw [issue]. That's costing you [impact]."

2. [Competitive gap] → [Your opportunity]
   "[Competitor] is doing [tactic]. You're not. That's why they're winning [outcome]."

3. [Quick win] → [Immediate result]
   "If you fix just this one thing — [action] — you'll see [result] within [timeframe]."

OBJECTION HANDLERS:

"I already get enough leads from referrals"
→ [Response based on audit finding]

"My current site is fine"
→ [Response based on specific gap]

"I need to think about it"
→ [Response based on opportunity cost]

CLOSE WITH:
"I've already built you a concept that addresses [key issue]. 10 minutes to see it — if it doesn't make sense for your business, no hard feelings."

---
REF: Full audit: [filename]
REF: Executive summary: [filename]
```

---

## Rules

- **Be specific:** "Slow website" → "4.2s mobile load time (benchmark: <2.5s)"
- **Quantify when possible:** Use numbers, percentages, counts
- **Link to business impact:** Every finding connects to revenue, leads, or positioning
- **Problem → Solution format:** Always pair issues with actionable fixes
- **Prioritize ruthlessly:** Focus on what drives results
- **Format for use:** Detailed report for reference, summary for quick scan, closing notes for conversation

---

## File Naming

**Detailed Report:** `scratch/audits/[subject]-audit-YYYY-MM-DD.md`

**Executive Summary:** `scratch/audits/[subject]-executive-summary-YYYY-MM-DD.md`

---

## Usage Workflow

**Before the call:**
1. Review Executive Summary PDF (1-2 pages) for key points
2. Skim Detailed Report if you need specific data

**During the call:**
3. Reference Closing Notes in chat for talking points
4. Use specific findings as ammunition

**After the call:**
5. Reference Detailed Report for any follow-up questions
6. Use Executive Summary for proposal or follow-up email

---

## Success Criteria

- All three outputs created and saved/displayed
- Detailed report is comprehensive (reference depth)
- Executive summary is scannable (1-2 pages max)
- Closing notes are conversational (ready to speak)
- Each output serves its specific purpose
- Key findings consistent across all three formats

---

## Notes

This skill creates your **complete audit package**: reference depth, quick-scan summary, and conversation ammunition. Use the right output for the right moment.

The difference between surface research and deep audit is the difference between "I looked at your site" and "I found 5 specific gaps costing you market share, here's the data, and here's how we fix it."

That's the moat.
