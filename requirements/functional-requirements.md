# Functional requirements

What the **plant performance KPI platform** must do. Each functional requirement
describes one behaviour, is traceable to the [user story](user-stories.md) that
motivates it, and carries a Given-When-Then acceptance criterion a test can
assert. When a slice is ready to build, baseline it into an initiative spec from
[`../product/requirements-template.md`](../product/requirements-template.md).

**How to use:** give each requirement a stable `FR-NNN` id (never reused). Keep it
atomic — split "the system shall do X and Y" into two ids. Prioritise
(`MUST` / `SHOULD` / `COULD`) and set a target iteration so requirements are
resolved stepwise. Track the **Spec status** so drift stays visible.

## Requirements

| ID | Priority | Requirement | Acceptance criterion (Given-When-Then) | Story | Iteration | Spec status |
| --- | --- | --- | --- | --- | --- | --- |
| FR-001 | MUST | The system shall [what it does]. | Given [context] When [action] Then [result]. | US-001 | 1 | Specified |

**Priority key:** `MUST` — required for the baseline release · `SHOULD` — important
but deferrable · `COULD` — nice to have.

**Spec status key:** `Specified` (not built) · `Implemented` (built) · `Verified`
(built and covered by a passing, traceable test) · `Drifted` (code and spec
disagree — reconcile before the iteration closes).
