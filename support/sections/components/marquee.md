### Marquee

> Marquees are a great way to show a list of items in a horizontal scrolling motion.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/marquee.json"
```

#### Dependencies

External packages installed automatically:
- `react-fast-marquee` — horizontal scrolling animation engine

#### Anatomy

```tsx
import {
  Marquee,
  MarqueeContent,
  MarqueeFade,
  MarqueeItem,
} from "@/components/kibo-ui/marquee"
```

| Component | Description |
|-----------|-------------|
| `Marquee` | Root container. Provides relative positioning and hides overflow. |
| `MarqueeContent` | Scrolling track powered by react-fast-marquee. Wraps all items. |
| `MarqueeFade` | Gradient fade overlay on the left or right edge. |
| `MarqueeItem` | Individual item in the scrolling track. |

#### Props

**Marquee**

Accepts standard `HTMLDivElement` attributes.

**MarqueeContent**

Extends `react-fast-marquee` props.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `speed` | `number` | `50` | Scroll speed in pixels per second. |
| `direction` | `"left" \| "right" \| "up" \| "down"` | `"left"` | Scroll direction. |
| `delay` | `number` | `0` | Delay before animation starts, in seconds. |
| `loop` | `number` | `0` | Number of loops. `0` means infinite. |
| `autoFill` | `boolean` | `true` | Fills the track with copies of children to prevent gaps. |
| `pauseOnHover` | `boolean` | `true` | Pauses scrolling when the user hovers. |
| `pauseOnClick` | `boolean` | `false` | Pauses scrolling when the user clicks. |
| `play` | `boolean` | `true` | Controls whether the animation is running. |
| `gradient` | `boolean` | `false` | Renders built-in gradient overlays on the edges. |
| `gradientWidth` | `number \| string` | `200` | Width of the built-in gradient overlay. |

**MarqueeFade**

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `side` | `"left" \| "right"` | — | Which edge to position the fade gradient on. Required. |

**MarqueeItem**

Accepts standard `HTMLDivElement` attributes.

#### Usage

##### Basic

```tsx
"use client"

import {
  Marquee,
  MarqueeContent,
  MarqueeFade,
  MarqueeItem,
} from "@/components/kibo-ui/marquee"

export function Example() {
  return (
    <Marquee>
      <MarqueeFade side="left" />
      <MarqueeFade side="right" />
      <MarqueeContent>
        <MarqueeItem className="h-32 w-32">
          <img
            alt="Avatar 1"
            className="rounded-full"
            src="/avatars/alice.jpg"
          />
        </MarqueeItem>
        <MarqueeItem className="h-32 w-32">
          <img
            alt="Avatar 2"
            className="rounded-full"
            src="/avatars/bob.jpg"
          />
        </MarqueeItem>
        <MarqueeItem className="h-32 w-32">
          <img
            alt="Avatar 3"
            className="rounded-full"
            src="/avatars/carol.jpg"
          />
        </MarqueeItem>
      </MarqueeContent>
    </Marquee>
  )
}
```

##### Without Fade

Omits the `MarqueeFade` components for a clean edge-to-edge scroll.

```tsx
"use client"

import {
  Marquee,
  MarqueeContent,
  MarqueeItem,
} from "@/components/kibo-ui/marquee"

export function Example() {
  return (
    <Marquee>
      <MarqueeContent>
        <MarqueeItem className="h-16 w-16">
          <img
            alt="Logo 1"
            className="rounded-full"
            src="/logos/acme.png"
          />
        </MarqueeItem>
        <MarqueeItem className="h-16 w-16">
          <img
            alt="Logo 2"
            className="rounded-full"
            src="/logos/globex.png"
          />
        </MarqueeItem>
        <MarqueeItem className="h-16 w-16">
          <img
            alt="Logo 3"
            className="rounded-full"
            src="/logos/initech.png"
          />
        </MarqueeItem>
      </MarqueeContent>
    </Marquee>
  )
}
```

##### Single Loop with No Auto-fill

Plays the scroll once and stops. Disables auto-fill and pause-on-hover.

```tsx
"use client"

import {
  Marquee,
  MarqueeContent,
  MarqueeFade,
  MarqueeItem,
} from "@/components/kibo-ui/marquee"

export function Example() {
  return (
    <Marquee>
      <MarqueeFade side="left" />
      <MarqueeFade side="right" />
      <MarqueeContent
        autoFill={false}
        loop={1}
        pauseOnHover={false}
      >
        <MarqueeItem className="h-16 w-16">
          <img
            alt="Photo 1"
            className="rounded-full"
            src="/photos/1.jpg"
          />
        </MarqueeItem>
        <MarqueeItem className="h-16 w-16">
          <img
            alt="Photo 2"
            className="rounded-full"
            src="/photos/2.jpg"
          />
        </MarqueeItem>
        <MarqueeItem className="h-16 w-16">
          <img
            alt="Photo 3"
            className="rounded-full"
            src="/photos/3.jpg"
          />
        </MarqueeItem>
      </MarqueeContent>
    </Marquee>
  )
}
```

##### Overlapping Items

Uses negative margin on items to create an overlapping stacked look.

```tsx
"use client"

import {
  Marquee,
  MarqueeContent,
  MarqueeFade,
  MarqueeItem,
} from "@/components/kibo-ui/marquee"

export function Example() {
  return (
    <Marquee>
      <MarqueeFade side="left" />
      <MarqueeFade side="right" />
      <MarqueeContent>
        <MarqueeItem className="-mx-2 h-16 w-16">
          <img
            alt="User 1"
            className="rounded-full ring-2 ring-background"
            src="/avatars/alice.jpg"
          />
        </MarqueeItem>
        <MarqueeItem className="-mx-2 h-16 w-16">
          <img
            alt="User 2"
            className="rounded-full ring-2 ring-background"
            src="/avatars/bob.jpg"
          />
        </MarqueeItem>
        <MarqueeItem className="-mx-2 h-16 w-16">
          <img
            alt="User 3"
            className="rounded-full ring-2 ring-background"
            src="/avatars/carol.jpg"
          />
        </MarqueeItem>
      </MarqueeContent>
    </Marquee>
  )
}
```
