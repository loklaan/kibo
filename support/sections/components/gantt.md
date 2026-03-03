### Gantt

> A Gantt chart for visualizing project schedules and tracking task progress over time.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/gantt.json"
```

#### Dependencies

External packages installed automatically:
- `@dnd-kit/core` and `@dnd-kit/modifiers` — drag-and-drop for moving and resizing feature bars
- `@uidotdev/usehooks` — mouse position and scroll tracking hooks
- `date-fns` — date arithmetic and formatting
- `jotai` — shared atom state for drag and scroll position
- `lodash.throttle` — throttled scroll handler
- `lucide-react` — icons for add and remove actions

#### Anatomy

```tsx
import {
  GanttProvider,
  GanttHeader,
  GanttSidebar,
  GanttSidebarGroup,
  GanttSidebarItem,
  GanttTimeline,
  GanttFeatureList,
  GanttFeatureListGroup,
  GanttFeatureItem,
  GanttFeatureRow,
  GanttMarker,
  GanttToday,
  GanttCreateMarkerTrigger,
  useGanttDragging,
  useGanttScrollX,
} from "@/components/kibo-ui/gantt"
```

| Component | Description |
|-----------|-------------|
| `GanttProvider` | Root provider. Manages timeline context, zoom, range, and scroll state. |
| `GanttHeader` | Renders time-period column headers (daily, monthly, or quarterly). |
| `GanttSidebar` | Left panel listing features with names, status dots, and durations. |
| `GanttSidebarGroup` | Groups sidebar items under a named heading. |
| `GanttSidebarItem` | Individual feature entry in the sidebar. Clicking scrolls to the feature. |
| `GanttTimeline` | Scrollable content area containing headers, features, and markers. |
| `GanttFeatureList` | Container for all feature rows, positioned below the header. |
| `GanttFeatureListGroup` | Groups feature rows with top padding matching the sidebar group header. |
| `GanttFeatureItem` | Draggable and resizable bar representing a single feature on the timeline. |
| `GanttFeatureRow` | Renders multiple features in a single row with automatic sub-row stacking for overlapping items. |
| `GanttMarker` | Vertical line marker at a specific date with a label. Right-click to remove. |
| `GanttToday` | Vertical line highlighting the current date. |
| `GanttCreateMarkerTrigger` | Invisible overlay that shows a date tooltip on hover and creates a marker on click. |

| Hook | Description |
|------|-------------|
| `useGanttDragging` | Returns `[isDragging, setIsDragging]` for the global drag state. |
| `useGanttScrollX` | Returns `[scrollX, setScrollX]` for the horizontal scroll position. |

| Type | Description |
|------|-------------|
| `GanttFeature` | Shape of a feature passed to `GanttFeatureItem` and `GanttSidebarItem`. |
| `GanttStatus` | Status object with id, name, and color used by `GanttFeature`. |
| `Range` | Time-period granularity: `"daily"`, `"monthly"`, or `"quarterly"`. |

```ts
type GanttStatus = {
  id: string
  name: string
  color: string
}

type GanttFeature = {
  id: string
  name: string
  startAt: Date
  endAt: Date
  status: GanttStatus
  lane?: string
}

