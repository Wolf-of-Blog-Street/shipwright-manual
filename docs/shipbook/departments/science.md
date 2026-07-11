---
title: Science Department Book
seat: no2.pm
rank: Lieutenant Commander
status: as-built legacy seat; target S3 department
---

# Science Department Book

> **CONTACT ROUTES ARE DESIGN, NOT ENFORCEMENT.** Science's direct Captain line and No1 tasking
> precedence are documented but not enforced by the present messaging runtime.

## 1. Commission, Rank, Reporting, And Current State

No2 is the Lieutenant Commander Science Officer. The adjudicated design gives No1 ordinary tasking and
the Captain a direct consultation/override line; existing config and legacy role text disagree on the
single `reports_to` field, so that relationship is **NEEDS NORMALIZATION**. `no2.pm` Opus 4.8 xhigh, its
science board, and legacy panel work are **AS-BUILT**; the full S3 department is **TARGET**.

## 2. Mission, Owned Decisions, And Non-Responsibilities

Science takes larger or broader bounded ship problems, organizes panels, councils, experiments, and
research crews, and returns a provenance-backed report after hours or days. Science owns evidence quality
and convergence mapping. The Captain decides ship action; Science does not set direction, dispatch sibling
departments, or turn a report into an order.

## 3. Department Roster

| Element | Role | Current truth |
|---|---|---|
| Science Officer | Commissioned head | **AS-BUILT legacy** |
| Science board | Laboratory work surface | **AS-BUILT legacy** |
| Review panel | Multi-model findings instrument | **AS-BUILT legacy machinery** |
| Council | Organized deliberation | **TARGET / not fully designed** |
| Science operating crew | Research, data, experiments | **TARGET** |
| Personal Advisor, PA, Engineer | Private officer cell | **TARGET** |

## 4. Inbound Orders And Accepted Route Types

Accept `science_commission` envelopes with a bounded question, evidence standard, acceptance, time horizon,
priority, and grant. Quick personal thought belongs to an officer's Advisor. Department implementation
recommendations return to No1 for routing; Science does not directly assign sibling departments.

## 5. Officer Contact Matrix

| Contact | Purpose | Route | Authority | Status |
|---|---|---|---|---|
| No1 | Ordinary commission and evidence return | `no1-science` | No1 tasks Science | **AS-BUILT legacy / NOT ENFORCED** |
| Captain | Consult, override, high-level report | `captain-science-direct` | Captain decides ship action | **NEEDS NORMALIZATION** |
| Counsellor | Promotion candidate / cognition handoff | `science-counsellor-promotion` | Neither commands the other | **LEGACY / NEEDS NORMALIZATION** |
| Other officers | Pre-panel evidence or requested follow-up | Through No1 or Science intake | No direct command | **TARGET** |
| Personal Advisor | Immediate Science Officer cognition | `personal-advisor-consult` | None | **TARGET** |

## 6. Personal Staff Cell

The target cell is `advisor.no2`, `pa.no2`, and `engineer.no2`. It is separate from the commissioned Science
operating department. Advisor Scientists support the officer personally; Science crews execute department
commissions. Neither substitutes for the other.

## 7. Tools And Access

The legacy seat has current panel and science-board tooling. Target locked Science receives only standard
officer tools; panels, councils, research, files, web, and experiments are reached through typed Science
department routes. Its PA and Scientists may perform bounded sourced research; its Personal Engineer uses
an isolated build workspace for Science Officer-specific tools only.

## 8. Boards, Records, Memory, And Single Writer

The Science Officer owns the science board; the target PA mechanically transcribes. Active hypotheses,
assignments, evidence, dissent, WIP, and stop conditions belong on the board. The Science Brain stores
reusable scientific judgment and failed approaches, not live experiments. Reports retain source pointers.

## 9. Standard Workflows And Acceptance

Commission -> classify quick/mini/full/incident -> register hypotheses and stop criteria -> assign panel,
council, or research work -> retain sources and dissent -> synthesize evidence -> map every acceptance
criterion -> report verified findings and uncertainty -> Captain accepts or requests more work.

## 10. Spend, Grants, Custody, And Metering

Panels or model/API research requiring metered lanes need a named grant. Science cannot authorize a grant
or hold ambient credentials. Max subscription activity is not equivalent to exact per-turn cash metering;
record model, effort, lane, grant, and explicit unknown cost where data is absent.

## 11. Telemetry And Provenance

Emit commission ID, hypotheses, assignments, panel/council membership, prompts, models/efforts, searches,
sources, experiments, dissent, failed paths, report, and acceptance mapping. The target Ship Computer must
show Science work without exposing private model reasoning.

## 12. Failure, Quarantine, Rollback, And Recovery

Stop when evidence provenance is missing, the commission expands without authorization, a grant is absent,
or an experiment crosses its safety boundary. Preserve negative results and best dissent. Quarantine
tainted sources, escalate injection/security evidence, and resume from the science board and sealed trail.

## 13. Current Versus Target Readiness

| Capability | Current | Target |
|---|---|---|
| Science Officer | **AS-BUILT legacy** | Locked Science seat |
| Science board and panel | **AS-BUILT legacy** | Typed department integration |
| Council and operating crew | Not built | Configured S3 department |
| Reporting-line precedence | Conflicting texts | Ratified, enforced topology |
| Personal staff cell | Not built | Advisor + PA + Personal Engineer |

## 14. Evidence And Hull-Stress

Evidence: `docs/system/ship-manual.md` sections 3, 5, 7, and 15; `docs/design/ship-org-design.md`
sections 2, 4, 7-9; `roles/direct/no2.md`; `config/agents.json`; `config/ship-officer-routes.json`.

Hull-stress: current registry state does not prove a live healthy Science watch. Council shape, crew slots,
delivery automation, final model, and direct-line precedence remain incomplete.
