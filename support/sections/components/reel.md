### Reel

> A composable Reel component that looks like Instagram Stories - a full-height, 9:16 aspect ratio container with video playback and progress indicators.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/reel.json"
```

#### Dependencies

External packages installed automatically:
- `@radix-ui/react-use-controllable-state` — controllable state management
- `motion` — animated transitions between reel items
- `lucide-react` — default icons for playback and navigation controls

#### Anatomy

```tsx
import {
  Reel,
  ReelContent,
  ReelItem,
  ReelVideo,
  ReelImage,
  ReelProgress,
  ReelControls,
  ReelPreviousButton,
  ReelNextButton,
  ReelPlayButton,
  ReelMuteButton,
  ReelNavigation,
  ReelOverlay,
  ReelHeader,
  ReelFooter,
} from "@/components/kibo-ui/reel"

import type { ReelItem as ReelItemType } from "@/components/kibo-ui/reel"
```

| Component | Description |
|-----------|-------------|
| `Reel` | Root provider. Manages playback state and wraps all children in a 9:16 aspect-ratio container. |
| `ReelContent` | Animated content area. Accepts a render function receiving the current item. |
| `ReelItem` | Container for an individual reel slide. |
| `ReelVideo` | Video element with automatic progress tracking. |
| `ReelImage` | Image element with timed progress for image slides. |
| `ReelProgress` | Progress indicator bars at the top, one per item. |
| `ReelControls` | Bottom control bar container with a gradient background. |
| `ReelPreviousButton` | Navigates to the previous item. |
| `ReelNextButton` | Navigates to the next item. |
| `ReelPlayButton` | Toggles play/pause. |
| `ReelMuteButton` | Toggles mute/unmute. |
| `ReelNavigation` | Invisible tap overlay. Tap left half for previous, right half for next. |
| `ReelOverlay` | Non-interactive overlay layer for custom content above the media. |
| `ReelHeader` | Top-positioned container with a gradient background for header content. |
| `ReelFooter` | Bottom-positioned container with a gradient background for footer content. |

| Type | Description |
|------|-------------|
| `ReelItem` | Shape of a single reel data item passed to the `data` prop. |

```ts
type ReelItem = {
  id: string | number
  type: "video" | "image"
  src: string
  duration: number
  alt?: string
  title?: string
  description?: string
}
```

#### Props

**Reel**

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `data` | `ReelItem[]` | — | Array of reel items to display. |
| `defaultIndex` | `number` | `0` | Initial active item index (uncontrolled). |
| `index` | `number` | — | Active item index (controlled). |
| `onIndexChange` | `(index: number) => void` | — | Called when the active index changes. |
| `defaultPlaying` | `boolean` | — | Initial playing state (uncontrolled). Defaults to `autoPlay` value. |
| `playing` | `boolean` | — | Playing state (controlled). |
| `onPlayingChange` | `(playing: boolean) => void` | — | Called when playing state changes. |
| `defaultMuted` | `boolean` | `true` | Initial muted state (uncontrolled). |
| `muted` | `boolean` | — | Muted state (controlled). |
| `onMutedChange` | `(muted: boolean) => void` | — | Called when muted state changes. |
| `autoPlay` | `boolean` | `true` | Starts playback automatically on mount. |

**ReelContent**

Extends `HTMLDivElement` attributes (except `children`).

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `children` | `(item: ReelItem, index: number) => ReactNode` | — | Render function called with the current item and index. |

**ReelItem**

Accepts standard `HTMLDivElement` attributes.

**ReelVideo**

Accepts standard `HTMLVideoElement` attributes.

**ReelImage**

Extends `HTMLImageElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `alt` | `string` | — | Required alt text for the image. |
| `duration` | `number` | `5` | Display duration in seconds before auto-advancing. |

**ReelProgress**

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `children` | `(item: ReelItem, index: number, isActive: boolean, progress: number) => ReactNode` | — | Optional render function for custom progress indicators. |

**ReelControls**

Accepts standard `HTMLDivElement` attributes.

