### Image Crop

> Helps you crop images to a specific size or aspect ratio.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/image-crop.json"
```

#### Dependencies

External packages installed automatically:
- `react-image-crop` — interactive image cropping UI
- `lucide-react` — icon primitives
- `radix-ui` — slot primitive for `asChild` support

#### Anatomy

```tsx
import {
  ImageCrop,
  ImageCropContent,
  ImageCropApply,
  ImageCropReset,
  Cropper,
} from "@/components/kibo-ui/image-crop"
```

| Component | Description |
|-----------|-------------|
| `ImageCrop` | Root provider. Reads the `File`, manages crop state, and provides context to children. |
| `ImageCropContent` | Renders the interactive crop area with the image preview. |
| `ImageCropApply` | Button that applies the current crop and calls `onCrop` with the resulting data URL. |
| `ImageCropReset` | Button that resets the crop region to its initial centered position. |
| `Cropper` | Convenience wrapper combining `ImageCrop` and `ImageCropContent` into a single component. |

#### Props

**ImageCrop**

Extends `react-image-crop` `ReactCropProps` (excluding `onChange`, `onComplete`, and `children`).

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `file` | `File` | — | The image file to crop. |
| `maxImageSize` | `number` | `5242880` | Maximum output size in bytes (default 5 MB). Automatically recompresses if exceeded. |
| `onCrop` | `(croppedImage: string) => void` | — | Called with the cropped image as a PNG data URL when the crop is applied. |
| `onChange` | `(pixelCrop: PixelCrop, percentCrop: PercentCrop) => void` | — | Called on every crop region change. |
| `onComplete` | `(pixelCrop: PixelCrop, percentCrop: PercentCrop) => void` | — | Called when the user finishes a crop interaction. |
| `aspect` | `number` | `undefined` | Forces a fixed aspect ratio (e.g., `1` for square, `16/9` for widescreen). |
| `circularCrop` | `boolean` | `false` | Renders the crop region as a circle. |
| `minWidth` | `number` | `undefined` | Minimum crop width in pixels. |
| `minHeight` | `number` | `undefined` | Minimum crop height in pixels. |
| `maxWidth` | `number` | `undefined` | Maximum crop width in pixels. |
| `maxHeight` | `number` | `undefined` | Maximum crop height in pixels. |
| `keepSelection` | `boolean` | `undefined` | Prevents the crop selection from being removed when clicking outside. |
| `disabled` | `boolean` | `undefined` | Disables all crop interaction. |
| `locked` | `boolean` | `undefined` | Locks the crop region so it cannot be resized, only moved. |
| `ruleOfThirds` | `boolean` | `undefined` | Displays rule-of-thirds grid lines over the crop region. |

**ImageCropContent**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `className` | `string` | `undefined` | CSS class applied to the crop container. |
| `style` | `CSSProperties` | `undefined` | Inline styles applied to the crop container. |

**ImageCropApply**

Extends `HTMLButtonElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `asChild` | `boolean` | `false` | Merges props onto the child element instead of rendering a default button. |

**ImageCropReset**

Extends `HTMLButtonElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `asChild` | `boolean` | `false` | Merges props onto the child element instead of rendering a default button. |

**Cropper**

Extends `react-image-crop` `ReactCropProps` (excluding `onChange`).

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `file` | `File` | — | The image file to crop. |
| `maxImageSize` | `number` | `5242880` | Maximum output size in bytes. |
| `onCrop` | `(croppedImage: string) => void` | — | Called with the cropped image as a PNG data URL. |
| `onChange` | `(pixelCrop: PixelCrop, percentCrop: PercentCrop) => void` | — | Called on every crop region change. |

#### Usage

##### Basic

```tsx
"use client"

import { useState, type ChangeEvent } from "react"
import {
  ImageCrop,
  ImageCropContent,
  ImageCropApply,
  ImageCropReset,
} from "@/components/kibo-ui/image-crop"

