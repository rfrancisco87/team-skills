---
name: ci-and-quality-gates
description: How continuous integration enforces quality so agent self-reports are never trusted — green CI is a precondition for review and merge. Apply whenever opening, reviewing, or merging a PR, or configuring a repo's checks. Use for any task touching CI config, PR checks, or the decision to approve or merge.
---

# CI & Quality Gates

Machine-verified, not agent-reported. An agent claiming "tests pass" is not
evidence; a green CI run is. **GitHub is the gate — the board's approval is
advisory.**

## Required checks on every PR

- `lint`, `typecheck`, `test` (with a coverage threshold), `build`.
- `gitleaks` secret scanning — required and blocking. Never rely on an agent
  remembering not to commit a secret.
- SAST (`semgrep` or CodeQL) — the Reviewer reads its output; it does not replace
  the Reviewer.

## Branch protection (main)

- All checks green required; ≥ 1 review; no direct push; no force-push; linear
  history; branches up to date before merge.
- `CODEOWNERS` makes the human a required reviewer on `/auth`, `/prisma`,
  `/payments`, infra, and CI paths.

## Rules for agents

- **Builder:** do not open a PR while local `lint`/`typecheck`/`test` fail. A new
  env var is documented in the PR and `.env.example`, never given a real value.
- **Reviewer:** a PR with red or missing checks is **not reviewable** — send it
  back before reviewing content. Read the gitleaks/SAST output as part of review.
- No agent bypasses checks. Only a human merges, and only when everything is green.
- Installs use `--ignore-scripts` (supply-chain safety).

## Reference workflow

```yaml
# .github/workflows/ci.yml
name: ci
on: [pull_request]
jobs:
  verify:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: pnpm/action-setup@v4
      - uses: actions/setup-node@v4
        with: { node-version: 22, cache: pnpm }
      - run: pnpm install --frozen-lockfile --ignore-scripts
      - run: pnpm lint
      - run: pnpm typecheck
      - run: pnpm test -- --coverage
      - run: pnpm build
      - uses: gitleaks/gitleaks-action@v2
```