type Range = "daily" | "monthly" | "quarterly"
```

#### Props

**GanttProvider**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `range` | `Range` | `"monthly"` | Time-period granularity for columns. |
| `zoom` | `number` | `100` | Zoom percentage controlling column width. |
| `onAddItem` | `(date: Date) => void` | — | Called when clicking the add-feature helper in a column. |
| `children` | `ReactNode` | — | Sidebar and timeline content. |
| `className` | `string` | — | Additional CSS classes on the root container. |

**GanttHeader**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `className` | `string` | — | Additional CSS classes. |

**GanttSidebar**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `children` | `ReactNode` | — | Sidebar groups and items. |
| `className` | `string` | — | Additional CSS classes. |

**GanttSidebarGroup**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `name` | `string` | — | Group heading text. |
| `children` | `ReactNode` | — | `GanttSidebarItem` elements. |
| `className` | `string` | — | Additional CSS classes. |

**GanttSidebarItem**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `feature` | `GanttFeature` | — | Feature to display. |
| `onSelectItem` | `(id: string) => void` | — | Called when the item is clicked. Also scrolls the timeline to the feature. |
| `className` | `string` | — | Additional CSS classes. |

**GanttTimeline**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `children` | `ReactNode` | — | Header, feature list, markers, and today indicator. |
| `className` | `string` | — | Additional CSS classes. |

**GanttFeatureList**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `children` | `ReactNode` | — | `GanttFeatureListGroup` elements. |
| `className` | `string` | — | Additional CSS classes. |

**GanttFeatureListGroup**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `children` | `ReactNode` | — | `GanttFeatureItem` or `GanttFeatureRow` elements. |
| `className` | `string` | — | Additional CSS classes. |

**GanttFeatureItem**

Accepts all `GanttFeature` fields as spread props.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `id` | `string` | — | Feature identifier. |
| `name` | `string` | — | Feature name (shown as default content). |
| `startAt` | `Date` | — | Start date of the feature. |
| `endAt` | `Date` | — | End date of the feature. |
| `status` | `GanttStatus` | — | Status with color used by the sidebar. |
| `onMove` | `(id: string, startAt: Date, endAt: Date \| null) => void` | — | Called after dragging or resizing. Enables drag-and-drop when provided. |
| `children` | `ReactNode` | — | Custom content inside the feature bar. Defaults to the feature name. |
| `className` | `string` | — | Additional CSS classes. |

**GanttFeatureRow**

Renders multiple features in a single row with automatic sub-row stacking when items overlap. Uses a render-prop `children` to customize each feature's content.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `features` | `GanttFeature[]` | — | Array of features to render in this row. |
| `onMove` | `(id: string, startAt: Date, endAt: Date \| null) => void` | — | Called after dragging or resizing any feature in the row. |
| `children` | `(feature: GanttFeature) => ReactNode` | — | Render function receiving each feature. Defaults to the feature name. |
| `className` | `string` | — | Additional CSS classes. |

**GanttMarker**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `id` | `string` | — | Marker identifier. |
| `date` | `Date` | — | Date position on the timeline. |
| `label` | `string` | — | Text displayed on the marker. |
| `onRemove` | `(id: string) => void` | — | Called when "Remove marker" is selected from the context menu. |
| `className` | `string` | — | Additional CSS classes applied to the marker label and line. |

**GanttToday**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `className` | `string` | — | Additional CSS classes. |

**GanttCreateMarkerTrigger**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `onCreateMarker` | `(date: Date) => void` | — | Called with the date at the click position. |
| `className` | `string` | — | Additional CSS classes. |

#### Usage

##### Basic

A read-only Gantt chart with a sidebar, grouped features, markers, and today indicator.

```tsx
"use client"

import {
  GanttProvider,
  GanttHeader,
  GanttSidebar,
  GanttSidebarGroup,
  GanttSidebarItem,
  GanttTimeline,
  GanttFeatureList,
  GanttFeatureListGroup,
  GanttFeatureItem,
  GanttMarker,
  GanttToday,
} from "@/components/kibo-ui/gantt"

const statuses = [
  { id: "s1", name: "Planned", color: "#6B7280" },
  { id: "s2", name: "In Progress", color: "#F59E0B" },
  { id: "s3", name: "Done", color: "#10B981" },
]

const features = [
  {
    id: "f1",
    name: "User authentication",
    startAt: new Date(2026, 0, 10),
    endAt: new Date(2026, 2, 15),
    status: statuses[0],
    group: "Backend",
  },
  {
    id: "f2",
    name: "Dashboard UI",
    startAt: new Date(2026, 1, 1),
    endAt: new Date(2026, 3, 30),
    status: statuses[1],
    group: "Frontend",
  },
  {
    id: "f3",
    name: "API documentation",
    startAt: new Date(2025, 11, 1),
    endAt: new Date(2026, 1, 28),
    status: statuses[2],
    group: "Backend",
  },
]

const markers = [
  {
    id: "m1",
    date: new Date(2026, 2, 1),
    label: "Beta Launch",
  },
]

const grouped: Record<string, typeof features> = {
  Backend: features.filter((f) => f.group === "Backend"),
  Frontend: features.filter((f) => f.group === "Frontend"),
}

