---
name: Append-only event log with derived read models
kind: code-pattern
source: Event sourcing (Greg Young); accounting practice of correcting entries
url: https://martinfowler.com/eaaDev/EventSourcing.html
status: proposed
applies-to:
  - inventory and stock movements
  - ledgers and journals
  - audit trail requirements
  - anything that must be reconstructable after the fact
---

# Append-only event log with derived read models

**What it is:** facts are written once and never changed; current state is a view computed from the log.

## Take

- One table (or one per aggregate type) of events: `id`, `aggregate_id`, `sequence`, `type`, `payload jsonb`, `occurred_at`, `recorded_at`, `actor`. Rows are inserted, never updated or deleted. Enforce with a database role that lacks `UPDATE`/`DELETE` on that table.
- Mistakes are fixed by a compensating event (`StockAdjusted`, `InvoiceVoided`, `PaymentReversed`) that references the original event id and states a reason. The original stays visible.
- Read models (current stock per SKU, account balances, open invoices) are separate tables rebuilt by replaying events. A rebuild command exists and runs in CI against the test log.
- Each event type has a versioned schema; new fields are optional, old events are never rewritten. Upcasters convert old versions on read.
- Event `type` names are past tense (`GoodsReceived`, not `ReceiveGoods`). Commands are the imperative counterpart and may be rejected; events may not.
- Idempotency: every command carries a client-generated key; the same key twice produces no second event.
- Sequence numbers per aggregate enforce optimistic concurrency (`WHERE last_sequence = $expected`).

## Leave

- Full CQRS with message buses for a small team; a transactional outbox and synchronous projection in the same database is enough until proven otherwise.
- Storing only the derived state and reconstructing events later; that is not possible.
- Soft-delete flags as a substitute; they lose the reason and the actor.

## Evidence

- Fowler's Event Sourcing article (URL above).
- Accounting rule: ledgers are never erased, errors are reversed with a correcting entry.
