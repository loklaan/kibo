### Image Zoom

> A component that allows you to zoom in on an image.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/image-zoom.json"
```

#### Dependencies

External packages installed automatically:
- `react-medium-image-zoom` — provides the zoom behavior and dialog overlay

#### Anatomy

```tsx
import { ImageZoom } from "@/components/kibo-ui/image-zoom"
```

| Component | Description |
|-----------|-------------|
| `ImageZoom` | Zoomable wrapper. Place any image or element with `role="img"` inside as children. |

#### Props

**ImageZoom**

Extends `react-medium-image-zoom` `UncontrolledProps`.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `isZoomed` | `boolean` | `undefined` | Controls the zoom state for controlled usage. |
| `onZoomChange` | `(value: boolean) => void` | — | Called when the zoom state changes. |
| `className` | `string` | `undefined` | Class name applied to the outer wrapper div. |
| `backdropClassName` | `string` | `undefined` | Class name applied to the zoom dialog overlay. |
| `zoomMargin` | `number` | `0` | Margin in pixels around the zoomed image. |
| `zoomImg` | `ImgHTMLAttributes<HTMLImageElement>` | — | Attributes for a separate high-resolution image shown when zoomed. |
| `IconZoom` | `React.ElementType` | — | Custom icon component for the zoom-in button. |
| `IconUnzoom` | `React.ElementType` | — | Custom icon component for the zoom-out button. |
| `canSwipeToUnzoom` | `boolean` | `true` | Enables swipe-to-unzoom on touch devices. |
| `swipeToUnzoomThreshold` | `number` | `100` | Swipe distance in pixels required to trigger unzoom. |
| `wrapElement` | `"div" \| "span"` | `"div"` | HTML element used by the inner zoom wrapper. |
| `isDisabled` | `boolean` | `false` | Disables the zoom interaction entirely. |
| `a11yNameButtonZoom` | `string` | `"Zoom image"` | Accessible label for the zoom-in button. |
| `a11yNameButtonUnzoom` | `string` | `"Minimize image"` | Accessible label for the zoom-out button. |

#### Usage

##### Basic

```tsx
import { ImageZoom } from "@/components/kibo-ui/image-zoom"

export function Example() {
  return (
    <ImageZoom>
      <img
        src="/photo.jpg"
        alt="A scenic landscape"
        className="h-auto w-96"
      />
    </ImageZoom>
  )
}
```

##### Custom Backdrop

Use `backdropClassName` to override the zoom dialog overlay
styles, such as setting a solid dark background.

```tsx
import { ImageZoom } from "@/components/kibo-ui/image-zoom"

export function Example() {
  return (
    <ImageZoom
      backdropClassName={
        '[&_[data-rmiz-modal-overlay="visible"]]:bg-black/80'
      }
    >
      <img
        src="/photo.jpg"
        alt="A scenic landscape"
        className="h-auto w-96"
      />
    </ImageZoom>
  )
}
```

##### Custom Zoom Margin

Set `zoomMargin` to add padding around the zoomed image,
preventing it from touching the viewport edges.

```tsx
import { ImageZoom } from "@/components/kibo-ui/image-zoom"

export function Example() {
  return (
    <ImageZoom zoomMargin={100}>
      <img
        src="/photo.jpg"
        alt="A scenic landscape"
        className="h-auto w-96"
      />
    </ImageZoom>
  )
}
```

##### Controlled Zoom

Use `isZoomed` and `onZoomChange` to control the zoom state
programmatically.

```tsx
"use client"

import { ImageZoom } from "@/components/kibo-ui/image-zoom"
import { useState } from "react"

export function Example() {
  const [zoomed, setZoomed] = useState(false)

  return (
    <div>
      <button onClick={() => setZoomed(true)}>
        Open zoom
      </button>
      <ImageZoom
        isZoomed={zoomed}
        onZoomChange={setZoomed}
      >
        <img
          src="/photo.jpg"
          alt="A scenic landscape"
          className="h-auto w-96"
        />
      </ImageZoom>
    </div>
  )
}
```
