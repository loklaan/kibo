# Kibo UI Component Inventory

Complete catalog of all 41 Kibo UI components. Each entry documents the package name, description, exported components, types, hooks, and dependencies.

---

## 1. Announcement

**Package:** `@repo/announcement`
**Description:** Announcements are a great way to inform users about new features, updates, or other important information.
**Source:** `packages/announcement/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `Announcement` | `AnnouncementProps` (HTMLAttributes\<HTMLAnchorElement\>) | Root announcement container, renders as an anchor element |
| `AnnouncementBadge` | `AnnouncementBadgeProps` (ComponentProps\<typeof Badge\>) | Badge sub-component within the announcement |
| `AnnouncementMessage` | `AnnouncementMessageProps` (HTMLAttributes\<HTMLSpanElement\>) | Text message sub-component |
| `AnnouncementIcon` | `AnnouncementIconProps` ({ className?: string }) | Arrow icon indicator |

### Exported Types

- `AnnouncementProps`
- `AnnouncementBadgeProps`
- `AnnouncementMessageProps`
- `AnnouncementIconProps`

### shadcn/ui Dependencies

- `@/components/ui/badge`
- `@/lib/utils`

### External Dependencies

- `lucide-react`

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 2. Avatar Stack

**Package:** `@repo/avatar-stack`
**Description:** Stacked avatars component with tooltips for displaying groups of users.
**Source:** `packages/avatar-stack/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `AvatarStack` | `AvatarStackProps` | Root container rendering stacked avatars with overflow indicator |

### Exported Types

- `AvatarStackProps` - `{ avatars: { src: string; alt: string }[]; limit?: number; size?: number; className?: string }`

### shadcn/ui Dependencies

- `@/components/ui/avatar`
- `@/components/ui/tooltip`
- `@/lib/utils`

### External Dependencies

- None

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 3. Banner

**Package:** `@repo/banner`
**Description:** A banner is a component that displays a message to the user. It can be used to display a promotion, a warning, or any other message.
**Source:** `packages/banner/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `Banner` | `BannerProps` | Root banner container |
| `BannerContent` | `BannerContentProps` | Content area of the banner |
| `BannerTitle` | `BannerTitleProps` | Title text element |
| `BannerDescription` | `BannerDescriptionProps` | Description text element |
| `BannerAction` | `BannerActionProps` | Action button area |
| `BannerImage` | `BannerImageProps` | Image element for the banner |

### Exported Types

- `BannerProps` - HTMLAttributes\<HTMLDivElement\>
- `BannerContentProps` - HTMLAttributes\<HTMLDivElement\>
- `BannerTitleProps` - HTMLAttributes\<HTMLHeadingElement\>
- `BannerDescriptionProps` - HTMLAttributes\<HTMLParagraphElement\>
- `BannerActionProps` - HTMLAttributes\<HTMLDivElement\>
- `BannerImageProps` - ComponentProps\<"img"\> & { alt: string }

### shadcn/ui Dependencies

- `@/lib/utils`

### External Dependencies

- None

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 4. Calendar

**Package:** `@repo/calendar`
**Description:** The Calendar component is used to display a calendar with events.
**Source:** `packages/calendar/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `CalendarProvider` | `CalendarProviderProps` | Root provider wrapping the calendar with context |
| `CalendarDate` | `CalendarDateProps` | Displays the current date |
| `CalendarDatePagination` | `CalendarDatePaginationProps` | Navigation buttons for date pagination |
| `CalendarDatePicker` | `CalendarDatePickerProps` | Date picker popover |
| `CalendarHeader` | `CalendarHeaderProps` | Header row of the calendar |
| `CalendarMonthPicker` | `CalendarMonthPickerProps` | Month selection popover |
| `CalendarViewTrigger` | `CalendarViewTriggerProps` | Toggle between calendar views |
| `CalendarBody` | `CalendarBodyProps` | Body content of the calendar |
| `CalendarItem` | `CalendarItemProps` | Individual calendar cell |

### Exported Types

- `CalendarEvent` - `{ id: string; name: string; startAt: Date; endAt: Date; color: string }`
- `CalendarProviderProps<T>` - `{ children: ReactNode; events?: T[]; className?: string; locale?: string }`
- `CalendarDateProps`, `CalendarDatePaginationProps`, `CalendarDatePickerProps`
- `CalendarHeaderProps`, `CalendarMonthPickerProps`, `CalendarViewTriggerProps`
- `CalendarBodyProps`, `CalendarItemProps`

### shadcn/ui Dependencies

- `@/components/ui/button`
- `@/components/ui/calendar` (DayPicker)
- `@/components/ui/popover`
- `@/components/ui/select`
- `@/lib/utils`

### External Dependencies

- `date-fns`, `lucide-react`

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 5. Choicebox

**Package:** `@repo/choicebox`
**Description:** Choiceboxes are a great way to let users select one or more options from a list.
**Source:** `packages/choicebox/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `Choicebox` | `ChoiceboxProps` | Individual selectable card item |
| `ChoiceboxGroup` | `ChoiceboxGroupProps` | Container for grouping choicebox items |

### Exported Types

- `ChoiceboxProps` - `{ value?: string; title?: string; description?: string; icon?: ReactNode; disabled?: boolean; className?: string }`
- `ChoiceboxGroupProps` - `{ children: ReactNode; defaultValue?: string | string[]; value?: string | string[]; onValueChange?: (value: string | string[]) => void; multiple?: boolean; columns?: number; className?: string }`

### shadcn/ui Dependencies

- `@/lib/utils`

### External Dependencies

- `lucide-react`, `radix-ui`

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 6. Code Block

**Package:** `@repo/code-block`
**Description:** Code blocks are used to display code snippets with syntax highlighting.
**Source:** `packages/code-block/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `CodeBlock` | `CodeBlockProps` | Root container for the code block |
| `CodeBlockHeader` | `CodeBlockHeaderProps` | Header area with filename/language |
| `CodeBlockBody` | `CodeBlockBodyProps` | Body area containing the highlighted code |
| `CodeBlockCopyButton` | `CodeBlockCopyButtonProps` | Copy-to-clipboard button |
| `CodeBlockContent` | `CodeBlockContentProps` | All-in-one code block combining header, body, and copy button |

### Exported Types

- `CodeBlockProps` - HTMLAttributes\<HTMLDivElement\> & { filename?: string }
- `CodeBlockHeaderProps` - HTMLAttributes\<HTMLDivElement\>
- `CodeBlockBodyProps` - HTMLAttributes\<HTMLDivElement\>
- `CodeBlockCopyButtonProps` - ButtonHTMLAttributes\<HTMLButtonElement\> & { value: string; onCopy?: () => void; onError?: (error: Error) => void; timeout?: number }
- `CodeBlockContentProps` - `{ code: string; language?: BundledLanguage; theme?: BundledTheme; filename?: string }`

### shadcn/ui Dependencies

- `@/lib/utils`

### External Dependencies

- `lucide-react`, `shiki`

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 7. Color Picker

