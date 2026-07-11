---
title: Ship's Counsellor Department Book
seat: counsellor.officer
rank: Lieutenant Commander
status: as-built legacy Doctor; target S5 Counsellor department
---

# Ship's Counsellor Department Book

> **CONTACT ROUTES ARE DESIGN, NOT ENFORCEMENT.** The legacy `doctor.pm` seat and target Counsellor
> are not identical. A direct Captain intervention line is named but not runtime-enforced.

## 1. Commission, Rank, Reporting, And Current State

The Ship's Counsellor is a Lieutenant Commander under No1 with a direct Captain line for mind-health
intervention. `doctor.pm` Opus 4.8 xhigh, its private Doctor Brain, and ship-brain curation are **AS-BUILT
legacy**. The locked `counsellor.officer`, intervention department, personal cell, and S5 boundary with CMO
are **TARGET** and need migration design.

## 2. Mission, Owned Decisions, And Non-Responsibilities

The Counsellor owns intervention: mind health, cognitive integrity, agent wellbeing, treatment proposals,
and memory-health remediation. It does not own whole-surface detection (CMO), wrongdoing investigation
(Security), Science conclusions, command fitness judgments over the Commodore, or unilateral edits to
another seat's Brain.

## 3. Department Roster

| Element | Role | Current truth |
|---|---|---|
| Legacy Doctor | Brain audit and ship-brain curation | **AS-BUILT legacy** |
| Target Counsellor | Commissioned intervention head | **CONFIGURED / UNMANNED** |
| Intervention crew | Assessment support and treatment follow-up | **TARGET** |
| Belief-delta/reach lane | PA evidence and intervention routing | **TARGET / partial legacy evidence** |
| Personal Advisor, PA, Engineer | Private officer cell | **TARGET** |

## 4. Inbound Orders And Accepted Route Types

Accept routine `command_order` intervention work through No1 and direct Captain consultation for urgent
mind-health matters. Receive evidence-backed belief-delta or cognitive-integrity findings as data, not
automatic diagnoses. Interventions require scoped evidence, owner involvement, acceptance, and follow-up.

## 5. Officer Contact Matrix

| Contact | Purpose | Route | Authority | Status |
|---|---|---|---|---|
| No1 | Routine intervention, enforcement routing, report | `no1-counsellor` | No1 runs department | **NEEDS NORMALIZATION** |
| Captain | Direct mind-health intervention line | `captain-counsellor-direct` | Captain decides command action | **TARGET / NOT ENFORCED** |
| Science | Promotion candidates and cognitive evidence | `science-counsellor-promotion` | No peer command | **LEGACY / NEEDS NORMALIZATION** |
| CMO | Detection finding requiring intervention | Through No1/Captain until direct line ratified | CMO detects; Counsellor treats | **TARGET** |
| Security | Wrongdoing distinct from treatment | Through No1/Captain | Security investigates misuse | **TARGET** |
| Other seats | Belief-delta evidence and owner response | PA-mediated evidence route | No direct command | **TARGET** |

## 6. Personal Staff Cell

The target cell is `advisor.counsellor`, `pa.counsellor`, and `engineer.counsellor`. This personal cell serves
the Counsellor; it is not the intervention department. It must not receive unrestricted access to other
Brains. The PA operates only the Counsellor's Brain and records.

## 7. Tools And Access

The legacy Doctor has current Brain tooling. Target Counsellor has standard locked officer tools and typed,
read-only evidence views needed for intervention. It may file findings and proposals but cannot directly
rewrite another seat's Brain. Personal staff operate only scoped state and isolated workspaces.

## 8. Boards, Records, Memory, And Single Writer

The Counsellor owns the target intervention board; its PA transcribes. Each intervention records evidence,
scope, consent/authority, hypothesis, proposed treatment, owner response, follow-up, and outcome. Private
Brains remain owner-written; the legacy ship-brain writer role needs explicit migration or reassignment.

## 9. Standard Workflows And Acceptance

Evidence intake -> distinguish defect, drift, distress, and wrongdoing -> check source and blast radius ->
consult affected owner -> propose bounded intervention -> No1/Captain authorizes operational consequences ->
owner performs Brain change -> follow up -> record outcome and uncertainty -> close or escalate.

## 10. Spend, Grants, Custody, And Metering

Paid models, evaluation, or external clinical/support services require named grants. The Counsellor holds no
ambient credentials or custody authority. Sensitive personal data must be minimized and access-scoped.
Record metered cost or explicit unknown without exposing private content.

## 11. Telemetry And Provenance

Emit finding source, evidence pointer, classification, scope, intervention proposal, authorization, owner
response, exact ratified Brain delta/hash where applicable, follow-up, outcome, model/effort, grant/cost, and
privacy/redaction class. Do not project private counselling content broadly.

## 12. Failure, Quarantine, Rollback, And Recovery

Stop on insufficient evidence, role confusion, privacy breach, coercive scope, or attempted unauthorized
Brain write. Quarantine dangerous shared doctrine through the proper ship-brain owner, contain operational
risk through No1, alert Captain when material, preserve the prior node, and require evidence for replacement.

## 13. Current Versus Target Readiness

| Capability | Current | Target |
|---|---|---|
| Legacy Doctor seat | **AS-BUILT** | Migrated Counsellor role |
| Intervention department | Not built | S5 staffed department |
| CMO/Counsellor split | Design | Enforced detection/treatment boundary |
| Direct Captain line | Design metadata | Purpose-bound enforced route |
| Personal staff cell | Not built | Advisor + PA + Personal Engineer |

## 14. Evidence And Hull-Stress

Evidence: `docs/system/ship-manual.md` sections 2, 3, 10-15; `docs/design/ship-org-design.md`
sections 2-4 and 9; `roles/direct/doctor.md`; `config/agents.json`; `config/ship-officer-routes.json`.

Hull-stress: the legacy Doctor's ship-brain duties and target Counsellor intervention duties are not fully
migrated. Direct-line precedence, sensitive-data policy, intervention crew, and reach mechanics need proof.
