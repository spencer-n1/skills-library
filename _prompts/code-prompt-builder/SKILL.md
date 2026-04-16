# App Builder — SKILL.md

**name:** app-builder  
**description:** Build ultra-compact "code-like" prompts for complex applications. Uses shorthand notation, design system references, and structured specifications instead of prose. Supports both new builds and conversion from existing prompts.  
**type:** procedural  
**version:** 1.0 — April 5, 2026

---

## Purpose

Write prompts in a compressed, code-like format that:
- Eliminates repetitive prose
- Establishes design system once, references everywhere
- Structures features declaratively (like code)
- Maintains editability (line-based, surgical edits work)
- Prioritizes Base44 consumption over human readability

**Use when:**
- Building complex apps (CRM, dashboards, multi-page tools)
- Converting existing prose prompts to compact format
- Features are stable and well-defined
- Speed/compression matters more than narrative flow

**Don't use when:**
- Client website prompts (still use prompt-builder prose style)
- Heavy storytelling/brand narrative needed
- Design direction is exploratory/vague

---

## 2-Prompt Architecture

**Split at the data boundary:**

**Prompt 1 — Foundation (Data Layer):**
- DS (Design System)
- ENTITIES (Data Models)
- NAV (Navigation)
- COMPONENTS (Reusable UI)
- LOGIC (Complex Rules)
- SAMPLE (Optional — only if needed for testing)

**Prompt 2 — Shell (Presentation Layer):**
- PAGES (UI Screens)
- FIGMA (Reference to screenshot/Figma for layout)

---

## Mode Selection: 1-Prompt vs 2-Prompt

**Choose based on app complexity:**

| Mode | Use When | Structure |
|------|----------|-----------|
| **1-Prompt** | Simple apps (3-5 pages, standard CRUD, no complex logic) | All sections in single prompt |
| **2-Prompt** | Complex apps (6+ pages, intricate logic, data relationships) | Foundation → Shell split |

**1-Prompt Benefits:**
- Faster iteration
- Less context switching
- Base44 sees full picture at once

**2-Prompt Benefits:**
- Locks data model before UI
- Reduces drift on complex builds
- Easier to fix foundation issues without rebuilding pages

**FIGMA Section Purpose:**
Direct Base44 to use your screenshot/Figma as the layout source of truth. Do NOT manually specify pixel measurements — the screenshot IS the spec.

**Format:**
- Simple reference: "Use attached screenshot for all page layouts"
- Per-page: "Dashboard layout from screenshot"
- Back-to-back runs: Context already exists, minimal reference needed

**What NOT to put:**
- Manual pixel measurements (redundant with screenshot)
- Detailed layout descriptions (screenshot already shows it)

**Execution Flow:**
1. Run Prompt 1 → Get Foundation built (DS, Entities, Nav, Components, Logic, Sample)
2. Verify data model is correct
3. Reference Figma/screenshot for page layouts
4. Run Prompt 2 → Build Pages on top of locked foundation

**Why split:**
- Locks data model before building views on top of it
- Cuts drift surface in half
- Figma references only needed when building pages
- Can run Prompt 1 and 2 back-to-back

---

## Output Format

**File:** `prompts/engineering/[app-name].md`  
**Extension:** All files use this format, no separate folder needed

---

## Format Specification (The Language)

### Section Order (Fixed)

**1-Prompt Mode (All Sections):**
```
# APP: [Name]

## DS (Design System)
## ENTITIES (Data Models)
## NAV (Navigation)
## COMPONENTS (Reusable UI)
## PAGES (UI Screens)
## LOGIC (Complex Rules)
## SAMPLE (Optional)
```

**2-Prompt Mode:**
- **Prompt 1:** DS → ENTITIES → NAV → COMPONENTS → LOGIC → SAMPLE (optional)
- **Prompt 2:** FIGMA → PAGES

**CRITICAL:** Sections must appear in this order. SAMPLE is optional — only include if demo data is needed for testing.

---

### 1. DS — Design System

Define visual system once. Everything else references it.

