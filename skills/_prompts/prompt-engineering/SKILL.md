---
name: prompt-engineering
description: Surgical editing of existing prompts using the edit tool. Only change what is specifically requested — no rewriting, no cleaning up, no "improving."
type: behavior
keywords: ["engineer prompt", "fix prompt", "update prompt", "prompt engineering", "edit prompt", "refine prompt", "change prompt", "modify prompt", "prompt", "update the skill", "fix the skill", "edit the prompt"]
auto_detect: true
agent_type: main
input_schema:
  existing_prompt_file: string
  changes: specific edits to make
output_schema:
  file_path: same file (edited in place)
quality_metrics:
  success_rate: 0.95
  avg_tokens: 2000
evolution:
  parent: null
  version: "3.2"
  lineage: []
status: active
---

# Prompt Engineering

**Skill:** Surgical editing of existing prompts using the `edit` tool

---

## Purpose

Make precise, surgical changes to existing prompt files. **Only change what Spencer specifically requests.** Nothing else. No rewriting. No "improving." No shortening. No formatting cleanup.

---

## Activation

**Enter skill mode when Spencer says:**
- "Skill mode: prompt-engineering"
- "Use prompt-engineering skill"
- "Prompt engineering mode"
- "Update the skill to..."

**Lock behavior:** Stay in this workflow until explicitly told otherwise or task completes.

**ALSO auto-trigger when:**
- Target file path contains `/prompts/`
- Target file ends in `.md` and path includes "prompt"
- Spencer says "add to [filename]" and [filename] is in prompts/
- Any request that would modify a prompt file

---

## MANDATORY RULE — NO EXCEPTIONS

**NEVER edit a prompt file without following this skill workflow.**

**If you are about to use the `edit` tool on ANY file in `prompts/`:**
1. STOP
2. Read this skill file completely
3. Follow the workflow exactly (Clarify → Confirm → Edit)
4. If you already started editing without following the skill: STOP and notify Spencer

**This applies to:**
- Any `.md` file in `prompts/` directory
- Any file Spencer refers to as "the prompt" or "prompt file"
- Any file with "prompt" in the name

**NO EXCUSES:** "I forgot", "It was just a small change", "I already knew what to do" — none of these override this rule.

---

## Pre-Edit Safety Gate

**Before ANY edit tool call on a prompt file, you MUST:**

1. Say explicitly: "This is a prompt file. Activating prompt engineering skill."
2. Read the skill file (this file) completely
3. Confirm the bullet-point list of changes with Spencer
4. Only then proceed to edit

**If you catch yourself about to edit without doing steps 1-3:**
→ STOP. Say: "I was about to edit without following the skill. Let me do this properly."
→ Then follow the workflow.

---

## Pre-Flight Checklist

Before touching any files:

1. **Read the complete file** — Use `read` to load the entire file. Don't assume you know it.
2. **Confirm exact changes** — Get the complete list of what Spencer wants changed.
3. **Confirm scope** — Ask: "Just to confirm, I should ONLY change [X] and leave everything else exactly as-is?"
4. **Signal lock-in:** Reply: "Prompt engineering mode locked. Editing `[filename]` — changing only: [list]."

**If uncertain:** Pause and ask. Never proceed with unclear requirements.

---

## The Workflow

### 1. Read The Entire File

```
read: file_path
```

Load the complete file into context. You need to see the exact text you're editing.

### 2. Confirm Exact Changes

Extract the complete list of changes from Spencer's request.

**If he gives you multiple items at once:**
- List them all in bullet points
- Ask: "Did I capture all changes correctly?"

**If he gives you one item:**
- Confirm: "Just to confirm: Change [X] to [Y] — correct?"

### 2.5 Clarify All Changes (NEW STEP)

**BEFORE executing ANY edits**, convert Spencer's request into a bullet-point list of specific changes:

