---
title: Intelligence Department Book
seat: intelligence.officer
rank: Lieutenant Commander
status: configured endpoint; target S4 department; unmanned
---

# Intelligence Department Book

> **CONTACT ROUTES ARE DESIGN, NOT ENFORCEMENT.** The endpoint is configured but unmanned. Direct
> Captain contact exists only when the Captain calls the seat; ordinary work routes through No1.

## 1. Commission, Rank, Reporting, And Current State

The Intelligence Officer is a Lieutenant Commander reporting through No1, with a purpose-bounded direct
Captain line when called. The `intelligence.officer` endpoint is **CONFIGURED / UNMANNED**. The S4 locked
officer, recon pyramid, source pipeline, board, crew, and personal staff cell are **TARGET**.

## 2. Mission, Owned Decisions, And Non-Responsibilities

Intelligence performs reconnaissance at scale: source discovery, capture, triage, filing, synthesis, and
provenance-retained intelligence. It owns collection quality and uncertainty. It does not set missions,
declare source claims true without evidence, command sibling departments, conduct mind intervention, or
make Security privilege decisions.

## 3. Department Roster

| Element | Role | Current truth |
|---|---|---|
| Intelligence Officer | Commissioned head | **CONFIGURED / UNMANNED** |
| Recon pyramid | Fetch, keep/throw, tiered filing, synthesis | **TARGET S4** |
| Source and provenance ledger | Retained source pointers and uncertainty | **TARGET** |
| Intelligence board | Commissions, WIP, reports | **TARGET** |
| Personal Advisor, PA, Engineer | Private officer cell | **TARGET** |

Exact manager ranks, slot counts, model mix, WIP limits, and source-retention policy are not yet canonical.

## 4. Inbound Orders And Accepted Route Types

Accept bounded `command_order` intelligence commissions from No1. A Captain direct request is valid only
when the Captain explicitly calls the seat. Each commission needs question, jurisdiction, source standard,
time horizon, privacy constraints, acceptance, and grant. Unscoped monitoring is not an Intelligence order.

## 5. Officer Contact Matrix

| Contact | Purpose | Route | Authority | Status |
|---|---|---|---|---|
| No1 | Ordinary reconnaissance commission and report | `no1-intelligence` | No1 runs department | **TARGET / NOT ENFORCED** |
| Captain | Direct consultation only when called | `captain-intelligence-called` | Captain commands; purpose-bounded | **TARGET / NOT ENFORCED** |
| Security | Source-risk or injection concern | Through No1 unless incident escalation applies | No peer command | **UNVERIFIED** |
| Science | Evidence package for broader analysis | Through No1 | No peer command | **TARGET** |
| Other officers | Intelligence request | Through No1 | No direct route | **TARGET** |

## 6. Personal Staff Cell

The target cell is `advisor.intelligence`, `pa.intelligence`, and `engineer.intelligence`. Personal Advisor
work is immediate cognition, not recon production. The PA handles officer-scoped research and records;
the operating department owns ship intelligence. The Personal Engineer builds Intelligence Officer tools.

## 7. Tools And Access

The target officer has standard locked tools only. Department collectors receive bounded search/fetch and
source-recording access under grants, not arbitrary credentials or ship command. The PA and Personal
Engineer use separate scoped workspaces. No Intelligence actor writes the default repository working copy.

## 8. Boards, Records, Memory, And Single Writer

The Intelligence Officer owns the target Intelligence board; the PA mechanically writes it. The source
ledger retains URL or identifier, fetch time, excerpt/hash, collector, transformation lineage, and
uncertainty. The officer Brain stores durable reconnaissance judgment, not active collection state.

## 9. Standard Workflows And Acceptance

Commission -> define collection plan -> fetch into bounded stream -> cheap keep/throw triage -> provenance-
preserving filing -> higher-tier synthesis -> contradictory-source check -> report with citations and gaps ->
No1 integrates -> Captain accepts ship-level use.

## 10. Spend, Grants, Custody, And Metering

Paid search, model, proxy, storage, and data-source lanes require named grants. Intelligence holds no ambient
credentials. Ops allocates budget; Security approves privilege and issues revocable access. Report per-run
cost or explicit unknown, never API-equivalent estimates as billed cash.

## 11. Telemetry And Provenance

Emit commission ID, query, collector, source ID, retrieval time, transformations, keep/throw decision,
model/effort, citation, report claim, uncertainty, grant/cost, and acceptance. Sensitive content requires
redaction before Ship Computer projection.

## 12. Failure, Quarantine, Rollback, And Recovery

Quarantine prompt-injected or provenance-broken sources. Stop unauthorized collection, privacy boundary
breach, credential exposure, or scope expansion. Preserve source and transformation history, notify Security
for incidents, and resume from the board and source ledger without inventing missing chronology.

## 13. Current Versus Target Readiness

| Capability | Current | Target |
|---|---|---|
| Endpoint | **CONFIGURED / UNMANNED** | Locked Intelligence Officer |
| Recon pyramid | Not built | S4 department |
| Source ledger and board | Not proven | Durable, queryable state |
| Direct Captain route | Metadata only | Purpose-bound enforced route |
| Personal staff cell | Not built | Advisor + PA + Personal Engineer |

## 14. Evidence And Hull-Stress

Evidence: `docs/system/ship-manual.md` sections 2, 3, 11-15; `docs/design/ship-org-design.md`
sections 2, 3, 7, and 9; `ship/captain-harness/src/staff.mjs`; `config/ship-personal-departments.json`;
`config/ship-officer-routes.json`.

Hull-stress: the department has no canonical internal roster, live collector, retention policy, board, or
end-to-end delivery proof. “Recon pyramid” is architecture, not a staffed capability.
