---
name: Money as integer minor units with exact arithmetic
kind: code-pattern
source: Martin Fowler, "Patterns of Enterprise Application Architecture" (Money pattern); ISO 4217
url: https://martinfowler.com/eaaCatalog/money.html
status: proposed
applies-to:
  - money handling
  - pricing, tax, and discount calculation
  - ledgers and invoices
  - database schema for amounts
---

# Money as integer minor units with exact arithmetic

**What it is:** amounts are stored and computed as integers in the currency's smallest unit; floats never touch money.

## Take

- Store every amount as an integer count of minor units (cents, fils, piastres) plus a currency code. In PostgreSQL: `bigint` plus `char(3)`, or `numeric(19,4)` when fractional minor units are required by tax law. Never `float`/`double`/`real`.
- In TypeScript, represent amounts as `bigint` or as a branded integer `number` guarded below `Number.MAX_SAFE_INTEGER`; one `Money` type, constructed only through a factory that validates currency and integrality.
- Intermediate results of percentages and divisions use exact rational arithmetic (numerator/denominator as integers, or a decimal library with fixed scale). Round once, at the end, with a named rounding rule (`half-up`, `half-even`, `banker`) stored with the configuration.
- Allocation (splitting a total across lines) uses the largest-remainder method so the parts sum exactly to the total. Assert the sum in tests.
- Arithmetic between different currencies is a type error. Conversion is an explicit function taking a rate with a timestamp.
- Formatting is a separate, pure function from storage: `format(money, locale)` produces the display string; parsing user input goes through one `parseMoney(text, currency)` that rejects ambiguous input.
- Every function that takes an amount takes `Money`, not `number`.

## Leave

- Storing amounts as formatted strings or as decimal `number`s in JSON; serialise as `{ amount: "12345", currency: "USD" }` (string integer) to survive JSON parsers.
- Rounding at every step; it accumulates error that does not reconcile.

## Evidence

- Fowler's Money pattern (URL above). ISO 4217 lists minor unit exponents per currency.
- Known failure: `0.1 + 0.2 !== 0.3` in IEEE 754 doubles.
