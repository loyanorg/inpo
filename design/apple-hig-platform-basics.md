---
name: Apple Human Interface Guidelines — touch targets, dynamic type, platform conventions
kind: design
source: Apple Human Interface Guidelines
url: https://developer.apple.com/design/human-interface-guidelines/
status: proposed
applies-to:
  - touch input
  - tablet-first screens
  - accessibility
  - form and control sizing
  - any screen used on iPad or iPhone
---

# Apple Human Interface Guidelines — touch targets, dynamic type, platform conventions

**What it is:** Apple's published rules for apps on its platforms; most of them hold for web apps used on iPad too.

## Take

- Minimum tappable area is 44 x 44 pt for every control, including icon buttons, table row actions and chips. Visual size may be smaller; the hit area may not.
- At least 8 pt between adjacent tappable controls so a thumb does not hit both.
- Body text scales with the user's text size setting (Dynamic Type). On the web: use rem units for font size and let containers grow; never clip text at larger sizes.
- Standard controls where they exist (segmented control for 2 to 5 mutually exclusive options, switch for on/off, sheet for a short task, alert only for destructive or blocking decisions).
- Destructive actions are red, placed away from the primary action, and confirmed once.
- Navigation back is always available in the top-left of the content area; modal tasks have an explicit Cancel.
- Safe areas and keyboard: content and primary buttons stay visible when the on-screen keyboard is up; forms scroll the focused field into view.
- Contrast ratio at least 4.5:1 for text, 3:1 for large text and icons.

## Leave

- iOS visual styling (translucent bars, SF Symbols) on a web app that is also used on Windows desktops; keep conventions, not the skin.
- Phone-first assumptions where the project's primary device is an iPad or desktop.

## Evidence

- Public guidelines as generally known, no screenshot saved yet.
- Guideline text is public at the URL above; quote by section name when citing.
