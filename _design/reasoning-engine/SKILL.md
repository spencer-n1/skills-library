# Reasoning Engine

**Purpose:** Analyze business type and context → recommend design direction (aesthetic, patterns, style).

Used by: `prompt-builder`, `web-builder`, and any future website-building skills.

---

## Input

- Business type (e.g., "HVAC", "law firm", "beauty spa")
- Optional context: location, target audience, brand vibe

## Output

```json
{
  "business_type": "home-services",
  "recommended_aesthetic": "navy-professional",
  "style_keywords": ["trustworthy", "urgent", "local"],
  "recommended_patterns": {
    "nav": "simple-sticky-phone",
    "hero": "split-with-form",
    "sections": ["stats-bar", "services-3-card", "why-choose-us", "reviews-carousel"],
    "cta": "final-banner"
  },
  "color_mood": "navy-blue + urgency-orange",
  "typography_mood": "bold-sans",
  "anti_patterns": ["decorative-waves", "serif-fonts", "pastel-colors"],
  "trust_signals": ["licensed-insured", "24-7", "years-experience"]
}
```

---

## Process

### Step 1: Match Business Type
Query `business-types.json` for the closest match.

### Step 2: Determine Style Direction
Use `style-matching.json` to find the best aesthetic and visual approach.

### Step 3: Select Patterns
Query `pattern-selection.json` for section recommendations based on business category.

### Step 4: Apply Taste Profile
Check `library/taste-profile.md` for overrides:
- If a pattern is marked "avoid" for this context, skip it
- If a pattern is marked "preferred", bump it to top recommendation

### Step 5: Return Complete Design Direction
Output the JSON recommendation to the calling skill.

---

## Integration with Skills

**Prompt-Builder:**
```
1. Read research file
2. Call reasoning-engine → get design direction
3. Query library for specific pattern details
4. Assemble Base44 prompt
```

**Web-Builder:**
```
1. Read requirements
2. Call reasoning-engine → get design direction
3. Query library for pattern code/specs
4. Build website/app code
```

---

## Feedback Loop

When Spencer gives feedback on a build:
1. Identify which pattern/aesthetic was used
2. Update `library/taste-profile.md`
3. Future reasoning queries will incorporate the updated preference
