# Brain

Public bootstrap repository for a private Obsidian vault and local code
workspace. Vault notes under `content/` and projects under `code/` are ignored;
only their public bootstrap files are tracked by this Git repository.

## Install on a Debian or Ubuntu VPS

```bash
sudo apt-get update
sudo apt-get install -y ca-certificates curl git
git clone https://github.com/chainyo/brain.git "$HOME/brain"
cd "$HOME/brain"
curl https://mise.run | sh
export PATH="$HOME/.local/bin:$PATH"
mise trust --yes
mise install --yes
mise run install
exec bash -l
```

## Set up QMD

Mise installs QMD with Bun. From the repository root, register the private vault,
build its local search index, and expose it to Codex over MCP:

```bash
qmd collection add "$PWD/content" --name brain
qmd context add qmd://brain "Private Obsidian vault"
qmd embed
codex mcp add qmd -- qmd mcp
```

Run these commands after notes change significantly:

```bash
qmd update
qmd embed
```

## Clone a code project

```bash
cd "$HOME/brain/code"
git clone <repository-url>
```

## Update

```bash
cd "$HOME/brain"
git pull --ff-only
mise run install
```

## Check

```bash
cd "$HOME/brain"
mise run check
```