export function Example() {
  return (
    <GanttProvider
      className="border"
      range="monthly"
      zoom={100}
    >
      <GanttSidebar>
        {Object.entries(grouped).map(
          ([group, items]) => (
            <GanttSidebarGroup key={group} name={group}>
              {items.map((feature) => (
                <GanttSidebarItem
                  feature={feature}
                  key={feature.id}
                />
              ))}
            </GanttSidebarGroup>
          )
        )}
      </GanttSidebar>
      <GanttTimeline>
        <GanttHeader />
        <GanttFeatureList>
          {Object.entries(grouped).map(
            ([group, items]) => (
              <GanttFeatureListGroup key={group}>
                {items.map((feature) => (
                  <div className="flex" key={feature.id}>
                    <GanttFeatureItem {...feature} />
                  </div>
                ))}
              </GanttFeatureListGroup>
            )
          )}
        </GanttFeatureList>
        {markers.map((marker) => (
          <GanttMarker key={marker.id} {...marker} />
        ))}
        <GanttToday />
      </GanttTimeline>
    </GanttProvider>
  )
}
```

##### Draggable with Callbacks

Enable drag-and-drop by passing `onMove` to `GanttFeatureItem` and handle feature creation, marker creation, and marker removal.

```tsx
"use client"

import { useState } from "react"
import {
  GanttProvider,
  GanttHeader,
  GanttSidebar,
  GanttSidebarGroup,
  GanttSidebarItem,
  GanttTimeline,
  GanttFeatureList,
  GanttFeatureListGroup,
  GanttFeatureItem,
  GanttMarker,
  GanttToday,
  GanttCreateMarkerTrigger,
} from "@/components/kibo-ui/gantt"
import type { GanttFeature } from "@/components/kibo-ui/gantt"

const statuses = [
  { id: "s1", name: "Planned", color: "#6B7280" },
  { id: "s2", name: "In Progress", color: "#F59E0B" },
]

const initialFeatures: GanttFeature[] = [
  {
    id: "f1",
    name: "Design system",
    startAt: new Date(2026, 0, 5),
    endAt: new Date(2026, 2, 20),
    status: statuses[0],
  },
  {
    id: "f2",
    name: "API integration",
    startAt: new Date(2026, 1, 10),
    endAt: new Date(2026, 4, 15),
    status: statuses[1],
  },
]

export function Example() {
  const [features, setFeatures] = useState(initialFeatures)

  const handleMove = (
    id: string,
    startAt: Date,
    endAt: Date | null
  ) => {
    if (!endAt) return
    setFeatures((prev) =>
      prev.map((f) =>
        f.id === id ? { ...f, startAt, endAt } : f
      )
    )
  }

  const handleAddItem = (date: Date) => {
    console.log("Add feature at:", date)
  }

  const handleCreateMarker = (date: Date) => {
    console.log("Create marker at:", date)
  }

  return (
    <GanttProvider
      className="border"
      range="monthly"
      zoom={100}
      onAddItem={handleAddItem}
    >
      <GanttSidebar>
        <GanttSidebarGroup name="Project">
          {features.map((feature) => (
            <GanttSidebarItem
              feature={feature}
              key={feature.id}
            />
          ))}
        </GanttSidebarGroup>
      </GanttSidebar>
      <GanttTimeline>
        <GanttHeader />
        <GanttFeatureList>
          <GanttFeatureListGroup>
            {features.map((feature) => (
              <div className="flex" key={feature.id}>
                <GanttFeatureItem
                  {...feature}
                  onMove={handleMove}
                >
                  <p className="flex-1 truncate text-xs">
                    {feature.name}
                  </p>
                </GanttFeatureItem>
              </div>
            ))}
          </GanttFeatureListGroup>
        </GanttFeatureList>
        <GanttToday />
        <GanttCreateMarkerTrigger
          onCreateMarker={handleCreateMarker}
        />
      </GanttTimeline>
    </GanttProvider>
  )
}
```

##### Without a Sidebar

Omit `GanttSidebar` for a compact timeline-only layout. The provider automatically adjusts when no sidebar is present.

```tsx
"use client"

import {
  GanttProvider,
  GanttHeader,
  GanttTimeline,
  GanttFeatureList,
  GanttFeatureListGroup,
  GanttFeatureItem,
  GanttToday,
} from "@/components/kibo-ui/gantt"

