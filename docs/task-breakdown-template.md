# Task breakdown — template

This template turns the **solution design + the spec slice for the current
iteration** into a small, ordered, independently-verifiable **task list**. It is
produced at the **task-decomposition** step of the delivery loop (see
[`delivery-loop.md`](delivery-loop.md)) by the senior software architect, and it is
the per-iteration backlog — the unit of the agile increment.

Instantiate it in the engagement workspace (for example as `05-tasks.md`), never in
this catalog repository.

## Iteration

- **Iteration:** [n]
- **Spec revision covered:** [e.g. r3]
- **Goal of this iteration (thin increment):** [one sentence describing the
  working slice of behaviour this iteration delivers]

## Tasks

Each task is small, independently verifiable, and traceable to one or more
requirement IDs. Order tasks so dependencies come first.

| Task ID | Requirement IDs | Description | Acceptance check | Dependencies | Definition of done |
| --- | --- | --- | --- | --- | --- |
| T-001 | FR-001 | [what to build] | [observable check that proves it] | — | [tests pass, spec updated, reviewed] |
| T-002 | FR-002, NFR-003 | [what to build] | [observable check] | T-001 | [tests pass, spec updated, reviewed] |

**Rules:**

- Every task references at least one `FR`/`NFR` ID. A task with no requirement is
  out of scope — add the requirement to the spec first (spec-first, then code).
- Keep each task small enough to complete and verify within the iteration.
- The **definition of done** for every task includes: acceptance check passes, the
  spec reflects the delivered behaviour (no drift), and the change is reviewed.

## Out of scope for this iteration

List work deferred to a later iteration so the increment stays thin.

- [Deferred: …]
