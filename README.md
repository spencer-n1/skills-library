# Skills Library

This is Spencer's personal AI skill library — a collection of documented, procedural capabilities used by his coding agent (Kimi Code CLI) to execute complex tasks consistently.

Think of it as an operating system extension: each skill contains step-by-step instructions, constraints, examples, and failure modes for a specific domain.

---

## How It Works

### 1. The Orchestrator

Every request starts with the **Orchestrator** (`ORCHESTRATOR.md`). Before doing any work, the agent:

1. Parses your intent
2. Queries the **Skill Registry** (`skills/registry/skill-index.json`)
3. Suggests the best matching skill(s)
4. Waits for your confirmation
5. Loads the skill file and executes it exactly as written

**You can always override the orchestrator:**
- Say **"just do it"** or **"no skills"** to skip suggestions
- Say **"use [skill-name]"** to force a specific skill
- Chain manually: **"Do customer-research, then copywriter"**

### 2. The Registry

`skills/registry/skill-index.json` is the single source of truth for all available skills. Each entry contains:

```json
{
  "name": "skill-name",
  "description": "What it does",
  "path": "skills/category/skill-name/SKILL.md",
  "keywords": ["trigger", "words"],
  "category": "research|copy|ads|sales|coding|design|misc|utility",
  "type": "procedural|utility|reference"
}
```

The agent matches requests using:
- **Keywords** (primary)
- **Description** (secondary)
- **Category** (contextual)

### 3. Skill Structure

Every skill lives in its own folder and includes a `SKILL.md` file. Depending on the skill, it may also include:
- JSON data files
- Template files
- Helper scripts
- Reference materials

Skills are designed to be **read and executed**, not just referenced. They contain:
- Pre-flight checks
- Step-by-step procedures
- Validation checklists
- Universal rules (non-negotiable)
- Failure modes and error handling

---

## Skill Categories

| Category | Purpose |
|----------|---------|
| **Research** | Business research, competitor analysis, customer research, marketing ideas, pricing strategy |
| **Copy** | Copywriting, email sequences, SEO audits, social content, content strategy |
| **Ads** | Paid ads strategy, ad creative generation |
| **Sales** | Sales enablement, lead magnets, outreach |
| **Coding** | Website builds, app builds, code editing, WordPress transfer, browser automation |
| **Design** | Aesthetic systems, pattern libraries, design reasoning engine |
| **Prompts** | Prompt building, prompt engineering, prompt redesign |
| **Utility** | Git backups, PDF generation, skill builder, reviewer |

---

## Common Workflows

| Goal | Skill Chain |
|------|-------------|
| Build a client website | `customer-research` → `prompt-builder` → `vibe-website` |
| Outreach campaign | `lead-magnets` → `cold-email` |
| Content campaign | `content-strategy` → `copywriter` → `social-content` |
| SEO overhaul | `seo-audit` → `schema-markup` → `ai-seo` |
| Launch a product | `launch-strategy` → `email-sequence` → `social-content` |

---

## Adding or Updating Skills

1. Create a new folder under the appropriate category (e.g., `skills/_coding/my-skill/`)
2. Write a `SKILL.md` with clear inputs, outputs, steps, and failure modes
3. Add the skill to `skills/registry/skill-index.json`
4. Commit and push

For help building a new skill, use the **`skill-builder`** skill.

---

## Key Design Principles

- **Skills are executable documents** — not reference docs, but procedures
- **Orchestrator-mediated** — no skill runs without user confirmation
- **Minimal intrusion** — skills follow existing codebase style
- **Failure-aware** — every skill documents what can go wrong and how to handle it

---

*This library is continuously evolving. Skills improve through use — patterns that work get documented, mistakes get noted with fixes.*
