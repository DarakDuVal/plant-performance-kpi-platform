# Setting up this workspace

This repository is the workspace for the **plant performance KPI platform**. It was created from the `get-IT-done`
agent-team template and now carries both the application skeleton and the embedded agentic delivery team that builds it.

Follow the steps below to get productive.

## 1. Confirm the team roster

- Review `docs/team-manifest.md` and keep only the agent roles this project needs. Remove rows (and the matching agent
  `.md` files) for roles you are not using.
- The **team version** in the manifest is referenced by every customer request, so keep it current.

## 2. Update `.github/CODEOWNERS`

Replace every `REPLACE_WITH_*` placeholder with real GitHub usernames or team slugs (`@your-org/team-name`):

```text
*                      @your-default-reviewer
engineering/           @your-tech-lead
product/               @your-product-lead
testing/               @your-qa-lead
marketing/             @your-marketing-lead
design/                @your-design-lead
studio-operations/     @your-ops-lead
```

## 3. Customise agent files

Open each agent `.md` file and adjust:

- **Role narrative** — tailor the background and operating style to this project.
- **Tools** — list only the tools your agent runtime actually provides.
- **Examples** — replace or extend the bundled examples with real workflows.
- **Delivery loop position** — update if you have changed the loop order.

Remove the entire file for any role this workspace does not need.

After changing which agents exist or editing their descriptions, regenerate the VS Code chat modes so they stay in sync
(see `docs/vscode.md`):

```bash
node scripts/generate-vscode-chatmodes.mjs
```

Then update `docs/agent-catalog.md` to match, and record the change in `CHANGELOG.md`.

## 4. Running the delivery loop

See `docs/delivery-loop.md` for the full step-by-step. The loop is **iterative and spec-anchored**: each iteration
delivers a thin, working increment against a slice of the requirements spec, and the spec stays the living source of
truth (no drift). Key rules:

- Develop the application in this repository under `backend/`, `frontend/`, and `database/`.
- Record the **team version** from `docs/team-manifest.md` at intake for every customer request.
- At intake, instantiate the **project context / steering** artifact (`00-context.md`, from `docs/context-template.md`)
  and carry it, plus the **constitution** (`docs/constitution.md`), into every step.
- Decompose design into a traceable task list (`docs/task-breakdown-template.md`) before implementation, and clear the
  **spec-conformance gate** in validation.
- Keep agent-to-agent communication and code minimal, exact, and clear per `docs/communication-standard.md`, even when
  the customer request is wordy.

## 5. Keeping the team up to date

When you add, remove, or update agents, follow the process in `docs/versioning.md`:

1. Edit or add the agent `.md` file and bump its `version` frontmatter field.
2. Update `docs/team-manifest.md` and bump the team version.
3. Record the change in `CHANGELOG.md`.
4. Regenerate the VS Code chat modes: `node scripts/generate-vscode-chatmodes.mjs`.
5. Open a pull request — the PR template will guide you through the checklist.

## 6. GitHub Actions

The workflow at `.github/workflows/validate-frontmatter.yml` runs on every pull request. It enforces the following
quality checks automatically — no setup required:

| Job                    | What it checks                                                                     |
| ---------------------- | ---------------------------------------------------------------------------------- |
| `validate-frontmatter` | Required frontmatter fields and semver in all agent `.md` files                    |
| `lint-markdown`        | Markdown style and structure via `markdownlint-cli2` (config: `.markdownlint.yml`) |
| `lint-yaml`            | YAML structure and style via `yamllint` (config: `.yamllint.yml`)                  |
| `lint-shell`           | Workflow + inline bash correctness via `actionlint` (includes ShellCheck)          |

As the application grows, extend this workflow with coverage and language-specific lint/test jobs for the chosen stack.

## 7. Quality standards

Read `docs/quality-standards.md` before contributing. It defines the minimum quality bar for the application:

- TDD / BDD practices and unit test coverage ≥ 80 %
- Per-language linting and formatting tools
- Deployment description requirements
- Documentation policy (minimal, consistent, no bloat)
- Mermaid architecture diagrams as code
- Architecture Decision Records (ADRs) in `docs/decisions/`
- Functional and non-functional requirements via `product/requirements-template.md`

### Quality setup checklist

- [ ] Read and adapt `docs/quality-standards.md` to the chosen language stack
- [ ] Work through `docs/repo-setup.md` — the repository setup standard covering both developer experience (DX) and user
      experience (UX)
- [ ] Adopt `docs/constitution.md` as the invariant rule set; amend only via ADR
- [ ] Instantiate `docs/context-template.md` as `00-context.md` per engagement
- [ ] Extend `.github/workflows/validate-frontmatter.yml` with coverage and language-specific lint jobs for the stack
- [ ] Add a **requirement-traceability CI job** that scans tests for referenced requirement IDs and fails if any `MUST`
      requirement lacks a linked test (enforces the spec-conformance gate)
- [ ] Copy `docs/decisions/ADR-000-template.md` as the basis for all future ADRs
- [ ] Create `docs/decisions/ADR-001-…` to record your first significant decision
- [ ] Copy `product/requirements-template.md` for each initiative
- [ ] Decompose design into tasks with `docs/task-breakdown-template.md` each iteration
- [ ] Verify `design/architecture.md` Mermaid diagrams match the actual architecture
- [ ] Confirm all CI jobs pass on the `main` branch before accepting the first PR

### Developer and user experience checklist

Apply `docs/repo-setup.md` from the first commit. Copy-ready starter files live in `docs/templates/`.

- [ ] Add a one-command bootstrap (for example a `make setup` target)
- [ ] Provide a reproducible environment (devcontainer and/or `docker-compose.yml`) with pinned tool versions
- [ ] Enable pre-commit hooks (`docs/templates/pre-commit-config.yaml`)
- [ ] Commit `.editorconfig` (`docs/templates/editorconfig`) and recommended `.vscode/` settings
- [ ] Add `.env.example` (`docs/templates/env.example`) and document every environment variable; keep real `.env` files
      out of Git
- [ ] Add `CONTRIBUTING.md`, `SECURITY.md`, and `.gitattributes` from `docs/templates/`
- [ ] State an accessibility target (for example WCAG 2.2 AA) for user-facing work
- [ ] Maintain user-facing release notes so UX changes are communicated
