### Tags

> Tags are a way to apply multiple labels to an item.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/tags.json"
```

#### Anatomy

```tsx
import {
  Tags,
  TagsTrigger,
  TagsValue,
  TagsContent,
  TagsInput,
  TagsList,
  TagsEmpty,
  TagsGroup,
  TagsItem,
} from "@/components/kibo-ui/tags"
```

| Component | Description |
|-----------|-------------|
| `Tags` | Root provider. Wraps a popover and shared context. |
| `TagsTrigger` | Button that opens the popover and displays selected tags. |
| `TagsValue` | Badge for a single selected tag with an optional remove button. |
| `TagsContent` | Popover dropdown containing the command palette. |
| `TagsInput` | Search input inside the popover for filtering tags. |
| `TagsList` | Scrollable list of tag options. |
| `TagsEmpty` | Empty state shown when no tags match the search query. |
| `TagsGroup` | Group container for tag items. |
| `TagsItem` | Individual selectable tag option. |

#### Props

**Tags**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `value` | `string` | `undefined` | Current search/filter value. |
| `setValue` | `(value: string) => void` | — | Callback when the search value changes. |
| `open` | `boolean` | `false` | Controlled open state of the popover. |
| `onOpenChange` | `(open: boolean) => void` | — | Called when the popover open state changes. |
| `children` | `ReactNode` | — | Child components. |
| `className` | `string` | `undefined` | Additional CSS classes for the root container. |

**TagsTrigger**

Extends `Button` attributes from shadcn/ui.

**TagsValue**

Extends `Badge` attributes from shadcn/ui.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `onRemove` | `() => void` | `undefined` | Called when the remove button is clicked. Shows a remove icon when provided. |

**TagsContent**

Extends `PopoverContent` attributes from shadcn/ui.

**TagsInput**

Extends `CommandInput` attributes from shadcn/ui.

**TagsList**

Extends `CommandList` attributes from shadcn/ui.

**TagsEmpty**

Extends `CommandEmpty` attributes from shadcn/ui. Defaults to "No tags found." when no children are provided.

**TagsGroup**

Extends `CommandGroup` attributes from shadcn/ui.

**TagsItem**

Extends `CommandItem` attributes from shadcn/ui.

#### Usage

##### Basic

```tsx
"use client"

import {
  Tags,
  TagsTrigger,
  TagsValue,
  TagsContent,
  TagsInput,
  TagsList,
  TagsEmpty,
  TagsGroup,
  TagsItem,
} from "@/components/kibo-ui/tags"
import { CheckIcon } from "lucide-react"
import { useState } from "react"

const tags = [
  { id: "react", label: "React" },
  { id: "typescript", label: "TypeScript" },
  { id: "javascript", label: "JavaScript" },
  { id: "nextjs", label: "Next.js" },
]

export function Example() {
  const [selected, setSelected] = useState<string[]>([])

  const handleRemove = (value: string) => {
    setSelected((prev) => prev.filter((v) => v !== value))
  }

  const handleSelect = (value: string) => {
    if (selected.includes(value)) {
      handleRemove(value)
      return
    }
    setSelected((prev) => [...prev, value])
  }

  return (
    <Tags>
      <TagsTrigger>
        {selected.map((tag) => (
          <TagsValue
            key={tag}
            onRemove={() => handleRemove(tag)}
          >
            {tags.find((t) => t.id === tag)?.label}
          </TagsValue>
        ))}
      </TagsTrigger>
      <TagsContent>
        <TagsInput placeholder="Search tag..." />
        <TagsList>
          <TagsEmpty />
          <TagsGroup>
            {tags.map((tag) => (
              <TagsItem
                key={tag.id}
                value={tag.id}
                onSelect={handleSelect}
              >
                {tag.label}
                {selected.includes(tag.id) && (
                  <CheckIcon size={14} />
                )}
              </TagsItem>
            ))}
          </TagsGroup>
        </TagsList>
      </TagsContent>
    </Tags>
  )
}
```

##### Filtered List

Hide already-selected tags from the dropdown list so users
only see available options.

```tsx
"use client"

import {
  Tags,
  TagsTrigger,
  TagsValue,
  TagsContent,
  TagsInput,
  TagsList,
  TagsEmpty,
  TagsGroup,
  TagsItem,
} from "@/components/kibo-ui/tags"
import { useState } from "react"

const tags = [
  { id: "react", label: "React" },
  { id: "typescript", label: "TypeScript" },
  { id: "javascript", label: "JavaScript" },
  { id: "nextjs", label: "Next.js" },
]

