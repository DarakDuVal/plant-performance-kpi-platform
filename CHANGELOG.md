# Changelog

All notable changes to the agent setup are recorded here. Changes are tracked
against the **team version** defined in [`docs/team-manifest.md`](docs/team-manifest.md).
See [`docs/versioning.md`](docs/versioning.md) for the versioning scheme and the
team-update (onboarding/offboarding) process.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/).

## [Unreleased]

### Changed

- Repurposed this repository from the `get-IT-done` template catalog into the
  **plant performance KPI platform** workspace. Rewrote `README.md` and `SETUP.md`
  to describe the web application (backend + database + browser frontend) and drop
  the "Use this template" provisioning framing, and updated
  `.github/copilot-instructions.md` so application code is expected here alongside
  the agent catalog.
- Tailored the repository as a **clone-and-go template** for the agents to apply
  to a real software project (not this catalog itself): reframed `README.md` and
  removed the external `DarakDuVal/agents` reference.
- Converted `design/architecture.md` into a template for the **project's** own
  Mermaid architecture diagrams instead of diagramming this catalog.

### Removed

- This framework's own Architecture Decision Records
  (`docs/decisions/ADR-001-quality-standards.md`,
  `docs/decisions/ADR-002-spec-anchored-sdlc.md`). The `docs/decisions/` directory
  now keeps only the ADR template plus a `README.md`, so real projects record
  their own decisions there. References to the removed ADRs were dropped from
  `README.md`, `docs/agent-catalog.md`, `docs/quality-standards.md`, and
  `docs/delivery-loop.md`.

### Added

- Web-app skeleton directories `backend/`, `frontend/`, and `database/`, each with
  a `README.md` placeholder describing its intended contents, plus a root
  `.gitignore` for the application stack.
- `docs/repo-setup.md` — repository setup standard that lists the items every
  new repo or migration should include before work starts, split into developer
  experience (DX) and user experience (UX) checklists, plus repository
  foundation, quality gates, security/supply chain, operations, and traceability.
- `docs/templates/` — copy-ready starter files for new workspaces:
  `editorconfig`, `env.example`, `gitattributes`, `pre-commit-config.yaml`,
  `CONTRIBUTING.md`, and `SECURITY.md`.
- DX/UX setup checklist in `SETUP.md` and cross-links to `docs/repo-setup.md`
  from `README.md` and `docs/quality-standards.md`.
- VS Code optimization: repository instructions
  (`.github/copilot-instructions.md`) and a generated custom chat mode for every
  agent role (`.github/chatmodes/`), so roles can be selected from the Copilot
  Chat mode dropdown.
- `scripts/generate-vscode-chatmodes.mjs` to generate the chat modes from the
  agent files, plus a CI check that they stay in sync.
- `docs/vscode.md` explaining how to use and regenerate the chat modes.

## [2.0.0]

### Added

- Onboarded 15 new agent roles (each starting at `1.0.0`), expanding the roster
  to 38 agents and introducing three new departments:
  - **Delivery management**: `project-delivery-manager`, `agile-delivery-lead`,
    `engineering-manager`.
  - **Security**: `security-engineer`, `compliance-and-data-protection-expert`.
  - **Data**: `data-engineer`, `data-analyst`, `database-administrator`.
  - **Engineering**: `software-developer-mobile`, `devops-release-engineer`.
  - **Product**: `product-manager`, `technical-writer`.
  - **Studio operations**: `people-and-talent-expert`,
    `legal-and-contracts-expert`, `customer-success-manager`.
- Generated VS Code chat modes for every new agent role
  (`.github/chatmodes/`).

### Changed

- `it-infrastructure-expert` now also covers internal IT support
  (helpdesk/sysadmin); bumped from `1.1.0` to `1.2.0`.
- `docs/delivery-loop.md` integrates the new coordinating, cross-cutting,
  implementation, deployment, documentation, and supporting roles.
- `docs/agent-catalog.md` adds the new departments and agents and updates the
  collaboration pattern.
- `.github/workflows/validate-frontmatter.yml` and
  `scripts/generate-vscode-chatmodes.mjs` now include the `data`,
  `delivery-management`, and `security` department folders.
- Team version bumped to `2.0.0` (MAJOR — roster change).

