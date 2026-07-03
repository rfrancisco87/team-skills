---
name: skill-curation
description: How the team learns — turning recurring review findings and shipped-feature lessons into durable updates to the skills, so the team improves instead of repeating mistakes. Apply when a class of issue recurs, after a notable feature ships, or after an incident. Use for any task about improving, adding, or maintaining the team's skills. Proposed skill changes always go through the human In Review gate.
---

# Skill Curation

Multica's promise is that skills compound. Close the loop: convert repeated lessons
into rules in the relevant skill so no one relearns them.

## Triggers

- A Reviewer (code / copy / design) flags the same class of issue ~3× across
  tickets.
- A feature ships that establishes a new pattern worth standardizing.
- A postmortem or incident yields a preventable cause.

## What to do

1. Identify the smallest durable rule that would have prevented the recurrence.
2. Find the right home: prefer **editing an existing skill** over adding one. Add a
   new skill only for a genuinely new capability — avoid sprawl. Keep skills scoped
   to capabilities, not agents.
3. Propose the edit as a **PR to the skill file** (skills are versioned like code),
   with a one-line rationale and links to the tickets that motivated it.
4. Keep skills concise.

## Human gate

Skill changes affect every agent, so they are never self-approved. A proposed skill
change goes to **In Review** for a human to accept and merge. Never edit a live
skill without that approval.

## Skills vs decisions

Skills hold reusable rules. One-off, context-specific choices belong in ADRs, not
skills.
