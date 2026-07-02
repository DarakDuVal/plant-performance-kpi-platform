# Versioning and team updates

This document defines how the agent setup is versioned and how the team changes over time. It exists so that, for any
customer request, it is **clear which agent setup resolved it**, and so that long-running projects can **update the
team** (associates leaving and onboarding) in a controlled, traceable way.

Two things are versioned:

1. **Each agent** — an individual prompt definition (a single markdown file).
2. **The team** — the whole roster of agents and their versions at a point in time, captured in
   [`team-manifest.md`](team-manifest.md).

## Why version the agent setup

An agent's behavior comes from its prompt. When a prompt changes, the agent can behave differently, so the version of
the setup that handled a request is part of that request's audit trail. Recording the team version against an engagement
lets you answer later: _"Which exact agents, at which versions, produced this result?"_

## Agent versioning

Every agent file carries a `version` field in its YAML frontmatter and follows
[Semantic Versioning](https://semver.org/) (`MAJOR.MINOR.PATCH`):

- **MAJOR** — a change that meaningfully alters the agent's role, scope, or behavior (for example, removing a
  responsibility or changing its position in the delivery loop).
- **MINOR** — a backward-compatible capability or guidance addition (for example, a new skill, tool, or example).
- **PATCH** — a wording, typo, or formatting fix that does not change behavior.

Rules:

- Bump the agent's `version` in the same change that edits its prompt.
- Never reuse a version number for different content.
- A new agent starts at `1.0.0`.

## Team versioning (the manifest)

The team as a whole is versioned in [`team-manifest.md`](team-manifest.md). The manifest lists every active agent and
its current version, plus a single **team version** that identifies the roster as a snapshot.

The team version also follows Semantic Versioning:

- **MAJOR** — an agent is **onboarded** or **offboarded** (the roster changes), or an agent receives a MAJOR bump.
- **MINOR** — one or more agents receive a MINOR bump, with no roster change.
- **PATCH** — only PATCH-level agent changes, with no roster change.

Whenever any agent version changes or the roster changes, bump the team version and update the manifest and
[`../CHANGELOG.md`](../CHANGELOG.md) in the same change.

## Recording the team version on a customer request

The team version is the link between a customer request and the agent setup that resolved it. During the delivery loop
(see [`delivery-loop.md`](delivery-loop.md)):

1. At **intake**, record the current **team version** (from the manifest) in the engagement workspace — for example in
   the `01-intake.md` artifact.
2. Keep that recorded version with the engagement's outputs. It identifies the exact agent setup used.
3. If the team is updated **mid-engagement**, record the new team version at the point it is adopted, so the engagement
   history shows which setup produced which output.

Because the catalog repository is read-only during a run, the recorded version lives in the engagement workspace, never
back in this repository.

## Updating the team (onboarding and offboarding)

Long-running projects need the team to change, much like a real company where associates leave and new ones join. Use
this process:

### Onboarding a new agent

1. Add the agent's markdown file in the correct department folder, starting at `version: 1.0.0`.
2. Register the agent in [`agent-catalog.md`](agent-catalog.md) and, where it participates, in
   [`delivery-loop.md`](delivery-loop.md).
3. Add it to the roster in [`team-manifest.md`](team-manifest.md).
4. Bump the **team version** (MAJOR) and record the change in [`../CHANGELOG.md`](../CHANGELOG.md).

### Offboarding an agent

1. Remove the agent's markdown file (or move it out of the active roster).
2. Remove its entries from [`agent-catalog.md`](agent-catalog.md) and [`delivery-loop.md`](delivery-loop.md),
   reassigning any responsibilities.
3. Remove it from the roster in [`team-manifest.md`](team-manifest.md).
4. Bump the **team version** (MAJOR) and record the change in [`../CHANGELOG.md`](../CHANGELOG.md).

### Updating an existing agent

1. Edit the agent's prompt and bump its `version` per the rules above.
2. Update its version in [`team-manifest.md`](team-manifest.md) and bump the **team version** accordingly.
3. Record the change in [`../CHANGELOG.md`](../CHANGELOG.md).

Running engagements keep using the team version they recorded until they explicitly adopt a newer one, so a mid-project
team change never silently rewrites the setup behind already-delivered work.