export function Example() {
  const [selected, setSelected] = useState<string[]>([])

  const handleRemove = (value: string) => {
    setSelected((prev) => prev.filter((v) => v !== value))
  }

  const handleSelect = (value: string) => {
    setSelected((prev) => [...prev, value])
  }

  return (
    <Tags>
      <TagsTrigger>
        {selected.map((tag) => (
          <TagsValue
            key={tag}
            onRemove={() => handleRemove(tag)}
          >
            {tags.find((t) => t.id === tag)?.label}
          </TagsValue>
        ))}
      </TagsTrigger>
      <TagsContent>
        <TagsInput placeholder="Search tag..." />
        <TagsList>
          <TagsEmpty />
          <TagsGroup>
            {tags
              .filter((tag) => !selected.includes(tag.id))
              .map((tag) => (
                <TagsItem
                  key={tag.id}
                  value={tag.id}
                  onSelect={handleSelect}
                >
                  {tag.label}
                </TagsItem>
              ))}
          </TagsGroup>
        </TagsList>
      </TagsContent>
    </Tags>
  )
}
```

##### Create Tag

Allow users to create tags that do not exist yet. The
`TagsEmpty` component accepts custom children to render a
creation prompt when no tags match the search.

```tsx
"use client"

import {
  Tags,
  TagsTrigger,
  TagsValue,
  TagsContent,
  TagsInput,
  TagsList,
  TagsEmpty,
  TagsGroup,
  TagsItem,
} from "@/components/kibo-ui/tags"
import { CheckIcon, PlusIcon } from "lucide-react"
import { useState } from "react"

const defaultTags = [
  { id: "react", label: "React" },
  { id: "typescript", label: "TypeScript" },
  { id: "nextjs", label: "Next.js" },
]

export function Example() {
  const [selected, setSelected] = useState<string[]>([])
  const [newTag, setNewTag] = useState("")
  const [tags, setTags] = useState(defaultTags)

  const handleRemove = (value: string) => {
    setSelected((prev) => prev.filter((v) => v !== value))
  }

  const handleSelect = (value: string) => {
    if (selected.includes(value)) {
      handleRemove(value)
      return
    }
    setSelected((prev) => [...prev, value])
  }

  const handleCreateTag = () => {
    setTags((prev) => [
      ...prev,
      { id: newTag, label: newTag },
    ])
    setSelected((prev) => [...prev, newTag])
    setNewTag("")
  }

  return (
    <Tags>
      <TagsTrigger>
        {selected.map((tag) => (
          <TagsValue
            key={tag}
            onRemove={() => handleRemove(tag)}
          >
            {tags.find((t) => t.id === tag)?.label}
          </TagsValue>
        ))}
      </TagsTrigger>
      <TagsContent>
        <TagsInput
          placeholder="Search tag..."
          onValueChange={setNewTag}
        />
        <TagsList>
          <TagsEmpty>
            <button
              type="button"
              className="mx-auto flex items-center gap-2"
              onClick={handleCreateTag}
            >
              <PlusIcon size={14} />
              Create: {newTag}
            </button>
          </TagsEmpty>
          <TagsGroup>
            {tags.map((tag) => (
              <TagsItem
                key={tag.id}
                value={tag.id}
                onSelect={handleSelect}
              >
                {tag.label}
                {selected.includes(tag.id) && (
                  <CheckIcon size={14} />
                )}
              </TagsItem>
            ))}
          </TagsGroup>
        </TagsList>
      </TagsContent>
    </Tags>
  )
}
```

##### Controlled Open State

Control the popover open state externally using the `open`
and `onOpenChange` props on the root `Tags` component.

```tsx
"use client"

import {
  Tags,
  TagsTrigger,
  TagsValue,
  TagsContent,
  TagsInput,
  TagsList,
  TagsEmpty,
  TagsGroup,
  TagsItem,
} from "@/components/kibo-ui/tags"
import { CheckIcon } from "lucide-react"
import { useState } from "react"

const tags = [
  { id: "bug", label: "Bug" },
  { id: "feature", label: "Feature" },
  { id: "docs", label: "Documentation" },
]

export function Example() {
  const [selected, setSelected] = useState<string[]>([])
  const [open, setOpen] = useState(false)

  const handleSelect = (value: string) => {
    if (selected.includes(value)) {
      setSelected((prev) =>
        prev.filter((v) => v !== value)
      )
      return
    }
    setSelected((prev) => [...prev, value])
  }

  return (
    <Tags open={open} onOpenChange={setOpen}>
      <TagsTrigger>
        {selected.map((tag) => (
          <TagsValue
            key={tag}
            onRemove={() =>
              setSelected((prev) =>
                prev.filter((v) => v !== tag)
              )
            }
          >
            {tags.find((t) => t.id === tag)?.label}
          </TagsValue>
        ))}
      </TagsTrigger>
      <TagsContent>
        <TagsInput placeholder="Search tag..." />
        <TagsList>
          <TagsEmpty />
          <TagsGroup>
            {tags.map((tag) => (
              <TagsItem
                key={tag.id}
                value={tag.id}
                onSelect={handleSelect}
              >
                {tag.label}
                {selected.includes(tag.id) && (
                  <CheckIcon size={14} />
                )}
              </TagsItem>
            ))}
          </TagsGroup>
        </TagsList>
      </TagsContent>
    </Tags>
  )
}
```
