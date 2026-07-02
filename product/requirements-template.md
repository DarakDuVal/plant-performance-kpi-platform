# Requirements — [Initiative name]

**ID:** REQ-[NNN]  
**Spec revision:** r[N]  
**Date:** YYYY-MM-DD  
**Author:** [role or name]  
**Status:** Draft | Under review | Baselined | Superseded  
**Related ADRs:** ADR-NNN, …

> **Intended consumers: humans + AI agents.** This spec is the living source of truth and is read by people and by AI
> agents that generate design, tasks, code, and tests from it. Author it per
> [`../docs/spec-authoring-guide.md`](../docs/spec-authoring-guide.md): atomic, unambiguous, testable, no implementation
> detail, and keep it lean and reviewable. Keep domain background in the project context artifact
> ([`../docs/context-template.md`](../docs/context-template.md)), not inlined here.

---

## Context

One paragraph describing the business situation, user need, or problem that these requirements address. Keep it to what
a developer or tester needs to understand the scope.

## Stakeholders

| Role          | Interest               |
| ------------- | ---------------------- |
| [stakeholder] | [what they care about] |

---

## Functional requirements

Each functional requirement describes **what** the system must do.

The **Spec status** marks each requirement against the implementation so drift is visible at a glance: `Specified` (in
spec, not built) · `Implemented` (built) · `Verified` (built and covered by a passing, traceable test) · `Drifted` (code
and spec disagree — must be reconciled before an iteration closes). **Traceability** links each requirement to its
design element, test(s), and implementation reference.

| ID     | Priority | Requirement          | Acceptance criterion    | Spec status | Traceability (design → test → code)   |
| ------ | -------- | -------------------- | ----------------------- | ----------- | ------------------------------------- |
| FR-001 | MUST     | [The system shall …] | [Given … When … Then …] | Specified   | [design ref] → [test id] → [code ref] |
| FR-002 | SHOULD   | [The system shall …] | [Given … When … Then …] | Specified   | …                                     |
| FR-003 | COULD    | [The system shall …] | [Given … When … Then …] | Specified   | …                                     |

**Priority key:**

- `MUST` — required for the baseline release; no exceptions.
- `SHOULD` — important but can be deferred to the next iteration if necessary.
- `COULD` — nice to have; only if capacity allows.

---

## Non-functional requirements

Each non-functional requirement describes **how well** the system must do it.

| ID      | Category        | Priority | Requirement                                                         | Measurement        | Spec status | Traceability (design → test → code) |
| ------- | --------------- | -------- | ------------------------------------------------------------------- | ------------------ | ----------- | ----------------------------------- |
| NFR-001 | Performance     | MUST     | [e.g. API p95 response ≤ 200 ms under 100 concurrent users]         | Load test result   | Specified   | …                                   |
| NFR-002 | Reliability     | MUST     | [e.g. Service availability ≥ 99.5 % per calendar month]             | Uptime monitoring  | Specified   | …                                   |
| NFR-003 | Security        | MUST     | [e.g. All data in transit encrypted with TLS 1.2+]                  | Security scan      | Specified   | …                                   |
| NFR-004 | Maintainability | SHOULD   | [e.g. Unit test coverage ≥ 80 %]                                    | CI coverage report | Specified   | …                                   |
| NFR-005 | Scalability     | SHOULD   | [e.g. System handles 10× baseline load without architecture change] | Capacity test      | Specified   | …                                   |
| NFR-006 | Usability       | COULD    | [e.g. New user completes onboarding in < 5 minutes]                 | Usability test     | Specified   | …                                   |

**NFR categories:** Performance · Reliability · Security · Maintainability · Scalability · Usability · Compliance ·
Portability

---

## Assumptions and constraints

- **Assumption:** [Something assumed to be true that has not been confirmed.]
- **Constraint:** [A limit imposed by technology, regulation, or the existing system.]

---

## Out of scope

List anything explicitly excluded to prevent scope creep.

- [Not in scope: …]

---

## Open questions

| #   | Question              | Owner  | Due        |
| --- | --------------------- | ------ | ---------- |
| 1   | [Unresolved question] | [role] | YYYY-MM-DD |

---

## Spec revision history

The spec is the living source of truth and is **revised per iteration**. Record a new **spec revision** whenever the
spec changes (new iteration, change request, or drift reconciliation). Update the **Spec revision** field in the header
to match the latest row. Spec-first, then code: behaviour changes are entered here before they are implemented.

| Spec revision | Date       | Author | Iteration | Change           |
| ------------- | ---------- | ------ | --------- | ---------------- |
| r1            | YYYY-MM-DD | [role] | 1         | Initial baseline |
