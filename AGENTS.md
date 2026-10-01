# AGENTS.md — inspiration

1. This repo is a reference library for coding agents, not a product. Every file under `design/`, `code-patterns/`, `architecture/`, `writing/`, `prompts/` is one entry.
2. Start with `README.md`: it holds the index (per kind, with status and applies-to) and the Rejected list.
3. When working on another project, open only the entries whose `applies-to` matches the task, borrow the patterns in **Take**, and cite the entry by name in your rationale, commit message, or design note.
4. The project's own conventions always win over an entry here.
5. Never copy branding, voice, or licensed code verbatim. Take patterns and structure, not text or assets.
6. Never re-propose anything on the Rejected list in `README.md`.
7. To add an entry: copy `_template.md`, keep it under 60 lines, fill every front-matter field, set `status: proposed`, save evidence as `images/<kind>-<slug>-<n>.png`, and add a row to the README index.
8. `url` is the homepage or canonical link only. Do not invent deep links.
9. Only the owner changes `status` to `owner-approved` or `rejected`.
10. Write Take bullets as checkable facts (sizes, counts, order, rules), in plain words, no marketing tone.
