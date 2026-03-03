### Credit Card

> Credit card components for displaying and validating credit card information.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/credit-card.json"
```

#### Dependencies

External packages installed automatically:
- `react-svg-credit-card-payment-icons` — SVG payment network logos (Visa, Mastercard, Amex, etc.)

#### Anatomy

```tsx
import {
  CreditCard,
  CreditCardFlipper,
  CreditCardFront,
  CreditCardBack,
  CreditCardChip,
  CreditCardLogo,
  CreditCardName,
  CreditCardNumber,
  CreditCardExpiry,
  CreditCardCvv,
  CreditCardServiceProvider,
  CreditCardMagStripe,
} from "@/components/kibo-ui/credit-card"
```

| Component | Description |
|-----------|-------------|
| `CreditCard` | Root container. Sets the card aspect ratio and perspective for 3D flip. |
| `CreditCardFlipper` | Wraps front and back faces. Flips on hover (desktop) or tap (touch). |
| `CreditCardFront` | Front face of the card. Positioned absolutely within the flipper. |
| `CreditCardBack` | Back face of the card. Automatically rotated 180 degrees when inside a flipper. |
| `CreditCardChip` | Renders a default chip SVG, or accepts children for a custom chip graphic. |
| `CreditCardLogo` | Positioned container for a card issuer logo (top-right by default). |
| `CreditCardName` | Displays the cardholder name in uppercase. |
| `CreditCardNumber` | Displays the card number in monospace font. |
| `CreditCardExpiry` | Displays the expiration date in monospace font. |
| `CreditCardCvv` | Displays the CVV code in monospace font. |
| `CreditCardServiceProvider` | Renders a payment network icon via `react-svg-credit-card-payment-icons`, or accepts children for a custom logo. |
| `CreditCardMagStripe` | Renders the magnetic stripe bar on the card back. |

#### Props

**CreditCard**

Accepts standard `HTMLDivElement` attributes.

**CreditCardFlipper**

Accepts standard `HTMLDivElement` attributes.

**CreditCardFront**

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `safeArea` | `number` | `20` | Inner margin in pixels applied to the card face content area. |

**CreditCardBack**

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `safeArea` | `number` | `16` | Inner margin in pixels applied to the card face content area. |

**CreditCardChip**

Accepts standard `SVGSVGElement` attributes when rendering the default chip. When children are provided, renders them inside a positioned `div` instead.

**CreditCardLogo**

Accepts standard `HTMLDivElement` attributes.

**CreditCardName**

Accepts standard `HTMLParagraphElement` attributes.

**CreditCardNumber**

Accepts standard `HTMLParagraphElement` attributes.

**CreditCardExpiry**

Accepts standard `HTMLParagraphElement` attributes.

**CreditCardCvv**

Accepts standard `HTMLParagraphElement` attributes.

**CreditCardServiceProvider**

Extends `PaymentIcon` props from `react-svg-credit-card-payment-icons`. When children are provided, renders them inside a positioned `div` instead.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `type` | `string` | `"Visa"` | Payment network icon to display (e.g., `"Visa"`, `"Mastercard"`, `"Amex"`). |
| `format` | `string` | `undefined` | Icon format variant (e.g., `"logo"` for logo-only display). |

**CreditCardMagStripe**

Accepts standard `HTMLDivElement` attributes.

#### Usage

##### Basic

```tsx
"use client"

import {
  CreditCard,
  CreditCardFlipper,
  CreditCardFront,
  CreditCardBack,
  CreditCardChip,
  CreditCardName,
  CreditCardNumber,
  CreditCardExpiry,
  CreditCardCvv,
  CreditCardServiceProvider,
  CreditCardMagStripe,
} from "@/components/kibo-ui/credit-card"

export function Example() {
  return (
    <CreditCard>
      <CreditCardFlipper>
        <CreditCardFront className="bg-slate-800">
          <CreditCardChip />
          <CreditCardServiceProvider type="Visa" />
          <CreditCardName className="absolute bottom-0 left-0">
            Jane Smith
          </CreditCardName>
        </CreditCardFront>
        <CreditCardBack className="bg-slate-800">
          <CreditCardMagStripe />
          <CreditCardNumber
            className="absolute bottom-0 left-0"
          >
            4111 2222 3333 4444
          </CreditCardNumber>
          <div
            className="-translate-y-1/2 absolute top-1/2 flex gap-4"
          >
            <CreditCardExpiry>09/27</CreditCardExpiry>
            <CreditCardCvv>321</CreditCardCvv>
          </div>
        </CreditCardBack>
      </CreditCardFlipper>
    </CreditCard>
  )
}
```

##### With Issuer Logo

Adds a custom issuer logo to the front face using `CreditCardLogo`.

```tsx
"use client"

