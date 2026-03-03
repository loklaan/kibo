### Combobox

> Autocomplete input and command palette with a list of suggestions.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/combobox.json"
```

#### Dependencies

External packages installed automatically:
- `@radix-ui/react-use-controllable-state` — controllable state management for value and open state

#### Anatomy

```tsx
import {
  Combobox,
  ComboboxTrigger,
  ComboboxContent,
  ComboboxInput,
  ComboboxList,
  ComboboxEmpty,
  ComboboxGroup,
  ComboboxItem,
  ComboboxSeparator,
  ComboboxCreateNew,
} from "@/components/kibo-ui/combobox"
```

| Component | Description |
|-----------|-------------|
| `Combobox` | Root provider. Wraps a Popover and supplies context to all children. |
| `ComboboxTrigger` | Button that opens the popover. Displays the selected label or a placeholder. |
| `ComboboxContent` | Popover dropdown containing the command palette. |
| `ComboboxInput` | Search input for filtering items. |
| `ComboboxList` | Scrollable container for groups and items. |
| `ComboboxEmpty` | Shown when no items match the search query. |
| `ComboboxGroup` | Groups related items together with an optional heading. |
| `ComboboxItem` | A single selectable option. Selecting it closes the popover. |
| `ComboboxSeparator` | Visual divider between groups or items. |
| `ComboboxCreateNew` | Action button for creating a new item from the current search input. |

| Type | Description |
|------|-------------|
| `ComboboxData` | Shape of each item in the `data` array. |

```ts
type ComboboxData = {
  label: string
  value: string
}
```

#### Props

**Combobox**

Extends `Popover` component props.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `data` | `ComboboxData[]` | — | Array of items available for selection. |
| `type` | `string` | — | Label used in placeholder text (e.g. "Select {type}..."). |
| `defaultValue` | `string` | `""` | Initial selected value in uncontrolled mode. |
| `value` | `string` | — | Selected value in controlled mode. |
| `onValueChange` | `(value: string) => void` | — | Called when the selected value changes. |
| `open` | `boolean` | `false` | Whether the popover is open in controlled mode. |
| `onOpenChange` | `(open: boolean) => void` | — | Called when the open state changes. |

**ComboboxTrigger**

Extends `Button` component props.

No additional custom props. Renders the selected item label
or a "Select {type}..." placeholder by default. Pass `children`
to provide a custom trigger.

**ComboboxContent**

Extends `Command` component props.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `popoverOptions` | `ComponentProps<typeof PopoverContent>` | — | Props forwarded to the underlying `PopoverContent`. |

**ComboboxInput**

Extends `CommandInput` component props.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `value` | `string` | — | Controlled search input value. |
| `defaultValue` | `string` | — | Initial search input value. |
| `onValueChange` | `(value: string) => void` | — | Called when the search input value changes. |

**ComboboxList**

Accepts standard `CommandList` props.

**ComboboxEmpty**

Accepts standard `CommandEmpty` props. Displays "No {type}
found." by default when no children are provided.

**ComboboxGroup**

Accepts standard `CommandGroup` props.

**ComboboxItem**

Accepts standard `CommandItem` props. Selecting an item sets
the combobox value and closes the popover.

**ComboboxSeparator**

Accepts standard `CommandSeparator` props.

**ComboboxCreateNew**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `onCreateNew` | `(value: string) => void` | — | Called with the trimmed input value when clicked. |
| `children` | `(inputValue: string) => ReactNode` | — | Render function for custom content. Receives the current input value. |
| `className` | `string` | — | Additional CSS class names. |

#### Usage

##### Basic

```tsx
"use client"

import {
  Combobox,
  ComboboxContent,
  ComboboxEmpty,
  ComboboxGroup,
  ComboboxInput,
  ComboboxItem,
  ComboboxList,
  ComboboxTrigger,
} from "@/components/kibo-ui/combobox"

const frameworks = [
  { value: "next.js", label: "Next.js" },
  { value: "remix", label: "Remix" },
  { value: "astro", label: "Astro" },
]

