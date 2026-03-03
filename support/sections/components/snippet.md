### Snippet

> Snippet is a component that allows you to display and copy code in a tabbed interface.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/snippet.json"
```

#### Dependencies

External packages installed automatically:
- `lucide-react` — copy and check icons for the copy button

#### Anatomy

```tsx
import {
  Snippet,
  SnippetHeader,
  SnippetCopyButton,
  SnippetTabsList,
  SnippetTabsTrigger,
  SnippetTabsContent,
} from "@/components/kibo-ui/snippet"
```

| Component | Description |
|-----------|-------------|
| `Snippet` | Root container. Built on the Radix Tabs primitive. Manages the active tab value. |
| `SnippetHeader` | Header bar containing the tab list and copy button. |
| `SnippetCopyButton` | Copies a given string to the clipboard. Shows a check icon on success. |
| `SnippetTabsList` | Container for tab triggers. Alias for the Radix TabsList. |
| `SnippetTabsTrigger` | A single tab trigger button. |
| `SnippetTabsContent` | Tab content panel rendered as a `<pre>` element. |

#### Props

**Snippet**

Extends Radix `Tabs` component props.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `value` | `string` | — | Active tab value (controlled). |
| `defaultValue` | `string` | — | Initial active tab value (uncontrolled). |
| `onValueChange` | `(value: string) => void` | — | Called when the active tab changes. |

**SnippetHeader**

Accepts standard `HTMLDivElement` attributes.

**SnippetCopyButton**

Extends shadcn/ui `Button` props.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `value` | `string` | — | The string to copy to the clipboard. |
| `onCopy` | `() => void` | — | Called after the value is copied. |
| `onError` | `(error: Error) => void` | — | Called if the copy operation fails. |
| `timeout` | `number` | `2000` | Duration in ms to show the check icon after copying. |
| `asChild` | `boolean` | `false` | Render as a child element instead of the default button. |

**SnippetTabsList**

Accepts standard Radix `TabsList` props.

**SnippetTabsTrigger**

Accepts standard Radix `TabsTrigger` props.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `value` | `string` | — | The tab value this trigger activates. |

**SnippetTabsContent**

Accepts standard Radix `TabsContent` props. Renders content inside a `<pre>` element.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `value` | `string` | — | The tab value this content corresponds to. |

#### Usage

##### Basic

A single-tab snippet displaying one command with a copy button.

```tsx
"use client"

import {
  Snippet,
  SnippetCopyButton,
  SnippetHeader,
  SnippetTabsContent,
  SnippetTabsList,
  SnippetTabsTrigger,
} from "@/components/kibo-ui/snippet"

export function Example() {
  return (
    <Snippet defaultValue="bash">
      <SnippetHeader>
        <SnippetTabsList>
          <SnippetTabsTrigger value="bash">
            bash
          </SnippetTabsTrigger>
        </SnippetTabsList>
        <SnippetCopyButton value="npm install react" />
      </SnippetHeader>
      <SnippetTabsContent value="bash">
        npm install react
      </SnippetTabsContent>
    </Snippet>
  )
}
```

##### Multiple Package Managers

Tabbed snippet showing the same install command across
different package managers.

```tsx
"use client"

import {
  Snippet,
  SnippetCopyButton,
  SnippetHeader,
  SnippetTabsContent,
  SnippetTabsList,
  SnippetTabsTrigger,
} from "@/components/kibo-ui/snippet"
import { useState } from "react"

const commands = [
  { label: "npm", code: "npx next-forge@latest init" },
  { label: "yarn", code: "yarn dlx next-forge@latest init" },
  { label: "pnpm", code: "pnpx next-forge@latest init" },
  { label: "bun", code: "bunx next-forge@latest init" },
]

export function Example() {
  const [value, setValue] = useState(commands[0].label)
  const active = commands.find((c) => c.label === value)

  return (
    <Snippet onValueChange={setValue} value={value}>
      <SnippetHeader>
        <SnippetTabsList>
          {commands.map((cmd) => (
            <SnippetTabsTrigger
              key={cmd.label}
              value={cmd.label}
            >
              {cmd.label}
            </SnippetTabsTrigger>
          ))}
        </SnippetTabsList>
        {active && (
          <SnippetCopyButton value={active.code} />
        )}
      </SnippetHeader>
      {commands.map((cmd) => (
        <SnippetTabsContent key={cmd.label} value={cmd.label}>
          {cmd.code}
        </SnippetTabsContent>
      ))}
    </Snippet>
  )
}
```

##### With Icons and Copy Callbacks

Tab triggers with icons and copy event handlers for
logging or toast notifications.

```tsx
"use client"

import {
  Snippet,
  SnippetCopyButton,
  SnippetHeader,
  SnippetTabsContent,
  SnippetTabsList,
  SnippetTabsTrigger,
} from "@/components/kibo-ui/snippet"
import { BoxIcon, HeartIcon } from "lucide-react"
import { useState } from "react"

const commands = [
  {
    label: "kibo-ui",
    icon: HeartIcon,
    code: "npx kibo-ui@latest add snippet",
  },
  {
    label: "shadcn",
    icon: BoxIcon,
    code: "npx shadcn@latest add https://www.kibo-ui.com/r/snippet.json",
  },
]

export function Example() {
  const [value, setValue] = useState(commands[0].label)
  const active = commands.find((c) => c.label === value)

  return (
    <Snippet onValueChange={setValue} value={value}>
      <SnippetHeader>
        <SnippetTabsList>
          {commands.map((cmd) => (
            <SnippetTabsTrigger
              key={cmd.label}
              value={cmd.label}
            >
              <cmd.icon size={14} />
              <span>{cmd.label}</span>
            </SnippetTabsTrigger>
          ))}
        </SnippetTabsList>
        {active && (
          <SnippetCopyButton
            onCopy={() => console.log("Copied:", active.code)}
            onError={(err) => console.error("Copy failed:", err)}
            value={active.code}
          />
        )}
      </SnippetHeader>
      {commands.map((cmd) => (
        <SnippetTabsContent key={cmd.label} value={cmd.label}>
          {cmd.code}
        </SnippetTabsContent>
      ))}
    </Snippet>
  )
}
```

##### Custom Copy Button Timeout

Adjust the duration the check icon displays after copying
by passing a custom `timeout` value.

```tsx
"use client"

import {
  Snippet,
  SnippetCopyButton,
  SnippetHeader,
  SnippetTabsContent,
  SnippetTabsList,
  SnippetTabsTrigger,
} from "@/components/kibo-ui/snippet"

export function Example() {
  return (
    <Snippet defaultValue="curl">
      <SnippetHeader>
        <SnippetTabsList>
          <SnippetTabsTrigger value="curl">
            curl
          </SnippetTabsTrigger>
        </SnippetTabsList>
        <SnippetCopyButton
          value="curl -X GET https://api.example.com/data"
          timeout={5000}
        />
      </SnippetHeader>
      <SnippetTabsContent value="curl">
        curl -X GET https://api.example.com/data
      </SnippetTabsContent>
    </Snippet>
  )
}
```
