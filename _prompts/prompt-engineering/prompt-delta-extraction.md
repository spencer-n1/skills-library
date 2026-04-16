# Prompt Delta Extraction

Use this at the end of any Base44 edit session to capture changes as structured deltas your prompt engineering agent can apply surgically.

---

**Paste this into Base44:**

```
Summarize every change made in this session as a structured prompt delta. My prompt engineering agent has zero context from this conversation — these deltas must be self-contained and actionable.

Format per change:

LOCATION: [Section → Subsection]
TYPE: [add | modify | delete | fix | refactor]
---
PROSE: What changed and why. Include the trigger (what was wrong or missing) and the resolution.
---
SPEC: Exact new logic in pseudocode, shorthand, or precise descriptive format. If modifying existing content, show the delta clearly (before/after or strikethrough/insertion). If adding, show full new block.

Rules:
- One delta per distinct logic change. Group related UI tweaks together.
- SPEC must be copy-paste ready into my master prompt without interpretation.
- If a change fixes a bug, explicitly state the failure mode that was prevented.
- Never summarize with "updated the styling" — show the exact CSS/values.
- If a change affects multiple locations, list each LOCATION separately with the same SPEC reference.
```

---

**What the fields capture:**
- **TYPE**: Prevents ambiguity about whether you're adding new content or modifying existing
- **PROSE**: Documents *why* the change happened (prevents regression)
- **SPEC**: The exact, copy-pasteable content your Kimi agent needs

**Last updated:** 2026-03-31
