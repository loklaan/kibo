### QR Code

> QR Code is a component that generates a QR code from a string.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/qr-code.json"
```

#### Dependencies

External packages installed automatically:
- `qrcode` — generates QR code data
- `culori` — converts oklch CSS color values to hex

#### Anatomy

```tsx
import { QRCode } from "@/components/kibo-ui/qr-code"
```

| Component | Description |
|-----------|-------------|
| `QRCode` | Generates and renders a QR code as an inline SVG. |

A server-compatible export is also available:

```tsx
import { QRCode } from "@/components/kibo-ui/qr-code/server"
```

The server export is an async component that requires explicit
`foreground` and `background` hex color values since it cannot
read CSS variables from the DOM.

#### Props

**QRCode** (client)

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `data` | `string` | — | The string to encode as a QR code. |
| `foreground` | `string` | CSS `--foreground` | Foreground color in oklch format. |
| `background` | `string` | CSS `--background` | Background color in oklch format. |
| `robustness` | `"L" \| "M" \| "Q" \| "H"` | `"M"` | Error correction level. Higher levels resist more damage but reduce capacity. |

**QRCode** (server)

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `data` | `string` | — | The string to encode as a QR code. |
| `foreground` | `string` | — | Foreground color as a hex value (required). |
| `background` | `string` | — | Background color as a hex value (required). |
| `robustness` | `"L" \| "M" \| "Q" \| "H"` | `"M"` | Error correction level. Higher levels resist more damage but reduce capacity. |

#### Usage

##### Basic

```tsx
"use client"

import { QRCode } from "@/components/kibo-ui/qr-code"

export function Example() {
  return <QRCode data="https://example.com" />
}
```

##### Custom Styling

The QR code is wrapped in a div, so you can pass a custom
`className` to style it.

```tsx
"use client"

import { QRCode } from "@/components/kibo-ui/qr-code"

export function Example() {
  return (
    <QRCode
      className="size-48 rounded border bg-white p-4 shadow-xs"
      data="https://example.com"
    />
  )
}
```

##### Robustness Levels

The `robustness` prop controls the error correction level. `"L"`
offers ~7% recovery, `"M"` ~15%, `"Q"` ~25%, and `"H"` ~30%.

```tsx
"use client"

import { QRCode } from "@/components/kibo-ui/qr-code"

export function Example() {
  return (
    <div className="grid grid-cols-4 gap-4">
      <div className="flex flex-col items-center gap-2">
        <QRCode data="https://example.com" robustness="L" />
        <p className="text-sm text-muted-foreground">L</p>
      </div>
      <div className="flex flex-col items-center gap-2">
        <QRCode data="https://example.com" robustness="M" />
        <p className="text-sm text-muted-foreground">M</p>
      </div>
      <div className="flex flex-col items-center gap-2">
        <QRCode data="https://example.com" robustness="Q" />
        <p className="text-sm text-muted-foreground">Q</p>
      </div>
      <div className="flex flex-col items-center gap-2">
        <QRCode data="https://example.com" robustness="H" />
        <p className="text-sm text-muted-foreground">H</p>
      </div>
    </div>
  )
}
```

##### Server Component

Use the server export when rendering in a React Server Component.
You must provide explicit hex color values for `foreground` and
`background` since CSS variables are not accessible on the server.

```tsx
import { QRCode } from "@/components/kibo-ui/qr-code/server"

export function Example() {
  return (
    <QRCode
      data="https://example.com"
      foreground="#111111"
      background="#eeeeee"
    />
  )
}
```
