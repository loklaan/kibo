### Tree

> A composable tree component with animated expand/collapse and customizable nodes.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/tree.json"
```

#### Dependencies

External packages installed automatically:
- `motion` — animated expand/collapse transitions
- `lucide-react` — default file and folder icons

#### Anatomy

```tsx
import {
  TreeProvider,
  TreeView,
  TreeNode,
  TreeNodeTrigger,
  TreeNodeContent,
  TreeExpander,
  TreeIcon,
  TreeLabel,
} from "@/components/kibo-ui/tree"
```

| Component | Description |
|-----------|-------------|
| `TreeProvider` | Root provider. Manages expand/collapse and selection state for the entire tree. |
| `TreeView` | Outer container. Wraps all tree nodes with padding. |
| `TreeNode` | Individual node. Provides node-level context (id, level, position). |
| `TreeNodeTrigger` | Clickable row for a node. Handles expand/collapse and selection on click. |
| `TreeNodeContent` | Expandable children container. Renders child nodes with animated height transitions. |
| `TreeExpander` | Chevron icon that rotates to indicate expand/collapse state. |
| `TreeIcon` | File or folder icon. Renders default folder/file icons or a custom icon. |
| `TreeLabel` | Text label for the node. |

#### Props

**TreeProvider**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `defaultExpandedIds` | `string[]` | `[]` | Node IDs expanded on mount. |
| `showLines` | `boolean` | `true` | Show connector lines between nodes. |
| `showIcons` | `boolean` | `true` | Show file/folder icons. |
| `selectable` | `boolean` | `true` | Enable node selection on click. |
| `multiSelect` | `boolean` | `false` | Allow selecting multiple nodes with Ctrl/Cmd+click. |
| `selectedIds` | `string[]` | `undefined` | Controlled selected node IDs. |
| `onSelectionChange` | `(selectedIds: string[]) => void` | — | Called when selection changes. |
| `indent` | `number` | `20` | Pixels of indentation per nesting level. |
| `animateExpand` | `boolean` | `true` | Animate expand/collapse transitions. |

**TreeView**

Accepts standard `HTMLDivElement` attributes.

**TreeNode**

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `nodeId` | `string` | auto-generated | Unique identifier for the node. |
| `level` | `number` | `0` | Nesting depth (0 for root nodes). |
| `isLast` | `boolean` | `false` | Whether this is the last sibling at its level. Controls connector line rendering. |
| `parentPath` | `boolean[]` | `[]` | Tracks which ancestor levels are last children. Used internally for connector lines. |

**TreeNodeTrigger**

Extends `motion.div` attributes. Clicking toggles expand and selection.

**TreeNodeContent**

Extends `motion.div` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `hasChildren` | `boolean` | `false` | Set to `true` when the node has child nodes. Controls whether content renders when expanded. |

**TreeExpander**

Extends `motion.div` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `hasChildren` | `boolean` | `false` | Set to `true` to render the chevron arrow. When `false`, renders a spacer for alignment. |

**TreeIcon**

Extends `motion.div` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `icon` | `ReactNode` | `undefined` | Custom icon to render. When omitted, renders a folder icon (open/closed) for nodes with children and a file icon for leaf nodes. |
| `hasChildren` | `boolean` | `false` | Determines whether to render a folder or file icon by default. |

**TreeLabel**

Accepts standard `HTMLSpanElement` attributes.

#### Usage

##### Basic

```tsx
"use client"

import {
  TreeProvider,
  TreeView,
  TreeNode,
  TreeNodeTrigger,
  TreeNodeContent,
  TreeExpander,
  TreeIcon,
  TreeLabel,
} from "@/components/kibo-ui/tree"

export function Example() {
  return (
    <TreeProvider>
      <TreeView>
        <TreeNode nodeId="documents">
          <TreeNodeTrigger>
            <TreeExpander hasChildren />
            <TreeIcon hasChildren />
            <TreeLabel>Documents</TreeLabel>
          </TreeNodeTrigger>
          <TreeNodeContent hasChildren>
            <TreeNode level={1} nodeId="report">
              <TreeNodeTrigger>
                <TreeExpander />
                <TreeIcon />
                <TreeLabel>Report.pdf</TreeLabel>
              </TreeNodeTrigger>
            </TreeNode>
            <TreeNode isLast level={1} nodeId="notes">
              <TreeNodeTrigger>
                <TreeExpander />
                <TreeIcon />
                <TreeLabel>Notes.txt</TreeLabel>
              </TreeNodeTrigger>
            </TreeNode>
          </TreeNodeContent>
        </TreeNode>
        <TreeNode isLast nodeId="readme">
          <TreeNodeTrigger>
            <TreeExpander />
            <TreeIcon />
            <TreeLabel>README.md</TreeLabel>
          </TreeNodeTrigger>
        </TreeNode>
      </TreeView>
    </TreeProvider>
  )
}
```

##### Custom Icons

Override the default file/folder icons with custom icons per node.

```tsx
"use client"

import {
  TreeProvider,
  TreeView,
  TreeNode,
  TreeNodeTrigger,
  TreeNodeContent,
  TreeExpander,
  TreeIcon,
  TreeLabel,
} from "@/components/kibo-ui/tree"
import { Database, Key, Lock, Table } from "lucide-react"

