### Stories

> A composable Stories component - a carousel of individual video cards like you'd see on Facebook.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/stories.json"
```

#### Anatomy

```tsx
import {
  Stories,
  StoriesContent,
  Story,
  StoryVideo,
  StoryImage,
  StoryAuthor,
  StoryAuthorImage,
  StoryAuthorName,
  StoryTitle,
  StoryOverlay,
} from "@/components/kibo-ui/stories"
```

| Component | Description |
|-----------|-------------|
| `Stories` | Root carousel container. Wraps all story items in a horizontally scrollable carousel. |
| `StoriesContent` | Content wrapper for the story items. |
| `Story` | Individual story card with hover and focus effects. |
| `StoryVideo` | Video element that plays on hover/focus and resets on mouse out/blur. |
| `StoryImage` | Image element positioned to fill the story card. |
| `StoryAuthor` | Author info overlay positioned at the bottom of the card. |
| `StoryAuthorImage` | Author avatar using shadcn/ui Avatar with fallback support. |
| `StoryAuthorName` | Author name text label. |
| `StoryTitle` | Title overlay positioned at the top of the card. |
| `StoryOverlay` | Gradient overlay for readability. Positioned at the top or bottom. |

#### Props

**Stories**

Extends shadcn/ui `Carousel` props (`HTMLDivElement` attributes plus carousel options).

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `opts` | `CarouselOptions` | `{ align: "start", loop: false, dragFree: true }` | Embla Carousel options. Merged with the defaults shown. |
| `orientation` | `"horizontal" \| "vertical"` | `"horizontal"` | Scroll direction. |
| `plugins` | `CarouselPlugin` | — | Embla Carousel plugins. |
| `setApi` | `(api: CarouselApi) => void` | — | Callback to receive the Embla Carousel API instance. |

**StoriesContent**

Accepts standard `HTMLDivElement` attributes.

**Story**

Accepts standard `HTMLDivElement` attributes.

**StoryVideo**

Accepts standard `HTMLVideoElement` attributes. Plays on hover/focus and pauses on mouse out/blur, resetting to the initial time. Supports `#t=` hash fragments in `src` to set the initial seek position.

**StoryImage**

Extends `HTMLImageElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `alt` | `string` | — | Required alt text for the image. |

**StoryAuthor**

Accepts standard `HTMLDivElement` attributes.

**StoryAuthorImage**

Extends shadcn/ui `Avatar` props.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `src` | `string` | — | Avatar image URL. |
| `name` | `string` | — | Author name. First character is used as the fallback when `fallback` is not provided. |
| `fallback` | `string` | — | Text displayed when the avatar image fails to load. |

**StoryAuthorName**

Accepts standard `HTMLSpanElement` attributes.

**StoryTitle**

Accepts standard `HTMLDivElement` attributes.

**StoryOverlay**

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `side` | `"top" \| "bottom"` | `"bottom"` | Position and gradient direction of the overlay. |

#### Usage

##### Basic

```tsx
"use client"

import {
  Stories,
  StoriesContent,
  Story,
  StoryAuthor,
  StoryAuthorImage,
  StoryAuthorName,
  StoryOverlay,
  StoryVideo,
} from "@/components/kibo-ui/stories"

const stories = [
  {
    id: 1,
    author: "Alex Johnson",
    avatar: "/avatars/alex.jpg",
    fallback: "AJ",
    video: "/videos/bunny.mp4#t=20",
  },
  {
    id: 2,
    author: "Sarah Chen",
    avatar: "/avatars/sarah.jpg",
    fallback: "SC",
    video: "/videos/dream.mp4#t=10",
  },
  {
    id: 3,
    author: "Mike Rodriguez",
    avatar: "/avatars/mike.jpg",
    fallback: "MR",
    video: "/videos/blazes.mp4",
  },
]

export function Example() {
  return (
    <Stories>
      <StoriesContent>
        {stories.map((story) => (
          <Story
            className="aspect-[3/4] w-[200px]"
            key={story.id}
          >
            <StoryVideo src={story.video} />
            <StoryOverlay />
            <StoryAuthor>
              <StoryAuthorImage
                fallback={story.fallback}
                name={story.author}
                src={story.avatar}
              />
              <StoryAuthorName>
                {story.author}
              </StoryAuthorName>
            </StoryAuthor>
          </Story>
        ))}
      </StoriesContent>
    </Stories>
  )
}
```

##### Image Stories

Display image-based stories with a title overlay and gradient
overlays on both edges for readability.

```tsx
"use client"

