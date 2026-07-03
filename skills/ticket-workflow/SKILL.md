---
name: ticket-workflow
description: The shared board-status and agent-handoff protocol for every issue. Apply on EVERY assigned ticket — it governs the six board stages, when to change status, how to pass work to the next agent, when to loop, and when to stop for a human. Attach to all agents. Use whenever you start, finish, block, or hand off any piece of work, even small ones.
---

# Ticket Workflow & Handoff Protocol

Applies to every agent on every issue. It keeps work moving across the board
without anything stalling silently.

## The six board stages (the only statuses)

| Status | Meaning | Who acts next |
|---|---|---|
| Backlog | Captured but not ready — needs speccing/triage | Architect / human |
| Todo | Specced and ready to be picked up | the assigned agent |
| In Progress | Actively being worked — **includes the whole producer ⇄ reviewer agent loop** | current **assignee** |
| In Review | The reviewer agent has approved — a **human** accepts/rejects and merges/publishes/approves | human owner |
| Done | Merged / published / approved | — |
| Blocked | Needs a human decision before work can continue | human owner |

There is no separate "code/copy/design review" status. **Agent peer-review
happens inside In Progress.** The status tells you the *phase*; the **assignee**
tells you *whose turn it is*. If the reviewer agent is the assignee on an
In Progress ticket, it is being reviewed; if the producer is, it is being built
or fixed.

**In Review is the human gate only.** A ticket reaches In Review only after the
reviewer agent approves. Agents never move work to In Review for one another.

## The handoff

**During In Progress (agent ⇄ agent):** hand off by **reassigning** the issue to
the agent who acts next and posting a comment that @-mentions them with a short,
self-contained summary (what you did, what you need, links). The status stays
In Progress. Assignment/mention is what activates the next agent.

**Crossing to In Review (agent → human):** only the reviewer agent does this, and
only on approval — set In Review, reassign to the human owner, @-mention.

Multica activates agents on assignment, comment, or mention, so reassigning and
@-mentioning together reliably wakes the next agent.

## Golden rules (all agents)

- **Start = In Progress.** The moment you begin an assigned Todo item, set it to
  In Progress.
- **Never leave an issue silently.** Whenever you stop, the ticket must name who
  acts next — the right assignee (agent, for the In Progress loop) or the human
  (at In Review / Blocked) — with an @-mention.
- **Producer ≠ reviewer.** Never assign the review of your own work to yourself.
- **The agent loop lives in In Progress.** Producer builds → reassign reviewer →
  reviewer finds issues → reassign producer → producer fixes → reassign reviewer,
  all while the status stays In Progress. Repeat until the reviewer approves.
- **Only humans act on In Review.** There a human accepts and merges/publishes/
  approves (→ Done) or rejects (→ back to In Progress). Agents never set Done,
  never merge, never publish.
- **Blocked needs a human.** If you need a decision or missing input, set Blocked,
  @-mention the human owner, and stop — do not guess.
- **Backlog is intake.** Raw or unspecced items sit in Backlog; the Architect (or
  a human) grooms them into Todo with acceptance criteria before work starts.

## The producer ⇄ reviewer loop (code, copy, and design all share this shape)

```
Todo ─pick up─▶ In Progress ─────────────────────────────────────────────┐
                  (producer builds)                                       │
                  → reassign reviewer ─▶ reviewer audits                   │
                        │ issues → reassign producer → fix → reassign reviewer
                        │ (loops, status stays In Progress)                │
                        ▼ approves                                         │
                  In Review  ─▶ human accepts ─▶ Done                      │
                                 │ rejects → back to In Progress ──────────┘
```

## Example (canonical code flow)

1. Builder picks up a Todo item → sets **In Progress**.
2. Builder finishes the PR → stays **In Progress**, reassigns to the Reviewer,
   @-mentions: "PR #43 ready, criteria 1–3 covered."
3. Reviewer finds issues → stays **In Progress**, reassigns to the Builder,
   @-mentions the ranked blocking list. (Steps 2–3 repeat until approval.)
4. Reviewer approves → sets **In Review**, reassigns to the human owner.
5. Human reviews and accepts → merges → **Done**. (Or rejects → **In Progress**.)
