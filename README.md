# inpo

A library of named, well-regarded references that Claude Code sessions and other LLM-based coding agents read while working, so their output draws on specific examples instead of generic defaults. It serves every project in the org (current ones include a business system for trading businesses in TypeScript/React/PostgreSQL) and is tied to none. It holds five kinds of entry: UI and product design, code patterns, architecture, writing, and prompt or agent-instruction examples. Entries are text-first: observations a model can act on, not a gallery for people.

## How a session uses it

1. Read this file's index.
2. Open the entries whose `applies-to` matches the task at hand.
3. Borrow the patterns listed under **Take**. Respect **Leave**.
4. Cite the entry by name in your rationale, commit message, PR description or design note (for example "Pattern: inpo/design/stripe-dashboard-figures").
5. The project's own conventions always win over an entry here.
6. Never copy branding, voice, or licensed code verbatim. Take patterns and structure, not text or assets.
7. Never re-propose anything in the Rejected section below.

## How to add an entry

1. The owner drops a name, link, screenshot or snippet (in Slack, a file, or an issue).
2. A session copies `_template.md` into the matching `kind/` folder, fills every front-matter field (`name`, `kind`, `source`, `url`, `status`, `applies-to`), writes **What it is**, **Take**, **Leave**, **Evidence**, keeps it under 60 lines, and saves any screenshot as `images/<kind>-<slug>-<n>.png`.
3. The session sets `status: proposed` and adds a row to the index below.
4. The owner promotes the entry to `owner-approved` or marks it `rejected` (and, if rejected, adds a line to the Rejected section).

`url` is the homepage or canonical link only; never invent deep links. Take bullets state something a model can implement or check, not a mood.

## How a project points at it

Add this line to the project's `AGENTS.md` or `CLAUDE.md`:

> Before designing a screen, writing user-facing copy, or choosing a structure, read https://github.com/loyanorg/inpo (clone or fetch README.md and the matching kind/ folder) and cite entries by name.

Shallow-clone it into a sibling folder:

```sh
git clone --depth 1 https://github.com/loyanorg/inpo ../inpo
```

## Index

### design/

| Entry | Status | Applies to |
|---|---|---|
| [Linear — dense issue lists and command palette](design/linear-dense-lists.md) | proposed | dense list screens, keyboard-driven navigation, record metadata display, desktop web apps |
| [Stripe Dashboard — figures first, records as amount, status, timeline](design/stripe-dashboard-figures.md) | proposed | financial record pages, transaction and ledger lists, filtering large tables, reporting screens |
| [Square Point of Sale — touch-first tile grid and tender flow](design/square-pos-touch.md) | proposed | point of sale, tablet-first screens, touch input, cash and payment entry, counter and warehouse workflows |
| [Apple HIG — touch targets, dynamic type, platform conventions](design/apple-hig-platform-basics.md) | proposed | touch input, tablet-first screens, accessibility, form and control sizing, iPad/iPhone use |

### code-patterns/

| Entry | Status | Applies to |
|---|---|---|
| [Result type — errors as values with typed rejection codes](code-patterns/result-error-as-value.md) | proposed | business rule enforcement, service and engine functions, API error responses, UI-explained failures |
| [Money as integer minor units with exact arithmetic](code-patterns/money-integer-minor-units.md) | proposed | money handling, pricing/tax/discount calculation, ledgers and invoices, schema for amounts |
| [Append-only event log with derived read models](code-patterns/append-only-event-log.md) | proposed | inventory and stock movements, ledgers and journals, audit trail, reconstructable history |
| [Parse, don't validate — typed values at the boundary once](code-patterns/parse-dont-validate.md) | proposed | API request handling, form submission, file/CSV import, configuration loading, untrusted input |

### architecture/

| Entry | Status | Applies to |
|---|---|---|
| [Single engine package — all business rules in one place](architecture/single-engine-package.md) | proposed | monorepo layout, where a rule lives, systems with web/API/import paths, testing strategy |
| [Spec-driven acceptance — YAML scenarios plus reference model](architecture/spec-driven-acceptance-yaml.md) | proposed | acceptance testing, rule specification, regression on calculations, verifying agent-written code |
| [Local-first dev with an in-process database, same SQL in production](architecture/local-first-in-process-db.md) | proposed | developer setup, test speed, PostgreSQL projects, agent sessions without external services |
| [Twelve-factor config — env names documented in one place](architecture/twelve-factor-config.md) | proposed | configuration and secrets, deployment, onboarding, CLI and server startup |

### writing/

| Entry | Status | Applies to |
|---|---|---|
| [Stripe API docs — one concept per page, runnable examples, errors with fixes](writing/stripe-api-docs.md) | proposed | API reference docs, developer READMEs, error catalogues, engine documentation |
| [GOV.UK content style — plain words, one idea per sentence, answer first](writing/govuk-content-style.md) | proposed | user-facing copy, form labels and hints, help text, notifications and emails, error messages |
| [Commit messages — one change per commit, type prefix, named paths](writing/conventional-commits-named-paths.md) | proposed | commit messages, PR descriptions, agent-generated changes, changelog generation |
| [Error messages — what happened, what to do, what was recorded](writing/error-messages-what-then-do.md) | proposed | error messages, CLI error output, API error bodies, failed jobs and imports, toasts and banners |

### prompts/

| Entry | Status | Applies to |
|---|---|---|
| [Project AGENTS.md as the single entry point](prompts/project-agents-md-entry-point.md) | proposed | agent system prompt, onboarding coding agents, repository documentation layout |
| [Anchor document — non-negotiable principles in under a page](prompts/anchor-doc-principles.md) | proposed | agent system prompt, project principles, resolving design and scope disagreements, onboarding |
| [Design brief template with explicit anti-patterns](prompts/design-brief-with-anti-patterns.md) | proposed | briefing an agent to build a screen, design notes, new screen requests, tablet and desktop UI |
| [Verification-first instruction — run the check, paste the output, then claim done](prompts/verification-first-instruction.md) | proposed | agent system prompt, task hand-off, PR descriptions, definition of done |

## Rejected

Patterns the owner has turned down. Do not re-propose them.

- **Explanatory copy inside business software** (how-it-works cards, legends, hints that restate labels, notes explaining a figure). Users are professionals; clarity comes from design. Recorded 1 Oct 2026.
- **Deriving product assumptions from demo data** (treating sample goods or sample customer behaviour as requirements). Demo data exercises the UI; it is not a specification. Recorded 1 Oct 2026.
- **Generic first-pass layouts for new screens.** New screens are expected high-fidelity and production-ready from the first pass, with tablet as important as desktop. Recorded 1 Oct 2026.
