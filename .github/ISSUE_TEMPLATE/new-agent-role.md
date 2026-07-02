---
name: Onboard new agent role
about: Add a new agent to the team roster following the versioning process
title: "[AGENT] Onboard "
labels: agent-onboarding
assignees: ""
---

## Agent details

- **Agent name** (kebab-case): <!-- e.g. data-engineer -->
- **Department folder**: <!-- engineering / product / testing / marketing / design / studio-operations -->
- **Starting version**: `1.0.0`

## Role summary

<!-- What is this agent's primary responsibility? Where does it sit in the delivery loop? -->

## Delivery loop position

<!-- Which step(s) does this agent participate in? What does it receive and what does it produce? -->

## Rationale

<!-- Why is this agent being added now? What gap does it fill? -->

## Checklist

- [ ] New agent `.md` file created in the correct department folder with `version: 1.0.0`
- [ ] Agent added to `docs/agent-catalog.md`
- [ ] Agent added to `docs/delivery-loop.md` (if it participates in the loop)
- [ ] Agent added to `docs/team-manifest.md`
- [ ] Team version bumped (MAJOR) in `docs/team-manifest.md`
- [ ] Change recorded in `CHANGELOG.md`
- [ ] PR opened with the `agent-onboarding` label

See `docs/versioning.md` for the full onboarding policy.
