# Kibo UI `llms.txt` Generation Plan

## Goal

Generate a comprehensive `llms.txt` for the Kibo UI component library.
The file documents every UI component with installation, anatomy, and usage
variations, preceded by general installation and theming sections.

**Output:** `apps/docs/public/llms.txt`
**Intermediate files:** `support/sections/` (assembled in Milestone 7)

---

## Project Context

Kibo UI is a shadcn/ui registry of 41 composable, accessible React components.
Components live in `packages/<name>/` as single-file packages (`index.tsx` or
`styles.css`). Existing MDX documentation lives in
`apps/docs/content/components/<name>.mdx`. Usage examples live in
`apps/docs/examples/<name>*.tsx`.

### Component Inventory (41 components)

| # | Component | Source | Type |
|---|-----------|--------|------|
| 1 | announcement | `packages/announcement/index.tsx` | Composable |
| 2 | avatar-stack | `packages/avatar-stack/index.tsx` | Composable |
| 3 | banner | `packages/banner/index.tsx` | Composable |
| 4 | calendar | `packages/calendar/index.tsx` | Composable |
| 5 | choicebox | `packages/choicebox/index.tsx` | Composable |
| 6 | code-block | `packages/code-block/index.tsx` | Composable |
| 7 | color-picker | `packages/color-picker/index.tsx` | Context-based |
| 8 | combobox | `packages/combobox/index.tsx` | Composable |
| 9 | comparison | `packages/comparison/index.tsx` | Composable |
| 10 | contribution-graph | `packages/contribution-graph/index.tsx` | Composable |
| 11 | credit-card | `packages/credit-card/index.tsx` | Composable |
| 12 | cursor | `packages/cursor/index.tsx` | Simple |
| 13 | deck | `packages/deck/index.tsx` | Composable |
| 14 | dialog-stack | `packages/dialog-stack/index.tsx` | Context-based |
| 15 | dropzone | `packages/dropzone/index.tsx` | Composable |
| 16 | editor | `packages/editor/index.tsx` | Composable |
| 17 | gantt | `packages/gantt/index.tsx` | Context-based |
| 18 | glimpse | `packages/glimpse/index.tsx` | Composable |
| 19 | image-crop | `packages/image-crop/index.tsx` | Composable |
| 20 | image-zoom | `packages/image-zoom/index.tsx` | Simple |
| 21 | kanban | `packages/kanban/index.tsx` | Context-based |
| 22 | list | `packages/list/index.tsx` | Composable |
| 23 | marquee | `packages/marquee/index.tsx` | Composable |
| 24 | mini-calendar | `packages/mini-calendar/index.tsx` | Composable |
| 25 | pill | `packages/pill/index.tsx` | Composable |
| 26 | qr-code | `packages/qr-code/index.tsx` | Composable |
| 27 | rating | `packages/rating/index.tsx` | Composable |
| 28 | reel | `packages/reel/index.tsx` | Composable |
| 29 | relative-time | `packages/relative-time/index.tsx` | Simple |
| 30 | sandbox | `packages/sandbox/index.tsx` | Composable |
| 31 | snippet | `packages/snippet/index.tsx` | Composable |
| 32 | spinner | `packages/spinner/index.tsx` | Variant-based |
| 33 | status | `packages/status/index.tsx` | Composable |
| 34 | stories | `packages/stories/index.tsx` | Composable |
| 35 | table | `packages/table/index.tsx` | Composable |
| 36 | tags | `packages/tags/index.tsx` | Composable |
| 37 | theme-switcher | `packages/theme-switcher/index.tsx` | Composable |
| 38 | ticker | `packages/ticker/index.tsx` | Composable |
| 39 | tree | `packages/tree/index.tsx` | Composable |
| 40 | typography | `packages/typography/styles.css` | CSS-only |
| 41 | video-player | `packages/video-player/index.tsx` | Composable |

---

## Milestone 1: Foundation & Guidelines (Sequential)

**Goal:** Establish the documentation standard and build a complete API inventory
before writing any content.

### References for subagents

- Writing guide: `support/writing-guide.md`
- Component sources: `packages/<name>/index.tsx` (or `styles.css` for typography)
- Package metadata: `packages/<name>/package.json`
- Existing docs: `apps/docs/content/components/<name>.mdx`
- Existing examples: `apps/docs/examples/<name>*.tsx`
- General docs: `apps/docs/content/docs/setup.mdx`, `usage.mdx`, `philosophy.mdx`

### Tasks

- [ ] **1.1: Create component inventory** (`support/component-inventory.md`)
  - Read every `packages/*/index.tsx` (and `packages/typography/styles.css`)
  - Read every `packages/*/package.json`
  - For each component, catalog:
    - Package name and description (from `package.json`)
    - All exported components (name, props interface, description)
    - All exported types/interfaces
    - All exported hooks
    - External dependencies
    - shadcn/ui registry dependencies (which `@/components/ui/*` it imports)
    - Kibo inter-dependencies (which `@repo/*` packages it depends on)
  - Output: structured markdown with one section per component
  - **This task is large.** The subagent should process all 41 components
    systematically. The output can be long — completeness matters more than
    brevity here.

