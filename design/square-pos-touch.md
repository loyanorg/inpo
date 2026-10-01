---
name: Square Point of Sale — touch-first tile grid and tender flow
kind: design
source: Square Point of Sale
url: https://squareup.com
status: proposed
applies-to:
  - point of sale
  - tablet-first screens
  - touch input
  - cash and payment entry
  - counter and warehouse workflows
---

# Square Point of Sale — touch-first tile grid and tender flow

**What it is:** an iPad-first checkout app used at retail counters, built for speed under time pressure.

## Take

- Primary layout is iPad landscape: left two-thirds is a tile grid of items, right third is the running ticket. The ticket is always visible; nothing covers it.
- Item tiles are square or near-square, at least 88 x 88 pt, with a name and optionally a price; colour or image is per item, text stays readable on all of them.
- Tapping a tile adds one unit immediately with a brief highlight. Quantity is adjusted by tapping the ticket line, not by a stepper on the tile.
- The ticket shows line items, a subtotal, taxes or discounts as separate lines, and a total that is the largest text on screen.
- One full-width "Charge <total>" button at the bottom of the ticket. The amount is inside the button label.
- Tender screen offers: exact-amount button, three or four quick-cash buttons (next round amounts above the total), and a numeric keypad for a custom amount. Change due is computed and shown in the same large size as the total.
- After payment, a single receipt step (print, email, SMS, none), then automatic return to an empty ticket.
- Search and categories are tabs above the grid; the grid never scrolls horizontally.

## Leave

- Consumer-facing branding on the customer screen.
- Square-specific hardware prompts (reader pairing) unless the project has that hardware.
- Portrait phone layout as primary; it is a fallback here.

## Evidence

- Public UI as generally known, no screenshot saved yet.
- Suggested: `images/design-square-pos-touch-1.png` — landscape checkout with grid and ticket; `-2.png` — tender screen with quick-cash buttons.
