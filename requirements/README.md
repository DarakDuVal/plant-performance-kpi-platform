# Requirements

This directory is the single place where the **plant performance KPI platform**
requirements are gathered before they are resolved by the agent delivery loop.
It captures four artifact types and keeps them linked so work can be tackled in a
**structured, stepwise** way — one thin, prioritised slice per iteration.

## What lives here

| File | Purpose |
| --- | --- |
| [`user-journeys.md`](user-journeys.md) | End-to-end journeys per persona — the "why" and the flow. |
| [`user-stories.md`](user-stories.md) | User stories sliced from the journeys, each with acceptance criteria. |
| [`functional-requirements.md`](functional-requirements.md) | What the system must do (`FR-NNN`), traceable to stories. |
| [`non-functional-requirements.md`](non-functional-requirements.md) | How well it must do it (`NFR-NNN`) — performance, security, and so on. |

## How the artifacts connect

```text
user journey  ->  user stories  ->  functional / non-functional requirements
   (UJ-NNN)         (US-NNN)                  (FR-NNN / NFR-NNN)
```

- A **journey** frames a persona's goal and the steps to reach it.
- Each journey step yields one or more **user stories**.
- Each story is made testable by one or more **functional** requirements, with
  cross-cutting quality captured as **non-functional** requirements.
- IDs are **stable and never reused**, so a story or requirement can be traced
  back to the journey it came from and forward to the design, tests, and code.

## Stepwise resolution

The platform is delivered iteratively and spec-anchored (see
[`../docs/delivery-loop.md`](../docs/delivery-loop.md)). Gather requirements here,
then resolve them in priority order:

1. **Capture** journeys, stories, and requirements in the files above.
2. **Prioritise** each item as `MUST` / `SHOULD` / `COULD` and assign a target
   **iteration**.
3. **Slice** the next iteration from the `MUST` items whose dependencies are met.
4. **Baseline** that slice into an initiative spec from
   [`../product/requirements-template.md`](../product/requirements-template.md)
   and run it through the delivery loop.
5. **Reconcile** on close: update status here so the backlog reflects what is
   built and verified, and never drifts behind the code.

Track progress with the **Status** column in each file:
`Draft` -> `Ready` -> `In progress` -> `Done` (or `Deferred`).

## Authoring rules

Write every item so both humans and AI agents can consume it, following
[`../docs/spec-authoring-guide.md`](../docs/spec-authoring-guide.md):

- **Atomic** — one behaviour per requirement; split compound statements.
- **Unambiguous** — no vague words; put numbers and limits in NFRs.
- **Testable** — every requirement and story has a Given-When-Then acceptance
  criterion a test can assert.
- **No implementation detail** — describe *what* and *how well*, not *how*.
- Keep domain background in the project context artifact
  ([`../docs/context-template.md`](../docs/context-template.md)), referenced by
  link — not inlined here.
