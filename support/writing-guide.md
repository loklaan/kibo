# Kibo UI `llms.txt` Writing Guide

This document defines the format, conventions, and quality standards for
documenting Kibo UI components in `llms.txt`. Every component section must
follow these templates exactly to ensure consistency.

---

## File Format

The final `llms.txt` is a single Markdown-formatted file (`.txt` extension)
served from `apps/docs/public/llms.txt`. It is optimised for LLM consumption:
concise prose, comprehensive code examples, and consistent structure.

### Document Structure

```
# Kibo UI

> [One-line description]

[Overview prose]

## Installation

[General installation instructions]

## Theming

[Theming and customization guide]

---

## Components

### Announcement

[Component documentation]

### Avatar Stack

[Component documentation]

... (alphabetical order)
```

Component sections use `###` headings (H3). Sub-sections within a component
use `####` headings (H4).

---

## Component Documentation Template

Every component MUST include ALL of the following sections in this order.

### Template

````markdown
### Component Name

> One-line description from package.json.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/<name>.json"
```

#### Dependencies

External packages installed automatically:
- `package-a` — what it provides
- `package-b` — what it provides

(Omit this section if the component has no external dependencies beyond React.)

#### Anatomy

```tsx
import {
  ComponentA,
  ComponentB,
  ComponentC,
} from "@/components/kibo-ui/<name>"
```

| Component | Description |
|-----------|-------------|
| `ComponentA` | Root container. Wraps all child components. |
| `ComponentB` | Renders the [specific thing]. |
| `ComponentC` | Handles [specific responsibility]. |

(For hooks — include only if the component exports hooks for consumer use:)

| Hook | Description |
|------|-------------|
| `useComponentName` | Returns the current [state]. |

(For types — include only types the consumer needs to use directly, such as
data shapes passed to props, event types, or configuration objects:)

| Type | Description |
|------|-------------|
| `ItemType` | Shape of a single item passed to the `items` prop. |

#### Props

**ComponentA**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `propName` | `string` | `undefined` | What it does. |
| `onEvent` | `(value: T) => void` | — | Called when [event]. |

**ComponentB**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| ... | ... | ... | ... |

(Document props for EVERY exported component. Only include props that are
specific to the component — omit inherited HTML attributes like `className`,
`style`, `children`, `id`, etc., unless they have special behavior or
non-standard types. When a component extends HTML element attributes, note
this once at the top of its props table:
"Extends `HTMLDivElement` attributes." — then list only the custom props.)

#### Usage

##### Basic

```tsx
import {
  ComponentA,
  ComponentB,
} from "@/components/kibo-ui/<name>"

export function Example() {
  return (
    <ComponentA>
      <ComponentB />
    </ComponentA>
  )
}
```

##### [Variation Name]

Brief description of what this variation demonstrates.

```tsx
// Full working example
```

##### [Another Variation]

Brief description.

```tsx
// Full working example
```
````

---

## Component Type Classification

Each component falls into one of these categories. The category determines
which template adjustments apply. When writing documentation, identify the
correct category first, then follow the corresponding guidance below.

### 1. Composable Multi-component (majority of components)

**Examples:** banner, deck, code-block, credit-card, snippet, comparison,
cursor, marquee, qr-code, stories, table, tree, etc.

**Pattern:** A root component plus multiple sub-components composed as
children. May use internal context but does not export hooks.

Follow the standard template above. The Anatomy section lists all
sub-components. Usage examples show the composition pattern.

**Concrete example (Banner):**

```tsx
import {
  Banner,
  BannerIcon,
  BannerTitle,
  BannerAction,
  BannerClose,
} from "@/components/kibo-ui/banner"
import { CircleAlert } from "lucide-react"

export function Example() {
  return (
    <Banner>
      <BannerIcon icon={CircleAlert} />
      <BannerTitle>Important message</BannerTitle>
      <BannerAction>Learn more</BannerAction>
      <BannerClose />
    </Banner>
  )
}
```

### 2. Composable with Exported Hooks (color-picker, dialog-stack, gantt)

**Pattern:** Same as composable multi-component, but additionally exports
hooks that consumers call to read or control internal state. The hooks table
in Anatomy is required.

In the Anatomy section, list the hooks in a separate table after the
components table. In the Types table, document the return type of each hook.

One usage example MUST show the hook in action. If the hook is the primary
way to interact with the component (e.g., `useDialogStack` to programmatically
navigate dialogs), make this the "Controlled" or "Programmatic" example.

**Concrete example (Dialog Stack hook usage):**

```tsx
import {
  DialogStack,
  DialogStackBody,
  DialogStackContent,
  DialogStackTrigger,
  useDialogStack,
} from "@/components/kibo-ui/dialog-stack"

