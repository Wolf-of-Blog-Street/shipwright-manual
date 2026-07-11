---
title: Shipwright Officer Operating Standard
status: mixed as-built and target; route design is not runtime-enforced
audience: Captain, commissioned officers, personal staff, builders, auditors
---

# Shipwright Officer Operating Standard

> **ROUTE SAFETY NOTICE:** `config/ship-officer-routes.json` is a design registry, not an access
> control list. The present `seat.message` handler accepts an arbitrary target string, and the
> experimental Captain can enqueue to every configured officer endpoint. A documented contact does
> not prove delivery, liveness, authorization enforcement, or execution.

## Truth Classes

| Class | Meaning |
|---|---|
| **AS-BUILT** | A concrete implementation or durable artifact was inspected. This does not prove a healthy live watch. |
| **CONFIGURED** | A seat, endpoint, model, or route is named but execution is not proven. |
| **TARGET** | Directed architecture to build. Description is not availability. |
| **UNVERIFIED** | Evidence is absent, contradictory, stale, or insufficient. Treat the capability as unavailable. |

Status attaches to a claim, not a person. A seat may have an as-built legacy runtime, a configured
endpoint, and a target locked harness simultaneously.

## Command Spine

```text
Commodore -> Captain -> No1 / Commander -> commissioned department -> managers -> workers
```

The Captain also has named direct lines. A direct conversation line does not necessarily replace No1's
ordinary tasking authority. Sibling departments route through No1 unless an explicit, purpose-bounded
route is present in `config/ship-officer-routes.json`. A model's intelligence, cost, or confidence never
changes rank or authority.

## Target Officer Cockpit

The target locked officer receives only:

- `packet.read`, `pa.ask`, and `pa.tell`;
- `order.issue`, `order.amend`, `order.cancel`, `order.accept`, and `order.reject`;
- `seat.message` on an enforced direct-line allowlist;
- `escalate` up the authenticated chain.

The Captain additionally targets `panel.fire` and `gate.record`. Officers receive no raw filesystem,
shell, browser, generic agent, skill, plugin, credential, deployment, or release tool. Current legacy
officer runtimes and the experimental Captain cockpit do not yet equal this target.

## Repeated Personal Staff Cell

Every Captain and commissioned officer receives three private departments:

1. **Advisor / mini-science.** A Warrant Officer, non-line, with its own PA and configured
   Ensign-rank Scientist thinking partners. It supports cognition and holds no command authority.
2. **PA / mini-operations.** A Chief Petty Officer with an officer-scoped human-brain and a configured
   Petty Officer/specialist team. The PA retrieves, records, schedules, researches, and administers;
   the officer decides and speaks.
3. **Personal Engineer / mini-engineering.** A Lieutenant manager using an isolated engineering
   workspace and fresh Codex Ensign workers. It builds officer-specific tooling only. Ship-wide work
   routes through the Chief Engineer.

No AI writer targets the default working copy. Each writer uses an isolated workspace and submits a
candidate to the target landing broker. That invariant remains TARGET / UNVERIFIED until enforced.

## Orders, Queues, And Acceptance

Every executable order names issuer, target, authority source, objective, constraints, acceptance,
evidence, priority, grant where needed, epoch, idempotency key, and autonomy margin. Queue receipt is
only `queued`. It is not `delivered`, `working`, `reported`, `accepted`, or `complete`.

An officer rejects malformed, over-specified, ungranted, or unsafe work. A report remains data until the
authorized accepting seat checks it against the order's evidence and acceptance conditions.

## Boards, Memory, And Records

- No1 owns the main ship board; each commissioned officer owns one department board.
- A PA may mechanically transcribe for its officer but may not decide status or authority.
- An officer Brain stores durable personal judgment, not live work, orders, grants, or seals.
- A PA ledger stores events and actions. Belief-class writes require the owning officer's exact
  ratification.
- Records and telemetry never create command authority.

## Web, Credentials, Spend, And Provenance

Locked command seats do not browse and hold no ambient credentials. Sourced research routes through the
officer's PA, Advisor Scientists, or the commissioned Science department. Personal Engineers may use
technical web access only inside their isolated build lane.

New ships and new metered lanes start at `$0`. Spend requires a named grant. Ops owns intake and budget;
Security owns privilege and credential custody; custody-class movement requires a human gate. Every action
must retain issuer, route, model/effort, tool, workspace, grant/cost or explicit unknown, evidence, report,
acceptance, and prior-event linkage.

## Shared Failure Doctrine

- Stop and expose missing authority, missing grant, stale epoch, provenance gap, or route ambiguity.
- Never reinterpret a configured endpoint as a staffed seat or a queue receipt as execution.
- Preserve failed attempts and superseded records; do not rewrite history.
- Quarantine credentials through Security, contain operational impact through No1, and escalate material
  security or monitoring alerts directly to the Captain on their named lines.
- When route sources conflict, use No1 as the operational path and mark the direct line `UNVERIFIED` until
  an authenticated normalization lands.

## Evidence Basis And Known Gap

Primary sources are `docs/system/ship-manual.md`, `docs/design/ship-org-design.md`,
`config/ship-personal-departments.json`, `config/agents.json`, and the inspected harness implementations.
The largest open control gap is the absence of a runtime adjacency allowlist tied to the route registry.
No department manual may claim that peer communication is enforced until the implementation and negative
tests prove it.
