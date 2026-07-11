---
title: Communications Department Book
seat: comms.officer
rank: Lieutenant Commander
status: configured endpoint; capability-triggered target; unmanned
---

# Communications Department Book

> **CONTACT ROUTES ARE DESIGN, NOT ENFORCEMENT.** Communications is not staffed. The one-mouth
> doctrine does not make a configured endpoint a working review or delivery channel.

## 1. Commission, Rank, Reporting, And Current State

The Communications Officer is a Lieutenant Commander under No1. The `comms.officer` endpoint is
**CONFIGURED / UNMANNED**. A locked officer, department, glossary, outbound review loop, failure queue,
and complete Security-visible channel are **TARGET** after the capability trigger.

## 2. Mission, Owned Decisions, And Non-Responsibilities

Communications owns crafted human-facing external output: language, writing, presentation, glossary,
channel consistency, and final review. It is the ship's scoped external mouth. It does not control flag
traffic, substrate traffic, authenticated VCS/API transport, Intelligence fetches, or other enumerated
carve-outs; it does not censor internal evidence or change the originating officer's decision.

## 3. Department Roster

| Element | Role | Current truth |
|---|---|---|
| Communications Officer | Commissioned head | **CONFIGURED / UNMANNED** |
| Editorial/review crew | Craft, language, glossary, final review | **TARGET** |
| Outbound queue | Review, release, failure handling | **TARGET** |
| Security-visible log | Auditable outbound record | **TARGET** |
| Personal Advisor, PA, Engineer | Private officer cell | **TARGET** |

Internal manager roles, models, channel adapters, service levels, and stand-up trigger need specification.

## 4. Inbound Orders And Accepted Route Types

Accept `command_order` communication work through No1 with audience, intent, facts, source evidence,
channel, sensitivity, deadline, acceptance, and authorized sender. Communications may improve craft but
must not silently change factual claims, authority, policy, or mission intent.

## 5. Officer Contact Matrix

| Contact | Purpose | Route | Authority | Status |
|---|---|---|---|---|
| No1 | Commission crafted output and receive review result | `no1-communications` | No1 runs department | **TARGET / NOT ENFORCED** |
| Security | Monitoring, sensitivity, and incident handling | Through No1 or incident route | No peer command | **UNVERIFIED** |
| Originating officer | Factual clarification and approval | Through No1/packet | Originator owns facts and decision | **TARGET** |
| External recipient | Authorized crafted output | Governed outbound channel | No command | **TARGET / NOT BUILT** |
| Commodore/Captain flag lane | Not a Communications gate | Separate authenticated flag channel | Outside department | **EXPLICIT CARVE-OUT** |

## 6. Personal Staff Cell

The target cell is `advisor.comms`, `pa.comms`, and `engineer.comms`. It serves the Communications Officer,
not the ship's authors generally. The Advisor supports craft judgment, the PA handles records and sourced
checks, and the Personal Engineer builds officer-specific channel or review tools.

## 7. Tools And Access

The target officer has standard locked tools. Channel send, review, translation, formatting, and artifact
operations occur through typed department tools and scoped staff. No ambient email, social, publishing, or
credential access is permitted. A send tool must bind authorized sender, channel, audience, and final hash.

## 8. Boards, Records, Memory, And Single Writer

The Communications Officer owns the target Communications board; its PA transcribes. The glossary,
outbound queue, approved artifact/hash, source packet, channel receipt, correction, and failure queue are
durable records. The officer Brain stores reusable communication judgment, not unapproved drafts as policy.

## 9. Standard Workflows And Acceptance

Commission -> verify sender authority and carve-out -> retain source facts -> craft draft -> factual diff ->
glossary/style check -> sensitivity/Security check -> originator approval where required -> send through
authorized channel -> retain exact output and receipt -> report or queue failure.

## 10. Spend, Grants, Custody, And Metering

Paid translation, media, model, channel, or distribution services need named grants. Communications holds no
ambient channel credentials. Ops allocates budget and Security issues revocable access. Record exact billed
cost or explicit unknown; never hide channel charges in general ship operations.

## 11. Telemetry And Provenance

Emit source order, originator, source facts/hash, draft revisions, reviewers, model/effort, glossary version,
sensitivity decision, final hash, sender identity, channel, destination class, send receipt, cost, correction,
and failure state. Redact recipient secrets from broad projections.

## 12. Failure, Quarantine, Rollback, And Recovery

Queue rather than bypass a failed channel or missing reviewer. Stop on unverified facts, ambiguous sender,
credential leakage, unauthorized audience, or material draft/source divergence. Quarantine bad credentials,
issue corrections through the same governed channel, and preserve both original and corrected records.

## 13. Current Versus Target Readiness

| Capability | Current | Target |
|---|---|---|
| Officer endpoint | **CONFIGURED / UNMANNED** | Locked Communications Officer |
| One-mouth final review | Not live | Auditable scoped channel |
| Glossary and queue | Not proven | Versioned records |
| Channel credentials | No officer custody | Brokered, revocable access |
| Personal staff cell | Not built | Advisor + PA + Personal Engineer |

## 14. Evidence And Hull-Stress

Evidence: `docs/system/ship-manual.md` sections 2, 3, 11-15; `docs/design/ship-org-design.md`
sections 2, 3, 7, and 9; `ship/captain-harness/src/staff.mjs`; `config/ship-officer-routes.json`.

Hull-stress: the stand-up trigger, exact carve-out enforcement, channel adapters, delivery receipts, internal
crew, correction process, and failure doctrine are target descriptions rather than proven runtime behavior.
