---
name: vibe-admin-panel
description: Add a password-protected admin panel to any vibe-website or vibe-app project so clients can manage dynamic content without touching code.
type: procedural
keywords: ["admin panel", "cms", "client editing", "admin", "dashboard", "content management"]
category: coding
auto_detect: true
agent_type: main
---

# Vibe Admin Panel

**Purpose:** Add a password-protected admin panel to any vibe-website or vibe-app project so clients can manage dynamic content (reviews, blog posts, products, team members, etc.) without touching code.

**Output:** New `/admin` route + supporting pages + data layer wired to existing site content.

---

## Core Concept

No external CMS. No Decap. No Git-based setup.

The admin panel is a password-gated React route built directly into the existing project. Content is stored in a simple JSON file or lightweight backend (Supabase depending on project stack). The client gets a URL and a password. That's it.

---

## Activation Triggers

Use this skill when Spencer says:
- "Add an admin page to [site]"
- "The client wants to manage their own reviews"
- "Add a blog the client can update"
- "Make this an ecommerce site with product management"
- "Add an admin panel"

---

## Critical Compatibility Note

**For vibe-website (Next.js):** The current vibe-website skill uses `output: 'export'` (static HTML files only). API routes **do not work** in static export mode.

If Spencer wants a fully functional admin panel with real-time edits on a vibe-website, you have two options:
1. **Remove `output: 'export'`** from `next.config.js` and deploy to a serverful host (Vercel server mode, Node.js host, Cloudways with Node support) so API routes can run.
2. **Use a lightweight backend** like Supabase for all data reads/writes instead of local JSON + API routes.

For vibe-app (React + Vite), there is no static export limitation — Supabase or a small backend works out of the box.

**Always warn Spencer about this trade-off before building the admin panel on a Next.js site.**

---

## Input

1. Existing vibe-website or vibe-app project path
2. Content types to manage (reviews, blog posts, products, team members, etc.)
3. Admin password (default: `admin2026` — Spencer should change per client)

---

## Architecture

### Password Gate
- `/admin` route renders a simple password form
- Password stored as an env variable or hardcoded constant
- On success: sets `sessionStorage.setItem('admin_auth', 'true')` and redirects to `/admin/dashboard`
- Every admin sub-route checks sessionStorage on mount — redirects to `/admin` if not authenticated
- No user accounts, no JWT, no OAuth — just a simple gate

### Admin Dashboard
- Clean sidebar layout: logo, nav links for each content type, logout button
- Dark theme (`#0f0f0f` / `#1a1a1a`) — visually distinct from the client-facing site
- Each content type gets its own admin sub-route

### Data Layer

**For vibe-website (Next.js):**
- Store content in `/data/[content-type].json` files
- Admin reads/writes via Next.js API routes (`/api/admin/reviews`, etc.)
- API routes check a server-side password before allowing writes
- Client-facing pages read from the same JSON files at build time (SSG) or runtime (SSR)

**For vibe-app (React + Vite):**
- Use Supabase if already in the stack, otherwise localStorage for prototypes
- For production: wire to Supabase tables

---

## Content Type Templates

### Reviews
Fields: `id`, `author`, `rating` (1-5), `text`, `date`, `visible` (boolean)
Admin UI: Table view, add/edit modal, toggle visibility, delete

### Blog Posts
Fields: `id`, `title`, `slug`, `excerpt`, `body` (markdown), `date`, `published` (boolean), `coverImage`
Admin UI: Post list, full editor with markdown textarea, publish toggle, delete

### Products
Fields: `id`, `name`, `description`, `price`, `image`, `category`, `inStock` (boolean)
Admin UI: Product grid, add/edit modal, stock toggle, delete

### Team Members
Fields: `id`, `name`, `role`, `bio`, `photo`, `order`
Admin UI: Card list, add/edit modal, drag-to-reorder (or manual order field)

### General (Custom)
Ask Spencer what fields are needed before building.

---

## Procedural Steps

### Step 1: Read the Existing Project
- Identify project type (vibe-website vs vibe-app)
- Identify which content is currently hardcoded that should be dynamic
- Note the existing design system tokens

### Step 2: Define Content Types
- Confirm with Spencer which content types to manage
- Map each type to its fields (use templates above)
- Confirm admin password
- **For vibe-website:** Confirm whether Spencer accepts removing `output: 'export'` or using Supabase

### Step 3: Build the Data Layer
- Create `/data/[type].json` with existing hardcoded content seeded in
- Create API routes (Next.js) or Supabase tables (Vite) for CRUD
- Ensure all IDs are generated with `crypto.randomUUID()` or similar

### Step 4: Build the Admin Routes

Create these files:
- `app/admin/page.tsx` — Password gate
- `app/admin/dashboard/page.tsx` — Dashboard home (summary cards)
- `app/admin/[type]/page.tsx` — List + manage each content type
- `app/admin/[type]/new/page.tsx` — Add new record
- `app/admin/[type]/[id]/page.tsx` — Edit existing record

*(For Vite apps, adapt routing to the project's existing router.)*

### Step 5: Wire Client-Facing Pages
- Replace hardcoded content arrays with reads from the data layer
- Reviews on homepage → reads from `/data/reviews.json` or Supabase
- Blog index → reads from `/data/posts.json` or Supabase
- Products grid → reads from `/data/products.json` or Supabase

### Step 6: Add Admin Link to Footer
- Add a subtle, low-contrast link in the footer: `Admin` → `/admin`
- Style: small, muted, not prominent — just findable

### Step 7: Verify
- Test password gate (wrong password stays on `/admin`, correct redirects)
- Test adding a record → appears on client-facing page
- Test editing a record → updates correctly
- Test deleting a record → removed from client-facing page
- Confirm all admin sub-routes redirect to gate if not authenticated

---

## Admin UI Design Rules

- **Dark theme** — visually distinct from client site so there's no confusion
- **Sidebar navigation**, not tabs
- **Table/list views** for content with more than a few fields
- **Modal for add/edit** (not a separate page) unless form is very long
- **Confirmation dialog** before any delete
- **Success/error toast notifications** on save
- **Mobile is NOT a priority** for admin — optimize for desktop

---

## Security Notes

This is lightweight security — appropriate for small local business clients, not enterprise.
- Password in env variable (`ADMIN_PASSWORD`) or hardcoded constant
- API routes validate password on every write request
- sessionStorage clears on tab close
- For higher security needs: suggest proper auth (Clerk, NextAuth) as an upgrade

---

## Footer Link Format

```tsx
// In Footer component — subtle, low-contrast
<a
  href="/admin"
  style={{ color: 'rgba(255,255,255,0.2)', fontSize: '12px', textDecoration: 'none' }}
>
  Admin
</a>
```

---

## Dependencies

No new npm packages required for basic implementation.

Optional:
- `react-hot-toast` for notifications
- `@uiw/react-md-editor` for blog markdown editing

**Ask Spencer before adding any new dependency.**

---

## What Not to Do

- Do NOT use Decap CMS, Netlify CMS, or any Git-based CMS
- Do NOT require the client to use a third-party dashboard
- Do NOT build a full auth system — simple password gate is intentional
- Do NOT make the admin link prominent on the client-facing site
- Do NOT skip seeding existing hardcoded content into the data layer — client should see their content immediately on first login
