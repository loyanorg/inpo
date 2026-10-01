---
name: Result type — errors as values with typed rejection codes
kind: code-pattern
source: Rust std::result and the TypeScript "neverthrow" library (pattern, not the library)
url: https://doc.rust-lang.org/std/result/
status: proposed
applies-to:
  - business rule enforcement
  - service and engine functions
  - API error responses
  - anything a UI must explain to a user
---

# Result type — errors as values with typed rejection codes

**What it is:** business rules return `{ ok: true, value }` or `{ ok: false, code, details }` instead of throwing.

## Take

- Every engine or service function that can fail for a business reason returns a `Result<T, Rejection>`. Exceptions are reserved for bugs and infrastructure faults (network, disk, programmer error).
- `Rejection` has a closed union of string codes (for example `INSUFFICIENT_STOCK`, `PERIOD_CLOSED`, `DUPLICATE_REFERENCE`), each with a typed `details` object naming the entities and numbers involved.
- Codes are defined once, in one file per domain, and exported. Tests assert on codes, never on message text.
- The API layer maps each code to one HTTP status and one user-facing message template; the UI layer renders the message with `details` substituted. Neither layer invents its own codes.
- Callers must branch on `ok` before reading `value`; the type system enforces it (discriminated union, no `any`).
- Compose with early return: `const r = step(); if (!r.ok) return r;`. Do not wrap Result in try/catch.
- Log rejections at info level with the code and details; log thrown exceptions at error level with a stack.

## Leave

- Importing a heavy functional library just for Result; a 20-line type and two helpers (`ok()`, `err()`) are enough.
- Using Result for infrastructure failures; let those throw and be caught at the top of the request.
- Free-text error strings as the only payload; a UI cannot localise or act on them.

## Evidence

- Pattern as documented in the Rust standard library (URL above).
- Snippet (illustrative):
  `type Result<T, E = Rejection> = { ok: true; value: T } | { ok: false; error: E };`
  `type Rejection = { code: 'INSUFFICIENT_STOCK'; details: { sku: string; requested: number; available: number } } | ...`
