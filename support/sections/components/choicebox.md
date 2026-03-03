### Choicebox

> Choiceboxes are a great way to show radio or checkbox options with a card style.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/choicebox.json"
```

#### Dependencies

External packages installed automatically:
- `radix-ui` — accessible radio group primitives
- `lucide-react` — icon primitives

#### Anatomy

```tsx
import {
  Choicebox,
  ChoiceboxItem,
  ChoiceboxItemHeader,
  ChoiceboxItemTitle,
  ChoiceboxItemSubtitle,
  ChoiceboxItemDescription,
  ChoiceboxIndicator,
} from "@/components/kibo-ui/choicebox"
```

| Component | Description |
|-----------|-------------|
| `Choicebox` | Root container. Wraps a radio group and manages selection state. |
| `ChoiceboxItem` | A selectable card option. Provides item context to children. |
| `ChoiceboxItemHeader` | Content area for the title and description within an item. |
| `ChoiceboxItemTitle` | Displays the option label text. |
| `ChoiceboxItemSubtitle` | Secondary text displayed alongside the title. |
| `ChoiceboxItemDescription` | Descriptive text below the title. |
| `ChoiceboxIndicator` | Radio indicator that reflects the selection state. |

#### Props

**Choicebox**

Extends Radix `RadioGroup.Root` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `value` | `string` | `undefined` | Controlled selected value. |
| `defaultValue` | `string` | `undefined` | Initial value when uncontrolled. |
| `onValueChange` | `(value: string) => void` | — | Called when the selected value changes. |
| `disabled` | `boolean` | `false` | Disables all items in the group. |
| `required` | `boolean` | `false` | Marks the group as required for form validation. |
| `name` | `string` | `undefined` | Name attribute for the underlying radio inputs. |
| `orientation` | `"horizontal" \| "vertical"` | `undefined` | Orientation hint for keyboard navigation. |

**ChoiceboxItem**

Extends Radix `RadioGroupItem` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `value` | `string` | — | Unique value identifying this option. |
| `id` | `string` | `undefined` | HTML id for the underlying radio input. |
| `disabled` | `boolean` | `false` | Disables this individual item. |

**ChoiceboxItemHeader**

Accepts standard `HTMLDivElement` attributes.

**ChoiceboxItemTitle**

Accepts standard `HTMLDivElement` attributes.

**ChoiceboxItemSubtitle**

Accepts standard `HTMLSpanElement` attributes.

**ChoiceboxItemDescription**

Accepts standard `HTMLParagraphElement` attributes.

**ChoiceboxIndicator**

Extends Radix `RadioGroupItem` attributes. Reads its `value` from the parent `ChoiceboxItem` context automatically.

#### Usage

##### Basic

```tsx
import {
  Choicebox,
  ChoiceboxIndicator,
  ChoiceboxItem,
  ChoiceboxItemDescription,
  ChoiceboxItemHeader,
  ChoiceboxItemTitle,
} from "@/components/kibo-ui/choicebox"

export function Example() {
  return (
    <Choicebox defaultValue="email">
      <ChoiceboxItem value="email">
        <ChoiceboxItemHeader>
          <ChoiceboxItemTitle>Email</ChoiceboxItemTitle>
          <ChoiceboxItemDescription>
            Send notifications via email.
          </ChoiceboxItemDescription>
        </ChoiceboxItemHeader>
        <ChoiceboxIndicator />
      </ChoiceboxItem>
      <ChoiceboxItem value="sms">
        <ChoiceboxItemHeader>
          <ChoiceboxItemTitle>SMS</ChoiceboxItemTitle>
          <ChoiceboxItemDescription>
            Send notifications via text message.
          </ChoiceboxItemDescription>
        </ChoiceboxItemHeader>
        <ChoiceboxIndicator />
      </ChoiceboxItem>
    </Choicebox>
  )
}
```

##### With Subtitles

Displays supplementary text next to each option title.

```tsx
import {
  Choicebox,
  ChoiceboxIndicator,
  ChoiceboxItem,
  ChoiceboxItemDescription,
  ChoiceboxItemHeader,
  ChoiceboxItemSubtitle,
  ChoiceboxItemTitle,
} from "@/components/kibo-ui/choicebox"

