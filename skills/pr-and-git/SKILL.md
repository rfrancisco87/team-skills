---
name: pr-and-git
description: Git branch, commit, and pull-request conventions for every code change. Apply whenever creating branches, committing, or opening a PR, so history stays clean, reviewable, and no secret is ever committed. Use for any task that ends in a commit or a pull request, even small ones.
---

# Git & PR Conventions

Every code change ships as a small, reviewable pull request on a feature branch.
Nothing is committed directly to `main`.

## Branches

- Branch from up-to-date `main`.
- Naming: `feat/<issue-id>-<slug>`, `fix/<issue-id>-<slug>`,
  `chore/<slug>`, `docs/<slug>`, `refactor/<slug>`.
- One logical change per branch. If a branch grows past ~400 changed lines,
  split it.
- Never commit to `main`. `main` is protected; agents open PRs only.

## Commits

- Conventional Commits: `type(scope): summary` in the imperative, in English.
  - Types: `feat`, `fix`, `chore`, `docs`, `refactor`, `test`, `perf`, `build`.
- Small, atomic commits that each leave the tree in a working state.
- No "wip", "fix typo x5", or noise commits in the final history — squash if
  needed.

## Pull request template

```
## Summary
<what changed and why, 1–3 sentences>

## Acceptance criteria
- [ ] criterion → where/how it is satisfied
- [ ] ...

## Testing
<what was run: pnpm lint / typecheck / test, plus any manual checks>

## Risk & rollback
<migrations? breaking changes? how to revert>

## Notes
<anything the reviewer should know; [TO CONFIRM] items>
```

- Link the PR to its issue.
- Keep PRs small and focused. A reviewer should be able to read it in one sitting.

## Secrets — hard rules

- Never commit `.env`, API keys, tokens, passwords, connection strings, or
  certificates.
- Keep `.env.example` updated with variable **names only** (no values).
- If you add a new env var, document it in the PR and in `.env.example`.
- Never paste secret values into commit messages, PR descriptions, comments, or
  logs. If you discover a committed secret, treat it as an incident: flag it and
  assume it must be rotated.

## Merge policy

- Agents do **not** merge. A human merges after review approval.
- No force-push to shared branches.
- Rebase your branch on `main` before requesting review if it has drifted.
