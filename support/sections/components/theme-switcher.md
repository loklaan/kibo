### Theme Switcher

> A component to switch between light, dark and system theme.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/theme-switcher.json"
```

#### Dependencies

External packages installed automatically:
- `@radix-ui/react-use-controllable-state` — controllable state primitives for controlled/uncontrolled usage
- `motion` — spring-based layout animation for the active indicator
- `lucide-react` — provides the Monitor, Sun, and Moon icons

#### Anatomy

```tsx
import { ThemeSwitcher } from "@/components/kibo-ui/theme-switcher"
```

| Component | Description |
|-----------|-------------|
| `ThemeSwitcher` | Pill-shaped toggle with three icon buttons for system, light, and dark themes. Animates an active indicator between selections. |

#### Props

**ThemeSwitcher**

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `value` | `"light" \| "dark" \| "system"` | `undefined` | The controlled theme value. |
| `defaultValue` | `"light" \| "dark" \| "system"` | `"system"` | The initial theme when uncontrolled. |
| `onChange` | `(theme: "light" \| "dark" \| "system") => void` | — | Called when the user selects a theme. |
| `className` | `string` | `undefined` | Additional classes applied to the root container. |

#### Usage

##### Basic

Renders in uncontrolled mode with the system theme selected
by default.

```tsx
"use client"

import { ThemeSwitcher } from "@/components/kibo-ui/theme-switcher"

export function Example() {
  return <ThemeSwitcher />
}
```

##### Uncontrolled with Callback

Listen to theme changes without managing state. The component
tracks its own selection internally.

```tsx
"use client"

import { ThemeSwitcher } from "@/components/kibo-ui/theme-switcher"

export function Example() {
  return (
    <ThemeSwitcher
      defaultValue="system"
      onChange={(theme) => console.log("Selected:", theme)}
    />
  )
}
```

##### Controlled

Manage the selected theme externally with React state for
full control over the value.

```tsx
"use client"

import { ThemeSwitcher } from "@/components/kibo-ui/theme-switcher"
import { useState } from "react"

export function Example() {
  const [theme, setTheme] = useState<
    "light" | "dark" | "system"
  >("system")

  return (
    <div>
      <ThemeSwitcher value={theme} onChange={setTheme} />
      <p>Current theme: {theme}</p>
    </div>
  )
}
```

##### With next-themes Integration

Use with `next-themes` to persist the selected theme across
page navigations and apply it to the document.

```tsx
"use client"

import { ThemeSwitcher } from "@/components/kibo-ui/theme-switcher"
import { useTheme } from "next-themes"

export function Example() {
  const { theme, setTheme } = useTheme()

  return (
    <ThemeSwitcher
      value={theme as "light" | "dark" | "system"}
      onChange={setTheme}
    />
  )
}
```
