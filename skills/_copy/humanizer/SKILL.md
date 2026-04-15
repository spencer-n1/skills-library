---
name: humanizer
description: Remove signs of AI-generated writing from text. Makes copy sound more natural and human by detecting 29 AI writing patterns and rewriting them.
type: utility
keywords: ["humanize", "de-ai", "natural writing", "remove AI patterns", "rewrite text", "polish copy"]
auto_detect: true
agent_type: sub
---

# Humanizer

Remove signs of AI-generated writing from text. Makes copy sound more natural, conversational, and human.

## When to Use

- After writing copy with AI assistance
- Polishing client-provided text that sounds robotic
- Before publishing any marketing content
- Editing technical docs to sound less stiff
- Any text that needs to feel authentically human

## Don't Use When

- Content needs to stay formal/technical (legal, medical, compliance)
- Preserving exact AI phrasing is required
- The text is already conversational and natural

## The 29 Patterns

### Content Patterns

| # | Pattern | Before | After |
|---|---------|--------|-------|
| 1 | **Significance inflation** | "marking a pivotal moment in the evolution of..." | "was established in 1989 to collect regional statistics" |
| 2 | **Notability name-dropping** | "cited in NYT, BBC, FT, and The Hindu" | "In a 2024 NYT interview, she argued..." |
| 3 | **Superficial -ing analyses** | "symbolizing... reflecting... showcasing..." | Remove or expand with actual sources |
| 4 | **Promotional language** | "nestled within the breathtaking region" | "is a town in the Gonder region" |
| 5 | **Vague attributions** | "Experts believe it plays a crucial role" | "according to a 2019 survey by..." |
| 6 | **Formulaic challenges** | "Despite challenges... continues to thrive" | Specific facts about actual challenges |

### Language Patterns

| # | Pattern | Before | After |
|---|---------|--------|-------|
| 7 | **AI vocabulary** | "Actually... additionally... testament... landscape... showcasing" | "also... remain common" |
| 8 | **Copula avoidance** | "serves as... features... boasts" | "is... has" |
| 9 | **Negative parallelisms** | "It's not just X, it's Y", "..., no guessing" | State the point directly |
| 10 | **Rule of three** | "innovation, inspiration, and insights" | Use natural number of items |
| 11 | **Synonym cycling** | "protagonist... main character... central figure... hero" | "protagonist" (repeat when clearest) |
| 12 | **False ranges** | "from the Big Bang to dark matter" | List topics directly |
| 13 | **Passive voice / subjectless fragments** | "No configuration file needed" | Name the actor when it helps clarity |

### Style Patterns

| # | Pattern | Before | After |
|---|---------|--------|-------|
| 14 | **Em dash overuse** | "institutions—not the people—yet this continues—" | Prefer commas or periods |
| 15 | **Boldface overuse** | "**OKRs**, **KPIs**, **BMC**" | "OKRs, KPIs, BMC" |
| 16 | **Inline-header lists** | "**Performance:** Performance improved" | Convert to prose |
| 17 | **Title Case Headings** | "Strategic Negotiations And Partnerships" | "Strategic negotiations and partnerships" |
| 18 | **Emojis** | "🚀 Launch Phase: 💡 Key Insight:" | Remove emojis |
| 19 | **Curly quotes** | `said "the project"` | `said "the project"` |
| 26 | **Hyphenated word pairs** | "cross-functional, data-driven, client-facing" | Drop hyphens on common word pairs |
| 27 | **Persuasive authority tropes** | "At its core, what matters is..." | State the point directly |
| 28 | **Signposting announcements** | "Let's dive in", "Here's what you need to know" | Start with the content |
| 29 | **Fragmented headers** | "## Performance" + "Speed matters." | Let the heading do the work |

### Communication Patterns

| # | Pattern | Before | After |
|---|---------|--------|-------|
| 20 | **Chatbot artifacts** | "I hope this helps! Let me know if..." | Remove entirely |
| 21 | **Cutoff disclaimers** | "While details are limited in available sources..." | Find sources or remove |
| 22 | **Sycophantic tone** | "Great question! You're absolutely right!" | Respond directly |

### Filler and Hedging

| # | Pattern | Before | After |
|---|---------|--------|-------|
| 23 | **Filler phrases** | "In order to", "Due to the fact that" | "To", "Because" |
| 24 | **Excessive hedging** | "could potentially possibly" | "may" |
| 25 | **Generic conclusions** | "The future looks bright" | Specific plans or facts |

## Process

### Step 1: First Pass
Read through the text and identify all 29 patterns that appear. Mark each instance.

### Step 2: Rewrite
Rewrite the text removing or fixing each pattern:
- Replace AI vocabulary with simple words
- Remove filler and hedging
- Convert passive to active where helpful
- Remove chatbot artifacts entirely
- Make lists natural length
- Replace vague claims with specifics

### Step 3: Audit Pass
Read the rewritten text. Does it still sound obviously AI-generated?

**Check for lingering AI-isms:**
- Overly formal or stilted phrasing
- Generic conclusions
- Unnatural transitions
- Remaining buzzwords

### Step 4: Voice Calibration (Optional)
If user provides 2-3 paragraphs of their own writing:
- Analyze their sentence rhythm
- Note word choices and quirks
- Apply those patterns to the rewrite

## Output Format

**Before:**
```
[Original AI-sounding text]
```

**After:**
```
[Humanized text]
```

**Changes made:**
- Pattern X: [description of change]
- Pattern Y: [description of change]

## Example

**Before:**
> Great question! AI-assisted coding serves as an enduring testament to the transformative potential of large language models, marking a pivotal moment in the evolution of software development. In today's rapidly evolving technological landscape, these groundbreaking tools—nestled at the intersection of research and practice—are reshaping how engineers ideate, iterate, and deliver, underscoring their vital role in modern workflows.

**After:**
> AI coding assistants can speed up the boring parts of the job. They're great at boilerplate: config files and the little glue code you don't want to write. They can also help you sketch a test, but you still have to read it.

## Related Skills

- **copywriting** — Write initial copy, then humanize it
- **copy-editing** — Seven sweeps for editing; humanizer is the final polish
- **output-reviewer** — Quality check before humanizing