**Format:**
> **Proposed Changes to `[filename]`:**
> - [Section]: Change "[old]" → "[new]"
> - [Section]: Add [description]
> - [Section]: Remove [description]
> - [etc.]

**Then wait for confirmation:** "Confirm these changes? (yes/no/modify)"

**DO NOT proceed to Step 3 until Spencer confirms.**

### 3. Use edit Tool — Surgical Only

Use the `edit` tool with **exact text matching**:

```
edit:
  file_path: /path/to/file.md
  old_string: "EXACT text to find (including newlines, spaces, everything)"
  new_string: "EXACT replacement text"
```

**CRITICAL:** The `old_string` must match the file **exactly** — character for character, whitespace and all.

### 4. Change ONLY What Was Asked

| Allowed | NOT Allowed |
|---------|-------------|
| Remove a specific line | Remove "unnecessary" lines you think don't matter |
| Add a specific sentence | "Improve" the writing while I'm here |
| Change a specific word | Reformat sections for "consistency" |
| Replace a specific section | Rewrite paragraphs to be "cleaner" |
| Move content as requested | Reorganize structure because it "makes more sense" |

**Rule:** If Spencer didn't say to change it, DON'T TOUCH IT.

---

## Universal vs. Specific Changes

When Spencer requests changes, look for patterns that could become universal rules. This keeps prompts concise without losing specificity.

### When to Propose Universal Rules

**Use specific edits when:**
- One-off fix or unique case
- Exception to an existing pattern
- Details would be lost in a universal rule

**Propose universal rules when:**
- Same pattern applies to 3+ places
- Change is a design principle (icons vs emojis, hover states, etc.)
- Future similar cases would need the same change

### How to Propose

Instead of listing every instance, propose a universal rule and ask:

> "Instead of editing each card individually, I can add a universal rule: 'Use icons only, never emojis anywhere in the UI.' This covers all current and future cases. Should I do that?"

**Example:**
- ❌ "Remove 🔥 from Call Goal card, remove 🔥 from DM Goal card..."
- ✅ "Add to Design System: 'Use icons only, never emojis' — covers all UI elements"

### Key Constraint

**Never sacrifice specificity for brevity.** If a universal rule would cause details to be missed, stay specific. Universal rules should capture patterns, not gloss over important distinctions.

---

## Optional: Universal Review

**When Spencer says:** "Review for universal rules" or "Can this be more universal?"

**Process:**
1. Read the complete prompt
2. Identify repetitive patterns (same styling on 3+ elements, repeated phrases, etc.)
3. Propose universal rules that compress without losing meaning
4. Get confirmation before applying

**Scope:** Minor compressions only. Don't remove sections or change structure. Just consolidate repetitive specs into principles.

---

### 5. Verify Nothing Else Changed

After editing:

1. Read the file again
2. Confirm only the requested changes were made
3. Verify no accidental formatting changes
4. Check that line breaks, spacing, bullet points are intact

---

### NO Thinking Out Loud Rule

❌ **Don't narrate your process:**
- "Hmm, let me check this..."
- "I think I see what you mean..."
- "Let me find that section..."
- "Good progress..."
- "Working on this..."

✅ **Just state facts and ask for confirmation:**
- "Found 3 changes to make. Listing them now:"
- "Clarifying before I edit:"
- "Confirming scope: [X] only — correct?"

---

## Critical Rules

### DO:
- ✅ Use `edit` tool with exact text matching
- ✅ Read the complete file first
- ✅ Confirm exact scope before editing
- ✅ Change ONLY what Spencer requested
- ✅ Preserve all existing formatting, spacing, structure
- ✅ Verify the edit worked correctly
- ✅ Signal skill mode activation

### DON'T:
- ❌ Rewrite the entire prompt "cleanly"
- ❌ "Improve" writing that's not part of the request
- ❌ Reformat sections for consistency
- ❌ Remove "unnecessary" details you notice
- ❌ Shorten descriptions that seem too long
- ❌ Change anything outside the requested scope
- ❌ Assume you remember the file contents — READ it

