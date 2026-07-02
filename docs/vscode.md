# Using the agents in VS Code

This catalog is optimized for use with **GitHub Copilot in Visual Studio Code**. There are two pieces:

1. **Repository instructions** — `.github/copilot-instructions.md` teaches Copilot the conventions of this repository
   (agent file format, required frontmatter, kebab-case naming, the versioning workflow, and the rule that generated
   delivery output never lands in this catalog). VS Code applies these automatically whenever you use Copilot Chat in
   this repository, so any agent you run here follows the house rules.

2. **Custom chat modes** — every agent role is also published as a VS Code custom chat mode under `.github/chatmodes/`.
   This lets you pick a role (for example `senior-software-developer` or `requirements-engineer`) straight from the
   **Chat mode** dropdown in the Copilot Chat view.

## Selecting an agent in VS Code

1. Open this repository in VS Code with the GitHub Copilot and Copilot Chat extensions installed.
2. Open the Copilot Chat view.
3. Open the **Chat mode** dropdown (it usually shows _Ask_ / _Edit_ / _Agent_).
4. Choose the role you want — each `.github/chatmodes/<name>.chatmode.md` file appears as a selectable mode named after
   the agent.
5. Chat as usual. The agent's role narrative drives its behavior, and its `tools` list controls which Copilot tools it
   may use.

Each chat mode file declares the VS Code tools the role is allowed to use, mapped from the catalog `tools` field:

| Catalog tool         | VS Code tool  |
| -------------------- | ------------- |
| `Read`               | `codebase`    |
| `Grep`, `Glob`       | `search`      |
| `Write`, `MultiEdit` | `editFiles`   |
| `Bash`               | `runCommands` |
| `WebSearch`          | `fetch`       |

## Keeping the chat modes in sync

The department `.md` files remain the **single source of truth**. The chat mode files are generated from them, so do not
edit files in `.github/chatmodes/` by hand. After you add, remove, or edit an agent, regenerate the chat modes:

```bash
node scripts/generate-vscode-chatmodes.mjs
```

To verify that the committed chat modes match the agent files (useful in CI or a pre-commit check), run:

```bash
node scripts/generate-vscode-chatmodes.mjs --check
```

The `--check` flag exits with a non-zero status if any chat mode is out of date.

## Using the agents outside this repository

To use these chat modes in another project, copy the relevant `.github/chatmodes/<name>.chatmode.md` files into that
project's `.github/chatmodes/` folder, or place them in your VS Code user profile so they are available across all
workspaces.
