# Non-functional requirements

How well the **plant performance KPI platform** must do its job — the quality
attributes that cut across features. Each non-functional requirement is
measurable and testable. When a slice is ready to build, baseline it into an
initiative spec from
[`../product/requirements-template.md`](../product/requirements-template.md).

**How to use:** give each requirement a stable `NFR-NNN` id (never reused). State
a concrete, measurable threshold and how it is measured — avoid vague words like
"fast" or "robust". Prioritise (`MUST` / `SHOULD` / `COULD`) and set a target
iteration so requirements are resolved stepwise.

## Requirements

| ID | Category | Priority | Requirement | Measurement | Iteration | Spec status |
| --- | --- | --- | --- | --- | --- | --- |
| NFR-001 | Performance | MUST | [e.g. KPI dashboard loads in ≤ 2 s for 50 concurrent users] | Load test result | 1 | Specified |
| NFR-002 | Security | MUST | [e.g. All data in transit encrypted with TLS 1.2+] | Security scan | 1 | Specified |

**Categories:** Performance · Reliability · Security · Maintainability ·
Scalability · Usability · Compliance · Portability.

**Priority key:** `MUST` — required for the baseline release · `SHOULD` — important
but deferrable · `COULD` — nice to have.

**Spec status key:** `Specified` (not built) · `Implemented` (built) · `Verified`
(built and covered by a passing, traceable test) · `Drifted` (code and spec
disagree — reconcile before the iteration closes).
