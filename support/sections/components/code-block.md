### Code Block

> Provides syntax highlighting, line numbers, and copy to clipboard functionality for code blocks.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/code-block.json"
```

#### Dependencies

External packages installed automatically:
- `shiki` — syntax highlighting engine
- `@shikijs/transformers` — line highlight, diff, focus, and word highlight transformers
- `@radix-ui/react-use-controllable-state` — controlled/uncontrolled state management
- `lucide-react` — copy and check icons
- `react-icons` — file type icons for filename display

#### Anatomy

```tsx
import {
  CodeBlock,
  CodeBlockHeader,
  CodeBlockFiles,
  CodeBlockFilename,
  CodeBlockSelect,
  CodeBlockSelectTrigger,
  CodeBlockSelectValue,
  CodeBlockSelectContent,
  CodeBlockSelectItem,
  CodeBlockCopyButton,
  CodeBlockBody,
  CodeBlockItem,
  CodeBlockContent,
} from "@/components/kibo-ui/code-block"
```

| Component | Description |
|-----------|-------------|
| `CodeBlock` | Root container. Accepts a `data` array and manages the active tab value. |
| `CodeBlockHeader` | Header bar area for filenames, language select, and copy button. |
| `CodeBlockFiles` | Render-prop container that iterates over the data array to render filenames. |
| `CodeBlockFilename` | Displays the filename and an auto-detected file type icon for the active tab. |
| `CodeBlockSelect` | Language/tab selector built on the shadcn/ui Select primitive. |
| `CodeBlockSelectTrigger` | Trigger button for the language selector dropdown. |
| `CodeBlockSelectValue` | Displays the selected language value. |
| `CodeBlockSelectContent` | Render-prop dropdown content that iterates over data to render select items. |
| `CodeBlockSelectItem` | A single item in the language selector dropdown. |
| `CodeBlockCopyButton` | Copies the active tab's code to the clipboard. Shows a check icon on success. |
| `CodeBlockBody` | Render-prop container that iterates over the data array to render code panels. |
| `CodeBlockItem` | Wrapper for a single code panel. Controls line number display and visibility based on active tab. |
| `CodeBlockContent` | Renders syntax-highlighted code using Shiki. Accepts the raw code string as `children`. |

| Type | Description |
|------|-------------|
| `BundledLanguage` | Re-exported from `shiki`. Union of all supported language identifiers. |

```ts
type CodeBlockData = {
  language: string
  filename: string
  code: string
}
```

#### Props

**CodeBlock**

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `data` | `CodeBlockData[]` | -- | Array of code entries to display. |
| `defaultValue` | `string` | `""` | Initial active tab value (uncontrolled). |
| `value` | `string` | -- | Active tab value (controlled). |
| `onValueChange` | `(value: string) => void` | -- | Called when the active tab changes. |

**CodeBlockHeader**

Accepts standard `HTMLDivElement` attributes.

**CodeBlockFiles**

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `children` | `(item: CodeBlockData) => ReactNode` | -- | Render function called for each data entry. |

**CodeBlockFilename**

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `icon` | `IconType` | -- | Override the auto-detected file type icon. |
| `value` | `string` | -- | Tab value this filename corresponds to. Only renders when active. |

**CodeBlockSelect**

Accepts standard shadcn/ui `Select` props. Automatically binds to the CodeBlock context value.

**CodeBlockSelectTrigger**

Accepts standard shadcn/ui `SelectTrigger` props.

**CodeBlockSelectValue**

Accepts standard shadcn/ui `SelectValue` props.

**CodeBlockSelectContent**

Extends shadcn/ui `SelectContent` props.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `children` | `(item: CodeBlockData) => ReactNode` | -- | Render function called for each data entry. |

**CodeBlockSelectItem**

Accepts standard shadcn/ui `SelectItem` props.

**CodeBlockCopyButton**

Extends shadcn/ui `Button` props.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `onCopy` | `() => void` | -- | Called after code is copied to the clipboard. |
| `onError` | `(error: Error) => void` | -- | Called if the copy operation fails. |
| `timeout` | `number` | `2000` | Duration in ms to show the check icon after copying. |

**CodeBlockBody**

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `children` | `(item: CodeBlockData) => ReactNode` | -- | Render function called for each data entry. |

**CodeBlockItem**

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `value` | `string` | -- | Tab value this item corresponds to. Only renders when active. |
| `lineNumbers` | `boolean` | `true` | Whether to display line numbers. |

**CodeBlockContent**

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `children` | `string` | -- | The raw code string to highlight. |
| `language` | `BundledLanguage` | `"typescript"` | Language for syntax highlighting. |
| `themes` | `{ light: string; dark: string }` | `{ light: "github-light", dark: "github-dark-default" }` | Shiki themes for light and dark mode. |
| `syntaxHighlighting` | `boolean` | `true` | Whether to apply syntax highlighting. When `false`, renders plain text. |

#### Usage

##### Basic

Minimal code block without a header, displaying a single file.

```tsx
"use client"

