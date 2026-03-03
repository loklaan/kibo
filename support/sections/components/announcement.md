### Announcement

> A compound badge designed to display an announcement.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/announcement.json"
```

#### Anatomy

```tsx
import {
  Announcement,
  AnnouncementTag,
  AnnouncementTitle,
} from "@/components/kibo-ui/announcement"
```

| Component | Description |
|-----------|-------------|
| `Announcement` | Root container. Renders as a styled Badge with rounded-full appearance and hover shadow. |
| `AnnouncementTag` | Tag label displayed at the start of the announcement. |
| `AnnouncementTitle` | Title text displayed after the tag. |

#### Props

**Announcement**

Extends `Badge` component props.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `themed` | `boolean` | `false` | Enables themed mode, adjusting border and child background styles for colored variants. |
| `variant` | `"default" \| "secondary" \| "destructive" \| "outline"` | `"outline"` | Badge variant controlling the visual style. |

**AnnouncementTag**

Accepts standard `HTMLDivElement` attributes.

**AnnouncementTitle**

Accepts standard `HTMLDivElement` attributes.

#### Usage

##### Basic

```tsx
import {
  Announcement,
  AnnouncementTag,
  AnnouncementTitle,
} from "@/components/kibo-ui/announcement"
import { ArrowUpRightIcon } from "lucide-react"

export function Example() {
  return (
    <Announcement>
      <AnnouncementTag>Latest update</AnnouncementTag>
      <AnnouncementTitle>
        New feature added
        <ArrowUpRightIcon
          className="shrink-0 text-muted-foreground"
          size={16}
        />
      </AnnouncementTitle>
    </Announcement>
  )
}
```

##### Without Tag

The `AnnouncementTag` is optional. Omit it for a simpler layout.

```tsx
import {
  Announcement,
  AnnouncementTitle,
} from "@/components/kibo-ui/announcement"
import { ArrowUpRightIcon } from "lucide-react"

export function Example() {
  return (
    <Announcement>
      <AnnouncementTitle>
        New feature added
        <ArrowUpRightIcon
          className="shrink-0 text-muted-foreground"
          size={16}
        />
      </AnnouncementTitle>
    </Announcement>
  )
}
```

##### Themed

Enable `themed` mode and apply custom colors via `className` for
contextual announcements.

```tsx
import {
  Announcement,
  AnnouncementTag,
  AnnouncementTitle,
} from "@/components/kibo-ui/announcement"
import { ArrowUpRightIcon } from "lucide-react"

export function Example() {
  return (
    <div className="flex flex-col gap-2">
      <Announcement
        className="bg-emerald-100 text-emerald-700
          dark:bg-emerald-700 dark:text-emerald-100"
        themed
      >
        <AnnouncementTag>Success</AnnouncementTag>
        <AnnouncementTitle>
          Feature deployed
          <ArrowUpRightIcon
            className="shrink-0 opacity-70"
            size={16}
          />
        </AnnouncementTitle>
      </Announcement>

      <Announcement
        className="bg-rose-100 text-rose-700
          dark:bg-rose-700 dark:text-rose-100"
        themed
      >
        <AnnouncementTag>Error</AnnouncementTag>
        <AnnouncementTitle>
          Something went wrong
          <ArrowUpRightIcon
            className="shrink-0 opacity-70"
            size={16}
          />
        </AnnouncementTitle>
      </Announcement>
    </div>
  )
}
```

##### As a Link

The root `Announcement` renders a Badge which accepts an `asChild`
prop, allowing it to wrap a link element.

```tsx
import {
  Announcement,
  AnnouncementTag,
  AnnouncementTitle,
} from "@/components/kibo-ui/announcement"
import { ArrowUpRightIcon } from "lucide-react"

export function Example() {
  return (
    <Announcement asChild>
      <a href="/changelog">
        <AnnouncementTag>v2.0</AnnouncementTag>
        <AnnouncementTitle>
          View the changelog
          <ArrowUpRightIcon
            className="shrink-0 text-muted-foreground"
            size={16}
          />
        </AnnouncementTitle>
      </a>
    </Announcement>
  )
}
```