**Package:** `@repo/color-picker`
**Description:** Color picker component.
**Source:** `packages/color-picker/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `ColorPicker` | `ColorPickerProps` | Color picker with swatch grid, hue slider, and hex input |

### Exported Types

- `ColorPickerProps` - `{ value?: string; defaultValue?: string; onChange?: (value: string) => void; className?: string; swatches?: string[] }`

### shadcn/ui Dependencies

- `@/components/ui/input`
- `@/components/ui/label`
- `@/components/ui/popover`
- `@/lib/utils`

### External Dependencies

- `culori`, `lucide-react`

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 8. Combobox

**Package:** `@repo/combobox`
**Description:** Combobox is a component that allows you to search and select items from a list.
**Source:** `packages/combobox/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `Combobox` | `ComboboxProps` | Root combobox provider wrapping a Popover |
| `ComboboxTrigger` | `ComboboxTriggerProps` | Trigger button for the combobox popover |
| `ComboboxContent` | `ComboboxContentProps` | Popover content with Command component |
| `ComboboxInput` | `ComboboxInputProps` | Search input field |
| `ComboboxList` | `ComboboxListProps` | Scrollable list of items |
| `ComboboxEmpty` | `ComboboxEmptyProps` | Empty state message |
| `ComboboxGroup` | `ComboboxGroupProps` | Group container for items |
| `ComboboxItem` | `ComboboxItemProps` | Individual selectable item |

### Exported Types

- `ComboboxProps` - `{ value?: string; setValue?: (value: string) => void; open?: boolean; onOpenChange?: (open: boolean) => void; children?: ReactNode }`
- `ComboboxTriggerProps` - ComponentProps\<typeof Button\>
- `ComboboxContentProps` - ComponentProps\<typeof PopoverContent\>
- `ComboboxInputProps` - ComponentProps\<typeof CommandInput\>
- `ComboboxListProps` - ComponentProps\<typeof CommandList\>
- `ComboboxEmptyProps` - ComponentProps\<typeof CommandEmpty\>
- `ComboboxGroupProps` - ComponentProps\<typeof CommandGroup\>
- `ComboboxItemProps` - ComponentProps\<typeof CommandItem\>

### shadcn/ui Dependencies

- `@/components/ui/button`
- `@/components/ui/command`
- `@/components/ui/popover`
- `@/lib/utils`

### External Dependencies

- `lucide-react`

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 9. Comparison

**Package:** `@repo/comparison`
**Description:** A comparison slider is a visual tool that allows users to compare two images side by side.
**Source:** `packages/comparison/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `Comparison` | `ComparisonProps` | Root comparison container |
| `ComparisonImage` | `ComparisonImageProps` | An image that can be positioned as "first" or "last" in the comparison |
| `ComparisonSlider` | `ComparisonSliderProps` | The draggable slider divider |

### Exported Types

- `ComparisonProps` - HTMLAttributes\<HTMLDivElement\>
- `ComparisonImageProps` - ComponentProps\<"img"\> & { position: "first" | "last" }
- `ComparisonSliderProps` - HTMLAttributes\<HTMLDivElement\>

### shadcn/ui Dependencies

- `@/lib/utils`

### External Dependencies

- None

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 10. Contribution Graph

**Package:** `@repo/contribution-graph`
**Description:** A contribution graph is a visual representation of contributions over time.
**Source:** `packages/contribution-graph/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `ContributionGraph` | `ContributionGraphProps` | Root graph provider with context |
| `ContributionGraphHeader` | `ContributionGraphHeaderProps` | Header with title and year/level selectors |
| `ContributionGraphContent` | `ContributionGraphContentProps` | Main grid content area |
| `ContributionGraphFooter` | `ContributionGraphFooterProps` | Footer with legend |

### Exported Types

- `ContributionData` - `{ date: string; count: number }`
- `ContributionGraphProps` - HTMLAttributes\<HTMLDivElement\> & { data: ContributionData[]; levels?: number; colorScheme?: Record\<string, string\> }
- `ContributionGraphHeaderProps` - HTMLAttributes\<HTMLDivElement\>
- `ContributionGraphContentProps` - HTMLAttributes\<HTMLDivElement\>
- `ContributionGraphFooterProps` - HTMLAttributes\<HTMLDivElement\>

### shadcn/ui Dependencies

- `@/components/ui/select`
- `@/components/ui/tooltip`
- `@/lib/utils`

### External Dependencies

- `date-fns`, `lucide-react`

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 11. Credit Card

**Package:** `@repo/credit-card`
**Description:** A credit card component that displays a credit card with a number, name, and expiry date.
**Source:** `packages/credit-card/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `CreditCard` | `CreditCardProps` | Root card container |
| `CreditCardChip` | `CreditCardChipProps` | Card chip icon |
| `CreditCardNetwork` | `CreditCardNetworkProps` | Payment network logo (Visa, Mastercard, Amex, etc.) |
| `CreditCardNumber` | `CreditCardNumberProps` | Masked card number display |
| `CreditCardName` | `CreditCardNameProps` | Cardholder name |
| `CreditCardExpiry` | `CreditCardExpiryProps` | Expiration date |
| `CreditCardGroup` | `CreditCardGroupProps` | Group container for card sub-elements |

### Exported Types

- `CreditCardProps` - HTMLAttributes\<HTMLDivElement\>
- `CreditCardChipProps` - HTMLAttributes\<HTMLDivElement\>
- `CreditCardNetworkProps` - HTMLAttributes\<HTMLDivElement\> & { network: "visa" | "mastercard" | "amex" | "discover" | "diners" | "jcb" | "unionpay" }
- `CreditCardNumberProps` - HTMLAttributes\<HTMLParagraphElement\> & { number: string }
- `CreditCardNameProps` - HTMLAttributes\<HTMLParagraphElement\> & { name: string }
- `CreditCardExpiryProps` - HTMLAttributes\<HTMLParagraphElement\> & { month: number; year: number }
- `CreditCardGroupProps` - HTMLAttributes\<HTMLDivElement\>

### shadcn/ui Dependencies

- `@/lib/utils`

### External Dependencies

- None

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 12. Cursor

**Package:** `@repo/cursor`
**Description:** Cursor components are used to display a cursor with a name tag.
**Source:** `packages/cursor/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `Cursor` | `CursorProps` | Animated cursor with name badge |

### Exported Types

- `CursorProps` - `{ name: string; color?: string; className?: string }`

### shadcn/ui Dependencies

- `@/lib/utils`

### External Dependencies

- `motion` (motion/react)

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 13. Deck

**Package:** `@repo/deck`
**Description:** A deck component that displays a stack of cards. It is a great way to display a list of items.
**Source:** `packages/deck/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `Deck` | `DeckProps` | Root deck container, renders stacked cards |
| `DeckContent` | `DeckContentProps` | Content area for individual cards |
| `DeckTitle` | `DeckTitleProps` | Card title |
| `DeckDescription` | `DeckDescriptionProps` | Card description |
| `DeckNavigation` | `DeckNavigationProps` | Previous/Next navigation buttons |

### Exported Types

- `DeckProps` - HTMLAttributes\<HTMLDivElement\>
- `DeckContentProps` - HTMLAttributes\<HTMLDivElement\>
- `DeckTitleProps` - HTMLAttributes\<HTMLHeadingElement\>
- `DeckDescriptionProps` - HTMLAttributes\<HTMLParagraphElement\>
- `DeckNavigationProps` - HTMLAttributes\<HTMLDivElement\>

### shadcn/ui Dependencies

- `@/components/ui/button`
- `@/lib/utils`

### External Dependencies

- `lucide-react`, `motion` (motion/react)

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 14. Dialog Stack

**Package:** `@repo/dialog-stack`
**Description:** Stacked dialogs that animate in and out.
**Source:** `packages/dialog-stack/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `DialogStack` | `DialogStackProps` | Root provider managing stacked dialog state |
| `DialogStackTrigger` | `DialogStackTriggerProps` | Trigger to open a specific dialog by index |
| `DialogStackOverlay` | `DialogStackOverlayProps` | Background overlay |
| `DialogStackContent` | `DialogStackContentProps` | Individual dialog content panel |
| `DialogStackHeader` | `DialogStackHeaderProps` | Dialog header area |
| `DialogStackTitle` | `DialogStackTitleProps` | Dialog title |
| `DialogStackDescription` | `DialogStackDescriptionProps` | Dialog description |
| `DialogStackBody` | `DialogStackBodyProps` | Dialog body content |
| `DialogStackFooter` | `DialogStackFooterProps` | Dialog footer area |
| `DialogStackClose` | `DialogStackCloseProps` | Close button |

