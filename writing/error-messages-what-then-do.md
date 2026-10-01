---
name: Error messages — what happened with names and numbers, what to do, what was recorded
kind: writing
source: GOV.UK design system error patterns; Nielsen Norman Group error-message guidelines
url: https://design-system.service.gov.uk
status: proposed
applies-to:
  - error messages
  - CLI error output
  - API error bodies
  - failed background jobs and imports
  - toasts and banners
---

# Error messages — what happened with names and numbers, what to do, what was recorded

**What it is:** a three-part structure for every error shown to a person: fact, action, state.

## Take

- Part 1, what happened: one sentence with the concrete entity and figures. "Invoice INV-2041 could not be issued: stock for SKU-118 is 5, order needs 7."
- Part 2, what to do: one sentence naming the action available to this user. "Reduce the quantity or receive stock first." If nothing can be done, say who to contact.
- Part 3, what was or was not recorded: "Nothing has been saved." or "The payment of 1,250.00 AED was recorded; the receipt email was not sent." Never leave the user guessing whether a write happened.
- Each message maps to one rejection code (see Result entry); the code is shown in small text or a details disclosure for support, not in the headline.
- Inline field errors use parts 1 and 2 only, under 12 words: "Enter a date on or after 1 Oct 2026."
- CLI and log output: same three parts on separate lines, prefixed `error:`, `fix:`, `state:`; exit code non-zero; no stack trace unless `--verbose`.
- API error body: `{ code, message, details, recorded: boolean }` where `message` is the three parts joined.
- No apology, no exclamation marks, no "Oops". No blame of the user ("You entered an invalid value").

## Leave

- Generic fallbacks such as "Something went wrong" as the only message; if the cause is unknown, say that and give a reference id.
- Technical causes in the headline ("ECONNREFUSED 10.0.0.4:5432"); put them in details.

## Evidence

- GOV.UK design system, "Error message" component (URL above).
- NN/g, "Error Message Guidelines" (public article), rules 1 to 4.