function StepNavigation() {
  const { activeIndex, setActiveIndex } = useDialogStack()
  return (
    <button onClick={() => setActiveIndex(activeIndex + 1)}>
      Next Step
    </button>
  )
}
```

### 3. Render-prop Composable (kanban, gantt, list)

**Pattern:** A provider component accepts `children` as a render function
rather than standard JSX children. The render function receives the current
item (column, group, etc.) and returns JSX for each iteration.

This pattern MUST be clearly documented:
- In the Props section, show the `children` prop type as a render function
  signature: `(column: C) => ReactNode`
- In the Types section, document the data shape that the render function
  receives
- Usage examples MUST show the render function pattern

**Concrete example (Kanban):**

```tsx
import {
  KanbanProvider,
  KanbanBoard,
  KanbanHeader,
  KanbanCards,
  KanbanCard,
} from "@/components/kibo-ui/kanban"

const columns = [
  { id: "1", name: "To Do", color: "#6B7280" },
  { id: "2", name: "Done", color: "#10B981" },
]

const tasks = [
  { id: "a", name: "Write docs", column: "1" },
  { id: "b", name: "Ship feature", column: "2" },
]

export function Example() {
  const [data, setData] = useState(tasks)

  return (
    <KanbanProvider
      columns={columns}
      data={data}
      onDataChange={setData}
    >
      {(column) => (
        <KanbanBoard id={column.id} key={column.id}>
          <KanbanHeader>{column.name}</KanbanHeader>
          <KanbanCards id={column.id}>
            {(task) => (
              <KanbanCard
                id={task.id}
                name={task.name}
                column={column.id}
                key={task.id}
              />
            )}
          </KanbanCards>
        </KanbanBoard>
      )}
    </KanbanProvider>
  )
}
```

### 4. Props-driven Single Component (avatar-stack, image-zoom)

**Pattern:** A single exported component that accepts all configuration
through props. No sub-component composition.

Use the standard template but with a single-item Anatomy table. The Props
section has one table. When the component accepts a data array prop (like
`avatars` in avatar-stack), document the shape of array items in the Types
table.

**Concrete example (Avatar Stack):**

```tsx
import { AvatarStack } from "@/components/kibo-ui/avatar-stack"

export function Example() {
  return (
    <AvatarStack
      avatars={[
        { src: "/alice.jpg", alt: "Alice" },
        { src: "/bob.jpg", alt: "Bob" },
        { src: "/carol.jpg", alt: "Carol" },
      ]}
      limit={3}
    />
  )
}
```

### 5. Variant-based Single Component (spinner)

**Pattern:** A single exported component where the primary API surface is a
`variant` prop that selects between distinct visual or behavioral modes.

In the Props table, list ALL variants as a union type. Include one usage
example that demonstrates multiple variants side by side, and optionally
another showing customisation (size, color).

**Concrete example (Spinner):**

```tsx
import { Spinner } from "@/components/kibo-ui/spinner"

export function Example() {
  return (
    <div className="flex gap-4">
      <Spinner variant="default" />
      <Spinner variant="throbber" />
      <Spinner variant="pinwheel" />
      <Spinner variant="circle-filled" />
      <Spinner variant="ellipsis" />
      <Spinner variant="ring" />
      <Spinner variant="bars" />
      <Spinner variant="infinite" />
    </div>
  )
}
```

### 6. CSS-only (typography)

**Pattern:** The package exports a CSS stylesheet, not React components.
There are no component imports or props.

Replace the standard Anatomy section with:

```tsx
import "@/components/kibo-ui/typography/styles.css"
```

Replace the Props section with a **CSS Classes** section:

| Class | Description |
|-------|-------------|
| `.typography` | Apply to a container to style all prose elements within. |
| `.not-typography` | Apply to nested elements to exclude them from typography styles. |

List the styled HTML elements (headings, paragraphs, lists, tables, code,
blockquotes, etc.) as a prose description, not individual rows.

Usage examples show class application on standard HTML:

```tsx
import "@/components/kibo-ui/typography/styles.css"

