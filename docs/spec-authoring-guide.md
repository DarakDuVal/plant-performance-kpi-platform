# Spec authoring guide

The requirements spec is the living source of truth for an engagement. It is read by **humans and by AI agents**, and it
must stay reviewable as it grows. This guide defines how to write specs so both audiences can rely on them. Use it
together with [`../product/requirements-template.md`](../product/requirements-template.md).

## Dual audience: humans and AI agents

The spec is consumed by people **and** by AI agents that generate design, tasks, code, and tests from it. Write for
both:

- **Atomic requirements.** One behaviour per `FR`. Split compound requirements ("the system shall do X and Y") into
  separate IDs.
- **Unambiguous.** Avoid vague words ("fast", "robust", "user-friendly"); state measurable conditions instead. Put
  numbers and limits in non-functional requirements.
- **Testable.** Every requirement has a Given-When-Then acceptance criterion that a test can assert directly.
- **No implementation detail.** Requirements describe **what** and **how well**, not **how**. Implementation choices
  belong in design, ADRs, or tasks — not in the spec.

## Reviewability and anti-bloat

AI-generated specs grow quickly and become hard to review. Keep them lean:

- **Prefer tables and IDs over prose.** The requirements template is table-first; keep it that way.
- **Split when large.** When a spec exceeds roughly **40 requirements** (or a single area dominates), split it by
  capability or bounded context so each spec stays reviewable in one sitting.
- **Keep context out of the spec.** Domain background, glossary, and integrations belong in the project context /
  steering artifact ([`context-template.md`](context-template.md)), referenced by link — not inlined into the spec.
- **Human-review AI-generated specs.** Any spec drafted by an AI agent is reviewed and **trimmed** by a human (or the
  requirements engineer) before it is baselined. Remove duplicates, speculative requirements, and anything untestable.

## Determinism aids (anchors for AI consumption)

These make the spec a reliable machine input:

- **Controlled vocabulary.** Use `MUST` / `SHOULD` / `COULD` for priority exactly as defined in the template.
- **Stable IDs.** `FR-NNN` / `NFR-NNN` IDs never change meaning or get reused; superseded requirements are marked, not
  renumbered.
- **Explicit out-of-scope and assumptions.** Fill these sections; what is excluded is as important to an AI agent as
  what is included.
- **Status and traceability columns.** Keep each requirement's status (`Specified` / `Implemented` / `Verified` /
  `Drifted`) and its traceability links current so both humans and agents can see what is real versus planned.