import type { BundledLanguage } from "@/components/kibo-ui/code-block"
import {
  CodeBlock,
  CodeBlockBody,
  CodeBlockContent,
  CodeBlockItem,
} from "@/components/kibo-ui/code-block"

const data = [
  {
    language: "tsx",
    filename: "App.tsx",
    code: `export function App() {
  return <h1>Hello, world!</h1>
}`,
  },
]

export function Example() {
  return (
    <CodeBlock data={data} defaultValue="tsx">
      <CodeBlockBody>
        {(item) => (
          <CodeBlockItem key={item.language} value={item.language}>
            <CodeBlockContent
              language={item.language as BundledLanguage}
            >
              {item.code}
            </CodeBlockContent>
          </CodeBlockItem>
        )}
      </CodeBlockBody>
    </CodeBlock>
  )
}
```

##### With Header, File Tabs, and Copy Button

Full-featured code block with filename display, a language
selector dropdown, and a copy-to-clipboard button.

```tsx
"use client"

import type { BundledLanguage } from "@/components/kibo-ui/code-block"
import {
  CodeBlock,
  CodeBlockBody,
  CodeBlockContent,
  CodeBlockCopyButton,
  CodeBlockFilename,
  CodeBlockFiles,
  CodeBlockHeader,
  CodeBlockItem,
  CodeBlockSelect,
  CodeBlockSelectContent,
  CodeBlockSelectItem,
  CodeBlockSelectTrigger,
  CodeBlockSelectValue,
} from "@/components/kibo-ui/code-block"

const data = [
  {
    language: "jsx",
    filename: "App.jsx",
    code: `function App(props) {
  return (
    <div>
      <h1>Hello, {props.name}!</h1>
    </div>
  )
}`,
  },
  {
    language: "tsx",
    filename: "App.tsx",
    code: `function App(props: { name: string }) {
  return (
    <div>
      <h1>Hello, {props.name}!</h1>
    </div>
  )
}`,
  },
]

export function Example() {
  return (
    <CodeBlock data={data} defaultValue={data[0].language}>
      <CodeBlockHeader>
        <CodeBlockFiles>
          {(item) => (
            <CodeBlockFilename
              key={item.language}
              value={item.language}
            >
              {item.filename}
            </CodeBlockFilename>
          )}
        </CodeBlockFiles>
        <CodeBlockSelect>
          <CodeBlockSelectTrigger>
            <CodeBlockSelectValue />
          </CodeBlockSelectTrigger>
          <CodeBlockSelectContent>
            {(item) => (
              <CodeBlockSelectItem
                key={item.language}
                value={item.language}
              >
                {item.language}
              </CodeBlockSelectItem>
            )}
          </CodeBlockSelectContent>
        </CodeBlockSelect>
        <CodeBlockCopyButton />
      </CodeBlockHeader>
      <CodeBlockBody>
        {(item) => (
          <CodeBlockItem
            key={item.language}
            value={item.language}
          >
            <CodeBlockContent
              language={item.language as BundledLanguage}
            >
              {item.code}
            </CodeBlockContent>
          </CodeBlockItem>
        )}
      </CodeBlockBody>
    </CodeBlock>
  )
}
```

##### Line Highlighting and Diff

Use Shiki comment annotations inside your code strings to
highlight lines, show diffs, focus lines, or highlight words.

```tsx
"use client"