export function Example() {
  return (
    <div className="typography">
      <h1>Heading</h1>
      <p>Paragraph text with <code>inline code</code>.</p>
      <ul>
        <li>List item</li>
      </ul>
    </div>
  )
}
```

---

## Documenting Data Types

Many components accept typed data arrays or objects. When a component requires
the consumer to shape data in a specific way, document the type in the Types
table with its full shape.

### Rules for the Types Table

- Include types ONLY when the consumer must construct or reference them.
  Internal prop types (like `BannerTitleProps`) that just extend HTML
  attributes are not useful to document.
- DO include data shapes: `CalendarEvent`, `ContributionData`,
  `GanttFeature`, `GanttStatus`, etc.
- DO include re-exported types from dependencies that consumers use directly:
  `DragEndEvent` from `@dnd-kit/core` (re-exported by kanban and list).
- DO include hook return types when not obvious from the description.
- Format complex types as a mini code block within the table cell or
  immediately after the table if the shape is too wide for a table cell.

**Example — type too wide for table cell:**

After the Types table, add:

```ts
type CalendarEvent = {
  id: string
  name: string
  startAt: Date
  endAt: Date
  color: string
}
```

---

## Writing Rules

### Prose

- Be concise. One sentence per description. No filler words.
- Write for an LLM that will use this as a reference when generating code.
- Use present tense, active voice.
- Do not use marketing language or superlatives.
- Do not reference the documentation site, external links, or "see also"
  links. The llms.txt must be self-contained.

### Code Examples

- Every example must be a complete, working JSX snippet.
- Use function component syntax: `export function Example() { ... }`
- Always show the full import statement at the top.
- Use realistic but minimal data (e.g., 2-3 items in a list, not 10).
- Include TypeScript types when they add clarity (e.g., typed state).
- Do NOT use `'use client'` directives unless the component specifically
  requires client-side interactivity that wouldn't work in a server component.
  When in doubt, include it for interactive components.
- When adapting from existing examples in `apps/docs/examples/`, change the
  import path from `@repo/<name>` to `@/components/kibo-ui/<name>`.
- Do NOT use `@faker-js/faker` or other test data libraries. Use hardcoded
  realistic data instead.
- Prefer `export function Example()` over `const Example = () =>` for
  consistency.

### Props Tables

- Only document props that are specific to the component.
- When a component extends HTML element attributes, note this as a single
  line before the props table: "Extends `HTMLDivElement` attributes." Then
  list only the custom props below.
- If a component has NO custom props beyond the HTML attributes it extends,
  write: "Accepts standard `HTMLDivElement` attributes." and omit the table.
- Use TypeScript type notation (e.g., `string`, `number`, `boolean`,
  `(value: string) => void`).
- Use `—` (em dash) for props with no default value.
- For union types, list the full union: `"sm" | "md" | "lg"`.
- For complex types, use a simplified notation and reference the Types table.
- For callback/event props, show the full signature:
  `(event: DragEndEvent) => void`.

### Usage Variations

Each component should have **at minimum 3 usage examples**:

1. **Basic** — the simplest possible usage with minimal props
2. **With data / configuration** — shows key props in action
3. **Controlled** — shows controlled state pattern (if applicable), OR
   another meaningful variation (custom styling, event handling, etc.)

Aim for **3-5 examples** per component. Draw from:
- Existing examples in `apps/docs/examples/<name>*.tsx`
- Props that enable distinct usage patterns
- Common real-world use cases

**Exceptions to the 3-example minimum:**
- CSS-only components (typography): 2 examples are acceptable (basic usage
  and an example showing the `.not-typography` opt-out).
- Variant-based single components (spinner): a "Variants" example showing
  all variants counts as one example, plus customisation and sizing.

### Formatting

- Use fenced code blocks with `tsx` language tag for JSX examples.
- Use fenced code blocks with `bash` language tag for shell commands.
- Use fenced code blocks with `ts` language tag for standalone type
  definitions shown outside JSX.
- Use pipe tables for structured data (props, anatomy, types).
- Separate components with `---` (horizontal rule) between each H3 section.
- Keep lines under 80 characters in prose where reasonable.
- In code examples, keep lines under 80 characters where possible. Prefer
  multi-line JSX props formatting over single long lines.

---

## Quality Checklist

Before considering a component section complete, verify:

- [ ] Correct component type identified (composable, context-based,
      render-prop, props-driven, variant-based, or CSS-only)
- [ ] H3 heading matches the component display name (Title Case, e.g.,
      "Color Picker" not "color-picker")
- [ ] Description is one sentence from `package.json`
- [ ] Installation command uses correct URL format with the package's
      kebab-case name
- [ ] All exported components listed in Anatomy table
- [ ] All exported hooks listed (if any)
- [ ] Data types that consumers must construct are documented
- [ ] Re-exported types from dependencies are documented (if any)
- [ ] Props documented for every exported component
- [ ] "Extends `HTMLXElement` attributes" noted where applicable
- [ ] At least 3 working code examples (2 for CSS-only / variant-based)
- [ ] For render-prop components: at least one example shows the render
      function pattern clearly
- [ ] For hook-exporting components: at least one example shows hook usage
- [ ] Import paths use `@/components/kibo-ui/<name>` (not `@repo/<name>`)
- [ ] No `@faker-js/faker` or test-only dependencies in examples
- [ ] No references to external URLs or docs site
- [ ] No placeholder text or TODOs
