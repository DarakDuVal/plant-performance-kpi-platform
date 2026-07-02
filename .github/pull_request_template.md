# Pull request checklist

## What changed

<!-- Briefly describe the change. -->

## Type of change

- [ ] New agent onboarded
- [ ] Existing agent updated
- [ ] Documentation only (delivery loop, catalog, versioning, README)
- [ ] Repository scaffolding or configuration
- [ ] Other: <!-- describe -->

## Agent changes (complete for every modified agent file)

| Agent file | Old version | New version |
| --- | --- | --- |
| <!-- e.g. engineering/senior-software-developer.md --> | <!-- 1.0.0 --> | <!-- 1.1.0 --> |

## Versioning checklist

- [ ] Each modified agent's `version` field is bumped in its frontmatter
- [ ] `docs/team-manifest.md` reflects the new agent version(s)
- [ ] Team version in `docs/team-manifest.md` is bumped (PATCH / MINOR / MAJOR)
- [ ] Change is recorded in `CHANGELOG.md`
- [ ] `docs/agent-catalog.md` updated if an agent was added, removed, or repositioned
- [ ] `docs/delivery-loop.md` updated if the agent's loop position changed

## Related issue

Closes #<!-- issue number -->
