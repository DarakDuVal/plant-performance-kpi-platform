# Quality standards

This document defines the minimum quality bar for every new repository or workspace that uses this setup. Apply these standards from the first commit to prevent standards drift and keep the codebase maintainable as it grows.

For the broader repository setup checklist — including developer experience (DX) and user experience (UX) items such as bootstrap scripts, reproducible environments, pre-commit hooks, and accessibility targets — see [`repo-setup.md`](repo-setup.md).

## Test-driven and behavior-driven development

- Write tests before or alongside implementation code (TDD).
- Use behavior-driven techniques (BDD / Given-When-Then) for acceptance criteria and integration tests so they read as human-understandable specifications.
- Every user-facing behavior must have at least one BDD-style acceptance test traceable to a requirement in `product/`.

## Code coverage

- Maintain **unit test coverage ≥ 80 %** on all non-trivial production code (excluding generated files, migrations, and configuration).
- Enforce the threshold in CI so a failing coverage gate blocks merge.
- Language-specific tooling:

| Language | Coverage tool | Enforcement |
| --- | --- | --- |
| Python | `pytest-cov` / `coverage.py` | `--cov-fail-under=80` |
| JavaScript / TypeScript | `c8` or `nyc` (via Jest/Vitest) | `--coverage --coverage-threshold` |
| Java | JaCoCo | `<minimum>` element in Maven/Gradle config |
| PHP | PHPUnit with `--coverage-text` | `<coverageThreshold>` in phpunit.xml |
| Bash / scripting | `bats-core` with `kcov` | Manual threshold assertion in CI |

## Linting and formatting

Run linting and formatting checks in CI on every pull request. Fail the build on violations.

| Language | Linter | Formatter |
| --- | --- | --- |
| Python | `ruff` | `ruff format` |
| JavaScript / TypeScript | `eslint` (flat config, `@typescript-eslint`) | `prettier` |
| Java | `checkstyle` | `google-java-format` |
| PHP | `phpstan` + `php-cs-fixer` | `php-cs-fixer` |
| Bash | `shellcheck` | `shfmt` |
| YAML | `yamllint` | — |
| Markdown | `markdownlint-cli2` | — |

Configuration files (`.eslintrc`, `.ruff.toml`, `phpstan.neon`, `checkstyle.xml`, etc.) live in the repository root and are committed alongside code.

## Unit testing

- Each class / module / function with business logic has a dedicated unit test file.
- Tests follow **Arrange-Act-Assert** structure.
- Tests are isolated: no shared mutable state, no file system or network access unless explicitly mocked.
- Test files mirror the source tree (e.g. `src/foo.py` → `tests/test_foo.py`).
- Language-specific frameworks: pytest (Python), Jest / Vitest (JavaScript/TypeScript), JUnit 5 (Java), PHPUnit (PHP), Bats (bash).

## Deployment description

- Every service or application includes a deployment description at `deployment/README.md` (or inline in the repo root `README.md`) that covers: target environment, dependencies, environment variables, and rollback procedure.
- Infrastructure is expressed as code (Terraform, Pulumi, Ansible, Kubernetes manifests, or similar).
- At minimum, provide a `docker-compose.yml` or equivalent for local environment parity.
- CI/CD pipeline definition lives in `.github/workflows/` (or the equivalent for the chosen platform) and is version-controlled.

## Documentation

- Keep documentation **consistent, concise, and minimal**. Every document has a single stated purpose; remove sections that duplicate other sources.
- Required documents per repository:
  - `README.md` — purpose, quick-start, links to key docs.
  - `CHANGELOG.md` — version-controlled change log following [Keep a Changelog](https://keepachangelog.com/).
  - `docs/quality-standards.md` — this file (copy into each workspace).
  - `docs/decisions/` — Architecture Decision Records (see below).
- Document only what the next contributor needs to understand and operate the system. Delete docs that are stale or no longer accurate.

## Architecture diagrams

- Use [Mermaid](https://mermaid.js.org/) for all architecture and flow diagrams so they live as code inside Markdown and stay version-controlled.
- Every repository includes at least one Mermaid diagram describing its overall structure or runtime flow (in `design/architecture.md` or inline in `README.md`).
- Diagrams are updated when the architecture changes; a PR that changes structure without updating the diagram is not complete.
- Preferred diagram types: `graph` for component/dependency maps, `sequenceDiagram` for runtime flows, `classDiagram` for domain models, `flowchart` for decision logic.

## Architecture Decision Records (ADRs)

- Use the ADR format in `docs/decisions/` to capture significant design decisions.
- Template: `docs/decisions/ADR-000-template.md`.
- Number ADRs sequentially (`ADR-001`, `ADR-002`, …).
- A decision is significant when it: affects multiple components, has non-obvious trade-offs, or will be costly to reverse.
- ADRs are immutable once accepted. Superseded decisions get status `Superseded by ADR-NNN` rather than being deleted.

## Functional and non-functional requirements

- Use `product/requirements-template.md` for every deliverable.
- Functional requirements describe **what** the system must do; non-functional requirements describe **how well** it must do it (performance, security, reliability, maintainability).
- Every requirement has a unique ID (`FR-NNN` / `NFR-NNN`), an acceptance criterion, and a priority (`MUST` / `SHOULD` / `COULD`).
- Requirements are baselined in the requirements spec (delivery loop step 3) and referenced by tests and ADRs.

## Spec is the source of truth (no drift)

The requirements spec is the **living source of truth** for the lifetime of an
engagement, not a one-time artifact.

- Behaviour changes update the **spec first, then the code** ("spec-first, then
  code"). A pull request that changes behaviour without updating the spec is **not
  complete** — the same rule the architecture diagrams follow.
- Each requirement carries a **spec status** (`Specified` / `Implemented` /
  `Verified` / `Drifted`). No iteration closes with a requirement left `Drifted`;
  drift is reconciled back into the spec at the close-the-loop step.
- New or changed needs enter as a **new spec revision** at the requirements step,
  never as an ad-hoc code edit.

## Requirement traceability

- Every `FR`/`NFR` maps to **at least one test**. Every `MUST` requirement maps to
  a passing acceptance test.
- Encode the **requirement ID in the test name or tag** (for example
  `test_FR_001_*`, or a `@FR-001` tag) so traceability is **machine-checkable**.
- The requirements spec records the design → test → code traceability per
  requirement (see [`../product/requirements-template.md`](../product/requirements-template.md)).
- Validation enforces a **spec-conformance gate**: release-readiness is "go" only
  when every `MUST` requirement has a passing, traceable test and no requirement is
  `Drifted` (see [`delivery-loop.md`](delivery-loop.md)).
