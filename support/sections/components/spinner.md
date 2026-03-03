### Spinner

> A spinner is a visual indicator that shows progress or activity.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/spinner.json"
```

#### Dependencies

External packages installed automatically:
- `lucide-react` — provides icon-based spinner variants (throbber, pinwheel, circle-filled)

#### Anatomy

```tsx
import { Spinner } from "@/components/kibo-ui/spinner"
```

| Component | Description |
|-----------|-------------|
| `Spinner` | Renders an animated loading indicator. Selects between 8 animation styles via the `variant` prop. |

| Type | Description |
|------|-------------|
| `SpinnerProps` | Props for the `Spinner` component. |

```ts
type SpinnerProps = LucideProps & {
  variant?:
    | "default"
    | "throbber"
    | "pinwheel"
    | "circle-filled"
    | "ellipsis"
    | "ring"
    | "bars"
    | "infinite"
}
```

#### Props

**Spinner**

Extends `LucideProps` attributes (includes `size`, `className`, `color`, `strokeWidth`, and standard SVG attributes).

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `variant` | `"default" \| "throbber" \| "pinwheel" \| "circle-filled" \| "ellipsis" \| "ring" \| "bars" \| "infinite"` | `"default"` | Selects the animation style. |
| `size` | `number` | `24` | Width and height in pixels. |

#### Usage

##### Basic

```tsx
import { Spinner } from "@/components/kibo-ui/spinner"

export function Example() {
  return <Spinner />
}
```

##### Variants

Each variant renders a distinct animation style.

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

##### Custom Size and Color

Use the `size` prop and Tailwind text color classes to control appearance.

```tsx
import { Spinner } from "@/components/kibo-ui/spinner"

export function Example() {
  return (
    <div className="flex items-center gap-4">
      <Spinner size={16} />
      <Spinner size={32} />
      <Spinner
        className="text-blue-500"
        size={64}
      />
    </div>
  )
}
```
