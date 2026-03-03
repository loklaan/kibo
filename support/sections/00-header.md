# Kibo UI

> A custom registry of composable, accessible, open source React components designed for use with shadcn/ui.

Kibo UI extends shadcn/ui with higher-level components that cover a
wider range of use-cases. While shadcn/ui focuses on wrapping
primitives from Radix UI, Kibo UI wraps more complex logic from
various headless libraries to provide components like calendars, rich
text editors, drag-and-drop boards, and file uploaders. Components
use shadcn/ui CSS variables and integrate with existing shadcn/ui
primitives.

Kibo UI components are installed individually via the shadcn CLI and
placed directly in your project. You own the code — every component
can be read, modified, and extended. Components are written in
TypeScript, styled with Tailwind CSS, and built on top of accessible
headless libraries.

### Design Philosophy

**Composability.** Complex UIs are built by combining small, modular
pieces. Most components consist of a root component and several
sub-components composed as children, following a "building blocks"
pattern. You assemble exactly what your application needs.

**Simplicity.** Components have straightforward APIs with sensible
defaults. A single import and a few props gets you started.
Unnecessary abstractions are avoided — if a feature can be
implemented with plain React and Tailwind in a few lines, that is
preferred over complex configuration.

**Accessibility.** Every component is built to meet WCAG and ARIA
guidelines. Components leverage headless libraries like Radix UI for
robust keyboard navigation, focus management, screen-reader support,
and color contrast compliance.

### Component Index

| # | Component | Description |
|---|-----------|-------------|
| 1 | Announcement | Inform users about features, updates, or important information. |
| 2 | Avatar Stack | Stacked avatars with tooltips for displaying groups of users. |
| 3 | Banner | Dismissible banner for alerts and notifications. |
| 4 | Calendar | Date and event calendar with drag-and-drop support. |
| 5 | Choicebox | Selectable option cards for single or multiple selection. |
| 6 | Code Block | Syntax-highlighted code display with line numbers. |
| 7 | Color Picker | Color selection with hue, saturation, and alpha controls. |
| 8 | Combobox | Searchable dropdown for selecting from a list of options. |
| 9 | Comparison | Before-and-after image comparison slider. |
| 10 | Contribution Graph | GitHub-style activity heatmap visualization. |
| 11 | Credit Card | Credit card input form with formatting and validation. |
| 12 | Cursor | Animated cursor label for collaborative presence. |
| 13 | Deck | Swipeable stack of cards with gesture support. |
| 14 | Dialog Stack | Multi-step dialog with stacked navigation. |
| 15 | Dropzone | File upload area with drag-and-drop support. |
| 16 | Editor | Rich text editor with toolbar and formatting controls. |
| 17 | Gantt | Gantt chart for project timeline visualization. |
| 18 | Glimpse | Link preview tooltip on hover. |
| 19 | Image Crop | Interactive image cropping tool. |
| 20 | Image Zoom | Click-to-zoom image viewer. |
| 21 | Kanban | Drag-and-drop kanban board with columns and cards. |
| 22 | List | Sortable, drag-and-drop list. |
| 23 | Marquee | Infinitely scrolling horizontal content ticker. |
| 24 | Mini Calendar | Compact date picker calendar. |
| 25 | Pill | Small label for categorization and filtering. |
| 26 | QR Code | QR code generator with customizable styling. |
| 27 | Rating | Star rating input and display. |
| 28 | Reel | Horizontal scrolling content carousel. |
| 29 | Relative Time | Human-readable relative timestamp display. |
| 30 | Sandbox | Embedded code sandbox with live preview. |
| 31 | Snippet | Copyable code snippet with syntax highlighting. |
| 32 | Spinner | Loading indicator with multiple animation variants. |
| 33 | Status | Status indicator dot with label. |
| 34 | Stories | Instagram-style stories viewer. |
| 35 | Table | Data table with sorting, filtering, and pagination. |
| 36 | Tags | Tag input for adding and removing keyword labels. |
| 37 | Theme Switcher | Light, dark, and system theme toggle. |
| 38 | Ticker | Animated number transition display. |
| 39 | Tree | Hierarchical tree view with expand and collapse. |
| 40 | Typography | CSS stylesheet for prose content styling. |
| 41 | Video Player | Video playback controls with progress and volume. |
