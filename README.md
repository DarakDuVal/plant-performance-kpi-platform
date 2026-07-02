# plant-performance-kpi-platform

A contained web application for tracking and reporting **plant performance KPIs**. The platform is made up of a backend
service with a database and a browser-based frontend, delivered together in this single repository.

> **Status: skeleton.** This repository is an empty scaffold that will be filled gradually. The application
> requirements, technology choices, and detailed design will be added as work progresses. Nothing about the stack is
> fixed yet; concrete decisions are recorded as [ADRs](docs/decisions/) once made.

## What this repository contains

This repository holds two things side by side:

1. **The application** — the plant performance KPI web app, developed under the skeleton directories below.
2. **An embedded agentic delivery team** — a catalog of reusable AI agent role definitions plus the process docs the
   agents follow to build the app. This is the framework carried over from the `get-IT-done` template; it stays here so
   the app can be developed with the agents rather than being copied elsewhere.

## Application structure

```text
plant-performance-kpi-platform/
├── backend/      # Backend service and API (+ database access)
├── frontend/     # Browser frontend
├── database/     # Database schema, migrations, and seed data
├── requirements/ # Functional & non-functional requirements, user stories, journeys
└── ...           # Agent catalog and delivery-process docs (see below)
```

Each application directory currently contains only a `README.md` placeholder describing its intended contents. Agents
fill these in over successive iterations.

## The agentic delivery team

The app is built by a team of AI agents grouped by department. Each role is a standalone markdown file under its
department folder (`engineering/`, `product/`, `data/`, `security/`, `testing/`, `design/`, `delivery-management/`,
`studio-operations/`).

- [`docs/agent-catalog.md`](docs/agent-catalog.md) — the roles and their responsibilities.
- [`docs/team-manifest.md`](docs/team-manifest.md) — the current versioned roster and team version.
- [`docs/delivery-loop.md`](docs/delivery-loop.md) — the iterative, spec-anchored delivery loop the agents run.
- [`docs/constitution.md`](docs/constitution.md) — invariant rules carried into every step.
- [`docs/quality-standards.md`](docs/quality-standards.md) and [`docs/repo-setup.md`](docs/repo-setup.md) — the quality
  bar and setup standard applied to the application code.

The repository is optimized for **GitHub Copilot in VS Code**: it ships repository instructions
(`.github/copilot-instructions.md`) and a custom chat mode for every agent role (`.github/chatmodes/`). See
[`docs/vscode.md`](docs/vscode.md) for details.

## How to work here

1. Add or refine requirements for the app using [`product/requirements-template.md`](product/requirements-template.md).
2. Run the agents through the iterative loop in [`docs/delivery-loop.md`](docs/delivery-loop.md), delivering a thin,
   working increment against a slice of the spec each iteration.
3. Grow the `backend/`, `frontend/`, and `database/` skeletons as those increments land, following
   [`docs/quality-standards.md`](docs/quality-standards.md) and [`docs/repo-setup.md`](docs/repo-setup.md).
4. Record significant decisions as ADRs in [`docs/decisions/`](docs/decisions/).

## License

Released under the [MIT License](LICENSE).
