---
name: Stripe API documentation — one concept per page, runnable examples, errors with fixes
kind: writing
source: Stripe API Reference
url: https://docs.stripe.com
status: proposed
applies-to:
  - API reference docs
  - developer-facing READMEs
  - error catalogues
  - internal engine documentation
---

# Stripe API documentation — one concept per page, runnable examples, errors with fixes

**What it is:** reference docs that developers can read top to bottom or jump into, with a working request on every page.

## Take

- One resource or concept per page. The page opens with a one-sentence definition, then the object's fields, then each operation.
- Every field entry has: name in code font, type, required or optional, one-line meaning, and constraints (max length, allowed values, default).
- Every operation shows a complete, copy-pasteable request and the full response body. Examples use realistic values (`amount: 2000`, `currency: "usd"`), never `foo`/`bar`.
- Errors are a catalogue: each error code has a one-line cause and a one-line fix ("Use a card that has not expired"). Codes in docs match codes in responses exactly.
- Two-column layout: prose and field tables on the left, code on the right, scrolling together. On narrow screens code follows prose.
- Changelog is dated and per version; breaking changes are labelled and paired with a migration note.
- Terms are used consistently: one word per concept across all pages (a "charge" is never also a "transaction").

## Leave

- Multi-language code tabs when the project has one client language; show that one.
- Marketing introductions on reference pages; start with the definition.

## Evidence

- Public docs as generally known, no screenshot saved yet.
- Suggested: `images/writing-stripe-api-docs-1.png` — an endpoint page showing field table beside request and response.
