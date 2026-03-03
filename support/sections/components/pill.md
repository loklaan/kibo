### Pill

> A flexible badge component designed for a variety of use cases.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/pill.json"
```

#### Dependencies

External packages installed automatically:
- `lucide-react` — provides icons for delta, status, and icon sub-components

#### Anatomy

```tsx
import {
  Pill,
  PillAvatar,
  PillAvatarGroup,
  PillButton,
  PillDelta,
  PillIcon,
  PillIndicator,
  PillStatus,
} from "@/components/kibo-ui/pill"
```

| Component | Description |
|-----------|-------------|
| `Pill` | Root container. Renders a rounded badge. |
| `PillAvatar` | Displays a small avatar image with fallback text. |
| `PillAvatarGroup` | Groups multiple avatars with an overlapping layout. |
| `PillButton` | An action button rendered inside the pill. |
| `PillDelta` | Shows a directional icon for positive, negative, or neutral change. |
| `PillIcon` | Displays a Lucide icon inside the pill. |
| `PillIndicator` | A colored dot indicating status, with optional pulse animation. |
| `PillStatus` | A labeled status section separated by a right border. |

#### Props

**Pill**

Extends `Badge` component props from shadcn/ui.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `variant` | `"default" \| "secondary" \| "destructive" \| "outline"` | `"secondary"` | Visual style variant inherited from Badge. |
| `themed` | `boolean` | `false` | Enables themed styling. |

**PillAvatar**

Extends `AvatarImage` component props from shadcn/ui.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `fallback` | `string` | `undefined` | Text displayed when the image fails to load. |
| `src` | `string` | `undefined` | URL of the avatar image. |

**PillAvatarGroup**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `children` | `ReactNode` | — | `PillAvatar` elements to display overlapping. |

**PillButton**

Extends `Button` component props from shadcn/ui. Renders as a small ghost icon button.

**PillDelta**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `delta` | `number` | — | Numeric change value. Positive shows an up arrow, negative shows a down arrow, zero shows a minus. |

**PillIcon**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `icon` | `LucideIcon` | — | A Lucide icon component to render. |

**PillIndicator**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `variant` | `"success" \| "error" \| "warning" \| "info"` | `"success"` | Color of the indicator dot. |
| `pulse` | `boolean` | `false` | Enables a pulsing animation on the dot. |

**PillStatus**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `children` | `ReactNode` | — | Content displayed in the status section. |

#### Usage

##### Basic

```tsx
import { Pill } from "@/components/kibo-ui/pill"

export function Example() {
  return <Pill>Default pill</Pill>
}
```

##### With Avatar

A pill displaying a user avatar alongside a label.

```tsx
import {
  Pill,
  PillAvatar,
} from "@/components/kibo-ui/pill"

export function Example() {
  return (
    <Pill>
      <PillAvatar
        fallback="HB"
        src="/avatars/hayden.jpg"
      />
      @haydenbleasel
    </Pill>
  )
}
```

##### Status Indicator

A pill with a colored dot indicating the current state.

```tsx
import {
  Pill,
  PillIndicator,
} from "@/components/kibo-ui/pill"

export function Example() {
  return (
    <div className="flex gap-2">
      <Pill>
        <PillIndicator pulse variant="success" />
        Active
      </Pill>
      <Pill>
        <PillIndicator variant="error" />
        Error
      </Pill>
      <Pill>
        <PillIndicator variant="warning" />
        Warning
      </Pill>
    </div>
  )
}
```

##### Delta Values

Pills showing directional change with up, down, and neutral
indicators.

```tsx
import {
  Pill,
  PillDelta,
} from "@/components/kibo-ui/pill"

export function Example() {
  return (
    <div className="flex gap-2">
      <Pill>
        <PillDelta delta={10} />
        Up 10%
      </Pill>
      <Pill>
        <PillDelta delta={-5} />
        Down 5%
      </Pill>
      <Pill>
        <PillDelta delta={0} />
        No change
      </Pill>
    </div>
  )
}
```

##### Status Section with Dismissible Button

A pill combining a labeled status section with a close button.

```tsx
import {
  Pill,
  PillButton,
  PillStatus,
} from "@/components/kibo-ui/pill"
import { CheckCircleIcon, XIcon } from "lucide-react"

export function Example() {
  return (
    <Pill>
      <PillStatus>
        <CheckCircleIcon
          className="text-emerald-500"
          size={12}
        />
        Passed
      </PillStatus>
      Approval Status
      <PillButton>
        <XIcon size={12} />
      </PillButton>
    </Pill>
  )
}
```

##### Avatar Group

A pill with multiple overlapping avatars.

```tsx
import {
  Pill,
  PillAvatar,
  PillAvatarGroup,
} from "@/components/kibo-ui/pill"

export function Example() {
  return (
    <Pill>
      <PillAvatarGroup>
        <PillAvatar
          fallback="AB"
          src="/avatars/alice.jpg"
        />
        <PillAvatar
          fallback="CD"
          src="/avatars/bob.jpg"
        />
        <PillAvatar
          fallback="EF"
          src="/avatars/carol.jpg"
        />
      </PillAvatarGroup>
      3 contributors
    </Pill>
  )
}
```

##### With Icon

A pill displaying a Lucide icon alongside text.

```tsx
import { Pill, PillIcon } from "@/components/kibo-ui/pill"
import { UsersIcon } from "lucide-react"

export function Example() {
  return (
    <Pill>
      <PillIcon icon={UsersIcon} />
      17 users
    </Pill>
  )
}
```