const plans = [
  {
    id: "starter",
    label: "Starter",
    subtitle: "($9/mo)",
    description: "For individuals and small projects.",
  },
  {
    id: "pro",
    label: "Pro",
    subtitle: "($29/mo)",
    description: "For growing teams with advanced needs.",
  },
]

export function Example() {
  return (
    <Choicebox defaultValue="starter">
      {plans.map((plan) => (
        <ChoiceboxItem key={plan.id} value={plan.id}>
          <ChoiceboxItemHeader>
            <ChoiceboxItemTitle>
              {plan.label}
              <ChoiceboxItemSubtitle>
                {plan.subtitle}
              </ChoiceboxItemSubtitle>
            </ChoiceboxItemTitle>
            <ChoiceboxItemDescription>
              {plan.description}
            </ChoiceboxItemDescription>
          </ChoiceboxItemHeader>
          <ChoiceboxIndicator />
        </ChoiceboxItem>
      ))}
    </Choicebox>
  )
}
```

##### Inline Layout

Renders options side by side using CSS grid columns.

```tsx
import {
  Choicebox,
  ChoiceboxIndicator,
  ChoiceboxItem,
  ChoiceboxItemDescription,
  ChoiceboxItemHeader,
  ChoiceboxItemTitle,
} from "@/components/kibo-ui/choicebox"

const options = [
  { id: "light", label: "Light", description: "Use light theme." },
  { id: "dark", label: "Dark", description: "Use dark theme." },
  { id: "system", label: "System", description: "Follow OS setting." },
]

export function Example() {
  return (
    <Choicebox
      defaultValue="system"
      style={{
        gridTemplateColumns: `repeat(${options.length}, 1fr)`,
      }}
    >
      {options.map((option) => (
        <ChoiceboxItem key={option.id} value={option.id}>
          <ChoiceboxItemHeader>
            <ChoiceboxItemTitle>
              {option.label}
            </ChoiceboxItemTitle>
            <ChoiceboxItemDescription>
              {option.description}
            </ChoiceboxItemDescription>
          </ChoiceboxItemHeader>
          <ChoiceboxIndicator />
        </ChoiceboxItem>
      ))}
    </Choicebox>
  )
}
```

##### Controlled

Manages the selected value externally with React state.

```tsx
"use client"

import { useState } from "react"
import {
  Choicebox,
  ChoiceboxIndicator,
  ChoiceboxItem,
  ChoiceboxItemDescription,
  ChoiceboxItemHeader,
  ChoiceboxItemTitle,
} from "@/components/kibo-ui/choicebox"

export function Example() {
  const [value, setValue] = useState("weekly")

  return (
    <div>
      <p>Selected: {value}</p>
      <Choicebox value={value} onValueChange={setValue}>
        <ChoiceboxItem value="daily">
          <ChoiceboxItemHeader>
            <ChoiceboxItemTitle>Daily</ChoiceboxItemTitle>
            <ChoiceboxItemDescription>
              Receive a digest every day.
            </ChoiceboxItemDescription>
          </ChoiceboxItemHeader>
          <ChoiceboxIndicator />
        </ChoiceboxItem>
        <ChoiceboxItem value="weekly">
          <ChoiceboxItemHeader>
            <ChoiceboxItemTitle>Weekly</ChoiceboxItemTitle>
            <ChoiceboxItemDescription>
              Receive a digest every week.
            </ChoiceboxItemDescription>
          </ChoiceboxItemHeader>
          <ChoiceboxIndicator />
        </ChoiceboxItem>
      </Choicebox>
    </div>
  )
}
```
