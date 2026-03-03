### Kanban

> A kanban board is a visual tool that helps you manage and visualize your work. It is a board with columns, and each column represents a status.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/kanban.json"
```

#### Dependencies

External packages installed automatically:
- `@dnd-kit/core` — drag-and-drop primitives
- `@dnd-kit/sortable` — sortable list behavior
- `@dnd-kit/utilities` — CSS transform helpers
- `tunnel-rat` — portals for the drag overlay

#### Anatomy

```tsx
import {
  KanbanProvider,
  KanbanBoard,
  KanbanHeader,
  KanbanCards,
  KanbanCard,
} from "@/components/kibo-ui/kanban"
```

| Component | Description |
|-----------|-------------|
| `KanbanProvider` | Root provider. Supplies column and card data via context and sets up drag-and-drop sensors. Accepts `children` as a render function that iterates over columns. |
| `KanbanBoard` | Droppable column container. Renders a bordered section that highlights when a card is dragged over it. |
| `KanbanHeader` | Column header displayed at the top of a board. |
| `KanbanCards` | Scrollable card list. Filters cards by column `id` and renders each via a render function passed as `children`. |
| `KanbanCard` | Sortable card. Handles drag handles, transforms, and renders a drag overlay clone while dragging. |

| Type | Description |
|------|-------------|
| `DragEndEvent` | Re-exported from `@dnd-kit/core`. Event payload for the `onDragEnd` callback. |

Items passed to `data` must satisfy this base shape (extra fields are allowed):

```ts
type KanbanItem = {
  id: string
  name: string
  column: string
} & Record<string, unknown>
```

Columns passed to `columns` must satisfy this base shape (extra fields are allowed):

```ts
type KanbanColumn = {
  id: string
  name: string
} & Record<string, unknown>
```

#### Props

**KanbanProvider**

Extends `DndContextProps` attributes (excluding `children`).

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `columns` | `C[]` | — | Array of column objects. Each must have `id` and `name`. |
| `data` | `T[]` | — | Array of card objects. Each must have `id`, `name`, and `column`. |
| `children` | `(column: C) => ReactNode` | — | Render function called once per column. |
| `onDataChange` | `(data: T[]) => void` | — | Called with the reordered data array after a drag operation. |
| `onDragStart` | `(event: DragStartEvent) => void` | — | Called when a card drag begins. |
| `onDragOver` | `(event: DragOverEvent) => void` | — | Called when a card is dragged over a new target. |
| `onDragEnd` | `(event: DragEndEvent) => void` | — | Called when a card drag ends. |
| `className` | `string` | — | Class name applied to the outer grid container. |

**KanbanBoard**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `id` | `string` | — | Unique identifier matching a column `id`. Registers this element as a droppable target. |
| `children` | `ReactNode` | — | Column contents (typically a header and cards list). |
| `className` | `string` | — | Class name applied to the column container. |

**KanbanHeader**

Accepts standard `HTMLDivElement` attributes.

**KanbanCards**

Extends `HTMLDivElement` attributes (excluding `children` and `id`).

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `id` | `string` | — | Column `id` used to filter which cards appear in this list. |
| `children` | `(item: T) => ReactNode` | — | Render function called once per card in this column. |

**KanbanCard**

Extends the item type `T` (which includes `id`, `name`, and `column`).

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `id` | `string` | — | Unique card identifier. Registers this element as a sortable item. |
| `name` | `string` | — | Card label. Displayed as fallback text when no `children` are provided. |
| `column` | `string` | — | Column `id` this card belongs to. |
| `children` | `ReactNode` | — | Custom card content. Overrides the default name label. |
| `className` | `string` | — | Class name applied to the inner card element. |

#### Usage

##### Basic

The simplest kanban board with `onDataChange` handling
reordering automatically.

```tsx
"use client"

import { useState } from "react"
import {
  KanbanProvider,
  KanbanBoard,
  KanbanHeader,
  KanbanCards,
  KanbanCard,
} from "@/components/kibo-ui/kanban"

const columns = [
  { id: "todo", name: "To Do" },
  { id: "in-progress", name: "In Progress" },
  { id: "done", name: "Done" },
]

const initialTasks = [
  { id: "1", name: "Research competitors", column: "todo" },
  { id: "2", name: "Write proposal", column: "todo" },
  { id: "3", name: "Design mockups", column: "in-progress" },
  { id: "4", name: "Ship MVP", column: "done" },
]