export function Example() {
  return (
    <TreeProvider defaultExpandedIds={["database", "users"]}>
      <TreeView>
        <TreeNode isLast nodeId="database">
          <TreeNodeTrigger>
            <TreeExpander hasChildren />
            <TreeIcon
              hasChildren
              icon={
                <Database className="h-4 w-4 text-blue-500" />
              }
            />
            <TreeLabel>Database</TreeLabel>
          </TreeNodeTrigger>
          <TreeNodeContent hasChildren>
            <TreeNode isLast level={1} nodeId="users">
              <TreeNodeTrigger>
                <TreeExpander hasChildren />
                <TreeIcon
                  hasChildren
                  icon={
                    <Table className="h-4 w-4 text-green-500" />
                  }
                />
                <TreeLabel>Users</TreeLabel>
              </TreeNodeTrigger>
              <TreeNodeContent hasChildren>
                <TreeNode level={2} nodeId="id">
                  <TreeNodeTrigger>
                    <TreeExpander />
                    <TreeIcon
                      icon={
                        <Key className="h-4 w-4 text-yellow-500" />
                      }
                    />
                    <TreeLabel>id</TreeLabel>
                  </TreeNodeTrigger>
                </TreeNode>
                <TreeNode isLast level={2} nodeId="password">
                  <TreeNodeTrigger>
                    <TreeExpander />
                    <TreeIcon
                      icon={
                        <Lock className="h-4 w-4 text-red-500" />
                      }
                    />
                    <TreeLabel>password</TreeLabel>
                  </TreeNodeTrigger>
                </TreeNode>
              </TreeNodeContent>
            </TreeNode>
          </TreeNodeContent>
        </TreeNode>
      </TreeView>
    </TreeProvider>
  )
}
```

##### Without Lines

Disable connector lines for a cleaner look.

```tsx
"use client"

import {
  TreeProvider,
  TreeView,
  TreeNode,
  TreeNodeTrigger,
  TreeNodeContent,
  TreeExpander,
  TreeIcon,
  TreeLabel,
} from "@/components/kibo-ui/tree"

export function Example() {
  return (
    <TreeProvider
      defaultExpandedIds={["projects"]}
      showLines={false}
    >
      <TreeView>
        <TreeNode isLast nodeId="projects">
          <TreeNodeTrigger>
            <TreeExpander hasChildren />
            <TreeIcon hasChildren />
            <TreeLabel>Projects</TreeLabel>
          </TreeNodeTrigger>
          <TreeNodeContent hasChildren>
            <TreeNode level={1} nodeId="homepage">
              <TreeNodeTrigger>
                <TreeExpander />
                <TreeIcon />
                <TreeLabel>Homepage</TreeLabel>
              </TreeNodeTrigger>
            </TreeNode>
            <TreeNode isLast level={1} nodeId="about">
              <TreeNodeTrigger>
                <TreeExpander />
                <TreeIcon />
                <TreeLabel>About Page</TreeLabel>
              </TreeNodeTrigger>
            </TreeNode>
          </TreeNodeContent>
        </TreeNode>
      </TreeView>
    </TreeProvider>
  )
}
```

##### Controlled Selection

Manage selected nodes externally with `selectedIds` and `onSelectionChange`. Enable `multiSelect` to allow Ctrl/Cmd+click for selecting multiple nodes.

```tsx
"use client"

import {
  TreeProvider,
  TreeView,
  TreeNode,
  TreeNodeTrigger,
  TreeNodeContent,
  TreeExpander,
  TreeIcon,
  TreeLabel,
} from "@/components/kibo-ui/tree"
import { useState } from "react"

export function Example() {
  const [selectedIds, setSelectedIds] = useState<string[]>([])

  return (
    <div className="space-y-4">
      <TreeProvider
        defaultExpandedIds={["team", "engineering"]}
        multiSelect
        onSelectionChange={setSelectedIds}
        selectedIds={selectedIds}
      >
        <TreeView>
          <TreeNode isLast nodeId="team">
            <TreeNodeTrigger>
              <TreeExpander hasChildren />
              <TreeIcon hasChildren />
              <TreeLabel>Team</TreeLabel>
            </TreeNodeTrigger>
            <TreeNodeContent hasChildren>
              <TreeNode
                isLast
                level={1}
                nodeId="engineering"
              >
                <TreeNodeTrigger>
                  <TreeExpander hasChildren />
                  <TreeIcon hasChildren />
                  <TreeLabel>Engineering</TreeLabel>
                </TreeNodeTrigger>
                <TreeNodeContent hasChildren>
                  <TreeNode level={2} nodeId="alice">
                    <TreeNodeTrigger>
                      <TreeExpander />
                      <TreeIcon />
                      <TreeLabel>Alice</TreeLabel>
                    </TreeNodeTrigger>
                  </TreeNode>
                  <TreeNode isLast level={2} nodeId="bob">
                    <TreeNodeTrigger>
                      <TreeExpander />
                      <TreeIcon />
                      <TreeLabel>Bob</TreeLabel>
                    </TreeNodeTrigger>
                  </TreeNode>
                </TreeNodeContent>
              </TreeNode>
            </TreeNodeContent>
          </TreeNode>
        </TreeView>
      </TreeProvider>

      {selectedIds.length > 0 && (
        <p className="text-muted-foreground text-sm">
          Selected: {selectedIds.join(", ")}
        </p>
      )}
    </div>
  )
}
```