- [ ] **1.2: Review and refine writing guide** (`support/writing-guide.md`)
  - Read `support/writing-guide.md` (the draft created during planning)
  - Read `support/component-inventory.md` (output of 1.1)
  - Read 3-4 diverse existing component docs from `apps/docs/content/components/`
  - Read 3-4 diverse examples from `apps/docs/examples/`
  - Ensure the writing guide template handles all patterns found:
    - Composable multi-component (most components)
    - Context-based with hooks (color-picker, kanban, gantt, dialog-stack)
    - Variant-based (spinner)
    - CSS-only (typography)
    - Simple single-export (cursor, image-zoom, relative-time)
  - Add concrete before/after examples if helpful
  - Refine section ordering, formatting rules, and quality criteria
  - Commit: `docs: refine llms.txt writing guide based on component inventory`

---

## Milestone 2: General Documentation Sections (Sequential)

**Goal:** Write the non-component sections that precede the component reference.

### Tasks

- [ ] **2.1: Write header and overview** (`support/sections/00-header.md`)
  - Read: `apps/docs/content/docs/index.mdx`, `apps/docs/content/docs/philosophy.mdx`, `README.md`
  - Write the opening section of the llms.txt:
    - Project name and one-line description
    - What Kibo UI is and its relationship to shadcn/ui
    - Design philosophy summary (composability, simplicity, accessibility)
    - Table of contents / component index
  - Follow `support/writing-guide.md` formatting
  - Commit: `docs: write llms.txt header and overview section`

- [ ] **2.2: Write installation guide** (`support/sections/01-installation.md`)
  - Read: `apps/docs/content/docs/setup.mdx`, `apps/docs/content/docs/usage.mdx`
  - Write comprehensive installation documentation:
    - Prerequisites (Node.js 18+, React 18+, shadcn/ui with CSS Variables)
    - Installing via shadcn CLI (`npx shadcn@latest add "https://www.kibo-ui.com/r/<name>.json"`)
    - Where components are installed (`@/components/kibo-ui/<name>/`)
    - How to import and use (with code example)
    - Extensibility (HTML attributes, Tailwind classes)
  - Follow `support/writing-guide.md` formatting
  - Commit: `docs: write llms.txt installation section`

- [ ] **2.3: Write theming guide** (`support/sections/02-theming.md`)
  - Read: `apps/docs/content/docs/philosophy.mdx`, `packages/typography/styles.css`
  - Optionally read the shadcn-ui package: `packages/shadcn-ui/`
  - Write theming documentation:
    - CSS Variables integration with shadcn/ui
    - Dark mode support (automatic via data attributes)
    - Tailwind CSS usage patterns
    - Customization approaches (className overrides, CSS variables)
  - Follow `support/writing-guide.md` formatting
  - Commit: `docs: write llms.txt theming section`

---

## Milestone 3: Component Docs — Batch A: Display & Feedback (Parallelizable)

**Goal:** Write documentation for 11 display and feedback components.

All tasks in this milestone are **parallelizable** — each writes to its own file
and has no dependency on others within this batch.

### Per-task instructions (apply to ALL component tasks in Milestones 3-6)

For each component:
1. Read `support/writing-guide.md` for the documentation template
2. Read `support/component-inventory.md` for the API summary of this component
3. Read the component source: `packages/<name>/index.tsx` (or `.css`)
4. Read the existing MDX doc: `apps/docs/content/components/<name>.mdx`
5. Read all existing examples: `apps/docs/examples/<name>*.tsx`
6. Write `support/sections/components/<name>.md` following the writing guide
7. The documentation MUST include:
   - Component heading and description
   - Installation command
   - Anatomy (all exports, with import statement)
   - Props reference for every exported component
   - Basic usage example
   - 2-4 additional usage variation examples (drawn from existing examples
     and/or constructed from the API)
8. Commit: `docs: write llms.txt docs for <name> component`

### Tasks

- [ ] **3.1:** `announcement` → `support/sections/components/announcement.md`
- [ ] **3.2:** `avatar-stack` → `support/sections/components/avatar-stack.md`
- [ ] **3.3:** `banner` → `support/sections/components/banner.md`
- [ ] **3.4:** `cursor` → `support/sections/components/cursor.md`
- [ ] **3.5:** `marquee` → `support/sections/components/marquee.md`
- [ ] **3.6:** `pill` → `support/sections/components/pill.md`
- [ ] **3.7:** `rating` → `support/sections/components/rating.md`
- [ ] **3.8:** `relative-time` → `support/sections/components/relative-time.md`
- [ ] **3.9:** `spinner` → `support/sections/components/spinner.md`
- [ ] **3.10:** `status` → `support/sections/components/status.md`
- [ ] **3.11:** `typography` → `support/sections/components/typography.md`

