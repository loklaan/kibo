### Dialog Stack

> Composable stacked dialogs, useful for creating a wizard, nested form or multi-step process.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/dialog-stack.json"
```

#### Dependencies

External packages installed automatically:
- `@radix-ui/react-use-controllable-state` — controllable open state
- `radix-ui` — portal for rendering dialogs outside the DOM tree

#### Anatomy

```tsx
import {
  DialogStack,
  DialogStackTrigger,
  DialogStackOverlay,
  DialogStackBody,
  DialogStackContent,
  DialogStackHeader,
  DialogStackTitle,
  DialogStackDescription,
  DialogStackFooter,
  DialogStackNext,
  DialogStackPrevious,
} from "@/components/kibo-ui/dialog-stack"
```

| Component | Description |
|-----------|-------------|
| `DialogStack` | Root provider. Manages open state and active dialog index via context. |
| `DialogStackTrigger` | Button that opens the dialog stack. |
| `DialogStackOverlay` | Full-screen backdrop. Closes the stack on click. |
| `DialogStackBody` | Container for all `DialogStackContent` panels. Renders via a portal. |
| `DialogStackContent` | Individual dialog panel. Stacks visually behind or in front of siblings. |
| `DialogStackHeader` | Layout wrapper for the title and description area. |
| `DialogStackTitle` | Heading rendered as an `h2`. |
| `DialogStackDescription` | Muted paragraph below the title. |
| `DialogStackFooter` | Layout wrapper for action buttons at the bottom of a dialog. |
| `DialogStackNext` | Button that advances to the next dialog in the stack. |
| `DialogStackPrevious` | Button that returns to the previous dialog in the stack. |

#### Props

**DialogStack**

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `open` | `boolean` | — | Controlled open state. |
| `defaultOpen` | `boolean` | `false` | Initial open state when uncontrolled. |
| `onOpenChange` | `(open: boolean) => void` | — | Called when the open state changes. |
| `clickable` | `boolean` | `false` | When `true`, clicking a background dialog navigates to it. |

**DialogStackTrigger**

Extends `HTMLButtonElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `asChild` | `boolean` | `false` | Merge props onto the child element instead of rendering a button. |

**DialogStackOverlay**

Accepts standard `HTMLDivElement` attributes.

**DialogStackBody**

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `children` | `ReactElement \| ReactElement[]` | — | One or more `DialogStackContent` elements. |

**DialogStackContent**

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `index` | `number` | `0` | Position in the stack. Assigned automatically by `DialogStackBody`. |
| `offset` | `number` | `10` | Pixel offset between stacked dialogs. |

**DialogStackHeader**

Accepts standard `HTMLDivElement` attributes.

**DialogStackTitle**

Accepts standard `HTMLHeadingElement` attributes.

**DialogStackDescription**

Accepts standard `HTMLParagraphElement` attributes.

**DialogStackFooter**

Accepts standard `HTMLDivElement` attributes.

**DialogStackNext**

Extends `HTMLButtonElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `asChild` | `boolean` | `false` | Merge props onto the child element instead of rendering a button. |

**DialogStackPrevious**

Extends `HTMLButtonElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `asChild` | `boolean` | `false` | Merge props onto the child element instead of rendering a button. |

#### Usage

##### Basic

```tsx
"use client"

import {
  DialogStack,
  DialogStackBody,
  DialogStackContent,
  DialogStackDescription,
  DialogStackFooter,
  DialogStackHeader,
  DialogStackNext,
  DialogStackOverlay,
  DialogStackPrevious,
  DialogStackTitle,
  DialogStackTrigger,
} from "@/components/kibo-ui/dialog-stack"

export function Example() {
  return (
    <DialogStack>
      <DialogStackTrigger>Open</DialogStackTrigger>
      <DialogStackOverlay />

      <DialogStackBody>
        <DialogStackContent>
          <DialogStackHeader>
            <DialogStackTitle>Step 1</DialogStackTitle>
            <DialogStackDescription>
              Enter your details.
            </DialogStackDescription>
          </DialogStackHeader>
          <DialogStackFooter className="justify-end">
            <DialogStackNext>Next</DialogStackNext>
          </DialogStackFooter>
        </DialogStackContent>

        <DialogStackContent>
          <DialogStackHeader>
            <DialogStackTitle>Step 2</DialogStackTitle>
            <DialogStackDescription>
              Review your information.
            </DialogStackDescription>
          </DialogStackHeader>
          <DialogStackFooter className="justify-between">
            <DialogStackPrevious>Back</DialogStackPrevious>
            <DialogStackNext>Next</DialogStackNext>
          </DialogStackFooter>
        </DialogStackContent>

        <DialogStackContent>
          <DialogStackHeader>
            <DialogStackTitle>Step 3</DialogStackTitle>
            <DialogStackDescription>
              Confirm and submit.
            </DialogStackDescription>
          </DialogStackHeader>
          <DialogStackFooter className="justify-start">
            <DialogStackPrevious>Back</DialogStackPrevious>
          </DialogStackFooter>
        </DialogStackContent>
      </DialogStackBody>
    </DialogStack>
  )
}
```

##### Clickable Navigation

Enable `clickable` to let users click on background dialogs to navigate directly to them.

