---
name: Spec-driven acceptance — YAML scenarios plus an executable reference model
kind: architecture
source: Cucumber / Gherkin specification by example; model-based testing practice
url: https://cucumber.io
status: proposed
applies-to:
  - acceptance testing
  - business rule specification
  - regression protection on calculations
  - agent-written code that must be verified
---

# Spec-driven acceptance — YAML scenarios plus an executable reference model

**What it is:** behaviour is written as data files, run against both the real engine and a small reference model; the two must agree.

## Take

- Each scenario is one YAML file under `specs/<domain>/<slug>.yaml` with `given` (initial state as plain data), `when` (a list of commands), `then` (expected state, expected rejections, expected events). No code in the spec.
- A single runner loads every spec and executes it against the real engine. The runner is the only test harness for business behaviour; unit tests cover algorithms and parsers.
- A reference model (`packages/reference-model`) implements the same commands in the simplest possible way (plain objects, no persistence, no optimisation). The runner executes every spec against it too and fails if the two outputs differ.
- When a business question arises, the answer is a new spec file, reviewed by the owner, before any code changes.
- Specs are named by rule, not by ticket: `stock-cannot-go-negative.yaml`, not `BUG-123.yaml`.
- The runner prints a per-spec pass/fail table; CI fails on any mismatch; the table is pasted into the PR.
- Property-style generators may produce random command sequences, run against both engine and model, and save any divergence as a new YAML spec.

## Leave

- Natural-language Gherkin with regex step definitions; the step layer becomes its own maintenance burden. Plain data is enough.
- Browser-driven acceptance tests as the primary oracle; keep those for a handful of smoke paths.

## Evidence

- Specification by example as practised in the Cucumber community (URL above).
- Illustrative spec:
  `given: { stock: { SKU-1: 5 } }`
  `when: [ { issue: { sku: SKU-1, qty: 7 } } ]`
  `then: { rejected: INSUFFICIENT_STOCK, stock: { SKU-1: 5 } }`
