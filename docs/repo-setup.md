# Repository setup standard

Every new software repository — and every migration — repeats the same setup steps before the team can be productive.
This document is the **standard checklist** for that setup. Apply it from the first commit so each workspace starts with
a strong **developer experience (DX)** and a clear path to a good end-user **user experience (UX)**.

This standard **builds on**, and never duplicates, [`quality-standards.md`](quality-standards.md) (the minimum quality
bar) and the workspace steps in [`../SETUP.md`](../SETUP.md). Where an item is already covered there, this document
links to it rather than restating it.

Copy-ready starter files for several items live in [`templates/`](templates/) so a new workspace inherits them quickly.

## How to use this standard

1. Create the workspace (see [`../SETUP.md`](../SETUP.md)).
2. Work top-to-bottom through the checklists below, ticking each item.
3. Skip an item only with a recorded reason (an ADR in [`decisions/`](decisions/) when the choice is significant).
4. Confirm CI is green before accepting the first pull request.

## 1. Repository foundation (baseline files)

Every repository starts with the same baseline files so contributors and tools know where to look.

- [ ] `README.md` — purpose, quick start, and links to key docs.
- [ ] `LICENSE` — explicit license for reuse.
- [ ] `CHANGELOG.md` — follows [Keep a Changelog](https://keepachangelog.com/) and
      [Semantic Versioning](https://semver.org/).
- [ ] `.gitignore` — language-appropriate ignore rules (no build output, secrets, or local env files committed).
- [ ] `.gitattributes` — normalize line endings and mark generated/binary files (see
      [`templates/gitattributes`](templates/gitattributes)).
- [ ] `.github/CODEOWNERS` — review ownership per area (see [`../SETUP.md`](../SETUP.md)).
- [ ] `SECURITY.md` — responsible-disclosure contact and policy (see [`templates/SECURITY.md`](templates/SECURITY.md)).
- [ ] `CONTRIBUTING.md` — how to set up, branch, commit, and open a pull request (see
      [`templates/CONTRIBUTING.md`](templates/CONTRIBUTING.md)).
- [ ] `CODE_OF_CONDUCT.md` — expected behavior for contributors.
- [ ] Issue templates and a pull request template under `.github/` (this catalog already ships a reusable set — keep
      them as the standard).

## 2. Developer experience (DX)

DX is the time and friction between a new developer (or agent) joining and shipping their first reviewed change.
Minimize it.

- [ ] **One-command bootstrap.** A single documented entry point (a `Makefile` target such as `make setup`, or a
      task-runner script) that installs dependencies, sets up Git hooks, and verifies the toolchain. A new contributor
      runs one command and is ready.
- [ ] **Reproducible environment.** Provide a devcontainer (`.devcontainer/`) and/or a `docker-compose.yml` for local
      parity, and pin tool versions (for example `.tool-versions`, `.nvmrc`) so everyone runs the same stack.
- [ ] **Pre-commit hooks.** Run formatters and fast linters locally before commit to shorten the feedback loop and
      mirror the CI linters (see [`templates/pre-commit-config.yaml`](templates/pre-commit-config.yaml)).
- [ ] **Editor consistency.** Commit an `.editorconfig` (see [`templates/editorconfig`](templates/editorconfig)) and
      recommended VS Code workspace settings/extensions under `.vscode/`, aligned with the Copilot chat modes described
      in [`vscode.md`](vscode.md).
- [ ] **Fast inner loop.** Document the test, lint, format, and run commands behind one consistent interface, with
      watch/hot-reload guidance and seed/fixture data so the loop is quick.
- [ ] **Secrets and config.** Provide a `.env.example` (see [`templates/env.example`](templates/env.example)), document
      every environment variable, and never commit real secrets. Keep real `.env` files in `.gitignore`.
- [ ] **Onboarding doc.** A short developer-onboarding section (in `README.md` or `CONTRIBUTING.md`) that ties the above
      together and states the expected time-to-first-pull-request.

## 3. User experience (UX)

UX is the experience the end user gets. Even infrastructure work eventually serves a user, so capture UX intent early.

- [ ] **Design notes location.** Keep UX and design notes in `design/`, with at least one
      [Mermaid](https://mermaid.js.org/) diagram of structure or flow, kept current (see
      [`quality-standards.md`](quality-standards.md#architecture-diagrams)).
- [ ] **Accessibility baseline.** State an accessibility target (for example WCAG 2.2 AA) for any user-facing surface,
      and make it part of the definition of done.
- [ ] **UX acceptance criteria.** Trace user-facing behavior to requirements via
      [`../product/requirements-template.md`](../product/requirements-template.md) with BDD-style acceptance criteria.
- [ ] **User-facing change communication.** Maintain release notes or a user-facing changelog so UX changes are
      communicated to users.

## 4. Quality and verification gates

The quality bar is defined in [`quality-standards.md`](quality-standards.md). Setup must wire it in, not redefine it.

- [ ] TDD/BDD with unit-test coverage ≥ 80 %, enforced in CI.
- [ ] Per-language linting and formatting on every pull request.
- [ ] Branch protection on `main` requiring all CI jobs to pass.
- [ ] Conventional commits and a pull-request checklist.
- [ ] Coverage and language-specific lint jobs added to CI for the chosen stack (also flagged in
      [`../SETUP.md`](../SETUP.md)).

## 5. Security and supply chain

Security setup is part of DX: it should be automatic, not a manual chore.

- [ ] Dependency management with committed lockfiles.
- [ ] Automated dependency updates (Dependabot or Renovate).
- [ ] Secret scanning enabled on the repository.
- [ ] Static analysis / SAST (for example CodeQL) wired into CI.
- [ ] License and vulnerability checks in CI.
- [ ] `SECURITY.md` with a responsible-disclosure contact.

## 6. Operations and delivery

- [ ] Deployment description at `deployment/README.md` (or in the root `README.md`) covering environment, dependencies,
      environment variables, and rollback (see [`quality-standards.md`](quality-standards.md#deployment-description)).
- [ ] Infrastructure expressed as code (Terraform, Pulumi, Ansible, Kubernetes manifests, or similar).
- [ ] CI/CD pipeline definition version-controlled under `.github/workflows/` (or the platform equivalent).
- [ ] Observability baseline: logging, metrics, and a health-check convention noted for every new service.

## 7. Decisions and traceability

- [ ] Record significant setup decisions as ADRs in [`decisions/`](decisions/) using
      [`decisions/ADR-000-template.md`](decisions/ADR-000-template.md).
- [ ] Baseline requirements via [`../product/requirements-template.md`](../product/requirements-template.md).
- [ ] Record the **team version** from [`team-manifest.md`](team-manifest.md) at intake, per
      [`versioning.md`](versioning.md).

## Boundaries

This repository is the **catalog**. The tooling above describes the standard to apply in an **engagement workspace**,
not in this catalog repo. Never commit customer documents, generated delivery output, application code, or build tooling
into this catalog (see [`delivery-loop.md`](delivery-loop.md)).
