---
name: Verification-first instruction — run the check, paste the output, then claim done
kind: prompt
source: Practice in Claude Code and similar agent workflows; test-driven development discipline
url: https://docs.anthropic.com
status: proposed
applies-to:
  - agent system prompt
  - task hand-off to a coding agent
  - pull request descriptions
  - definition of done
---

# Verification-first instruction — run the check, paste the output, then claim done

**What it is:** an instruction block that makes "done" mean "the named command ran and its output is in the report".

## Take

- Name the exact commands that define done, in order: for example `pnpm typecheck`, `pnpm test`, `pnpm lint`, and for UI work a screenshot command per viewport. Put them in AGENTS.md and repeat them in the task prompt.
- Require the final report to contain, verbatim: each command, its exit code, and the last 20 lines of its output (or the full failure). A report without pasted output is treated as not done.
- State the order: write or update the test or spec first, see it fail, implement, see it pass, then refactor. Ask for the failing run to be pasted too when the change is a bug fix.
- Forbid claims the agent did not observe: "should work", "I believe this passes". Allowed phrasing: "ran X, got Y".
- When a check cannot be run (missing service, missing credentials), the report says so by name and marks the task not verified; it does not substitute reasoning for the run.
- For UI: screenshots saved to a known path per viewport and state, with file names listed in the report; the agent describes what each shows in one line.
- Scope the claim: list what was verified and what was not, separately.
- Keep the instruction under 15 lines so it survives in every prompt.

## Leave

- Asking for "thorough testing" without naming commands; it produces prose instead of evidence.
- Requiring 100 percent coverage figures; require the specific checks that matter for the change.

## Evidence

- Illustrative block:
  `Done means: pnpm typecheck && pnpm test && pnpm lint all exit 0. Paste each command and its output in your report. Do not say "should"; say "ran, got".`
- Practice recorded in this org's agent instructions, 2026.
