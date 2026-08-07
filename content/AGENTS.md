# Vault writing rules

This directory is a private Obsidian vault. This guideline is public; every
other note remains untracked and is synchronized separately.

## Before writing

- Search with QMD and read only the relevant results.
- Update an existing note instead of creating a duplicate.
- Create a note only for knowledge that will remain useful beyond the current
  conversation. Do not save raw transcripts or temporary reasoning.
- Keep retrieval and edits within the task's scope unless cross-scope context is
  necessary.

## Metadata

Start each note with two properties:

```yaml
---
type: decision
scope: example-scope
---
```

- Use one of these types: `project`, `decision`, `how-to`, `reference`, `note`,
  or `log`.
- Use a short, stable scope that identifies the note's context or ownership.
- Do not add lifecycle status. A note is current while it exists; update or
  delete it when it is no longer valid.
- Add `last_verified: YYYY-MM-DD` only when the information can become stale.
- Avoid tags and additional properties unless they solve a recurring retrieval
  need.

## Writing

- Use a specific H1 title followed by a one- or two-sentence summary.
- Keep one primary subject or outcome per file and use explicit headings.
- Prefer precise, searchable terms over shorthand that depends on conversation
  context.
- Link related notes with `[[Obsidian links]]` when the relationship is useful.
- Cite sources for external claims and record when changeable facts were last
  verified.
- Label assumptions, hypotheses, and unresolved questions explicitly.
- Never store credentials, secret values, or unnecessary sensitive data.
- Use descriptive lowercase kebab-case filenames. Prefix dated logs with
  `YYYY-MM-DD-`.

## Type-specific structure

Use only the sections that add value.

### Project

```markdown
## Outcome
## Current state
## Next actions
## Decisions
## Related
```

### Decision

```markdown
## Context
## Decision
## Consequences
## Alternatives
## Related
```

### How-to

```markdown
## When to use
## Prerequisites
## Steps
## Verification
## Recovery
## Related
```

### Reference

```markdown
## Summary
## Details
## Sources
## Related
```

`note` and `log` are free-form beyond the shared writing rules.

## Maintenance

- Keep folders shallow and organize by scope only when it improves navigation.
- Update links when moving, renaming, or deleting notes.
- Do not create large taxonomies, generated indexes, or new conventions without
  a demonstrated need.
- Do not reorganize or rewrite unrelated notes as part of a focused task.
