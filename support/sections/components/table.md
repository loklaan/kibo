### Table

> Table views are used to display data in a tabular format. They are useful for displaying large amounts of data in a structured way.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/table.json"
```

#### Dependencies

External packages installed automatically:
- `@tanstack/react-table` — headless table utilities (sorting, row models, column definitions)
- `jotai` — atom-based state management for sorting state
- `lucide-react` — sort indicator icons

#### Anatomy

```tsx
import {
  TableProvider,
  TableHeader,
  TableHeaderGroup,
  TableHead,
  TableColumnHeader,
  TableBody,
  TableRow,
  TableCell,
} from "@/components/kibo-ui/table"

import type { ColumnDef } from "@/components/kibo-ui/table"
```

| Component | Description |
|-----------|-------------|
| `TableProvider` | Root provider. Initializes TanStack Table and supplies context to all children. Renders the underlying `<table>` element. |
| `TableHeader` | Table header section. Iterates over header groups via a render function. |
| `TableHeaderGroup` | A single header row. Iterates over headers via a render function. |
| `TableHead` | Individual header cell. Renders the column header definition. |
| `TableColumnHeader` | Sortable column header with a dropdown menu for ascending/descending sort. |
| `TableBody` | Table body section. Iterates over rows via a render function. Shows "No results." when empty. |
| `TableRow` | A single data row. Iterates over visible cells via a render function. |
| `TableCell` | Individual data cell. Renders the column cell definition. |

| Type | Description |
|------|-------------|
| `ColumnDef<TData, TValue>` | Column definition from `@tanstack/react-table`. Defines accessors, headers, and cell renderers. |

#### Props

**TableProvider**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `columns` | `ColumnDef<TData, TValue>[]` | — | Column definitions for the table. |
| `data` | `TData[]` | — | Array of row data objects. |
| `children` | `ReactNode` | — | Child components (TableHeader, TableBody, etc.). |
| `className` | `string` | `undefined` | CSS class applied to the root `<table>` element. |

**TableHeader**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `children` | `(props: { headerGroup: HeaderGroup }) => ReactNode` | — | Render function called for each header group. |
| `className` | `string` | `undefined` | CSS class for the `<thead>` element. |

**TableHeaderGroup**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `headerGroup` | `HeaderGroup` | — | Header group instance from TanStack Table. |
| `children` | `(props: { header: Header }) => ReactNode` | — | Render function called for each header in the group. |

**TableHead**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `header` | `Header` | — | Header instance from TanStack Table. |
| `className` | `string` | `undefined` | CSS class for the `<th>` element. |

**TableColumnHeader**

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `column` | `Column<TData, TValue>` | — | Column instance from TanStack Table. |
| `title` | `string` | — | Display title for the column header. |

**TableBody**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `children` | `(props: { row: Row }) => ReactNode` | — | Render function called for each row. |
| `className` | `string` | `undefined` | CSS class for the `<tbody>` element. |

**TableRow**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `row` | `Row` | — | Row instance from TanStack Table. |
| `children` | `(props: { cell: Cell }) => ReactNode` | — | Render function called for each visible cell in the row. |
| `className` | `string` | `undefined` | CSS class for the `<tr>` element. |

**TableCell**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `cell` | `Cell` | — | Cell instance from TanStack Table. |
| `className` | `string` | `undefined` | CSS class for the `<td>` element. |

#### Usage

##### Basic

A minimal table with string accessor columns and no sorting.

```tsx
"use client"

import type { ColumnDef } from "@/components/kibo-ui/table"
import {
  TableProvider,
  TableHeader,
  TableHeaderGroup,
  TableHead,
  TableBody,
  TableRow,
  TableCell,
} from "@/components/kibo-ui/table"

type User = {
  name: string
  email: string
  role: string
}

const data: User[] = [
  { name: "Alice", email: "alice@acme.com", role: "Admin" },
  { name: "Bob", email: "bob@acme.com", role: "Editor" },
  { name: "Carol", email: "carol@acme.com", role: "Viewer" },
]

const columns: ColumnDef<User>[] = [
  { accessorKey: "name", header: "Name" },
  { accessorKey: "email", header: "Email" },
  { accessorKey: "role", header: "Role" },
]

