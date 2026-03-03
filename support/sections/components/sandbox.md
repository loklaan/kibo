### Sandbox

> The sandbox component allows you to preview and test components in a sandboxed environment.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/sandbox.json"
```

#### Dependencies

External packages installed automatically:
- `@codesandbox/sandpack-react` — in-browser code editor, preview, console, and file explorer powered by CodeSandbox

#### Anatomy

```tsx
import {
  SandboxProvider,
  SandboxLayout,
  SandboxTabs,
  SandboxTabsList,
  SandboxTabsTrigger,
  SandboxTabsContent,
  SandboxCodeEditor,
  SandboxConsole,
  SandboxPreview,
  SandboxFileExplorer,
} from "@/components/kibo-ui/sandbox"
```

| Component | Description |
|-----------|-------------|
| `SandboxProvider` | Root provider. Wraps all child components and initializes the Sandpack context. |
| `SandboxLayout` | Layout container for arranging editor, preview, and console panels. |
| `SandboxTabs` | Tabbed interface for switching between panels. Manages the active tab via internal context. |
| `SandboxTabsList` | Container for tab trigger buttons. |
| `SandboxTabsTrigger` | A single tab button that activates its associated content panel. |
| `SandboxTabsContent` | Content panel displayed when its corresponding tab is active. |
| `SandboxCodeEditor` | Code editor panel with syntax highlighting. |
| `SandboxConsole` | Console output panel for runtime logs. |
| `SandboxPreview` | Live preview panel that renders the sandboxed code. |
| `SandboxFileExplorer` | File tree panel for navigating multiple files in the sandbox. |

#### Props

**SandboxProvider**

Accepts all `SandpackProviderProps` from `@codesandbox/sandpack-react`. Key props:

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `template` | `"react" \| "react-ts" \| "vanilla" \| "vanilla-ts" \| "vue" \| "angular" \| "svelte" \| ...` | `"react"` | Starter template for the sandbox environment. |
| `files` | `Record<string, string \| { code: string; hidden?: boolean; active?: boolean }>` | -- | Custom files to load into the sandbox. |
| `customSetup` | `{ dependencies?: Record<string, string>; devDependencies?: Record<string, string>; entry?: string }` | -- | Custom npm dependencies and entry point configuration. |
| `options` | `{ showNavigator?: boolean; showTabs?: boolean; ... }` | -- | Sandpack behavior options. |
| `theme` | `"light" \| "dark" \| "auto" \| SandpackTheme` | -- | Editor color theme. |

**SandboxLayout**

Accepts all `SandpackLayoutProps` from `@codesandbox/sandpack-react`.

**SandboxTabs**

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `defaultValue` | `string` | `undefined` | Initial active tab value (uncontrolled). |
| `value` | `string` | `undefined` | Active tab value (controlled). |
| `onValueChange` | `(value: string) => void` | -- | Called when the active tab changes. |

**SandboxTabsList**

Accepts standard `HTMLDivElement` attributes.

**SandboxTabsTrigger**

Extends `HTMLButtonElement` attributes (except `onClick`).

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `value` | `string` | -- | The tab value this trigger activates. |

**SandboxTabsContent**

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `value` | `string` | -- | The tab value this content panel corresponds to. Only visible when active. |

**SandboxCodeEditor**

Accepts all `CodeEditorProps` from `@codesandbox/sandpack-react`.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `showTabs` | `boolean` | `false` | Whether to show the built-in Sandpack file tabs above the editor. |

**SandboxConsole**

Accepts all `SandpackConsole` props from `@codesandbox/sandpack-react`.

**SandboxPreview**

Accepts all `PreviewProps` from `@codesandbox/sandpack-react`.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `showOpenInCodeSandbox` | `boolean` | `false` | Whether to show the "Open in CodeSandbox" button. |

**SandboxFileExplorer**

Accepts all `SandpackFileExplorer` props from `@codesandbox/sandpack-react`.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `autoHiddenFiles` | `boolean` | `true` | Whether to automatically hide configuration files. |

#### Usage

##### Basic

A tabbed sandbox with code editor, preview, and console panels.

```tsx
"use client"

import {
  SandboxCodeEditor,
  SandboxConsole,
  SandboxLayout,
  SandboxPreview,
  SandboxProvider,
  SandboxTabs,
  SandboxTabsContent,
  SandboxTabsList,
  SandboxTabsTrigger,
} from "@/components/kibo-ui/sandbox"

export function Example() {
  return (
    <SandboxProvider>
      <SandboxLayout>
        <SandboxTabs defaultValue="preview">
          <SandboxTabsList>
            <SandboxTabsTrigger value="code">
              Code
            </SandboxTabsTrigger>
            <SandboxTabsTrigger value="preview">
              Preview
            </SandboxTabsTrigger>
            <SandboxTabsTrigger value="console">
              Console
            </SandboxTabsTrigger>
          </SandboxTabsList>
          <SandboxTabsContent value="code">
            <SandboxCodeEditor showTabs />
          </SandboxTabsContent>
          <SandboxTabsContent value="preview">
            <SandboxPreview />
          </SandboxTabsContent>
          <SandboxTabsContent value="console">
            <SandboxConsole />
          </SandboxTabsContent>
        </SandboxTabs>
      </SandboxLayout>
    </SandboxProvider>
  )
}
```

##### With File Explorer

Add a file explorer alongside the code editor using
resizable panels.

```tsx
"use client"

