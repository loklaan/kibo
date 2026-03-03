### Dropzone

> Allows users to drag-and-drop files into a container to upload or process them.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/dropzone.json"
```

#### Dependencies

External packages installed automatically:
- `react-dropzone` — drag-and-drop file handling
- `lucide-react` — icon primitives

#### Anatomy

```tsx
import {
  Dropzone,
  DropzoneContent,
  DropzoneEmptyState,
} from "@/components/kibo-ui/dropzone"
```

| Component | Description |
|-----------|-------------|
| `Dropzone` | Root container. Wraps a hidden file input and drop target, provides context to children. |
| `DropzoneContent` | Displays the selected file names when files are present. Renders nothing when no files are set. |
| `DropzoneEmptyState` | Displays upload instructions and constraint hints when no files are set. Renders nothing when files are present. |

#### Props

**Dropzone**

Extends `react-dropzone` `DropzoneOptions` (excluding `onDrop`).

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `src` | `File[]` | `undefined` | The currently selected files. |
| `accept` | `Record<string, string[]>` | `undefined` | Accepted MIME types and extensions. |
| `maxFiles` | `number` | `1` | Maximum number of files allowed. |
| `maxSize` | `number` | `undefined` | Maximum file size in bytes. |
| `minSize` | `number` | `undefined` | Minimum file size in bytes. |
| `disabled` | `boolean` | `undefined` | Disables the dropzone. |
| `onDrop` | `(acceptedFiles: File[], fileRejections: FileRejection[], event: DropEvent) => void` | — | Called when files are dropped or selected. |
| `onError` | `(error: Error) => void` | — | Called when a file is rejected. |
| `className` | `string` | `undefined` | Additional CSS classes for the root button. |

**DropzoneContent**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `children` | `ReactNode` | `undefined` | Custom content to render when files are present. Falls back to a default file name list. |
| `className` | `string` | `undefined` | Additional CSS classes for the container. |

**DropzoneEmptyState**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `children` | `ReactNode` | `undefined` | Custom empty state content. Falls back to a default prompt with constraint hints. |
| `className` | `string` | `undefined` | Additional CSS classes for the container. |

#### Usage

##### Basic

```tsx
"use client"

import { useState } from "react"
import {
  Dropzone,
  DropzoneContent,
  DropzoneEmptyState,
} from "@/components/kibo-ui/dropzone"

export function Example() {
  const [files, setFiles] = useState<File[]>()

  return (
    <Dropzone
      onDrop={(accepted) => setFiles(accepted)}
      onError={console.error}
      src={files}
    >
      <DropzoneEmptyState />
      <DropzoneContent />
    </Dropzone>
  )
}
```

##### Multiple Files

Allows up to three files to be uploaded at once.

```tsx
"use client"

import { useState } from "react"
import {
  Dropzone,
  DropzoneContent,
  DropzoneEmptyState,
} from "@/components/kibo-ui/dropzone"

export function Example() {
  const [files, setFiles] = useState<File[]>()

  return (
    <Dropzone
      maxFiles={3}
      onDrop={(accepted) => setFiles(accepted)}
      onError={console.error}
      src={files}
    >
      <DropzoneEmptyState />
      <DropzoneContent />
    </Dropzone>
  )
}
```

##### Restricted File Types

Accepts only image files using the `accept` prop.

```tsx
"use client"

import { useState } from "react"
import {
  Dropzone,
  DropzoneContent,
  DropzoneEmptyState,
} from "@/components/kibo-ui/dropzone"

export function Example() {
  const [files, setFiles] = useState<File[]>()

  return (
    <Dropzone
      accept={{ "image/*": [] }}
      onDrop={(accepted) => setFiles(accepted)}
      onError={console.error}
      src={files}
    >
      <DropzoneEmptyState />
      <DropzoneContent />
    </Dropzone>
  )
}
```

##### With Size Constraints

Sets minimum and maximum file size limits. The empty state
automatically displays the constraint hints.

```tsx
"use client"

import { useState } from "react"
import {
  Dropzone,
  DropzoneContent,
  DropzoneEmptyState,
} from "@/components/kibo-ui/dropzone"

export function Example() {
  const [files, setFiles] = useState<File[]>()

  return (
    <Dropzone
      maxSize={1024 * 1024 * 10}
      minSize={1024}
      onDrop={(accepted) => setFiles(accepted)}
      onError={console.error}
      src={files}
    >
      <DropzoneEmptyState />
      <DropzoneContent />
    </Dropzone>
  )
}
```

##### Image Preview

Reads the dropped image file and renders a preview inside
`DropzoneContent` using a custom child element.

```tsx
"use client"

import { useState } from "react"
import {
  Dropzone,
  DropzoneContent,
  DropzoneEmptyState,
} from "@/components/kibo-ui/dropzone"

export function Example() {
  const [files, setFiles] = useState<File[]>()
  const [preview, setPreview] = useState<string>()

  const handleDrop = (accepted: File[]) => {
    setFiles(accepted)
    if (accepted.length > 0) {
      const reader = new FileReader()
      reader.onload = (e) => {
        if (typeof e.target?.result === "string") {
          setPreview(e.target.result)
        }
      }
      reader.readAsDataURL(accepted[0])
    }
  }

  return (
    <Dropzone
      accept={{ "image/*": [".png", ".jpg", ".jpeg"] }}
      onDrop={handleDrop}
      onError={console.error}
      src={files}
    >
      <DropzoneEmptyState />
      <DropzoneContent>
        {preview && (
          <div className="h-[102px] w-full">
            <img
              alt="Preview"
              className="absolute top-0 left-0 h-full w-full object-cover"
              src={preview}
            />
          </div>
        )}
      </DropzoneContent>
    </Dropzone>
  )
}
```

##### Custom Empty State

Replaces the default empty state with a custom layout.

```tsx
"use client"

import { useState } from "react"
import {
  Dropzone,
  DropzoneContent,
  DropzoneEmptyState,
} from "@/components/kibo-ui/dropzone"
import { UploadIcon } from "lucide-react"

export function Example() {
  const [files, setFiles] = useState<File[]>()

  return (
    <Dropzone
      onDrop={(accepted) => setFiles(accepted)}
      onError={console.error}
      src={files}
    >
      <DropzoneEmptyState>
        <div className="flex w-full items-center gap-4 p-8">
          <div className="flex size-16 items-center justify-center rounded-lg bg-muted text-muted-foreground">
            <UploadIcon size={24} />
          </div>
          <div className="text-left">
            <p className="font-medium text-sm">
              Upload a file
            </p>
            <p className="text-muted-foreground text-xs">
              Drag and drop or click to upload
            </p>
          </div>
        </div>
      </DropzoneEmptyState>
      <DropzoneContent />
    </Dropzone>
  )
}
```