export function Example() {
  return (
    <TableProvider columns={columns} data={data}>
      <TableHeader>
        {({ headerGroup }) => (
          <TableHeaderGroup
            headerGroup={headerGroup}
            key={headerGroup.id}
          >
            {({ header }) => (
              <TableHead
                header={header}
                key={header.id}
              />
            )}
          </TableHeaderGroup>
        )}
      </TableHeader>
      <TableBody>
        {({ row }) => (
          <TableRow key={row.id} row={row}>
            {({ cell }) => (
              <TableCell cell={cell} key={cell.id} />
            )}
          </TableRow>
        )}
      </TableBody>
    </TableProvider>
  )
}
```

##### Sortable Columns

Use `TableColumnHeader` in the column definition's
`header` field to enable sorting via a dropdown menu.

```tsx
"use client"

import type { ColumnDef } from "@/components/kibo-ui/table"
import {
  TableProvider,
  TableHeader,
  TableHeaderGroup,
  TableHead,
  TableColumnHeader,
  TableBody,
  TableRow,
  TableCell,
} from "@/components/kibo-ui/table"

type Task = {
  id: string
  title: string
  status: string
  priority: string
}

const data: Task[] = [
  {
    id: "1",
    title: "Set up CI pipeline",
    status: "Done",
    priority: "High",
  },
  {
    id: "2",
    title: "Write API docs",
    status: "In Progress",
    priority: "Medium",
  },
  {
    id: "3",
    title: "Fix login bug",
    status: "Planned",
    priority: "High",
  },
]

const columns: ColumnDef<Task>[] = [
  {
    accessorKey: "title",
    header: ({ column }) => (
      <TableColumnHeader column={column} title="Title" />
    ),
  },
  {
    accessorKey: "status",
    header: ({ column }) => (
      <TableColumnHeader column={column} title="Status" />
    ),
  },
  {
    accessorKey: "priority",
    header: ({ column }) => (
      <TableColumnHeader
        column={column}
        title="Priority"
      />
    ),
  },
]

export function Example() {
  return (
    <TableProvider columns={columns} data={data}>
      <TableHeader>
        {({ headerGroup }) => (
          <TableHeaderGroup
            headerGroup={headerGroup}
            key={headerGroup.id}
          >
            {({ header }) => (
              <TableHead
                header={header}
                key={header.id}
              />
            )}
          </TableHeaderGroup>
        )}
      </TableHeader>
      <TableBody>
        {({ row }) => (
          <TableRow key={row.id} row={row}>
            {({ cell }) => (
              <TableCell cell={cell} key={cell.id} />
            )}
          </TableRow>
        )}
      </TableBody>
    </TableProvider>
  )
}
```

##### Custom Cell Renderers

Use the `cell` property in column definitions to render
custom content such as formatted dates or styled badges.

```tsx
"use client"

import type { ColumnDef } from "@/components/kibo-ui/table"
import {
  TableProvider,
  TableHeader,
  TableHeaderGroup,
  TableHead,
  TableColumnHeader,
  TableBody,
  TableRow,
  TableCell,
} from "@/components/kibo-ui/table"

type Feature = {
  id: string
  name: string
  status: string
  startAt: Date
  endAt: Date
}

const data: Feature[] = [
  {
    id: "1",
    name: "User dashboard",
    status: "In Progress",
    startAt: new Date("2025-01-15"),
    endAt: new Date("2025-03-30"),
  },
  {
    id: "2",
    name: "Billing integration",
    status: "Planned",
    startAt: new Date("2025-04-01"),
    endAt: new Date("2025-06-15"),
  },
  {
    id: "3",
    name: "Search indexing",
    status: "Done",
    startAt: new Date("2024-10-01"),
    endAt: new Date("2025-01-10"),
  },
]

const statusColors: Record<string, string> = {
  Planned: "#6B7280",
  "In Progress": "#F59E0B",
  Done: "#10B981",
}

