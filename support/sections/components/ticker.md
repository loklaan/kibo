### Ticker

> A composable finance ticker for displaying symbols, prices and changes.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/ticker.json"
```

#### Anatomy

```tsx
import {
  Ticker,
  TickerIcon,
  TickerSymbol,
  TickerPrice,
  TickerPriceChange,
} from "@/components/kibo-ui/ticker"
```

| Component | Description |
|-----------|-------------|
| `Ticker` | Root container. Provides currency formatter context and renders as a button. |
| `TickerIcon` | Token or coin icon with avatar fallback. Supports `asChild` for custom images. |
| `TickerSymbol` | Uppercase symbol label. |
| `TickerPrice` | Formatted price display using the formatter from context. |
| `TickerPriceChange` | Price change with color-coded up/down arrow indicator. |

| Hook | Description |
|------|-------------|
| `useTickerContext` | Returns the current `Intl.NumberFormat` formatter from the nearest `Ticker` provider. |

#### Props

**Ticker**

Extends `HTMLButtonElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `currency` | `string` | `"USD"` | ISO 4217 currency code for formatting prices. |
| `locale` | `string` | `"en-US"` | BCP 47 locale tag for number formatting. |

**TickerIcon**

Extends `HTMLImageElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `src` | `string` | `undefined` | Image source URL for the icon. |
| `symbol` | `string` | `undefined` | Fallback text displayed when the image is unavailable. Uses the first two characters. |
| `asChild` | `boolean` | `undefined` | When true, renders children inside a rounded container instead of an avatar. |

**TickerSymbol**

Extends `HTMLSpanElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `symbol` | `string` | — | The ticker symbol to display. Rendered in uppercase. |

**TickerPrice**

Extends `HTMLSpanElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `price` | `number` | — | The price value. Formatted using the currency formatter from context. |

**TickerPriceChange**

Extends `HTMLSpanElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `change` | `number` | — | The change value. Positive values render green with an up arrow; negative values render red with a down arrow. |
| `isPercent` | `boolean` | `undefined` | When true, formats the change as a percentage instead of a currency value. |

#### Usage

##### Basic

```tsx
import {
  Ticker,
  TickerIcon,
  TickerSymbol,
  TickerPrice,
  TickerPriceChange,
} from "@/components/kibo-ui/ticker"

export function Example() {
  return (
    <Ticker>
      <TickerIcon src="/google.png" symbol="GOOG" />
      <TickerSymbol symbol="GOOG" />
      <TickerPrice price={175.41} />
      <TickerPriceChange change={2.13} />
    </Ticker>
  )
}
```

##### Percentage Change

Display the price change as a percentage instead of a currency value.

```tsx
import {
  Ticker,
  TickerIcon,
  TickerSymbol,
  TickerPrice,
  TickerPriceChange,
} from "@/components/kibo-ui/ticker"

export function Example() {
  return (
    <div className="flex flex-col gap-2">
      <Ticker>
        <TickerIcon src="/tesla.png" symbol="TSLA" />
        <TickerSymbol symbol="TSLA" />
        <TickerPrice price={182.12} />
        <TickerPriceChange change={-3.12} isPercent />
      </Ticker>

      <Ticker>
        <TickerIcon src="/microsoft.png" symbol="MSFT" />
        <TickerSymbol symbol="MSFT" />
        <TickerPrice price={409.33} />
        <TickerPriceChange change={2.18} isPercent />
      </Ticker>
    </div>
  )
}
```

##### Currencies and Locales

Set the `currency` and `locale` props on the root `Ticker` to format prices for different regions.

```tsx
import {
  Ticker,
  TickerIcon,
  TickerSymbol,
  TickerPrice,
  TickerPriceChange,
} from "@/components/kibo-ui/ticker"

export function Example() {
  return (
    <div className="flex flex-col gap-2">
      <Ticker currency="EUR" locale="de-DE">
        <TickerIcon src="/diebold.png" symbol="DBD" />
        <TickerSymbol symbol="DBD" />
        <TickerPrice price={102.33} />
        <TickerPriceChange change={1.05} />
      </Ticker>

      <Ticker currency="JPY" locale="ja-JP">
        <TickerIcon src="/toyota.png" symbol="7203.T" />
        <TickerSymbol symbol="7203.T" />
        <TickerPrice price={2460} />
        <TickerPriceChange change={-120} />
      </Ticker>
    </div>
  )
}
```

##### Inline Usage

Embed a ticker inline within a paragraph of text.

```tsx
import {
  Ticker,
  TickerIcon,
  TickerSymbol,
  TickerPrice,
  TickerPriceChange,
} from "@/components/kibo-ui/ticker"

export function Example() {
  return (
    <p>
      Shares of{" "}
      <Ticker
        className="rounded-full bg-muted p-1 pr-2 text-xs"
      >
        <TickerIcon src="/google.png" symbol="GOOG" />
        <TickerSymbol symbol="GOOG" />
        <TickerPrice price={175.41} />
        <TickerPriceChange change={2.13} />
      </Ticker>{" "}
      rose in early trading on Thursday.
    </p>
  )
}
```

##### Custom Icon with asChild

Use the `asChild` prop on `TickerIcon` to render a custom image element.

```tsx
import {
  Ticker,
  TickerIcon,
  TickerSymbol,
  TickerPrice,
  TickerPriceChange,
} from "@/components/kibo-ui/ticker"

export function Example() {
  return (
    <Ticker>
      <TickerIcon asChild>
        <img
          alt="AAPL"
          height={26}
          src="/apple.png"
          width={26}
        />
      </TickerIcon>
      <TickerSymbol symbol="AAPL" />
      <TickerPrice price={198.50} />
      <TickerPriceChange change={-1.24} />
    </Ticker>
  )
}
```
