# Spencer's Skills Library

> A modular, executable skill system for agency work — research, copy, code, design, sales, and ops.

This repo is the **single source of truth** for every skill in Spencer's AI agency stack. Each skill is a self-contained capability with a `SKILL.md` file that defines inputs, outputs, procedures, and failure modes.

---

## How It Works (The Orchestrator)

Every request Spencer makes is matched to a skill **before** any work happens.

1. **Parse** the request → detect intent and keywords
2. **Query** `registry/skill-index.json` → find the best match
3. **Load** the matching `SKILL.md` → follow the procedure exactly
4. **Execute** → build, write, research, or edit using the skill's authorized path
5. **Log** → report what skill was used, files touched, and how correctness was verified

### Confidence Thresholds

| Score | Action |
|-------|--------|
| **80%+** | Auto-execute single skill |
| **65–79%** | Auto-execute, announce the skill name |
| **50–64%** | Present top 2 options, wait for choice |
| **<50%** | Proceed without a skill |

### User Overrides
- "No skills" → skip the orchestrator
- "Use [skill-name]" → force a specific skill
- "Just do it" → bypass skills this time only

📄 **Read the full system in [`orchestrator.md`](orchestrator.md)**

---

## The Hard Gate (Coding Tasks)

**STOP.** If Spencer asks you to edit, fix, update, refactor, or build code, you **must** load the correct coding skill **before** opening any file.

| If Spencer says... | You must load... |
|--------------------|------------------|
| "Build a new website" | `vibe-website` |
| "Build a new app/dashboard" | `vibe-app` |
| "Edit my website/app" | `vibe-editor` |
| "Add polish / animations / fixes" | `vibe-polish` |
| "Replicate this site" | `vibe-replicate` |
| "Add an admin panel" | `vibe-admin-panel` |
| "Search / refactor code structure" | `ast-grep` |
| "Take a screenshot / test a page" | `playwright-cli` |
| "Move this to WordPress" | `base44-to-wordpress` |

**Violating this gate is a failure mode.** Self-correct immediately if you catch yourself editing code without loading the skill first.

---

## Skill Catalog

### 🔬 Research
| Skill | What It Does |
|-------|--------------|
| `business-researcher` | Research leads, extract GMB info, reviews, competitors |
| `customer-research` | Build personas, mine reviews, analyze JTBD |
| `deep-research-audit` | Run intensive comprehensive research on any business or market |
| `competitor-alternatives` | Create competitor comparison / alternative pages |
| `marketing-ideas` | Library of 139 proven marketing tactics |
| `marketing-psychology` | Apply behavioral science and persuasion principles |
| `launch-strategy` | Plan product launches, Product Hunt, waitlists |
| `pricing-strategy` | Pricing decisions, packaging, monetization |

### ✍️ Copy
| Skill | What It Does |
|-------|--------------|
| `copywriter` | On-demand copy for blogs, emails, landing pages, ads |
| `copy-editing` | Edit and tighten copy with the seven sweeps framework |
| `cold-email` | Write B2B cold emails and follow-ups |
| `email-sequence` | Build drip campaigns, nurture flows, onboarding |
| `content-strategy` | Plan pillars, topic clusters, editorial calendars |
| `seo-audit` | Technical and on-page SEO audits |
| `ai-seo` | Optimize for ChatGPT, Perplexity, Google AI Overviews |
| `schema-markup` | Add structured data / JSON-LD for rich snippets |
| `social-content` | Create LinkedIn, Twitter/X, Instagram, TikTok content |
| `humanizer` | Remove AI patterns and make copy sound natural |

### 🎯 Ads
| Skill | What It Does |
|-------|--------------|
| `paid-ads` | Google Ads, Meta, LinkedIn, Twitter/X campaigns |
| `ad-creative` | Generate headlines, descriptions, variations at scale |

### 💼 Sales
| Skill | What It Does |
|-------|--------------|
| `sales-enablement` | Pitch decks, one-pagers, objection handling, demo scripts |
| `lead-magnets` | Checklists, templates, ebooks, webinars for capture |

### 💻 Coding
| Skill | What It Does |
|-------|--------------|
| `vibe-website` | Build production-ready Next.js client websites |
| `vibe-app` | Build React + Vite + Tailwind apps and dashboards |
| `vibe-editor` | Surgical edits on existing vibe projects |
| `vibe-polish` | Portfolio-ready polish, animations, micro-interactions |
| `vibe-replicate` | Rebuild a site from source + screenshots |
| `vibe-admin-panel` | Add password-protected admin/CMS panels |
| `ast-grep` | Structural code search and replace |
| `playwright-cli` | Browser automation, screenshots, form filling |
| `base44-to-wordpress` | Base44 → WordPress/Elementor transfer pipeline |

### 🎨 Design
| Skill | What It Does |
|-------|--------------|
| `reasoning-engine` | Analyze business types and recommend aesthetics, patterns, styles |

### 💬 Prompts
| Skill | What It Does |
|-------|--------------|
| `prompt-builder` | Build client website prompts from research |
| `code-prompt-builder` | Build compressed code-like prompts for complex apps |
| `prompt-redesign` | Create redesign prompts from existing URLs |
| `prompt-engineering` | Surgical prompt editing |

### 📣 Outreach
| Skill | What It Does |
|-------|--------------|
| `cold-dm-hook` | Generate personalized cold DM hooks |
| `follow-up-email` | Follow-up emails after cold calls |
| `thank-you-email` | Post-launch thank you emails for clients |

### 🔧 Utility
| Skill | What It Does |
|-------|--------------|
| `skill-builder` | Build new skills through collaborative planning |
| `git-backup` | Backup repos and manage snapshots |

### 🧰 Misc
| Skill | What It Does |
|-------|--------------|
| `reviewer` | Review output, score quality, catch errors |
| `md-to-pdf` | Convert Markdown documents to PDF |

---

## Common Skill Chains

These workflows run in sequence:

| Goal | Chain |
|------|-------|
| **New client website** | `customer-research` → `copywriter` → `vibe-website` |
| **Agency outreach** | `lead-magnets` → `cold-email` |
| **Content campaign** | `content-strategy` → `copywriter` → `social-content` |
| **Product launch** | `launch-strategy` → `email-sequence` → `social-content` |
| **SEO overhaul** | `seo-audit` → `schema-markup` → `ai-seo` |
| **App build** | `code-prompt-builder` → `vibe-app` |
| **Website polish** | `vibe-polish` |
| **Surgical edit** | `vibe-editor` |

---

## Repo Structure

```
_orchestrator.md          # Full orchestrator rules and protocols
README.md                 # You are here
registry/
  skill-index.json        # The master skill registry
_research/                # Research skills
_copy/                    # Copywriting skills
_ads/                     # Advertising skills
_sales/                   # Sales skills
_coding/                  # Coding/build skills
_design/                  # Design reasoning and library
_prompts/                 # Prompt engineering skills
_outreach/                # Outreach skills
_misc/                    # Misc utilities
skill-builder/            # Skill creation skill
reviewer/                 # Quality review skill
git-backup/               # Git utility skill
```

---

## Rules for Agents

1. **Read `registry/skill-index.json` before acting.**
2. **Skills are mandatory, not optional.** If it matches, you must use it.
3. **Never edit code without loading the coding skill first.**
4. **Use subagents** for any skill with 5+ steps or 3+ file reads.
5. **Log every execution:** skill name, tier/phase, files touched, verification.

---

*Questions? Read [`orchestrator.md`](orchestrator.md) for the complete system spec.*
