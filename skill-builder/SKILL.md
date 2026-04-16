---
name: skill-builder
description: Heavy planning back-and-forth session for building new skills. Manual collaboration mode - never automatic.
type: behavior
keywords: ["build a skill", "create skill", "new skill", "skill builder", "make a skill"]
auto_detect: true
agent_type: main
input_schema:
  skill_concept: string
  purpose: string
output_schema:
  skill_file: skills/[skill-name]/SKILL.md
  registry_entry: skills/registry/skill-index.json update
quality_metrics:
  success_rate: 1.0
  avg_tokens: 5000
evolution:
  parent: null
  version: "1.0"
  lineage: []
status: active
---

# Skill Builder — Collaborative Skill Creation

**Version:** 1.0  
**Type:** Manual Collaboration Mode  
**Status:** Active

---

## Purpose

Build new skills through heavy back-and-forth planning. Not automatic — only triggered when the user explicitly wants to create a skill.

**Use this when:**
- the user says "let's build a skill for X"
- You have a repetitive workflow that needs formalization
- You want to delegate a new type of task to sub-agents

**Don't use when:**
- the user just mentions a task (that's auto-detection)
- You've done something 2-3 times (not enough pattern)
- It's a one-off request

---

## Process (5 Phases)

### Phase 1: Concept Definition

**Goal:** One sentence description of what this skill does.

**Questions to ask:**
1. "What should this skill do in one sentence?"
2. "What problem does it solve?"
3. "Who/what will use this skill? (you, sub-agent, both)"

**Example:**
> "This skill researches any website and extracts their design patterns, color schemes, and typography for inspiration."

**Exit criteria:** Clear one-liner that the user confirms.

---

### Phase 2: Inputs & Outputs

**Goal:** Define exactly what goes in and what comes out.

**Questions to ask:**
1. "What information does it need to start? (URL? Name? Parameters?)"
2. "What format is the input? (string, URL, file path?)"
3. "What does it produce? (file, text, data?)"
4. "Where does output get saved?"

**Template:**
```yaml
input_schema:
  field_name: type (required/optional)
  
output_schema:
  file_path: location
  format: type
```

**Exit criteria:** Input/output schema defined and confirmed.

---

### Phase 3: Procedure Definition

**Goal:** Step-by-step workflow (if procedural) or guidelines (if behavioral).

**For Procedural Skills:**
1. Break into numbered steps
2. Each step has one clear action
3. Include validation/checkpoints
4. Note failure modes

**For Behavioral Skills:**
1. Define approach/philosophy
2. List DOs and DON'Ts
3. Provide examples
4. Note when to use vs alternatives

**Questions:**
- "Walk me through the steps..."
- "What could go wrong at each step?"
- "How do you know it's done?"

**Exit criteria:** Complete procedure the user confirms.

---

### Phase 4: Keywords & Detection

**Goal:** How will this skill be auto-detected?

**Questions:**
1. "What phrases would trigger this skill?"
2. "What type is this? (procedural|behavior|utility|system)"
3. "Who runs this? (main agent | sub-agent)"

**Template:**
```yaml
keywords: ["trigger", "words", "phrases"]
type: procedural|behavior|utility|system
agent_type: main|sub
```

**Exit criteria:** Keywords defined, type confirmed.

---

### Phase 5: Write & Review

**Goal:** Create the SKILL.md file.

**Steps:**
1. Write YAML frontmatter (metadata)
2. Write full SKILL.md content
3. Show the user preview
4. Revise based on feedback
5. Save to `skills/[name]/SKILL.md`
6. Add entry to `skills/registry/skill-index.json`

**Exit criteria:** Skill file created, registry updated, the user confirms it's ready.

---

## Output Format

### SKILL.md Template

```markdown
---
name: [skill-name]
description: [one sentence]
type: [procedural|behavior|utility|system]
keywords: ["word1", "word2"]
auto_detect: true
agent_type: [main|sub]
input_schema:
  field1: type
output_schema:
  file_path: path
quality_metrics:
  success_rate: 0.0
  avg_tokens: 0
evolution:
  parent: null
  version: "1.0"
  lineage: []
status: active
---

# [Skill Name]

**Version:** 1.0  
**Type:** [Type]  
**Status:** Active

---

## Purpose

[Description]

**Use this when:**
- [Condition 1]
- [Condition 2]

**Don't use when:**
- [Condition 1]
- [Condition 2]

---

## Input

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| [field] | [type] | [yes/no] | [description] |

---

## Output

[What gets produced]

---

## Procedure

### Step 1: [Action]
[Details]

### Step 2: [Action]
[Details]

---

## Failure Modes

| Issue | Response |
|-------|----------|
| [Problem] | [Solution] |

---

## Examples

**Example 1: [Scenario]**
```
Input: [example input]
Output: [example output]
```
```

---

## Rules

- **Always confirm:** [Rule 1]
- **Never:** [Rule 2]

---

## Integration

How this skill fits into the larger workflow.
```

---

## Example Session

```
the user: "Let's build a skill for researching competitors"

**Phase 1: Concept**
Me: "What should this do in one sentence?"
the user: "Research any business's competitors and analyze their positioning"

**Phase 2: Input/Output**
Me: "What does it need to start?"
the user: "Business name and location"
Me: "What does it produce?"
the user: "Competitor analysis report"

**Phase 3: Procedure**
[...back and forth on steps...]

**Phase 4: Keywords**
Me: "What phrases trigger this?"
the user: "research competitors, competitor analysis, who are their competitors"

**Phase 5: Write**
[Create file, show preview, revise, save]
```

---

## Completion Signal

When done:
> "**Skill Builder** complete — created `skills/[name]/SKILL.md` and updated registry."

---

## Notes

- This is **manual mode** — never automatic
- Take time to get it right
- the user can bail out at any phase
- Skills can be updated later via FIX
- Start simple, evolve later
