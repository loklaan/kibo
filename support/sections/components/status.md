### Status

> Status components are used to display the uptime of a service.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/status.json"
```

#### Anatomy

```tsx
import {
  Status,
  StatusIndicator,
  StatusLabel,
} from "@/components/kibo-ui/status"
```

| Component | Description |
|-----------|-------------|
| `Status` | Root container. Renders a Badge with status-based styling. |
| `StatusIndicator` | Animated pulsing dot colored by the current status. |
| `StatusLabel` | Text label. Displays automatic text matching the status when no children are provided. |

#### Props

**Status**

Extends `Badge` component props from shadcn/ui.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `status` | `"online" \| "offline" \| "maintenance" \| "degraded"` | — | The current status. Controls indicator color and default label text. |

**StatusIndicator**

Accepts standard `HTMLSpanElement` attributes.

**StatusLabel**

Accepts standard `HTMLSpanElement` attributes. When no `children` are provided, renders a default label matching the parent `status` value ("Online", "Offline", "Maintenance", or "Degraded").

#### Usage

##### Basic

```tsx
import {
  Status,
  StatusIndicator,
  StatusLabel,
} from "@/components/kibo-ui/status"

export function Example() {
  return (
    <Status status="online">
      <StatusIndicator />
      <StatusLabel />
    </Status>
  )
}
```

##### All Statuses

Display each status variant side by side.

```tsx
import {
  Status,
  StatusIndicator,
  StatusLabel,
} from "@/components/kibo-ui/status"

export function Example() {
  return (
    <div className="flex gap-2">
      <Status status="online">
        <StatusIndicator />
        <StatusLabel />
      </Status>

      <Status status="offline">
        <StatusIndicator />
        <StatusLabel />
      </Status>

      <Status status="maintenance">
        <StatusIndicator />
        <StatusLabel />
      </Status>

      <Status status="degraded">
        <StatusIndicator />
        <StatusLabel />
      </Status>
    </div>
  )
}
```

##### Custom Label and Styling

Override the default label text and apply custom styles.

```tsx
import {
  Status,
  StatusIndicator,
  StatusLabel,
} from "@/components/kibo-ui/status"

export function Example() {
  return (
    <Status
      className="gap-4 rounded-full px-6 py-2 text-sm"
      status="online"
      variant="outline"
    >
      <StatusIndicator />
      <StatusLabel className="font-mono">
        Fully operational
      </StatusLabel>
    </Status>
  )
}
```

##### Indicator Only

Render the pulsing indicator without a text label.

```tsx
import {
  Status,
  StatusIndicator,
} from "@/components/kibo-ui/status"

export function Example() {
  return (
    <Status status="degraded">
      <StatusIndicator />
    </Status>
  )
}
```
