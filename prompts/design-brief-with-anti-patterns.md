---
name: Design brief template with explicit anti-patterns
kind: prompt
source: Practice in this org; design-brief structure common in product teams
url: https://github.com/loyanorg/inpo
status: proposed
applies-to:
  - briefing an agent to build a screen
  - design notes
  - new screen or feature requests
  - tablet and desktop UI work
---

# Design brief template with explicit anti-patterns

**What it is:** a one-page brief given to an agent before it builds a screen, with a "do not" list as long as the goals.

## Take

- Sections, in order: Who uses it (role, device, frequency); Job (one sentence, the outcome); Data on screen (fields, with source and format); Primary action (one); Secondary actions (up to three); States (empty, loading, error, partial permissions); Anti-patterns; References; Done when.
- Anti-patterns is a bulleted list of concrete things not to do, each with a reason, at least as many bullets as the goals. Seed every brief with the org's Rejected list (explanatory copy, demo-data assumptions, generic first-pass layouts) and add screen-specific ones.
- References names entries from this library by file name and says which Take bullets apply ("design/stripe-dashboard-figures: tabular numerals, filter chips").
- Devices are listed with exact viewport widths to design for (for example 1024 x 768 iPad landscape, 1440 desktop) and which is primary.
- "Done when" is a checklist the agent can run: screenshots at each viewport, states covered, no copy that restates a label, figures use tabular numerals, touch targets 44 pt.
- The brief states fidelity expectation: production-ready, not wireframe.
- Under 60 lines; anything longer is split into two screens.

## Leave

- Mood words ("clean", "modern", "intuitive") as requirements; they cannot be checked.
- Pixel-perfect mockups attached to the brief when the project has a design system; reference the system components instead.

## Evidence

- Internal practice; this repository's Rejected list records the three seed anti-patterns (1 Oct 2026).
- No screenshot applicable.
