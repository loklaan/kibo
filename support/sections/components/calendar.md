### Calendar

> The calendar view displays features on a grid calendar, showing the end date of each feature and grouping features by day.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/calendar.json"
```

#### Dependencies

External packages installed automatically:
- `date-fns` — date arithmetic and comparison utilities
- `jotai` — atomic state management for month/year state
- `lucide-react` — icon primitives

#### Anatomy

```tsx
import {
  CalendarProvider,
  CalendarDate,
  CalendarDatePicker,
  CalendarMonthPicker,
  CalendarYearPicker,
  CalendarDatePagination,
  CalendarHeader,
  CalendarBody,
  CalendarItem,
} from "@/components/kibo-ui/calendar"
```

| Component | Description |
|-----------|-------------|
| `CalendarProvider` | Root provider. Supplies locale and start-day context to all children. |
| `CalendarDate` | Toolbar row. Lays out the date picker and pagination controls. |
| `CalendarDatePicker` | Container for month and year picker controls. |
| `CalendarMonthPicker` | Combobox dropdown for selecting the displayed month. |
| `CalendarYearPicker` | Combobox dropdown for selecting the displayed year. |
| `CalendarDatePagination` | Previous/next month navigation buttons. |
| `CalendarHeader` | Weekday header row (Sun, Mon, Tue, etc.). |
| `CalendarBody` | Grid body that renders day cells and maps features to their end dates. Accepts a render function as `children`. |
| `CalendarItem` | Renders a single feature inside a day cell with a color dot and truncated name. |

| Hook | Description |
|------|-------------|
| `useCalendarMonth` | Returns `[month, setMonth]` for the currently displayed month (0–11). |
| `useCalendarYear` | Returns `[year, setYear]` for the currently displayed year. |

| Type | Description |
|------|-------------|
| `Feature` | Shape of a single feature passed to the `features` prop. |
| `Status` | Shape of a feature's status, used for color coding. |
| `CalendarState` | Object with `month` (0–11) and `year` fields. |

```ts
type Status = {
  id: string
  name: string
  color: string
}

type Feature = {
  id: string
  name: string
  startAt: Date
  endAt: Date
  status: Status
}

type CalendarState = {
  month: 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11
  year: number
}
```

| Utility | Description |
|---------|-------------|
| `monthsForLocale(locale, monthFormat?)` | Returns an array of 12 month names for the given locale. |
| `daysForLocale(locale, startDay)` | Returns an array of 7 weekday abbreviations starting from the given day. |

#### Props

**CalendarProvider**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `locale` | `Intl.LocalesArgument` | `"en-US"` | Locale for month and weekday names. |
| `startDay` | `number` | `0` | First day of the week (0 = Sunday, 1 = Monday, etc.). |
| `className` | `string` | `undefined` | Class name for the root container. |

**CalendarDate**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `children` | `ReactNode` | — | Toolbar content (date picker, pagination). |

**CalendarDatePicker**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `className` | `string` | `undefined` | Class name for the picker container. |
| `children` | `ReactNode` | — | Month and year picker components. |

**CalendarMonthPicker**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `className` | `string` | `undefined` | Class name for the month combobox trigger. |

**CalendarYearPicker**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `className` | `string` | `undefined` | Class name for the year combobox trigger. |
| `start` | `number` | — | First year in the selectable range. |
| `end` | `number` | — | Last year in the selectable range. |

**CalendarDatePagination**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `className` | `string` | `undefined` | Class name for the pagination container. |

**CalendarHeader**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `className` | `string` | `undefined` | Class name for the weekday header row. |

**CalendarBody**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `features` | `Feature[]` | — | Array of features to display on the calendar. |
| `children` | `(props: { feature: Feature }) => ReactNode` | — | Render function called for each feature in a day cell. |

**CalendarItem**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `feature` | `Feature` | — | The feature to render. |
| `className` | `string` | `undefined` | Class name for the item container. |

#### Usage

##### Basic

Renders a calendar grid without date picker controls.

```tsx
"use client"

import {
  CalendarProvider,
  CalendarHeader,
  CalendarBody,
  CalendarItem,
} from "@/components/kibo-ui/calendar"
import type { Feature } from "@/components/kibo-ui/calendar"

const statuses = [
  { id: "1", name: "Planned", color: "#6B7280" },
  { id: "2", name: "In Progress", color: "#F59E0B" },
  { id: "3", name: "Done", color: "#10B981" },
]

const features: Feature[] = [
  {
    id: "a",
    name: "Design system audit",
    startAt: new Date(2026, 2, 1),
    endAt: new Date(2026, 2, 5),
    status: statuses[0],
  },
  {
    id: "b",
    name: "API integration",
    startAt: new Date(2026, 2, 3),
    endAt: new Date(2026, 2, 12),
    status: statuses[1],
  },
  {
    id: "c",
    name: "Launch landing page",
    startAt: new Date(2026, 2, 10),
    endAt: new Date(2026, 2, 20),
    status: statuses[2],
  },
]