---

## Milestone 4: Component Docs — Batch B: Forms & Input (Parallelizable)

**Goal:** Write documentation for 8 form and input components.

All tasks in this milestone are **parallelizable**.

### Tasks

- [ ] **4.1:** `choicebox` → `support/sections/components/choicebox.md`
- [ ] **4.2:** `color-picker` → `support/sections/components/color-picker.md`
- [ ] **4.3:** `combobox` → `support/sections/components/combobox.md`
- [ ] **4.4:** `credit-card` → `support/sections/components/credit-card.md`
- [ ] **4.5:** `dropzone` → `support/sections/components/dropzone.md`
- [ ] **4.6:** `image-crop` → `support/sections/components/image-crop.md`
- [ ] **4.7:** `tags` → `support/sections/components/tags.md`
- [ ] **4.8:** `theme-switcher` → `support/sections/components/theme-switcher.md`

---

## Milestone 5: Component Docs — Batch C: Media & Visualization (Parallelizable)

**Goal:** Write documentation for 11 media and visualization components.

All tasks in this milestone are **parallelizable**.

### Tasks

- [ ] **5.1:** `calendar` → `support/sections/components/calendar.md`
- [ ] **5.2:** `code-block` → `support/sections/components/code-block.md`
- [ ] **5.3:** `comparison` → `support/sections/components/comparison.md`
- [ ] **5.4:** `contribution-graph` → `support/sections/components/contribution-graph.md`
- [ ] **5.5:** `deck` → `support/sections/components/deck.md`
- [ ] **5.6:** `glimpse` → `support/sections/components/glimpse.md`
- [ ] **5.7:** `image-zoom` → `support/sections/components/image-zoom.md`
- [ ] **5.8:** `mini-calendar` → `support/sections/components/mini-calendar.md`
- [ ] **5.9:** `qr-code` → `support/sections/components/qr-code.md`
- [ ] **5.10:** `reel` → `support/sections/components/reel.md`
- [ ] **5.11:** `stories` → `support/sections/components/stories.md`

---

## Milestone 6: Component Docs — Batch D: Data & Complex (Parallelizable)

**Goal:** Write documentation for 11 complex and data-heavy components.

All tasks in this milestone are **parallelizable**.

### Tasks

- [ ] **6.1:** `dialog-stack` → `support/sections/components/dialog-stack.md`
- [ ] **6.2:** `editor` → `support/sections/components/editor.md`
- [ ] **6.3:** `gantt` → `support/sections/components/gantt.md`
- [ ] **6.4:** `kanban` → `support/sections/components/kanban.md`
- [ ] **6.5:** `list` → `support/sections/components/list.md`
- [ ] **6.6:** `sandbox` → `support/sections/components/sandbox.md`
- [ ] **6.7:** `snippet` → `support/sections/components/snippet.md`
- [ ] **6.8:** `table` → `support/sections/components/table.md`
- [ ] **6.9:** `ticker` → `support/sections/components/ticker.md`
- [ ] **6.10:** `tree` → `support/sections/components/tree.md`
- [ ] **6.11:** `video-player` → `support/sections/components/video-player.md`

---

## Milestone 7: Assembly & Quality (Sequential)

**Goal:** Assemble all intermediate files into the final `llms.txt` and validate.

### Tasks

- [ ] **7.1: Assemble `apps/docs/public/llms.txt`**
  - Read `support/writing-guide.md` for final format rules
  - Read all section files in order:
    1. `support/sections/00-header.md`
    2. `support/sections/01-installation.md`
    3. `support/sections/02-theming.md`
    4. All `support/sections/components/*.md` files in **alphabetical order**
  - Concatenate into a single file: `apps/docs/public/llms.txt`
  - Validate:
    - All 41 components are present
    - Each component has: heading, installation, anatomy, at least one usage example
    - Formatting is consistent throughout
    - No broken markdown or unclosed code blocks
  - Commit: `docs: assemble llms.txt from generated sections`

- [ ] **7.2: Final quality pass**
  - Read `apps/docs/public/llms.txt`
  - Verify every component from the inventory table is documented
  - Verify import paths use `@/components/kibo-ui/<name>` consistently
  - Verify install commands use `npx shadcn@latest add "https://www.kibo-ui.com/r/<name>.json"` consistently
  - Fix any issues found
  - Commit: `docs: quality review pass on llms.txt`

---

## Notes

- The registry.json is dynamically generated by the Next.js API route at
  `apps/docs/app/r/registry.json/route.ts`. It does not need to be built as a
  static file for this work. Subagents read component sources directly.

- The `packages/patterns/` directory contains shadcn/ui pattern variants and is
  **excluded** from this documentation effort (it's filtered out of the registry).

- The `packages/shadcn-ui/` and `packages/typescript-config/` packages are
  internal infrastructure and are **excluded** from component documentation.
