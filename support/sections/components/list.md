### List

> List views are a great way to show a list of tasks grouped by status and ranked by priority.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/list.json"
```

#### Dependencies

External packages installed automatically:
- `@dnd-kit/core` — drag-and-drop primitives for draggable items and droppable groups
- `@dnd-kit/modifiers` — restricts drag movement to the vertical axis

#### Anatomy

```tsx
import {
  ListProvider,
  ListGroup,
  ListHeader,
  ListItems,
  ListItem,
} from "@/components/kibo-ui/list"

import type { DragEndEvent } from "@/components/kibo-ui/list"
```

| Component | Description |
|-----------|-------------|
| `ListProvider` | Root provider. Wraps all children in a DnD context with vertical-axis constraint. |
| `ListGroup` | Droppable group container. Highlights when an item is dragged over it. |
| `ListHeader` | Group header. Accepts either `children` for custom content or `name`/`color` props for a default status header. |
| `ListItems` | Flex container for list items within a group. |
| `ListItem` | Draggable item. Renders a default label from `name` or custom content via `children`. |

| Type | Description |
|------|-------------|
| `DragEndEvent` | Re-exported from `@dnd-kit/core`. Passed to the `onDragEnd` callback. |

#### Props

**ListProvider**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `onDragEnd` | `(event: DragEndEvent) => void` | — | Called when an item is dropped. Use this to update your data. |
| `className` | `string` | `undefined` | Class name applied to the outer wrapper div. |

**ListGroup**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `id` | `string` | — | Unique identifier for this droppable group. |
| `className` | `string` | `undefined` | Class name applied to the group container. |

**ListHeader**

Accepts one of two prop shapes:

*Custom content:*

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `children` | `ReactNode` | — | Custom header content. |

*Default status header:*

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `name` | `string` | — | Status name displayed as text. |
| `color` | `string` | — | CSS color for the status dot. |
| `className` | `string` | `undefined` | Class name applied to the header container. |

**ListItems**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `className` | `string` | `undefined` | Class name applied to the items container. |

**ListItem**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `id` | `string` | — | Unique identifier for this draggable item. |
| `name` | `string` | — | Display name. Rendered as default content when `children` is not provided. |
| `index` | `number` | — | Position index of the item within its group. |
| `parent` | `string` | — | Identifier of the parent group this item belongs to. |
| `children` | `ReactNode` | `undefined` | Custom item content. Overrides the default name label. |
| `className` | `string` | `undefined` | Class name applied to the item container. |

#### Usage

##### Basic

A minimal grouped list with drag-and-drop between groups.

```tsx
"use client"

import type { DragEndEvent } from "@/components/kibo-ui/list"
import {
  ListGroup,
  ListHeader,
  ListItem,
  ListItems,
  ListProvider,
} from "@/components/kibo-ui/list"
import { useState } from "react"

const statuses = [
  { id: "planned", name: "Planned", color: "#6B7280" },
  { id: "done", name: "Done", color: "#10B981" },
]

const initialTasks = [
  { id: "1", name: "Write documentation", status: "Planned" },
  { id: "2", name: "Review pull request", status: "Planned" },
  { id: "3", name: "Ship feature", status: "Done" },
]

export function Example() {
  const [tasks, setTasks] = useState(initialTasks)

  const handleDragEnd = (event: DragEndEvent) => {
    const { active, over } = event
    if (!over) return

    setTasks((prev) =>
      prev.map((task) =>
        task.id === active.id
          ? { ...task, status: String(over.id) }
          : task
      )
    )
  }

  return (
    <ListProvider onDragEnd={handleDragEnd}>
      {statuses.map((status) => (
        <ListGroup id={status.name} key={status.name}>
          <ListHeader
            color={status.color}
            name={status.name}
          />
          <ListItems>
            {tasks
              .filter((t) => t.status === status.name)
              .map((task, index) => (
                <ListItem
                  id={task.id}
                  index={index}
                  key={task.id}
                  name={task.name}
                  parent={status.name}
                />
              ))}
          </ListItems>
        </ListGroup>
      ))}
    </ListProvider>
  )
}
```

##### Custom Item Content

Pass `children` to `ListItem` to render custom content instead of the default name label.

```tsx
"use client"

