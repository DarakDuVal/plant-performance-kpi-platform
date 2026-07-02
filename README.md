# get-IT-done

A clone-and-go framework of reusable AI agent roles that work together to deliver
**your** software and IT projects.

## Purpose

This repository is a **template**: clone or copy it into your workspace, point the
agents at your software project, and they run a complete, spec-anchored delivery
loop against it. The agents are grouped by department so the catalog stays easy to
expand, review, and customize. Everything here describes *how the agents work* — it
is not the project they work on. Keep all generated project output in a separate
engagement workspace, never in this catalog.

The agents run as an **iterative, spec-anchored agile SDLC**, not a one-time pass: each iteration delivers a thin, working increment against a slice of the requirements spec, the spec stays the living source of truth (no drift), and a constitution of invariant rules plus a durable project-context artifact are carried into every step. See [`docs/delivery-loop.md`](docs/delivery-loop.md).

## Directory structure

```text
get-IT-done/
├── .github/
│   ├── chatmodes/            # VS Code custom chat modes (generated)
│   └── copilot-instructions.md
├── data/                     # data-engineer, data-analyst, database-administrator
├── delivery-management/      # project-delivery-manager, agile-delivery-lead, engineering-manager
├── design/
│   ├── architecture.md           ← template for YOUR project's Mermaid diagrams
│   └── ux-and-design-expert.md
├── docs/
│   ├── decisions/
│   │   ├── README.md             ← how to record YOUR project's ADRs
│   │   └── ADR-000-template.md   ← ADR template (no framework ADRs kept here)
│   ├── agent-catalog.md
│   ├── communication-standard.md
│   ├── constitution.md           ← invariant rules carried into every step
│   ├── context-template.md       ← project context / steering (memory bank)
│   ├── delivery-loop.md
│   ├── quality-standards.md      ← Minimum quality bar for every workspace
│   ├── repo-setup.md             ← Repository setup standard (DX + UX)
│   ├── spec-authoring-guide.md   ← AI-consumable, reviewable specs
│   ├── task-breakdown-template.md ← per-iteration task decomposition
│   ├── team-manifest.md
│   ├── templates/                ← Copy-ready setup stub files
│   ├── versioning.md
│   └── vscode.md
├── engineering/              # architect, senior dev, language + mobile + AI devs, devops
├── marketing/                # marketing-and-communications, sales-engineer, social-media
├── product/                  # requirements-engineer, business-analyst, product-manager, technical-writer
├── security/                 # security-engineer, compliance-and-data-protection-expert
├── studio-operations/        # IT, support, finance, purchasing, people, legal, success
├── testing/                  # unit, integration/systems, load/performance, acceptance experts
├── scripts/
│   └── generate-vscode-chatmodes.mjs
├── .markdownlint.yml             ← Markdown lint configuration
├── .yamllint.yml                 ← YAML lint configuration
├── CHANGELOG.md
├── LICENSE
├── SETUP.md
└── README.md
```

For the full, authoritative list of agent roles and their responsibilities, see
[`docs/agent-catalog.md`](docs/agent-catalog.md).

## Included agent roles

The catalog ships roles across nine departments — **engineering**, **delivery
management**, **product**, **data**, **security**, **testing**, **studio
operations**, **marketing**, and **design** — covering architecture, language and
mobile development, DevOps, requirements, data, security and compliance, testing,
operations, go-to-market, and UX.

See [`docs/agent-catalog.md`](docs/agent-catalog.md) for the full list of roles and
their responsibilities, and [`docs/team-manifest.md`](docs/team-manifest.md) for the
current versioned roster.

## Engineering setup and GitHub Octoverse 2025

The engineering roles reflect findings from the [GitHub Octoverse 2025 report](https://github.blog/news-insights/octoverse/octoverse-a-new-developer-joins-github-every-second-as-ai-leads-typescript-to-1/):

- **AI is now baseline.** A dedicated AI tools and LLM developer role embeds AI capabilities, and every role treats AI-assisted code as something to review and verify.
- **TypeScript leads.** The JavaScript developer defaults to TypeScript, reflecting its rise to the most-used language on GitHub and its fit with AI-assisted development.
- **Typed, verifiable code.** Backend roles emphasize typed contracts and clear interfaces so both humans and AI agents can extend code safely.
- **Rapid growth and scale.** The senior infrastructure architect plans environments, deployment, and monitoring that absorb fast change and support AI-enabled services.

## Agent file format

Each agent is defined as a standalone markdown file with:

- YAML frontmatter for `name`, `version`, `description`, `color`, and `tools`
- a role narrative describing background and operating style
- responsibilities, skills, and collaboration guidance
- examples showing when the agent should be used

## Versioning and team updates

The agent setup is versioned so it stays clear which agents — and which versions — resolved a given customer request, and so the team can change over the life of a long-running project (associates leaving and onboarding, much like a real company).

- **Per-agent versioning.** Every agent file carries a `version` in its frontmatter and follows [Semantic Versioning](https://semver.org/).
- **Team manifest.** `docs/team-manifest.md` is a versioned snapshot of the whole roster (every agent and its version) under a single **team version**. Record the team version against a customer request — at intake in the delivery loop — to capture exactly which setup resolved it.
- **Changelog.** `CHANGELOG.md` tracks how the team setup evolves over time.
- **Updating the team.** `docs/versioning.md` defines the onboarding/offboarding process and how to bump versions, so mid-project team changes stay traceable and never silently rewrite the setup behind already-delivered work.

## How to use

1. Review the department folders and adjust role descriptions to match your company.
2. Copy the relevant agent files into your preferred agent runtime.
3. Extend the prompts, tools, and examples as your company processes mature.
4. Use `docs/agent-catalog.md` as the high-level reference for ownership and collaboration.
5. Follow `docs/delivery-loop.md` to run the agents as an **iterative, spec-anchored agile loop**, chaining each step's output into the next. Each iteration delivers a thin, working increment against a slice of the spec; the requirements spec stays the living source of truth, and the **constitution** (`docs/constitution.md`) and a per-engagement **project context** (`docs/context-template.md`) are carried into every step. Design is decomposed into traceable tasks (`docs/task-breakdown-template.md`), and validation enforces a **spec-conformance gate**. Each agent file also documents its own position in the loop.
6. Keep agent-to-agent communication and code minimal, exact, and clear per `docs/communication-standard.md`, even when the customer request is wordy or imprecise.
7. Record the **team version** from `docs/team-manifest.md` against each customer request, and follow `docs/versioning.md` when updating the team. See `CHANGELOG.md` for the history of team changes.
8. Read `docs/quality-standards.md` and complete the quality setup checklist in `SETUP.md` for every new workspace. This establishes TDD/BDD, coverage gates, linting, ADRs, and requirements templates from the first commit.
9. Apply `docs/repo-setup.md` — the repository setup standard covering both developer experience (DX) and user experience (UX) — so every new repo or migration starts with a one-command bootstrap, reproducible environment, pre-commit hooks, and clear UX criteria. Copy-ready starter files live in `docs/templates/`.

## Using the agents in VS Code

This repository is optimized for **GitHub Copilot in VS Code**: it ships
repository instructions (`.github/copilot-instructions.md`) and a custom chat
mode for every agent role (`.github/chatmodes/`), so you can pick a role straight
from the Copilot Chat mode dropdown. See `docs/vscode.md` for details and how to
regenerate the chat modes.

## License

This project is released under the MIT License so you can reuse, adapt, and build on it as the backbone of your company.
