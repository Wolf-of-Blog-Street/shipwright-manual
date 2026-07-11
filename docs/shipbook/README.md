---
date_created: 2026-07-09
date_updated: 2026-07-11
status: active manual system; Captain volume generated from whole owning sources
---

# THE SHIPBOOK - the ship's manual system

The Shipbook is Shipwright's complete operating manual. It serves three readers without creating three
incompatible truths:

- the Captain receives the whole ship in one generated volume;
- the Commodore receives the same truth in a human-first visual/manual presentation;
- every commissioned officer receives the complete manual for that officer's department, including the
  exact officers it may contact, why, through which route, and whether that route is live or only designed.

## Truth Before Presentation

Every operational claim is labeled `AS-BUILT`, `CONFIGURED`, `TARGET`, or `UNVERIFIED` according to
`docs/system/ship-manual.md`. Status attaches to a claim, not a person. A configured endpoint is not a
staffed seat, a queue receipt is not execution, and a documented route is not an enforced permission.

> **CURRENT ROUTE GAP:** `config/ship-officer-routes.json` has status `design_not_enforced`. The current
> `seat.message` handler does not check an adjacency allowlist, and the experimental Captain can enqueue to
> every configured officer endpoint. Manuals must say **NOT RUNTIME-ENFORCED** until code and negative tests
> prove otherwise.

## Ownership And Volumes

| Volume/source | Audience | Ownership |
|---|---|---|
| `docs/system/ship-manual.md` | Whole ship | Operational source maintained through the documentation process |
| `shared/officer-operating-standard.md` | Every commissioned seat | Shared command, tool, personal-staff, record, and failure contract |
| `departments/*.md` | Owning officer and Captain | Atomic department truth; one department, one owning commissioned seat |
| `shipbook-captain.md` | Captain | Generated assembly containing every source above whole |
| `shipbook-commodore.md` | Commodore | Human-first companion volume; it must preserve the same facts |
| `config/ship-officer-routes.json` | Runtime builders and manual renderer | Structured route design; not authority and not current enforcement |

The department books are the atomic officer manuals. Do not create a second hand-maintained officer summary
that can drift from the department book. The Captain's volume is generated, never hand-edited.

## Department Books

| Department book | Owning seat | Current truth |
|---|---|---|
| `departments/no1-command-floor.md` | No1 / Commander | Legacy seat as-built; locked S2 target |
| `departments/science.md` | Science Officer | Legacy seat as-built; full S3 target |
| `departments/intelligence.md` | Intelligence Officer | Configured/unmanned; S4 target |
| `departments/security.md` | Security Officer | Configured/unmanned; instruments partly as-built |
| `departments/operations.md` | Operations Officer | Configured/unmanned; instruments partly as-built |
| `departments/communications.md` | Communications Officer | Configured/unmanned; capability-triggered target |
| `departments/tactical.md` | Tactical Officer | Configured/unmanned; depends on Ops and Security |
| `departments/counsellor.md` | Ship's Counsellor | Legacy Doctor as-built; S5 migration target |
| `departments/monitoring.md` | Chief Monitoring Officer | Configured/unmanned; S5 target; name unnormalized |
| `departments/chief-engineer.md` | Chief Engineer | Configured/unmanned; external factory as-built; interface unverified |

## Required Department Schema

Every department book carries exactly these fourteen operating chapters:

1. Commission, rank, reporting, and current state.
2. Mission, owned decisions, and non-responsibilities.
3. Department roster.
4. Inbound orders and accepted route types.
5. Officer contact matrix: purpose, route, authority, and status.
6. Personal staff cell.
7. Tools and access.
8. Boards, records, memory, and single writer.
9. Standard workflows and acceptance.
10. Spend, grants, custody, and metering.
11. Telemetry and provenance.
12. Failure, quarantine, rollback, and recovery.
13. Current versus target readiness.
14. Evidence and hull-stress.

The renderer fails if any department omits a chapter or its prominent non-enforcement warning.

## Build And Check

```bash
node scripts/render-shipbooks.mjs
node scripts/render-shipbooks.mjs --check
```

The renderer validates the route registry, validates all ten department books, and atomically rebuilds
`shipbook-captain.md`. It embeds `docs/system/ship-manual.md`, the shared operating standard, and every
department book whole, with a SHA-256 source manifest and source-boundary comments.

## Officer Boot Contract

A future locked officer boot should receive only:

1. that seat's commission;
2. `shared/officer-operating-standard.md`;
3. that seat's department book;
4. a runtime-generated, enforced contact slice from `config/ship-officer-routes.json`;
5. the seat's packet/current and scoped Brain focus.

The Captain receives `shipbook-captain.md` as the complete whole-ship manual through the experimental
harness's existing read-only `ship.knowledge` surface. `topic=captain_shipbook` without a `part` returns
the generated volume's hash-verified index; a second call with one exact `ship_manual`,
`officer_standard`, or `department_*` part returns that assembled source whole. The large volume
is not injected into every boot prompt, and the tool accepts no raw path. This access is **AS-BUILT**;
manual content still carries its own mixed truth classes, and documented officer routes remain
**NOT RUNTIME-ENFORCED**.

## Definition Of Done

A ship-org slice is not complete until its department book, route status, tools, records, telemetry,
failure doctrine, current/target table, and Captain-volume render are updated and `--check` passes. Manual
assembly does not prove the runtime it describes; live acceptance still requires behavioral evidence.