import type { DragEndEvent } from "@/components/kibo-ui/list"
import {
  ListGroup,
  ListHeader,
  ListItem,
  ListItems,
  ListProvider,
} from "@/components/kibo-ui/list"
import { useState } from "react"

const statuses = [
  { id: "planned", name: "Planned", color: "#6B7280" },
  { id: "in-progress", name: "In Progress", color: "#F59E0B" },
  { id: "done", name: "Done", color: "#10B981" },
]

const initialTasks = [
  {
    id: "1",
    name: "Write documentation",
    status: "Planned",
    assignee: "Alice",
  },
  {
    id: "2",
    name: "Review pull request",
    status: "In Progress",
    assignee: "Bob",
  },
  {
    id: "3",
    name: "Ship feature",
    status: "Done",
    assignee: "Carol",
  },
]

export function Example() {
  const [tasks, setTasks] = useState(initialTasks)

  const handleDragEnd = (event: DragEndEvent) => {
    const { active, over } = event
    if (!over) return

    const status = statuses.find((s) => s.name === over.id)
    if (!status) return

    setTasks((prev) =>
      prev.map((task) =>
        task.id === active.id
          ? { ...task, status: status.name }
          : task
      )
    )
  }

  return (
    <ListProvider onDragEnd={handleDragEnd}>
      {statuses.map((status) => (
        <ListGroup id={status.name} key={status.name}>
          <ListHeader
            color={status.color}
            name={status.name}
          />
          <ListItems>
            {tasks
              .filter((t) => t.status === status.name)
              .map((task, index) => (
                <ListItem
                  id={task.id}
                  index={index}
                  key={task.id}
                  name={task.name}
                  parent={status.name}
                >
                  <div
                    className="h-2 w-2 shrink-0 rounded-full"
                    style={{
                      backgroundColor: statuses.find(
                        (s) => s.name === task.status
                      )?.color,
                    }}
                  />
                  <p className="m-0 flex-1 font-medium text-sm">
                    {task.name}
                  </p>
                  <span className="text-muted-foreground text-xs">
                    {task.assignee}
                  </span>
                </ListItem>
              ))}
          </ListItems>
        </ListGroup>
      ))}
    </ListProvider>
  )
}
```

##### Custom Header

Use the `children` prop on `ListHeader` to render a fully custom group header.

```tsx
"use client"

import type { DragEndEvent } from "@/components/kibo-ui/list"
import {
  ListGroup,
  ListHeader,
  ListItem,
  ListItems,
  ListProvider,
} from "@/components/kibo-ui/list"
import { useState } from "react"

const statuses = [
  { id: "todo", name: "To Do", color: "#6B7280", count: 2 },
  { id: "done", name: "Done", color: "#10B981", count: 1 },
]

const initialTasks = [
  { id: "1", name: "Design mockups", status: "To Do" },
  { id: "2", name: "Set up CI", status: "To Do" },
  { id: "3", name: "Deploy staging", status: "Done" },
]

export function Example() {
  const [tasks, setTasks] = useState(initialTasks)

  const handleDragEnd = (event: DragEndEvent) => {
    const { active, over } = event
    if (!over) return

    setTasks((prev) =>
      prev.map((task) =>
        task.id === active.id
          ? { ...task, status: String(over.id) }
          : task
      )
    )
  }

  return (
    <ListProvider onDragEnd={handleDragEnd}>
      {statuses.map((status) => {
        const count = tasks.filter(
          (t) => t.status === status.name
        ).length
        return (
          <ListGroup id={status.name} key={status.name}>
            <ListHeader>
              <div className="flex items-center gap-2 bg-foreground/5 p-3">
                <div
                  className="h-2 w-2 rounded-full"
                  style={{ backgroundColor: status.color }}
                />
                <span className="font-semibold text-sm">
                  {status.name}
                </span>
                <span className="text-muted-foreground text-xs">
                  ({count})
                </span>
              </div>
            </ListHeader>
            <ListItems>
              {tasks
                .filter((t) => t.status === status.name)
                .map((task, index) => (
                  <ListItem
                    id={task.id}
                    index={index}
                    key={task.id}
                    name={task.name}
                    parent={status.name}
                  />
                ))}
            </ListItems>
          </ListGroup>
        )
      })}
    </ListProvider>
  )
}
```
