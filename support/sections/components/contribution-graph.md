### Contribution Graph

> A GitHub-style contribution graph component that displays activity levels over time.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/contribution-graph.json"
```

#### Dependencies

External packages installed automatically:
- `date-fns` — date manipulation and interval generation

#### Anatomy

```tsx
import {
  ContributionGraph,
  ContributionGraphBlock,
  ContributionGraphCalendar,
  ContributionGraphFooter,
  ContributionGraphTotalCount,
  ContributionGraphLegend,
} from "@/components/kibo-ui/contribution-graph"
```

| Component | Description |
|-----------|-------------|
| `ContributionGraph` | Root provider. Wraps all child components and supplies context. |
| `ContributionGraphCalendar` | SVG grid that renders day blocks via a render function. |
| `ContributionGraphBlock` | Individual day cell rendered as an SVG `<rect>`. |
| `ContributionGraphFooter` | Footer container for the total count and legend. |
| `ContributionGraphTotalCount` | Displays the total activity count for the year. |
| `ContributionGraphLegend` | Displays the activity level color scale. |

| Type | Description |
|------|-------------|
| `Activity` | Shape of a single day's data passed in the `data` array. |
| `Labels` | Customizable label strings for months, weekdays, and legend. |

```ts
type Activity = {
  date: string
  count: number
  level: number
}

type Labels = {
  months?: string[]
  weekdays?: string[]
  totalCount?: string
  legend?: {
    less?: string
    more?: string
  }
}
```

#### Props

**ContributionGraph**

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `data` | `Activity[]` | — | Activity data for each day. |
| `blockMargin` | `number` | `4` | Pixel gap between blocks. |
| `blockRadius` | `number` | `2` | Border radius of each block. |
| `blockSize` | `number` | `12` | Width and height of each block in pixels. |
| `fontSize` | `number` | `14` | Font size for month labels and footer text. |
| `labels` | `Labels` | See defaults | Custom label strings. |
| `maxLevel` | `number` | `4` | Maximum activity level (minimum is 1). |
| `totalCount` | `number` | Sum of all counts | Override the displayed total count. |
| `weekStart` | `Day` | `0` | Day the week starts on (0 = Sunday, 1 = Monday, etc.). `Day` is from `date-fns`. |
| `children` | `ReactNode` | — | Child components. |

**ContributionGraphCalendar**

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `hideMonthLabels` | `boolean` | `false` | Hides the month labels above the grid. |
| `children` | `(props: { activity: Activity; dayIndex: number; weekIndex: number }) => ReactNode` | — | Render function called for each day. |

**ContributionGraphBlock**

Extends `SVGRectElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `activity` | `Activity` | — | The activity data for this day. |
| `dayIndex` | `number` | — | Row index (0-6) of this day in the week. |
| `weekIndex` | `number` | — | Column index of this day's week. |

**ContributionGraphFooter**

Accepts standard `HTMLDivElement` attributes.

**ContributionGraphTotalCount**

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `children` | `(props: { totalCount: number; year: number }) => ReactNode` | — | Optional render function for custom total count display. |

**ContributionGraphLegend**

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `children` | `(props: { level: number }) => ReactNode` | — | Optional render function for custom legend swatches. |

#### Usage

##### Basic

```tsx
"use client"

import {
  ContributionGraph,
  ContributionGraphBlock,
  ContributionGraphCalendar,
  ContributionGraphFooter,
  ContributionGraphTotalCount,
  ContributionGraphLegend,
} from "@/components/kibo-ui/contribution-graph"

const data = [
  { date: "2025-01-01", count: 0, level: 0 },
  { date: "2025-01-02", count: 3, level: 1 },
  { date: "2025-01-03", count: 7, level: 2 },
  { date: "2025-01-04", count: 12, level: 3 },
  { date: "2025-01-05", count: 18, level: 4 },
  { date: "2025-03-15", count: 5, level: 2 },
]

export function Example() {
  return (
    <ContributionGraph data={data}>
      <ContributionGraphCalendar>
        {({ activity, dayIndex, weekIndex }) => (
          <ContributionGraphBlock
            activity={activity}
            dayIndex={dayIndex}
            weekIndex={weekIndex}
          />
        )}
      </ContributionGraphCalendar>
      <ContributionGraphFooter>
        <ContributionGraphTotalCount />
        <ContributionGraphLegend />
      </ContributionGraphFooter>
    </ContributionGraph>
  )
}
```

##### Minimal

Hide month labels and footer for a compact display.

```tsx
"use client"

import {
  ContributionGraph,
  ContributionGraphBlock,
  ContributionGraphCalendar,
} from "@/components/kibo-ui/contribution-graph"

const data = [
  { date: "2025-01-01", count: 0, level: 0 },
  { date: "2025-01-02", count: 4, level: 1 },
  { date: "2025-02-10", count: 9, level: 3 },
  { date: "2025-03-20", count: 15, level: 4 },
]

export function Example() {
  return (
    <ContributionGraph data={data}>
      <ContributionGraphCalendar hideMonthLabels>
        {({ activity, dayIndex, weekIndex }) => (
          <ContributionGraphBlock
            activity={activity}
            dayIndex={dayIndex}
            weekIndex={weekIndex}
          />
        )}
      </ContributionGraphCalendar>
    </ContributionGraph>
  )
}
```

