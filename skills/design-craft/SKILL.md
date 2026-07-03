---
name: design-craft
description: How to create distinctive, intentional app and website designs with a fresh visual direction chosen for each specific project — never a generic, templated "AI look." Apply whenever designing or reshaping any UI: landing pages, app screens, marketing sites, dashboards, components. Use for any task involving visual direction, layout, typography, colour, or the look and feel of a product.
---

# Design Craft

Approach every project as the design lead at a studio whose work must never be
mistaken for a template. The client is paying for a distinctive point of view.
Make deliberate, opinionated choices specific to *this* brief, and take one real
aesthetic risk you can justify. A design that could be dropped onto an unrelated
product unchanged has failed.

## Ground the design in the subject first

Before any pixels, pin down: the concrete product/subject, its audience, the
single job of this screen or flow, the brand context, and the platform (web/app).
If the brief leaves these open, decide them and state your choice. Distinctive
choices come from the subject's own world — its materials, vocabulary, artifacts,
and feeling — not from a generic UI kit.

## Establish a direction (a token system) before building

Write this down as a DIRECTION plan and critique it *before* coding:

- **Colour** — 4–6 named hex values with roles (surface, ink, accent, etc.).
  A palette chosen for this brand, not a default.
- **Type** — a characterful display face used with restraint, a complementary
  body face, and a utility face for captions/data if needed. Set an intentional
  type scale (weights, sizes, spacing). Typography carries the personality of the
  page; it is not a neutral delivery vehicle. Do **not** reach for the same
  families you'd use on any other project (Inter-on-everything is a tell).
- **Layout** — a concept in one or two sentences plus an ASCII wireframe to
  compare options. The hero is a thesis: open with the most characteristic thing
  in the subject's world, in whatever form fits (headline, image, live demo,
  interactive moment).
- **Signature** — the single element this design is remembered by, embodying the
  brief. Spend your boldness here; keep everything around it quiet.

## Principles

- **Structure is information.** Numbering, eyebrows, dividers, and labels should
  encode something true about the content, not decorate it. Numbered markers
  (01/02/03) are only right when the content is genuinely a sequence.
- **Motion is deliberate.** A single orchestrated moment (a load sequence, a
  scroll reveal, a hover micro-interaction) lands harder than scattered effects.
  Often less is more — excess animation is itself a mark of AI-generated work.
- **Match complexity to the vision.** Maximalist directions need elaborate
  execution; minimal directions need precision in spacing, type, and detail.
  Elegance is executing the chosen vision well, not adding more.

## Anti–"AI look" calibration

Current AI design clusters around three defaults that appear regardless of
subject. Treat them as red flags, not starting points, unless the brief
explicitly asks for one:

1. Warm cream background + high-contrast serif display + terracotta/warm-clay
   accent (the terracotta near #D97757 especially reads as an AI tell).
2. Near-black background + a single bright acid-green or vermilion accent.
3. Broadsheet layout: hairline rules, zero border-radius, dense newspaper columns.

Where the brief pins a direction, follow it exactly. Where it leaves an axis free,
do **not** spend that freedom on one of these defaults — make a choice for this
brief instead.

## Give each project its own identity

Vary the aesthetic to fit the brand — never reuse one project's look on the next:

- **Appear.pt** (B2B AI) — precise, confident, technical; restraint and clarity.
- **Beira Tech** (community) — energetic, inclusive, local; approachable.
- **Atelier da Alma e do Ser** (wellness) — warm, organic, calm; sensory, grounded.
- **Client work** — derive the direction from the client's own world and brand.

## Process: plan → critique → build → critique again

1. Brainstorm the DIRECTION token plan above.
2. **Critique it against the generic default:** would you arrive at the same plan
   for any similar brief? If a part reads as the default answer, revise it and note
   what changed and why.
3. Build high-fidelity, implementable artifacts in the project stack (Tailwind +
   shadcn/ui + Framer Motion). Derive every colour and type decision from the
   plan. Watch CSS specificity (type-based `.section` vs element selectors
   cancelling paddings/margins).
4. Self-critique as you build — screenshot rendered output if the runtime allows
   (a picture is worth 1000 tokens). Then remove one thing: the design equivalent
   of taking off one accessory before leaving the house.

## Quality floor (non-negotiable, never announced)

Responsive down to mobile; visible keyboard focus; `prefers-reduced-motion`
respected; WCAG AA contrast. Build to this floor quietly.

## Words are design material

Copy can make a design feel as templated as the visuals. Write from the user's
side of the screen: name things by what people control ("Manage notifications",
not "Webhook config"). Active voice; a control says what it does ("Save changes",
not "Submit") and keeps its name through the flow ("Publish" → "Published").
Treat empty and error states as direction, not mood — say what happened and what
to do next. Portuguese-facing copy in pt_PT; coordinate production copy with the
Senior Copywriter.