const statuses = [
  { id: "s1", name: "Planned", color: "#6B7280" },
  { id: "s2", name: "Done", color: "#10B981" },
]

const features = [
  {
    id: "f1",
    name: "Research phase",
    startAt: new Date(2026, 0, 1),
    endAt: new Date(2026, 1, 15),
    status: statuses[0],
  },
  {
    id: "f2",
    name: "Implementation",
    startAt: new Date(2026, 1, 16),
    endAt: new Date(2026, 4, 1),
    status: statuses[1],
  },
]

export function Example() {
  return (
    <GanttProvider
      className="border"
      range="monthly"
      zoom={100}
    >
      <GanttTimeline>
        <GanttHeader />
        <GanttFeatureList>
          <GanttFeatureListGroup>
            {features.map((feature) => (
              <div className="flex" key={feature.id}>
                <GanttFeatureItem {...feature} />
              </div>
            ))}
          </GanttFeatureListGroup>
        </GanttFeatureList>
        <GanttToday />
      </GanttTimeline>
    </GanttProvider>
  )
}
```

##### Multiple Items Per Row (Lanes)

Use `GanttFeatureRow` with a render-prop `children` to display multiple features sharing the same row. Overlapping items are automatically stacked into sub-rows.

```tsx
"use client"

import { useState } from "react"
import {
  GanttProvider,
  GanttHeader,
  GanttSidebar,
  GanttSidebarGroup,
  GanttSidebarItem,
  GanttTimeline,
  GanttFeatureList,
  GanttFeatureListGroup,
  GanttFeatureRow,
  GanttToday,
} from "@/components/kibo-ui/gantt"
import type { GanttFeature } from "@/components/kibo-ui/gantt"

const statuses = [
  { id: "s1", name: "Confirmed", color: "#10B981" },
  { id: "s2", name: "Pending", color: "#F59E0B" },
]

const rooms = [
  { id: "r1", name: "Room 101" },
  { id: "r2", name: "Room 102" },
]

const reservations: (GanttFeature & { lane: string })[] = [
  {
    id: "res1",
    name: "Alice - Vacation",
    startAt: new Date(2026, 2, 1),
    endAt: new Date(2026, 2, 7),
    status: statuses[0],
    lane: "r1",
  },
  {
    id: "res2",
    name: "Bob - Conference",
    startAt: new Date(2026, 2, 10),
    endAt: new Date(2026, 2, 14),
    status: statuses[1],
    lane: "r1",
  },
  {
    id: "res3",
    name: "Carol - Business",
    startAt: new Date(2026, 2, 3),
    endAt: new Date(2026, 2, 12),
    status: statuses[0],
    lane: "r2",
  },
]

export function Example() {
  const [data, setData] = useState(reservations)

  const handleMove = (
    id: string,
    startAt: Date,
    endAt: Date | null
  ) => {
    if (!endAt) return
    setData((prev) =>
      prev.map((r) =>
        r.id === id ? { ...r, startAt, endAt } : r
      )
    )
  }

  const byRoom = rooms.map((room) => ({
    room,
    items: data.filter((r) => r.lane === room.id),
  }))

  return (
    <GanttProvider
      className="border"
      range="monthly"
      zoom={100}
    >
      <GanttSidebar>
        <GanttSidebarGroup name="Reservations">
          {byRoom.map(({ room, items }) => (
            <GanttSidebarItem
              key={room.id}
              feature={{
                id: room.id,
                name: room.name,
                startAt: items[0]?.startAt ?? new Date(),
                endAt: items[0]?.endAt ?? new Date(),
                status: statuses[0],
              }}
            />
          ))}
        </GanttSidebarGroup>
      </GanttSidebar>
      <GanttTimeline>
        <GanttHeader />
        <GanttFeatureList>
          <GanttFeatureListGroup>
            {byRoom.map(({ room, items }) => (
              <div key={room.id}>
                <GanttFeatureRow
                  features={items}
                  onMove={handleMove}
                >
                  {(feature) => (
                    <p className="flex-1 truncate text-xs">
                      {feature.name}
                    </p>
                  )}
                </GanttFeatureRow>
              </div>
            ))}
          </GanttFeatureListGroup>
        </GanttFeatureList>
        <GanttToday />
      </GanttTimeline>
    </GanttProvider>
  )
}
```
