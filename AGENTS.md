# AGENTS.md

This repository is public. Treat every tracked file as internet-visible.

## Repository boundaries

- `content/` is the only knowledge directory and is the Obsidian vault.
- Everything inside `content/` is private, synchronized separately, and ignored
  by Git except for `content/.gitkeep`.
- `code/` contains independently cloned Git repositories and is ignored by this
  repository except for `code/.gitkeep`.
- Treat every direct child of `code/` as a separate repository and run Git
  commands from inside that child repository.
- `chezmoi/` contains public, generic Chezmoi source state.
- `mise.toml` contains public tool versions and repeatable setup tasks.
- Do not add tracked knowledge notes, Markdown templates, generated indexes, or
  additional vault directories.

## Safety

- Never commit personal information, company information, tokens, secrets,
  credentials, private endpoints, hostnames, account IDs, or machine state.
- Never copy content from `content/`, `code/`, sibling repositories, connected
  accounts, or the home directory into tracked files.
- Examples must use public repository URLs or obvious placeholders.
- Configuration must obtain credentials from the environment or a secret
  manager; no real values belong in this repository.
- Before completing a change, inspect `git status --short`, verify ignore rules,
  and review every file Git would add.

## Common rules

Apply these rules here and under `code/` unless local guidance is stricter.

- Use [Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/#specification)
  for every commit and pull request title, including documentation and
  configuration changes. Keep each change focused.
- Use `uv` exclusively for Python environments, dependencies, locking, commands,
  and publishing. Commit `uv.lock` for reproducible projects.
- Prefer the smallest clear change that fixes the root cause. Avoid speculative
  abstractions, compatibility layers, dependencies, and fallbacks.
- Test behavior and contracts, not incidental markup, CSS, or implementation
  details. Run relevant tests, linting, type checks, and builds before committing;
  report anything not run.
- Keep reviews casual, concise, and actionable: state the problem, its
  non-obvious impact, and a concrete fix.
- Read local guidance, use repository-native commands, preserve unrelated
  changes, and never edit generated files manually.
- Use isolated branches or worktrees for implementation and do not broaden the
  requested scope without agreement.
- Keep documentation and examples aligned with shipped behavior.
