---
name: thank-you-email
description: Generate post-launch thank you email for clients. Crafts unique opening paragraph based on context, with flexible PS and sign-off options.
type: procedural
keywords: ["thank you email", "client email", "post launch email", "appreciation email"]
auto_detect: true
agent_type: main
input_schema:
  website_url: string
  client_name: string
  your_name: string
output_schema:
  file_path: scratch/emails/thank-you-[client-name]-YYYY-MM-DD.txt
quality_metrics:
  success_rate: 0.80
  avg_tokens: 2000
evolution:
  parent: null
  version: "1.1"
  lineage: []
status: active
---

# thank-you-email — SKILL.md

**Version:** 1.1  
**Last Updated:** 2026-03-30  
**Type:** Procedural

---

## Purpose

Generate the post-launch thank you email for clients. Crafts a unique opening paragraph based on context, with flexible PS and sign-off options.

---

## Input

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `website_url` | string | Yes | Client's live website URL |
| `client_name` | string | Yes | Client's first name |
| `your_name` | string | Yes | Your name for sign-off |
| `your_email` | string | Yes | Your email |
| `your_phone` | string | No | Your phone number |
| `industry` | string | No | Industry for subtle personalization (e.g., "plumbing", "photography") |
| `ps_style` | enum | No | `standard`, `fast-turnaround`, `growth-focused`, `confident`, `results-tease` — default: `standard` |
| `tone` | enum | No | `standard`, `supportive`, `excited`, `casual`, `always-here` — default: `standard` |
| `context_notes` | string | No | Any notes about the project to inform opening paragraph |

---

## Output

### 1. Email File

Saved to: `scratch/emails/thank-you-[client-name]-YYYY-MM-DD.txt`

### 2. Chat Confirmation

Displays the generated email for immediate use.

---

## Email Structure

**SUBJECT:** Your new website is live! 🚀

**BODY:**

Hey [First Name],

**Your new site is live:** [URL]

[UNIQUE OPENING PARAGRAPH — crafted based on project context, industry, and notes]

Take a look around and let me know what you think — if anything needs tweaking or you spot something you want adjusted, just shoot me a message and I'll take care of it.

A couple quick questions while it's fresh:
- **Are you satisfied with how everything turned out?**
- **What could I have done better during this whole process?**
- **Anything you'd suggest I change or improve?**

Also, if you have a minute to leave a review on my Google Business Profile, it would mean a lot. No pressure at all — only if you genuinely had a good experience working with me.

Quick favor: I'm always looking to help more business owners like you. **Who do you know that could use a website like this?** A friend, family member, or another business owner who needs a better online presence? Send them my way.

Thanks for trusting me with this project.

[SIGN-OFF based on tone selection],
[Your Name]  
[Your Email]  
[Your Phone]

[P.S. based on ps_style selection]

---

## Opening Paragraph Examples

Crafted uniquely based on context. Previous successful examples:

**Conversion-focused:**
> I built this to be clean, professional, and actually get you results.

**Clean redesign:**
> I built this to give you a clean, professional presence that represents your business well.

**Minimal:**
> This gives you a solid foundation to build on — clean, professional, and ready to grow with you.

**Informational:**
> This gives you a professional home base for your business — clean, easy to navigate, and built to make a strong first impression.

**Industry-personalized:**
> I built this to make homeowners choose you when they need [industry] services.

**Competitive:**
> Built this to make [industry] customers choose you over the competition.

**Foundation-focused:**
> This gives you a foundation that actually works — not just looks pretty.

**Results-focused:**
> Clean, fast, and ready to bring you business.

**Craft fresh variations based on:**
- Project scope and depth
- Industry vibe (professional, creative, trades, luxury, etc.)
- Client personality (if known)
- Specific context notes provided

---

## PS Style Options

| Option | P.S. Line |
|--------|-----------|
| **standard** | P.S. — Your monthly maintenance covers any small edits you need. Just send me what you want changed and I'll handle it. |
| **fast-turnaround** | P.S. — I typically turn around small edits within 24 hours. Just reply to this email with what you need. |
| **growth-focused** | P.S. — This site is built to grow with you. When you're ready to add more pages, services, or features, just let me know. |
| **confident** | P.S. — Your competitors are going to wonder what hit them. |
| **results-tease** | P.S. — Don't be surprised if your phone starts ringing more. |

---

## Sign-Off Tone Options

| Option | Closing |
|--------|---------|
| **standard** | Talk soon, |
| **supportive** | Rooting for your success, |
| **excited** | Excited to see how this performs for you, |
| **casual** | Here's to more business, |
| **always-here** | Always here if you need me, |

---

## Process

1. **Receive inputs** — URL, names, style preferences, context notes
2. **Craft opening paragraph** — unique to this project based on all inputs
3. **Select PS** — based on ps_style parameter
4. **Select sign-off** — based on tone parameter
5. **Assemble email** — insert all components
6. **Save to file** — dated file in scratch/emails/
7. **Display in chat** — show final email for copy-paste

---

## File Naming

`scratch/emails/thank-you-[client-name]-YYYY-MM-DD.txt`

Example: `scratch/emails/thank-you-xpo-rehab-2026-03-30.txt`

---

## Rules

- **Craft fresh openings:** Don't default to templates — write something that fits the specific project
- **Keep the core consistent:** Middle section (feedback + referral ask) stays exactly the same
- **Subtle industry nods:** Weave in industry naturally, don't force it
- **Match the vibe:** Sign-off and PS should feel cohesive with the opening tone
- **Save every time:** Create a record even for small tweaks
- **Provide in chat:** Always display the full email ready to send

---

## Usage Examples

**Standard conversion-focused:**
```
website_url: https://johnsplumbing.com
client_name: John
industry: plumbing
ps_style: standard
tone: standard
```

**Clean redesign with personality:**
```
website_url: https://xporehab.com
client_name: Michael
context_notes: Small site, clean refresh, not conversion-heavy
ps_style: growth-focused
tone: supportive
```

**Confident close:**
```
website_url: https://sarahsphotography.com
client_name: Sarah
industry: photography
ps_style: confident
tone: excited
```

**Fast turnaround emphasized:**
```
website_url: https://markslandscaping.com
client_name: Mark
industry: landscaping
ps_style: fast-turnaround
tone: always-here
```

---

## Success Criteria

- Email file created and saved
- Opening paragraph feels fresh and specific to the project
- Feedback questions included (satisfaction, process improvement, suggestions)
- Review ask feels natural and low-pressure
- PS and sign-off match the selected styles
- All client details inserted correctly
- Core referral ask remains consistent
- Ready-to-send email displayed in chat

---

## Notes

This skill balances consistency (the referral ask works) with creativity (the opening shows you actually thought about their project). 

**The feedback section serves three purposes:**
1. Catches issues early before they become problems
2. Gives you actionable improvements for your process
3. Shows clients you actually care about their experience

The review ask is intentionally soft — "if you genuinely had a good experience" removes pressure while still asking.

Refine openings over time based on what gets the best responses.