**ReelPreviousButton**

Accepts standard `Button` props from shadcn/ui.

**ReelNextButton**

Accepts standard `Button` props from shadcn/ui.

**ReelPlayButton**

Accepts standard `Button` props from shadcn/ui.

**ReelMuteButton**

Accepts standard `Button` props from shadcn/ui.

**ReelNavigation**

Accepts standard `HTMLButtonElement` attributes.

**ReelOverlay**

Accepts standard `HTMLDivElement` attributes.

**ReelHeader**

Accepts standard `HTMLDivElement` attributes.

**ReelFooter**

Accepts standard `HTMLDivElement` attributes.

#### Usage

##### Basic

```tsx
"use client"

import {
  Reel,
  ReelContent,
  ReelControls,
  ReelItem,
  type ReelItem as ReelItemType,
  ReelMuteButton,
  ReelNavigation,
  ReelNextButton,
  ReelPlayButton,
  ReelPreviousButton,
  ReelProgress,
  ReelVideo,
} from "@/components/kibo-ui/reel"

const reels: ReelItemType[] = [
  {
    id: 1,
    type: "video",
    src: "/videos/demo-1.mp4",
    duration: 6,
    title: "Demo 1",
  },
  {
    id: 2,
    type: "video",
    src: "/videos/demo-2.mp4",
    duration: 6,
    title: "Demo 2",
  },
]

export function Example() {
  return (
    <Reel data={reels}>
      <ReelProgress />
      <ReelContent>
        {(reel) => (
          <ReelItem>
            <ReelVideo src={reel.src} />
          </ReelItem>
        )}
      </ReelContent>
      <ReelNavigation />
      <ReelControls>
        <ReelPreviousButton />
        <div className="flex gap-2">
          <ReelPlayButton />
          <ReelMuteButton />
        </div>
        <ReelNextButton />
      </ReelControls>
    </Reel>
  )
}
```

##### Image Reel

Display a series of images with automatic timed transitions
and footer captions.

```tsx
"use client"

import {
  Reel,
  ReelContent,
  ReelControls,
  ReelFooter,
  ReelImage,
  ReelItem,
  type ReelItem as ReelItemType,
  ReelNavigation,
  ReelNextButton,
  ReelPlayButton,
  ReelPreviousButton,
  ReelProgress,
} from "@/components/kibo-ui/reel"

const slides: ReelItemType[] = [
  {
    id: 1,
    type: "image",
    src: "/images/mountain.jpg",
    alt: "Mountain Adventure",
    title: "Mountain Adventure",
    description: "Exploring the peaks",
    duration: 5,
  },
  {
    id: 2,
    type: "image",
    src: "/images/ocean.jpg",
    alt: "Ocean Waves",
    title: "Ocean Waves",
    description: "Sunset at the beach",
    duration: 5,
  },
]

export function Example() {
  return (
    <Reel data={slides}>
      <ReelProgress />
      <ReelContent>
        {(reel) => (
          <ReelItem>
            <ReelImage
              alt={reel.alt ?? ""}
              duration={reel.duration}
              src={reel.src}
            />
            <ReelFooter className="pb-16">
              <div className="text-white">
                <h3 className="font-semibold text-lg">
                  {reel.title}
                </h3>
                <p className="text-sm opacity-90">
                  {reel.description}
                </p>
              </div>
            </ReelFooter>
          </ReelItem>
        )}
      </ReelContent>
      <ReelNavigation />
      <ReelControls>
        <ReelPreviousButton />
        <ReelPlayButton />
        <ReelNextButton />
      </ReelControls>
    </Reel>
  )
}
```

##### Minimal

A stripped-down reel with only progress bars and tap navigation,
no visible control buttons.