```markdown
## DS

COLORS:
BG:[hex] | CARD:[hex] | RED:[hex] | GRN:[hex] | YEL:[hex] | BLU:[hex] | TXT:[hex] | MUTE:[hex]

TYPOGRAPHY:
FONT:[name] | HEAD:[size/weight] | BODY:[size/weight] | SMALL:[size]

SPACING:
RADIUS:[px] | PAD:[px] | GAP:[px] | SECTION:[px]

MOTION:
HOVER:[effect] | SHADOW:[effect] | TRANSITION:[ms] | SCROLL:[ms] | FADE:[ms] | STAGGER:[ms]

**Determinism Rules:**
- ZERO conditional styling based on data values unless explicitly listed
- When a value is 0 or empty, apply the SAME styles as non-zero — no special fallback colors
- EVERY color must reference DS token explicitly (never hardcode hex in PAGES)
```

**Shorthand Notation:**
- `BG:#0a0a0a` — Background color
- `HOVER:RED-BORDER + SHADOW-GLOW(...)` — Hover effect (part of MOTION)
- `FADE:200ms` — Animation timing (part of MOTION)
- `RADIUS:16px` — Border radius everywhere (unless overridden)

**Reference Pattern:**  
In PAGES section: `CARD[hover:DS.HOVER]` — uses design system hover

---

### 2. COMPONENTS — Reusable UI

Define common UI patterns that appear on multiple pages. Not design system (visual), but component behavior/structure.

```markdown
## COMPONENTS

DeleteModal:[
  title:"Confirm Delete",
  message:"Are you sure? This cannot be undone.",
  buttons:[
    Cancel[text:"Cancel", style:outline],
    Confirm[text:"Delete", style:destructive, icon:trash]
  ]
]

NumberInput:[
  type:text,
  inputMode:numeric,
  pattern:"[0-9]*",
  onFocus:setSelectionRange[0,value.length]
]

StatusBadge:[
  type:dropdown,
  options:enum[not_called,no_response,meeting_booked,converted],
  colors:[gray,blue,yellow,green]
]

StarToggle:[
  icon:Star,
  maxSelect:3,
  animation:pop
]

DataTable:[
  features:[sort,filter,checkbox,rowClick],
  checkboxStyle:black-bg + red-outline,
  hover:row-highlight,
  actions:icon-only
]
```

**Notation Rules:**
- `ComponentName:[props]` — Component definition
- Reference in PAGES: `@DeleteModal` or `Modal[type:DeleteModal]`
- Define once, reuse everywhere
- Complex props use `[]` grouping

**When to Define:**
- UI pattern appears on 2+ pages
- Specific interaction behavior needed
- Consistency critical across app

**When NOT to Define:**
- One-off component (define inline in PAGES)
- Simple variation of DS element

**Using Components in PAGES:**
- Reference: `@DeleteModal` or `Modal[type:DeleteModal]` — uses component as-is
- Override: Define inline in PAGES when page needs specific behavior (e.g., table with unique columns)
- Extend: `MODAL[EditLead]:extends[AddLead] + Delete` — inherits + adds

---

### 3. ENTITIES — Data Models

Define data structures. JSON-like notation.

```markdown
## ENTITIES

Lead:{
  id:uuid,
  businessName:string,
  contactName:string,
  phone:string,
  industry:string?,
  website:url?,
  status:enum[not_called,no_response,not_interested,meeting_booked,converted],
  createdAt:datetime,
  isDuplicate:boolean,
  duplicateGroupId:string?
}

Client:{
  id:uuid,
  leadId:uuid,
  businessName:string,
  contactName:string,
  phone:string,
  saleDate:date,
  oneTimeAmount:number,
  recurringAmount:number,
  isYearly:boolean
}

Meeting:{
  id:uuid,
  leadId:uuid,
  date:date,
  time:time,
  meetingUrl:url?,
  siteUrl:url?,
  notes:text?
}
```

**Notation Rules:**
- `[field]:[type]` — Required field
- `[field]:[type]?` — Optional (nullable)
- `[field]:enum[a,b,c]` — Enum with values
- Nested objects use `{}`
- Arrays use `[]`

