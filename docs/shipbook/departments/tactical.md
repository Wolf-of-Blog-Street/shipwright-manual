---
title: Tactical Department Book
seat: tactical.officer
rank: Lieutenant Commander
status: configured endpoint; target after Operations and Security; unmanned
---

# Tactical Department Book

> **CONTACT ROUTES ARE DESIGN, NOT ENFORCEMENT.** Tactical is not staffed and cannot bypass No1,
> Operations, Security, grants, or the Captain merely because an opportunity is urgent or profitable.

## 1. Commission, Rank, Reporting, And Current State

The Tactical Officer is a Lieutenant Commander under No1. The endpoint is **CONFIGURED / UNMANNED**. Stand-up
depends on manned Operations and Security. A locked officer, opportunity pipeline, evaluation crew, board,
and personal staff cell are **TARGET**.

## 2. Mission, Owned Decisions, And Non-Responsibilities

Tactical finds earning paths and mission tactics that can fund and expand the fleet, then gives bounded
options to the Captain. It owns opportunity discovery, comparison, downside analysis, and execution-plan
recommendations. It does not choose the mission, authorize spend, move money, issue credentials, bind the
ship to a deal, manipulate markets, or execute outside lawful and ethical constraints.

## 3. Department Roster

| Element | Role | Current truth |
|---|---|---|
| Tactical Officer | Commissioned head | **CONFIGURED / UNMANNED** |
| Opportunity/recon crew | Discover and characterize options | **TARGET** |
| Evaluation/risk crew | Evidence, downside, feasibility | **TARGET** |
| Tactical board | Funnel, experiments, results | **TARGET** |
| Personal Advisor, PA, Engineer | Private officer cell | **TARGET** |

Exact crew, legal review, risk model, experiment limits, and activation dependency checks are unspecified.

## 4. Inbound Orders And Accepted Route Types

Accept `command_order` work through No1 with desired outcome, constraints, jurisdiction, risk ceiling,
evidence, grant, acceptance, and forbidden tactics. Tactical returns options and recommendations. Execution
requires a separate authenticated order, resource allocation, Security privilege, and Captain decision.

## 5. Officer Contact Matrix

| Contact | Purpose | Route | Authority | Status |
|---|---|---|---|---|
| No1 | Commission tactics and route reports | `no1-tactical` | No1 runs department | **TARGET / NOT ENFORCED** |
| Captain | Receive decision-ready options | Through No1 | Captain chooses | **TARGET** |
| Operations | Budget/capacity dependency | Through No1 and resource flow | Ops controls allocation only | **TARGET** |
| Security | Privilege, custody, risk dependency | Through No1 and governance flow | Security controls access only | **TARGET** |
| Intelligence/Science | Research or validation need | Through No1 | No direct peer command | **TARGET** |

## 6. Personal Staff Cell

The target cell is `advisor.tactical`, `pa.tactical`, and `engineer.tactical`. The Advisor challenges options;
the PA obtains sourced research and administers records; the Personal Engineer builds Tactical Officer tools.
The private cell cannot authorize or execute an opportunity.

## 7. Tools And Access

The target officer has standard locked tools. Market, account, deal, financial, or execution tools are absent
from the command seat. Research and simulations use bounded staff lanes. Any real execution tool requires a
separate grant, Security-approved privilege, external custody, and full provenance.

## 8. Boards, Records, Memory, And Single Writer

The Tactical Officer owns the target Tactical board; its PA transcribes. Record opportunity source, thesis,
jurisdiction, evidence, assumptions, downside, dependencies, experiment, result, and decision. Tactical Brain
stores durable strategic judgment and failed theses, not live positions, balances, or standing authority.

## 9. Standard Workflows And Acceptance

Commission -> discover options -> retain sources -> screen legality/mission fit -> model upside/downside ->
identify Ops/Security dependencies -> propose cheap reversible test -> Captain selects -> separately authorize
execution -> observe result -> report actual outcome and failed assumptions -> accept, revise, or stop.

## 10. Spend, Grants, Custody, And Metering

Discovery starts at `$0` unless granted. Paid data, models, experiments, transactions, or execution require
named duty grants. Tactical never holds custody credentials. Report gross and net outcome, fees, risk exposure,
grant, cost class, and unknowns; projected return is never reported as realized money.

## 11. Telemetry And Provenance

Emit commission, source, thesis, evidence, model/effort, assumptions, risk, grant, dependencies, proposed and
approved actions, human/custody gates, execution receipts, realized outcome, counterfactual, and acceptance.
The Ship Computer must distinguish proposal, authorization, execution, and settlement.

## 12. Failure, Quarantine, Rollback, And Recovery

Stop on missing authority, unlawful tactic, unverifiable counterpart, custody ambiguity, grant breach, or risk
outside the order. Revoke execution access through Security, contain exposure through Ops, preserve receipts,
notify No1/Captain, and resume only after explicit reauthorization and updated downside analysis.

## 13. Current Versus Target Readiness

| Capability | Current | Target |
|---|---|---|
| Tactical endpoint | **CONFIGURED / UNMANNED** | Locked staffed seat |
| Ops/Security dependencies | Seats unmanned | Manned prerequisite controls |
| Opportunity pipeline | Not built | Evidence-backed funnel |
| Execution/custody | No authority | Typed, human-gated external control |
| Personal staff cell | Not built | Advisor + PA + Personal Engineer |

## 14. Evidence And Hull-Stress

Evidence: `docs/system/ship-manual.md` sections 2, 3, 10-15; `docs/design/ship-org-design.md`
sections 2, 3, 5, 7, and 9; `ship/captain-harness/src/staff.mjs`;
`config/ship-officer-routes.json`.

Hull-stress: no internal roster, lawful-opportunity policy, risk framework, live dependency check, experiment
lane, or settlement ledger is proven. Profit language must not be mistaken for execution authority.