```tsx
"use client"

import {
  Reel,
  ReelContent,
  ReelItem,
  type ReelItem as ReelItemType,
  ReelNavigation,
  ReelProgress,
  ReelVideo,
} from "@/components/kibo-ui/reel"

const reels: ReelItemType[] = [
  {
    id: 1,
    type: "video",
    src: "/videos/clip-1.mp4",
    duration: 6,
    title: "Clip 1",
  },
  {
    id: 2,
    type: "video",
    src: "/videos/clip-2.mp4",
    duration: 6,
    title: "Clip 2",
  },
]

export function Example() {
  return (
    <Reel data={reels}>
      <ReelProgress />
      <ReelContent>
        {(reel) => (
          <ReelItem>
            <ReelVideo src={reel.src} />
          </ReelItem>
        )}
      </ReelContent>
      <ReelNavigation />
    </Reel>
  )
}
```

##### With Header and Footer Overlays

A social-media-style reel with author info in the header and
interaction buttons in the footer.

```tsx
"use client"

import {
  Reel,
  ReelContent,
  ReelFooter,
  ReelHeader,
  ReelItem,
  type ReelItem as ReelItemType,
  ReelProgress,
  ReelVideo,
} from "@/components/kibo-ui/reel"
import { Heart, MessageCircle, Share } from "lucide-react"

const reels: ReelItemType[] = [
  {
    id: 1,
    type: "video",
    src: "/videos/adventure.mp4",
    duration: 6,
    title: "Amazing view",
    description: "Check out this view! #travel",
  },
  {
    id: 2,
    type: "video",
    src: "/videos/sunset.mp4",
    duration: 6,
    title: "Golden hour",
    description: "Sunset vibes #nature",
  },
]

export function Example() {
  return (
    <Reel data={reels}>
      <ReelProgress />
      <ReelContent>
        {(reel) => (
          <ReelItem>
            <ReelVideo src={reel.src} />
            <ReelHeader>
              <div className="flex items-center gap-2">
                <div className="h-8 w-8 rounded-full bg-white/30" />
                <span className="font-medium text-sm text-white">
                  @username
                </span>
              </div>
            </ReelHeader>
            <ReelFooter>
              <p className="text-sm text-white">
                {reel.description}
              </p>
              <div className="mt-2 flex gap-4">
                <button className="text-white" type="button">
                  <Heart className="h-6 w-6" />
                </button>
                <button className="text-white" type="button">
                  <MessageCircle className="h-6 w-6" />
                </button>
                <button className="text-white" type="button">
                  <Share className="h-6 w-6" />
                </button>
              </div>
            </ReelFooter>
          </ReelItem>
        )}
      </ReelContent>
    </Reel>
  )
}
```

##### Controlled

Manage the active index, playing state, and muted state
externally via React state.

```tsx
"use client"

import { useState } from "react"
import {
  Reel,
  ReelContent,
  ReelControls,
  ReelItem,
  type ReelItem as ReelItemType,
  ReelMuteButton,
  ReelNextButton,
  ReelPlayButton,
  ReelPreviousButton,
  ReelProgress,
  ReelVideo,
} from "@/components/kibo-ui/reel"

const reels: ReelItemType[] = [
  {
    id: 1,
    type: "video",
    src: "/videos/demo-1.mp4",
    duration: 6,
  },
  {
    id: 2,
    type: "video",
    src: "/videos/demo-2.mp4",
    duration: 6,
  },
]

export function Example() {
  const [index, setIndex] = useState(0)
  const [playing, setPlaying] = useState(true)
  const [muted, setMuted] = useState(false)

  return (
    <div>
      <p>
        Slide {index + 1} of {reels.length}
      </p>
      <Reel
        data={reels}
        index={index}
        muted={muted}
        onIndexChange={setIndex}
        onMutedChange={setMuted}
        onPlayingChange={setPlaying}
        playing={playing}
      >
        <ReelProgress />
        <ReelContent>
          {(reel) => (
            <ReelItem>
              <ReelVideo src={reel.src} />
            </ReelItem>
          )}
        </ReelContent>
        <ReelControls>
          <ReelPreviousButton />
          <div className="flex gap-2">
            <ReelPlayButton />
            <ReelMuteButton />
          </div>
          <ReelNextButton />
        </ReelControls>
      </Reel>
    </div>
  )
}
```