### Exported Types

- `DialogStackProps` - `{ children: ReactNode; open?: boolean; onOpenChange?: (open: boolean) => void }`
- All individual props types for each sub-component

### Exported Hooks

- `useDialogStack()` - Returns `{ activeIndex, setActiveIndex, open, setOpen }`

### shadcn/ui Dependencies

- `@/lib/utils`

### External Dependencies

- `lucide-react`, `motion` (motion/react), `radix-ui`

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 15. Dropzone

**Package:** `@repo/dropzone`
**Description:** A dropzone component that allows users to upload files by dragging and dropping them into the component.
**Source:** `packages/dropzone/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `Dropzone` | `DropzoneProps` | Root dropzone provider with context |
| `DropzoneContent` | `DropzoneContentProps` | The drop target area |
| `DropzoneInput` | `DropzoneInputProps` | Hidden file input element |
| `DropzoneTrigger` | `DropzoneTriggerProps` | Clickable trigger to open the file dialog |
| `DropzoneMessage` | `DropzoneMessageProps` | Message displayed in the dropzone |

### Exported Types

- `DropzoneProps` - `{ children: ReactNode; accept?: Record<string, string[]>; maxFiles?: number; maxSize?: number; onDrop?: (acceptedFiles: File[]) => void; className?: string }`
- `DropzoneContentProps` - HTMLAttributes\<HTMLDivElement\>
- `DropzoneInputProps` - InputHTMLAttributes\<HTMLInputElement\>
- `DropzoneTriggerProps` - ComponentProps\<typeof Button\>
- `DropzoneMessageProps` - HTMLAttributes\<HTMLParagraphElement\>

### shadcn/ui Dependencies

- `@/components/ui/button`
- `@/lib/utils`

### External Dependencies

- `react-dropzone`

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 16. Editor

**Package:** `@repo/editor`
**Description:** A block-style rich text editor built on Tiptap.
**Source:** `packages/editor/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `EditorProvider` | `EditorProviderProps` | Root editor provider wrapping Tiptap |
| `EditorFloatingMenu` | `EditorFloatingMenuProps` | Floating toolbar menu |
| `EditorBubbleMenu` | `EditorBubbleMenuProps` | Selection bubble toolbar |
| `EditorSelector` | `EditorSelectorProps` | Block type selector dropdown |
| `EditorClearFormatting` | `EditorClearFormattingProps` | Clear formatting button |
| `EditorNodeText` | `EditorNodeTextProps` | Paragraph node button |
| `EditorNodeHeading1` | `EditorNodeHeading1Props` | Heading 1 node button |
| `EditorNodeHeading2` | `EditorNodeHeading2Props` | Heading 2 node button |
| `EditorNodeHeading3` | `EditorNodeHeading3Props` | Heading 3 node button |
| `EditorNodeBulletList` | `EditorNodeBulletListProps` | Bullet list node button |
| `EditorNodeOrderedList` | `EditorNodeOrderedListProps` | Ordered list node button |
| `EditorNodeTaskList` | `EditorNodeTaskListProps` | Task list node button |
| `EditorNodeQuote` | `EditorNodeQuoteProps` | Blockquote node button |
| `EditorNodeCode` | `EditorNodeCodeProps` | Code block node button |
| `EditorNodeTable` | `EditorNodeTableProps` | Table node button |
| `EditorFormatBold` | `EditorFormatBoldProps` | Bold format toggle |
| `EditorFormatItalic` | `EditorFormatItalicProps` | Italic format toggle |
| `EditorFormatStrike` | `EditorFormatStrikeProps` | Strikethrough format toggle |
| `EditorFormatCode` | `EditorFormatCodeProps` | Inline code format toggle |
| `EditorFormatSubscript` | `EditorFormatSubscriptProps` | Subscript format toggle |
| `EditorFormatSuperscript` | `EditorFormatSuperscriptProps` | Superscript format toggle |
| `EditorFormatUnderline` | `EditorFormatUnderlineProps` | Underline format toggle |
| `EditorLinkSelector` | `EditorLinkSelectorProps` | Link insertion/editing popover |
| `EditorTableMenu` | `EditorTableMenuProps` | Table operations menu |
| `EditorTableGlobalMenu` | `EditorTableGlobalMenuProps` | Global table operations |
| `EditorTableColumnMenu` | `EditorTableColumnMenuProps` | Column operations menu |
| `EditorTableRowMenu` | `EditorTableRowMenuProps` | Row operations menu |
| `EditorTableColumnBefore` | (none) | Insert column before |
| `EditorTableColumnAfter` | (none) | Insert column after |
| `EditorTableRowBefore` | (none) | Insert row before |
| `EditorTableRowAfter` | (none) | Insert row after |
| `EditorTableColumnDelete` | (none) | Delete column |
| `EditorTableRowDelete` | (none) | Delete row |
| `EditorTableHeaderColumnToggle` | (none) | Toggle header column |
| `EditorTableHeaderRowToggle` | (none) | Toggle header row |
| `EditorTableDelete` | (none) | Delete table |
| `EditorTableMergeCells` | (none) | Merge cells |
| `EditorTableSplitCell` | (none) | Split cell |
| `EditorTableFix` | (none) | Fix table |
| `EditorCharacterCount` | object | Character/word count display (with `.Text` and `.Words` sub-components) |

### Exported Types

- `EditorProviderProps` - TiptapEditorProviderProps & { className?: string; throttleDelay?: number }
- `SuggestionItem` - `{ title: string; description: string; icon: ReactNode; command: (props: { editor: Editor; range: Range }) => void }`
- Re-exported: `Editor`, `JSONContent` from `@tiptap/react`
- `EditorFloatingMenuProps`, `EditorBubbleMenuProps`, `EditorSelectorProps`
- `EditorLinkSelectorProps`, `EditorTableMenuProps`, and many more
- `EditorCharacterCountProps` - `{ className?: string; limit?: number }`

### Exported Constants

- `defaultSlashSuggestions` - Default slash command suggestion items

### shadcn/ui Dependencies

- `@/components/ui/button`
- `@/components/ui/command`
- `@/components/ui/dropdown-menu`
- `@/components/ui/popover`
- `@/components/ui/separator`
- `@/components/ui/tooltip`
- `@/lib/utils`

### External Dependencies

- `@tiptap/core`, `@tiptap/react`, `@tiptap/react/menus`, `@tiptap/pm/model`, `@tiptap/pm/state`
- `@tiptap/extension-code-block-lowlight`, `@tiptap/extension-list`, `@tiptap/extension-subscript`
- `@tiptap/extension-superscript`, `@tiptap/extension-table`, `@tiptap/extension-text-style`
- `@tiptap/extension-typography`, `@tiptap/extensions`
- `lucide-react`, `tippy.js`

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 17. Gantt

