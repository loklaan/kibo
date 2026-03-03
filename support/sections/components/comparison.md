### Comparison

> A slider-based component for comparing two items in an overlay.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/comparison.json"
```

#### Dependencies

External packages installed automatically:
- `motion` — spring-based animations for the slider and clip-path transitions
- `lucide-react` — default grip icon for the drag handle

#### Anatomy

```tsx
import {
  Comparison,
  ComparisonItem,
  ComparisonHandle,
} from "@/components/kibo-ui/comparison"
```

| Component | Description |
|-----------|-------------|
| `Comparison` | Root container. Provides context and handles mouse/touch interaction. |
| `ComparisonItem` | Positions content on the left or right side of the slider. |
| `ComparisonHandle` | Draggable divider between the two sides. |

#### Props

**Comparison**

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `mode` | `"hover" \| "drag"` | `"drag"` | Interaction mode. `"drag"` requires click-and-drag; `"hover"` follows the cursor. |
| `onDragStart` | `() => void` | — | Called when the user begins dragging (drag mode only). |
| `onDragEnd` | `() => void` | — | Called when the user stops dragging (drag mode only). |

**ComparisonItem**

Extends `motion.div` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `position` | `"left" \| "right"` | — | Which side of the slider this item occupies. |

**ComparisonHandle**

Extends `motion.div` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `children` | `ReactNode` | — | Custom handle content. Defaults to a vertical line with a grip icon. |

#### Usage

##### Basic

```tsx
"use client"

import {
  Comparison,
  ComparisonItem,
  ComparisonHandle,
} from "@/components/kibo-ui/comparison"

export function Example() {
  return (
    <Comparison className="aspect-video">
      <ComparisonItem
        className="bg-red-500"
        position="left"
      >
        <img
          alt="Before"
          className="h-full w-full object-cover opacity-50"
          src="/before.jpg"
        />
      </ComparisonItem>
      <ComparisonItem
        className="bg-blue-500"
        position="right"
      >
        <img
          alt="After"
          className="h-full w-full object-cover opacity-50"
          src="/after.jpg"
        />
      </ComparisonItem>
      <ComparisonHandle />
    </Comparison>
  )
}
```

##### Hover Mode

The slider follows the cursor without requiring a click.

```tsx
"use client"

import {
  Comparison,
  ComparisonItem,
  ComparisonHandle,
} from "@/components/kibo-ui/comparison"

export function Example() {
  return (
    <Comparison className="aspect-video" mode="hover">
      <ComparisonItem
        className="bg-red-500"
        position="left"
      >
        <img
          alt="Before"
          className="h-full w-full object-cover opacity-50"
          src="/before.jpg"
        />
      </ComparisonItem>
      <ComparisonItem
        className="bg-blue-500"
        position="right"
      >
        <img
          alt="After"
          className="h-full w-full object-cover opacity-50"
          src="/after.jpg"
        />
      </ComparisonItem>
      <ComparisonHandle />
    </Comparison>
  )
}
```

##### With Event Handlers

Track drag start and end events for analytics or UI feedback.

```tsx
"use client"

import { useState } from "react"
import {
  Comparison,
  ComparisonItem,
  ComparisonHandle,
} from "@/components/kibo-ui/comparison"

export function Example() {
  const [dragging, setDragging] = useState(false)

  return (
    <div>
      <p>{dragging ? "Dragging..." : "Idle"}</p>
      <Comparison
        className="aspect-video"
        onDragStart={() => setDragging(true)}
        onDragEnd={() => setDragging(false)}
      >
        <ComparisonItem
          className="bg-red-500"
          position="left"
        >
          <img
            alt="Before"
            className="h-full w-full object-cover opacity-50"
            src="/before.jpg"
          />
        </ComparisonItem>
        <ComparisonItem
          className="bg-blue-500"
          position="right"
        >
          <img
            alt="After"
            className="h-full w-full object-cover opacity-50"
            src="/after.jpg"
          />
        </ComparisonItem>
        <ComparisonHandle />
      </Comparison>
    </div>
  )
}
```

##### Custom Handle

Replace the default grip icon with custom content.

```tsx
"use client"

import {
  Comparison,
  ComparisonItem,
  ComparisonHandle,
} from "@/components/kibo-ui/comparison"
import { ArrowLeftRight } from "lucide-react"

export function Example() {
  return (
    <Comparison className="aspect-video">
      <ComparisonItem
        className="bg-red-500"
        position="left"
      >
        <img
          alt="Before"
          className="h-full w-full object-cover opacity-50"
          src="/before.jpg"
        />
      </ComparisonItem>
      <ComparisonItem
        className="bg-blue-500"
        position="right"
      >
        <img
          alt="After"
          className="h-full w-full object-cover opacity-50"
          src="/after.jpg"
        />
      </ComparisonItem>
      <ComparisonHandle>
        <div className="absolute left-1/2 h-full w-0.5 -translate-x-1/2 bg-white" />
        <div className="z-50 flex h-10 w-10 items-center justify-center rounded-full bg-white shadow-md">
          <ArrowLeftRight className="h-5 w-5 text-gray-700" />
        </div>
      </ComparisonHandle>
    </Comparison>
  )
}
```
