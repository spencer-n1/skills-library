---
name: reviewer
description: Review any output before delivery to catch errors, gaps, or quality issues. Score quality and detect patterns for continuous improvement.
type: procedural
keywords: ["review", "check", "validate", "proofread", "verify", "quality check"]
auto_detect: true
agent_type: sub
input_schema:
  file_path: string
  content_type: enum [research, prompt, copy, email, general]
output_schema:
  report: review report with verdict
quality_metrics:
  success_rate: 0.50
  avg_tokens: 5000
evolution:
  parent: null
  version: "2.2"
  lineage: []
status: active
---

# Reviewer

**Version:** 2.2  
Review any output before delivery to catch errors, gaps, or quality issues. Score quality and detect patterns for continuous improvement.

---

## When to Use

- Before sending research to prompt-builder
- Before delivering prompts to clients
- Before publishing any copy or content
- When you say "review this first" or "check this"
- After any new skill runs for the first time

## Don't Use When

- The output is clearly a rough draft (wait for final version)
- Time constraints make thorough review impossible
- The content is internal/experimental only

---

## 7-Point Review System

1. **Accuracy** — Facts, dates, numbers, citations
2. **Completeness** — Full brief met, all sections present
3. **Tone & Voice** — Brand match, appropriate formality
4. **Logic & Flow** — Arguments make sense, smooth transitions
5. **Formatting** — Professional, scannable, meets specs
6. **Hallucination** — No AI inventions, fake sources
7. **Value-Add** — Strategic insights, customization

---

## Input

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `file_path` | string | Yes | Path to file to review |
| `content_type` | enum | Yes | `research`, `prompt`, `copy`, `email`, `general` |
| `context` | string | No | What this is for |
| `source_skill` | string | No | Which skill created this |

---

## Output

Returns a review report with:
- **Verdict:** `✅ PASS` or `❌ NEEDS WORK`
- **Quality Score:** 0-100 with category breakdown
- **Issues Found:** List of specific problems
- **Patterns Detected:** Recurring issues or strong points
- **Suggested Fixes:** Actionable corrections
- **Skill Update Suggestions:** Patterns worth adding to SKILL.md

---

## Quality Scoring

### Research Scoring

| Category | Points | Criteria |
|----------|--------|----------|
| **Completeness** | 25 | Business name, contact, services, reviews, location |
| **Accuracy** | 25 | No factual errors, sources cited |
| **Actionability** | 25 | Key findings highlighted |
| **Organization** | 25 | Logical structure, easy to scan |

### Prompt Scoring

| Category | Points | Criteria |
|----------|--------|----------|
| **Completeness** | 25 | All sections filled, no placeholders |
| **Clarity** | 25 | Specific instructions, clear CTAs |
| **Tone Match** | 25 | Voice fits industry and brand |
| **Structure** | 25 | Logical flow, proper formatting |

### Copy Scoring

| Category | Points | Criteria |
|----------|--------|----------|
| **Accuracy** | 15 | Facts verified, sources real |
| **Completeness** | 15 | Full brief met |
| **Tone & Voice** | 20 | Brand voice match |
| **Logic & Flow** | 20 | Smooth transitions |
| **Formatting** | 15 | Professional presentation |
| **Value-Add** | 15 | Strategic insights |

### Scoring Interpretation

| Score | Verdict |
|-------|---------|
| 90-100 | ✅ **PASS** |
| 70-89 | ⚠️ **PASS WITH NOTES** |
| 50-69 | ❌ **NEEDS WORK** |
| 0-49 | ❌ **REDO** |

---

## Checklists by Type

### Research Review
- [ ] Business name clearly stated
- [ ] Contact info present
- [ ] Services listed
- [ ] Review stats included
- [ ] 3-5 review quotes extracted
- [ ] Platforms/tools identified
- [ ] Key findings highlighted
- [ ] No obvious factual errors

### Prompt Review
- [ ] Clear brand voice defined
- [ ] Target audience specified
- [ ] Services mapped to sections
- [ ] Visual direction included
- [ ] CTA strategy specific
- [ ] All placeholders filled
- [ ] Company Information section at bottom

### Copy Review
- [ ] Facts verified
- [ ] Full brief met
- [ ] Brand voice consistent
- [ ] Active voice used
- [ ] Smooth transitions
- [ ] Professional formatting
- [ ] No hallucinations
- [ ] Strategic insights present

### Email Review
- [ ] Subject line compelling
- [ ] Opening personalized
- [ ] Purpose clear
- [ ] Ask specific and easy
- [ ] No walls of text
- [ ] Signature included

---

## Output Format

```markdown
## Review Report: [filename]

**Content Type:** [research|prompt|copy|email|general]
**Source Skill:** [skill-name]
**Verdict:** [✅ PASS | ⚠️ PASS WITH NOTES | ❌ NEEDS WORK]

### Quality Score: [XX]/100

| Category | Score | Notes |
|----------|-------|-------|
| [Category 1] | [X]/25 | [brief note] |

### Summary
[1-2 sentence overview]

### Issues Found
| # | Issue | Location | Severity |
|---|-------|----------|----------|
| 1 | [description] | [section] | [critical/medium/low] |

### Suggested Fixes
- **Issue 1:** [specific fix]

### Patterns Detected
**Recurring Issues:**
- [Pattern] - [frequency]

**Strong Points:**
- [What's working]

### Quick Wins
- [easy improvements]
```

---

## Rules

- **Score honestly** — Don't inflate to be nice
- **Be specific** — Line/paragraph references
- **Prioritize** — Critical issues first
- **Pattern detection** — Note recurring issues
- **Err on side of flagging** — Better to catch small than miss big

---

## Related Skills

- **humanizer** — Remove AI patterns from copy
- **copy-editing** — Seven sweeps for detailed editing
- **copywriter** — Create the copy to be reviewed
