# AGENTS.md

This repository is public. Treat every tracked file as internet-visible.

## Repository boundaries

- `content/` is the only knowledge directory and is the Obsidian vault.
- Vault notes inside `content/` are private, synchronized separately, and
  ignored by Git. Only `content/.gitkeep` and the public writing rules in
  `content/AGENTS.md` are tracked.
- Read `content/AGENTS.md` before creating, updating, moving, or deleting vault
  notes.
- `code/` contains independently cloned Git repositories and is ignored by this
  repository except for `code/.gitkeep`.
- Treat every direct child of `code/` as a separate repository and run Git
  commands from inside that child repository.
- Never create a worktree for this bootstrap repository. Use worktrees only in
  the independent code repositories that need them.
- `chezmoi/` contains public, generic Chezmoi source state.
- `mise.toml` contains public tool versions and repeatable setup tasks.
- Do not add other tracked knowledge notes, Markdown templates, generated
  indexes, or additional vault directories.

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
- When asked to commit, also push the commit unless explicitly told otherwise.
- Assign every pull request created on the user's behalf, including drafts, to
  the user unless explicitly instructed otherwise. When authenticated as the
  user, use `gh pr create --assignee @me` or
  `gh pr edit <pr-url> --add-assignee @me`. If using a bot or service account,
  resolve the user's GitHub login instead of assigning the bot. Verify the
  assignment and report any failure.
- Use `uv` exclusively for Python environments, dependencies, locking, commands,
  and publishing. Commit `uv.lock` for reproducible projects.
- Prefer the smallest clear change that fixes the root cause. Avoid speculative
  abstractions, compatibility layers, dependencies, and fallbacks.
- Test behavior and contracts, not incidental markup, CSS, or implementation
  details. Run relevant tests, linting, type checks, and builds before committing;
  report anything not run.
- Before every commit, run
  `kingfisher scan . --staged --quiet --redact --no-validate --no-update-check`
  from the target repository and resolve every finding.
- Keep reviews casual, concise, and actionable: state the problem, its
  non-obvious impact, and a concrete fix.
- Read local guidance, use repository-native commands, preserve unrelated
  changes, and never edit generated files manually.
- Search private knowledge with `brain-qmd` (or the configured `qmd` MCP
  server) before recursively reading `content/`, and retrieve only the relevant
  documents. Never use bare `qmd`; its upstream default is a separate index
  named `index`, not this repository's `brain` index.
- Use isolated branches or worktrees for implementation in code repositories
  and do not broaden the requested scope without agreement.
- Keep documentation and examples aligned with shipped behavior.

## Linear

Use these rules for work tracked in Linear, here and in the independent code
repositories. Follow the relevant team's current Linear guide and local rules.

- Consult Linear before planning or changing tracked work. Search for existing
  issues, milestones, and projects before creating records.
- Maintain tracking for agreed work as part of the task. Create missing issues
  within the authorized scope and update existing records instead of duplicating
  them. Keep unrelated backlogs outside the change.
- Organize delivery under an existing project and a milestone with a clear
  outcome. Agree new projects with the team before creating them.
  Use parent issues for substantial tasks and linked sub-issues for
  bounded implementation or verification work. Keep small steps in checklists.
- Set the project, milestone, and parent on sub-issues. Record blocking and
  related work with Linear relationships, including dependencies across repos.
- Confirm the project lead and one delivery assignee for each issue. Keep these
  responsibilities distinct. Use agreed owners; resolve unknown ownership with
  the requester. Follow local rules for milestone ownership and agent delegation.
- Write issues with an outcome, scope, source references, and acceptance checks.
  Apply the team's existing priority and label conventions for useful filtering.
  Add target or due dates only when a real deadline has been agreed.
- Track blocking decisions with an owner. Reference the applicable PRDs and
  ADRs, and record new technical decisions in the team's established ADR system.
- Update status, blockers, and meaningful progress as work proceeds. Link PRs
  and verification evidence. Complete issues only after their acceptance checks
  pass; complete parent work only after all required child work is complete.
- Keep Linear authoritative for delivery status, ownership, and dates. Keep
  requirements and decisions in their established documentation systems, with
  links between them and Linear. Follow the team's cycle and progress-update
  cadence without inventing commitments.
- Make repository READMEs identify the associated Linear projects. Make new or
  changed capability documentation identify relevant milestones or issues.
  Include issue identifiers and URLs in PR descriptions and link PRs from Linear.
  Keep these references current without copying live task lists into docs.
- Respect each destination's confidentiality rules. In this public bootstrap
  repository, keep instructions generic and use placeholders for private links.
  Never copy workspace details or private tracking records into tracked files.
  Keep private tracking links and identifiers out of public PR descriptions too.
- Report unavailable Linear access and any updates that could not be saved.
  Do not claim tracking changes succeeded without verifying the result.
