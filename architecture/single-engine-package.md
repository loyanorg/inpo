---
name: Single engine package — all business rules in one place, thin API and UI on top
kind: architecture
source: Hexagonal / ports-and-adapters (Alistair Cockburn); "functional core, imperative shell" (Gary Bernhardt)
url: https://alistair.cockburn.us/hexagonal-architecture/
status: proposed
applies-to:
  - monorepo layout
  - deciding where a rule lives
  - business systems with web, API and import paths
  - testing strategy
---

# Single engine package — all business rules in one place, thin API and UI on top

**What it is:** one package (`packages/engine`) owns every rule; HTTP, CLI, importers and the React app only call it.

## Take

- `packages/engine` exports commands (`receiveGoods`, `issueInvoice`, `recordPayment`) and queries. It depends on nothing framework-specific: no HTTP, no React, no ORM types in its public API.
- The engine defines the ports it needs (`StockRepository`, `Clock`, `IdGenerator`) as interfaces; adapters in other packages implement them for PostgreSQL, PGlite, and in-memory tests.
- The API package is a mapping layer: parse request, call one engine command, map the Result to a status and body. No `if` on business data in a handler.
- The UI never computes a business figure. Totals, taxes, allowed actions and validation messages come from the engine (directly in-process, or over the API).
- Every rule has a test in the engine package that runs without a server or browser, in under a second.
- A rule changed in the engine is automatically reflected in every entry point; if a fix requires touching the API and UI too, the rule leaked and should be moved back.
- Dependency rule, enforced by lint (`eslint-plugin-boundaries` or `dependency-cruiser`): api → engine, ui → engine or api, engine → nothing above it.

## Leave

- Microservices per domain for a small org; one engine package in one repo is simpler and still cleanly layered.
- Anaemic entities plus a "service" per table; group by use case, not by table.

## Evidence

- Cockburn's hexagonal architecture (URL above).
- Bernhardt's "Boundaries" talk (2012) for functional core, imperative shell.
