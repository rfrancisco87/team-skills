---
name: design-system
description: How to express a design direction as an implementable, consistent system — design tokens, a component library, and a clean handoff to the Builder — in the Next.js + Tailwind + shadcn/ui + Framer Motion stack. Apply whenever turning a visual direction into tokens/components, maintaining UI consistency, or handing a design over for implementation. Use for any task about design tokens, style guides, component specs, or design-to-code handoff.
---

# Design System

A design is only real when it's implementable and consistent. Every project gets
its **own** token set — never share one project's look with another.

## Tokens are the source of truth

Express the direction as tokens, then derive everything from them. No one-off
values in components.

- **Colour** — semantic roles (surface, elevated, ink, muted, accent, accent-ink,
  border, success/warn/danger). Map to CSS variables and Tailwind theme config.
- **Type** — the chosen display/body/utility faces wired via `next/font`; a
  named type scale (display, h1–h4, body, small, caption) with weights,
  line-heights, and tracking.
- **Spacing** — one consistent scale; components use scale steps, not arbitrary
  px.
- **Radii, shadows, borders** — a small named set that matches the direction
  (a broadsheet look has different radii than a soft wellness look).
- **Motion** — named durations/easings; respect `prefers-reduced-motion`.

Wire tokens into `tailwind.config` / `globals.css` so the whole app inherits
them. Changing a token should change the app, not just one screen.

## Components: build on shadcn/ui, but don't ship it stock

shadcn/ui is the primitive layer, not the finished look — stock shadcn *is* the
AI-look. Re-theme it through the tokens so buttons, inputs, cards, dialogs carry
the project's direction. Document each component's variants and states (default,
hover, focus, active, disabled, loading, empty, error) and its responsive
behaviour. Keep the accessible semantics shadcn gives you.

## Style guide

Ship a single styleguide page (a route or a prototype) that renders the tokens
and every component in all states. It is the shared reference for the Designer,
the Design Reviewer, and the Builder, and the fastest way to catch drift.

## Handoff to the Builder

When a design is approved, the Builder receives, as an implementable package:

1. **Tokens** — the Tailwind config / CSS-variable file.
2. **Style guide** — the rendered components/states reference.
3. **Prototypes** — the page/component prototypes (HTML or React + Tailwind).
4. **UI acceptance criteria** — states, breakpoints, interactions, and empty/
   error cases, written so the Builder and the Design Reviewer can verify them
   objectively (this plugs into the normal issue acceptance-criteria contract).

The Builder implements from tokens and prototypes, not from a screenshot. The
Design Reviewer later checks the built UI against this package for drift (while
the implementation ticket is In Progress, before it goes to the human In Review
gate).