---

### 3. NAV — Navigation Structure

Simple list or hierarchical.

```markdown
## NAV

PRIMARY:
Dashboard | Leads | StartCalling | Meetings | ClientsWon | Stats

SECONDARY:
Libraries[SalesScripts, ObjectionHandles, ClosingNotes]

LOGO-CLICK:Intro
```

**Notation:**
- `|` separates items at same level
- `[]` for expandable/collapsible groups
- `:` for actions (LOGO-CLICK:Intro means clicking logo goes to Intro)

---

### 4. PAGES — UI Screens

Each page is a section with components.

```markdown
## PAGES

### Dashboard

LAYOUT:Grid[2x2] | MAX-WIDTH:1200px

CARDS[4]:
- DailyCalls[goal:N, current:N, streak:N, onclick:StartCalling]
- DailyDMs[goal:N, current:N, progress:bar]
- LeadsNotCalled[count:N, onclick:Leads]
- MeetingsBooked[count:N, onclick:Meetings]

### Leads

LAYOUT:Table | FILTERS:top | ACTIONS:row-click

TABLE:
  COLS:Checkbox | Lead | Phone | Status | Created | Actions
  FILTERS:Search | Duplicates | Status[dropdown] | Sort[dropdown]
  ACTIONS:Delete[icon:trash], RowClick:EditModal
  ROW-HOVER:none
  CHECKBOX:style[DS.CHECKBOX]

MODAL[AddLead]:
  FIELDS:BusinessName | ContactName | Phone | Industry | Website | Status
  BUTTONS:Save | Cancel

MODAL[EditLead]:extends[AddLead] + Delete

### StartCalling

LAYOUT:Centered | MAX-WIDTH:600px

HEADER:"Live Calls" + RED-PULSE-DOT[animation:pulse,2s]
SUBHEADER:"Each session goes through your filtered uncalled leads..."

COUNT-DISPLAY:
  ICON:Phone[white,large]
  NUMBER:[filtered-count]
  LABEL:"leads ready to call"
  LAYOUT:horizontal

BUTTONS:
  StartCalling[
    color:GRN,
    warningIf:duplicates[icon:YEL-triangle,modal:DupWarning],
    width:constant
  ]
  Filter[dropdown:All|HasWebsite|NoWebsite,width:match]

GAP:24px

CARD:MindsetReminder[
  style:red-shadow-glow,
  icon:Brain,
  rotate:8s[fade:500ms],
  quotes:array,
  editButton:bottom-right
]

### Meetings

LAYOUT:Table

HEADER-STATS:
  LEFT:"Meetings"
  RIGHT:Today[count] | ThisWeek[count] | AddMeeting[button]

TABLE:
  COLS:Time | Lead | MeetingLink | SiteLink | Actions
  TIME-FORMAT:
    LINE1:"10:40A on"[time:white + on:mute]
    LINE2:"04/05"[date:mute]
  LEAD:BusinessName[bold] + ContactName[small,mute]
  ACTIONS:Complete[icon:checkmark-circle,onclick:remove]
  ROW-CLICK:EditModal

MODAL[EditMeeting]:
  INFO[read-only]:BusinessName | ContactName | Phone | Email
  FIELDS:Date | Time | MeetingUrl | SiteUrl | Notes
```

**Component Notation:**
- `NAME[props]` — Component with properties
- `prop:value` — Property assignment
- `|` separates columns/filters
- `+` combines elements
- `extends[OtherComponent]` — inherits + adds
- `onclick:Destination` — navigation action
- `icon:name` — icon reference
- `style:reference` — uses DS or custom

**Layout Shorthand:**
- `Grid[2x2]` — 2x2 grid
- `Table` — data table
- `Centered` — single column centered
- `Horizontal` — row layout
- `MAX-WIDTH:1200px` — container constraint

---

### 5. LOGIC — Complex Rules

For critical logic that needs heavy emphasis.

