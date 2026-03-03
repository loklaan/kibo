### Deck

> A Tinder-like swipeable card stack component with smooth animations.

#### Installation

```bash
npx shadcn@latest add "https://www.kibo-ui.com/r/deck.json"
```

#### Dependencies

External packages installed automatically:
- `motion` — provides drag gestures, spring animations, and motion values
- `@radix-ui/react-use-controllable-state` — controlled/uncontrolled state management

#### Anatomy

```tsx
import {
  Deck,
  DeckCards,
  DeckItem,
  DeckEmpty,
} from "@/components/kibo-ui/deck"
```

| Component | Description |
|-----------|-------------|
| `Deck` | Root container. Wraps the card stack and empty state. |
| `DeckCards` | Manages the swipeable card stack, animations, and index tracking. |
| `DeckItem` | A single card rendered inside the stack. |
| `DeckEmpty` | Placeholder shown when all cards have been swiped away. |

#### Props

**Deck**

Accepts standard `HTMLDivElement` attributes.

**DeckCards**

Extends `HTMLDivElement` attributes.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `onSwipe` | `(index: number, direction: "left" \| "right") => void` | — | Called when a card is swiped. |
| `onSwipeEnd` | `(index: number, direction: "left" \| "right") => void` | — | Called after the swipe completes. |
| `threshold` | `number` | `150` | Drag distance in pixels required to trigger a swipe. |
| `stackSize` | `number` | `3` | Number of cards visible in the stack at once. |
| `perspective` | `number` | `1000` | CSS perspective value for the 3D stack effect. |
| `scale` | `number` | `0.05` | Scale reduction per card in the stack. |
| `currentIndex` | `number` | — | Controlled index of the active card. |
| `defaultCurrentIndex` | `number` | `0` | Initial index for uncontrolled mode. |
| `onCurrentIndexChange` | `(index: number) => void` | — | Called when the active index changes. |
| `animateOnIndexChange` | `boolean` | `true` | Animate the card exit when the index changes externally. |
| `indexChangeDirection` | `"left" \| "right"` | `"left"` | Direction of the exit animation when the index changes externally. |

**DeckItem**

Accepts standard `HTMLDivElement` attributes.

**DeckEmpty**

Accepts standard `HTMLDivElement` attributes. Renders a default "No more cards" message when no children are provided.

#### Usage

##### Basic

```tsx
"use client"

import {
  Deck,
  DeckCards,
  DeckItem,
  DeckEmpty,
} from "@/components/kibo-ui/deck"

export function Example() {
  return (
    <Deck className="h-80 w-60">
      <DeckCards>
        <DeckItem className="bg-red-500 text-white">
          Card 1
        </DeckItem>
        <DeckItem className="bg-blue-500 text-white">
          Card 2
        </DeckItem>
        <DeckItem className="bg-green-500 text-white">
          Card 3
        </DeckItem>
      </DeckCards>
      <DeckEmpty />
    </Deck>
  )
}
```

##### Swipe Callbacks

Respond to swipe events to track which card was swiped and in which direction.

```tsx
"use client"

import {
  Deck,
  DeckCards,
  DeckItem,
  DeckEmpty,
} from "@/components/kibo-ui/deck"

const cards = [
  { id: 1, label: "Wireless Headphones", price: "$199" },
  { id: 2, label: "Smart Watch", price: "$299" },
  { id: 3, label: "Coffee Maker", price: "$149" },
]

export function Example() {
  return (
    <Deck className="h-96 w-72">
      <DeckCards
        onSwipe={(index, direction) => {
          console.log(`Swiped card ${index} ${direction}`)
        }}
      >
        {cards.map((card) => (
          <DeckItem className="flex-col" key={card.id}>
            <p className="font-semibold text-lg">{card.label}</p>
            <p className="text-muted-foreground">
              {card.price}
            </p>
          </DeckItem>
        ))}
      </DeckCards>
      <DeckEmpty>No more products</DeckEmpty>
    </Deck>
  )
}
```

##### Controlled Index

Control the active card index externally with buttons, animating the exit direction.

```tsx
"use client"

import { useState } from "react"
import {
  Deck,
  DeckCards,
  DeckItem,
  DeckEmpty,
} from "@/components/kibo-ui/deck"

const cards = [
  { id: 1, title: "Card 1", color: "bg-red-500" },
  { id: 2, title: "Card 2", color: "bg-blue-500" },
  { id: 3, title: "Card 3", color: "bg-green-500" },
]

export function Example() {
  const [currentIndex, setCurrentIndex] = useState(0)
  const [direction, setDirection] = useState<
    "left" | "right"
  >("left")

  const advance = (dir: "left" | "right") => {
    if (currentIndex >= cards.length) return
    setDirection(dir)
    setTimeout(() => {
      setCurrentIndex((prev) => prev + 1)
    }, 0)
  }

  return (
    <div className="space-y-4">
      <div className="flex justify-center gap-2">
        <button onClick={() => advance("left")}>
          Reject
        </button>
        <button onClick={() => advance("right")}>
          Accept
        </button>
      </div>
      <Deck className="h-60 w-48">
        <DeckCards
          animateOnIndexChange
          currentIndex={currentIndex}
          indexChangeDirection={direction}
          onCurrentIndexChange={setCurrentIndex}
        >
          {cards.map((card) => (
            <DeckItem
              className={`${card.color} text-white`}
              key={card.id}
            >
              {card.title}
            </DeckItem>
          ))}
        </DeckCards>
        <DeckEmpty />
      </Deck>
    </div>
  )
}
```

##### Custom Stack Appearance

Adjust the stack size, perspective, and scale to change the visual depth effect.

```tsx
"use client"

import {
  Deck,
  DeckCards,
  DeckItem,
  DeckEmpty,
} from "@/components/kibo-ui/deck"

export function Example() {
  return (
    <Deck className="h-80 w-64">
      <DeckCards
        stackSize={5}
        perspective={600}
        scale={0.08}
        threshold={100}
      >
        <DeckItem>First</DeckItem>
        <DeckItem>Second</DeckItem>
        <DeckItem>Third</DeckItem>
        <DeckItem>Fourth</DeckItem>
        <DeckItem>Fifth</DeckItem>
      </DeckCards>
      <DeckEmpty />
    </Deck>
  )
}
```