**Package:** `@repo/gantt`
**Description:** A Gantt chart is a visual tool for planning and scheduling projects over time.
**Source:** `packages/gantt/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `GanttProvider` | `GanttProviderProps` | Root provider with Gantt context and DnD |
| `GanttHeader` | `GanttHeaderProps` | Header area |
| `GanttSidebar` | `GanttSidebarProps` | Side panel listing features |
| `GanttSidebarHeader` | (none) | Sidebar header |
| `GanttSidebarGroup` | `GanttSidebarGroupProps` | Group within sidebar |
| `GanttSidebarItem` | `GanttSidebarItemProps` | Individual feature item in sidebar |
| `GanttTimeline` | `GanttTimelineProps` | Timeline content area |
| `GanttContentHeader` | `GanttContentHeaderProps` | Column headers for time periods |
| `GanttColumns` | `GanttColumnsProps` | Column grid lines |
| `GanttColumn` | `GanttColumnProps` | Individual column |
| `GanttFeatureList` | `GanttFeatureListProps` | List of feature rows |
| `GanttFeatureListGroup` | `GanttFeatureListGroupProps` | Grouped features |
| `GanttFeatureRow` | `GanttFeatureRowProps` | Individual feature row |
| `GanttFeatureItem` | `GanttFeatureItemProps` | Draggable feature bar |
| `GanttFeatureItemCard` | `GanttFeatureItemCardProps` | Card inside feature bar |
| `GanttFeatureDragHelper` | `GanttFeatureDragHelperProps` | Drag helper for resizing |
| `GanttAddFeatureHelper` | `GanttAddFeatureHelperProps` | Add feature inline |
| `GanttCreateMarkerTrigger` | `GanttCreateMarkerTriggerProps` | Trigger to create a marker |
| `GanttMarker` | (FC with props) | Timeline marker |
| `GanttToday` | `GanttTodayProps` | Today indicator line |

### Exported Types

- `GanttStatus` - `{ id: string; name: string; color: string }`
- `GanttFeature` - `{ id: string; name: string; startAt: Date; endAt: Date; status: GanttStatus }`
- `GanttMarkerProps` - `{ id: string; date: Date; label: string; className?: string }`
- `Range` - `"daily" | "monthly" | "quarterly"`
- `TimelineData` - `{ year: number; quarters: { months: { date: Date; days: Date[] }[] }[] }`
- `GanttContextProps` - Context type for Gantt state
- `GanttProviderProps`, and all sub-component props types

### Exported Hooks

- `useGanttDragging()` - Returns `[boolean, (value: boolean) => void]`
- `useGanttScrollX()` - Returns `[number, (value: number) => void]`

### shadcn/ui Dependencies

- `@/components/ui/card`
- `@/components/ui/context-menu`
- `@/lib/utils`

### External Dependencies

- `@dnd-kit/core`, `@dnd-kit/modifiers`
- `@uidotdev/usehooks`, `date-fns`, `jotai`, `lodash.throttle`, `lucide-react`

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 18. Glimpse

**Package:** `@repo/glimpse`
**Description:** A component that shows a preview of a URL when hovering over a link.
**Source:** `packages/glimpse/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `Glimpse` | `GlimpseProps` | Root hover card wrapper |
| `GlimpseContent` | `GlimpseContentProps` | Hover card content area |
| `GlimpseTrigger` | `GlimpseTriggerProps` | Hover trigger element |
| `GlimpseTitle` | `GlimpseTitleProps` | Title text |
| `GlimpseDescription` | `GlimpseDescriptionProps` | Description text |
| `GlimpseImage` | `GlimpseImageProps` | Preview image |

### Exported Types

- `GlimpseProps` - ComponentProps\<typeof HoverCard\>
- `GlimpseContentProps` - ComponentProps\<typeof HoverCardContent\>
- `GlimpseTriggerProps` - ComponentProps\<typeof HoverCardTrigger\>
- `GlimpseTitleProps` - ComponentProps\<"p"\>
- `GlimpseDescriptionProps` - ComponentProps\<"p"\>
- `GlimpseImageProps` - ComponentProps\<"img"\>

### shadcn/ui Dependencies

- `@/components/ui/hover-card`
- `@/lib/utils` (imported from `@repo/shadcn-ui/lib/utils`)

### External Dependencies

- None

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 19. Image Crop

**Package:** `@repo/image-crop`
**Description:** Helps you crop images to a specific size or aspect ratio.
**Source:** `packages/image-crop/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `ImageCrop` | `ImageCropProps` | Root provider managing crop state |
| `ImageCropContent` | `ImageCropContentProps` | The crop area with ReactCrop |
| `ImageCropApply` | `ImageCropApplyProps` | Apply crop button |
| `ImageCropReset` | `ImageCropResetProps` | Reset crop button |
| `Cropper` | `CropperProps` | All-in-one crop component (convenience wrapper) |

### Exported Types

- `ImageCropProps` - `{ file: File; maxImageSize?: number; onCrop?: (croppedImage: string) => void; children: ReactNode } & Omit<ReactCropProps, "onChange" | "onComplete" | "children">`
- `ImageCropContentProps` - `{ style?: CSSProperties; className?: string }`
- `ImageCropApplyProps` - ComponentProps\<"button"\> & { asChild?: boolean }
- `ImageCropResetProps` - ComponentProps\<"button"\> & { asChild?: boolean }
- `CropperProps` - Omit\<ReactCropProps, "onChange"\> & { file: File; maxImageSize?: number; onCrop?: (croppedImage: string) => void; onChange?: ReactCropProps["onChange"] }

### shadcn/ui Dependencies

- `@/components/ui/button` (imported from `@repo/shadcn-ui/components/ui/button`)
- `@/lib/utils`

### External Dependencies

- `lucide-react`, `radix-ui`, `react-image-crop`

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 20. Image Zoom

**Package:** `@repo/image-zoom`
**Description:** Image zoom is a component that allows you to zoom in on an image.
**Source:** `packages/image-zoom/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `ImageZoom` | `ImageZoomProps` | Zoomable image wrapper using react-medium-image-zoom |

### Exported Types

- `ImageZoomProps` - UncontrolledProps & { isZoomed?: ControlledProps["isZoomed"]; onZoomChange?: ControlledProps["onZoomChange"]; className?: string; backdropClassName?: string }

### shadcn/ui Dependencies

- `@/lib/utils`

### External Dependencies

- `react-medium-image-zoom`

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 21. Kanban

**Package:** `@repo/kanban`
**Description:** A kanban board is a visual tool that helps you manage and visualize your work. It is a board with columns, and each column represents a status.
**Source:** `packages/kanban/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `KanbanProvider` | `KanbanProviderProps<T, C>` | Root provider with DnD context |
| `KanbanBoard` | `KanbanBoardProps` | A droppable column container |
| `KanbanCard` | `KanbanCardProps<T>` | Sortable card item |
| `KanbanCards` | `KanbanCardsProps<T>` | Container rendering cards filtered by column |
| `KanbanHeader` | `KanbanHeaderProps` | Column header |

### Exported Types

- Re-exported: `DragEndEvent` from `@dnd-kit/core`
- `KanbanBoardProps` - `{ id: string; children: ReactNode; className?: string }`
- `KanbanCardProps<T>` - T & { children?: ReactNode; className?: string }
- `KanbanCardsProps<T>` - Omit\<HTMLAttributes\<HTMLDivElement\>, "children" | "id"\> & { children: (item: T) => ReactNode; id: string }
- `KanbanHeaderProps` - HTMLAttributes\<HTMLDivElement\>
- `KanbanProviderProps<T, C>` - Omit\<DndContextProps, "children"\> & { children: (column: C) => ReactNode; className?: string; columns: C[]; data: T[]; onDataChange?: (data: T[]) => void; onDragStart?: ...; onDragEnd?: ...; onDragOver?: ... }

### shadcn/ui Dependencies

- `@/components/ui/card`
- `@/components/ui/scroll-area`
- `@/lib/utils`

### External Dependencies

- `@dnd-kit/core`, `@dnd-kit/sortable`, `@dnd-kit/utilities`, `tunnel-rat`

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 22. List

**Package:** `@repo/list`
**Description:** List views are a great way to show a list of tasks grouped by status and ranked by priority.
**Source:** `packages/list/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `ListProvider` | `ListProviderProps` | Root DnD provider with vertical axis constraint |
| `ListGroup` | `ListGroupProps` | Droppable group container |
| `ListHeader` | `ListHeaderProps` | Group header (accepts children or name/color) |
| `ListItems` | `ListItemsProps` | Items container |
| `ListItem` | `ListItemProps` | Draggable list item |