---

## Common Mistakes to Avoid

| Mistake | Why It Fails | Correct Approach |
|---------|--------------|------------------|
| Rewriting from memory | Forgets details, changes wording unintentionally | `read` the file, then `edit` exactly |
| "Cleaning up" while editing | Changes Spencer didn't ask for | Change ONLY what was requested |
| Reformatting bullet points | Breaks existing structure | Keep exact formatting |
| Shortening long descriptions | Removes information Spencer wants | Leave text exactly as-is |
| Not verifying the edit | May have accidentally changed more | Always re-read and confirm |

---

## Error Handling

**If file missing:**
→ Stop. Ask Spencer to provide correct path.

**If edit fails (no match):**
→ Re-read the file. The `old_string` didn't match exactly. Get the exact text including whitespace.

**If Spencer says "that's not what I asked for":**
→ You touched something you shouldn't have. Revert and be more surgical.

**If Spencer adds more changes mid-work:**
→ Complete current edit, then confirm: "You also want [new change] — should I do that as a separate edit?"

---

## Completion Signal

**Only execute edits AFTER Spencer confirms the bullet-point list.**

Once all edits are complete:

> "**Prompt engineered!** Edited: `[filename]`"

Include:
- Explicit "Prompt engineered!" header
- File path
- Exact changes made (bullet list)
- Confirmation that nothing else was touched

**Example:**
```
Prompt engineered! Edited: prompts/redesign/SolidState-Studio-Zero-Client-Redesign.md

Changes made:
- Navigation section: Removed FEATURED WORK link
- Left nav: HOME, WHY CHOOSE US
- Right nav: SERVICES, PORTFOLIO, CTA

Everything else left exactly as-is.
```

---

## Complex Logic Formatting Guidelines

When Spencer asks to format or emphasize complex/critical logic sections, use these patterns:

### 1. Visual Hierarchy for Critical Sections

```markdown
---

## ⚠️ CRITICAL LOGIC — [Section Name]

**WHY THIS MATTERS:**  
One sentence explaining the business purpose. This helps developers understand intent before implementation.

**MUST IMPLEMENT EXACTLY AS FOLLOWS:**
```

### 2. Use Tables for Rule Definitions

Complex logic with multiple conditions should use tables:

```markdown
| Scenario | Action | Result | Why |
|----------|--------|--------|-----|
| Adding monthly client | Total += one-time + first month | Immediate update | Cash received now |
| Month anniversary | Total += monthly amount | Auto-increment | Recurring payment |
| Deleting client | Total STAYS SAME | No decrease | Historical record |
```

### 3. Use Code Blocks for Examples

Show the math/behavior with code blocks:

```markdown
```
Monthly Client: $800 + $50/month
→ Total: $850 (immediate)
→ Monthly Recurring: +$50
```
```

### 4. Repeat Vital Constraints

Critical warnings should appear **at least twice** in the section:

```markdown
**⚠️ CRITICAL WARNING — Total Revenue Never Decreases:**  
Deleting a client preserves historical payments. Total Revenue STAYS THE SAME.

| Metric | Behavior |
|--------|----------|
| **Total Revenue** | **STAYS THE SAME** ← repeated in table too |
```

### 5. Include Verification Checklist

End complex logic sections with testable checkboxes:

```markdown
### Implementation Verification

After building, confirm ALL of these:

- [ ] New monthly client shows $850 Total Revenue immediately
- [ ] Month later, Total Revenue auto-increments to $900
- [ ] Deleting client: Total Revenue STAYS THE SAME
```

### 6. Separate WHY from HOW

```markdown
**WHY:** Total Revenue shows cash already received. Must never decrease.

**HOW:** 
- On sale: Total += one-time + first recurring
- On anniversary: Total += recurring amount
- On delete: Total unchanged, recurring stats decrease
```

---

*Skill Version: 3.3 — April 5, 2026 (Added Complex Logic Formatting Guidelines)*
