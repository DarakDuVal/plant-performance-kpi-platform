# Constitution

This is the set of **invariant rules** every agent must honour in **every step of every iteration** of the delivery
loop. It is the project's non-negotiable layer: it sits above any single step, agent, or iteration and is carried into
each step alongside the requirements spec and the project context (see [`delivery-loop.md`](delivery-loop.md)).

The constitution is intentionally short and rule-shaped. It states **what must always hold**; the _how_ lives in
[`quality-standards.md`](quality-standards.md), [`spec-authoring-guide.md`](spec-authoring-guide.md), and the templates.
Where a rule needs detail, it links out rather than restating it.

## Articles

1. **Spec-first, then code.** Required behaviour is changed in the requirements spec **before** it is changed in code.
   No behaviour ships that is not described in the spec. (See [`spec-authoring-guide.md`](spec-authoring-guide.md).)
2. **No drift.** The spec is the living source of truth for the lifetime of the engagement. A change that alters
   behaviour without updating the spec — or that leaves a requirement in `Drifted` status — is incomplete and must not
   be accepted.
3. **Traceability.** Every `MUST` requirement maps to at least one passing acceptance test that references its
   requirement ID. Code, tests, and design trace back to requirement IDs.
4. **Test-first quality bar.** Tests are written before or alongside code (TDD), acceptance criteria use Given-When-Then
   (BDD), and unit test coverage stays **≥ 80 %**, enforced in CI. (See [`quality-standards.md`](quality-standards.md).)
5. **Linting and formatting gates.** Linting and formatting run in CI on every pull request and block merge on
   violation.
6. **Significant decisions are recorded.** Decisions that affect multiple components, carry non-obvious trade-offs, or
   are costly to reverse are captured as ADRs in [`decisions/`](decisions/).
7. **Security and least privilege.** Agents request only the access they need; no secrets are committed; changes must
   not introduce known vulnerabilities.
8. **Minimal documentation.** Documentation stays consistent, concise, and minimal — every document has a single stated
   purpose and stale docs are removed.
9. **Iterate in thin increments.** Work is delivered as small, working increments against a slice of the spec, not as a
   single end-to-end pass.
10. **Keep generation out of the catalog.** All customer documents and generated output stay in a separate engagement
    workspace, never in this catalog repository.

## Governance

- The constitution is **amended only via an ADR** in [`decisions/`](decisions/), so every rule change is deliberate and
  audited.
- Amending the constitution is a team change: bump the **team version** and record it in
  [`team-manifest.md`](team-manifest.md) and [`../CHANGELOG.md`](../CHANGELOG.md) (see
  [`versioning.md`](versioning.md)).
- When a rule and a more detailed document appear to conflict, the constitution states the intent; fix the detailed
  document to agree with it (or amend the constitution by ADR).
