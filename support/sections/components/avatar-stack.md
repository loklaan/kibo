### Avatar Stack

> A component that stacks and overlaps avatars for displaying groups of users.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/avatar-stack.json"
```

#### Anatomy

```tsx
import { AvatarStack } from "@/components/kibo-ui/avatar-stack"
```

| Component | Description |
|-----------|-------------|
| `AvatarStack` | Root container. Wraps shadcn `Avatar` children and renders them in an overlapping stack with radial masks. |

AvatarStack accepts shadcn `Avatar` components as children.
Each child is wrapped in a clipping container with a circular
mask that creates the overlapping cutout effect.

#### Props

**AvatarStack**

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `animate` | `boolean` | `false` | Enables hover animation that expands the stack spacing on hover. |
| `size` | `number` | `40` | Width and height in pixels for each avatar slot. |

#### Usage

##### Basic

```tsx
import { AvatarStack } from "@/components/kibo-ui/avatar-stack"
import {
  Avatar,
  AvatarFallback,
  AvatarImage,
} from "@/components/ui/avatar"

export function Example() {
  return (
    <AvatarStack>
      <Avatar>
        <AvatarImage src="/alice.jpg" />
        <AvatarFallback>AL</AvatarFallback>
      </Avatar>
      <Avatar>
        <AvatarImage src="/bob.jpg" />
        <AvatarFallback>BO</AvatarFallback>
      </Avatar>
      <Avatar>
        <AvatarImage src="/carol.jpg" />
        <AvatarFallback>CA</AvatarFallback>
      </Avatar>
    </AvatarStack>
  )
}
```

##### Hover Animation

Enable the `animate` prop to expand spacing between avatars
on hover, revealing each one fully.

```tsx
import { AvatarStack } from "@/components/kibo-ui/avatar-stack"
import {
  Avatar,
  AvatarFallback,
  AvatarImage,
} from "@/components/ui/avatar"

export function Example() {
  return (
    <AvatarStack animate>
      <Avatar>
        <AvatarImage src="/alice.jpg" />
        <AvatarFallback>AL</AvatarFallback>
      </Avatar>
      <Avatar>
        <AvatarImage src="/bob.jpg" />
        <AvatarFallback>BO</AvatarFallback>
      </Avatar>
      <Avatar>
        <AvatarImage src="/carol.jpg" />
        <AvatarFallback>CA</AvatarFallback>
      </Avatar>
    </AvatarStack>
  )
}
```

##### Custom Size

Use the `size` prop to control the pixel dimensions of each
avatar slot. The default is 40px.

```tsx
import { AvatarStack } from "@/components/kibo-ui/avatar-stack"
import {
  Avatar,
  AvatarFallback,
  AvatarImage,
} from "@/components/ui/avatar"

export function Example() {
  return (
    <div className="flex flex-col gap-4">
      <AvatarStack size={24}>
        <Avatar>
          <AvatarImage src="/alice.jpg" />
          <AvatarFallback>AL</AvatarFallback>
        </Avatar>
        <Avatar>
          <AvatarImage src="/bob.jpg" />
          <AvatarFallback>BO</AvatarFallback>
        </Avatar>
      </AvatarStack>

      <AvatarStack size={64}>
        <Avatar>
          <AvatarImage src="/alice.jpg" />
          <AvatarFallback>AL</AvatarFallback>
        </Avatar>
        <Avatar>
          <AvatarImage src="/bob.jpg" />
          <AvatarFallback>BO</AvatarFallback>
        </Avatar>
      </AvatarStack>
    </div>
  )
}
```

##### Fallback Only

AvatarStack works with fallback-only avatars for cases
where no image is available.

```tsx
import { AvatarStack } from "@/components/kibo-ui/avatar-stack"
import {
  Avatar,
  AvatarFallback,
} from "@/components/ui/avatar"

export function Example() {
  return (
    <AvatarStack animate size={48}>
      <Avatar>
        <AvatarFallback>AL</AvatarFallback>
      </Avatar>
      <Avatar>
        <AvatarFallback>BO</AvatarFallback>
      </Avatar>
      <Avatar>
        <AvatarFallback>CA</AvatarFallback>
      </Avatar>
      <Avatar>
        <AvatarFallback>DV</AvatarFallback>
      </Avatar>
    </AvatarStack>
  )
}
```
