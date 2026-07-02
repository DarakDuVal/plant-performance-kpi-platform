# Copilot instructions for get-IT-done

This repository is a **catalog of reusable AI agent role definitions** for an
agentic software and IT company. It contains documentation and prompts — there is
no application code to build or run. Treat every change as a change to a prompt
library and keep the catalog clean, consistent, and reviewable.

## What lives here

- Department folders (`data/`, `delivery-management/`, `design/`,
  `engineering/`, `marketing/`, `product/`, `security/`,
  `studio-operations/`, `testing/`) each contain one markdown file per agent
  role.
- `docs/` holds the catalog, delivery loop, team manifest, and versioning policy.
- `.github/chatmodes/` holds VS Code custom chat modes generated from the agent
  role files (see `docs/vscode.md`).
- `CHANGELOG.md` tracks how the team setup evolves over time.

## Agent file format

Every agent role file is a standalone markdown file with:

- YAML frontmatter containing **all** of these required fields: `name`,
  `version`, `description`, `color`, `tools`.
- `version` must follow [Semantic Versioning](https://semver.org/) (`x.y.z`).
- `name` must be kebab-case and match the file name (without `.md`).
- A body with the role narrative, responsibilities, key capabilities,
  collaboration guidance, and a **Delivery loop** section describing the role's
  position in the loop (see `docs/delivery-loop.md`).

When adding or editing an agent, mirror the structure of the existing files in
the same department.

## Conventions to follow

- Keep agent role names kebab-case and group new agents by department.
- A GitHub Actions workflow (`.github/workflows/validate-frontmatter.yml`)
  validates the required frontmatter fields and the semver format on every pull
  request that touches an agent file. Make sure new or edited agent files pass it.
- When you add, remove, or update an agent, follow `docs/versioning.md`:
  1. Edit or add the agent `.md` file and bump its `version` frontmatter field.
  2. Update `docs/team-manifest.md` and bump the team version.
  3. Update `docs/agent-catalog.md` if roles or descriptions changed.
  4. Record the change in `CHANGELOG.md`.
- If you change the set of agents or their descriptions, also update the
  generated chat modes by running the generator described in `docs/vscode.md`.

## Important boundaries

- This repository is the **catalog**. Never commit customer documents or
  generated delivery output here — keep that work in a separate engagement
  workspace, as described in `docs/delivery-loop.md`.
- This project is documentation-only. Do not add build tooling, dependencies, or
  application code unless explicitly requested.
