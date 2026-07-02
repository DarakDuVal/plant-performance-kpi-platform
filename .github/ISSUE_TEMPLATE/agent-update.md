---
name: Update existing agent
about: Improve or correct an existing agent's prompt, skills, or examples
title: "[AGENT] Update "
labels: agent-update
assignees: ""
---

## Agent being updated

- **Agent file**: <!-- e.g. engineering/senior-software-developer.md -->
- **Current version**: <!-- e.g. 1.0.0 -->
- **Proposed new version**: <!-- e.g. 1.1.0 -->

## Type of change

- [ ] PATCH — wording, typo, or formatting fix (no behavior change)
- [ ] MINOR — new skill, tool, example, or backward-compatible guidance
- [ ] MAJOR — role scope, responsibilities, or delivery loop position changes

## Description

<!-- What is changing and why? -->

## Checklist

- [ ] Agent `.md` file updated with the new content
- [ ] `version` field in the agent's frontmatter bumped
- [ ] `docs/team-manifest.md` updated with the new agent version
- [ ] Team version bumped in `docs/team-manifest.md` (PATCH / MINOR / MAJOR as appropriate)
- [ ] Change recorded in `CHANGELOG.md`

See `docs/versioning.md` for the full update policy.