```markdown
## LOGIC

### Revenue[CRITICAL]

DEFINITION:
- Total:OneTime + AllRecurringReceived
- Monthly:Sum(active monthly)
- Annual:Sum(active yearly)

RULES:
  ADD:
    Monthly → Total+=OneTime+FirstMonth
    Yearly → Total+=OneTime+YearlyAmount
  AUTO-INCREMENT:
    Monthly → Anniversary+=MonthlyAmount
    Yearly → Anniversary+=YearlyAmount
  DELETE:
    Total:STAYS-SAME[already earned]
    Recurring:-=ClientAmount

EXAMPLE[Monthly $800+$50]:
  T0:Total=$850
  T1:Total=$900[auto]
  T12:Total=$1450[auto]

VERIFICATION:
- [ ] New client shows correct Total immediately
- [ ] Month anniversary auto-increments
- [ ] Delete preserves Total, decreases Recurring

### DuplicateDetection

RULES:
  MATCH[BusinessName~90% OR Phone~100%] → isDuplicate=true
  GROUP:assign[dup-###]
  VISUAL:alt-row-colors[per-group]
  FILTER:show-only-dups
  CLEANUP:on-delete[reevaluate-groups, auto-clear-filter-if-empty]

### StatusWorkflow

STATUSES:
  not_called → no_response_callback → meeting_booked → converted
  not_called → not_interested

BADGES:
  not_called:gray | no_response:blue | not_interested:red | meeting_booked:yellow | converted:green
```

**Critical Section Format:**
- `### Name[CRITICAL]` — marks high-priority logic
- `DEFINITION:` — what concepts mean
- `RULES:` — behavior specifications
- `EXAMPLE:` — concrete timeline/data
- `VERIFICATION:` — testable checkboxes

---

### 6. SAMPLE — Demo Data (Optional)

Include only if demo data is needed for testing. For most apps, omit this section.

```markdown
## SAMPLE

Leads[9]:
  Group1[ABC Electric]:3[John Smith, John, J. Smith]
  Group2[Quick Plumbing]:3[Mike Johnson, Mike, Michael]
  Group3[Sunset Landscaping]:3[Sarah Chen, Sarah, S. Chen]
  Status:mix[not_called,no_response]
  Purpose:demo-duplicates

Meetings[0]:none
Clients[0]:none
```

---

## Prompt Templates

Choose mode based on app complexity.

### 1-Prompt Mode (Simple Apps)

Use for: 3-5 pages, standard CRUD, no complex logic

```markdown
# APP: [Name]

DETERMINISM: STRICT

## DS

COLORS:
BG:[hex]|CARD:[hex]|RED:[hex]|GRN:[hex]|YEL:[hex]|BLU:[hex]|TXT:[hex]|MUTE:[hex]

TYPOGRAPHY:
FONT:[name]|HEAD:[size/weight]|BODY:[size/weight]|SMALL:[size]

SPACING:
RADIUS:[px]|PAD:[px]|GAP:[px]|SECTION:[px]

MOTION:
HOVER:[effect]|SHADOW:[effect]|TRANSITION:[ms]|FADE:[ms]|STAGGER:[ms]

ICON-RULES:
- NO emojis
- Straight/outline icons only
- NO colored backgrounds on icons
- NO outlines around icons

DETERMINISM-RULES:
- EVERY color must reference DS token explicitly
- ZERO conditional styling based on data values unless explicitly listed
- When value is 0 or empty, apply SAME styles as non-zero

## ENTITIES

[Define data models]

## NAV

[Define navigation]

## COMPONENTS

[Define reusable UI]

## PAGES

### [PageName]
[Layout + components]

### [PageName]
...

## LOGIC

[Define complex rules]
```

### 2-Prompt Mode (Complex Apps)

Use for: 6+ pages, intricate logic, data relationships

**Prompt 1 — Foundation:**
```markdown
# APP: [Name] — FOUNDATION (Prompt 1)

DETERMINISM: STRICT

## DS
[Design system]

## ENTITIES
[Data models]

## NAV
[Navigation]

## COMPONENTS
[Reusable UI]

## LOGIC
[Complex rules]
```