### Exported Types

- Re-exported: `DragEndEvent` from `@dnd-kit/core`
- `ListProviderProps` - `{ children: ReactNode; onDragEnd: (event: DragEndEvent) => void; className?: string }`
- `ListGroupProps` - `{ id: string; children: ReactNode; className?: string }`
- `ListHeaderProps` - `{ children: ReactNode } | { name: string; color: string; className?: string }`
- `ListItemsProps` - `{ children: ReactNode; className?: string }`
- `ListItemProps` - `{ id: string; name: string; index: number; parent: string; children?: ReactNode; className?: string }`

### shadcn/ui Dependencies

- `@/lib/utils`

### External Dependencies

- `@dnd-kit/core`, `@dnd-kit/modifiers`

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 23. Marquee

**Package:** `@repo/marquee`
**Description:** Marquees are a great way to show a list of items in a horizontal scrolling motion.
**Source:** `packages/marquee/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `Marquee` | `MarqueeProps` | Root container with overflow hidden |
| `MarqueeContent` | `MarqueeContentProps` | Scrolling content powered by react-fast-marquee |
| `MarqueeFade` | `MarqueeFadeProps` | Gradient fade overlay on left or right side |
| `MarqueeItem` | `MarqueeItemProps` | Individual item in the marquee |

### Exported Types

- `MarqueeProps` - HTMLAttributes\<HTMLDivElement\>
- `MarqueeContentProps` - FastMarqueeProps
- `MarqueeFadeProps` - HTMLAttributes\<HTMLDivElement\> & { side: "left" | "right" }
- `MarqueeItemProps` - HTMLAttributes\<HTMLDivElement\>

### shadcn/ui Dependencies

- `@/lib/utils`

### External Dependencies

- `react-fast-marquee`

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 24. Mini Calendar

**Package:** `@repo/mini-calendar`
**Description:** A composable mini calendar component for picking dates close to today.
**Source:** `packages/mini-calendar/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `MiniCalendar` | `MiniCalendarProps` | Root provider with controllable date state |
| `MiniCalendarNavigation` | `MiniCalendarNavigationProps` | Prev/next navigation buttons |
| `MiniCalendarDays` | `MiniCalendarDaysProps` | Renders consecutive date buttons |
| `MiniCalendarDay` | `MiniCalendarDayProps` | Individual day button |

### Exported Types

- `MiniCalendarProps` - HTMLAttributes\<HTMLDivElement\> & { value?: Date; defaultValue?: Date; onValueChange?: (date: Date | undefined) => void; startDate?: Date; defaultStartDate?: Date; onStartDateChange?: (date: Date | undefined) => void; days?: number }
- `MiniCalendarNavigationProps` - ButtonHTMLAttributes\<HTMLButtonElement\> & { direction: "prev" | "next"; asChild?: boolean }
- `MiniCalendarDaysProps` - Omit\<HTMLAttributes\<HTMLDivElement\>, "children"\> & { children: (date: Date) => ReactNode }
- `MiniCalendarDayProps` - ComponentProps\<typeof Button\> & { date: Date }

### shadcn/ui Dependencies

- `@/components/ui/button`
- `@/lib/utils`

### External Dependencies

- `@radix-ui/react-use-controllable-state`, `date-fns`, `lucide-react`, `radix-ui`

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 25. Pill

**Package:** `@repo/pill`
**Description:** A flexible badge component designed for a variety of use cases.
**Source:** `packages/pill/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `Pill` | `PillProps` | Root pill badge |
| `PillAvatar` | `PillAvatarProps` | Small avatar within the pill |
| `PillButton` | `PillButtonProps` | Action button within the pill |
| `PillStatus` | `PillStatusProps` | Status section with border separator |
| `PillIndicator` | `PillIndicatorProps` | Colored dot indicator |
| `PillDelta` | `PillDeltaProps` | Up/down/neutral change indicator |
| `PillIcon` | `PillIconProps` | Icon within the pill |
| `PillAvatarGroup` | `PillAvatarGroupProps` | Overlapping avatar group |

### Exported Types

- `PillProps` - ComponentProps\<typeof Badge\> & { themed?: boolean }
- `PillAvatarProps` - ComponentProps\<typeof AvatarImage\> & { fallback?: string }
- `PillButtonProps` - ComponentProps\<typeof Button\>
- `PillStatusProps` - `{ children: ReactNode; className?: string }`
- `PillIndicatorProps` - `{ variant?: "success" | "error" | "warning" | "info"; pulse?: boolean }`
- `PillDeltaProps` - `{ className?: string; delta: number }`
- `PillIconProps` - `{ icon: typeof ChevronUpIcon; className?: string }`
- `PillAvatarGroupProps` - `{ children: ReactNode; className?: string }`

### shadcn/ui Dependencies

- `@/components/ui/avatar`
- `@/components/ui/badge`
- `@/components/ui/button`
- `@/lib/utils`

### External Dependencies

- `lucide-react`

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 26. QR Code

**Package:** `@repo/qr-code`
**Description:** QR Code is a component that generates a QR code from a string.
**Source:** `packages/qr-code/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `QRCode` | `QRCodeProps` | Generates and renders a QR code SVG |

### Exported Types

- `QRCodeProps` - HTMLAttributes\<HTMLDivElement\> & { data: string; foreground?: string; background?: string; robustness?: "L" | "M" | "Q" | "H" }

### shadcn/ui Dependencies

- `@/lib/utils`

### External Dependencies

- `culori`, `qrcode`

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 27. Rating

**Package:** `@repo/rating`
**Description:** A star rating component with keyboard navigation and hover effects.
**Source:** `packages/rating/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `Rating` | `RatingProps` | Root rating provider with keyboard navigation |
| `RatingButton` | `RatingButtonProps` | Individual star/icon button |

### Exported Types

- `RatingProps` - `{ defaultValue?: number; value?: number; onChange?: (event, value: number) => void; onValueChange?: (value: number) => void; readOnly?: boolean; className?: string; children?: ReactNode }`
- `RatingButtonProps` - LucideProps & { index?: number; icon?: ReactElement\<LucideProps\> }

### shadcn/ui Dependencies

- `@/lib/utils`

### External Dependencies

- `@radix-ui/react-use-controllable-state`, `lucide-react`

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 28. Reel

**Package:** `@repo/reel`
**Description:** A composable Reel component that looks like Instagram Stories - a full-height, 9:16 aspect ratio container with video playback and progress indicators.
**Source:** `packages/reel/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `Reel` | `ReelProps` | Root provider managing playback state |
| `ReelContent` | `ReelContentProps` | Animated content area with item transitions |
| `ReelItem` | `ReelItemProps` | Container for individual reel items |
| `ReelVideo` | `ReelVideoProps` | Video element with progress tracking |
| `ReelImage` | `ReelImageProps` | Image element with timed progress |
| `ReelProgress` | `ReelProgressProps` | Progress indicator bar (like Stories) |
| `ReelControls` | `ReelControlsProps` | Control bar container |
| `ReelPreviousButton` | `ReelPreviousButtonProps` | Previous item button |
| `ReelNextButton` | `ReelNextButtonProps` | Next item button |
| `ReelPlayButton` | `ReelPlayButtonProps` | Play/pause toggle |
| `ReelMuteButton` | `ReelMuteButtonProps` | Mute/unmute toggle |
| `ReelNavigation` | `ReelNavigationProps` | Tap-to-navigate overlay |
| `ReelOverlay` | `ReelOverlayProps` | Overlay layer |
| `ReelHeader` | `ReelHeaderProps` | Top gradient header |
| `ReelFooter` | `ReelFooterProps` | Bottom gradient footer |

