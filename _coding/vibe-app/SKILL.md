---
name: vibe-app
description: Build React + Vite + Tailwind apps from feature descriptions. Direct code generation for functional tools, dashboards, and internal apps.
type: procedural
keywords: ["build app", "react app", "dashboard", "vite app", "vibe code app"]
category: coding
---

# Vibe App Builder

**Purpose:** Build complete, functional React applications directly from feature descriptions.

**Input:**
1. App description / feature requirements from Spencer
2. Optional: screenshots, Figma links, or Google Stitch exported files

**Output:** Complete React + Vite project written to `Kimi Code Apps/[app-name]/`

**Stack:** React 18+, Vite, TypeScript, Tailwind CSS

---

## Pre-Flight

Before starting Step 1, **read `skills/_coding/base44-wisdom.md`**.

Apply these principles as hard constraints, not suggestions.

---

## Procedural Steps

### Step 0: Determine App Name and Project Path
- Extract app name from Spencer's description
- Create slug: lowercase, hyphenated (e.g., `call-quest`, `lead-tracker`)
- Project root: `Kimi Code Apps/[app-name]/`

### Step 1: Scope Clarification
Before writing code, confirm with Spencer:
- **Core features** — What are the 3-5 must-have features?
- **Data persistence** — localStorage only, backend API, or none?
- **Authentication** — Needed or public app?
- **Google Stitch** — Did Spencer generate a UI in Stitch? If yes, request the exported files.
- **Target device** — Desktop-first, mobile-first, or responsive?

### Step 2: Data Modeling (Hard Gate)
Define entities and state shape. Write `src/types/index.ts`.

**Rule:** This is a hard gate. No UI files are generated until types are locked.

Use this notation for planning:
- `[field]:[type]` — Required
- `[field]:[type]?` — Optional
- `[field]:enum[a,b,c]` — Enum

Example:
```typescript
export interface Lead {
  id: string;
  businessName: string;
  contactName: string;
  phone: string;
  status: 'not_called' | 'no_response' | 'meeting_booked' | 'converted';
  createdAt: string;
}
```

### Step 3: Component Architecture
Plan the component tree. Typical structure:
- `src/App.tsx` — Router or main layout
- `src/pages/` — Top-level screens
- `src/components/` — Reusable UI pieces
- `src/hooks/` — Custom hooks for logic/state
- `src/lib/` — Utilities, constants, formatters
- `src/types/` — TypeScript interfaces

**Rule:** Every component must declare its full prop interface before implementation.

### Step 4: Design System Lock
Create `src/lib/design-system.ts` with:
- Color tokens
- Typography tokens
- Spacing tokens
- Border radius / shadow tokens

**Rule:** No hardcoded hex colors in components. Everything references the DS.

### Step 5: Foundation Pass or Full Generate?

**For simple apps** (≤3 pages, no shared state, no auth):
- Generate all code in one pass.

**For complex apps** (4+ pages, shared state, auth, data relationships):
- **Foundation Pass:** Write file structure, routing, types, layout shell, hooks, and empty page shells. Stop here if Spencer wants verification.
- **UI Pass:** Fill in components, pages, and visual polish one route at a time.

### Step 6: Generate Code

Write these files into `Kimi Code Apps/[app-name]/`:

#### `index.html`
- Standard Vite HTML entry
- App title

#### `src/main.tsx`
- React root render
- StrictMode enabled

#### `src/App.tsx`
- Main app shell
- Simple client-side routing (use state-based routing or `wouter` if needed)
- Keep routing simple — no heavy router unless necessary

#### `src/types/index.ts`
- All TypeScript interfaces and enums

#### `src/lib/design-system.ts`
- Exported color tokens
- Exported spacing/typography tokens

#### `src/lib/utils.ts`
- Helper functions
- Date formatters
- Validators

#### `src/hooks/useLocalStorage.ts`
- If persistence is localStorage, write a typed hook

#### `src/hooks/use[Feature].ts`
- Custom hooks for domain logic

#### `src/components/ui/`
- `Button.tsx` — Primary, outline, destructive variants
- `Card.tsx` — Container card
- `Input.tsx` — Text input
- `Modal.tsx` — Dialog/modal shell
- `Badge.tsx` — Status badges
- `DataTable.tsx` — Sortable/filterable table if needed

#### `src/pages/`
- One file per major screen
- Name pages after their function: `Dashboard.tsx`, `LeadsPage.tsx`, `Settings.tsx`

#### `package.json`
- `react`, `react-dom`, `vite`, `tailwindcss`, `typescript`
- Build scripts: `dev`, `build`, `preview`

#### `vite.config.ts`
- Standard Vite + React plugin
- Path alias: `@/` → `/src`

