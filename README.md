# Brain

Public bootstrap repository for a private Obsidian vault and local code
workspace. Vault notes under `content/` and projects under `code/` are ignored;
only their public bootstrap files are tracked by this Git repository.

## Install on macOS

Install Apple's Command Line Tools first if `git` is not already available:

```bash
xcode-select --install
```

Then install the repository and its managed tools:

```bash
git clone https://github.com/chainyo/brain.git "$HOME/brain"
cd "$HOME/brain"
curl https://mise.run | sh
export PATH="$HOME/.local/bin:$PATH"
mise trust --yes
mise install --yes
mise run install
exec zsh -l
```

Open `content/` as the Obsidian vault and let BYOC finish synchronizing it. Then
create the local QMD index and Codex MCP registration:

```bash
cd "$HOME/brain"
brain-qmd-setup
launchctl bootout "gui/$UID/dev.brain.qmd-refresh" 2>/dev/null || true
launchctl bootstrap "gui/$UID" \
  "$HOME/Library/LaunchAgents/dev.brain.qmd-refresh.plist"
```

The same command works from another clone location because it detects the brain
repository from the current directory. The LaunchAgent refreshes QMD every two
minutes after BYOC changes the vault. QMD indexes private Markdown notes while
excluding the public `AGENTS.md` guidance and local `.obsidian/` state. Check it
with:

```bash
launchctl print "gui/$UID/dev.brain.qmd-refresh"
qmd --index brain status
codex mcp get qmd
```

Run `brain-qmd-refresh` directly whenever an immediate index refresh is needed.
The VPS timer provides the equivalent automation on Linux.

## Install on a Debian or Ubuntu VPS

```bash
sudo apt-get update
sudo apt-get install -y ca-certificates curl git util-linux
git clone https://github.com/chainyo/brain.git "$HOME/brain"
cd "$HOME/brain"
curl https://mise.run | sh
export PATH="$HOME/.local/bin:$PATH"
mise trust --yes
mise install --yes
mise run install
exec bash -l
```

## Synchronize the private vault

The vault uses Obsidian BYOC on personal computers and an rclone crypt remote on
the VPS. Both clients read and write the same encrypted Cloudflare R2 prefix.
The public repository never contains vault notes, R2 credentials, or encryption
passwords.

1. Create a private R2 bucket and a token limited to that bucket.
2. Configure BYOC with the R2 S3 endpoint, bucket, and optional prefix. Enable
   its rclone-compatible encryption with Base64 filename encoding.
3. Run `rclone config` on the VPS. Create:
   - an S3 remote for R2; and
   - a crypt remote named `brain-vault` over the same bucket and prefix.
4. Give the crypt remote the same password as BYOC, leave the second password
   empty, and select Base64 filename encoding. Keep the generated rclone config
   private and outside this repository.
5. Let BYOC complete its first upload, then verify that rclone can decrypt the
   vault:

```bash
rclone lsf brain-vault:
```

Preview and perform the first two-way merge from the VPS:

```bash
brain-sync --init --dry-run
brain-sync --init
```

The successful initial sync creates the QMD collection and embeddings, then
registers a `qmd` MCP server in the current VPS user's Codex configuration.
Normal syncs preserve both sides of a conflict, limit unexpected deletions, and
refresh QMD only after the vault sync succeeds.

To use a different brain path or rclone remote, create a machine-local file:

```bash
mkdir -p "$HOME/.config/brain"
chmod 700 "$HOME/.config/brain"
printf '%s\n' \
  'BRAIN_ROOT=/path/to/brain' \
  'BRAIN_RCLONE_REMOTE=remote:path' \
  >"$HOME/.config/brain/sync.env"
chmod 600 "$HOME/.config/brain/sync.env"
```

Never put credentials or passwords in this environment file. They belong in
the private rclone configuration or a secret manager.

## Keep the VPS synchronized

Enable the user timer after the initial sync:

```bash
systemctl --user daemon-reload
systemctl --user enable --now brain-sync.timer
sudo loginctl enable-linger "$USER"
```

The timer runs every two minutes and continues after SSH disconnects. Check it
with:

```bash
systemctl --user status brain-sync.timer
journalctl --user -u brain-sync.service -n 100
qmd --index brain status
codex mcp get qmd
```

Run `brain-qmd-setup` once for every VPS Unix user that needs its own QMD index
and Codex MCP registration. Only one user or service should run the rclone sync
timer for a shared vault. Additional users can keep their independent indexes
current without starting another vault sync:

```bash
systemctl --user enable --now brain-qmd-refresh.timer
```

The brain files are independent of a ChatGPT account. Codex authentication,
MCP configuration, and QMD indexes remain per VPS Unix user; they are never
stored in R2 or this repository.

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

The tracked Mise lockfiles resolve the readable major and `latest` tool targets
to tested versions and download checksums for macOS ARM64 and Linux x64. Update
them intentionally with `mise lock` when refreshing the managed toolchain.

## Check

```bash
cd "$HOME/brain"
mise run check
```
