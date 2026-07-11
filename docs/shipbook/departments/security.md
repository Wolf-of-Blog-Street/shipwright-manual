---
title: Security Department Book
seat: security.officer
rank: Lieutenant Commander
status: configured endpoint; instruments partly as-built; officer unmanned
---

# Security Department Book

> **CONTACT ROUTES ARE DESIGN, NOT ENFORCEMENT.** Security's direct Captain alert lane is named,
> but peer adjacency is not checked by the current runtime. Security does not monitor or command the Captain.

## 1. Commission, Rank, Reporting, And Current State

The Security Officer is a Lieutenant Commander under No1 with a direct Captain line for security alerts.
The endpoint is **CONFIGURED / UNMANNED**. Grant, inventory, spend-watch, and custody instruments are partly
**AS-BUILT** independently of the seat. A locked officer and complete department are **TARGET**.

## 2. Mission, Owned Decisions, And Non-Responsibilities

Security owns provenance security, privilege review, grant registry integrity, credential custody,
revocation, quarantine, and rogue-watch. It hunts misuse and wrongdoing. It does not monitor the Captain,
diagnose minds, originate missions, allocate operating budgets, or treat every defect as malicious.

## 3. Department Roster

| Element | Role | Current truth |
|---|---|---|
| Security Officer | Commissioned head | **CONFIGURED / UNMANNED** |
| Grant and key instruments | Registry, inventory, watch, custody | Partly **AS-BUILT** |
| Security monitoring crew | Misuse and privilege analysis | **TARGET** |
| Quarantine/revocation lane | Pull access and contain | Partly procedural; full enforcement **UNVERIFIED** |
| Personal Advisor, PA, Engineer | Private officer cell | **TARGET** |

## 4. Inbound Orders And Accepted Route Types

Accept routine `command_order` work through No1 and governance checks from Ops. Security may send direct,
evidence-backed alerts to the Captain without routing through a suspected seat. A security finding is not
permission to enlarge surveillance, seize command, or invent a grant.

## 5. Officer Contact Matrix

| Contact | Purpose | Route | Authority | Status |
|---|---|---|---|---|
| No1 | Routine security work and remediation | `no1-security` | No1 runs department | **TARGET / NOT ENFORCED** |
| Captain | Material security and rogue-watch alert | `security-captain-alert` | Report only; Captain decides | **TARGET / NOT ENFORCED** |
| Operations | Privilege, credential, allocation, revocation | `ops-security-resource-check` | Stage ownership, no peer command | **TARGET / NOT ENFORCED** |
| CMO | CMO watches Security for defects/drift | Observability surface, not command | CMO cannot operate Security | **TARGET / UNVERIFIED** |
| Intelligence / Comms | Source or outbound security concern | Through No1 unless incident | No direct command | **UNVERIFIED** |

## 6. Personal Staff Cell

The target cell is `advisor.security`, `pa.security`, and `engineer.security`. It serves the Security Officer
privately and does not inherit credential custody by default. Personal staff receive only named,
purpose-bounded access; no Advisor or Scientist receives operational keys.

## 7. Tools And Access

The target officer has standard locked tools. Credential inventory and issue/revoke operations must be
typed, externally custodied, least-privilege, and fully logged. No secret value enters a manual, Brain,
packet, prompt, or Bridge projection. Technical tools run through scoped staff or governed execution lanes.

## 8. Boards, Records, Memory, And Single Writer

The Security Officer owns the target Security board and findings register; its PA transcribes. The grant
registry and key inventory remain separate authoritative instruments with pointer/fingerprint data only.
Security Brain stores reusable security judgment, never live credentials or unverified accusations.

## 9. Standard Workflows And Acceptance

Request -> verify authenticated authority -> classify privilege -> check grant/scope -> issue constrained
credential or deny -> monitor usage -> revoke/quarantine on evidence -> notify No1 and direct-alert Captain
when material -> preserve evidence -> close only after independent verification and explicit acceptance.

## 10. Spend, Grants, Custody, And Metering

Security does not create grants or choose budgets. Commodore authorization flows through Captain; Ops owns
resource intake/allocation; Security verifies privilege and holds issuance/revocation. Custody-class movement
requires canary, human gate, movement record, and watch. Missing cost evidence remains `unknown`.

## 11. Telemetry And Provenance

Emit authenticated request, grant, privilege decision, credential fingerprint/pointer, scope, issuer,
revocation, quarantine, alert, evidence, remediation, reviewer, and outcome. Redact secret material before
persistence. CMO reads the observable surface to detect Security's own defects.

## 12. Failure, Quarantine, Rollback, And Recovery

Fail closed on missing authority, grant, custody, provider limit, or provenance. Revoke exposed or overbroad
credentials, quarantine affected lanes, preserve immutable evidence, and direct-alert the Captain. Recovery
requires new scoped credentials, verified containment, and explicit reauthorization; never reuse a leaked key.

## 13. Current Versus Target Readiness

| Capability | Current | Target |
|---|---|---|
| Security Officer | **CONFIGURED / UNMANNED** | Locked staffed seat |
| Registry/inventory/watch | Partly **AS-BUILT** | Officer-owned typed integration |
| Credential isolation | Partial custody | External, revocable per-seat limits |
| Direct alert route | Design metadata | Enforced and tested |
| Personal staff cell | Not built | Advisor + PA + Personal Engineer |

## 14. Evidence And Hull-Stress

Evidence: `docs/system/ship-manual.md` sections 2, 3, 10-15; `docs/design/ship-org-design.md`
sections 2, 3, and 5; `docs/system/spend-governance.md`; `ship/captain-harness/src/staff.mjs`;
`config/ship-officer-routes.json`.

Hull-stress: the officer, watcher crew, per-seat provider-limit provisioning, enforced alert adjacency, and
complete external custody are not proven. Existing instruments must not be attributed to an unmanned seat.
