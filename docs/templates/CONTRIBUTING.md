# Contributing

Thanks for contributing. This guide gets you from clone to first pull request. Adapt it to your workspace's stack and
tools.

## Quick start (time-to-first-PR)

```bash
# 1. Set up the toolchain, dependencies, and Git hooks in one step.
make setup

# 2. Run the fast inner loop while you work.
make test
make lint
```

If there is no `Makefile`, document the equivalent commands here.

## Branching and commits

- Branch from `main`: `git switch -c <type>/<short-description>`.
- Use [Conventional Commits](https://www.conventionalcommits.org/) for messages (for example `feat: add user search`).
- Keep changes small and focused; one logical change per pull request.

## Before you open a pull request

- [ ] Tests pass and coverage stays at or above the project threshold.
- [ ] Linters and formatters pass (run them via the pre-commit hooks).
- [ ] No secrets are committed; real `.env` files stay out of Git.
- [ ] Docs updated when behavior or structure changes.
- [ ] The pull request description explains the change and links the requirement.

## Code review

Open a pull request and request review from the relevant `CODEOWNERS`. Address review feedback by pushing follow-up
commits to the same branch.
