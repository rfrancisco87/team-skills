---
name: testing
description: Testing standards and patterns using Vitest and React Testing Library. Apply when writing or reviewing tests, or when verifying that a change meets its acceptance criteria. Use for any task that adds, changes, or evaluates test coverage — including verifying a PR before it is approved.
---

# Testing

Tests prove behavior and protect acceptance criteria. They are written with
Vitest + React Testing Library.

## Philosophy

- **Test behavior, not implementation.** Assert on what the user/consumer
  observes, not on internal state or private functions.
- Query the DOM by role, label, and text (RTL `getByRole`, `getByLabelText`,
  `findByText`) — not by test IDs unless there is no accessible alternative.
- A test that breaks on a harmless refactor is testing the wrong thing.

## Coverage rules

- **Every acceptance criterion maps to at least one assertion.** When verifying a
  PR, point to the test that proves each criterion.
- Cover the happy path **and** edge/error paths (empty, invalid, unauthorized,
  network failure).
- No snapshot-only coverage of logic. Snapshots are acceptable for stable
  presentational output, never as a substitute for asserting behavior.

## Structure

- Co-locate tests: `feature.test.ts(x)` next to the unit under test.
- One clear behavior per `it`/`test`; descriptive names ("redirects
  unauthenticated users to /login").
- Arrange–Act–Assert; keep setup readable.

## Mocking

- Mock at boundaries only: network, database, time, external SDKs.
- Use MSW (or the project's standard) for HTTP; avoid mocking your own modules.
- Don't over-mock — a test that mocks everything proves nothing.
- Use fake timers for time-dependent logic; keep tests deterministic (no real
  sleeps, no reliance on wall-clock).

## User interaction

- Use `@testing-library/user-event` for clicks, typing, etc., not raw
  `fireEvent`, so interactions match real browser behavior.
- `await` async queries and user events.

## Hard rules

- **Never change production code solely to make a test pass.** If a test fails,
  fix the cause or hand the issue back to the Builder.
- A criterion that cannot be tested as written is a finding: say so and propose
  how to make it testable.
- `pnpm test` must pass and be free of flaky timing before a PR is approved.
