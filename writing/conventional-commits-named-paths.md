---
name: Commit messages — one change per commit, type prefix, named paths
kind: writing
source: Conventional Commits specification; Linux kernel and Git project commit practice
url: https://www.conventionalcommits.org
status: proposed
applies-to:
  - commit messages
  - pull request descriptions
  - agent-generated changes
  - changelog generation
---

# Commit messages — one change per commit, type prefix, named paths

**What it is:** a commit message format that a reader (or a script) can scan and act on without opening the diff.

## Take

- Subject line: `<type>(<scope>): <imperative summary>`, under 72 characters. Types from a fixed list: `feat`, `fix`, `refactor`, `test`, `docs`, `chore`, `perf`. Scope is the package or area (`engine`, `api`, `ui/invoices`).
- Imperative mood, no trailing period: `fix(engine): reject stock issue below zero`.
- Body (after a blank line) says what changed and why, and names the files or symbols touched: "Adds `assertNonNegativeStock` in `packages/engine/src/stock.ts`; `issueGoods` now returns `INSUFFICIENT_STOCK`."
- One logical change per commit. Formatting-only changes are their own commit. A commit that needs "and also" in the subject should be split.
- Breaking changes carry `!` after the type and a `BREAKING CHANGE:` footer stating the migration step.
- Reference the issue or spec by name in a footer (`Refs: specs/stock/stock-cannot-go-negative.yaml`), not only by number.
- When a pattern from this library was used, cite it in the body: "Pattern: inpo/code-patterns/result-error-as-value".
- PR description mirrors the commit body and adds: how it was verified (command and pasted result), and what was deliberately left out.

## Leave

- Emoji prefixes; they do not sort or grep.
- Subjects like "update", "fixes", "wip", or a ticket number alone.

## Evidence

- Specification at the URL above, section "Summary".
- Example subject from practice: `feat(ui/pos): add quick-cash tender buttons`
