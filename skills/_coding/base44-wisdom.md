# Base44 Architectural Wisdom

**Purpose:** Cross-cutting principles for building clean, maintainable React apps and websites. Read this before making structural decisions.

---

## 1. Constraint Before Creativity

Lock these three things before writing any UI:
1. **Data model** — exact shape of every entity
2. **Design tokens** — colors, spacing, typography in one file
3. **Component boundaries** — what is a prop, what is internal state, what is fetched

> The reason outputs get messy is not lack of creativity. It's ambiguous constraints filled in with "reasonable" defaults that don't match the project's taste profile.

---

## 2. Data Model First Rule

Types are a **hard gate**. No component file is written until `src/types/index.ts` (or equivalent) is locked.

**Why:** Every messy build traces back to components assuming slightly different field names, optional fields treated as required, or types written early and then quietly abandoned.

**Test:** Can you describe every prop a component needs using only the types file? If not, the model isn't done.

---

## 3. Design Token Discipline

Global tokens or they're useless. One `lib/design-system.ts` (or `globals.css`) with every color, spacing step, font size, and shadow.

**Rule:** Components import from the token file. Never define a hex code, pixel value, or magic number inline.

**Test:** Can you change the primary color in one place and have it propagate everywhere? If not, the tokens aren't real.

---

## 4. Foundation-then-UI Rule

**Pass 1 — Foundation:**
- File structure
- Routing
- Data models / types
- Shared layout shell
- Design system tokens

**Pass 2 — UI:**
- Individual components
- Page content
- Visual polish

**When to split:** Any app with 4+ pages, shared state, auth, or routing. One-shot is fine for landing pages and single-screen tools.

**Why:** Writing UI before the foundation produces components that assume the wrong data shape or layout context.

---

## 5. Chunk Size Rule

The right atomic unit is **one complete route or one complete feature** at a time.

- **Too small** (one component) — you lose context of how it connects
- **Too big** (whole app) — things drift mid-build
- **Just right** — one route with its data fetching, state, and UI

---

## 6. Explicit Component Boundaries

Every component must declare, in writing or code comments:
- **Props** — what the parent must pass
- **Internal state** — what the component owns
- **Fetched data** — what the component requests itself (ideally none)

**Failure mode:** Ambiguous boundaries. "Build a card" — does it fetch its own data or receive it? Does it handle hover internally or let the parent control it? The more explicit, the cleaner the output.

**Preferred phrasing:**
> "A `ServiceCard` component that receives `{title, description, ctaText, ctaLink}` as props and handles only its own hover animation internally."

---

## 7. Surgical Over Sweeping

When something is wrong, fix the **specific thing**.

**Do not** rewrite an entire section or component to fix one element. Sweeping fixes introduce ~3 new bugs per fix.

**Protocol:**
1. Name the exact problem
2. Identify the exact file and line range
3. Make the minimal change
4. Verify

---

## 8. CSS Architecture

**Pattern that holds up:**
- Component-scoped styles for component-specific rules
- Global tokens for colors, spacing, typography
- Never duplicate tokens in component files

**Failure mode:** Global CSS that accidentally scopes itself to one component's internals. It works until you render the component twice and they fight.

---

## 9. Implicit Assumptions Warning

AI-generated components often have **hidden coupling** — they "just work" because they share a closure with something above them, or a CSS rule depends on a specific parent DOM structure.

**Fix:**
- Make all props explicit
- Never rely on context that wasn't explicitly passed
- Comment any CSS that depends on parent structure

---

## Quick Reference: What Makes Output Messy

| Root Cause | Symptom | Fix |
|------------|---------|-----|
| Data model undefined | Components use different field names | Lock types before UI |
| Design tokens missing | Inline hex codes everywhere | One token file, strict import rule |
| Foundation skipped | Components break when moved | Two-pass build |
| Chunk too big | Inconsistent patterns across files | One route at a time |
| Boundaries ambiguous | Hidden coupling, context leaks | Explicit prop declarations |
| Sweeping fixes | 3 new bugs per fix | Surgical edits only |
