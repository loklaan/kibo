### Editor

> A block-style rich text editor built on Tiptap.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/editor.json"
```

#### Dependencies

External packages installed automatically:
- `@tiptap/core` — core editor engine
- `@tiptap/react` — React bindings for Tiptap
- `@tiptap/starter-kit` — essential editor extensions
- `@tiptap/extension-code-block-lowlight` — syntax-highlighted code blocks
- `@tiptap/extension-list` — task list support
- `@tiptap/extension-subscript` — subscript text formatting
- `@tiptap/extension-superscript` — superscript text formatting
- `@tiptap/extension-table` — table editing support
- `@tiptap/extension-text-style` — text style utilities
- `@tiptap/extension-typography` — typographic corrections
- `@tiptap/extensions` — character count and placeholder
- `@tiptap/suggestion` — slash command suggestions
- `lowlight` — syntax highlighting for code blocks
- `fuse.js` — fuzzy search for slash commands
- `tippy.js` — tooltip positioning for slash menu
- `lucide-react` — icons

#### Anatomy

```tsx
import {
  EditorProvider,
  EditorFloatingMenu,
  EditorBubbleMenu,
  EditorSelector,
  EditorClearFormatting,
  EditorNodeText,
  EditorNodeHeading1,
  EditorNodeHeading2,
  EditorNodeHeading3,
  EditorNodeBulletList,
  EditorNodeOrderedList,
  EditorNodeTaskList,
  EditorNodeQuote,
  EditorNodeCode,
  EditorNodeTable,
  EditorFormatBold,
  EditorFormatItalic,
  EditorFormatStrike,
  EditorFormatCode,
  EditorFormatSubscript,
  EditorFormatSuperscript,
  EditorFormatUnderline,
  EditorLinkSelector,
  EditorTableMenu,
  EditorTableGlobalMenu,
  EditorTableColumnMenu,
  EditorTableRowMenu,
  EditorTableColumnBefore,
  EditorTableColumnAfter,
  EditorTableColumnDelete,
  EditorTableRowBefore,
  EditorTableRowAfter,
  EditorTableRowDelete,
  EditorTableHeaderColumnToggle,
  EditorTableHeaderRowToggle,
  EditorTableDelete,
  EditorTableMergeCells,
  EditorTableSplitCell,
  EditorTableFix,
  EditorCharacterCount,
  defaultSlashSuggestions,
} from "@/components/kibo-ui/editor"

