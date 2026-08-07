# Brain

Public bootstrap repository for a private Obsidian vault and local code
workspace. Everything under `content/` and `code/` is ignored by this Git
repository.

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