```tsx
"use client"

import {
  DialogStack,
  DialogStackBody,
  DialogStackContent,
  DialogStackDescription,
  DialogStackFooter,
  DialogStackHeader,
  DialogStackNext,
  DialogStackOverlay,
  DialogStackPrevious,
  DialogStackTitle,
  DialogStackTrigger,
} from "@/components/kibo-ui/dialog-stack"

export function Example() {
  return (
    <DialogStack clickable>
      <DialogStackTrigger>Open</DialogStackTrigger>
      <DialogStackOverlay />

      <DialogStackBody>
        <DialogStackContent>
          <DialogStackHeader>
            <DialogStackTitle>First</DialogStackTitle>
            <DialogStackDescription>
              Click a background dialog to jump to it.
            </DialogStackDescription>
          </DialogStackHeader>
          <DialogStackFooter className="justify-end">
            <DialogStackNext>Next</DialogStackNext>
          </DialogStackFooter>
        </DialogStackContent>

        <DialogStackContent>
          <DialogStackHeader>
            <DialogStackTitle>Second</DialogStackTitle>
            <DialogStackDescription>
              You can navigate forward or back.
            </DialogStackDescription>
          </DialogStackHeader>
          <DialogStackFooter className="justify-between">
            <DialogStackPrevious>Back</DialogStackPrevious>
            <DialogStackNext>Next</DialogStackNext>
          </DialogStackFooter>
        </DialogStackContent>

        <DialogStackContent>
          <DialogStackHeader>
            <DialogStackTitle>Third</DialogStackTitle>
            <DialogStackDescription>
              Final step.
            </DialogStackDescription>
          </DialogStackHeader>
          <DialogStackFooter className="justify-start">
            <DialogStackPrevious>Back</DialogStackPrevious>
          </DialogStackFooter>
        </DialogStackContent>
      </DialogStackBody>
    </DialogStack>
  )
}
```

##### Controlled

Manage the open state externally with `open` and `onOpenChange`.

```tsx
"use client"

import { useState } from "react"
import {
  DialogStack,
  DialogStackBody,
  DialogStackContent,
  DialogStackDescription,
  DialogStackFooter,
  DialogStackHeader,
  DialogStackNext,
  DialogStackOverlay,
  DialogStackPrevious,
  DialogStackTitle,
} from "@/components/kibo-ui/dialog-stack"

export function Example() {
  const [open, setOpen] = useState(false)

  return (
    <>
      <button onClick={() => setOpen(true)}>
        Toggle Dialog
      </button>

      <DialogStack open={open} onOpenChange={setOpen}>
        <DialogStackOverlay />
        <DialogStackBody>
          <DialogStackContent>
            <DialogStackHeader>
              <DialogStackTitle>Step 1</DialogStackTitle>
              <DialogStackDescription>
                Controlled via parent state.
              </DialogStackDescription>
            </DialogStackHeader>
            <DialogStackFooter className="justify-end">
              <DialogStackNext>Next</DialogStackNext>
            </DialogStackFooter>
          </DialogStackContent>

          <DialogStackContent>
            <DialogStackHeader>
              <DialogStackTitle>Step 2</DialogStackTitle>
              <DialogStackDescription>
                Navigate between steps.
              </DialogStackDescription>
            </DialogStackHeader>
            <DialogStackFooter className="justify-between">
              <DialogStackPrevious>Back</DialogStackPrevious>
              <DialogStackNext>Next</DialogStackNext>
            </DialogStackFooter>
          </DialogStackContent>

          <DialogStackContent>
            <DialogStackHeader>
              <DialogStackTitle>Step 3</DialogStackTitle>
              <DialogStackDescription>
                Final step.
              </DialogStackDescription>
            </DialogStackHeader>
            <DialogStackFooter className="justify-start">
              <DialogStackPrevious>Back</DialogStackPrevious>
            </DialogStackFooter>
          </DialogStackContent>
        </DialogStackBody>
      </DialogStack>
    </>
  )
}
```

##### With asChild Trigger

Use `asChild` on the trigger to render a custom element.

```tsx
"use client"

import {
  DialogStack,
  DialogStackBody,
  DialogStackContent,
  DialogStackDescription,
  DialogStackFooter,
  DialogStackHeader,
  DialogStackNext,
  DialogStackOverlay,
  DialogStackPrevious,
  DialogStackTitle,
  DialogStackTrigger,
} from "@/components/kibo-ui/dialog-stack"
import { Button } from "@/components/ui/button"

export function Example() {
  return (
    <DialogStack>
      <DialogStackTrigger asChild>
        <Button variant="outline">Show me</Button>
      </DialogStackTrigger>
      <DialogStackOverlay />

      <DialogStackBody>
        <DialogStackContent>
          <DialogStackHeader>
            <DialogStackTitle>Welcome</DialogStackTitle>
            <DialogStackDescription>
              Triggered from a shadcn Button.
            </DialogStackDescription>
          </DialogStackHeader>
          <DialogStackFooter className="justify-end">
            <DialogStackNext asChild>
              <Button variant="outline">Next</Button>
            </DialogStackNext>
          </DialogStackFooter>
        </DialogStackContent>

        <DialogStackContent>
          <DialogStackHeader>
            <DialogStackTitle>Almost done</DialogStackTitle>
            <DialogStackDescription>
              One more step to go.
            </DialogStackDescription>
          </DialogStackHeader>
          <DialogStackFooter className="justify-between">
            <DialogStackPrevious asChild>
              <Button variant="outline">Previous</Button>
            </DialogStackPrevious>
            <DialogStackNext asChild>
              <Button variant="outline">Next</Button>
            </DialogStackNext>
          </DialogStackFooter>
        </DialogStackContent>

        <DialogStackContent>
          <DialogStackHeader>
            <DialogStackTitle>All done</DialogStackTitle>
            <DialogStackDescription>
              That's the last dialog.
            </DialogStackDescription>
          </DialogStackHeader>
          <DialogStackFooter className="justify-start">
            <DialogStackPrevious asChild>
              <Button variant="outline">Previous</Button>
            </DialogStackPrevious>
          </DialogStackFooter>
        </DialogStackContent>
      </DialogStackBody>
    </DialogStack>
  )
}
```
