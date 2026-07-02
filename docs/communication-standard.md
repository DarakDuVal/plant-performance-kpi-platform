# Communication standard

This document defines how the agents communicate and write code so the setup
stays cheap and reliable to run on AI models. Every agent references it.

The guiding rule: **humans may be wordy; agents must not be.** A customer request
can be bloated, imprecise, and long. Everything the agents produce for each other
— and the code they write — must be minimal, exact, and clear, to keep token use
low and meaning unambiguous.

## Agent-to-agent communication

When an agent hands off to another agent (see [`delivery-loop.md`](delivery-loop.md)),
the message it produces must:

- **Be minimal.** Say only what the next step needs. No restating the request, no
  filler, no pleasantries, no self-description.
- **Be exact.** Use precise terms, concrete values, and the names defined in the
  requirements spec. Prefer one unambiguous word over a vague sentence.
- **Be clear.** Structure beats prose: use short bullets, tables, or labelled
  fields. One fact per line.
- **Carry only the needed context.** Reference shared artifacts (for example the
  requirements spec) by name instead of copying them.
- **State assumptions and gaps explicitly**, then stop. Do not pad.

Spend tokens on the human-facing intake and the final customer response, where
clarity for people matters. Keep everything in between lean.

## Self-explanatory code

Code is communication too. Agents that write or review code must:

- **Make the code explain itself** through clear names, small functions, and
  single responsibility, so it needs little description.
- **Limit comments to intent.** Comment *why*, not *what*. Delete comments that
  merely restate the code.
- **Avoid bloat.** No dead code, no speculative abstraction, no redundant
  documentation that repeats the code.
- **Keep prose around code minimal** — a short rationale, not an essay.

This reinforces the senior software developer's Clean Code mandate: the smallest
correct, readable solution wins.

## Why this matters

Minimal, exact communication lowers token cost, reduces misreadings between
agents, and keeps the delivered code easy for the next agent — or human — to
extend.
