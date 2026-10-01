---
name: Twelve-factor config — environment variables, documented in one place
kind: architecture
source: The Twelve-Factor App (Adam Wiggins / Heroku), factor III
url: https://12factor.net
status: proposed
applies-to:
  - configuration and secrets
  - deployment to any host
  - onboarding a new developer or agent
  - CLI and server startup
---

# Twelve-factor config — environment variables, documented in one place

**What it is:** everything that differs between deploys is an environment variable; one file lists every name, type, default and purpose.

## Take

- One module (`packages/config` or `src/config.ts`) reads `process.env` exactly once at startup, parses every variable with a schema (see parse-don't-validate), and exports a frozen typed object. No other file reads `process.env`.
- Startup fails fast with one message listing every missing or malformed variable by name, before any connection is opened.
- `.env.example` in the repo root lists every variable with a comment: purpose, type, example value, whether it is required. It is kept in sync by a test that compares the schema keys to the example file.
- Variable names are `UPPER_SNAKE_CASE`, prefixed by app or subsystem (`DIWAAN_DATABASE_URL`, `SMTP_HOST`). Booleans accept only `true`/`false`.
- Secrets never have defaults. Non-secrets may have defaults, which are stated in the schema and in `.env.example`.
- No config file per environment checked into the repo (`config/production.json`); the environment supplies the values.
- The running app can print its effective non-secret config (`--print-config` or an admin endpoint) with secrets masked, for debugging deploys.

## Leave

- Grouping dozens of variables into one JSON blob variable; it defeats per-variable documentation and per-variable overrides.
- Reading env vars lazily deep in the code; failures then appear at request time instead of startup.

## Evidence

- 12factor.net, "III. Config" (URL above).
- Quote: "Apps sometimes store config as constants in the code. This is a violation of twelve-factor, which requires strict separation of config from code."
