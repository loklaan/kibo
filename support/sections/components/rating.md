### Rating

> A star rating component with keyboard navigation and hover effects.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/rating.json"
```

#### Dependencies

External packages installed automatically:
- `@radix-ui/react-use-controllable-state` — controllable state management
- `lucide-react` — default star icon

#### Anatomy

```tsx
import { Rating, RatingButton } from "@/components/kibo-ui/rating"
```

| Component | Description |
|-----------|-------------|
| `Rating` | Root container and context provider. Manages value state, keyboard navigation, and hover tracking. Renders as a `div` with `role="radiogroup"`. |
| `RatingButton` | Individual rating icon button. Renders a star (or custom icon) that fills when active. |

#### Props

**Rating**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `defaultValue` | `number` | `0` | Initial value for uncontrolled usage. |
| `value` | `number` | — | Controlled value. |
| `onChange` | `(event: MouseEvent \| KeyboardEvent, value: number) => void` | — | Called with the native event and the selected value. |
| `onValueChange` | `(value: number) => void` | — | Called with the selected value only. |
| `readOnly` | `boolean` | `false` | Disables interaction when `true`. |
| `className` | `string` | — | Class name applied to the root container. |
| `children` | `ReactNode` | — | `RatingButton` elements to render. |

**RatingButton**

Extends `LucideProps` attributes (includes `size`, `className`, etc.).

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `icon` | `ReactElement<LucideProps>` | `<StarIcon />` | Custom icon element to render. |
| `index` | `number` | — | Positional index. Assigned automatically by `Rating`; do not set manually. |

#### Usage

##### Basic

```tsx
"use client"

import {
  Rating,
  RatingButton,
} from "@/components/kibo-ui/rating"

export function Example() {
  return (
    <Rating defaultValue={3}>
      <RatingButton />
      <RatingButton />
      <RatingButton />
      <RatingButton />
      <RatingButton />
    </Rating>
  )
}
```

##### Custom Colors

Apply a text color class to each `RatingButton` to change
the fill and stroke color.

```tsx
"use client"

import {
  Rating,
  RatingButton,
} from "@/components/kibo-ui/rating"

export function Example() {
  return (
    <Rating defaultValue={3}>
      {Array.from({ length: 5 }).map((_, index) => (
        <RatingButton
          className="text-yellow-500"
          key={index}
        />
      ))}
    </Rating>
  )
}
```

##### Custom Icon

Pass any Lucide icon element via the `icon` prop to replace
the default star.

```tsx
"use client"

import {
  Rating,
  RatingButton,
} from "@/components/kibo-ui/rating"
import { HeartIcon } from "lucide-react"

export function Example() {
  return (
    <Rating defaultValue={3}>
      {Array.from({ length: 5 }).map((_, index) => (
        <RatingButton icon={<HeartIcon />} key={index} />
      ))}
    </Rating>
  )
}
```

##### Custom Size

Set the `size` prop on `RatingButton` to control icon
dimensions in pixels.

```tsx
"use client"

import {
  Rating,
  RatingButton,
} from "@/components/kibo-ui/rating"

export function Example() {
  return (
    <Rating defaultValue={3}>
      {Array.from({ length: 5 }).map((_, index) => (
        <RatingButton key={index} size={30} />
      ))}
    </Rating>
  )
}
```

##### Controlled

Use `value` and `onValueChange` for controlled state.

```tsx
"use client"

import { useState } from "react"
import {
  Rating,
  RatingButton,
} from "@/components/kibo-ui/rating"

export function Example() {
  const [value, setValue] = useState(3)

  return (
    <div className="flex items-center gap-4">
      <Rating onValueChange={setValue} value={value}>
        {Array.from({ length: 5 }).map((_, index) => (
          <RatingButton key={index} />
        ))}
      </Rating>
      <span className="text-sm text-muted-foreground">
        {value} / 5
      </span>
    </div>
  )
}
```

##### Read-Only

Set `readOnly` to display a rating without allowing
interaction.

```tsx
"use client"

import {
  Rating,
  RatingButton,
} from "@/components/kibo-ui/rating"

export function Example() {
  return (
    <Rating defaultValue={4} readOnly>
      {Array.from({ length: 5 }).map((_, index) => (
        <RatingButton key={index} />
      ))}
    </Rating>
  )
}
```
