### Video Player

> A composable, shadcn/ui styled video player component that uses the media-chrome library.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/video-player.json"
```

#### Dependencies

External packages installed automatically:
- `media-chrome` — accessible, customizable media player controls

#### Anatomy

```tsx
import {
  VideoPlayer,
  VideoPlayerContent,
  VideoPlayerControlBar,
  VideoPlayerMuteButton,
  VideoPlayerPlayButton,
  VideoPlayerSeekBackwardButton,
  VideoPlayerSeekForwardButton,
  VideoPlayerTimeDisplay,
  VideoPlayerTimeRange,
  VideoPlayerVolumeRange,
} from "@/components/kibo-ui/video-player"
```

| Component | Description |
|-----------|-------------|
| `VideoPlayer` | Root media controller. Applies themed CSS variables and wraps all children. |
| `VideoPlayerContent` | The `<video>` element. Must include `slot="media"` to connect to the controller. |
| `VideoPlayerControlBar` | Container for playback controls. |
| `VideoPlayerPlayButton` | Toggles play/pause. |
| `VideoPlayerSeekBackwardButton` | Seeks backward by a configurable offset. |
| `VideoPlayerSeekForwardButton` | Seeks forward by a configurable offset. |
| `VideoPlayerTimeRange` | Interactive seek/progress bar. |
| `VideoPlayerTimeDisplay` | Displays current time and optionally total duration. |
| `VideoPlayerMuteButton` | Toggles mute/unmute. |
| `VideoPlayerVolumeRange` | Volume slider. |

#### Props

**VideoPlayer**

Extends `MediaController` attributes from media-chrome.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `style` | `CSSProperties` | — | Merged with default themed CSS variables. |
| `autohide` | `number` | `2` | Seconds of inactivity before controls hide. Set `-1` to disable. |
| `audio` | `boolean` | `false` | Renders as an audio-only player when `true`. |

**VideoPlayerContent**

Extends `HTMLVideoElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `src` | `string` | — | URL of the video source. |
| `slot` | `string` | — | Set to `"media"` to connect the video to the controller. |
| `muted` | `boolean` | `false` | Starts the video muted. |
| `preload` | `"none" \| "metadata" \| "auto"` | — | Hint for how much content to preload. |
| `crossOrigin` | `string` | — | CORS setting for the video resource. |

**VideoPlayerControlBar**

Accepts standard `MediaControlBar` attributes from media-chrome.

**VideoPlayerPlayButton**

Accepts standard `MediaPlayButton` attributes from media-chrome.

**VideoPlayerSeekBackwardButton**

Extends `MediaSeekBackwardButton` attributes from media-chrome.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `seekOffset` | `number` | `30` | Number of seconds to seek backward. |

**VideoPlayerSeekForwardButton**

Extends `MediaSeekForwardButton` attributes from media-chrome.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `seekOffset` | `number` | `30` | Number of seconds to seek forward. |

**VideoPlayerTimeRange**

Accepts standard `MediaTimeRange` attributes from media-chrome.

**VideoPlayerTimeDisplay**

Extends `MediaTimeDisplay` attributes from media-chrome.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `showDuration` | `boolean` | `false` | Shows total duration alongside current time. |
| `remaining` | `boolean` | `false` | Displays remaining time instead of elapsed. |

**VideoPlayerMuteButton**

Accepts standard `MediaMuteButton` attributes from media-chrome.

**VideoPlayerVolumeRange**

Accepts standard `MediaVolumeRange` attributes from media-chrome.

#### Usage

##### Basic

```tsx
"use client"

import {
  VideoPlayer,
  VideoPlayerContent,
  VideoPlayerControlBar,
  VideoPlayerMuteButton,
  VideoPlayerPlayButton,
  VideoPlayerSeekBackwardButton,
  VideoPlayerSeekForwardButton,
  VideoPlayerTimeDisplay,
  VideoPlayerTimeRange,
  VideoPlayerVolumeRange,
} from "@/components/kibo-ui/video-player"

export function Example() {
  return (
    <VideoPlayer className="overflow-hidden rounded-lg border">
      <VideoPlayerContent
        slot="media"
        src="https://stream.mux.com/DS00Spx1CV902MCtPj5WknGlR102V5HFkDe/high.mp4"
        preload="auto"
        muted
        crossOrigin=""
      />
      <VideoPlayerControlBar>
        <VideoPlayerPlayButton />
        <VideoPlayerSeekBackwardButton />
        <VideoPlayerSeekForwardButton />
        <VideoPlayerTimeRange />
        <VideoPlayerTimeDisplay showDuration />
        <VideoPlayerMuteButton />
        <VideoPlayerVolumeRange />
      </VideoPlayerControlBar>
    </VideoPlayer>
  )
}
```

##### Minimal Controls

A compact player with only play/pause and a progress bar.

```tsx
"use client"

import {
  VideoPlayer,
  VideoPlayerContent,
  VideoPlayerControlBar,
  VideoPlayerPlayButton,
  VideoPlayerTimeRange,
} from "@/components/kibo-ui/video-player"

export function Example() {
  return (
    <VideoPlayer className="overflow-hidden rounded-lg border">
      <VideoPlayerContent
        slot="media"
        src="/videos/demo.mp4"
        preload="metadata"
        muted
      />
      <VideoPlayerControlBar>
        <VideoPlayerPlayButton />
        <VideoPlayerTimeRange />
      </VideoPlayerControlBar>
    </VideoPlayer>
  )
}
```

##### Remaining Time Display

Show remaining time instead of elapsed, with custom seek offsets.

```tsx
"use client"

import {
  VideoPlayer,
  VideoPlayerContent,
  VideoPlayerControlBar,
  VideoPlayerMuteButton,
  VideoPlayerPlayButton,
  VideoPlayerSeekBackwardButton,
  VideoPlayerSeekForwardButton,
  VideoPlayerTimeDisplay,
  VideoPlayerTimeRange,
  VideoPlayerVolumeRange,
} from "@/components/kibo-ui/video-player"

export function Example() {
  return (
    <VideoPlayer className="overflow-hidden rounded-lg border">
      <VideoPlayerContent
        slot="media"
        src="/videos/tutorial.mp4"
        preload="auto"
      />
      <VideoPlayerControlBar>
        <VideoPlayerPlayButton />
        <VideoPlayerSeekBackwardButton seekOffset={10} />
        <VideoPlayerSeekForwardButton seekOffset={10} />
        <VideoPlayerTimeRange />
        <VideoPlayerTimeDisplay remaining showDuration />
        <VideoPlayerMuteButton />
        <VideoPlayerVolumeRange />
      </VideoPlayerControlBar>
    </VideoPlayer>
  )
}
```

##### Audio Only

Use the `audio` prop for audio-only playback without a video frame.

```tsx
"use client"

import {
  VideoPlayer,
  VideoPlayerControlBar,
  VideoPlayerMuteButton,
  VideoPlayerPlayButton,
  VideoPlayerTimeDisplay,
  VideoPlayerTimeRange,
  VideoPlayerVolumeRange,
} from "@/components/kibo-ui/video-player"

export function Example() {
  return (
    <VideoPlayer
      audio
      className="overflow-hidden rounded-lg border"
    >
      <audio slot="media" src="/audio/podcast.mp3" preload="auto" />
      <VideoPlayerControlBar>
        <VideoPlayerPlayButton />
        <VideoPlayerTimeRange />
        <VideoPlayerTimeDisplay showDuration />
        <VideoPlayerMuteButton />
        <VideoPlayerVolumeRange />
      </VideoPlayerControlBar>
    </VideoPlayer>
  )
}
```