import {
  SandboxCodeEditor,
  SandboxConsole,
  SandboxFileExplorer,
  SandboxLayout,
  SandboxPreview,
  SandboxProvider,
  SandboxTabs,
  SandboxTabsContent,
  SandboxTabsList,
  SandboxTabsTrigger,
} from "@/components/kibo-ui/sandbox"
import {
  ResizableHandle,
  ResizablePanel,
  ResizablePanelGroup,
} from "@/components/ui/resizable"
import {
  AppWindowIcon,
  CodeIcon,
  TerminalIcon,
} from "lucide-react"

export function Example() {
  return (
    <SandboxProvider>
      <SandboxLayout>
        <SandboxTabs defaultValue="preview">
          <SandboxTabsList>
            <SandboxTabsTrigger value="code">
              <CodeIcon size={14} />
              Code
            </SandboxTabsTrigger>
            <SandboxTabsTrigger value="preview">
              <AppWindowIcon size={14} />
              Preview
            </SandboxTabsTrigger>
            <SandboxTabsTrigger value="console">
              <TerminalIcon size={14} />
              Console
            </SandboxTabsTrigger>
          </SandboxTabsList>
          <SandboxTabsContent
            className="overflow-hidden"
            value="code"
          >
            <ResizablePanelGroup direction="horizontal">
              <ResizablePanel
                className="overflow-y-auto"
                defaultSize={25}
                maxSize={40}
                minSize={20}
              >
                <SandboxFileExplorer />
              </ResizablePanel>
              <ResizableHandle withHandle />
              <ResizablePanel className="overflow-y-auto">
                <SandboxCodeEditor />
              </ResizablePanel>
            </ResizablePanelGroup>
          </SandboxTabsContent>
          <SandboxTabsContent value="preview">
            <SandboxPreview />
          </SandboxTabsContent>
          <SandboxTabsContent value="console">
            <SandboxConsole />
          </SandboxTabsContent>
        </SandboxTabs>
      </SandboxLayout>
    </SandboxProvider>
  )
}
```

##### Custom Files and Template

Provide custom files and a TypeScript React template
to pre-populate the sandbox.

```tsx
"use client"

import {
  SandboxCodeEditor,
  SandboxLayout,
  SandboxPreview,
  SandboxProvider,
  SandboxTabs,
  SandboxTabsContent,
  SandboxTabsList,
  SandboxTabsTrigger,
} from "@/components/kibo-ui/sandbox"

const files = {
  "/App.tsx": `export default function App() {
  return (
    <div style={{ padding: 16, fontFamily: "sans-serif" }}>
      <h1>Hello from Sandbox</h1>
      <p>Edit this file to see live changes.</p>
    </div>
  )
}`,
  "/utils.ts": `export function greet(name: string) {
  return \`Hello, \${name}!\`
}`,
}

export function Example() {
  return (
    <SandboxProvider
      template="react-ts"
      files={files}
    >
      <SandboxLayout>
        <SandboxTabs defaultValue="code">
          <SandboxTabsList>
            <SandboxTabsTrigger value="code">
              Code
            </SandboxTabsTrigger>
            <SandboxTabsTrigger value="preview">
              Preview
            </SandboxTabsTrigger>
          </SandboxTabsList>
          <SandboxTabsContent value="code">
            <SandboxCodeEditor showTabs />
          </SandboxTabsContent>
          <SandboxTabsContent value="preview">
            <SandboxPreview />
          </SandboxTabsContent>
        </SandboxTabs>
      </SandboxLayout>
    </SandboxProvider>
  )
}
```

##### Controlled Tabs

Control the active tab externally with the `value` and
`onValueChange` props on `SandboxTabs`.

```tsx
"use client"

import { useState } from "react"
import {
  SandboxCodeEditor,
  SandboxConsole,
  SandboxLayout,
  SandboxPreview,
  SandboxProvider,
  SandboxTabs,
  SandboxTabsContent,
  SandboxTabsList,
  SandboxTabsTrigger,
} from "@/components/kibo-ui/sandbox"

export function Example() {
  const [tab, setTab] = useState("preview")

  return (
    <div>
      <div className="mb-2 flex gap-2">
        <button onClick={() => setTab("code")}>
          Show Code
        </button>
        <button onClick={() => setTab("preview")}>
          Show Preview
        </button>
      </div>
      <SandboxProvider>
        <SandboxLayout>
          <SandboxTabs
            value={tab}
            onValueChange={setTab}
          >
            <SandboxTabsList>
              <SandboxTabsTrigger value="code">
                Code
              </SandboxTabsTrigger>
              <SandboxTabsTrigger value="preview">
                Preview
              </SandboxTabsTrigger>
              <SandboxTabsTrigger value="console">
                Console
              </SandboxTabsTrigger>
            </SandboxTabsList>
            <SandboxTabsContent value="code">
              <SandboxCodeEditor showTabs />
            </SandboxTabsContent>
            <SandboxTabsContent value="preview">
              <SandboxPreview />
            </SandboxTabsContent>
            <SandboxTabsContent value="console">
              <SandboxConsole />
            </SandboxTabsContent>
          </SandboxTabs>
        </SandboxLayout>
      </SandboxProvider>
    </div>
  )
}
```