import type {
  Editor,
  JSONContent,
} from "@/components/kibo-ui/editor"
```

| Component | Description |
|-----------|-------------|
| `EditorProvider` | Root provider. Wraps all child components and initializes Tiptap. |
| `EditorFloatingMenu` | Floating toolbar shown on empty lines. |
| `EditorBubbleMenu` | Toolbar shown on text selection. |
| `EditorSelector` | Dropdown selector for block types or formatting groups. |
| `EditorClearFormatting` | Button that clears all formatting from the selection. |
| `EditorNodeText` | Button to convert selection to paragraph text. |
| `EditorNodeHeading1` | Button to toggle heading level 1. |
| `EditorNodeHeading2` | Button to toggle heading level 2. |
| `EditorNodeHeading3` | Button to toggle heading level 3. |
| `EditorNodeBulletList` | Button to toggle a bullet list. |
| `EditorNodeOrderedList` | Button to toggle a numbered list. |
| `EditorNodeTaskList` | Button to toggle a task/to-do list. |
| `EditorNodeQuote` | Button to toggle a blockquote. |
| `EditorNodeCode` | Button to toggle a code block. |
| `EditorNodeTable` | Button to insert a table. |
| `EditorFormatBold` | Button to toggle bold formatting. |
| `EditorFormatItalic` | Button to toggle italic formatting. |
| `EditorFormatStrike` | Button to toggle strikethrough formatting. |
| `EditorFormatCode` | Button to toggle inline code formatting. |
| `EditorFormatSubscript` | Button to toggle subscript formatting. |
| `EditorFormatSuperscript` | Button to toggle superscript formatting. |
| `EditorFormatUnderline` | Button to toggle underline formatting. |
| `EditorLinkSelector` | Popover for inserting or editing a link. |
| `EditorTableMenu` | Container that shows table operations when a table is active. |
| `EditorTableGlobalMenu` | Floating toolbar for global table operations. |
| `EditorTableColumnMenu` | Dropdown menu for column operations. |
| `EditorTableRowMenu` | Dropdown menu for row operations. |
| `EditorTableColumnBefore` | Menu item to insert a column before the current one. |
| `EditorTableColumnAfter` | Menu item to insert a column after the current one. |
| `EditorTableColumnDelete` | Menu item to delete the current column. |
| `EditorTableRowBefore` | Menu item to insert a row before the current one. |
| `EditorTableRowAfter` | Menu item to insert a row after the current one. |
| `EditorTableRowDelete` | Menu item to delete the current row. |
| `EditorTableHeaderColumnToggle` | Button to toggle a header column. |
| `EditorTableHeaderRowToggle` | Button to toggle a header row. |
| `EditorTableDelete` | Button to delete the entire table. |
| `EditorTableMergeCells` | Button to merge selected cells. |
| `EditorTableSplitCell` | Button to split a merged cell. |
| `EditorTableFix` | Button to fix broken table structure. |
| `EditorCharacterCount.Characters` | Displays the character count. |
| `EditorCharacterCount.Words` | Displays the word count. |

| Type | Description |
|------|-------------|
| `Editor` | Tiptap editor instance (re-exported from `@tiptap/react`). |
| `JSONContent` | Tiptap JSON document format (re-exported from `@tiptap/react`). |
| `SuggestionItem` | Shape of a slash command suggestion item. |

```ts
type SuggestionItem = {
  title: string
  description: string
  icon: LucideIcon
  searchTerms: string[]
  command: (props: {
    editor: Editor
    range: Range
  }) => void
}
```

| Constant | Description |
|----------|-------------|
| `defaultSlashSuggestions` | Default set of slash command items (text, headings, lists, quote, code, table). |

#### Props

**EditorProvider**

Extends `TiptapEditorProviderProps` from `@tiptap/react` (includes `content`, `onUpdate`, `extensions`, `editorProps`, etc.).

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `className` | `string` | `undefined` | CSS class for the editor wrapper. |
| `limit` | `number` | `undefined` | Character limit for the editor content. |
| `placeholder` | `string` | `undefined` | Placeholder text shown when the editor is empty. |
| `content` | `JSONContent \| string` | `undefined` | Initial editor content as JSON or HTML string. |
| `onUpdate` | `(props: { editor: Editor }) => void` | — | Called when the editor content changes. |
| `extensions` | `Extension[]` | `[]` | Additional Tiptap extensions to register. |

**EditorFloatingMenu**

Extends `FloatingMenuProps` from `@tiptap/react/menus` (minus `editor`, which is injected automatically).

Accepts standard floating menu attributes.

**EditorBubbleMenu**

Extends `BubbleMenuProps` from `@tiptap/react/menus` (minus `editor`, which is injected automatically).

Accepts standard bubble menu attributes.

**EditorSelector**

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `title` | `string` | — | Label text displayed on the selector button. |
| `open` | `boolean` | `undefined` | Controlled open state. |
| `onOpenChange` | `(open: boolean) => void` | — | Called when the popover open state changes. |

**EditorLinkSelector**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `open` | `boolean` | `undefined` | Controlled open state. |
| `onOpenChange` | `(open: boolean) => void` | — | Called when the popover open state changes. |

**EditorClearFormatting, EditorNodeText, EditorNodeHeading1, EditorNodeHeading2, EditorNodeHeading3, EditorNodeBulletList, EditorNodeOrderedList, EditorNodeTaskList, EditorNodeQuote, EditorNodeCode, EditorNodeTable, EditorFormatBold, EditorFormatItalic, EditorFormatStrike, EditorFormatCode, EditorFormatSubscript, EditorFormatSuperscript, EditorFormatUnderline**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `hideName` | `boolean` | `false` (`true` for `EditorClearFormatting`) | Hides the button label, showing only the icon. |

**EditorTableMenu, EditorTableGlobalMenu, EditorTableColumnMenu, EditorTableRowMenu**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `children` | `ReactNode` | — | Menu items to render inside. |

**EditorTableColumnBefore, EditorTableColumnAfter, EditorTableColumnDelete, EditorTableRowBefore, EditorTableRowAfter, EditorTableRowDelete, EditorTableHeaderColumnToggle, EditorTableHeaderRowToggle, EditorTableDelete, EditorTableMergeCells, EditorTableSplitCell, EditorTableFix**

These components accept no custom props. Each renders a
self-contained action button or menu item.

**EditorCharacterCount.Characters, EditorCharacterCount.Words**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `children` | `ReactNode` | — | Label text rendered before the count value. |
| `className` | `string` | `undefined` | CSS class for the count container. |

#### Usage

##### Basic

A minimal editor with placeholder text and an `onUpdate` callback.

```tsx
"use client"

import {
  EditorProvider,
} from "@/components/kibo-ui/editor"
import type { Editor } from "@/components/kibo-ui/editor"

export function Example() {
  const handleUpdate = ({ editor }: { editor: Editor }) => {
    console.log(editor.getJSON())
  }

  return (
    <EditorProvider
      className="min-h-[200px] rounded-lg border p-4"
      onUpdate={handleUpdate}
      placeholder="Start typing..."
    />
  )
}
```

##### With Floating and Bubble Menus

An editor with a floating menu on empty lines and a bubble
menu on text selection, including node type and format selectors.

```tsx
"use client"

import {
  EditorProvider,
  EditorFloatingMenu,
  EditorBubbleMenu,
  EditorSelector,
  EditorNodeText,
  EditorNodeHeading1,
  EditorNodeHeading2,
  EditorNodeHeading3,
  EditorNodeBulletList,
  EditorNodeOrderedList,
  EditorNodeQuote,
  EditorNodeCode,
  EditorFormatBold,
  EditorFormatItalic,
  EditorFormatUnderline,
  EditorFormatStrike,
  EditorFormatCode,
  EditorLinkSelector,
  EditorClearFormatting,
} from "@/components/kibo-ui/editor"
import type { Editor } from "@/components/kibo-ui/editor"