### Exported Types

- `ReelItem` (type) - `{ id: string | number; type: "video" | "image"; src: string; duration: number; alt?: string; title?: string; description?: string }`
- `ReelProps` - HTMLAttributes\<HTMLDivElement\> & { data: ReelItem[]; defaultIndex?: number; index?: number; onIndexChange?: ...; playing?: boolean; muted?: boolean; autoPlay?: boolean; ... }
- All individual component props types

### shadcn/ui Dependencies

- `@/components/ui/button`
- `@/components/ui/progress`
- `@/lib/utils`

### External Dependencies

- `@radix-ui/react-use-controllable-state`, `lucide-react`, `motion` (motion/react)

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 29. Relative Time

**Package:** `@repo/relative-time`
**Description:** A component that displays time in various timezones.
**Source:** `packages/relative-time/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `RelativeTime` | `RelativeTimeProps` | Root provider with auto-updating time |
| `RelativeTimeZone` | `RelativeTimeZoneProps` | Timezone display group |
| `RelativeTimeZoneDisplay` | `RelativeTimeZoneDisplayProps` | Formatted time display |
| `RelativeTimeZoneDate` | `RelativeTimeZoneDateProps` | Formatted date display |
| `RelativeTimeZoneLabel` | `RelativeTimeZoneLabelProps` | Timezone label badge |

### Exported Types

- `RelativeTimeProps` - HTMLAttributes\<HTMLDivElement\> & { time?: Date; defaultTime?: Date; onTimeChange?: (time: Date) => void; dateFormatOptions?: Intl.DateTimeFormatOptions; timeFormatOptions?: Intl.DateTimeFormatOptions }
- `RelativeTimeZoneProps` - HTMLAttributes\<HTMLDivElement\> & { zone: string; dateFormatOptions?: ...; timeFormatOptions?: ... }
- `RelativeTimeZoneContextType` - `{ zone: string }`
- `RelativeTimeZoneDisplayProps` - HTMLAttributes\<HTMLDivElement\>
- `RelativeTimeZoneDateProps` - HTMLAttributes\<HTMLDivElement\>
- `RelativeTimeZoneLabelProps` - HTMLAttributes\<HTMLDivElement\>

### shadcn/ui Dependencies

- `@/lib/utils`

### External Dependencies

- `@radix-ui/react-use-controllable-state`

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 30. Sandbox

**Package:** `@repo/sandbox`
**Description:** The sandbox component allows you to preview and test components in a sandboxed environment.
**Source:** `packages/sandbox/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `SandboxProvider` | `SandboxProviderProps` | Root Sandpack provider wrapper |
| `SandboxLayout` | `SandboxLayoutProps` | Layout wrapper for Sandpack |
| `SandboxTabs` | `SandboxTabsProps` | Custom tabbed interface |
| `SandboxTabsList` | `SandboxTabsListProps` | Tab list container |
| `SandboxTabsTrigger` | `SandboxTabsTriggerProps` | Individual tab trigger |
| `SandboxTabsContent` | `SandboxTabsContentProps` | Tab content panel |
| `SandboxCodeEditor` | `SandboxCodeEditorProps` | Code editor panel |
| `SandboxConsole` | `SandboxConsoleProps` | Console output panel |
| `SandboxPreview` | `SandboxPreviewProps` | Live preview panel |
| `SandboxFileExplorer` | `SandboxFileExplorerProps` | File explorer panel |

### Exported Types

- `SandboxProviderProps` - SandpackProviderProps
- `SandboxLayoutProps` - SandpackLayoutProps
- `SandboxTabsProps` - HTMLAttributes\<HTMLDivElement\> & { defaultValue?: string; value?: string; onValueChange?: (value: string) => void }
- `SandboxTabsListProps` - HTMLAttributes\<HTMLDivElement\>
- `SandboxTabsTriggerProps` - Omit\<ButtonHTMLAttributes\<HTMLButtonElement\>, "onClick"\> & { value: string }
- `SandboxTabsContentProps` - HTMLAttributes\<HTMLDivElement\> & { value: string }
- `SandboxCodeEditorProps` - CodeEditorProps
- `SandboxConsoleProps` - Parameters\<typeof SandpackConsole\>[0]
- `SandboxPreviewProps` - PreviewProps & { className?: string }
- `SandboxFileExplorerProps` - ComponentProps\<typeof SandpackFileExplorer\>
- `SandboxTabsContextValue` - `{ selectedTab: string | undefined; setSelectedTab: (value: string) => void }`

### shadcn/ui Dependencies

- `@/lib/utils`

### External Dependencies

- `@codesandbox/sandpack-react`

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 31. Snippet