## [1.2.0]

### Added

- `docs/constitution.md` — invariant rules carried into every step of every
  iteration (spec-first, no drift, traceability, quality gates, least privilege),
  amendable only via ADR.
- `docs/context-template.md` — persistent project context / steering artifact
  (domain glossary, entities, integrations, prior decisions, non-goals, lessons),
  distinct from the per-iteration spec.
- `docs/task-breakdown-template.md` — per-iteration task list decomposing design
  and the spec slice into small, ordered, requirement-traceable tasks.
- `docs/spec-authoring-guide.md` — guidance for authoring AI-consumable, reviewable
  specs (atomic, unambiguous, testable; anti-bloat).
- `docs/decisions/ADR-002-spec-anchored-sdlc.md` — records the decision to adopt a
  spec-anchored, iterative agile SDLC (over one-pass spec-first or spec-as-source).
- `docs/communication-standard.md` — agent-to-agent handoffs and code must stay
  minimal, exact, and clear to limit token use, even when the incoming human
  request is wordy or imprecise.

### Changed

- `docs/delivery-loop.md` rewritten as an **iterative, spec-anchored cycle**: adds a
  task-decomposition step (now step 5), renumbers downstream steps, adds loop-back
  and change-request entry points, a spec-reconciliation activity, a spec-conformance
  gate, the spec-vs-context distinction, and the constitution + context as standing
  inputs to every step (with a Mermaid flowchart).
- `design/architecture.md` — delivery-loop diagram replaced with the iterative
  flowchart; docs structure updated with the new files.
- `product/requirements-template.md` — added spec-revision tracking, per-requirement
  spec-status (`Specified`/`Implemented`/`Verified`/`Drifted`) and traceability
  columns, and an "intended consumers: humans + AI agents" note.
- `docs/quality-standards.md` — added "Spec is the source of truth (no drift)" and
  "Requirement traceability" sections.
- All 23 agent files bumped to `1.1.0`: each now references the constitution and
  project context; step numbers renumbered for the new task-decomposition step;
  developers receive tasks; the architect owns decomposition; the requirements
  engineer owns spec maintenance and drift reconciliation; the senior software
  developer flags spec drift; customer-support initialises context and confirms
  reconciliation; the business analyst maintains context; the unit and acceptance
  test experts tag tests with requirement IDs and assert the conformance gate.
- `README.md` and `SETUP.md` updated for the iterative loop, constitution, context,
  task breakdown, and spec-conformance gate.
- **Team version** bumped to `1.2.0` (capability additions, no roster change).
- Every agent now references the communication standard.

## [1.1.0]

### Added

- `docs/quality-standards.md` — minimum quality bar covering TDD/BDD, code
  coverage ≥ 80 %, per-language linting and formatting, unit testing, deployment
  descriptions, minimal documentation policy, Mermaid architecture diagrams, ADRs,
  and functional/non-functional requirements.
- `docs/decisions/ADR-000-template.md` — standard ADR template.
- `docs/decisions/ADR-001-quality-standards.md` — records the decision to adopt
  the quality standards baseline.
- `design/architecture.md` — Mermaid diagrams for agent catalog structure, delivery
  loop, repository layout, and CI quality enforcement.
- `product/requirements-template.md` — template for capturing functional and
  non-functional requirements with IDs, priorities, and acceptance criteria.
- `.markdownlint.yml` — Markdown linting configuration.
- `.yamllint.yml` — YAML linting configuration.
- Three new CI jobs in `.github/workflows/validate-frontmatter.yml`:
  `lint-markdown` (markdownlint-cli2), `lint-yaml` (yamllint), `lint-shell`
  (shellcheck). Workflow renamed to **Quality checks**.
- Quality setup checklist and updated GitHub Actions section in `SETUP.md`.
- Reference to `docs/quality-standards.md` in `README.md` and step 7 in "How to
  use".

## [1.0.0]

### Added

- Initial team roster of 23 agents across engineering, product, testing, studio
  operations, marketing, and design.
- `version` field in every agent's frontmatter, starting at `1.0.0`.
- Team manifest (`docs/team-manifest.md`) capturing the versioned roster snapshot.
- Versioning and team-update policy (`docs/versioning.md`).
