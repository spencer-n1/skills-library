---
name: vibe-editor
description: Surgical editing skill for existing vibe-app and vibe-website projects. Handles simple copy changes through complex multi-file refactors. Uses ast-grep for structural search.
type: procedural
keywords: ["edit", "fix", "change", "update", "refactor", "add section", "add component", "rename"]
category: coding
auto_detect: true
agent_type: main
---

# Vibe Editor

**Purpose:** Make surgical, reliable edits to existing Next.js (vibe-website) and React + Vite (vibe-app) projects in the workspace.

**What this is NOT:** A build-from-scratch skill. It only operates on projects that already exist.

**Dependencies:** Calls on `skills/_coding/ast-grep/SKILL.md` for structural search and blast-radius mapping.

---

## Activation Triggers

Use this skill when Spencer says things like:
- "Change the hero headline on [site]"
- "Add a new section to [site]"
- "Fix the card layout on [app]"
- "Refactor the useLeads hook"
- "The nav is broken on mobile"
- "Add a new page to [site]"
- "Update the color tokens"
- Any request referencing an existing project by name

---

## Core Philosophy

**Surgical over sweeping.** Touch the minimum files and lines necessary.

**Read before touching.** The file on disk is the source of truth. Never edit from memory.

**ast-grep for location, direct edit for change.** Use ast-grep to find exact nodes. Make the actual edit directly for precision.

**Verify the chain.** After any edit, check imports, props, types, and state flow are still consistent.

---

## Edit Tiers

Route every request to the correct tier before starting work.

---

### Tier 1 — Surgical
**Scope:** Single file, no new files, no type changes.

**Examples:**
- Copy changes (headlines, labels, button text)
- Color or style changes
- Spacing or layout adjustments
- Fixing a broken element
- Changing a prop value or hardcoded constant

**Protocol:**
1. Identify the exact file from the project structure
2. If the location is obvious — read the file, find it, change it
3. If the location is unclear — use ast-grep to find the exact node first
4. Make only the change requested
5. Write the file back in full
6. Report: file changed, what was changed, done

**Rules:**
- Never rewrite a full component to change one line
- Never touch adjacent code that wasn't part of the request
- Never "clean up" or "improve" anything that wasn't asked about

---

### Tier 2 — Additive
**Scope:** New component, new section, new hook, new page — no schema/type changes.

**Examples:**
- Adding a new section to an existing page
- Building a new reusable component and wiring it in
- Adding a new custom hook
- Adding a new utility function
- Adding a new page to an existing site

**Protocol:**
1. Read the page or component where the addition will connect
2. Understand the existing data flow and props pattern
3. Write the new file matching the project's conventions — same design system tokens, same import style, same typing patterns
4. Add the import and usage to the connecting file
5. For new pages on vibe-website — add the route to the nav and sitemap if appropriate
6. Write all touched files in full
7. Report: files created, files modified, how they connect, done

**Rules:**
- New reusable component = new file in `components/` or `components/ui/`
- New hook = new file in `hooks/`
- New page = new file in `app/[route]/page.tsx` (Next.js) or `pages/` (Vite)
- Match the existing design system — never introduce new tokens without updating `lib/design-system.ts`
- Never inline a complex component directly in a page file

---

### Tier 3 — Structural
**Scope:** Type changes, data model changes, multi-file refactors.

**Examples:**
- Changing a TypeScript interface or type
- Renaming a component used in multiple places
- Changing how data flows through the app
- Refactoring a hook that multiple components depend on
- Changing the design system tokens globally
- Adding or removing a field from a core data model

**Protocol:**
1. **Map the blast radius first.** Use ast-grep to find every file that imports or uses the thing being changed. List them all.
2. Plan the edit order — start with the source of truth (type definition, hook, design system) and work outward to consumers
3. Make changes in dependency order: types first → hooks/utils → components → pages
4. After each file, verify its imports and exports still match what consumers expect
5. After all files are written, do a final ast-grep pass to check nothing was missed
6. Report: full list of files changed, what changed in each, any remaining TODOs

**Rules:**
- Never start a structural edit without mapping the blast radius first
- Never rename something in one file without updating every reference
- If a type change breaks more than 5 files, pause and confirm with Spencer before proceeding
- Design system token changes cascade everywhere — treat them as Tier 3 always

---

## ast-grep Integration

Invoke `skills/_coding/ast-grep/SKILL.md` in two scenarios:

### 1. Location Finding (Tier 1 + Tier 2)
When the file is large or the element location isn't immediately obvious:
```bash
# Find the hero headline component
ast-grep run --pattern '<h1 $PROPS>$TEXT</h1>' --lang tsx websites/[slug]/

# Find where a specific component is used
ast-grep run --pattern '<ServiceCard $PROPS />' --lang tsx websites/[slug]/
```

### 2. Blast Radius Mapping (Tier 3)
Before any structural change, find every reference:
```bash
# Find every import of a component being renamed
ast-grep run --pattern "import { $NAME } from '$PATH'" --lang typescript websites/[slug]/

# Find every usage of a type being changed
ast-grep run --pattern ': Lead' --lang typescript Kimi Code Apps/[slug]/
```

**Rule:** Use ast-grep to find. Make the actual edit directly, not via ast-grep rewrite, for anything beyond trivial replacements.

---

## Project Convention Matching

Every edit must match the conventions already established in the project. Before writing any new code, check:

- **Import style** — `@/` path aliases or relative imports?
- **Component style** — named exports or default exports?
- **Typing** — props typed inline or via interface?
- **CSS approach** — pure Tailwind, or mixed with `style={{ }}` for DS tokens?
- **Design system usage** — how are tokens referenced? (`colors.primary` vs CSS variables vs Tailwind theme)

New code must be indistinguishable from existing code in style and convention.

---

## What Never to Do

- **Never rewrite a full file to make a small change.** Read it, find the node, change only that.
- **Never introduce new dependencies** without asking Spencer first.
- **Never change design tokens** as a side effect of another edit. Token changes are their own Tier 3 edit.
- **Never skip reading the file first.** Memory is not reliable. The file is.
- **Never silently expand scope.** If fixing the requested thing reveals another problem, report it — don't fix it unasked.
- **Never leave TypeScript errors.** If an edit introduces a type mismatch, fix it before reporting done.

---

## Output Format

After every edit, report:

```
Files changed:
- [filename] — [what changed, 1 line]
- [filename] — [what changed, 1 line]

Files created:
- [filename] — [what it is]

Done. [One sentence summary.]

[Optional: flag anything Spencer should know — e.g. "noticed the mobile nav has an unrelated bug, want me to fix it?"]
```

Keep it short. Spencer reviews visually. Don't explain every line.
