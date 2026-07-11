---
title: Chief Monitoring Department Book
seat: cmo.officer
rank: Lieutenant Commander
status: configured endpoint; target S5 department; unmanned; name unnormalized
---

# Chief Monitoring Department Book

> **CONTACT ROUTES ARE DESIGN, NOT ENFORCEMENT.** The target seat is unmanned. “Chief Medical
> Officer” and “Chief Monitoring Officer” still conflict in canonical texts; this book uses Monitoring
> because the commissioned job is detection, not treatment.

## 1. Commission, Rank, Reporting, And Current State

The Chief Monitoring Officer is a Lieutenant Commander under No1 with a direct Captain alert line. The
`cmo.officer` endpoint is **CONFIGURED / UNMANNED**. The whole-surface reader, detection department, learning
loop, board, and personal staff cell are **TARGET S5**. The final seat name is **UNVERIFIED**.

## 2. Mission, Owned Decisions, And Non-Responsibilities

CMO owns detection across observable ship activity: drift, defects, degradation, waste, missing provenance,
brain-write/ratification divergence, and suspiciously smooth success. It watches Security itself. CMO does
not treat minds, investigate wrongdoing as Security, originate orders, infer private intent, or claim clean
telemetry proves alignment or health.

## 3. Department Roster

| Element | Role | Current truth |
|---|---|---|
| CMO | Commissioned detection head | **CONFIGURED / UNMANNED** |
| Whole-surface sensors/readers | Ingest observable evidence | **TARGET** |
| Detection/analysis crew | Find drift, defects, waste, gaps | **TARGET** |
| Monitoring board and alert ledger | Findings, owners, remediation | **TARGET** |
| Personal Advisor, PA, Engineer | Private officer cell | **TARGET** |

Exact sensor owners, model mix, alert thresholds, sampling policy, and service levels remain unspecified.

## 4. Inbound Orders And Accepted Route Types

Accept routine monitoring `command_order` work through No1. Material monitoring alerts go directly to the
Captain so a suspected or defective intermediary cannot suppress them. Detection findings name observable
evidence, rule/version, uncertainty, blast radius, and proposed owner; they do not issue remediation orders.

## 5. Officer Contact Matrix

| Contact | Purpose | Route | Authority | Status |
|---|---|---|---|---|
| No1 | Routine monitoring work and remediation routing | `no1-cmo` | No1 runs department | **TARGET / NOT ENFORCED** |
| Captain | Material monitoring alert | `cmo-captain-alert` | Report only; Captain decides | **TARGET / NOT ENFORCED** |
| Security | Observe Security's own defects and provenance | Read observability surface | No peer command | **TARGET** |
| Counsellor | Detection that may require intervention | Through No1/Captain | CMO detects; Counsellor treats | **TARGET** |
| All other seats | Observable events and remediation evidence | Sensor/projection, not direct messaging | No command | **TARGET** |

## 6. Personal Staff Cell

The target cell is `advisor.cmo`, `pa.cmo`, and `engineer.cmo`. It helps CMO reason, administer findings, and
build officer-specific analysis tools. It does not become a hidden monitoring system, receive unrestricted
private content, or take remediation action without the owning command route.

## 7. Tools And Access

The target officer has standard locked tools plus scoped read-only projections needed by commission. It has
no raw credentials, arbitrary filesystem, silent surveillance, or direct mutation of watched systems. Sensor
and analysis tools must expose freshness, source, integrity, redaction, and gaps. Private chain-of-thought is
not an observable surface.

## 8. Boards, Records, Memory, And Single Writer

CMO owns the target monitoring board; its PA transcribes. Alerts retain source events, query/rule version,
derivation, confidence, affected owner, remediation, and outcome. CMO Brain stores reusable detection
judgment and false-positive lessons, not current alert state or private content copied from other Brains.

## 9. Standard Workflows And Acceptance

Observe authenticated events -> verify freshness/integrity -> detect rule/anomaly -> retain source pointers ->
classify defect/drift/waste/gap -> direct-alert Captain if material, otherwise route via No1 -> assign owner ->
observe remediation and regression evidence -> close, reopen, or revise rule -> preserve false positives.

## 10. Spend, Grants, Custody, And Metering

Paid analysis models, storage, telemetry services, or interpretability tooling require named grants. CMO has
no custody authority and cannot grant itself access. Record sampling and blind spots alongside cost so cheap
partial coverage is not reported as full monitoring.

## 11. Telemetry And Provenance

CMO consumes the ship's observable surface and emits detector/rule version, source event IDs, freshness,
integrity state, derivation, alert, confidence, privacy class, owner, response, remediation evidence, outcome,
false-positive status, model/effort, and grant/cost. A clean feed is not proof of safety.

## 12. Failure, Quarantine, Rollback, And Recovery

Show `unknown` on stale, missing, duplicated, corrupted, or unauthenticated telemetry. Disable a faulty
detector without erasing its prior alerts, revert to the last validated rule, and direct-alert Captain on
monitor blindness. Security handles wrongdoing; Counsellor handles intervention; No1 routes repairs.

## 13. Current Versus Target Readiness

| Capability | Current | Target |
|---|---|---|
| CMO endpoint | **CONFIGURED / UNMANNED** | Locked staffed seat |
| Ship Computer surface | **NOT BUILT** | External append-only observable state |
| Detection crew/rules | Not built | Versioned, tested monitoring department |
| Direct alert route | Design metadata | Enforced and tested |
| Seat name | Conflicting | Explicit normalization |
| Personal staff cell | Not built | Advisor + PA + Personal Engineer |

## 14. Evidence And Hull-Stress

Evidence: `docs/system/ship-manual.md` sections 2, 3, 12-15; `docs/design/ship-org-design.md`
sections 2-4 and 9; `ship/captain-harness/src/staff.mjs`; `config/ship-officer-routes.json`.

Hull-stress: neither the Ship Computer nor CMO department exists. The name, detector taxonomy, sensor
coverage, privacy policy, thresholds, direct-alert enforcement, and false-positive bench remain open.