export function Example() {
  return (
    <Combobox data={frameworks} type="framework">
      <ComboboxTrigger />
      <ComboboxContent>
        <ComboboxInput />
        <ComboboxEmpty />
        <ComboboxList>
          <ComboboxGroup>
            {frameworks.map((item) => (
              <ComboboxItem
                key={item.value}
                value={item.value}
              >
                {item.label}
              </ComboboxItem>
            ))}
          </ComboboxGroup>
        </ComboboxList>
      </ComboboxContent>
    </Combobox>
  )
}
```

##### Controlled

Manage the selected value and open state externally
with React state.

```tsx
"use client"

import {
  Combobox,
  ComboboxContent,
  ComboboxEmpty,
  ComboboxGroup,
  ComboboxInput,
  ComboboxItem,
  ComboboxList,
  ComboboxTrigger,
} from "@/components/kibo-ui/combobox"
import { useState } from "react"

const colors = [
  { value: "red", label: "Red" },
  { value: "green", label: "Green" },
  { value: "blue", label: "Blue" },
]

export function Example() {
  const [open, setOpen] = useState(false)
  const [value, setValue] = useState("red")

  return (
    <Combobox
      data={colors}
      onOpenChange={setOpen}
      onValueChange={setValue}
      open={open}
      type="color"
      value={value}
    >
      <ComboboxTrigger />
      <ComboboxContent>
        <ComboboxInput />
        <ComboboxEmpty />
        <ComboboxList>
          <ComboboxGroup>
            {colors.map((color) => (
              <ComboboxItem
                key={color.value}
                value={color.value}
              >
                {color.label}
              </ComboboxItem>
            ))}
          </ComboboxGroup>
        </ComboboxList>
      </ComboboxContent>
    </Combobox>
  )
}
```

##### Create New Items

Allow users to add items that do not exist in the list.
`ComboboxCreateNew` renders inside `ComboboxEmpty` and
calls `onCreateNew` with the current search input.

```tsx
"use client"

import {
  Combobox,
  ComboboxContent,
  ComboboxCreateNew,
  ComboboxEmpty,
  ComboboxGroup,
  ComboboxInput,
  ComboboxItem,
  ComboboxList,
  ComboboxTrigger,
} from "@/components/kibo-ui/combobox"
import { useState } from "react"

const initial = [
  { value: "next.js", label: "Next.js" },
  { value: "remix", label: "Remix" },
  { value: "astro", label: "Astro" },
]

export function Example() {
  const [items, setItems] = useState(initial)
  const [value, setValue] = useState("")

  const handleCreateNew = (input: string) => {
    const slug = input.toLowerCase().replace(/\s+/g, "-")
    setItems((prev) => [...prev, { value: slug, label: input }])
    setValue(slug)
  }

  return (
    <Combobox
      data={items}
      onValueChange={setValue}
      type="framework"
      value={value}
    >
      <ComboboxTrigger className="w-[300px]" />
      <ComboboxContent>
        <ComboboxInput />
        <ComboboxEmpty>
          <ComboboxCreateNew onCreateNew={handleCreateNew} />
        </ComboboxEmpty>
        <ComboboxList>
          <ComboboxGroup>
            {items.map((item) => (
              <ComboboxItem
                key={item.value}
                value={item.value}
              >
                {item.label}
              </ComboboxItem>
            ))}
          </ComboboxGroup>
        </ComboboxList>
      </ComboboxContent>
    </Combobox>
  )
}
```

##### Fixed Width Trigger

Set a fixed width on the trigger button using a className.
The dropdown automatically matches the trigger width.

```tsx
"use client"

import {
  Combobox,
  ComboboxContent,
  ComboboxEmpty,
  ComboboxGroup,
  ComboboxInput,
  ComboboxItem,
  ComboboxList,
  ComboboxTrigger,
} from "@/components/kibo-ui/combobox"

const sizes = [
  { value: "sm", label: "Small" },
  { value: "md", label: "Medium" },
  { value: "lg", label: "Large" },
]

export function Example() {
  return (
    <Combobox data={sizes} type="size">
      <ComboboxTrigger className="w-[250px]" />
      <ComboboxContent>
        <ComboboxInput />
        <ComboboxEmpty />
        <ComboboxList>
          <ComboboxGroup>
            {sizes.map((size) => (
              <ComboboxItem
                key={size.value}
                value={size.value}
              >
                {size.label}
              </ComboboxItem>
            ))}
          </ComboboxGroup>
        </ComboboxList>
      </ComboboxContent>
    </Combobox>
  )
}
```
