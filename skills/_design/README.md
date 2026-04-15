# Design System

**Shared design library + reasoning engine for all website-building skills.**

---

## Structure

```
skills/_design/
├── library/              # Visual assets, patterns, aesthetics
├── reasoning-engine/     # Business analysis → design recommendations
├── prompt-builder/       # Base44 prompt builder skill
├── web-builder/          # Direct code builder skill (future)
└── README.md             # This file
```

---

## How It Works

1. **Reasoning Engine** analyzes the business type
2. **Library** provides the visual patterns and aesthetics
3. **Skill** (prompt-builder or web-builder) assembles the output
4. **Your feedback** evolves the library over time

---

## Library Contents

- **32 patterns** (navs, heroes, sections, CTAs, footers)
- **5 foundations** (color, typography, spacing, motion, layout)
- **10+ aesthetics** (coastal-blue, navy-gold, linear-dark, stripe-modern, etc.)
- **1 taste-profile** (your preferences and rules)

## Reasoning Engine Contents

- **13 business categories** with design recommendations
- **14 style definitions** with best-fit contexts
- **Pattern selection guide** for each section type

---

## Feedback

Tell me what you liked or hated after a build:
- "That hero worked" → preferred
- "Hated the wave divider for garages" → avoid
- "Use serif for law only" → context rule

I update `library/taste-profile.md` and future builds get better.
