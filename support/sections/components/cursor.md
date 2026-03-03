### Cursor

> A cursor component, great for realtime interactive applications.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/cursor.json"
```

#### Anatomy

```tsx
import {
  Cursor,
  CursorPointer,
  CursorBody,
  CursorName,
  CursorMessage,
} from "@/components/kibo-ui/cursor"
```

| Component | Description |
|-----------|-------------|
| `Cursor` | Root container. Wraps the pointer and body. |
| `CursorPointer` | Renders the arrow-shaped cursor icon as an SVG. |
| `CursorBody` | Tooltip-style label container next to the pointer. |
| `CursorName` | Displays the user name inside the body. |
| `CursorMessage` | Displays a message inside the body. |

#### Props

**Cursor**

Extends `HTMLSpanElement` attributes.

No custom props. Uses `className` and `children` from standard
span attributes.

**CursorPointer**

Extends `SVGSVGElement` attributes.

No custom props. The SVG defaults to a 20x20 arrow icon filled
with `currentColor`. Override the color via `className`.

**CursorBody**

Extends `HTMLSpanElement` attributes.

No custom props. Applies rounded label styling automatically.
When the body contains more than one child, the first child is
displayed at reduced opacity (for the name above a message).

**CursorName**

Accepts standard `HTMLSpanElement` attributes.

**CursorMessage**

Accepts standard `HTMLSpanElement` attributes.

#### Usage

##### Basic

The simplest cursor with just a pointer icon.

```tsx
import { Cursor, CursorPointer } from "@/components/kibo-ui/cursor"

export function Example() {
  return (
    <Cursor>
      <CursorPointer />
    </Cursor>
  )
}
```

##### With Name

Display a user name label next to the cursor pointer.

```tsx
import {
  Cursor,
  CursorBody,
  CursorName,
  CursorPointer,
} from "@/components/kibo-ui/cursor"

export function Example() {
  return (
    <Cursor>
      <CursorPointer />
      <CursorBody>
        <CursorName>Hayden</CursorName>
      </CursorBody>
    </Cursor>
  )
}
```

##### With Name and Message

Show both a name and a message in the cursor label.
When both are present, the name is displayed at reduced
opacity above the message.

```tsx
import {
  Cursor,
  CursorBody,
  CursorMessage,
  CursorName,
  CursorPointer,
} from "@/components/kibo-ui/cursor"

export function Example() {
  return (
    <Cursor>
      <CursorPointer />
      <CursorBody>
        <CursorName>Hayden</CursorName>
        <CursorMessage>That looks great!</CursorMessage>
      </CursorBody>
    </Cursor>
  )
}
```

##### Custom Colors

Override the pointer and body colors using Tailwind classes
to distinguish cursors by user.

```tsx
import {
  Cursor,
  CursorBody,
  CursorMessage,
  CursorName,
  CursorPointer,
} from "@/components/kibo-ui/cursor"

export function Example() {
  return (
    <Cursor>
      <CursorPointer className="text-indigo-500" />
      <CursorBody className="bg-indigo-50 text-indigo-700">
        <CursorName>@haydenbleasel</CursorName>
        <CursorMessage>Can we adjust the color?</CursorMessage>
      </CursorBody>
    </Cursor>
  )
}
```

##### Multiple Cursors

Render multiple cursors positioned within a container
to simulate a collaborative canvas.

```tsx
import {
  Cursor,
  CursorBody,
  CursorMessage,
  CursorName,
  CursorPointer,
} from "@/components/kibo-ui/cursor"

export function Example() {
  return (
    <div className="relative h-96 w-full">
      <Cursor className="absolute top-24 left-24">
        <CursorPointer className="text-emerald-500" />
        <CursorBody className="bg-emerald-50 text-emerald-700">
          <CursorName>@alice</CursorName>
          <CursorMessage>Looking good!</CursorMessage>
        </CursorBody>
      </Cursor>
      <Cursor className="absolute top-48 right-32">
        <CursorPointer className="text-rose-500" />
        <CursorBody className="bg-rose-50 text-rose-700">
          <CursorName>@bob</CursorName>
          <CursorMessage>One more thing...</CursorMessage>
        </CursorBody>
      </Cursor>
    </div>
  )
}
```