export function Example() {
  const [tasks, setTasks] = useState(initialTasks)

  return (
    <KanbanProvider
      columns={columns}
      data={tasks}
      onDataChange={setTasks}
    >
      {(column) => (
        <KanbanBoard id={column.id} key={column.id}>
          <KanbanHeader>{column.name}</KanbanHeader>
          <KanbanCards id={column.id}>
            {(task) => (
              <KanbanCard
                id={task.id}
                name={task.name}
                column={column.id}
                key={task.id}
              />
            )}
          </KanbanCards>
        </KanbanBoard>
      )}
    </KanbanProvider>
  )
}
```

##### Custom Card Content

Render rich card content by passing `children` to `KanbanCard`
instead of relying on the default `name` label.

```tsx
"use client"

import { useState } from "react"
import {
  KanbanProvider,
  KanbanBoard,
  KanbanHeader,
  KanbanCards,
  KanbanCard,
} from "@/components/kibo-ui/kanban"

const columns = [
  { id: "planned", name: "Planned", color: "#6B7280" },
  { id: "in-progress", name: "In Progress", color: "#F59E0B" },
  { id: "done", name: "Done", color: "#10B981" },
]

const initialFeatures = [
  {
    id: "1",
    name: "User authentication",
    column: "planned",
    owner: "Alice",
    priority: "High",
  },
  {
    id: "2",
    name: "Dashboard redesign",
    column: "in-progress",
    owner: "Bob",
    priority: "Medium",
  },
  {
    id: "3",
    name: "API documentation",
    column: "done",
    owner: "Carol",
    priority: "Low",
  },
]

export function Example() {
  const [features, setFeatures] = useState(initialFeatures)

  return (
    <KanbanProvider
      columns={columns}
      data={features}
      onDataChange={setFeatures}
    >
      {(column) => (
        <KanbanBoard id={column.id} key={column.id}>
          <KanbanHeader>
            <div className="flex items-center gap-2">
              <div
                className="h-2 w-2 rounded-full"
                style={{ backgroundColor: column.color }}
              />
              <span>{column.name}</span>
            </div>
          </KanbanHeader>
          <KanbanCards id={column.id}>
            {(feature: (typeof features)[number]) => (
              <KanbanCard
                id={feature.id}
                name={feature.name}
                column={column.id}
                key={feature.id}
              >
                <div className="flex flex-col gap-1">
                  <p className="m-0 font-medium text-sm">
                    {feature.name}
                  </p>
                  <div className="flex items-center justify-between">
                    <span className="text-xs text-muted-foreground">
                      {feature.owner}
                    </span>
                    <span className="text-xs text-muted-foreground">
                      {feature.priority}
                    </span>
                  </div>
                </div>
              </KanbanCard>
            )}
          </KanbanCards>
        </KanbanBoard>
      )}
    </KanbanProvider>
  )
}
```

##### Custom Drag End Handler

Use `onDragEnd` instead of `onDataChange` for full control over
how cards are reassigned to columns after a drop.

```tsx
"use client"

import { useState } from "react"
import type { DragEndEvent } from "@/components/kibo-ui/kanban"
import {
  KanbanProvider,
  KanbanBoard,
  KanbanHeader,
  KanbanCards,
  KanbanCard,
} from "@/components/kibo-ui/kanban"

const columns = [
  { id: "backlog", name: "Backlog" },
  { id: "active", name: "Active" },
  { id: "complete", name: "Complete" },
]

const initialItems = [
  { id: "1", name: "Set up CI", column: "backlog" },
  { id: "2", name: "Write tests", column: "backlog" },
  { id: "3", name: "Deploy staging", column: "active" },
]

export function Example() {
  const [items, setItems] = useState(initialItems)

  const handleDragEnd = (event: DragEndEvent) => {
    const { active, over } = event

    if (!over) {
      return
    }

    const targetColumn = columns.find(
      ({ id }) => id === over.id
    )

    if (!targetColumn) {
      return
    }

    setItems((prev) =>
      prev.map((item) =>
        item.id === active.id
          ? { ...item, column: targetColumn.id }
          : item
      )
    )
  }

  return (
    <KanbanProvider
      columns={columns}
      data={items}
      onDragEnd={handleDragEnd}
    >
      {(column) => (
        <KanbanBoard id={column.id} key={column.id}>
          <KanbanHeader>{column.name}</KanbanHeader>
          <KanbanCards id={column.id}>
            {(item) => (
              <KanbanCard
                id={item.id}
                name={item.name}
                column={column.id}
                key={item.id}
              />
            )}
          </KanbanCards>
        </KanbanBoard>
      )}
    </KanbanProvider>
  )
}
```
