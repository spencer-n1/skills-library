# Kimi Code Orchestrator

**Purpose:** Detect and auto-execute the correct skill for every request. Skills are **mandatory workflows**, not optional suggestions.

---

## Core Philosophy

**Process over guessing.** Every request that matches a skill must run through that skill's procedure. The skill is the only authorized path to the goal.

This is not a suggestion box. This is a **command center**.

---

## Iron Rules

### Rule 1: Check for skills BEFORE doing anything
Read `registry/skill-index.json` on every substantive request. Match against keywords, description, and category.

### Rule 2: Auto-execute on match
If confidence is **70%+**, load the skill and execute it **immediately**. Do not ask for permission unless one of the exceptions below applies.

**Exceptions (ask for confirmation):**
- Multiple skills match with similar confidence (within 15 points)
- The request is ambiguous or missing critical details
- The task involves deletion, deployment, or external publication
- User explicitly says "don't use skills" or "just do it"

### Rule 3: Hard gate for all coding tasks
**STOP.** If the user requests any edit, fix, change, update, refactor, addition, or build for:
- An existing project in `Kimi Code Apps/`
- Any existing `vibe-website` or `vibe-app` project
- Any file with `.tsx`, `.ts`, `.jsx`, `.js`, `.css`, `.json` config

You **MUST** load the appropriate coding skill **BEFORE** touching any file.

| Request Type | Mandatory Skill |
|--------------|-----------------|
| Edit/update/refactor existing website/app | `vibe-editor` |
| Build new website from scratch | `vibe-website` |
| Build new app from scratch | `vibe-app` |
| Add admin panel to existing project | `vibe-admin-panel` |
| Polish/animations on existing project | `vibe-polish` |
| Replicate/clone existing project | `vibe-replicate` |
| Structural code search needed | `ast-grep` |
| Browser automation/testing | `playwright-cli` |
| Base44 → WordPress transfer | `base44-to-wordpress` |

**Violating this gate is prohibited.** If you edit code without first loading the skill, you have failed.

### Rule 4: Use subagents for non-trivial tasks
If a skill's procedure has more than 5 steps, or requires reading more than 3 files, **delegate to a subagent** via the `Agent` tool.

- Load the full skill text into the subagent's prompt
- Include the user's exact request
- The subagent executes the skill procedure in isolation
- You verify the output before reporting back

### Rule 5: Log every skill execution
After completing any skill, report:
1. **Skill loaded:** [name]
2. **Tier/phase:** [what part of the skill was executed]
3. **Files touched:** [list]
4. **Verification:** [how you confirmed correctness]

---

## Execution Process

### Step 1: Parse User Request
Extract:
- Main intent (what they want to do)
- Context (business type, goal, constraints)
- Explicit mentions ("write email", "audit SEO", "edit my app")
- **Hard gate triggers** (any mention of editing/building code)

### Step 2: Query Registry
Read `registry/skill-index.json`

Match against:
- **Keywords** — Direct phrase matching (highest weight)
- **Description** — Semantic intent matching
- **Category** — Research, Copy, Ads, Sales, Coding, Design, Prompts, Utility
- **Hard gate category** — Coding requests auto-boost to coding skills

### Step 3: Execute or Escalate

**Single match (80%+ confidence):**
> Executing **[skill-name]**...
> [Load skill, follow procedure, do the work]

**Multiple matches (50-79% confidence):**
> I see a few possible approaches:
> 1. **[skill-1]** — [description]
> 2. **[skill-2]** — [description]
>
> Which fits best? (or say "none" to proceed without skills)

**No match (<50%):**
> Proceeding without a skill.

### Step 4: Post-Skill
If a natural next skill exists in a common chain, suggest it:
> **[skill-1]** complete ✓
>
> Ready for **[skill-2]**? [yes / no]

---

## Confidence Thresholds

| Score | Action |
|-------|--------|
| 80%+ | Auto-execute single skill |
| 65-79% | Auto-execute, but briefly announce which skill is running |
| 50-64% | Present top 2 skills, wait for user choice |
| <50% | Proceed normally without skill assistance |

---

## User Override

User can always:
- **Say no** — "No, just do it normally" (skip skill this time)
- **Name different skill** — "Use copy-editing instead"
- **Chain manually** — "Do customer-research then copywriting"
- **Skip orchestrator globally** — "Don't suggest skills for this" / "No skills"

---

## Skill Chains

Common workflows that chain skills:

| Workflow | Skills in Order |
|----------|-----------------|
| **New Client Website** | customer-research → copywriter → vibe-website |
| **Agency Outreach** | lead-magnets → cold-email |
| **Content Campaign** | content-strategy → copywriter → social-content |
| **Launch** | launch-strategy → email-sequence → social-content |
| **SEO Overhaul** | seo-audit → schema-markup → ai-seo |
| **App Build** | code-prompt-builder → vibe-app |
| **Website Polish** | vibe-polish (standalone) |
| **Surgical Edit** | vibe-editor (standalone) |

---

## Subagent Delegation Protocol

For any matched skill that requires reading 3+ files or has 5+ procedural steps:

1. Read the full `SKILL.md` file
2. Spawn a subagent with:
   - The complete skill text
   - The user's exact request
   - Any relevant file paths or context
3. Subagent executes the skill procedure
4. Review subagent output for completeness
5. Report back to user with the execution log

---

## Universal Rules

### Rule 1: Source Code Wins on Structure
If the source has 8 pages, the rebuild has 8 pages. No shortcuts.

### Rule 2: Screenshots Win on Visuals
If the live site has a blurred nav on scroll but the code doesn't show it clearly, replicate the visual behavior.

### Rule 3: Prompt Wins on Intent
If the user explicitly asked for something in the prompt that got lost in the source code, honor the original request.

### Rule 4: Clean Rebuild Only
Exports are noisy. Extract the intent, then rewrite it cleanly.

### Rule 5: Surgical Fixes
If something is slightly off after the build, fix the specific file/line. Do not rewrite entire sections.

---

## Failure Modes

| Issue | Response |
|-------|----------|
| Registry missing | "Skills unavailable. Proceeding normally." |
| Skill file missing | "Skill [name] not found. Proceeding normally." |
| User declines skill | "No problem. Proceeding without skills." |
| Ambiguous request | Ask clarifying questions before selecting skill |
| Hard gate violated | **Self-correct:** stop editing, load required skill, restart from step 1 |
