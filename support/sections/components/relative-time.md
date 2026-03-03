### Relative Time

> A component that displays time in various timezones.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/relative-time.json"
```

#### Dependencies

External packages installed automatically:
- `@radix-ui/react-use-controllable-state` — controlled/uncontrolled state management

#### Anatomy

```tsx
import {
  RelativeTime,
  RelativeTimeZone,
  RelativeTimeZoneDate,
  RelativeTimeZoneDisplay,
  RelativeTimeZoneLabel,
} from "@/components/kibo-ui/relative-time"
```

| Component | Description |
|-----------|-------------|
| `RelativeTime` | Root provider. Manages time state and passes it to descendants via context. Auto-updates every second when uncontrolled. |
| `RelativeTimeZone` | Groups date, time, and label displays for a single timezone. |
| `RelativeTimeZoneDate` | Renders the formatted date for the parent zone. |
| `RelativeTimeZoneDisplay` | Renders the formatted time for the parent zone. |
| `RelativeTimeZoneLabel` | Displays a short label badge for the timezone. |

#### Props

**RelativeTime**

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `time` | `Date` | — | Controlled time value. When set, auto-update is disabled. |
| `defaultTime` | `Date` | `new Date()` | Initial time for uncontrolled mode. |
| `onTimeChange` | `(time: Date) => void` | — | Called when the internal time updates. |
| `dateFormatOptions` | `Intl.DateTimeFormatOptions` | `{ dateStyle: "long" }` | Format options applied to all `RelativeTimeZoneDate` descendants. |
| `timeFormatOptions` | `Intl.DateTimeFormatOptions` | `{ hour: "2-digit", minute: "2-digit", second: "2-digit" }` | Format options applied to all `RelativeTimeZoneDisplay` descendants. |

**RelativeTimeZone**

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `zone` | `string` | — | IANA timezone identifier (e.g. `"America/New_York"`). Required. |

**RelativeTimeZoneDate**

Accepts standard `HTMLDivElement` attributes.

**RelativeTimeZoneDisplay**

Accepts standard `HTMLDivElement` attributes.

**RelativeTimeZoneLabel**

Accepts standard `HTMLDivElement` attributes.

#### Usage

##### Basic

```tsx
"use client"

import {
  RelativeTime,
  RelativeTimeZone,
  RelativeTimeZoneDate,
  RelativeTimeZoneDisplay,
  RelativeTimeZoneLabel,
} from "@/components/kibo-ui/relative-time"

const timezones = [
  { label: "EST", zone: "America/New_York" },
  { label: "GMT", zone: "Europe/London" },
  { label: "JST", zone: "Asia/Tokyo" },
]

export function Example() {
  return (
    <RelativeTime>
      {timezones.map(({ zone, label }) => (
        <RelativeTimeZone key={zone} zone={zone}>
          <RelativeTimeZoneLabel>
            {label}
          </RelativeTimeZoneLabel>
          <RelativeTimeZoneDate />
          <RelativeTimeZoneDisplay />
        </RelativeTimeZone>
      ))}
    </RelativeTime>
  )
}
```

##### Custom Date Format

Pass `dateFormatOptions` to `RelativeTime` to change the date
format across all zones. Uses `Intl.DateTimeFormatOptions`.

```tsx
"use client"

import {
  RelativeTime,
  RelativeTimeZone,
  RelativeTimeZoneDate,
  RelativeTimeZoneDisplay,
  RelativeTimeZoneLabel,
} from "@/components/kibo-ui/relative-time"

const timezones = [
  { label: "EST", zone: "America/New_York" },
  { label: "GMT", zone: "Europe/London" },
  { label: "JST", zone: "Asia/Tokyo" },
]

export function Example() {
  return (
    <RelativeTime
      dateFormatOptions={{ dateStyle: "full" }}
    >
      {timezones.map(({ zone, label }) => (
        <RelativeTimeZone key={zone} zone={zone}>
          <RelativeTimeZoneLabel>
            {label}
          </RelativeTimeZoneLabel>
          <RelativeTimeZoneDate />
          <RelativeTimeZoneDisplay />
        </RelativeTimeZone>
      ))}
    </RelativeTime>
  )
}
```

##### Custom Time Format

Pass `timeFormatOptions` to `RelativeTime` to change the time
format. This example omits seconds.

```tsx
"use client"

import {
  RelativeTime,
  RelativeTimeZone,
  RelativeTimeZoneDate,
  RelativeTimeZoneDisplay,
  RelativeTimeZoneLabel,
} from "@/components/kibo-ui/relative-time"

const timezones = [
  { label: "EST", zone: "America/New_York" },
  { label: "GMT", zone: "Europe/London" },
  { label: "JST", zone: "Asia/Tokyo" },
]

export function Example() {
  return (
    <RelativeTime
      timeFormatOptions={{
        hour: "2-digit",
        minute: "2-digit",
      }}
    >
      {timezones.map(({ zone, label }) => (
        <RelativeTimeZone key={zone} zone={zone}>
          <RelativeTimeZoneLabel>
            {label}
          </RelativeTimeZoneLabel>
          <RelativeTimeZoneDate />
          <RelativeTimeZoneDisplay />
        </RelativeTimeZone>
      ))}
    </RelativeTime>
  )
}
```

##### Controlled Time

Manage the time externally by passing `time` and
`onTimeChange`. When `time` is provided, the component
disables its internal auto-update interval.

```tsx
"use client"

import {
  RelativeTime,
  RelativeTimeZone,
  RelativeTimeZoneDate,
  RelativeTimeZoneDisplay,
  RelativeTimeZoneLabel,
} from "@/components/kibo-ui/relative-time"
import { useEffect, useState } from "react"

const timezones = [
  { label: "EST", zone: "America/New_York" },
  { label: "GMT", zone: "Europe/London" },
  { label: "JST", zone: "Asia/Tokyo" },
]

export function Example() {
  const [time, setTime] = useState(new Date())

  useEffect(() => {
    const interval = setInterval(() => {
      setTime(new Date())
    }, 1000)
    return () => clearInterval(interval)
  }, [])

  return (
    <RelativeTime time={time} onTimeChange={setTime}>
      {timezones.map(({ zone, label }) => (
        <RelativeTimeZone key={zone} zone={zone}>
          <RelativeTimeZoneLabel>
            {label}
          </RelativeTimeZoneLabel>
          <RelativeTimeZoneDate />
          <RelativeTimeZoneDisplay />
        </RelativeTimeZone>
      ))}
    </RelativeTime>
  )
}
```