**Prompt 2 — Shell:**
```markdown
# APP: [Name] — SHELL (Prompt 2)

FIGMA:
- Use attached screenshot for all page layouts
- Match spacing, sizing, and component placement exactly
- Reference DS tokens for colors, never sample from image

## PAGES

### [PageName]
[Component structure — layout comes from screenshot]

### [PageName]
...
```

**Note:** The FIGMA section is a reference pointer, not a spec sheet. The screenshot IS the layout specification — don't manually write pixel measurements.
...
```

**Note:** The FIGMA section is a reference pointer, not a spec sheet. The screenshot IS the layout specification — don't manually write pixel measurements.

---

## Mode: Convert Only

**Trigger:** the user provides app information (description, features, requirements)

**Process:**
1. Determine mode: Simple (1-Prompt) or Complex (2-Prompt)
2. Gather app information from the user's description
3. Define DS, ENTITIES, NAV, COMPONENTS, LOGIC (SAMPLE optional)
4. If 2-Prompt: Split into Foundation + Shell
5. If 1-Prompt: Include PAGES inline
6. Output compact code-style markdown prompt(s)
7. Hand off to prompt-engineering skill for edits/refinement

**File Naming:**
- 1-Prompt: `prompts/engineering/[app-name].md`
- 2-Prompt: `prompts/engineering/[app-name]/prompt1.md` + `prompt2.md`
- the user may specify custom path

**What I Output:**
- Code-style markdown in the format specified above
- Complete first draft with all sections
- Ready for prompt-engineering skill to refine

**What Happens Next:**
- Prompt-engineering skill takes over for edits
- Follows Clarify → Confirm → Edit workflow
- the user directs specific changes

---

## Rules

1. **Choose mode first:** Simple app → 1-Prompt | Complex app → 2-Prompt
2. **Section order is fixed per mode:**
   - 1-Prompt: DS → ENTITIES → NAV → COMPONENTS → PAGES → LOGIC
   - 2-Prompt Prompt 1: DS → ENTITIES → NAV → COMPONENTS → LOGIC
   - 2-Prompt Prompt 2: FIGMA → PAGES
3. **SAMPLE is optional** — only include if demo data is needed for testing
4. **DS defines once, reference everywhere** — never repeat design specs
5. **DS Determinism enforced** — zero conditional styling, same styles for 0/empty, explicit tokens only
6. **COMPONENTS for reusable UI** — define patterns used 2+ times; inline in PAGES for one-offs
7. **Use shorthand** — compress to minimal characters while remaining readable
8. **CRITICAL tags for complex logic** — ensures emphasis
9. **Examples prove the rules** — always include concrete data
10. **Verification checkboxes** — testable criteria for Base44
11. **Line-based** — each component/rule on its own line for surgical editing
12. **Convert mode only** — I write the first draft, prompt-engineering handles edits

---

## Why This Format Works

**For You:**
- Ultra compact (Call Quest in ~150 lines vs 1000+)
- No repetition
- Fast to write once learned
- Easy to scan

**For Base44:**
- Structured like code
- Clear component hierarchy
- No ambiguous prose
- Reference patterns it already knows
- COMPONENTS section eliminates redundant descriptions

**For Editing:**
- Line-based = surgical edits work
- Exact string matching possible
- Prompt-engineering skill compatible

---

*Version 3.0 — April 7, 2026 (Added 1-Prompt/2-Prompt mode selection, SAMPLE now optional, added template variants)*
nal, added template variants)*
# Why This Format Works

**For You:**
- Ultra compact (Call Quest in ~150 lines vs 1000+)
- No repetition
- Fast to write once learned
- Easy to scan

**For Base44:**
- Structured like code
- Clear component hierarchy
- No ambiguous prose
- Reference patterns it already knows
- COMPONENTS section eliminates redundant descriptions

**For Editing:**
- Line-based = surgical edits work
- Exact string matching possible
- Prompt-engineering skill compatible

---

*Version 3.0 — April 7, 2026 (Added 1-Prompt/2-Prompt mode selection, SAMPLE now optional, added template variants)*