import {
  CreditCard,
  CreditCardFlipper,
  CreditCardFront,
  CreditCardBack,
  CreditCardChip,
  CreditCardLogo,
  CreditCardName,
  CreditCardNumber,
  CreditCardExpiry,
  CreditCardCvv,
  CreditCardServiceProvider,
  CreditCardMagStripe,
} from "@/components/kibo-ui/credit-card"

export function Example() {
  return (
    <CreditCard>
      <CreditCardFlipper>
        <CreditCardFront className="bg-[#063573]">
          <CreditCardLogo>
            <span className="text-lg font-bold">BANK</span>
          </CreditCardLogo>
          <CreditCardChip />
          <CreditCardServiceProvider
            className="brightness-0 invert"
            format="logo"
            type="Visa"
          />
          <CreditCardName
            className="absolute bottom-0 left-0"
          >
            John R. Doe
          </CreditCardName>
        </CreditCardFront>
        <CreditCardBack className="bg-[#063573]">
          <CreditCardMagStripe />
          <CreditCardNumber
            className="absolute bottom-0 left-0"
          >
            0123 4567 8901 2345
          </CreditCardNumber>
          <div
            className="-translate-y-1/2 absolute top-1/2 flex gap-4"
          >
            <CreditCardExpiry>01/24</CreditCardExpiry>
            <CreditCardCvv>123</CreditCardCvv>
          </div>
        </CreditCardBack>
      </CreditCardFlipper>
    </CreditCard>
  )
}
```

##### Back Only

Displays only the back face of the card without a flipper.

```tsx
"use client"

import {
  CreditCard,
  CreditCardBack,
  CreditCardCvv,
  CreditCardExpiry,
  CreditCardMagStripe,
  CreditCardName,
  CreditCardNumber,
} from "@/components/kibo-ui/credit-card"

export function Example() {
  return (
    <CreditCard>
      <CreditCardBack className="bg-[#9EE672] text-black">
        <CreditCardMagStripe />
        <CreditCardNumber
          className="absolute bottom-0 left-0"
        >
          0123 4567 8901 2345
        </CreditCardNumber>
        <div
          className="absolute bottom-8 flex w-full flex-col gap-4"
        >
          <CreditCardName>John R. Doe</CreditCardName>
          <div className="flex gap-4">
            <CreditCardExpiry>01/24</CreditCardExpiry>
            <CreditCardCvv>123</CreditCardCvv>
          </div>
        </div>
      </CreditCardBack>
    </CreditCard>
  )
}
```

##### Custom Chip and Service Provider

Uses children to replace the default chip SVG and service provider icon with custom graphics.

```tsx
"use client"

import {
  CreditCard,
  CreditCardFlipper,
  CreditCardFront,
  CreditCardBack,
  CreditCardChip,
  CreditCardLogo,
  CreditCardName,
  CreditCardServiceProvider,
  CreditCardMagStripe,
} from "@/components/kibo-ui/credit-card"

export function Example() {
  return (
    <CreditCard>
      <CreditCardFlipper>
        <CreditCardFront
          className="bg-[#F2F2F2] text-[#909090]"
          safeArea={24}
        >
          <CreditCardLogo
            className="absolute top-0 right-auto left-0 size-1/8"
          >
            <svg viewBox="0 0 24 24" fill="currentColor">
              <title>Logo</title>
              <circle cx="12" cy="12" r="10" />
            </svg>
          </CreditCardLogo>
          <CreditCardChip
            className="right-1 left-auto w-1/5"
          >
            <svg viewBox="0 0 132 92">
              <title>Chip</title>
              <rect
                fill="#EAEAEA"
                height="91"
                rx="20.5"
                stroke="#CECCC8"
                width="131"
                x="0.5"
                y="0.5"
              />
            </svg>
          </CreditCardChip>
          <CreditCardName
            className="-translate-y-1/2 absolute top-1/2 mt-4"
          >
            Jane Smith
          </CreditCardName>
        </CreditCardFront>
        <CreditCardBack
          className="bg-[#F2F2F2] text-[#909090]"
          safeArea={0}
        >
          <CreditCardServiceProvider
            className="top-6 right-6 max-h-1/4 max-w-1/4"
            type="Mastercard"
          >
            <svg viewBox="0 0 48 32" fill="none">
              <title>Mastercard</title>
              <circle cx="18" cy="16" r="12" fill="#999" />
              <circle cx="30" cy="16" r="12" fill="#BBB" />
            </svg>
          </CreditCardServiceProvider>
          <CreditCardMagStripe
            className="top-auto bottom-0 bg-[#BEBEC0]"
          />
        </CreditCardBack>
      </CreditCardFlipper>
    </CreditCard>
  )
}
```