export function Example() {
  return (
    <CalendarProvider>
      <CalendarHeader />
      <CalendarBody features={features}>
        {({ feature }) => (
          <CalendarItem
            feature={feature}
            key={feature.id}
          />
        )}
      </CalendarBody>
    </CalendarProvider>
  )
}
```

##### With Date Picker and Pagination

Adds month/year selection and previous/next navigation.

```tsx
"use client"

import {
  CalendarProvider,
  CalendarDate,
  CalendarDatePicker,
  CalendarMonthPicker,
  CalendarYearPicker,
  CalendarDatePagination,
  CalendarHeader,
  CalendarBody,
  CalendarItem,
} from "@/components/kibo-ui/calendar"
import type { Feature } from "@/components/kibo-ui/calendar"

const statuses = [
  { id: "1", name: "Planned", color: "#6B7280" },
  { id: "2", name: "In Progress", color: "#F59E0B" },
  { id: "3", name: "Done", color: "#10B981" },
]

const features: Feature[] = [
  {
    id: "a",
    name: "Design system audit",
    startAt: new Date(2026, 0, 15),
    endAt: new Date(2026, 2, 5),
    status: statuses[0],
  },
  {
    id: "b",
    name: "API integration",
    startAt: new Date(2026, 1, 1),
    endAt: new Date(2026, 2, 12),
    status: statuses[1],
  },
  {
    id: "c",
    name: "Launch landing page",
    startAt: new Date(2026, 2, 10),
    endAt: new Date(2026, 3, 20),
    status: statuses[2],
  },
]

export function Example() {
  return (
    <CalendarProvider>
      <CalendarDate>
        <CalendarDatePicker>
          <CalendarMonthPicker />
          <CalendarYearPicker start={2025} end={2027} />
        </CalendarDatePicker>
        <CalendarDatePagination />
      </CalendarDate>
      <CalendarHeader />
      <CalendarBody features={features}>
        {({ feature }) => (
          <CalendarItem
            feature={feature}
            key={feature.id}
          />
        )}
      </CalendarBody>
    </CalendarProvider>
  )
}
```

##### Custom Locale and Start Day

Configures the calendar for a Monday-start week with German locale.

```tsx
"use client"

import {
  CalendarProvider,
  CalendarDate,
  CalendarDatePicker,
  CalendarMonthPicker,
  CalendarYearPicker,
  CalendarDatePagination,
  CalendarHeader,
  CalendarBody,
  CalendarItem,
} from "@/components/kibo-ui/calendar"
import type { Feature } from "@/components/kibo-ui/calendar"

const statuses = [
  { id: "1", name: "Geplant", color: "#6B7280" },
  { id: "2", name: "In Bearbeitung", color: "#F59E0B" },
]

const features: Feature[] = [
  {
    id: "a",
    name: "Systemprüfung",
    startAt: new Date(2026, 2, 1),
    endAt: new Date(2026, 2, 10),
    status: statuses[0],
  },
  {
    id: "b",
    name: "Dokumentation",
    startAt: new Date(2026, 2, 5),
    endAt: new Date(2026, 2, 18),
    status: statuses[1],
  },
]

export function Example() {
  return (
    <CalendarProvider locale="de-DE" startDay={1}>
      <CalendarDate>
        <CalendarDatePicker>
          <CalendarMonthPicker />
          <CalendarYearPicker start={2025} end={2027} />
        </CalendarDatePicker>
        <CalendarDatePagination />
      </CalendarDate>
      <CalendarHeader />
      <CalendarBody features={features}>
        {({ feature }) => (
          <CalendarItem
            feature={feature}
            key={feature.id}
          />
        )}
      </CalendarBody>
    </CalendarProvider>
  )
}
```

##### Programmatic Month and Year Control

Uses the `useCalendarMonth` and `useCalendarYear` hooks to read and set the displayed period from outside the calendar tree.

```tsx
"use client"

import {
  CalendarProvider,
  CalendarHeader,
  CalendarBody,
  CalendarItem,
  useCalendarMonth,
  useCalendarYear,
} from "@/components/kibo-ui/calendar"
import type {
  Feature,
  CalendarState,
} from "@/components/kibo-ui/calendar"

const statuses = [
  { id: "1", name: "Done", color: "#10B981" },
]

const features: Feature[] = [
  {
    id: "a",
    name: "Q1 Review",
    startAt: new Date(2026, 0, 1),
    endAt: new Date(2026, 2, 15),
    status: statuses[0],
  },
]

function JumpToToday() {
  const [, setMonth] = useCalendarMonth()
  const [, setYear] = useCalendarYear()

  const handleClick = () => {
    const now = new Date()
    setMonth(
      now.getMonth() as CalendarState["month"]
    )
    setYear(now.getFullYear())
  }

  return (
    <button onClick={handleClick}>
      Jump to today
    </button>
  )
}

export function Example() {
  return (
    <CalendarProvider>
      <JumpToToday />
      <CalendarHeader />
      <CalendarBody features={features}>
        {({ feature }) => (
          <CalendarItem
            feature={feature}
            key={feature.id}
          />
        )}
      </CalendarBody>
    </CalendarProvider>
  )
}
```
