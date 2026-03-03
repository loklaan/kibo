### Mini Calendar

> A composable mini calendar component for picking dates close to today.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/mini-calendar.json"
```

#### Dependencies

External packages installed automatically:
- `date-fns` — date arithmetic and formatting
- `@radix-ui/react-use-controllable-state` — controlled/uncontrolled state management
- `lucide-react` — chevron icons for navigation
- `radix-ui` — slot primitive for `asChild` support

#### Anatomy

```tsx
import {
  MiniCalendar,
  MiniCalendarNavigation,
  MiniCalendarDays,
  MiniCalendarDay,
} from "@/components/kibo-ui/mini-calendar"
```

| Component | Description |
|-----------|-------------|
| `MiniCalendar` | Root provider. Manages selected date and navigation state via context. |
| `MiniCalendarNavigation` | Prev/next button that shifts the visible date range. |
| `MiniCalendarDays` | Container that iterates over consecutive dates using a render function. |
| `MiniCalendarDay` | Individual day button displaying the month abbreviation and day number. |

#### Props

**MiniCalendar**

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `value` | `Date` | — | Selected date (controlled). |
| `defaultValue` | `Date` | — | Initial selected date (uncontrolled). |
| `onValueChange` | `(date: Date \| undefined) => void` | — | Called when the selected date changes. |
| `startDate` | `Date` | — | First visible date (controlled). |
| `defaultStartDate` | `Date` | `new Date()` | Initial first visible date (uncontrolled). |
| `onStartDateChange` | `(date: Date \| undefined) => void` | — | Called when the start date changes via navigation. |
| `days` | `number` | `5` | Number of consecutive days to display. |

**MiniCalendarNavigation**

Extends `HTMLButtonElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `direction` | `"prev" \| "next"` | — | Navigation direction. |
| `asChild` | `boolean` | `false` | Render as the child element instead of the default button. |

**MiniCalendarDays**

Extends `HTMLDivElement` attributes (except `children`).

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `children` | `(date: Date) => ReactNode` | — | Render function called for each date in the range. |

**MiniCalendarDay**

Extends `Button` component props.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `date` | `Date` | — | The date this day button represents. |

#### Usage

##### Basic

```tsx
"use client"

import {
  MiniCalendar,
  MiniCalendarDay,
  MiniCalendarDays,
  MiniCalendarNavigation,
} from "@/components/kibo-ui/mini-calendar"

export function Example() {
  return (
    <MiniCalendar>
      <MiniCalendarNavigation direction="prev" />
      <MiniCalendarDays>
        {(date) => (
          <MiniCalendarDay
            date={date}
            key={date.toISOString()}
          />
        )}
      </MiniCalendarDays>
      <MiniCalendarNavigation direction="next" />
    </MiniCalendar>
  )
}
```

##### Controlled

Manage the selected date externally with `value` and `onValueChange`.

```tsx
"use client"

import {
  MiniCalendar,
  MiniCalendarDay,
  MiniCalendarDays,
  MiniCalendarNavigation,
} from "@/components/kibo-ui/mini-calendar"
import { useState } from "react"

export function Example() {
  const [selectedDate, setSelectedDate] = useState<
    Date | undefined
  >(undefined)

  return (
    <div className="space-y-4">
      <MiniCalendar
        value={selectedDate}
        onValueChange={setSelectedDate}
      >
        <MiniCalendarNavigation direction="prev" />
        <MiniCalendarDays>
          {(date) => (
            <MiniCalendarDay
              date={date}
              key={date.toISOString()}
            />
          )}
        </MiniCalendarDays>
        <MiniCalendarNavigation direction="next" />
      </MiniCalendar>

      {selectedDate && (
        <p className="text-muted-foreground text-sm">
          Selected:{" "}
          {selectedDate.toLocaleDateString("en-US", {
            weekday: "long",
            year: "numeric",
            month: "long",
            day: "numeric",
          })}
        </p>
      )}
    </div>
  )
}
```

##### Custom Days Count

Display more days by setting the `days` prop.

```tsx
"use client"

import {
  MiniCalendar,
  MiniCalendarDay,
  MiniCalendarDays,
  MiniCalendarNavigation,
} from "@/components/kibo-ui/mini-calendar"

export function Example() {
  return (
    <MiniCalendar days={7}>
      <MiniCalendarNavigation direction="prev" />
      <MiniCalendarDays>
        {(date) => (
          <MiniCalendarDay
            date={date}
            key={date.toISOString()}
          />
        )}
      </MiniCalendarDays>
      <MiniCalendarNavigation direction="next" />
    </MiniCalendar>
  )
}
```

##### Custom Layout

Use `asChild` on `MiniCalendarNavigation` to render custom
navigation buttons, and pass `className` to adjust styling.

```tsx
"use client"

import {
  MiniCalendar,
  MiniCalendarDay,
  MiniCalendarDays,
  MiniCalendarNavigation,
} from "@/components/kibo-ui/mini-calendar"
import { Button } from "@/components/ui/button"
import { ArrowLeftIcon, ArrowRightIcon } from "lucide-react"

export function Example() {
  return (
    <MiniCalendar className="bg-card p-4 shadow-lg">
      <div className="flex items-center gap-4">
        <MiniCalendarNavigation asChild direction="prev">
          <Button size="icon" variant="outline">
            <ArrowLeftIcon className="size-4" />
          </Button>
        </MiniCalendarNavigation>

        <MiniCalendarDays className="gap-2">
          {(date) => (
            <MiniCalendarDay
              date={date}
              key={date.toISOString()}
            />
          )}
        </MiniCalendarDays>

        <MiniCalendarNavigation asChild direction="next">
          <Button size="icon" variant="outline">
            <ArrowRightIcon className="size-4" />
          </Button>
        </MiniCalendarNavigation>
      </div>
    </MiniCalendar>
  )
}
```
