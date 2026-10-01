---
name: Stripe Dashboard — figures first, records as amount, status, timeline
kind: design
source: Stripe Dashboard
url: https://stripe.com
status: proposed
applies-to:
  - financial record pages
  - transaction and ledger lists
  - filtering large tables
  - reporting screens
---

# Stripe Dashboard — figures first, records as amount, status, timeline

**What it is:** the admin console for a payments company, where every screen is built around amounts.

## Take

- The figure is the primary object. On an overview, the big number comes first, then its period and comparison, then the chart. Labels are secondary in size and weight.
- All numeric columns use tabular (monospaced-digit) numerals, right-aligned, with the currency symbol or code in a consistent position. Decimal places are fixed per currency, never trimmed.
- Filters are removable chips above the table, each showing field and value (for example "Status: Succeeded"). Clearing one chip reruns the query; a "Clear all" link appears when two or more are active.
- A record page (payment, invoice, customer) leads with: amount, status badge, and primary identifier on one line; then a key-value block of 6 to 10 fields; then a chronological event timeline (created, updated, paid, refunded) with timestamps.
- Status badges are a fixed, small set (succeeded, pending, failed, refunded, disputed) with one colour each, used identically everywhere.
- Tables show 10 to 100 rows with explicit pagination, not infinite scroll, so a row can be bookmarked and shared.
- Export is a first-class action on every table, producing the same columns as shown.

## Leave

- Stripe's specific colour palette and gradient branding.
- Marketing-grade illustrations on empty states; business systems need a plain line and a primary action.
- Multi-level product navigation (Stripe has dozens of products); a single-product app needs one level.

## Evidence

- Public UI as generally known, no screenshot saved yet.
- Suggested: `images/design-stripe-dashboard-figures-1.png` — payment detail page showing amount, status, then timeline.
