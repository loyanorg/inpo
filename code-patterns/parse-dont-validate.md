---
name: Parse, don't validate — typed values at the boundary once
kind: code-pattern
source: Alexis King, "Parse, don't validate" (2019); Zod/Valibot as TypeScript implementations
url: https://lexi-lambda.github.io/blog/2019/11/05/parse-don-t-validate/
status: proposed
applies-to:
  - API request handling
  - form submission
  - file and CSV import
  - configuration loading
  - any untrusted input
---

# Parse, don't validate — typed values at the boundary once

**What it is:** input is converted into a precise type at the edge; inner code receives only values that cannot be invalid.

## Take

- Every boundary (HTTP handler, CLI argument, file import, env var) runs a parser that returns either a typed value or a structured error listing each failing field with a code. Nothing downstream re-checks.
- Parsed types are narrower than their source: `NonEmptyString`, `PositiveInt`, `Money`, `Sku`, `EmailAddress`, `IsoDate`. Use branded types so a plain `string` cannot be passed where a `Sku` is expected.
- Parsers live next to the type they produce and are the only way to construct it (no public constructor or literal).
- Schemas (Zod or similar) are defined once and used for both the parser and the generated API documentation or OpenAPI, so they cannot drift.
- Errors from the parser are returned as a Result (see the Result entry), with field path, code and the rejected value, not thrown.
- Internal functions take the parsed types and have no `if (!x) throw` guards. Guard clauses inside the domain indicate the boundary parser is incomplete; fix the parser.
- Dates and numbers are parsed with an explicit format and locale; no `new Date(string)` or `parseFloat` on user input.

## Leave

- Validating the same field in the UI, the API and the database with three different rule sets; the schema is shared, the UI reuses it.
- Trusting internal callers less than external ones; once typed, the value is trusted everywhere.

## Evidence

- Blog post at the URL above, section "The power of parsing".
- Quote: "a parser is just a function that consumes less-structured input and produces more-structured output."