import {
  Stories,
  StoriesContent,
  Story,
  StoryAuthor,
  StoryAuthorImage,
  StoryAuthorName,
  StoryImage,
  StoryOverlay,
  StoryTitle,
} from "@/components/kibo-ui/stories"

const stories = [
  {
    id: 1,
    author: "Alex Johnson",
    avatar: "/avatars/alex.jpg",
    fallback: "AJ",
    preview: "/images/mountain.jpg",
    title: "Mountain Adventure",
  },
  {
    id: 2,
    author: "Sarah Chen",
    avatar: "/avatars/sarah.jpg",
    fallback: "SC",
    preview: "/images/ocean.jpg",
    title: "Ocean Waves",
  },
  {
    id: 3,
    author: "Mike Rodriguez",
    avatar: "/avatars/mike.jpg",
    fallback: "MR",
    preview: "/images/forest.jpg",
    title: "Forest Trail",
  },
]

export function Example() {
  return (
    <Stories>
      <StoriesContent>
        {stories.map((story) => (
          <Story
            className="aspect-[3/4] w-[200px]"
            key={story.id}
          >
            <StoryImage
              alt={story.title}
              src={story.preview}
            />
            <StoryOverlay side="top" />
            <StoryOverlay side="bottom" />
            <StoryTitle
              className="truncate font-medium text-sm"
            >
              {story.title}
            </StoryTitle>
            <StoryAuthor>
              <StoryAuthorImage
                fallback={story.fallback}
                name={story.author}
                src={story.avatar}
              />
              <StoryAuthorName>
                {story.author}
              </StoryAuthorName>
            </StoryAuthor>
          </Story>
        ))}
      </StoriesContent>
    </Stories>
  )
}
```

##### Avatar Bubbles

Render compact circular avatar bubbles with a gradient ring,
similar to social media story indicators.

```tsx
"use client"

import {
  Stories,
  StoriesContent,
  Story,
  StoryAuthor,
  StoryAuthorImage,
} from "@/components/kibo-ui/stories"

const people = [
  {
    id: 1,
    name: "Hayden Bleasel",
    avatar: "https://github.com/haydenbleasel.png",
    fallback: "HB",
  },
  {
    id: 2,
    name: "shadcn",
    avatar: "https://github.com/shadcn.png",
    fallback: "CN",
  },
  {
    id: 3,
    name: "Lee Robinson",
    avatar: "https://github.com/leerob.png",
    fallback: "LR",
  },
]

export function Example() {
  return (
    <Stories>
      <StoriesContent className="justify-center">
        {people.map((person) => (
          <Story
            className="aspect-square w-12 rounded-full p-0"
            key={person.id}
          >
            <StoryAuthor className="p-0">
              <span
                aria-hidden="true"
                className="inline-flex size-full rounded-full bg-gradient-to-tr from-[#f9ce34] via-[#ee2a7b] to-[#6228d7] p-0.5"
              >
                <span className="inline-flex size-full rounded-full bg-white p-0.5">
                  <StoryAuthorImage
                    className="size-full"
                    fallback={person.fallback}
                    src={person.avatar}
                  />
                </span>
              </span>
            </StoryAuthor>
          </Story>
        ))}
      </StoriesContent>
    </Stories>
  )
}
```

##### Square Aspect Ratio

Adjust the aspect ratio and width to create square story
cards instead of the default portrait layout.

```tsx
"use client"

import {
  Stories,
  StoriesContent,
  Story,
  StoryAuthor,
  StoryAuthorImage,
  StoryAuthorName,
  StoryImage,
  StoryOverlay,
} from "@/components/kibo-ui/stories"

const stories = [
  {
    id: 1,
    author: "Alex Johnson",
    avatar: "/avatars/alex.jpg",
    fallback: "AJ",
    preview: "/images/mountain.jpg",
  },
  {
    id: 2,
    author: "Sarah Chen",
    avatar: "/avatars/sarah.jpg",
    fallback: "SC",
    preview: "/images/ocean.jpg",
  },
]

export function Example() {
  return (
    <Stories>
      <StoriesContent>
        {stories.map((story) => (
          <Story
            className="aspect-square w-[180px]"
            key={story.id}
          >
            <StoryImage
              alt={story.author}
              src={story.preview}
            />
            <StoryOverlay />
            <StoryAuthor>
              <StoryAuthorImage
                fallback={story.fallback}
                name={story.author}
                src={story.avatar}
              />
              <StoryAuthorName>
                {story.author}
              </StoryAuthorName>
            </StoryAuthor>
          </Story>
        ))}
      </StoriesContent>
    </Stories>
  )
}
```
