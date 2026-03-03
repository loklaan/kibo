### Typography

> A typography component designed to display text with a consistent style.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/typography.json"
```

#### Anatomy

```tsx
import "@/components/kibo-ui/typography/styles.css"
```

Apply the `typography` class to a container element. All prose
elements within that container receive consistent styling
automatically.

#### CSS Classes

| Class | Description |
|-------|-------------|
| `.typography` | Apply to a container to style all prose elements within. |
| `.not-typography` | Apply to a nested element to exclude its children from typography styles. |

The `.typography` class styles the following HTML elements:

- **Headings** (`h1`-`h6`) — Scaled font sizes with tight letter
  spacing, scroll margins, and automatic top margins (suppressed
  for first children and for paragraphs immediately following a
  heading). `h1` increases in size at the `lg` breakpoint.
- **Paragraphs** (`p`) — 1.75 line-height with top margin between
  siblings.
- **Links** (`a`) — Primary color, medium weight, underlined with
  offset.
- **Lists** (`ul`, `ol`) — Disc or decimal markers with left
  indent and vertical spacing between items.
- **Blockquotes** (`blockquote`) — Left border, padding, and
  italic style.
- **Tables** (`table`, `th`, `td`) — Full-width with bordered
  cells, bold headers, and alternating row backgrounds.
- **Code** (`pre`, `code`) — Muted background with rounded
  corners. Inline `code` uses monospace font at a smaller size.
  `pre` blocks add vertical margin and overflow scrolling.
- **Media** (`img`, `picture`, `video`) — Vertical margin above
  and below. Images inside `picture` suppress extra margin.
- **Keyboard** (`kbd`) — Small rounded badge with muted
  background.
- **Definition lists** (`dl`, `dt`) — Bold terms with tight
  letter spacing and vertical margin.
- **Details/Summary** (`details`, `summary`) — Clickable summary
  with bold text and expandable content.
- **Highlight** (`mark`) — Yellow background.
- **Small** (`small`) — Extra-small font size.
- **Horizontal rules** (`hr`) — Generous vertical margin.

In addition, four utility classes are available inside a
`.typography` container:

| Class | Description |
|-------|-------------|
| `.lead` | Larger muted text for introductory paragraphs. |
| `.large` | Large semibold text. |
| `.small` | Small medium-weight text. |
| `.muted` | Small text in the muted foreground color. |

The container itself sets `max-width: 65ch` and uses the
`foreground` CSS variable for text color. All styles are declared
inside `@layer base`, so they integrate with Tailwind's cascade.

#### Usage

##### Basic

```tsx
import "@/components/kibo-ui/typography/styles.css"

export function Example() {
  return (
    <div className="typography">
      <h1>Getting Started</h1>
      <p>
        Welcome to the project. This guide covers
        installation, configuration, and first steps.
      </p>
      <h2>Installation</h2>
      <p>
        Run the setup command and follow the prompts.
        You will need <code>Node.js 18+</code> installed.
      </p>
      <ul>
        <li>Clone the repository</li>
        <li>Install dependencies</li>
        <li>Start the dev server</li>
      </ul>
    </div>
  )
}
```

##### Opting Out with not-typography

Apply the `not-typography` class to any nested element to
exclude its children from the typography styles.

```tsx
import "@/components/kibo-ui/typography/styles.css"

export function Example() {
  return (
    <div className="typography">
      <h1>Article Title</h1>
      <p>This paragraph is styled by typography.</p>

      <div className="not-typography">
        <p>This paragraph is not styled by typography.</p>
        <ul>
          <li>This list uses default browser styles.</li>
        </ul>
      </div>

      <blockquote>
        "Design is how it works." — Steve Jobs
      </blockquote>
    </div>
  )
}
```