import type { BundledLanguage } from "@/components/kibo-ui/code-block"
import {
  CodeBlock,
  CodeBlockBody,
  CodeBlockContent,
  CodeBlockHeader,
  CodeBlockCopyButton,
  CodeBlockFilename,
  CodeBlockFiles,
  CodeBlockItem,
} from "@/components/kibo-ui/code-block"

const data = [
  {
    language: "ts",
    filename: "utils.ts",
    code: `function calculateTotal(items: Item[]) {
  let total = 0
  for (const item of items) {
    total += item.price * item.quantity // [!code --]
    const subtotal = item.price * item.quantity // [!code ++]
    total += subtotal // [!code ++]
  }
  return total // [!code highlight]
}`,
  },
]

export function Example() {
  return (
    <CodeBlock data={data} defaultValue="ts">
      <CodeBlockHeader>
        <CodeBlockFiles>
          {(item) => (
            <CodeBlockFilename
              key={item.language}
              value={item.language}
            >
              {item.filename}
            </CodeBlockFilename>
          )}
        </CodeBlockFiles>
        <CodeBlockCopyButton />
      </CodeBlockHeader>
      <CodeBlockBody>
        {(item) => (
          <CodeBlockItem
            key={item.language}
            value={item.language}
          >
            <CodeBlockContent
              language={item.language as BundledLanguage}
            >
              {item.code}
            </CodeBlockContent>
          </CodeBlockItem>
        )}
      </CodeBlockBody>
    </CodeBlock>
  )
}
```

Supported annotations within code strings:
- `// [!code highlight]` -- highlights the line
- `// [!code ++]` -- marks the line as an addition (green)
- `// [!code --]` -- marks the line as a removal (red)
- `// [!code focus]` -- focuses the line, blurring all others
- `// [!code word:term]` -- highlights occurrences of "term"

##### Custom Theme

Override the default Shiki themes for light and dark mode
via the `themes` prop on `CodeBlockContent`.

```tsx
"use client"

import type { BundledLanguage } from "@/components/kibo-ui/code-block"
import {
  CodeBlock,
  CodeBlockBody,
  CodeBlockContent,
  CodeBlockItem,
} from "@/components/kibo-ui/code-block"

const data = [
  {
    language: "tsx",
    filename: "App.tsx",
    code: `export function App() {
  return <h1>Hello, world!</h1>
}`,
  },
]

export function Example() {
  return (
    <CodeBlock data={data} defaultValue="tsx">
      <CodeBlockBody>
        {(item) => (
          <CodeBlockItem
            key={item.language}
            value={item.language}
          >
            <CodeBlockContent
              language={item.language as BundledLanguage}
              themes={{
                light: "vitesse-light",
                dark: "vitesse-dark",
              }}
            >
              {item.code}
            </CodeBlockContent>
          </CodeBlockItem>
        )}
      </CodeBlockBody>
    </CodeBlock>
  )
}
```

##### Hidden Line Numbers

Disable line numbers by setting `lineNumbers={false}` on
`CodeBlockItem`.

```tsx
"use client"

import type { BundledLanguage } from "@/components/kibo-ui/code-block"
import {
  CodeBlock,
  CodeBlockBody,
  CodeBlockContent,
  CodeBlockItem,
} from "@/components/kibo-ui/code-block"

const data = [
  {
    language: "tsx",
    filename: "App.tsx",
    code: `export function App() {
  return <h1>Hello, world!</h1>
}`,
  },
]

export function Example() {
  return (
    <CodeBlock data={data} defaultValue="tsx">
      <CodeBlockBody>
        {(item) => (
          <CodeBlockItem
            key={item.language}
            value={item.language}
            lineNumbers={false}
          >
            <CodeBlockContent
              language={item.language as BundledLanguage}
            >
              {item.code}
            </CodeBlockContent>
          </CodeBlockItem>
        )}
      </CodeBlockBody>
    </CodeBlock>
  )
}
```
