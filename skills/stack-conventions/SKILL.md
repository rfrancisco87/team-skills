---
name: stack-conventions
description: The canonical tech stack, architecture patterns, and coding conventions for all Next.js projects (Horta, Terra, Reciply, Squad, Vault, and client work). Apply this whenever writing, reviewing, or planning ANY application code, so every agent produces consistent, idiomatic output. Use for any task that touches TypeScript, React, Next.js, Tailwind, shadcn/ui, Prisma, Neon, or project/file structure — even if the task doesn't explicitly mention them.
---

# Stack Conventions

The single source of truth for how code is written across all projects. If a
choice is not covered here, prefer the smallest, most idiomatic option and note
it for the Architect — do not invent a competing convention.

## Stack (non-negotiable defaults)

- **Framework:** Next.js 15+ (App Router only — no Pages Router).
- **Language:** TypeScript in `strict` mode.
- **Styling:** Tailwind CSS, utility-first.
- **Components:** shadcn/ui primitives.
- **Animation:** Framer Motion.
- **Icons:** Lucide.
- **Database:** Neon (PostgreSQL) via Prisma.
- **Package manager:** pnpm only (lockfile committed).
- **Testing:** Vitest + React Testing Library.

Do not introduce alternatives (styled-components, Yarn, Drizzle in a Prisma
project, etc.) without an explicit decision recorded by the Architect.

## Architecture

- **Server Components by default.** Add `"use client"` only for genuinely
  interactive components (state, effects, event handlers, browser APIs). Keep
  the client boundary as low in the tree as possible.
- **Typed data-access layer.** All database access goes through Prisma and a
  small typed query/service layer. Components and route handlers stay thin — no
  business logic embedded in JSX.
- **Server Actions / Route Handlers** validate input and check authorization
  before doing anything. Never trust client-provided IDs, roles, or flags.
- **Validation at boundaries.** Use `zod` (or equivalent) to parse and validate
  any external input — form data, query params, webhook bodies, API responses.
- **No raw, string-interpolated SQL.** Use Prisma or parameterized queries only.

## TypeScript rules

- No `any`. Use `unknown` + narrowing when the type is truly unknown.
- No non-null assertions (`!`) without a comment explaining why it is safe.
- Explicit return types on exported functions.
- No `// @ts-ignore` / `// eslint-disable` without an inline justification.
- Prefer discriminated unions and exhaustive `switch` over loose booleans.

## Styling

- Tailwind utilities first; extract a component before repeating long class
  strings.
- Use shadcn/ui primitives instead of hand-rolling buttons, dialogs, inputs.
- Framer Motion for animation; respect `prefers-reduced-motion`.
- Lucide for icons. No mixing icon libraries.

## Data & Prisma

- The Prisma schema is the source of truth.
- Use migrations (`prisma migrate`) for shared/prod environments — never
  `db push`. (See the `migrations-and-secrets` skill for the full procedure.)
- Index foreign keys and frequent filters.

## Internationalization

- **User-facing strings:** European Portuguese (pt_PT) for PT audiences.
- **Code, comments, identifiers, commit messages, PR text:** English.
- Never hardcode user-facing copy that should live in a locale file when the
  project already has i18n set up.

## Project structure

- Feature-oriented folders; co-locate component, test, and styles.
- `kebab-case` for files/folders, `PascalCase` for components, `camelCase` for
  functions/variables, `SCREAMING_SNAKE_CASE` for constants.
- Keep route handlers and server actions thin; push logic into the service layer.

## Quality gates (must pass before a PR is opened)

```
pnpm lint && pnpm typecheck && pnpm test
```

A change that fails any of these is not ready for review.
