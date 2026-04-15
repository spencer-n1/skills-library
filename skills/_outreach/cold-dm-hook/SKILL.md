# Cold DM Hook Generator

**Version:** 1.0  
**Last Updated:** 2025-03-27  
**Type:** Utility

---

## What This Skill Does

Generates cold DM outreach messages for Instagram/Facebook. Input a business type, get back:
1. **The Hook** — First message that sounds like a curious customer
2. **Voice Script** — Follow-up pitch to send as voice message

---

## How It Works

### Input

- `{business_type}` — e.g., "barber", "hvac", "construction", "landscaper"
- Optional: `{area}` — for location-based hooks

### Output

1. **Hook message** — Short question designed to get a reply
2. **Voice script** — 30-60 second pitch referencing the hook

---

## Usage

**Basic:**
```
"Generate cold DM hook for barber"
"What's a good hook for electrician"
"DM script for auto mechanic"
```

**With location:**
```
"Hook for landscaper in Orange County"
"Construction business DM, area is LA"
```

---

## The Method (For Reference)

1. Like 3 posts
2. Follow them
3. Send hook message
4. When they reply → voice message pitch

**Hook Rules:**
- Sound like a curious customer
- Ask a question they'd actually reply to
- Secretly related to web design (pitch makes sense in retrospect)
- Goal = get reply, nothing else

---

## File Structure

| File | Purpose |
|------|---------|
| `hooks.json` | Business type → hook angle mapping |
| `templates.md` | Voice message templates by scenario |

---

## Example Output

**Input:** `barber`

**Hook:**
> "do you take all types of clients?"

**Voice Script:**
> "Hey thanks for replying! Real talk — I build websites for barbershops. I noticed you don't have a site and since you said you take all types of clients, figured you'd want people to actually find you online. I actually built a concept for you already. No pressure — just 10 minutes to check it out. What do you think?"

---

## Notes

- Hooks are intentionally lowercase/casual for DMs
- Voice scripts always reference back to the hook
- Area variable auto-fills as "your area" if not specified