##### Custom Size

Adjust block size, margin, and font size.

```tsx
"use client"

import {
  ContributionGraph,
  ContributionGraphBlock,
  ContributionGraphCalendar,
  ContributionGraphFooter,
  ContributionGraphTotalCount,
  ContributionGraphLegend,
} from "@/components/kibo-ui/contribution-graph"

const data = [
  { date: "2025-01-01", count: 0, level: 0 },
  { date: "2025-01-02", count: 2, level: 1 },
  { date: "2025-01-03", count: 8, level: 3 },
  { date: "2025-02-01", count: 14, level: 4 },
]

export function Example() {
  return (
    <ContributionGraph
      blockMargin={2}
      blockSize={20}
      data={data}
      fontSize={16}
    >
      <ContributionGraphCalendar>
        {({ activity, dayIndex, weekIndex }) => (
          <ContributionGraphBlock
            activity={activity}
            dayIndex={dayIndex}
            weekIndex={weekIndex}
          />
        )}
      </ContributionGraphCalendar>
      <ContributionGraphFooter>
        <ContributionGraphTotalCount />
        <ContributionGraphLegend />
      </ContributionGraphFooter>
    </ContributionGraph>
  )
}
```

##### Custom GitHub Theme

Override block colors using `className` with `data-[level]` selectors.

```tsx
"use client"

import {
  ContributionGraph,
  ContributionGraphBlock,
  ContributionGraphCalendar,
  ContributionGraphFooter,
} from "@/components/kibo-ui/contribution-graph"
import { cn } from "@/lib/utils"

const data = [
  { date: "2025-01-01", count: 0, level: 0 },
  { date: "2025-01-02", count: 3, level: 1 },
  { date: "2025-01-03", count: 7, level: 2 },
  { date: "2025-01-04", count: 12, level: 3 },
  { date: "2025-01-05", count: 18, level: 4 },
  { date: "2025-03-01", count: 5, level: 2 },
]

export function Example() {
  return (
    <ContributionGraph data={data}>
      <ContributionGraphCalendar>
        {({ activity, dayIndex, weekIndex }) => (
          <ContributionGraphBlock
            activity={activity}
            className={cn(
              'data-[level="0"]:fill-[#ebedf0]',
              'dark:data-[level="0"]:fill-[#161b22]',
              'data-[level="1"]:fill-[#9be9a8]',
              'dark:data-[level="1"]:fill-[#0e4429]',
              'data-[level="2"]:fill-[#40c463]',
              'dark:data-[level="2"]:fill-[#006d32]',
              'data-[level="3"]:fill-[#30a14e]',
              'dark:data-[level="3"]:fill-[#26a641]',
              'data-[level="4"]:fill-[#216e39]',
              'dark:data-[level="4"]:fill-[#39d353]',
            )}
            dayIndex={dayIndex}
            weekIndex={weekIndex}
          />
        )}
      </ContributionGraphCalendar>
      <ContributionGraphFooter />
    </ContributionGraph>
  )
}
```

##### Custom Footer

Use render functions on `ContributionGraphTotalCount` and
`ContributionGraphLegend` to customize the footer.

```tsx
"use client"

import {
  ContributionGraph,
  ContributionGraphBlock,
  ContributionGraphCalendar,
  ContributionGraphFooter,
  ContributionGraphLegend,
  ContributionGraphTotalCount,
} from "@/components/kibo-ui/contribution-graph"

const data = [
  { date: "2025-01-01", count: 0, level: 0 },
  { date: "2025-01-02", count: 3, level: 1 },
  { date: "2025-01-03", count: 7, level: 2 },
  { date: "2025-01-04", count: 12, level: 3 },
  { date: "2025-01-05", count: 18, level: 4 },
]

export function Example() {
  return (
    <ContributionGraph data={data}>
      <ContributionGraphCalendar>
        {({ activity, dayIndex, weekIndex }) => (
          <ContributionGraphBlock
            activity={activity}
            dayIndex={dayIndex}
            weekIndex={weekIndex}
          />
        )}
      </ContributionGraphCalendar>
      <ContributionGraphFooter>
        <ContributionGraphTotalCount>
          {({ totalCount, year }) => (
            <span className="text-sm text-muted-foreground">
              {totalCount.toLocaleString()} contributions
              {" "}in {year}
            </span>
          )}
        </ContributionGraphTotalCount>
        <ContributionGraphLegend>
          {({ level }) => (
            <div
              className={`h-3 w-3 rounded-sm border border-border ${
                level === 0 ? "bg-muted" : ""
              } ${level === 1 ? "bg-emerald-200" : ""} ${
                level === 2 ? "bg-emerald-400" : ""
              } ${level === 3 ? "bg-emerald-600" : ""} ${
                level === 4 ? "bg-emerald-800" : ""
              }`}
              data-level={level}
            />
          )}
        </ContributionGraphLegend>
      </ContributionGraphFooter>
    </ContributionGraph>
  )
}
```