export function Example() {
  const [file, setFile] = useState<File | null>(null)
  const [cropped, setCropped] = useState<string | null>(null)

  const handleFileChange = (
    e: ChangeEvent<HTMLInputElement>
  ) => {
    const selected = e.target.files?.[0]
    if (selected) {
      setFile(selected)
      setCropped(null)
    }
  }

  if (!file) {
    return (
      <input
        type="file"
        accept="image/*"
        onChange={handleFileChange}
      />
    )
  }

  if (cropped) {
    return <img src={cropped} alt="Cropped" />
  }

  return (
    <ImageCrop file={file} onCrop={setCropped}>
      <ImageCropContent />
      <div style={{ display: "flex", gap: 8 }}>
        <ImageCropApply />
        <ImageCropReset />
      </div>
    </ImageCrop>
  )
}
```

##### Fixed Aspect Ratio

Locks the crop region to a 1:1 square aspect ratio.

```tsx
"use client"

import { useState, type ChangeEvent } from "react"
import {
  ImageCrop,
  ImageCropContent,
  ImageCropApply,
  ImageCropReset,
} from "@/components/kibo-ui/image-crop"

export function Example() {
  const [file, setFile] = useState<File | null>(null)
  const [cropped, setCropped] = useState<string | null>(null)

  const handleFileChange = (
    e: ChangeEvent<HTMLInputElement>
  ) => {
    const selected = e.target.files?.[0]
    if (selected) {
      setFile(selected)
      setCropped(null)
    }
  }

  if (!file) {
    return (
      <input
        type="file"
        accept="image/*"
        onChange={handleFileChange}
      />
    )
  }

  if (cropped) {
    return <img src={cropped} alt="Cropped" />
  }

  return (
    <ImageCrop
      file={file}
      aspect={1}
      maxImageSize={1024 * 1024}
      onCrop={setCropped}
    >
      <ImageCropContent className="max-w-md" />
      <div style={{ display: "flex", gap: 8 }}>
        <ImageCropApply />
        <ImageCropReset />
      </div>
    </ImageCrop>
  )
}
```

##### Circular Crop

Renders the crop region as a circle, suitable for avatar or profile picture selection.

```tsx
"use client"

import { useState, type ChangeEvent } from "react"
import {
  ImageCrop,
  ImageCropContent,
  ImageCropApply,
  ImageCropReset,
} from "@/components/kibo-ui/image-crop"

export function Example() {
  const [file, setFile] = useState<File | null>(null)
  const [cropped, setCropped] = useState<string | null>(null)

  const handleFileChange = (
    e: ChangeEvent<HTMLInputElement>
  ) => {
    const selected = e.target.files?.[0]
    if (selected) {
      setFile(selected)
      setCropped(null)
    }
  }

  if (!file) {
    return (
      <input
        type="file"
        accept="image/*"
        onChange={handleFileChange}
      />
    )
  }

  if (cropped) {
    return (
      <img
        src={cropped}
        alt="Cropped"
        style={{ borderRadius: "50%" }}
      />
    )
  }

  return (
    <ImageCrop
      file={file}
      aspect={1}
      circularCrop
      maxImageSize={1024 * 1024}
      onCrop={setCropped}
    >
      <ImageCropContent className="max-w-md" />
      <div style={{ display: "flex", gap: 8 }}>
        <ImageCropApply />
        <ImageCropReset />
      </div>
    </ImageCrop>
  )
}
```

##### Custom Buttons with asChild

Uses the `asChild` prop to render custom button elements instead of the default icon buttons.

```tsx
"use client"

import { useState, type ChangeEvent } from "react"
import {
  ImageCrop,
  ImageCropContent,
  ImageCropApply,
  ImageCropReset,
} from "@/components/kibo-ui/image-crop"

export function Example() {
  const [file, setFile] = useState<File | null>(null)
  const [cropped, setCropped] = useState<string | null>(null)

  const handleFileChange = (
    e: ChangeEvent<HTMLInputElement>
  ) => {
    const selected = e.target.files?.[0]
    if (selected) {
      setFile(selected)
      setCropped(null)
    }
  }

  if (!file) {
    return (
      <input
        type="file"
        accept="image/*"
        onChange={handleFileChange}
      />
    )
  }

  if (cropped) {
    return <img src={cropped} alt="Cropped" />
  }

  return (
    <ImageCrop
      file={file}
      aspect={1}
      maxImageSize={1024 * 1024}
      onCrop={setCropped}
    >
      <ImageCropContent className="max-w-md" />
      <div style={{ display: "flex", gap: 8 }}>
        <ImageCropApply asChild>
          <button type="button">Apply Crop</button>
        </ImageCropApply>
        <ImageCropReset asChild>
          <button type="button">Reset</button>
        </ImageCropReset>
      </div>
    </ImageCrop>
  )
}
```
