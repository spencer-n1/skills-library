---
name: post-call-followup
description: Generate follow-up email for prospects who said 'send me an email' during cold call. References call context while pitching website offer.
type: procedural
keywords: ["follow up email", "cold call follow up", "prospect email", "sales email"]
auto_detect: true
agent_type: main
input_schema:
  client_name: string
  business_name: string
  call_notes: string (optional)
output_schema:
  file_path: scratch/emails/followup-[client-name]-YYYY-MM-DD.txt
quality_metrics:
  success_rate: 0.75
  avg_tokens: 2000
evolution:
  parent: null
  version: "1.0"
  lineage: []
status: active
---

# post-call-followup — SKILL.md

**Version:** 1.0  
**Last Updated:** 2026-03-30  
**Type:** Procedural

---

## Purpose

Generate follow-up email for prospects who said "send me an email" during a cold call. References the call context while pitching the website offer.

---

## Input

| Field | Required | If Missing |
|-------|----------|------------|
| `client_name` | Yes | Ask |
| `business_name` | Yes | Ask |
| `call_notes` | No | Skip personalized reference |
| `industry` | No | Skip case study |
| `calendly_link` | No | Use "[Calendly link]" |
| `your_name` | Yes | Ask |
| `your_email` | Yes | Ask |

---

## Output

### 1. Email File

Saved to: `scratch/emails/followup-[client-name]-YYYY-MM-DD.txt`

### 2. Chat Confirmation

Displays the generated email for immediate use.

---

## Email Template

**SUBJECT:** As promised — [Business Name] website

**BODY:**

Hey [First Name],

[CALL REFERENCE — varies based on call_notes]

I built [Business Name] a custom website concept. Clean, professional design that's optimized for mobile and built to convert visitors into leads.

I handle the domain registration, hosting setup, professional copywriting, and all the technical details. You review it, and if it fits your business, we make it live. If not, no obligation whatsoever.

[OPTIONAL CASE STUDY — based on industry]

I'd like to show you what I built — it's currently hosted on my computer, so I have a couple screenshots of how it looks. The review takes about 10 minutes, and you can see exactly how it would represent your business online.

Schedule a time here: [Calendly link]

[Your Name]  
[Your Email]

---

## Call Reference Variations

### With call_notes (specific callback)
We spoke earlier about [specific detail from call]. I built [Business Name] a custom website concept to address that.

### Without call_notes (general follow-up)
As promised — here's more information about the website I mentioned for [Business Name].

---

## Optional Case Studies by Industry

Use if `industry` provided and matches:

**Home Services:**  
Last [trade] client I did this for saw a 40% increase in qualified leads within 60 days.

**Healthcare:**  
Last healthcare client used this approach to reduce patient acquisition cost by 30%.

**Professional Services:**  
Last [profession] client filled their consultation calendar within 3 weeks of launching.

**Trades:**  
Last [trade] business saw 15+ qualified quote requests in the first month.

**Creative Services:**  
Last [creative] client used this to book 8 new projects in their first 60 days.

**Generic (no match):**  
Skip case study line entirely.

---

## Process

1. **Receive inputs** — client details, call notes, industry
2. **Draft call reference** — specific if notes provided, general if not
3. **Select case study** — match to industry or skip
4. **Assemble email** — insert all components
5. **Flag missing elements** — remind to add Calendly link if placeholder used
6. **Save to file** — dated file in scratch/emails/
7. **Display in chat** — show final email for copy-paste

---

## File Naming

`scratch/emails/followup-[client-name]-YYYY-MM-DD.txt`

Example: `scratch/emails/followup-mike-xpo-2026-03-30.txt`

---

## Rules

- **Subject line stays consistent:** "As promised — [Business Name] website"
- **Reference the call:** Always acknowledge you spoke, use specifics when possible
- **Keep it brief:** Same ~125 word count as cold email version
- **Calendly reminder:** If placeholder used, remind user to update before sending
- **Flexible case studies:** Use when relevant, skip when not
- **Save every time:** Create record of what was sent

---

## Usage Examples

**With detailed call notes:**
```
client_name: Mike
business_name: XPO Rehab
call_notes: They rely on referrals, want consistent lead flow, mentioned 73% mobile traffic
industry: healthcare
calendly_link: https://calendly.com/spencer/review
```

**Minimal info:**
```
client_name: Sarah
business_name: Sarah's Photography
call_notes: (none provided)
industry: creative services
```

---

## Success Criteria

- Email file created and saved
- Call reference feels personal and specific
- Subject line follows format exactly
- Case study used only when industry match
- Placeholder flagged if Calendly link not provided
- Ready-to-send email displayed in chat

---

## Notes

This email bridges the gap between "I'll send you info" and actually booking the review. The "As promised" subject creates obligation (they asked for this) while the content delivers value (website is ready).

Refine case studies over time based on your actual results. Real data > generic claims.
