### Glimpse

> A component that shows a preview of a URL when hovering over a link.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/glimpse.json"
```

#### Anatomy

```tsx
import {
  Glimpse,
  GlimpseContent,
  GlimpseTrigger,
  GlimpseTitle,
  GlimpseDescription,
  GlimpseImage,
} from "@/components/kibo-ui/glimpse"
```

| Component | Description |
|-----------|-------------|
| `Glimpse` | Root hover card container. Manages open/close state. |
| `GlimpseTrigger` | Element that triggers the hover card on hover. |
| `GlimpseContent` | Popover content area displayed on hover. |
| `GlimpseTitle` | Renders the preview title as a truncated paragraph. |
| `GlimpseDescription` | Renders the preview description, clamped to 2 lines. |
| `GlimpseImage` | Renders a preview image with rounded borders. |

The package also exports a server-side helper for fetching
Open Graph metadata from a URL:

```tsx
import { glimpse } from "@/components/kibo-ui/glimpse/server"
```

| Function | Description |
|----------|-------------|
| `glimpse(url: string)` | Fetches the page at `url` and extracts `title`, `description`, and `image` from Open Graph and HTML meta tags. Returns `Promise<{ title: string | null; description: string | null; image: string | null }>`. |

#### Props

**Glimpse**

Extends Radix `HoverCard.Root` props.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `open` | `boolean` | `undefined` | Controlled open state. |
| `defaultOpen` | `boolean` | `false` | Initial open state when uncontrolled. |
| `onOpenChange` | `(open: boolean) => void` | -- | Called when open state changes. |
| `openDelay` | `number` | `700` | Delay in ms before opening on hover. |
| `closeDelay` | `number` | `300` | Delay in ms before closing on leave. |

**GlimpseTrigger**

Extends Radix `HoverCard.Trigger` props.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `asChild` | `boolean` | `false` | Merge props onto the child element instead of rendering a default element. |

**GlimpseContent**

Extends Radix `HoverCard.Content` props.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `align` | `"start" \| "center" \| "end"` | `"center"` | Horizontal alignment relative to the trigger. |
| `side` | `"top" \| "right" \| "bottom" \| "left"` | `"bottom"` | Preferred side of the trigger to render. |
| `sideOffset` | `number` | `4` | Distance in px from the trigger. |

**GlimpseTitle**

Accepts standard `HTMLParagraphElement` attributes.

**GlimpseDescription**

Accepts standard `HTMLParagraphElement` attributes.

**GlimpseImage**

Accepts standard `HTMLImageElement` attributes.

#### Usage

##### Basic

```tsx
import {
  Glimpse,
  GlimpseContent,
  GlimpseDescription,
  GlimpseImage,
  GlimpseTitle,
  GlimpseTrigger,
} from "@/components/kibo-ui/glimpse"

export function Example() {
  return (
    <p>
      Check out{" "}
      <Glimpse>
        <GlimpseTrigger asChild>
          <a
            className="font-medium text-primary underline"
            href="https://example.com"
          >
            Example
          </a>
        </GlimpseTrigger>
        <GlimpseContent className="w-80">
          <GlimpseImage src="/og-image.png" />
          <GlimpseTitle>Example Domain</GlimpseTitle>
          <GlimpseDescription>
            This domain is for use in illustrative examples.
          </GlimpseDescription>
        </GlimpseContent>
      </Glimpse>{" "}
      for more info.
    </p>
  )
}
```

##### With Server-Side Data Fetching

Use the `glimpse` server helper to fetch Open Graph metadata
at render time in a React Server Component.

```tsx
import {
  Glimpse,
  GlimpseContent,
  GlimpseDescription,
  GlimpseImage,
  GlimpseTitle,
  GlimpseTrigger,
} from "@/components/kibo-ui/glimpse"
import { glimpse } from "@/components/kibo-ui/glimpse/server"

export async function Example() {
  const data = await glimpse(
    "https://github.com/haydenbleasel/kibo-ui"
  )

  return (
    <p>
      Check out{" "}
      <Glimpse openDelay={0} closeDelay={0}>
        <GlimpseTrigger asChild>
          <a
            className="font-medium text-primary underline"
            href="https://github.com/haydenbleasel/kibo-ui"
          >
            Kibo UI
          </a>
        </GlimpseTrigger>
        <GlimpseContent className="w-80">
          <GlimpseImage src={data.image ?? ""} />
          <GlimpseTitle>{data.title}</GlimpseTitle>
          <GlimpseDescription>
            {data.description}
          </GlimpseDescription>
        </GlimpseContent>
      </Glimpse>{" "}
      on GitHub.
    </p>
  )
}
```

##### Custom Styling

Override default styles with className props on each
sub-component.

```tsx
import {
  Glimpse,
  GlimpseContent,
  GlimpseDescription,
  GlimpseImage,
  GlimpseTitle,
  GlimpseTrigger,
} from "@/components/kibo-ui/glimpse"

export function Example() {
  return (
    <p>
      Read the{" "}
      <Glimpse>
        <GlimpseTrigger asChild>
          <a
            className="font-medium text-primary underline"
            href="https://example.com/blog"
          >
            blog post
          </a>
        </GlimpseTrigger>
        <GlimpseContent className="w-80 bg-secondary">
          <GlimpseImage
            className="shadow-lg"
            src="/blog-cover.jpg"
          />
          <GlimpseTitle className="line-clamp-2 text-lg">
            Building Accessible Components
          </GlimpseTitle>
          <GlimpseDescription className="text-sm">
            A deep dive into building accessible,
            composable UI components with Radix.
          </GlimpseDescription>
        </GlimpseContent>
      </Glimpse>{" "}
      for details.
    </p>
  )
}
```

##### Without Image

Glimpse works without an image for text-only previews.

```tsx
import {
  Glimpse,
  GlimpseContent,
  GlimpseDescription,
  GlimpseTitle,
  GlimpseTrigger,
} from "@/components/kibo-ui/glimpse"

export function Example() {
  return (
    <p>
      Contact{" "}
      <Glimpse>
        <GlimpseTrigger asChild>
          <a
            className="font-medium text-primary underline"
            href="mailto:alice@example.com"
          >
            Alice
          </a>
        </GlimpseTrigger>
        <GlimpseContent>
          <GlimpseTitle>Alice Johnson</GlimpseTitle>
          <GlimpseDescription>
            Staff Engineer at Acme Corp.
          </GlimpseDescription>
        </GlimpseContent>
      </Glimpse>{" "}
      for questions.
    </p>
  )
}
```
