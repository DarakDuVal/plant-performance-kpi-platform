# User stories

User stories sliced from the [user journeys](user-journeys.md). Each story is a small, independently valuable increment
and is made testable by one or more [functional requirements](functional-requirements.md).

**How to use:** give each story a stable `US-NNN` id. Write it in the `As a … I want … so that …` form, add a
Given-When-Then acceptance criterion, link the journey it comes from and the requirements that satisfy it, then
prioritise (`MUST` / `SHOULD` / `COULD`) and set a target iteration so stories are resolved stepwise.

## Story backlog

| ID     | Story (As a … I want … so that …)                      | Acceptance criterion (Given-When-Then)       | Journey | Requirements | Priority | Iteration | Status |
| ------ | ------------------------------------------------------ | -------------------------------------------- | ------- | ------------ | -------- | --------- | ------ |
| US-001 | As a [persona], I want [capability] so that [benefit]. | Given [context] When [action] Then [result]. | UJ-001  | FR-001       | MUST     | 1         | Draft  |

**Priority key:** `MUST` — required for the baseline release · `SHOULD` — important but deferrable · `COULD` — nice to
have.

**Status key:** `Draft` -> `Ready` -> `In progress` -> `Done` (or `Deferred`).
