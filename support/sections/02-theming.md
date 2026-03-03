## Theming

Kibo UI inherits the shadcn/ui theming system. All components reference
CSS variables defined in your global stylesheet, so changing a single
variable updates every component that uses it.

### CSS Variables

shadcn/ui projects define a set of semantic CSS variables on `:root`
and override them for dark mode under the `.dark` class. Kibo UI
components use these same variables through Tailwind utility classes
like `bg-background`, `text-foreground`, `border-border`, and
`text-muted-foreground`. The core variables are:

```css
:root {
  --background: oklch(1 0 0);
  --foreground: oklch(0.145 0 0);
  --primary: oklch(0.623 0.214 259.815);
  --primary-foreground: oklch(0.97 0.014 254.604);
  --secondary: oklch(0.97 0 0);
  --secondary-foreground: oklch(0.205 0 0);
  --muted: oklch(0.97 0 0);
  --muted-foreground: oklch(0.556 0 0);
  --accent: oklch(0.97 0 0);
  --accent-foreground: oklch(0.205 0 0);
  --destructive: oklch(0.577 0.245 27.325);
  --border: oklch(0.922 0 0);
  --input: oklch(0.922 0 0);
  --ring: oklch(0.708 0 0);
  --radius: 0.625rem;
}
```

Tailwind maps these to color utilities via the `@theme` block in your
global CSS. For example, `--color-primary: var(--primary)` lets you
write `bg-primary` or `text-primary` in any component. To change
your project's color scheme, edit the variable values in `:root` and
`.dark` — no component code changes are needed.

### Dark Mode

Dark mode is controlled by adding the `dark` class to an ancestor
element (typically `<html>`). The recommended approach uses
`next-themes` with `attribute="class"`:

```tsx
import { ThemeProvider } from "next-themes"

export function Layout({ children }: { children: React.ReactNode }) {
  return (
    <ThemeProvider
      attribute="class"
      defaultTheme="system"
      enableSystem
      disableTransitionOnChange
    >
      {children}
    </ThemeProvider>
  )
}
```

When the `dark` class is present, CSS variables defined under `.dark`
take effect and all components update automatically. Some components
also use the Tailwind `dark:` variant for mode-specific adjustments
(e.g., `dark:hover:bg-input/50` for subtle background changes).

Kibo UI includes a Theme Switcher component that provides a toggle
between light, dark, and system modes.

### Tailwind CSS Usage Patterns

Kibo UI components are styled with Tailwind CSS utility classes. The
`cn()` helper (combining `clsx` and `tailwind-merge`) is used
throughout to merge class names and resolve conflicts:

```ts
import { clsx, type ClassValue } from "clsx"
import { twMerge } from "tailwind-merge"

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs))
}
```

Components reference Tailwind utilities that map to shadcn/ui CSS
variables rather than hardcoded colors. For example, a component uses
`bg-background` instead of `bg-white`, and `text-foreground` instead
of `text-gray-900`. This ensures all components respond to theme
changes. Some components use direct color utilities (e.g.,
`bg-emerald-500`) for semantic indicators like status dots where the
color carries specific meaning independent of the theme.

### Customization

**className overrides.** Every Kibo UI component accepts a `className`
prop. Because components use `cn()` to merge class names,
`tailwind-merge` resolves conflicts so your classes take precedence:

```tsx
<Banner className="rounded-none border-2 border-red-500">
  <BannerTitle>Custom styled banner</BannerTitle>
</Banner>
```

**CSS variable overrides.** Scope variable overrides to a container to
theme a section of the page without affecting the rest:

```tsx
<div
  style={{
    "--primary": "oklch(0.6 0.25 30)",
    "--primary-foreground": "oklch(0.98 0.01 30)",
  } as React.CSSProperties}
>
  {/* Components inside inherit the override */}
  <Button>Custom themed button</Button>
</div>
```

**Editing component source.** Because Kibo UI components are installed
as source files in your project, you can modify any component's
markup, styles, or behavior directly. Components live in
`@/components/kibo-ui/<name>/` and are plain React code.