#### `tailwind.config.js`
- Extend theme with DS colors
- Content paths for src

#### `tsconfig.json`
- Standard React TS config
- Path alias mapping

#### `README.md`
- How to run
- Feature list
- Data model summary
- Known gaps / TODOs

### Step 7: Stitch Integration (If Applicable)
If Spencer provides Stitch exports:
1. Read the exported HTML/CSS files
2. Extract the visual structure and class names
3. Convert static HTML into React components with state/props
4. Replace hardcoded Stitch colors with DS tokens
5. Add interactivity (onClick, onChange, state) where needed
6. Do NOT copy Stitch class names blindly — adapt to Tailwind

### Step 8: Validation Checklist
Before declaring done, verify:
- [ ] Every feature Spencer described has a corresponding component/page
- [ ] Data flow is traceable (props → state → UI → event → state update)
- [ ] No hardcoded hex colors in TSX/TS files — all use DS tokens
- [ ] TypeScript has zero `any` types for core entities
- [ ] localStorage hook is typed and handles JSON parse errors
- [ ] Responsive layout works on mobile if applicable
- [ ] No unnecessary animations — functional over pretty
- [ ] Empty/loading states handled gracefully
- [ ] Forms have basic validation
- [ ] Error boundary exists around major feature branches or routes
- [ ] No component fetches data that should be passed as props

### Step 9: Output Summary
Tell Spencer:
1. Project location (`Kimi Code Apps/[app-name]/`)
2. Tech stack and data persistence approach
3. How to run it: `npm install && npm run dev`
4. How to build: `npm run build` → static files in `dist/`
5. Any TODOs or missing pieces

---

## Universal Rules (Non-Negotiable)

### Rule 1: Functional Over Pretty
Apps exist to do work. Skip decorative animations, gradients, and flourishes unless they serve UX.

### Rule 2: Deterministic Styling
- ZERO conditional styling based on data values unless explicitly listed
- When a value is 0 or empty, apply the SAME styles as non-zero
- EVERY color must reference `src/lib/design-system.ts` explicitly

### Rule 3: TypeScript Everywhere
All props, entities, and hook returns must be typed. Avoid `any`.

### Rule 4: State Persistence Decided Upfront
Before writing state, decide: localStorage, backend API, or ephemeral?
- localStorage: good for solo tools, demos, small data
- Backend: good for multi-user, large data, sync
- Ephemeral: good for calculators, converters

### Rule 5: Simple Routing
Use state-based routing or `wouter` for simple apps. Only add `react-router-dom` for complex multi-route needs.

### Rule 6: Component Reusability
If a UI pattern appears on 2+ pages, extract it to `src/components/`.
If it's one-off, define it inline in the page.

### Rule 7: No Emojis in Apps
Use outline/straight icons only. No emoji icons.

### Rule 8: Surgical Edits Only
When Spencer requests a fix:
1. Name the exact problem
2. Identify the exact file and line range
3. Make the minimal change
4. Verify

Do not rewrite entire sections or components to fix one element.

---

## Design System Token Format

`src/lib/design-system.ts` should export:

```typescript
export const colors = {
  bg: '#0a0a0a',
  card: '#262626',
  cardLight: '#1a1a1a',
  red: '#dc2626',
  green: '#16a34a',
  yellow: '#eab308',
  blue: '#3b82f6',
  text: '#ffffff',
  muted: '#9ca3af',
} as const;

export const spacing = {
  radius: 'rounded-2xl',
  pad: 'p-6',
  gap: 'gap-4',
  section: 'py-24',
} as const;
```

---

## Example Page Pattern

```tsx
// src/pages/Dashboard.tsx
import { Card } from '@/components/ui/Card';
import { colors } from '@/lib/design-system';
import { useLeads } from '@/hooks/useLeads';

export function Dashboard() {
  const { leads, stats } = useLeads();

  return (
    <div className="p-6 grid grid-cols-2 gap-4 max-w-5xl mx-auto">
      <Card title="Leads" value={stats.total} />
      <Card title="Meetings" value={stats.meetings} />
    </div>
  );
}
```

---

## App Complexity Modes

### Simple App (1-Prompt)
- 3-5 pages
- Standard CRUD
- No complex logic
- **Output:** Single skill execution, all code generated at once

### Complex App (2-Prompt Equivalent)
- 6+ pages
- Intricate logic
- Data relationships
- **Output:** Foundation Pass first, pause for verification if Spencer wants it, then UI Pass one route at a time

---

## Feedback Integration

After building, ask: "Any tweaks to the data model or component structure?"

If Spencer gives feedback:
1. Identify the exact file(s) affected
2. Make surgical edits — minimal change, exact line range
3. Note patterns that worked for future app builds
