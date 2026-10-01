---
name: Linear — dense issue lists and command palette
kind: design
source: Linear (issue tracker)
url: https://linear.app
status: proposed
applies-to:
  - dense list screens
  - keyboard-driven navigation
  - record metadata display
  - desktop web apps
---

# Linear — dense issue lists and command palette

**What it is:** a project tracker whose list views fit 30 to 40 rows on a laptop screen without feeling cramped.

## Take

- Constant row height for every row in a list (about 36 to 40 px). No row grows to fit content; long titles truncate with an ellipsis.
- Metadata (status, priority, assignee, ID, date) sits in fixed-width columns aligned across rows, so the eye scans vertically. Only the title column is flexible.
- One accent colour for the whole app, used for selection, focus and the primary action. Status and priority use small icons, not coloured text.
- Hover reveals row actions; nothing in the row is a button until hovered or focused.
- A command palette (Cmd/Ctrl+K) lists every action and every navigation target, searchable by typed text. Each list item has a single-key shortcut that also works outside the palette.
- Group headers in lists are a single line with a count; collapsed state is remembered per view.
- Sidebar is 220 to 240 px, collapsible, with no icons larger than 16 px.
- Typography: one sans-serif family, 13 px body in lists, 11 to 12 px for secondary metadata, weights 400 and 500 only.

## Leave

- Dark-first palette and purple accent: these are Linear's brand, not a pattern.
- Animation on every transition; keep transitions under 150 ms or omit.
- The assumption that every user is a keyboard power user. Business users on tablets need touch targets too (see Apple HIG entry).

## Evidence

- Public UI as generally known, no screenshot saved yet.
- Suggested: `images/design-linear-dense-lists-1.png` — issue list with grouped rows and fixed metadata columns.
