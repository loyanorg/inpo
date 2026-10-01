---
name: Project AGENTS.md as the single entry point to anchor, state and backlog docs
kind: prompt
source: AGENTS.md convention (agents.md), CLAUDE.md practice in Claude Code projects
url: https://agents.md
status: proposed
applies-to:
  - agent system prompt
  - project onboarding for coding agents
  - repository documentation layout
---

# Project AGENTS.md as the single entry point to anchor, state and backlog docs

**What it is:** one short file at the repo root that tells an agent where everything else is and what to read first.

## Take

- `AGENTS.md` at the repo root, under 40 lines. `CLAUDE.md`, if present, contains one line: `Read AGENTS.md.`
- Section order: purpose (2 lines), read-first list (3 to 5 links), commands (install, test, lint, run; exact strings), rules (5 to 10 bullets), where to record decisions.
- The read-first list points at exactly three living documents: `docs/ANCHOR.md` (principles that do not change), `docs/STATE.md` (what is built, what is in progress, known gaps, updated every session), `docs/BACKLOG.md` (ordered list of next work with acceptance criteria).
- Each linked doc has an owner and a "last updated" date on its first line.
- Commands are copy-pasteable and verified by CI; if `pnpm test` is not what runs the tests, AGENTS.md is wrong and must be fixed in the same PR.
- Rules are checkable: "Run `pnpm check` before claiming done", "Business rules live only in `packages/engine`", "Cite inspiration entries by name".
- A pointer to this library: "Before designing a screen, writing user-facing copy, or choosing a structure, read https://github.com/loyanorg/inpo."
- The agent updates `STATE.md` at the end of every session; AGENTS.md says so explicitly.

## Leave

- Long narrative history in AGENTS.md; it belongs in `STATE.md` or git log.
- Duplicating rules across AGENTS.md, CLAUDE.md, CONTRIBUTING.md and README.md; one source, the others link.

## Evidence

- agents.md convention page (URL above).
- Illustrative structure: see the `AGENTS.md` in this repository for the compact form.
