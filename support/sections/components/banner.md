### Banner

> A banner is a full-width component that can be used to show a message and action to the user.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/banner.json"
```

#### Dependencies

External packages installed automatically:
- `@radix-ui/react-use-controllable-state` — controllable open/closed state
- `lucide-react` — icon primitives

#### Anatomy

```tsx
import {
  Banner,
  BannerIcon,
  BannerTitle,
  BannerAction,
  BannerClose,
} from "@/components/kibo-ui/banner"
```

| Component | Description |
|-----------|-------------|
| `Banner` | Root container. Manages visibility state and provides context to children. |
| `BannerIcon` | Renders a Lucide icon in a rounded badge. |
| `BannerTitle` | Displays the banner message text. |
| `BannerAction` | Action button rendered as a shadcn/ui `Button`. |
| `BannerClose` | Dismiss button that hides the banner. |

#### Props

**Banner**

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `visible` | `boolean` | `undefined` | Controlled visibility state. |
| `defaultVisible` | `boolean` | `true` | Initial visibility when uncontrolled. |
| `onClose` | `() => void` | — | Called when the banner is dismissed. |
| `inset` | `boolean` | `false` | Adds rounded corners for inset layouts. |

**BannerIcon**

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `icon` | `LucideIcon` | — | The Lucide icon component to render. |

**BannerTitle**

Accepts standard `HTMLParagraphElement` attributes.

**BannerAction**

Extends shadcn/ui `Button` props. Defaults to `variant="outline"` and `size="sm"`.

**BannerClose**

Extends shadcn/ui `Button` props. Defaults to `variant="ghost"` and `size="icon"`. Dismisses the banner on click.

#### Usage

##### Basic

```tsx
"use client"

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

##### Inset

Renders the banner with rounded corners for use inside card or panel layouts.

```tsx
"use client"

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
    <Banner inset>
      <BannerIcon icon={CircleAlert} />
      <BannerTitle>Important message</BannerTitle>
      <BannerAction>Learn more</BannerAction>
      <BannerClose />
    </Banner>
  )
}
```

##### Controlled Visibility

Uses the `visible` and `onClose` props to control dismissal externally.

```tsx
"use client"

import { useState } from "react"
import {
  Banner,
  BannerIcon,
  BannerTitle,
  BannerClose,
} from "@/components/kibo-ui/banner"
import { Info } from "lucide-react"

export function Example() {
  const [visible, setVisible] = useState(true)

  return (
    <div>
      <Banner
        visible={visible}
        onClose={() => setVisible(false)}
      >
        <BannerIcon icon={Info} />
        <BannerTitle>
          This banner is controlled externally.
        </BannerTitle>
        <BannerClose />
      </Banner>
      {!visible && (
        <button onClick={() => setVisible(true)}>
          Show banner
        </button>
      )}
    </div>
  )
}
```

##### Custom Colors

Overrides the primary color tokens via CSS variables to theme banners.

```tsx
"use client"

import type { CSSProperties } from "react"
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
    <div className="flex flex-col gap-4">
      <div
        style={
          {
            "--primary": "oklch(0.637 0.237 25.331)",
            "--primary-foreground":
              "oklch(0.971 0.013 17.38)",
          } as CSSProperties
        }
      >
        <Banner>
          <BannerIcon icon={CircleAlert} />
          <BannerTitle>
            Something went wrong.
          </BannerTitle>
          <BannerAction>Restart</BannerAction>
          <BannerClose />
        </Banner>
      </div>
      <div
        style={
          {
            "--primary": "oklch(0.723 0.219 149.579)",
            "--primary-foreground":
              "oklch(0.982 0.018 155.826)",
          } as CSSProperties
        }
      >
        <Banner>
          <BannerIcon icon={CircleAlert} />
          <BannerTitle>
            Operation completed successfully.
          </BannerTitle>
          <BannerAction>View</BannerAction>
          <BannerClose />
        </Banner>
      </div>
    </div>
  )
}
```
