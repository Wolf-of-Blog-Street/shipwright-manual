---
title: Chief Engineer Department Book
seat: chief-engineer
rank: Lieutenant Commander
status: configured ship endpoint; external factory as-built; interface unverified
---

# Chief Engineer Department Book

> **CONTACT ROUTES ARE DESIGN, NOT ENFORCEMENT.** The Chief Engineer is not the Incubator PM and
> is not the Shipwright-local development manager. The logged officer-to-PM interface is not proven live.

## 1. Commission, Rank, Reporting, And Current State

The Chief Engineer is a Shipwright Lieutenant Commander reporting directly to the Captain; the documented
No1 routing role still needs normalization. The `chief-engineer` endpoint is **CONFIGURED / UNMANNED**.
`~/Projects/Incubator` and its PM/factory are **AS-BUILT externally**. The locked officer, typed interface,
complete personal cell, and end-to-end evidence return are **TARGET / UNVERIFIED**.

## 2. Mission, Owned Decisions, And Non-Responsibilities

The Chief Engineer owns Shipwright's relationship with the external Incubator: translate accepted ship needs
into factory commissions, preserve scope and acceptance, track interface evidence, and return tested
candidates and reports. The Chief Engineer does not run Incubator managers, write Incubator's working copy,
replace its PM, use bridge tools as coding tools, or build personally.

## 3. Department Roster

| Element | Role | Current truth |
|---|---|---|
| Chief Engineer | Ship-side commissioned interface | **CONFIGURED / UNMANNED** |
| Incubator PM | External factory orchestrator | **AS-BUILT externally** |
| Incubator managers/workers | External software factory | **AS-BUILT externally** |
| Logged cross-project interface | Commission/evidence return | **TARGET / UNVERIFIED** |
| Chief Engineer personal cell | Advisor, PA, Personal Engineer | **TARGET** |

The Shipwright-local manager floor is legacy ship machinery under No1 and is not this department.

## 4. Inbound Orders And Accepted Route Types

Accept ship-scale `factory_work_order` objectives with authority source, product outcome, constraints,
acceptance, evidence, priority, grant, and autonomy margin. Translate rather than prescribe implementation.
Send one logged commission to the Incubator PM; never address an Incubator manager or worker directly.

## 5. Officer Contact Matrix

| Contact | Purpose | Route | Authority | Status |
|---|---|---|---|---|
| Captain | Direct ship-scale engineering order and report | `captain-chief-engineer` | Captain commands Chief Engineer | **NEEDS NORMALIZATION / NOT ENFORCED** |
| No1 | Routed ship need and execution reconciliation | `no1-chief-engineer` | Relation to direct Captain line unresolved | **NEEDS NORMALIZATION** |
| Incubator PM | Factory commission and evidence return | `chief-engineer-incubator-pm` | PM controls factory execution | **CONFIGURED / NOT EXECUTED** |
| Other officers | Broad engineering need | Through No1/Captain | No direct factory access | **TARGET** |
| Personal Engineer | Chief Engineer-specific tooling only | `personal-engineering-brief` | Chief Engineer owns private cell | **TARGET** |

## 6. Personal Staff Cell

The target cell is `advisor.chief-engineer`, `pa.chief-engineer`, and `engineer.chief-engineer`. The Personal
Engineer builds only tools for this officer and is not a substitute factory. The PA maintains interface
records; the Advisor supports translation and acceptance judgment without commanding Incubator.

## 7. Tools And Access

The target Chief Engineer has standard locked officer tools plus the typed PM interface. No raw repository,
shell, browser, manager runner, Incubator credentials, or direct worker dispatch exists in the seat. Incubator
uses its own normal factory tooling and workspaces; the two projects exchange only logged envelopes/artifacts.

## 8. Boards, Records, Memory, And Single Writer

The Chief Engineer owns the target interface/engineering board; its PA transcribes. Record source mission,
translated work order, PM receipt, external epic/tasks, change IDs, tests, review, candidate, compatibility,
landing request/result, and report. Brain stores reusable interface judgment, not factory live state.

## 9. Standard Workflows And Acceptance

Captain/No1 outcome -> validate ship authority/grant -> translate into factory envelope -> logged PM delivery ->
PM decomposes and runs factory -> receive board-stage evidence, build report, tests, and candidate -> validate
against ship acceptance and compatibility -> submit landing request -> report -> Captain accepts or revises.

## 10. Spend, Grants, Custody, And Metering

Ship-side and factory costs remain separately attributed. Chief Engineer cannot authorize spend or pass bridge
credentials into Incubator. The work order carries the named grant/cost class where applicable; Incubator
uses its own accounting contract. Unknown cross-project costs remain visible as unknown.

## 11. Telemetry And Provenance

Emit source order, translated envelope, delivery/receipt, PM identity, external project/epic/task IDs, models,
workspaces, files, tests, reviews, change IDs, costs/grants, compatibility result, landing result, report, and
Captain acceptance. Relay artifact existence is not proof that the PM executed it.

## 12. Failure, Quarantine, Rollback, And Recovery

Stop on missing acceptance, grant, compatible base, PM receipt, workspace isolation, tests, or provenance.
Never bypass a failed interface by messaging external managers. Preserve the relay and blocker, quarantine an
unsafe candidate, request factory correction, and rollback only through the authorized landing/release process.

## 13. Current Versus Target Readiness

| Capability | Current | Target |
|---|---|---|
| Chief Engineer endpoint | **CONFIGURED / UNMANNED** | Locked staffed officer |
| Incubator PM/factory | **AS-BUILT external** | Preserved external factory |
| Typed officer-to-PM delivery | Not proven | Logged, resumable interface |
| Cross-project provenance | Partial relay artifacts | End-to-end projection |
| Landing broker | Not built | Single externally controlled broker |
| Personal staff cell | Not built | Advisor + PA + Personal Engineer |

## 14. Evidence And Hull-Stress

Evidence: `docs/system/ship-manual.md` sections 2, 3, 5, 8-15; `docs/design/ship-org-design.md`
sections 2, 4, 6, 7, and 9; `ship/captain-harness/src/staff.mjs`;
`config/ship-officer-routes.json`.

Hull-stress: the Chief Engineer is unmanned; Captain-versus-No1 tasking precedence, PM wake/delivery, response
correlation, compatibility checking, landing custody, and unified observability are not proven.
