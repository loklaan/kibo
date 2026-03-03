## Installation

### Prerequisites

Kibo UI requires:

- **Node.js** version 18 or later
- **React** version 18 or later
- **shadcn/ui** initialized in your project with **CSS Variables** mode

If you have not set up shadcn/ui yet, run `npx shadcn@latest init` and
configure Tailwind CSS before installing any Kibo UI components.

### Installing Components

Install components individually using the shadcn CLI:

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/<name>.json"
```

Replace `<name>` with the component's kebab-case name. For example,
to install the Gantt chart:

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/gantt.json"
```

The CLI downloads the component source code into your project and
installs any required dependencies automatically.

### File Location

Components are placed in `@/components/kibo-ui/<name>/`. For example,
the Gantt component installs to `@/components/kibo-ui/gantt/`. You
own the code — every file can be read, modified, and extended.

### Importing and Using Components

Import sub-components from the component directory and compose them
as JSX children:

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
          size={16}
          className="shrink-0 text-muted-foreground"
        />
      </AnnouncementTitle>
    </Announcement>
  )
}
```

### Extensibility

All Kibo UI components accept standard HTML attributes for their
underlying element. For example, a component that renders a `div`
extends `HTMLAttributes<HTMLDivElement>`, so you can pass `className`,
`style`, event handlers, and any other valid `div` prop. Tailwind CSS
classes can be applied directly to customize appearance without
modifying the component source.
