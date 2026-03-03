### Color Picker

> Allows users to select a color. Modeled after the color picker in Figma.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/color-picker.json"
```

#### Dependencies

External packages installed automatically:
- `color` — color conversion and manipulation
- `radix-ui` — accessible slider primitives for hue and alpha
- `lucide-react` — icon for the eyedropper button

#### Anatomy

```tsx
import {
  ColorPicker,
  ColorPickerSelection,
  ColorPickerHue,
  ColorPickerAlpha,
  ColorPickerEyeDropper,
  ColorPickerOutput,
  ColorPickerFormat,
  useColorPicker,
} from "@/components/kibo-ui/color-picker"
```

| Component | Description |
|-----------|-------------|
| `ColorPicker` | Root provider. Manages color state via context. |
| `ColorPickerSelection` | 2D area for picking saturation and lightness. |
| `ColorPickerHue` | Slider for selecting hue (0-360). |
| `ColorPickerAlpha` | Slider for selecting opacity (0-100). |
| `ColorPickerEyeDropper` | Button that opens the browser EyeDropper API. |
| `ColorPickerOutput` | Dropdown to switch color format (HEX, RGB, CSS, HSL). |
| `ColorPickerFormat` | Displays the current color in the selected format. |

| Hook | Description |
|------|-------------|
| `useColorPicker` | Returns the current color state and setters from context. |

| Type | Description |
|------|-------------|
| `ColorPickerContextValue` | Shape returned by `useColorPicker`. |

```ts
type ColorPickerContextValue = {
  hue: number
  saturation: number
  lightness: number
  alpha: number
  mode: string
  setHue: (hue: number) => void
  setSaturation: (saturation: number) => void
  setLightness: (lightness: number) => void
  setAlpha: (alpha: number) => void
  setMode: (mode: string) => void
}
```

#### Props

**ColorPicker**

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `value` | `string \| number[] \| object` | — | Controlled color value (any format accepted by the `color` library). |
| `defaultValue` | `string \| number[] \| object` | `"#000000"` | Initial color when uncontrolled. |
| `onChange` | `(value: [number, number, number, number]) => void` | — | Called with an RGBA array when the color changes. |

**ColorPickerSelection**

Accepts standard `HTMLDivElement` attributes.

**ColorPickerHue**

Extends Radix `Slider.Root` props.

**ColorPickerAlpha**

Extends Radix `Slider.Root` props.

**ColorPickerEyeDropper**

Extends shadcn `Button` props.

**ColorPickerOutput**

Extends shadcn `SelectTrigger` props.

**ColorPickerFormat**

Accepts standard `HTMLDivElement` attributes.

#### Usage

##### Basic

```tsx
import {
  ColorPicker,
  ColorPickerSelection,
  ColorPickerHue,
  ColorPickerAlpha,
  ColorPickerEyeDropper,
  ColorPickerOutput,
  ColorPickerFormat,
} from "@/components/kibo-ui/color-picker"

export function Example() {
  return (
    <ColorPicker
      className="max-w-sm rounded-md border p-4"
    >
      <ColorPickerSelection />
      <div className="flex items-center gap-4">
        <ColorPickerEyeDropper />
        <div className="grid w-full gap-1">
          <ColorPickerHue />
          <ColorPickerAlpha />
        </div>
      </div>
      <div className="flex items-center gap-2">
        <ColorPickerOutput />
        <ColorPickerFormat />
      </div>
    </ColorPicker>
  )
}
```

##### Controlled

Track the selected color in parent state via the `onChange` callback.

```tsx
"use client"

import { useState } from "react"
import {
  ColorPicker,
  ColorPickerSelection,
  ColorPickerHue,
  ColorPickerAlpha,
  ColorPickerOutput,
  ColorPickerFormat,
} from "@/components/kibo-ui/color-picker"

export function Example() {
  const [rgba, setRgba] = useState<
    [number, number, number, number]
  >([66, 133, 244, 1])

  return (
    <div className="space-y-4">
      <ColorPicker
        defaultValue="#4285F4"
        onChange={setRgba}
        className="max-w-sm rounded-md border p-4"
      >
        <ColorPickerSelection />
        <div className="grid w-full gap-1">
          <ColorPickerHue />
          <ColorPickerAlpha />
        </div>
        <div className="flex items-center gap-2">
          <ColorPickerOutput />
          <ColorPickerFormat />
        </div>
      </ColorPicker>
      <p className="text-sm text-muted-foreground">
        RGBA: {rgba.join(", ")}
      </p>
    </div>
  )
}
```

##### Using the Hook

Access the color state from any descendant component via `useColorPicker`.

```tsx
"use client"

import {
  ColorPicker,
  ColorPickerSelection,
  ColorPickerHue,
  useColorPicker,
} from "@/components/kibo-ui/color-picker"

function Preview() {
  const { hue, saturation, lightness, alpha } =
    useColorPicker()

  const color = `hsla(${hue}, ${saturation}%, ${lightness}%, ${alpha / 100})`

  return (
    <div
      className="h-10 w-10 rounded-full border"
      style={{ backgroundColor: color }}
    />
  )
}

export function Example() {
  return (
    <ColorPicker
      defaultValue="#10B981"
      className="max-w-sm rounded-md border p-4"
    >
      <div className="flex items-center gap-4">
        <Preview />
        <div className="grid w-full gap-1">
          <ColorPickerSelection />
          <ColorPickerHue />
        </div>
      </div>
    </ColorPicker>
  )
}
```

##### Minimal (Hue Only)

Compose only the sub-components you need.

```tsx
import {
  ColorPicker,
  ColorPickerHue,
  ColorPickerFormat,
  ColorPickerOutput,
} from "@/components/kibo-ui/color-picker"

export function Example() {
  return (
    <ColorPicker
      defaultValue="#FF6600"
      className="max-w-xs space-y-2 rounded-md border p-4"
    >
      <ColorPickerHue />
      <div className="flex items-center gap-2">
        <ColorPickerOutput />
        <ColorPickerFormat />
      </div>
    </ColorPicker>
  )
}
```
