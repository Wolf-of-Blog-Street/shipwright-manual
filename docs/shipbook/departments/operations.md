---
title: Operations Department Book
seat: ops.officer
rank: Lieutenant Commander
status: configured endpoint; instruments partly as-built; officer unmanned
---

# Operations Department Book

> **CONTACT ROUTES ARE DESIGN, NOT ENFORCEMENT.** Operations has no proven live officer route.
> Resource allocation requires both authenticated grant authority and Security's privilege/custody stage.

## 1. Commission, Rank, Reporting, And Current State

The Operations Officer is a Lieutenant Commander under No1, with Captain resource decisions flowing
through command. The endpoint is **CONFIGURED / UNMANNED**. Spend registries and grants exist independently;
the complete Ops-owned resource plane, locked seat, and crew are **TARGET**.

## 2. Mission, Owned Decisions, And Non-Responsibilities

Operations owns ship funds administration, crypto operations, servers, API-key intake, usage budgets, cost
ledger, capacity, and operating cadence. It allocates only under authenticated grants. It does not mint
grants, approve its own privilege, issue credentials without Security, make custody-class movements without
a human gate, or choose mission priorities.

## 3. Department Roster

| Element | Role | Current truth |
|---|---|---|
| Operations Officer | Commissioned head | **CONFIGURED / UNMANNED** |
| Grant and cost instruments | Budget/cost records | Partly **AS-BUILT** |
| Resource operations crew | Servers, accounts, cadence, capacity | **TARGET** |
| Treasury/custody execution | Canary and human-gated movement | **TARGET / UNVERIFIED** |
| Personal Advisor, PA, Engineer | Private officer cell | **TARGET** |

## 4. Inbound Orders And Accepted Route Types

Accept authenticated resource `command_order` work through No1. Every request names purpose, owner, grant,
cost class, ceiling, duration, provider/resource, acceptance, and revocation condition. Requests without a
grant become a documented escalation, not an allocation.

## 5. Officer Contact Matrix

| Contact | Purpose | Route | Authority | Status |
|---|---|---|---|---|
| No1 | Resource work, cadence, and reporting | `no1-operations` | No1 runs department | **TARGET / NOT ENFORCED** |
| Security | Privilege check, credentials, revocation | `ops-security-resource-check` | Each owns one stage | **TARGET / NOT ENFORCED** |
| Captain | Resource decision and grant escalation | Through No1; Captain escalates to Commodore | Captain commands | **TARGET** |
| Tactical | Funding/capacity dependency | Through No1 | No direct peer route | **TARGET** |
| Other officers | Resource request | Through No1 and typed intake | No direct allocation authority | **TARGET** |

## 6. Personal Staff Cell

The target cell is `advisor.ops`, `pa.ops`, and `engineer.ops`. The personal PA is not the ship Operations
department: it handles only the Operations Officer's private administration. The Personal Engineer builds
Ops Officer tools but receives no ambient treasury or master credentials.

## 7. Tools And Access

The target officer has standard locked tools. Resource and cost actions use typed, scoped operations with
external credentials hidden from models. Server or connector execution belongs to bounded staff lanes.
Personal Engineer web/shell access stays inside its isolated workspace and cannot move funds or issue keys.

## 8. Boards, Records, Memory, And Single Writer

The Operations Officer owns the target Operations board; its PA transcribes. Grants, inventory, cost ledger,
provider receipts, server state, and custody records remain separate authoritative records. Ops Brain stores
reusable operating judgment, never secret values, live balances as memory, or grant authority.

## 9. Standard Workflows And Acceptance

Request -> authenticate order and grant -> ask Security for privilege/custody decision -> allocate bounded
resource -> record ceiling and cost class -> monitor consumption -> warn at threshold -> revoke/expire ->
weekly roll-up -> No1/Captain acceptance. Custody movement adds canary -> human gate -> move -> watch.

## 10. Spend, Grants, Custody, And Metering

Default is `$0`. Separate `ship-ops` from `duty`. At 80% or a blocking ceiling, escalate immediately with
spend, wall, impact, and proposed new ceiling. Report Max-plan headroom separately from billed cash. No
provisioning credential or master secret becomes ambient model context.

## 11. Telemetry And Provenance

Emit request/order, grant, cost class, privilege check, resource ID/fingerprint, ceiling, allocation,
consumption, provider receipt, alert, revocation, custody gate, human approval, roll-up, and explicit blind
spots. Never persist credential values.

## 12. Failure, Quarantine, Rollback, And Recovery

Fail closed on missing grant, privilege, custody, ceiling, or evidence. Stop further allocation at breach,
revoke affected access through Security, preserve provider receipts, and notify No1/Captain. Recovery needs
new authorization and verified state; do not infer funds or capacity from stale ledgers.

## 13. Current Versus Target Readiness

| Capability | Current | Target |
|---|---|---|
| Operations Officer | **CONFIGURED / UNMANNED** | Locked staffed seat |
| Grants/cost records | Partly **AS-BUILT** | Typed Ops ownership |
| Provider-level limits | Incomplete | External per-seat enforcement |
| Treasury movement | Not proven | Canary + human gate + watch |
| Personal staff cell | Not built | Advisor + PA + Personal Engineer |

## 14. Evidence And Hull-Stress

Evidence: `docs/system/ship-manual.md` sections 2, 3, 10-12, and 15;
`docs/design/ship-org-design.md` sections 2, 3, 5, and 7; `docs/system/spend-governance.md`;
`config/ship-officer-routes.json`.

Hull-stress: the endpoint is not a staffed office. Exact crew, provider provisioning authority, complete
metering, direct execution boxes, and custody-class transaction implementation remain unproven.