const columns: ColumnDef<Feature>[] = [
  {
    accessorKey: "name",
    header: ({ column }) => (
      <TableColumnHeader
        column={column}
        title="Name"
      />
    ),
    cell: ({ row }) => (
      <span className="font-medium">
        {row.original.name}
      </span>
    ),
  },
  {
    accessorKey: "status",
    header: ({ column }) => (
      <TableColumnHeader
        column={column}
        title="Status"
      />
    ),
    cell: ({ row }) => (
      <span className="flex items-center gap-2">
        <span
          className="inline-block h-2 w-2 rounded-full"
          style={{
            backgroundColor:
              statusColors[row.original.status],
          }}
        />
        {row.original.status}
      </span>
    ),
  },
  {
    accessorKey: "startAt",
    header: ({ column }) => (
      <TableColumnHeader
        column={column}
        title="Start"
      />
    ),
    cell: ({ row }) =>
      new Intl.DateTimeFormat("en-US", {
        dateStyle: "medium",
      }).format(row.original.startAt),
  },
  {
    accessorKey: "endAt",
    header: ({ column }) => (
      <TableColumnHeader
        column={column}
        title="End"
      />
    ),
    cell: ({ row }) =>
      new Intl.DateTimeFormat("en-US", {
        dateStyle: "medium",
      }).format(row.original.endAt),
  },
]

export function Example() {
  return (
    <TableProvider columns={columns} data={data}>
      <TableHeader>
        {({ headerGroup }) => (
          <TableHeaderGroup
            headerGroup={headerGroup}
            key={headerGroup.id}
          >
            {({ header }) => (
              <TableHead
                header={header}
                key={header.id}
              />
            )}
          </TableHeaderGroup>
        )}
      </TableHeader>
      <TableBody>
        {({ row }) => (
          <TableRow key={row.id} row={row}>
            {({ cell }) => (
              <TableCell cell={cell} key={cell.id} />
            )}
          </TableRow>
        )}
      </TableBody>
    </TableProvider>
  )
}
```

##### Computed Columns

Use `accessorFn` instead of `accessorKey` to derive a
column value from multiple fields or nested objects.

```tsx
"use client"

import type { ColumnDef } from "@/components/kibo-ui/table"
import {
  TableProvider,
  TableHeader,
  TableHeaderGroup,
  TableHead,
  TableColumnHeader,
  TableBody,
  TableRow,
  TableCell,
} from "@/components/kibo-ui/table"

type Order = {
  id: string
  product: string
  quantity: number
  unitPrice: number
}

const data: Order[] = [
  {
    id: "1",
    product: "Widget A",
    quantity: 10,
    unitPrice: 25,
  },
  {
    id: "2",
    product: "Widget B",
    quantity: 5,
    unitPrice: 40,
  },
  {
    id: "3",
    product: "Widget C",
    quantity: 20,
    unitPrice: 12,
  },
]

const columns: ColumnDef<Order>[] = [
  {
    accessorKey: "product",
    header: ({ column }) => (
      <TableColumnHeader
        column={column}
        title="Product"
      />
    ),
  },
  {
    accessorKey: "quantity",
    header: ({ column }) => (
      <TableColumnHeader
        column={column}
        title="Qty"
      />
    ),
  },
  {
    accessorKey: "unitPrice",
    header: ({ column }) => (
      <TableColumnHeader
        column={column}
        title="Unit Price"
      />
    ),
    cell: ({ row }) =>
      `$${row.original.unitPrice.toFixed(2)}`,
  },
  {
    id: "total",
    accessorFn: (row) =>
      row.quantity * row.unitPrice,
    header: ({ column }) => (
      <TableColumnHeader
        column={column}
        title="Total"
      />
    ),
    cell: ({ getValue }) =>
      `$${(getValue() as number).toFixed(2)}`,
  },
]

export function Example() {
  return (
    <TableProvider columns={columns} data={data}>
      <TableHeader>
        {({ headerGroup }) => (
          <TableHeaderGroup
            headerGroup={headerGroup}
            key={headerGroup.id}
          >
            {({ header }) => (
              <TableHead
                header={header}
                key={header.id}
              />
            )}
          </TableHeaderGroup>
        )}
      </TableHeader>
      <TableBody>
        {({ row }) => (
          <TableRow key={row.id} row={row}>
            {({ cell }) => (
              <TableCell cell={cell} key={cell.id} />
            )}
          </TableRow>
        )}
      </TableBody>
    </TableProvider>
  )
}
```