**Package:** `@repo/snippet`
**Description:** Snippet is a component that allows you to display and copy code in a tabbed interface.
**Source:** `packages/snippet/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `Snippet` | `SnippetProps` | Root tabbed container |
| `SnippetHeader` | `SnippetHeaderProps` | Header area |
| `SnippetCopyButton` | `SnippetCopyButtonProps` | Copy-to-clipboard button |
| `SnippetTabsList` | `SnippetTabsListProps` | Tab list (alias for TabsList) |
| `SnippetTabsTrigger` | `SnippetTabsTriggerProps` | Tab trigger button |
| `SnippetTabsContent` | `SnippetTabsContentProps` | Tab content rendered as pre |

### Exported Types

- `SnippetProps` - ComponentProps\<typeof Tabs\>
- `SnippetHeaderProps` - HTMLAttributes\<HTMLDivElement\>
- `SnippetCopyButtonProps` - ComponentProps\<typeof Button\> & { value: string; onCopy?: () => void; onError?: (error: Error) => void; timeout?: number }
- `SnippetTabsListProps` - ComponentProps\<typeof TabsList\>
- `SnippetTabsTriggerProps` - ComponentProps\<typeof TabsTrigger\>
- `SnippetTabsContentProps` - ComponentProps\<typeof TabsContent\>

### shadcn/ui Dependencies

- `@/components/ui/button`
- `@/components/ui/tabs`
- `@/lib/utils`

### External Dependencies

- `lucide-react`

### Kibo Inter-dependencies

- None (note: package.json does not list `@repo/shadcn-ui` but imports from `@/components/ui/*` which resolve via shadcn-ui)

---

## 32. Spinner

**Package:** `@repo/spinner`
**Description:** A spinner is a visual indicator that shows progress or activity.
**Source:** `packages/spinner/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `Spinner` | `SpinnerProps` | Multi-variant spinner with 8 animation styles |

### Exported Types

- `SpinnerProps` - LucideProps & { variant?: "default" | "throbber" | "pinwheel" | "circle-filled" | "ellipsis" | "ring" | "bars" | "infinite" }

### shadcn/ui Dependencies

- `@/lib/utils`
- `@repo/shadcn-ui/components/ui/spinner` (direct import)

### External Dependencies

- `lucide-react`

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 33. Status

**Package:** `@repo/status`
**Description:** Status components are used to display the uptime of a service.
**Source:** `packages/status/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `Status` | `StatusProps` | Root status badge with animated indicator |
| `StatusIndicator` | `StatusIndicatorProps` | Pulsing dot indicator |
| `StatusLabel` | `StatusLabelProps` | Status text label with auto-text based on status |

### Exported Types

- `StatusProps` - ComponentProps\<typeof Badge\> & { status: "online" | "offline" | "maintenance" | "degraded" }
- `StatusIndicatorProps` - HTMLAttributes\<HTMLSpanElement\>
- `StatusLabelProps` - HTMLAttributes\<HTMLSpanElement\>

### shadcn/ui Dependencies

- `@/components/ui/badge`
- `@/lib/utils`

### External Dependencies

- None

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 34. Stories

**Package:** `@repo/stories`
**Description:** A composable Stories component - a carousel of individual video cards like you'd see on Facebook.
**Source:** `packages/stories/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `Stories` | `StoriesProps` | Root carousel container |
| `StoriesContent` | `StoriesContentProps` | Carousel content wrapper |
| `Story` | `StoryProps` | Individual story card |
| `StoryVideo` | `StoryVideoProps` | Video element that plays on hover |
| `StoryImage` | `StoryImageProps` | Image element |
| `StoryAuthor` | `StoryAuthorProps` | Author info overlay |
| `StoryAuthorImage` | `StoryAuthorImageProps` | Author avatar |
| `StoryAuthorName` | `StoryAuthorNameProps` | Author name text |
| `StoryTitle` | `StoryTitleProps` | Story title overlay |
| `StoryOverlay` | `StoryOverlayProps` | Gradient overlay (top or bottom) |

### Exported Types

- `StoriesProps` - ComponentProps\<typeof Carousel\>
- `StoriesContentProps` - ComponentProps\<typeof CarouselContent\>
- `StoryProps` - HTMLAttributes\<HTMLDivElement\>
- `StoryVideoProps` - VideoHTMLAttributes\<HTMLVideoElement\>
- `StoryImageProps` - ComponentProps\<"img"\> & { alt: string }
- `StoryAuthorProps` - HTMLAttributes\<HTMLDivElement\>
- `StoryAuthorImageProps` - ComponentProps\<typeof Avatar\> & { src?: string; name?: string; fallback?: string }
- `StoryAuthorNameProps` - HTMLAttributes\<HTMLSpanElement\>
- `StoryTitleProps` - HTMLAttributes\<HTMLDivElement\>
- `StoryOverlayProps` - HTMLAttributes\<HTMLDivElement\> & { side?: "top" | "bottom" }

### shadcn/ui Dependencies

- `@/components/ui/avatar`
- `@/components/ui/carousel`
- `@/lib/utils`

### External Dependencies

- None

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 35. Table

**Package:** `@repo/table`
**Description:** Table views are used to display data in a tabular format. They are useful for displaying large amounts of data in a structured way.
**Source:** `packages/table/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `TableProvider` | `TableProviderProps<TData, TValue>` | Root provider with TanStack Table context |
| `TableHeader` | `TableHeaderProps` | Table header section |
| `TableHeaderGroup` | `TableHeaderGroupProps` | Header row group |
| `TableHead` | `TableHeadProps` | Individual header cell |
| `TableColumnHeader` | `TableColumnHeaderProps<TData, TValue>` | Sortable column header with dropdown |
| `TableBody` | `TableBodyProps` | Table body with empty state |
| `TableRow` | `TableRowProps` | Table data row |
| `TableCell` | `TableCellProps` | Individual data cell |

### Exported Types

- Re-exported: `ColumnDef` from `@tanstack/react-table`
- `TableContext` - Context object (exported as value)
- `TableProviderProps<TData, TValue>` - `{ columns: ColumnDef<TData, TValue>[]; data: TData[]; children: ReactNode; className?: string }`
- `TableHeadProps` - `{ header: Header<unknown, unknown>; className?: string }`
- `TableHeaderGroupProps` - `{ headerGroup: HeaderGroup<unknown>; children: (props) => ReactNode }`
- `TableHeaderProps` - `{ className?: string; children: (props) => ReactNode }`
- `TableColumnHeaderProps<TData, TValue>` - HTMLAttributes\<HTMLDivElement\> & { column: Column<TData, TValue>; title: string }
- `TableCellProps` - `{ cell: Cell<unknown, unknown>; className?: string }`
- `TableRowProps` - `{ row: Row<unknown>; children: (props) => ReactNode; className?: string }`
- `TableBodyProps` - `{ children: (props) => ReactNode; className?: string }`

### shadcn/ui Dependencies

- `@/components/ui/button`
- `@/components/ui/dropdown-menu`
- `@/components/ui/table`
- `@/lib/utils`

### External Dependencies

- `@tanstack/react-table`, `jotai`, `lucide-react`

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 36. Tags

**Package:** `@repo/tags`
**Description:** Tags are a way to apply multiple labels to an item.
**Source:** `packages/tags/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `Tags` | `TagsProps` | Root provider with popover for tag selection |
| `TagsTrigger` | `TagsTriggerProps` | Trigger button displaying selected tags |
| `TagsValue` | `TagsValueProps` | Individual selected tag badge with remove button |
| `TagsContent` | `TagsContentProps` | Popover content with Command search |
| `TagsInput` | `TagsInputProps` | Search input within the popover |
| `TagsList` | `TagsListProps` | Scrollable list of tag options |
| `TagsEmpty` | `TagsEmptyProps` | Empty state message |
| `TagsGroup` | `TagsGroupProps` | Group container (alias for CommandGroup) |
| `TagsItem` | `TagsItemProps` | Individual tag option |

### Exported Types

- `TagsProps` - `{ value?: string; setValue?: (value: string) => void; open?: boolean; onOpenChange?: (open: boolean) => void; children?: ReactNode; className?: string }`
- `TagsTriggerProps` - ComponentProps\<typeof Button\>
- `TagsValueProps` - ComponentProps\<typeof Badge\> & { onRemove?: () => void }
- `TagsContentProps` - ComponentProps\<typeof PopoverContent\>
- `TagsInputProps` - ComponentProps\<typeof CommandInput\>
- `TagsListProps` - ComponentProps\<typeof CommandList\>
- `TagsEmptyProps` - ComponentProps\<typeof CommandEmpty\>
- `TagsGroupProps` - ComponentProps\<typeof CommandGroup\>
- `TagsItemProps` - ComponentProps\<typeof CommandItem\>

### shadcn/ui Dependencies

- `@/components/ui/badge`
- `@/components/ui/button`
- `@/components/ui/command`
- `@/components/ui/popover`
- `@/lib/utils`

### External Dependencies

- `lucide-react`

### Kibo Inter-dependencies

- None (note: package.json does not list `@repo/shadcn-ui` but imports from `@/components/ui/*`)

---

## 37. Theme Switcher

**Package:** `@repo/theme-switcher`
**Description:** A component to switch between light, dark and system theme.
**Source:** `packages/theme-switcher/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `ThemeSwitcher` | `ThemeSwitcherProps` | Animated toggle between system/light/dark themes |

### Exported Types

- `ThemeSwitcherProps` - `{ value?: "light" | "dark" | "system"; onChange?: (theme: "light" | "dark" | "system") => void; defaultValue?: "light" | "dark" | "system"; className?: string }`

### shadcn/ui Dependencies

- `@/lib/utils`

### External Dependencies

- `@radix-ui/react-use-controllable-state`, `lucide-react`, `motion` (motion/react)

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 38. Ticker

**Package:** `@repo/ticker`
**Description:** A composable finance ticker for displaying symbols, prices and changes.
**Source:** `packages/ticker/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `Ticker` | `TickerProps` | Root provider with currency formatter context |
| `TickerIcon` | `TickerIconProps` | Token/coin icon with avatar fallback |
| `TickerSymbol` | `TickerSymbolProps` | Uppercase symbol label |
| `TickerPrice` | `TickerPriceProps` | Formatted price display |
| `TickerPriceChange` | `TickerPriceChangeProps` | Price change with up/down indicator |

### Exported Types

- `TickerProps` - HTMLAttributes\<HTMLButtonElement\> & { currency?: string; locale?: string }
- `TickerIconProps` - HTMLAttributes\<HTMLImageElement\> & { src?: string; symbol?: string; asChild?: boolean }
- `TickerSymbolProps` - HTMLAttributes\<HTMLSpanElement\> & { symbol: string }
- `TickerPriceProps` - HTMLAttributes\<HTMLSpanElement\> & { price: number }
- `TickerPriceChangeProps` - HTMLAttributes\<HTMLSpanElement\> & { change: number; isPercent?: boolean }

### Exported Hooks

- `useTickerContext()` - Returns `{ formatter: Intl.NumberFormat }`

### shadcn/ui Dependencies

- `@/components/ui/avatar`
- `@/lib/utils`

### External Dependencies

- None

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 39. Tree

**Package:** `@repo/tree`
**Description:** A composable tree component with animated expand/collapse and customizable nodes.
**Source:** `packages/tree/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `TreeProvider` | `TreeProviderProps` | Root provider managing tree expand/select state |
| `TreeView` | `TreeViewProps` | Outer tree container |
| `TreeNode` | `TreeNodeProps` | Individual node with context |
| `TreeNodeTrigger` | `TreeNodeTriggerProps` | Clickable node row |
| `TreeNodeContent` | `TreeNodeContentProps` | Expandable children container |
| `TreeExpander` | `TreeExpanderProps` | Chevron expand/collapse icon |
| `TreeIcon` | `TreeIconProps` | File/folder icon |
| `TreeLabel` | `TreeLabelProps` | Node label text |
| `TreeLines` | (none) | Tree connector lines (internal, but exported) |

### Exported Types

- `TreeProviderProps` - `{ children: ReactNode; defaultExpandedIds?: string[]; showLines?: boolean; showIcons?: boolean; selectable?: boolean; multiSelect?: boolean; selectedIds?: string[]; onSelectionChange?: (selectedIds: string[]) => void; indent?: number; animateExpand?: boolean; className?: string }`
- `TreeViewProps` - HTMLAttributes\<HTMLDivElement\>
- `TreeNodeProps` - HTMLAttributes\<HTMLDivElement\> & { nodeId?: string; level?: number; isLast?: boolean; parentPath?: boolean[]; children?: ReactNode }
- `TreeNodeTriggerProps` - ComponentProps\<typeof motion.div\>
- `TreeNodeContentProps` - ComponentProps\<typeof motion.div\> & { hasChildren?: boolean }
- `TreeExpanderProps` - ComponentProps\<typeof motion.div\> & { hasChildren?: boolean }
- `TreeIconProps` - ComponentProps\<typeof motion.div\> & { icon?: ReactNode; hasChildren?: boolean }
- `TreeLabelProps` - HTMLAttributes\<HTMLSpanElement\>

### shadcn/ui Dependencies

- `@/lib/utils`

### External Dependencies

- `lucide-react`, `motion` (motion/react)

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 40. Typography

**Package:** `@repo/typography`
**Description:** A typography component designed to display text with a consistent style.
**Source:** `packages/typography/styles.css`

### Exported Components

None -- this package exports a CSS stylesheet, not React components.

### CSS Classes

- `.typography` - Base class providing styled prose elements including:
  - `h1` through `h6` - Heading styles with scroll margin, font sizes, weights, and spacing
  - `p` - Paragraph with 1.75 line-height
  - `a` - Links with primary color and underline
  - `blockquote` - Bordered and italicized
  - `table`, `th`, `td` - Table styling with borders and alternating row backgrounds
  - `ul`, `ol` - List styling with proper margins
  - `pre`, `code` - Code block and inline code styling
  - `.lead`, `.large`, `.small`, `.muted` - Utility text classes
  - `img`, `picture`, `video` - Media spacing
  - `kbd` - Keyboard shortcut styling
  - `hr` - Horizontal rule spacing
  - `dl`, `dt` - Definition list styling
  - `details`, `summary` - Collapsible section styling
  - `mark` - Highlight styling
  - `small` - Small text styling
- `.not-typography` - Opt-out class to exclude nested elements from typography styles

### External Dependencies

- None

### Kibo Inter-dependencies

- `@repo/shadcn-ui`

---

## 41. Video Player

**Package:** `@repo/video-player`
**Description:** A composable, shadcn/ui styled video player component that uses the media-chrome library.
**Source:** `packages/video-player/index.tsx`

### Exported Components

| Component | Props Type | Description |
|-----------|-----------|-------------|
| `VideoPlayer` | `VideoPlayerProps` | Root media controller with themed CSS variables |
| `VideoPlayerControlBar` | `VideoPlayerControlBarProps` | Control bar container |
| `VideoPlayerTimeRange` | `VideoPlayerTimeRangeProps` | Seek/progress bar |
| `VideoPlayerTimeDisplay` | `VideoPlayerTimeDisplayProps` | Current/total time display |
| `VideoPlayerVolumeRange` | `VideoPlayerVolumeRangeProps` | Volume slider |
| `VideoPlayerPlayButton` | `VideoPlayerPlayButtonProps` | Play/pause button |
| `VideoPlayerSeekBackwardButton` | `VideoPlayerSeekBackwardButtonProps` | Seek backward button |
| `VideoPlayerSeekForwardButton` | `VideoPlayerSeekForwardButtonProps` | Seek forward button |
| `VideoPlayerMuteButton` | `VideoPlayerMuteButtonProps` | Mute/unmute button |
| `VideoPlayerContent` | `VideoPlayerContentProps` | The video element itself |

### Exported Types

- `VideoPlayerProps` - ComponentProps\<typeof MediaController\>
- `VideoPlayerControlBarProps` - ComponentProps\<typeof MediaControlBar\>
- `VideoPlayerTimeRangeProps` - ComponentProps\<typeof MediaTimeRange\>
- `VideoPlayerTimeDisplayProps` - ComponentProps\<typeof MediaTimeDisplay\>
- `VideoPlayerVolumeRangeProps` - ComponentProps\<typeof MediaVolumeRange\>
- `VideoPlayerPlayButtonProps` - ComponentProps\<typeof MediaPlayButton\>
- `VideoPlayerSeekBackwardButtonProps` - ComponentProps\<typeof MediaSeekBackwardButton\>
- `VideoPlayerSeekForwardButtonProps` - ComponentProps\<typeof MediaSeekForwardButton\>
- `VideoPlayerMuteButtonProps` - ComponentProps\<typeof MediaMuteButton\>
- `VideoPlayerContentProps` - ComponentProps\<"video"\>

### shadcn/ui Dependencies

- `@/lib/utils`

### External Dependencies

- `media-chrome` (media-chrome/react)

### Kibo Inter-dependencies

- `@repo/shadcn-ui`