export function Example() {
  const handleUpdate = ({ editor }: { editor: Editor }) => {
    console.log(editor.getJSON())
  }

  return (
    <EditorProvider
      className="min-h-[300px] rounded-lg border p-4"
      onUpdate={handleUpdate}
      placeholder="Type / for commands..."
    >
      <EditorFloatingMenu>
        <EditorNodeHeading1 hideName />
        <EditorNodeBulletList hideName />
        <EditorNodeQuote hideName />
        <EditorNodeCode hideName />
      </EditorFloatingMenu>
      <EditorBubbleMenu>
        <EditorSelector title="Text">
          <EditorNodeText />
          <EditorNodeHeading1 />
          <EditorNodeHeading2 />
          <EditorNodeHeading3 />
          <EditorNodeBulletList />
          <EditorNodeOrderedList />
          <EditorNodeQuote />
          <EditorNodeCode />
        </EditorSelector>
        <EditorSelector title="Format">
          <EditorFormatBold />
          <EditorFormatItalic />
          <EditorFormatUnderline />
          <EditorFormatStrike />
          <EditorFormatCode />
        </EditorSelector>
        <EditorLinkSelector />
        <EditorClearFormatting />
      </EditorBubbleMenu>
    </EditorProvider>
  )
}
```

##### Controlled Content with JSON

An editor initialized with JSON content and a controlled state
update callback.

```tsx
"use client"

import { useState } from "react"
import {
  EditorProvider,
} from "@/components/kibo-ui/editor"
import type {
  Editor,
  JSONContent,
} from "@/components/kibo-ui/editor"

export function Example() {
  const [content, setContent] = useState<JSONContent>({
    type: "doc",
    content: [
      {
        type: "heading",
        attrs: { level: 1 },
        content: [{ type: "text", text: "Hello World" }],
      },
      {
        type: "paragraph",
        content: [
          { type: "text", text: "This is a " },
          {
            type: "text",
            marks: [{ type: "bold" }],
            text: "rich text",
          },
          { type: "text", text: " editor." },
        ],
      },
    ],
  })

  const handleUpdate = ({ editor }: { editor: Editor }) => {
    setContent(editor.getJSON())
  }

  return (
    <EditorProvider
      className="min-h-[200px] rounded-lg border p-4"
      content={content}
      onUpdate={handleUpdate}
      placeholder="Start typing..."
    />
  )
}
```

##### With Table Editing

An editor with full table support including column, row, and
global table operations.

```tsx
"use client"

import {
  EditorProvider,
  EditorFloatingMenu,
  EditorNodeTable,
  EditorTableMenu,
  EditorTableColumnMenu,
  EditorTableColumnBefore,
  EditorTableColumnAfter,
  EditorTableColumnDelete,
  EditorTableRowMenu,
  EditorTableRowBefore,
  EditorTableRowAfter,
  EditorTableRowDelete,
  EditorTableGlobalMenu,
  EditorTableHeaderColumnToggle,
  EditorTableHeaderRowToggle,
  EditorTableDelete,
  EditorTableMergeCells,
  EditorTableSplitCell,
  EditorTableFix,
} from "@/components/kibo-ui/editor"

export function Example() {
  return (
    <EditorProvider
      className="min-h-[300px] rounded-lg border p-4"
      placeholder="Type / then select Table..."
    >
      <EditorFloatingMenu>
        <EditorNodeTable hideName />
      </EditorFloatingMenu>
      <EditorTableMenu>
        <EditorTableColumnMenu>
          <EditorTableColumnBefore />
          <EditorTableColumnAfter />
          <EditorTableColumnDelete />
        </EditorTableColumnMenu>
        <EditorTableRowMenu>
          <EditorTableRowBefore />
          <EditorTableRowAfter />
          <EditorTableRowDelete />
        </EditorTableRowMenu>
        <EditorTableGlobalMenu>
          <EditorTableHeaderColumnToggle />
          <EditorTableHeaderRowToggle />
          <EditorTableDelete />
          <EditorTableMergeCells />
          <EditorTableSplitCell />
          <EditorTableFix />
        </EditorTableGlobalMenu>
      </EditorTableMenu>
    </EditorProvider>
  )
}
```

##### With Character Count

An editor displaying a word count and enforcing a character limit.

```tsx
"use client"

import {
  EditorProvider,
  EditorCharacterCount,
} from "@/components/kibo-ui/editor"

export function Example() {
  return (
    <EditorProvider
      className="relative min-h-[200px] rounded-lg border p-4"
      limit={500}
      placeholder="Start typing (max 500 characters)..."
    >
      <EditorCharacterCount.Words>
        Words:{" "}
      </EditorCharacterCount.Words>
    </EditorProvider>
  )
}
```
