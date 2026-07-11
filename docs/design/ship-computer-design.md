---
date_created: 2026-07-10
date_updated: 2026-07-10
status: DESIGN - NOT BUILT
owner: Chief Engineer, Shipwright
implementation_route: Chief Engineer -> Incubator PM -> Incubator engineering department
---

# Ship Computer - architecture design

## 0. Status and decision

**The Ship Computer described here is NOT BUILT.**

Shipwright currently has useful observability precursors: a hash-chained Captain event ledger, a
read-only Bridge normalizer, local Bridge JSON endpoints, runner and board evidence, cost ledgers,
and a configured target organization. Those parts do not yet form the Ship Computer. In particular,
there is no independent event service, canonical command ledger, transactional delivery plane,
external canonical telemetry store, authenticated sensor ingestion, live event stream, complete
coverage registry, or enforced query policy.

This document is the implementation specification for that system. The name is **Ship Computer**.
It is the ship's instrumented nervous system and durable operational record. It observes, records,
correlates, and presents ship activity. It does not command the ship.

"Everything" in this design means every event available at an instrumented, governed boundary. It
does not mean inaccessible provider internals, private model chain-of-thought, uninstrumented
activity, or secrets. Gaps must be visible as gaps; the system must never imply omniscience.

## 1. Purpose

The Ship Computer gives the Commodore and authorized ship staff one live, provenance-backed answer
to five questions:

1. What is every observable part of the ship doing now?
2. What orders, messages, model calls, tools, tasks, files, workspaces, tests, and releases led here?
3. Which statements are direct records, which are derived, and which are configuration only?
4. What did the work cost, under which grant, and which model and tool produced it?
5. Where is observation absent, delayed, invalid, or unable to establish the truth?

The Bridge dashboard is the primary human presentation. The Ship Computer owns the normalized event
plane and query API that feeds it. Other authorized clients may consume the same API.

## 2. Boundaries

### 2.1 The Ship Computer is

- An append-only telemetry intake and canonical observation log.
- A normalized index over ship events and their source evidence.
- A correlation engine for orders, tasks, model calls, tool calls, workspaces, tests, and seals.
- A health and coverage registry for every expected sensor.
- An authenticated query service and Server-Sent Events (SSE) stream.
- A source of live state for the Bridge.
- A tamper-evident record, with explicit limits on what tamper evidence proves.

### 2.2 The Ship Computer is not

- A Captain, officer, manager, PA, Advisor, or worker.
- An autonomous command author, order approver, release authority, landing broker, or board writer.
- A substitute for source records, acceptance tests, human judgment, or external custody.
- A credential vault.
- A claim that recorded statements are factually correct.
- A private-reasoning recorder.
- Permission for any AI agent to write the main working copy.

The Computer may report that an actor said a task was complete. It may report a verified test receipt
or sealed change proving part of that claim. It may not collapse those two facts into the same truth.

### 2.3 Control-plane separation

The Ship Computer owns the canonical command ledger and reliable delivery records described in
Section 5. That makes it a command transport and record, not a command mind. It may accept and deliver
an authenticated typed order from an actor who already holds authority. It may not originate an
objective, approve an order, expand scope, choose a recipient, close a mission, change a board by its
own judgment, edit memory, land changes, move funds, send an uncommissioned external message, or
modify grants.

Command-write credentials, sensor-ingest credentials, and dashboard-read credentials are separate.
The Bridge must visually distinguish observation controls from authenticated command actions. A
compromised dashboard read token must not become command authority.

## 3. Governing truths

### 3.1 Evidence classes

Every normalized event carries exactly one `truth_class`:

| Class | Meaning | Example |
|---|---|---|
| `recorded` | A sensor durably observed an event at its own boundary | The model gateway returned a visible response |
| `receipt` | A named system returned a result that can be checked at its boundary | A connector returned a message ID; a test runner returned exit 0 |
| `reported` | An actor asserted something without independent confirmation | An officer reported an order complete |
| `derived` | The Computer inferred a state from one or more records | A process is probably stale because its PID is absent |
| `configured` | A declaration of intended capacity, not execution | An Advisor thinking slot exists but is disabled |
| `unknown` | Evidence is missing, invalid, or insufficient | Cost data was not returned by the provider |

The UI must display the class. Derived state must retain links to all input events and the derivation
rule version. Configuration must never light a seat as active.

### 3.2 Record supremacy without record worship

A verified sealed record wins over recollection about what was recorded. It does not prove that the
record's author was correct, that an external side effect occurred, or that a compromised sensor was
honest. Important claims require independent receipts or cross-source corroboration.

### 3.3 Observable and hidden

The Computer records, after redaction:

- Operator prompts submitted to an instrumented model runtime.
- Model-visible responses returned to the harness.
- Tool names, arguments, results, errors, timing, and side-effect receipts.
- Orders, amendments, cancellations, acceptance, rejection, delivery, and reports.
- Model, provider, effort, token, latency, fallback, refusal, and cost metadata.
- Task, board, workspace, file-change, test, landing, seal, and release events.
- Connector operations and provider receipts.
- Brain and memory operations as typed events, including authorization and changed-node identity.
- Process starts, stops, heartbeats, crashes, retries, queues, and backpressure.

The Computer cannot record:

- Provider-hidden reasoning or private chain-of-thought.
- Activity outside an instrumented boundary.
- Facts that a provider or external system does not expose.
- Secrets removed before intake.

For models that expose an explicit user-visible reasoning summary, that summary is a normal visible
output and may be recorded after redaction. It is not treated as the model's complete internal state.

### 3.4 Memory strata

The ship has several kinds of memory with different owners and authority. The Ship Computer brings
operational memory to life without collapsing those stores:

| Stratum | Purpose and owner | Ship Computer relationship |
|---|---|---|
| Ship Computer event/operational memory | Append-only account of observable actions, command lifecycle, evidence, and current projections | Owns normalized operational events and command revisions |
| Captain/officer Brain | Private cognition: beliefs, conclusions, and durable personal knowledge owned by that mind under its PA process | Observes authorized typed stage/ratify/write events and links node IDs; does not read beyond policy or write the Brain |
| Ship Brain | Curated shared semantic, doctrine, and institutional knowledge | Observes governed proposal/ratification/write events and source IDs; does not silently curate or replace it |
| Current and scratchpads | Ephemeral working memory, focus, active blockers, and temporary synthesis | Records typed access/change metadata and authorized snapshots where policy permits; does not treat working notes as doctrine |
| Sealed records | Immutable decisions, evidence, reports, and releases that carry record supremacy | Links seal IDs and digests, verifies continuity, and never edits the sealed artifact |

A Computer event that says `brain.write.completed` proves that the governed Brain boundary returned a
write receipt. It does not make the written belief correct, public, or command authority. Brain,
memory, current, and scratchpad adapters preserve owner, authorization, operation ID, affected node or
artifact ID, before/after digest where permitted, and the event that caused the operation.

The Computer cannot silently promote scratchpad text to Brain, private Brain content to Ship Brain,
an event summary to doctrine, or an unsealed report to a sealed record. Each crossing uses the owning
store's existing typed governance and produces a separately authorized event.

## 4. Organizational fit

Rank, model, tool access, and observation scope are separate fields.

- The Commodore is the human flag authority and receives the broadest sanitized ship view.
- The Captain commands Shipwright under the Commodore.
- No1 is a Commander and runs ship departments under the Captain.
- Commissioned ship officers are Lieutenant Commanders unless specifically recorded otherwise.
- The Chief Engineer is a commissioned Lieutenant Commander. He owns this design and the logged
  handoff to the external Incubator PM.
- Department managers and Personal Engineers are Lieutenants.
- Advisors are non-line Warrant Officers.
- PAs are Chief Petty Officers.
- PA operators are Petty Officers or specialist crew.
- Thinking partners are Ensigns with the non-line Scientist support designation.
- Engineering workers are Ensigns.
- The Incubator PM is an external Lieutenant Commander and remains Incubator's orchestrator and
  direct human interface.

Every Captain and commissioned officer has the same target personal cell:

1. Thinking: Advisor plus configured thinking partners.
2. Operations: PA plus configured operator team and officer-scoped human-brain.
3. Engineering: Personal Engineer plus isolated workers.

The Computer must represent each personal cell as a first-class subtree with distinct identities,
queues, boards, models, grants, workspaces, and coverage. A personal Advisor event must not be
misattributed to Science. A PA operation must not be rendered as a separate mini-ops officer. Broad
ship engineering must remain distinguishable from Personal Engineering and from Incubator work.

## 5. Canonical command graph and no-loss work ledger

### 5.1 Command doctrine

The Ship Computer command ledger is canonical for ship work authorization and lifecycle. Boards are
projections and work queues over that ledger. They are not a second source of command authority.

The Commodore sets directives and standing authority. The Captain is the sole ship work authorizer
under that direction. Officers may decompose an authorized order within its scope; they may not
create an independent ship mission or enlarge its authority. Managers may break authorized work into
tasks. Workers execute assignments; they do not create authority.

The no-loss rule is:

```text
Commodore directive or standing authority
  -> Captain-owned mission
  -> measurable objective
  -> typed order and route
  -> epic / task / subtask
  -> one or more attempts
  -> evidence and report
  -> Captain decision
  -> accepted closure, revision, rejection, cancellation, or supersession
```

Every node and lifecycle event has an immutable ID. Every executable node has exactly one primary
command parent and one `root_mission_id`. Secondary `contributes_to` links are allowed for discovery
and shared outcomes; they never replace or weaken the primary lineage.

No orphan work is accepted, dispatched, landed, paid, or reported complete. An unsolicited alert,
sensor finding, external request, or proposal enters the Captain intake as non-executable work. The
Captain explicitly adopts it into a mission/order chain or declines it. Emergency containment may
begin only under an already active, versioned standing order; its invocation supplies the missing
authority lineage immediately.

### 5.2 Three typed planes

The graph separates authority, execution, and return. This prevents a task or report from silently
becoming authority.

| Plane | Types | Purpose |
|---|---|---|
| Authority | `directive`, `standing_order`, `standing_order_run`, `mission`, `objective`, `order` | Establish why work is lawful, owned, bounded, and accepted |
| Execution | `epic`, `task`, `subtask`, `attempt` | Decompose and perform authorized work without expanding it |
| Return | `evidence`, `report`, `decision` | Return artifacts and claims, then record acceptance or next action |

`intake_item` is a pre-authority holding type. It is never executable. It exists only so unrequested
findings cannot bypass Captain adoption.

### 5.3 Common typed record

Every graph node has this common immutable identity and versioned body:

```json
{
  "schema": "falcon.command-node",
  "schema_version": 1,
  "node_id": "MIS-01J...",
  "node_type": "mission",
  "record_version": 3,
  "root_authority_id": "DIR-01J...",
  "root_mission_id": "MIS-01J...",
  "primary_parent_id": "DIR-01J...",
  "contributes_to": [],
  "created_by": "captain.canopus",
  "accountable_owner": "captain.canopus",
  "executing_owner": null,
  "destination_kind": "seat",
  "destination_id": "captain.canopus",
  "route_kind": null,
  "authority_basis": "DIR-01J...",
  "title": "Build live ship observability",
  "objective": "A bounded outcome, not implementation steps",
  "constraints": [],
  "expected_outcomes": [],
  "metrics": [],
  "acceptance_criteria": [],
  "evidence_requirements": [],
  "resource_links": [],
  "grant_id": null,
  "budget_id": null,
  "risk_level": "normal",
  "hold_reason": null,
  "canonical_phase": "authorized",
  "type_state": "commissioned",
  "created_at": "2026-07-10T20:00:00.000Z",
  "effective_at": "2026-07-10T20:00:00.000Z",
  "deadline_at": null,
  "supersedes_id": null,
  "cancel_reason": null,
  "idempotency_key": "captain:ship-computer:v1"
}
```

Updates append a new `record_version`; they never replace an earlier version. The current snapshot is
the highest valid version after transition validation. `node_id`, `node_type`, `created_by`, primary
lineage, and original authority basis cannot change. Revision, cancellation, and supersession use
typed transitions and new linked nodes or versions.

Non-executable authority definitions use `root_authority_id = node_id`. A directive or
standing-order definition does not have a `root_mission_id` until it produces or attaches to a
mission. A mission has `root_mission_id = node_id`. Every order, execution node, return node, and
event below a mission inherits that exact mission ID.

### 5.4 Common phase and type-specific state

The Bridge uses one canonical phase vocabulary:

`proposed`, `authorized`, `queued`, `delivered`, `acknowledged`, `active`, `blocked`,
`return_pending`, `review`, `accepted`, `closed`, `failed`, `cancelled`, `held`, `superseded`, and
`declined`.

Each node also retains a stricter `type_state`. The transition registry maps type-specific states to
the canonical phase. The API rejects any transition not present in the versioned registry. A UI
client cannot invent a transition by writing a board status.

Terminal states are immutable except for an appended correction that preserves the original terminal
record. `cancelled`, `superseded`, and `failed` are not synonyms for `closed`. A late report after
cancellation remains evidence but cannot reactivate or close the cancelled work.

### 5.5 Type semantics

| Type | Meaning and owner | Who may create | Required type-specific fields | Type-specific lifecycle |
|---|---|---|---|---|
| `directive` | One Commodore instruction; Commodore owns authority, Captain owns response | Commodore or authenticated flag-channel transcriber | issuer, text, priority, effective time, acknowledgement requirement | `issued -> acknowledged -> adopted/clarification_requested -> fulfilled/superseded/revoked` |
| `standing_order` | Versioned reusable authority definition | Commodore; Captain within delegated scope | scope, issuer, authority basis, trigger, constraints, owner, review, expiry | `draft -> active -> held -> active`, or `revoked/expired/superseded` |
| `standing_order_run` | One idempotent activation of one standing-order version | Trigger service under the active definition | standing-order ID/version, trigger evidence, occurrence key, mission/order attachment | `detected -> suppressed/queued -> acknowledged -> active -> reported -> accepted/failed/cancelled` |
| `mission` | Captain-owned root of executable ship work | Captain only; standing-order service acts only as pre-authorized Captain transport | authority basis, intent, scope, constraints, success definition, review cadence | `proposed -> commissioned -> active -> review -> accepted/closed`, or `held/cancelled/superseded` |
| `objective` | Measurable outcome within one mission | Captain, or a named officer proposing for Captain authorization | metric or observable outcome, target, acceptance, deadline/review | `draft -> authorized -> active -> review -> met/not_met/revised/cancelled` |
| `order` | Delegates bounded authority and acceptance to a named destination | Captain; commissioned officers only within a parent order's explicit delegation | issuer, route, destination, objective, constraints, autonomy margin, acceptance, evidence, ack SLA | `draft -> issued -> delivered -> acknowledged/accepted/rejected -> executing -> reported -> accepted/revised/cancelled` |
| `epic` | Officer/manager work package; never authority by itself | Accountable recipient or authorized manager | parent order, bounded scope, owner, expected return, completion gate | `planned -> ready -> active -> blocked -> review -> done/failed/cancelled` |
| `task` | Executable unit assigned to a named responsible owner | Officer, PA, or manager within parent scope | output, owner, dependencies, acceptance, return route | `to_do -> ready -> assigned -> active -> blocked -> review -> done/failed/cancelled` |
| `subtask` | Smaller executable unit under one task | Task owner or manager | same as task plus task parent | `to_do -> assigned -> active -> review -> done/failed/cancelled` |
| `attempt` | One concrete run by one model, person, agent, or process | Execution runtime or dispatcher | executor, runtime/model/tool, start, input refs, budget, terminal result | `created -> started -> succeeded/failed/timed_out/aborted`; never retried in place |
| `evidence` | Immutable artifact, receipt, measurement, test, or source | Sensor, executor, verifier, or connector | evidence kind, digest, source, producer, capture time, claim supported | `captured -> validated/rejected/quarantined`; content never edited |
| `report` | A named actor's return against an order or task | Accountable or executing owner | findings, outcome claim, evidence IDs, gaps, return recipient | `draft -> submitted -> received -> under_review -> accepted/revision_requested/rejected` |
| `decision` | Explicit authority action on returned work | Captain for mission/objective/final order closure; delegated owner for subordinate review | decision kind, subject, reasons, evidence considered, next action | `recorded`; correction appends a superseding decision |
| `intake_item` | Non-executable proposal, alert, or request awaiting Captain adoption | Sensors, authorized seats, or authenticated external interfaces | origin, urgency, claim, evidence, requested disposition | `received -> triaged -> adopted/declined/duplicate/quarantined` |

An `attempt` success does not complete its task. A task marked done does not accept an order. A report
does not close an objective. Only the actor holding the relevant acceptance authority may append the
corresponding decision. Final mission closure requires a Captain decision linked to objective and
evidence state.

### 5.6 Typed routing and destinations

Every order or request names a destination and route. Human-readable text cannot determine routing.

Destination kinds:

- `seat`: one authenticated commissioned or staff identity.
- `department`: one commissioned officer's ship department, accountable to that officer.
- `personal_cell`: one officer's Thinking, Operations, or Engineering cell.
- `external_interface`: a named governed boundary, initially Chief Engineer to Incubator PM.

Route kinds:

| Route | Valid destination | Meaning | Expected return |
|---|---|---|---|
| `command_order` | Commissioned seat or department | Delegated command authority within a bounded objective | Typed report plus required evidence |
| `consult` | Personal Advisor/Thinking cell or authorized peer | Non-line cognitive consultation; no command authority | Advice/synthesis with uncertainty and source refs |
| `ops_request` | Owning officer's PA/Operations cell | Personal operations, research, records, connectors, scheduling | Artifact/receipt/sourced packet and ops report |
| `engineering_brief` | Owning officer's Personal Engineer | Bounded personal tooling or prototype build | Tested artifact, workspace/change IDs, engineering report |
| `science_commission` | Science Officer/Science department | Broad asynchronous inquiry over hours or days | Evidence-backed Science report |
| `factory_work_order` | Chief Engineer's Incubator external interface | Broad build routed only through external Incubator PM | PM receipt, factory evidence, sealed returned change/report |
| `report_return` | The accountable issuer or named return seat | Return path only; cannot create new authority | Report, evidence, or decision request |

Every routed record includes `accountable_owner`, `executing_owner`, `destination_kind`,
`destination_id`, `route_kind`, `ack_sla`, `expected_return_type`, `return_to`, `root_mission_id`,
`objective_id`, and `primary_parent_id`.

Routing constraints are structural:

- Advisors and thinking partners are non-line. They receive `consult`, never a command order.
- PAs receive `ops_request`; they do not decide the officer's objective.
- Personal Engineers receive `engineering_brief` for officer-specific work.
- Science receives `science_commission` for broader asynchronous inquiry.
- Commissioned officers and sections receive `command_order`.
- Incubator receives work only through the Chief Engineer's logged external interface to the distinct
  Incubator PM. No Shipwright actor directly dispatches an Incubator manager or worker.
- The Captain does not bypass officers or managers to task anonymous workers. A named accountable
  owner decomposes and dispatches within the authorized order.
- Every route retains the same root mission and objective lineage through its return.

### 5.7 Standing orders

A standing order is a versioned definition, not an invisible permission. Each immutable version
contains:

- `standing_order_id`, `version`, `issuer`, authority basis, owner, and accountable Captain.
- Scope, permitted effects, explicit exclusions, budget/grant bounds, and required evidence.
- Trigger definition: recurring, scheduled, event-driven, or manual.
- Trigger source, evaluation window, timezone where applicable, and duplicate-suppression key.
- Mission template or an existing Captain-owned mission/order attachment rule.
- Ack SLA, completion SLA, escalation path, and maximum concurrent runs.
- Effective time, next review, expiry, and state: `active`, `held`, `revoked`, `expired`, or
  `superseded`.

Every trigger creates a `standing_order_run` with an immutable invocation ID and idempotency key made
from standing-order ID, version, and trigger occurrence. An invocation must create or attach to a
Captain-owned mission/order chain before execution. It carries `standing_order_id`, version, trigger
evidence, root mission, objective, and primary parent on every descendant.

Recurring and scheduled triggers maintain an expected-occurrence ledger. The Computer raises a
`missed_trigger` alert when an expected run is absent after its grace period. Event triggers retain
the source event ID. Manual triggers retain authenticated actor and reason. Repeated delivery of the
same occurrence returns the existing run; it never starts duplicate work.

Holding or revoking a definition stops new invocations immediately. Active runs follow the version's
declared suspension policy: finish, pause, or cancel. Revocation does not erase prior runs. Review and
expiry alerts begin before their deadlines. Queries can return a complete flow for any definition:
all versions, state changes, expected and actual triggers, suppressed duplicates, missed triggers,
runs, mission/order attachments, outcomes, evidence, and decisions.

### 5.8 Transactional outbox, inbox, and delivery

Creating an authorized routed node and its delivery outbox row is one database transaction. A work
item cannot exist in `issued` state without an outbox record. The outbox row contains the exact
immutable node version, destination, route, idempotency key, attempt count, next retry, and expiry.

The recipient transport inserts the envelope and recipient inbox receipt in one transaction. It then
returns an acknowledgement containing envelope ID, node/version, recipient identity, inbox sequence,
and receipt digest. Repeated delivery returns the same receipt. The sender marks the outbox
acknowledged only after validating that receipt.

Delivery behavior:

1. Retry unacknowledged envelopes with bounded exponential backoff and jitter.
2. Never create a new work ID on retry.
3. Alert at half the ack SLA and when the SLA expires.
4. Move exhausted deliveries to a visible dead-letter state; never drop them.
5. Require an authorized disposition: retry, reroute with a new linked route decision, cancel, or
   quarantine.
6. Reconcile ledger, outbox, destination inbox, recipient acknowledgement, and lifecycle events on a
   schedule and after every restart.

Delivery acknowledgement proves durable receipt, not acceptance or execution. The recipient records
`order.accepted` or `order.rejected` separately. Rejection includes a reason and returns to the issuer.

### 5.9 Cancellation, amendment, and supersession

An amendment appends a new version within the original authority and preserves the old version. If
scope, authority basis, accountable owner, or primary lineage changes, the issuer must supersede the
old node with a new node and explicit link.

Cancellation and supersession create high-priority delivery envelopes to every active descendant.
Each recipient acknowledges the control envelope and returns stopped, already committed, or unable
to stop. Completed evidence remains in the graph. Work performed after effective cancellation is
flagged `post_cancel_activity` and cannot be silently accepted.

### 5.10 Crash recovery and reconciliation

The command ledger is an append-only revision store in `command/commands.sqlite`. Its current-state
tables, transactional outbox, inbox receipts, and dead-letter rows are in the same SQLite database.
Each committed command revision also creates a telemetry outbox row in that transaction. The Ship
Computer event writer drains it into the canonical hash chain. Crash recovery therefore follows:

- Command committed, event not appended: telemetry outbox replay appends it.
- Envelope queued, not sent: delivery worker retries the same ID.
- Recipient persisted, sender missed ack: recipient returns the same receipt on retry.
- Ack persisted, projection not updated: projector replays ledger sequence.
- Report persisted, decision absent: stale-review alert remains until authorized decision.
- Board differs from ledger: ledger wins and the projector repairs or flags the board.

Startup does not infer success from a vanished process. It resumes only nonterminal delivery and
projection work. Execution attempts have terminal receipts or become stale/unknown for reconciliation.

### 5.11 Board projections and work queues

Officer, department, Captain, and personal-cell boards are destination-specific projections of the
canonical command graph. The projector creates or updates queue rows from accepted ledger revisions.
It records the last applied ledger sequence and a digest of the projected row.

Authorized board notes and local planning metadata may exist, but they cannot create executable work
without a command-ledger node. A board writer submits a typed ledger transition first; the projection
then changes. Reconciliation compares every open ledger node with its expected board projection and
alerts on missing, extra, or divergent rows.

### 5.12 No-loss invariants

The implementation enforces and continuously audits these invariants:

1. Every executable node has one and only one primary parent and a valid Captain-owned root mission.
2. Every root mission has a Commodore directive, active standing authority, or explicit Captain
   adoption decision within delegated authority.
3. Every issued route has one durable outbox row and eventually one ack, dead-letter, cancellation,
   or quarantine disposition.
4. Every accepted recipient inbox row has exactly one canonical source envelope.
5. Every attempt belongs to one task/subtask and preserves mission, objective, and order ancestry.
6. Every terminal work claim returns through evidence/report and an authorized decision.
7. No board-only row can be treated as authorized work.
8. Cancellation and supersession reach every nonterminal descendant or remain visibly unresolved.
9. No retry creates duplicate authority, work, side effects, or standing-order runs.
10. Every graph and delivery gap is visible in the Captain inbox and Bridge alerts.

### 5.13 Desired command state is not observed execution

The command graph records desired and authorized state. The provenance event graph records observed
execution. They are joined, never conflated.

- `queued` means a durable outbox exists. It does not prove delivery.
- `delivered` means a recipient inbox receipt exists. It does not prove acceptance.
- `assigned` means an accountable owner named an executor. It does not prove a process started.
- `active` requires observed start plus fresh liveness evidence under the event-family policy.
- `attempt.succeeded` means one run returned success. It does not prove the task acceptance passed.
- `task.done` is an execution claim. It does not close an order, objective, or mission.
- Closure requires the contracted report/evidence path and an authorized acceptance decision.

Every outbound command has a typed return contract: acknowledgement, progress cadence, report type,
required evidence, acceptance owner, acceptance criteria, and escalation deadline. Acceptance may be
delegated for subordinate epics or tasks only when the parent order explicitly names the delegate and
scope. Otherwise the issuing officer accepts the subordinate return. The Captain alone accepts final
mission and objective outcomes.

Desired-state projections and observed-state projections use separate fields in the Bridge. Both are
rebuildable from immutable command revisions and events. A projection cache is never authoritative.

### 5.14 Supporting concepts without hierarchy inflation

V1 deliberately stops at Mission as the root executable container. `campaign` and `program` are
reserved for a later schema version; they must not be introduced as aliases for Mission.

The following are first-class typed records or edges without becoming new parent containers:

- `intake_item` with kind `request`, `idea`, `incident`, or `alert`. It enters the Captain inbox and
  is non-executable until adopted. An incident may trigger pre-authorized containment only through a
  standing-order run.
- `depends_on` and `blocked_by` edges. They identify prerequisites and blockers but do not transfer
  authority or change primary lineage. A blocker has owner, reason, first-seen time, review time, and
  resolution event.
- `milestone` marker. It names a measurable checkpoint over one or more nodes; it is not a work
  container and cannot own tasks.
- `resource_link`, `grant_id`, and `budget_id`. They join work to the resource graph without making
  a budget record command authority.
- `artifact` and `evidence`. Artifact records describe produced material; evidence records state what
  claim a digest-addressed artifact or receipt supports.
- `risk` and `hold`. A risk record captures likelihood, impact, owner, mitigation, and review. A hold
  suspends permitted transitions without cancelling the underlying work.
- `change_reason`, `cancel_reason`, and `supersedes_id`. Every material revision, cancellation, or
  replacement explains why and identifies its authority.
- Expected outcome and metric records. Each objective names observable targets, measurement source,
  baseline where applicable, deadline, and acceptance threshold.

### 5.15 Joinable graphs

The Ship Computer exposes four distinct but joinable graphs:

1. **Command/work graph:** authority, execution, return, delivery, dependency, and acceptance.
2. **Organization graph:** identities, ranks, command relationships, departments, and personal cells.
3. **Provenance graph:** events, actors, model/tool runs, source evidence, and causal links.
4. **Resource graph:** grants, budgets, costs, credentials-as-opaque-references, infrastructure, and
   connector capacity.

IDs create joins across graphs, but no graph inherits another graph's semantics. A higher rank in the
organization graph does not prove authorization for a particular order. A cost allocation does not
prove command authority. An event does not become true because it belongs to a mission. A command
does not prove execution without provenance evidence.

## 6. High-level architecture

```text
Instrumented ship boundaries
  Captain and officer harnesses     Model gateways
  typed order/message transport     tool and connector gateways
  PAs, Advisors, personal cells     Science/panel runners
  boards and task services          workspace/landing broker
  jj and test/release adapters      Incubator handoff adapter
  process supervisors               cost/grant ledger
               |
               v
       Sensor adapters and local durable spools
               |                         |
       authenticated ingest API    authenticated command API
               |                         |
               v                         v
  +----------------------------------------------------------------+
  | Ship Computer                                                  |
  | event validator -> redactor -> dedupe -> chain writer          |
  | command ledger -> outbox/inbox -> delivery/reconciliation      |
  | projectors/indexer -> coverage registry -> health/gap detector |
  +----------------------------------------------------------------+
        | canonical event segments     | command ledger + query index
        | external, append-only         | external SQLite stores
        v                               v
       checkpoints               authenticated query API
                                          |
                                  SSE + snapshot/delta APIs
                                          |
                                     THE BRIDGE
```

### 6.1 Single writer, many sensors

Sensors never append directly to canonical segments. Each source writes to its own bounded durable
spool or calls the authenticated ingest endpoint. One Ship Computer writer validates and serializes
accepted observations. This gives the ship one accepted-observation order without pretending that
source clocks define causality.

### 6.2 Canonical logs, command ledger, and rebuildable projections

The canonical event segments are append-only JSON Lines files. `commands.sqlite` is the canonical
append-only command revision, delivery, and acceptance ledger because its transactional outbox must
commit with each command revision. Every command transaction emits a durable telemetry-outbox row;
the event writer drains it to the canonical event chain. Recovery reconciles both ledgers.

The general SQLite query index and all Bridge projections are materialized caches. They may be
rebuilt from verified event segments plus the command revision ledger. A projection row without
valid source revisions/events is invalid. Existing source ledgers remain evidence and are referenced
by digest; the Computer does not silently replace them.

## 7. External state store

Operational telemetry must not be written to the repository or an agent workspace. The default root
is:

```text
${SHIPWRIGHT_STATE_ROOT:-${XDG_STATE_HOME:-~/.local/state}/falcon-shipwright}/ship-computer/
  events/YYYY/MM/DD/segment-NNNNNN.jsonl
  checkpoints/YYYY/MM/DD.json
  command/commands.sqlite
  command/dead-letter/
  index/ship-computer.sqlite
  spools/<sensor-id>/*.jsonl
  quarantine/<sensor-id>/*
  runtime/service.json
```

Requirements:

- Directories are mode `0700`; files containing telemetry are mode `0600`.
- The service account is the only canonical-log writer.
- Both SQLite stores use WAL mode, foreign keys, and a bounded busy timeout.
- The command store contains immutable node revisions, typed edges, lifecycle events, transactional
  delivery outboxes, recipient receipts, dead letters, and telemetry outboxes.
- Canonical appends are flushed and `fsync` completed before acknowledgement.
- A segment is closed on size or UTC-day threshold, never rewritten, and checkpointed.
- Backups copy closed segments and checkpoints before the query index.
- Retention is policy-controlled by event class. Hashes and minimum audit metadata outlive optional
  large content blobs.
- Payloads too large for an event are stored as encrypted content blobs outside the repository;
  events contain the blob digest, media type, size, retention class, and authorization scope.
- The encryption key and any checkpoint signing key live in an OS keychain or external custodian,
  not in the repository, event store, prompt, or model environment.

The hash chain is tamper-evident, not tamper-proof. An attacker with the service account and all
checkpoint keys could rewrite history. Phase 4 adds externally held checkpoint custody so the ship
cannot silently rewrite a previously published head.

## 8. Event contract

### 8.1 Canonical envelope

Schema name: `falcon.ship.event`; version: `1`.

```json
{
  "schema": "falcon.ship.event",
  "schema_version": 1,
  "event_id": "01J...",
  "ship_id": "shipwright",
  "accepted_seq": 1842,
  "occurred_at": "2026-07-10T20:10:03.211Z",
  "observed_at": "2026-07-10T20:10:03.249Z",
  "accepted_at": "2026-07-10T20:10:03.257Z",
  "event_type": "tool.completed",
  "producer": "captain-harness",
  "sensor_id": "captain-harness.local",
  "actor": "captain.canopus",
  "actor_rank": "Captain",
  "target": "pa.captain",
  "status": "completed",
  "truth_class": "recorded",
  "correlation_id": "turn-...",
  "causation_id": "event-...",
  "root_authority_id": "DIR-...",
  "root_mission_id": "MIS-...",
  "primary_parent_id": "TSK-...",
  "work_item_id": "ATT-...",
  "objective_id": "OBJ-...",
  "order_id": "CAP-...",
  "standing_order_id": null,
  "standing_order_version": null,
  "standing_order_run_id": null,
  "task_id": "captain-board:SC-12",
  "workspace_id": null,
  "model_run_id": "run-...",
  "tool_run_id": "tool-...",
  "grant_id": null,
  "summary": "PA assignment queued",
  "payload": {},
  "redactions": [],
  "source": {
    "kind": "captain-event-ledger",
    "locator": "project-management/bridge/captain/events.jsonl",
    "offset": 91,
    "digest": "sha256:...",
    "source_event_id": "...",
    "source_seq": 91
  },
  "derivation": null,
  "prev_hash": "sha256:...",
  "event_hash": "sha256:..."
}
```

### 8.2 Required fields

`schema`, `schema_version`, `event_id`, `ship_id`, `occurred_at`, `observed_at`, `event_type`,
`producer`, `sensor_id`, `actor`, `status`, `truth_class`, `summary`, `payload`, and `source` are
required on ingest. An event about executable work also requires `root_mission_id`,
`primary_parent_id`, and `work_item_id`. `accepted_seq`, `accepted_at`, `prev_hash`, and `event_hash`
are assigned by the Computer. A sensor cannot select its position in the canonical chain.

### 8.3 Identities and references

- Actor and target IDs use the canonical roster identity, not display names.
- `correlation_id` groups one voyage of work, usually a model turn or commissioned assignment.
- `causation_id` points to the immediate event that caused this event.
- `root_authority_id`, `root_mission_id`, `primary_parent_id`, `work_item_id`, `objective_id`,
  `order_id`, `standing_order_id`, `task_id`, `workspace_id`, `model_run_id`, and `tool_run_id` make
  cross-surface joins explicit. Text search is never used as formal correlation.
- Rank is copied from the authenticated roster at acceptance. A producer-supplied rank is retained
  only as untrusted source data if it differs.
- Source locators are opaque references. Query responses expose them only to authorized roles.

### 8.4 Core event families

The v1 registry includes:

- `session.*`, `turn.*`, `prompt.received`, `response.visible`, `model.*`
- `tool.*`, `connector.*`, `side_effect.*`
- `directive.*`, `standing_order.*`, `mission.*`, `objective.*`, `order.*`
- `intake.*`, `message.*`, `report.*`, `decision.*`, `escalation.*`
- `epic.*`, `task.*`, `subtask.*`, `attempt.*`, `board.*`, `assignment.*`, `worker.*`
- `dependency.*`, `blocker.*`, `milestone.*`, `risk.*`, `hold.*`
- `workspace.*`, `change.*`, `test.*`, `landing.*`, `seal.*`, `release.*`
- `brain.*`, `memory.*`, `scratchpad.*`, `packet.*`
- `grant.*`, `spend.*`, `cost.*`, `resource.*`
- `process.*`, `heartbeat.*`, `queue.*`, `sensor.*`, `coverage.*`
- `auth.*`, `policy.*`, `redaction.*`, `integrity.*`

The event registry defines required payload fields and allowed state transitions for each family.
Unknown event types are quarantined until their schema is registered; they are not silently reduced
to generic activity.

## 9. Ingestion and sensors

### 9.1 Native emitters first

The durable target is explicit emission at the boundary where an action is accepted or completed.
Filesystem scans are migration adapters, not the final architecture. A native emitter can establish
more than a poller because it can correlate attempted, committed, failed, and compensated effects.

### 9.2 Required sensor inventory

| Sensor | Minimum events | Authority and limit |
|---|---|---|
| Captain harness | prompt, visible response, model, tool start/finish/fail, session | Authoritative for what that harness submitted and received; not provider internals |
| Officer harnesses | same as Captain, scoped per seat | Authoritative only at each harness boundary |
| Command ledger/typed transport | directive, standing order, mission, order, delivery, receipt, report, decision | Canonical for command lifecycle; desired state never proves execution |
| PA offices | assignment, operator work, connector receipt, packet and Brain operation | PA action record; officer acceptance remains separate |
| Advisors | conversation turns, thinking-team assignments/reports, synthesis | Personal cognition metadata/content by policy; no command effects |
| Science/panels | commission, member runs, evidence artifacts, report | Report remains reported until evidence is checked |
| Boards | committed item/dependency/status changes | Board state is advisory, not execution authority |
| Model gateway | provider/model/effort/tokens/latency/fallback/refusal/cost | Provider-returned measurements; unknown stays unknown |
| Tool gateway | arguments, result, error, side-effect receipt | Receipt proves only the named boundary |
| Workspace broker | create, scope, change, test, submit, land, clean | Authoritative for broker operations and policy checks |
| jj adapter | change IDs, parents, conflicts, seals, bookmarks | Repository evidence; description alone does not prove acceptance |
| Process supervisor | start, heartbeat, stop, crash, PID/host | Liveness evidence with bounded freshness |
| Grant/cost service | approval, reservation, measured cost, release | Named source for spend authority and accounting |
| Incubator interface | handoff, acceptance, PM receipt, reports, returned changes | Cross-project evidence only; no Shipwright access to Incubator managers |
| Bridge interaction | authenticated view, acknowledgement, comment | Human-interface event, not automatic ratification |

### 9.3 Authentication of producers

Each sensor gets a unique identity and narrowly scoped ingest credential. One shared ship token is
not acceptable. HTTP sensors use short-lived signed tokens or mutual TLS when deployed across hosts.
Local-process sensors may use a Unix domain socket plus peer credentials. Credentials are rotated,
revoked, and never sent through model context.

The service validates:

- Producer identity matches the sensor credential.
- Ship, actor, event type, and source are allowed for that sensor.
- Required correlation and schema fields are present.
- Payload and referenced blob sizes are within policy.
- Timestamps are parseable and within declared clock-skew bounds.
- The content passes centralized redaction and secret scanning.

Rejected events go to a metadata-only quarantine record. The rejected secret-bearing payload is not
persisted. Sensor health becomes degraded and the Bridge shows the gap.

### 9.4 Durable spooling and backpressure

Every side-effecting emitter writes a local spool entry before or atomically with its action record.
Delivery is at least once. The Computer acknowledges only after canonical persistence. An emitter
deletes a spool item only after a matching acknowledgement.

When the Computer is unavailable:

- Read-only cognition may continue if its sensor can spool durably within its quota.
- Orders and externally visible or irreversible side effects fail closed if their mandatory audit
  event cannot be durably spooled.
- A full spool stops new side effects and raises an operator-visible fault.
- Recovery replays in source sequence; deduplication makes replay safe.

## 10. Ordering, idempotency, and integrity

### 10.1 Three clocks, no invented chronology

- `occurred_at` is the source's event time and may be skewed or late.
- `observed_at` is when the sensor observed or emitted the record.
- `accepted_at` and `accepted_seq` are the Computer's durable intake order.

The canonical log is ordered by `accepted_seq`. Causal views use explicit `causation_id` and source
sequence, never timestamp sorting alone. Late events are appended; history is not rewritten.

### 10.2 Idempotency

`event_id` is globally unique. Native sensors persist it in their spool before the first send.
Migration adapters derive a stable ID from `sensor_id + source locator + source sequence + source
digest`. The unique event ID and unique source coordinate are both enforced.

Duplicate delivery returns the original acceptance receipt. A reused ID with different content is an
integrity violation and is quarantined. Exactly-once delivery is not claimed; the design is
at-least-once delivery with deterministic deduplication.

### 10.3 Append transaction

For each accepted event, the single writer:

1. Authenticates and validates the source event.
2. Redacts and canonicalizes it.
3. Checks event and source-coordinate uniqueness.
4. Assigns `accepted_seq`, `accepted_at`, and `prev_hash`.
5. Computes `event_hash` over canonical bytes.
6. Appends and syncs the segment.
7. Updates the SQLite index in a transaction.
8. Returns an acceptance receipt and publishes an SSE delta.

If the process dies after step 6, startup replay repairs the index from the segment. If it dies
before the segment sync, no acknowledgement was returned and the sensor retries. The index never
writes canonical history.

### 10.4 Verification and checkpoints

Startup verifies all events after the last trusted checkpoint and refuses to append behind an
invalid head. A background verifier checks closed segments and source digests. A closed-segment
checkpoint contains the segment digest, count, first and last sequence, previous checkpoint digest,
and signing-key identity. Invalid material is never auto-repaired or discarded.

The Bridge shows the last verified sequence, checkpoint age, chain status, and any quarantined
range. Valid hash linkage proves consistency of the retained bytes, not truth of their claims.

## 11. Query and live-update API

API prefix: `/api/v1`. All endpoints require authentication, including on localhost. Responses use
`Cache-Control: no-store`. The service validates `Host` and, for browser mutations, `Origin`.

### 11.1 Read endpoints

| Method and path | Purpose |
|---|---|
| `GET /api/v1/status` | Service, store, chain, index, checkpoint, queue, and version health |
| `GET /api/v1/snapshot` | Current authorized topology, counts, active work, alerts, and coverage |
| `GET /api/v1/events` | Cursor-paginated event query |
| `GET /api/v1/events/{event_id}` | One event with authorized payload and provenance |
| `GET /api/v1/correlations/{id}` | Causal event graph for a turn/order/task/workspace |
| `GET /api/v1/actors/{actor_id}` | Actor identity, rank, state, work, model, tools, and events |
| `GET /api/v1/orders/{order_id}` | Order lifecycle, reports, evidence, and unresolved gates |
| `GET /api/v1/missions/{mission_id}` | Full authority, objective, route, execution, return, and decision tree |
| `GET /api/v1/standing-orders/{id}` | Definition versions, trigger ledger, runs, misses, suppression, and outcomes |
| `GET /api/v1/work/{node_id}` | Typed command/execution/return node, revisions, lineage, and transitions |
| `GET /api/v1/deliveries` | Outbox/inbox, ack SLA, retry, dead-letter, and reconciliation state |
| `GET /api/v1/tasks/{task_id}` | Board history joined to orders, workers, tests, and seals |
| `GET /api/v1/workspaces/{workspace_id}` | Scope, owner, changes, tests, landing, and cleanup |
| `GET /api/v1/costs` | Measured spend, unknowns, grants, model, actor, and cost class |
| `GET /api/v1/coverage` | Expected sensors, last seen, lag, failures, blind spots, and exclusions |
| `GET /api/v1/stream` | Authorized SSE event and health deltas |

Event query filters include actor, target, event family, status, truth class, correlation, order,
root mission, objective, standing-order definition/run, task, workspace, model, tool, grant, source,
time, and accepted-sequence range. Cursor tokens bind the filter and authorization scope; clients
cannot widen a cursor by editing query text.

### 11.2 Command transaction endpoint

`POST /api/v1/command/transactions` accepts one authenticated typed command transaction: node
creation or revision, lifecycle transition, route envelope, acceptance decision, or control action.
It validates the actor's authority, schema version, transition, primary lineage, root mission,
destination, route, return contract, and idempotency key. Node revision plus delivery and telemetry
outboxes commit atomically. A retry returns the original transaction receipt.

This endpoint is not available to a dashboard read session. The Computer validates authority already
granted by the command graph; it never supplies missing authority or authors content.

### 11.3 Ingest endpoint

`POST /api/v1/ingest/events` accepts a bounded batch from one authenticated sensor. It returns, per
event, accepted, duplicate, or rejected plus canonical event ID and accepted sequence. The endpoint
has body, batch, rate, and decompression limits. It never returns another actor's data.

Browser sessions cannot call ingest. Sensor credentials cannot call query endpoints unless given a
separate read capability.

### 11.4 SSE contract

SSE messages include only an authorized compact delta: event ID, accepted sequence, type, actor,
target, status, truth class, summary, and changed projection IDs. Full payload is fetched on demand.
Clients resume with `Last-Event-ID`, which is the accepted sequence. If the requested sequence is
older than the retained stream window, the server sends `snapshot_required` and closes cleanly.

Heartbeats are transport liveness only. They are not ship activity. The Bridge falls back to bounded
polling after an SSE disconnect and displays that it is degraded.

## 12. Authentication, RBAC, and data policy

### 12.1 Capability model

Authentication establishes an identity. Authorization grants explicit capabilities over actor,
event family, field class, and time range. Rank alone does not grant API access.

Initial policy profiles:

| Identity | Default read scope |
|---|---|
| Commodore | All sanitized ship telemetry, including Captain events and coverage gaps |
| Captain | All sanitized operational ship telemetry and own personal-cell detail |
| No1 | Department execution under command; excludes private personal cognition unless commissioned |
| Commissioned officer | Own department and personal cell plus explicitly shared correlations |
| Security | Security charter scope; Captain-private and flag-channel content excluded by doctrine |
| CMO | System-wide health and observability fields under its charter; content fields follow separately ratified privacy policy |
| PA | Owning officer's operations, records, and authorized tools; no other personal cell |
| Advisor | Own conversation and thinking-team traces; no ship-wide operational read |
| Personal Engineer | Own engineering board, workspaces, workers, tests, and returned artifacts |
| Incubator PM | Logged cross-project handoff only |
| Bridge display session | The intersection of the signed-in human's capabilities and the active view |
| Sensor | Ingest only for named event families and actors |
| Ship Computer service | Validate, append, derive, and serve; no command capability |

The Commodore's "see everything" view remains sanitized: credentials are never visible because they
must never enter the store. Access to optional sensitive content blobs is separately logged.

### 12.2 Command-write authority

Command-write authorization is evaluated per transaction, not inferred from read access or rank:

- Commodore may issue/revise/revoke directives and standing authority through the flag channel.
- Captain may create/adopt missions, authorize objectives, issue orders, disposition intake, and
  accept/revise/cancel/close mission outcomes within Commodore authority.
- Commissioned officers may decompose and route only beneath a parent order that explicitly delegates
  that scope. They may accept subordinate returns only when the return contract names them.
- Managers may create epics/tasks/subtasks beneath their authorized work package.
- Workers and runtimes may create attempt/evidence/report records for work assigned to them; they may
  not create authority nodes or acceptance decisions.
- A PA may mechanically transcribe an owning officer's authenticated command. The record preserves
  both `authorized_by` and `transcribed_by`; PA identity never supplies the officer's authority.
- A standing-order trigger service may create only a run permitted by the exact active definition
  version and occurrence key.
- Sensors and external interfaces may create intake items, incidents, and alerts; those remain
  non-executable until Captain adoption or an active standing-order run supplies authority.

Every write check resolves the actor's current commission, parent delegation, route, destination,
grant, and acceptance scope. Revoked credentials or held authority fail closed and emit a sanitized
authorization event.

### 12.3 Browser authentication

The first local deployment may use a high-entropy, short-lived session token delivered out of band,
not embedded in generated HTML or logged in URLs. Target deployment uses a local identity broker or
mutual authentication. Cookies, if used, are `HttpOnly`, `Secure` where applicable, `SameSite=Strict`,
short lived, and protected against CSRF. Every authorization denial emits a metadata-only audit event.

### 12.4 Redaction

Redaction occurs before canonical persistence and again before query output.

- Sensitive key names are removed recursively.
- Known provider token, bearer token, private-key, cookie, URL-secret, and credential patterns are
  removed from strings.
- Connector payload schemas declare secret and personal-data fields.
- Binary and oversized results become digest-addressed blobs, never inline event strings.
- Redaction emits field paths, rule IDs, and counts, not secret values.
- Logs never contain request headers, query tokens, or raw authentication failures.
- Secret-scanner failure on a side-effect event is fail closed.

The source emitter must also avoid collecting credentials. Central redaction is defense in depth, not
permission to pass raw secrets through the fleet.

## 13. Projections for the Bridge

The Computer builds current-state projections from immutable events. Each projection includes the
last contributing accepted sequence and a list of evidence event IDs.

Required projections:

- Ship topology: command structure, departments, personal cells, Incubator boundary.
- Seat state: active, queued, blocked, failed, stale, unmanned, configured, or unknown.
- Current work: objective, order, task, responsible actor, start, last heartbeat, and blocker.
- Order lifecycle: issued, accepted/rejected, delivered, executing, reported, evidence checked,
  accepted, cancelled, or failed.
- Task lifecycle: board state plus linked order, workers, tests, and seal.
- Workspace lifecycle: created, scoped, active, submitted, reviewed, landed, cleaned, abandoned.
- Model activity: provider, model, effort, latency, tokens, cost, fallback, refusal, and run status.
- Tool activity: invocation, result, error, side effect, receipt, retry, and compensation.
- Spend: measured amount, API-equivalent estimate, unknown, grant, actor, duty class, and period.
- Sensor coverage: expected, healthy, lagging, failed, blocked, absent, or intentionally excluded.
- Command integrity: orphan checks, unacknowledged routes, dead letters, overdue returns, missing
  acceptance, post-cancel activity, and projection drift.

An `active` projection requires a nonterminal start plus a fresh heartbeat or other explicitly defined
liveness signal. A historical start can never keep a node active forever. A reported order must not
remain counted as queued. A completion-audit failure after a committed side effect is represented as
`committed_with_audit_failure`, not as a safe-to-retry failure.

### 13.1 Four required Bridge flows

The first command views are four explicit end-to-end flows:

1. **Standing order flow:** definition and version -> active/held/revoked state -> expected trigger ->
   invocation or missed/suppressed trigger -> Captain-owned mission/order attachment -> deliveries ->
   execution evidence -> report -> decision and run outcome.
2. **Mission flow:** Commodore directive or Captain adoption -> Captain-owned mission -> measurable
   objectives -> routed orders -> execution tree -> evidence/reports -> Captain decisions -> mission
   accepted, revised, held, cancelled, superseded, or closed.
3. **Epic flow:** parent order -> accountable officer/manager epic -> tasks and dependencies ->
   attempts/artifacts/evidence -> epic report -> delegated acceptance decision -> return continues to
   the parent order. The epic never appears as independent authority.
4. **Task flow:** authorized parent -> named assignment and recipient ack -> attempt history ->
   blockers/dependencies -> artifacts and evidence -> review/report -> acceptance or revision. A
   worker's `done` claim alone never closes it.

Each view displays immutable IDs, root mission, primary parent, authority basis, accountable and
executing owners, route and destination, desired phase, observed evidence state, ack/progress/report
SLAs, return contract, grants/cost, and unresolved gaps.

## 14. Boards and task management

The Computer owns the canonical command lifecycle, not officer planning judgment. Boards are
officer-authorized work queues and projections over that ledger.

- One board remains the designated work surface per domain under the ship organization design.
- The ship board is under No1's authority with mechanical writing through the authorized PA.
- Department officers own their department boards.
- Captain and personal departments retain separate personal boards.
- A board mutation that changes command lifecycle submits a command-ledger transition; the board
  projector applies the accepted revision and records its source sequence.
- Local notes, sorting, and planning metadata may remain board-native but grant no authority.
- Board event emitters record requested mutation, authenticated writer, before/after digest,
  committed result, ledger sequence, and any failure.
- Task IDs are namespaced and are carried through orders, assignments, model runs, tool calls,
  workspaces, tests, reports, and seals.
- A board status does not prove work occurred. The Bridge displays linked evidence separately.
- Polling existing SQLite boards is a migration adapter. Native board projection transactions use an
  outbox and are reconciled against the command ledger.

## 15. Workspaces, jj, tests, and landing

The target workspace doctrine is non-negotiable:

- Any AI agent with read/write access works in its own isolated workspace.
- No AI agent writes the main working copy.
- A single trusted, non-agent landing broker creates workspaces, validates path scope, runs required
  checks, integrates with `jj`, records provenance, and cleans up.
- Shared `jj` repository authority means a workspace is isolation, not full security. Agent access to
  repository-wide `jj` operations must be mediated.

The workspace broker emits:

1. `workspace.requested` with owner, task, base revision, allowed paths, and grant.
2. `workspace.created` with workspace ID and immutable base change.
3. `change.observed` summaries with paths and change IDs, not unbounded file contents.
4. `test.started` and `test.completed` with command policy ID, result, duration, and artifact digest.
5. `landing.submitted`, scope and provenance validation results, review result, and conflicts.
6. `landing.completed` with final change/seal, or `landing.rejected` with reasons.
7. `workspace.cleaned` or an overdue-cleanup alert.

The Computer reads repository facts through the broker or a read-only adapter. It never runs
arbitrary `jj` commands supplied by an event producer. File content views require separate scoped
authorization and are not embedded in the general event stream.

## 16. Models, tools, connectors, and cost

### 16.1 Model runs

Each model run has a stable `model_run_id` and records:

- Requesting actor and commissioned objective reference.
- Provider, exact model ID, effort/reasoning setting, transport, and harness version.
- Start/end, latency, retry, fallback, refusal, timeout, and error classification.
- Input/output token counts and cached-token fields when the provider returns them.
- Measured cost and currency when available.
- Explicit `blocked-no-data` when cost cannot be established.
- Prompt and visible response references after redaction and field authorization.

Model configuration is not runtime evidence. Candidate Fable, Opus, GLM, or Terra slots remain
configured until an actual model-run event exists. External benchmark claims remain hypotheses until
Shipwright's own bench verifies them.

### 16.2 Tool and connector runs

Each invocation has a stable `tool_run_id`, schema version, actor, tool, redacted arguments, start,
terminal result, retry relationship, and side-effect classification. External operations require a
provider receipt or an explicit `receipt_missing` event. A handler returning successfully before its
audit record commits is not represented as a clean failure that may be retried.

PA-owned tool catalogs and connector runbooks remain PA operational responsibilities. Engineering
builds or changes tools. The Computer records use and evidence; it does not provision access.

### 16.3 Cost

Cost records distinguish:

- `measured`: provider or treasury measurement.
- `api_equivalent`: a named comparison estimate, never displayed as actual spend.
- `allocated`: budget reservation under a grant.
- `unknown`: no trustworthy data.

Every measured or allocated cost links actor, model/tool, correlation, grant, and `cost_class` of
`ship-ops` or `duty`. Unknown cost is a visible coverage fault, not zero.

## 17. Health and coverage

The coverage registry is a first-class product, not a footer disclaimer. For every expected sensor it
stores:

- Sensor identity, owner, version, event families, and authorized actor scope.
- Expected heartbeat or maximum event silence.
- Last accepted sequence and source sequence.
- Ingest lag, spool depth, rejection count, and clock skew.
- Last successful integrity verification.
- Known exclusions and blind spots.
- Current state: healthy, lagging, degraded, failed, absent, disabled, or unknown.

Ship-level health separates:

- Computer process and API health.
- Canonical store and free-space health.
- Hash chain and checkpoint health.
- Index freshness and rebuild status.
- Sensor coverage and backpressure.
- Query/SSE delivery health.

No fresh evidence must render as `unknown` or `stale`, never `idle`. The Bridge must show the age and
source of every liveness claim.

## 18. Failure modes and required behavior

| Failure | Required response |
|---|---|
| Computer unavailable | Sensors spool; mandatory-audit side effects fail closed if durable spool is unavailable |
| Disk full | Stop acknowledgements, preserve existing chain, alert, and block audited side effects |
| Invalid chain | Refuse further append, quarantine the range, serve last verified state with a critical banner |
| SQLite corruption | Keep canonical segments read-only, rebuild a new index, do not edit history |
| Duplicate delivery | Return the original acceptance receipt |
| Same ID, different body | Quarantine as an integrity violation |
| Clock skew or late event | Append in intake order, flag skew, use causal links for sequence |
| Sensor silent | Mark coverage gap and affected projections unknown/stale |
| Sensor lies or is compromised | Preserve the claim as recorded; seek independent receipt; do not upgrade truth class |
| Redaction uncertainty | Reject or store metadata only; never persist suspected secret content |
| SSE disconnect | Client shows degraded state and uses bounded snapshot polling |
| Authorization service failure | Fail closed; do not return cached broader data |
| Event schema drift | Quarantine unknown version and flag the sensor |
| Partial side effect plus audit failure | Mark committed state and reconciliation required; prevent automatic retry |
| Incubator link unavailable | Keep handoff queued/blocked; never imply PM delivery or factory execution |
| Landing broker unavailable | Preserve submitted workspaces; no direct main-copy workaround |

Recovery actions are themselves events once intake is safe again. Manual repair never deletes the
original invalid evidence.

## 19. Bridge integration contract

The Bridge becomes a read client of the Ship Computer:

1. Load `/snapshot` under the operator's authenticated capability.
2. Subscribe to `/stream` from the snapshot's accepted sequence.
3. Apply compact deltas to topology, activity, order, cost, and coverage views.
4. Fetch full authorized event/correlation detail only when opened.
5. Display last sequence, stream health, chain status, data age, and coverage gaps at all times.

The Bridge must support these views:

- Full ship map, with commissioned departments and every officer's Thinking/Operations/Engineering
  personal cell.
- Live activity with actor, rank, objective, model, tool, status, truth class, and age.
- Order/task/workspace causal drilldown.
- Models, tokens, costs, grants, fallbacks, and unknowns.
- Tool and connector side effects with receipts.
- Provenance integrity and observation coverage.
- Alerts for stalled work, missing reports, failed tests, unlanded workspaces, and silent sensors.

Visual motion is driven only by events. The frontend must not invent activity to make the ship feel
alive. Prompt and response detail is on-demand and field-authorized, not dumped into the map.

This document defines the data and interaction contract, not the visual design. The Codex Frontend
Manager owns that product and visual design under direct Commodore direction. The accepted frontend
package must be reviewed against this contract, accessibility requirements, responsive behavior, and
performance budgets before the Chief Engineer sends it to the Incubator PM for implementation.

## 20. Deployment phases

### Phase 0 - contract and threat model

- Ratify command node schema, transition registry, routes, event schema, event registry, identity
  catalog, truth classes, and RBAC matrix.
- Ratify Captain-only mission authorization and explicit delegated acceptance rules.
- Inventory every current producer and expected sensor.
- Threat-model telemetry content, source impersonation, store compromise, and Bridge exposure.
- Define retention, blob encryption, and external checkpoint custody.

**Gate:** fixtures for every v1 command/event family validate; no executable orphan, invalid route,
or unresolved authority ambiguity is accepted.

### Phase 1 - local computer, command ledger, and Captain vertical slice

- Build external state root, command revision/outbox store, canonical event writer, verifier, SQLite
  index, query API, and coverage API.
- Implement directive -> mission -> objective -> order -> delivery/ack -> report/evidence -> Captain
  decision as the first no-loss command path.
- Ingest the native Captain ledger through an authenticated adapter.
- Add Bridge snapshot and SSE consumption behind a feature flag.
- Keep the current Bridge collector as a comparison path, not silent fallback truth.

**Gate:** end-to-end Captain prompt -> mission/order -> tool/work -> return -> decision appears with
valid authority lineage, delivery receipts, chain, correlation, redaction, crash recovery, and no
repository telemetry writes.

### Phase 2 - orders, boards, personal cells, and model/tool gateways

- Instrument typed transport, board outboxes, PAs, Advisors, Science, model calls, tools, costs, and
  process supervisors.
- Render each officer's three personal departments independently.
- Add explicit delivery, execution, report, evidence, and acceptance states.
- Add standing-order definitions, invocations, missed-trigger detection, and duplicate suppression.

**Gate:** a commissioned personal-cell voyage and a Science voyage are distinguishable end to end;
all work keeps its root mission, and unknown costs, overdue returns, and missing receipts remain
visible.

### Phase 3 - workspace broker, jj, and Incubator handoff

- Emit workspace, change, test, review, landing, seal, cleanup, and cross-project handoff events.
- Remove direct repository-state polling where a native broker event exists.
- Prove no AI actor writes the main working copy.

**Gate:** Chief Engineer -> Incubator PM -> factory -> returned change -> Shipwright landing can be
traced without granting Shipwright direct access to Incubator managers or main copies.

### Phase 4 - hardening and external custody

- Externalize signed checkpoints.
- Add backup/restore drills, key rotation, adversarial sensor tests, and retention enforcement.
- Run sustained load, partition, disk-full, corrupted-index, and compromised-sensor exercises.

**Gate:** independent verifier accepts restored history and external checkpoint continuity.

### Phase 5 - Ship Computer becomes Bridge source of record

- Compare Computer projections against legacy collectors for a defined parallel-run period.
- Resolve discrepancies in favor of verified source evidence, not whichever view looks newer.
- Retire duplicate collectors only after coverage and rollback gates pass.

**Gate:** Commodore acceptance, documented rollback, and zero unexplained coverage regressions.

## 21. Test and acceptance gates

### 21.1 Unit and contract tests

- Event schema validation, canonical serialization, rank resolution, and event registry transitions.
- Command schema/transition validation for every type, route, destination, return contract, and
  delegated acceptance boundary.
- Graph constraints reject missing roots, zero/multiple primary parents, cycles, unauthorized mission
  creation, anonymous-worker routing, and execution beneath an unadopted intake item.
- Standing-order fixtures cover version activation, hold, revocation, expiry, recurrence, missed
  trigger, duplicate occurrence, and mission/order attachment.
- Recursive redaction against key names, token families, URLs, cookies, private keys, binary data,
  circular values, and adversarial strings.
- Stable IDs, source-coordinate uniqueness, duplicate replay, and conflicting duplicate rejection.
- Hash linkage, checkpoint validation, segment rotation, and full replay.
- RBAC field filtering and cross-tenant/personal-cell denial.
- Projection handling for stale starts, late events, reported orders, partial side effects, and
  configured-but-disabled seats.

### 21.2 Integration tests

- Crash before append, after append/before index, and after index/before acknowledgement.
- Crash at every command outbox/inbox boundary: before/after command commit, send, recipient persist,
  receipt, sender ack, telemetry append, board projection, report, and acceptance decision.
- Repeated recovery proves one command node, one recipient receipt, one standing-order run, and no
  duplicated externally visible side effect.
- Reconciliation detects and surfaces missing outbox, missing inbox ack, orphan attempt, overdue
  report, unaccepted completion, dead letter, projection drift, and unresolved cancellation.
- Sensor spool replay, backpressure, full spool, out-of-order delivery, and clock skew.
- SQLite rebuild from segments and restore from backup.
- Captain, officer, PA, Advisor, Science, board, model, tool, workspace, and Incubator fixtures.
- Browser auth, SSE resume, snapshot-required fallback, cursor scope binding, and pagination.
- Secret canaries prove prohibited material never reaches canonical segments, query output, logs, or
  Bridge HTML.

### 21.3 Adversarial tests

- Producer impersonation and actor/rank spoofing.
- Malformed, oversized, compressed, recursive, and unknown-version events.
- Prompt injection embedded in tool results and source records.
- Forged report correlation using incidental order text.
- Reused event IDs with modified content.
- Compromised sensor asserting completion without an independent receipt.
- Attempted use of query credentials for ingest or command APIs.
- Agent attempts to write the main copy or use repository-wide `jj` authority.
- Officer attempts to create a new root mission, worker attempts to self-authorize, Advisor receives
  a command order, PA receives ship command authority, and Captain attempts to bypass managers for an
  anonymous worker; all are rejected.
- Board-only work, forged acknowledgement, forged acceptance, and incidental text containing another
  work ID cannot alter canonical lifecycle.

### 21.4 Frontend acceptance

- Desktop and mobile screenshots at agreed viewports; no overlap, clipping, or unreadable dense data.
- Keyboard navigation, visible focus, semantic labels, contrast, and reduced-motion behavior.
- A live voyage visibly updates without a full reload.
- Every active/failed/queued indicator opens the evidence that supports it.
- Every page shows stream health, data age, and coverage gaps.
- Large histories remain responsive through pagination and windowing.
- Private content is absent when tested under every narrower role.

### 21.5 Release bar

The Ship Computer is not ready to claim "everything observable" until:

1. All required sensors have an owner, contract, health state, and tested failure path.
2. Canonical segments survive crash and restore drills.
3. RBAC and redaction pass adversarial review.
4. The Bridge never fabricates liveness, completion, delivery, cost, or correlation.
5. Workspace and Incubator boundaries are proven with real voyages.
6. Known blind spots are displayed in the primary view, not buried in documentation.
7. No-loss invariant audits pass after normal, duplicate, delayed, cancelled, and crash-recovery
   voyages; every outbound command ends in ack, dead-letter/quarantine, or authorized cancellation.

## 22. Migration from the current Bridge

Current precursors are handled as follows:

| Current component | Migration |
|---|---|
| Captain `events.jsonl` hash chain | Preserve as source evidence; ingest with stable source IDs; native dual-write only after parity tests |
| Bridge `src/bridge/provenance.mjs` | Split collectors into versioned migration sensors; move projections into the Computer |
| Bridge server JSON endpoints | Keep behind feature flag while the UI adopts `/api/v1`; retire after parallel-run gate |
| Runner logs and dispatch JSON | Polling adapters first; replace with native supervisor events |
| Staff inboxes and packets | Ingest as queue/report records; require structured IDs, never text correlation |
| Existing untyped orders/tasks | Import as migration records with explicit uncertainty; Captain adopts, closes, or quarantines each open lineage |
| Cost ledgers | Ingest with measured/equivalent/unknown truth preserved; replace with native gateway emission |
| Brain file scans | Replace modification-time inference with authorized Brain-operation events |
| Board SQLite scans | Add transactional outboxes, then retire broad polling |
| `jj` log scans | Replace with read-only broker/seal events plus source digest verification |
| Static generated Bridge HTML | Retain only as a degraded snapshot artifact, clearly timestamped and non-live |

Migration must not rewrite old ledgers to make them fit the new schema. The adapter records source
limitations and import time. Imported events are distinguishable from native events.

## 23. Engineering handoff

The Chief Engineer owns the implementation handoff. The command path is:

```text
Captain commissions Chief Engineer
  -> Chief Engineer sends a typed, logged design/build envelope
  -> external Incubator PM accepts or rejects it
  -> Incubator PM decomposes work across its engineering department
  -> isolated workers build and test in Incubator-controlled workspaces
  -> Incubator PM returns evidence and sealed changes
  -> Chief Engineer reviews against this design and reports to the Captain
  -> Shipwright's trusted landing path integrates approved work
```

### 23.1 Required implementation package

The Chief Engineer sends one versioned package containing:

1. This architecture and a separate frontend interaction/visual plan.
2. JSON Schemas for command nodes, transitions, routes, return contracts, and events.
3. A versioned event/type/transition registry and identity/rank fixtures.
4. SQLite schema and migrations for command revisions, edges, outbox/inbox, receipts, dead letters,
   telemetry outbox, index, and projection cursors.
5. OpenAPI or equivalent machine-readable contracts for command, ingest, query, and SSE APIs.
6. RBAC field matrix, threat model, redaction corpus, retention policy, and credential plan.
7. Deterministic fixtures for the standing-order, mission, epic, and task Bridge flows.
8. Unit, crash-matrix, no-loss, adversarial, browser, backup/restore, and performance acceptance suites.
9. Parallel-run migration, discrepancy reconciliation, rollback, and operational runbooks.
10. A requirements trace mapping every MUST in this design to code owner, test, and evidence artifact.

The Chief Engineer does not become the Incubator PM, does not message Incubator managers directly,
and does not bypass the external PM's factory authority.

### 23.2 Codex Frontend Manager design ownership

The Codex Frontend Manager owns the Bridge product, interaction, and visual design under direct
Commodore direction. Its accepted design package must specify responsive Bridge flows, information
hierarchy, interaction states, accessibility behavior, and the four required flow fixtures. The Chief
Engineer hands that package to the distinct Incubator PM as the implementation contract; Incubator's
engineering department builds, tests, and returns evidence against it. Factory implementation does not
silently redesign the accepted product direction or change the Command Graph's truth semantics.

### 23.3 Handoff acceptance

The Chief Engineer accepts the factory return only when the package includes sealed change IDs, a
complete changed-file list, test and browser evidence, known gaps, migration/rollback proof, and a
requirements trace with no unexplained omissions. A design mockup, configured dashboard, or passing
happy path is not evidence that the Ship Computer has been built.

## 24. Explicit as-built ledger, 2026-07-10

| Capability | Status |
|---|---|
| Hash-chained Captain event ledger | Precursor exists |
| Bridge normalization of several repository sources | Precursor exists |
| Bridge local JSON snapshot/event/order APIs | Precursor exists; not the target authenticated API |
| Personal-cell target configuration | Design/config exists; most cells are not live |
| External canonical Ship Computer store | **NOT BUILT** |
| Ship Computer process and single writer | **NOT BUILT** |
| Authenticated per-sensor ingestion | **NOT BUILT** |
| Sensor registry and coverage health | **NOT BUILT** |
| Canonical event registry and source outboxes | **NOT BUILT** |
| Canonical command/work graph and revision ledger | **NOT BUILT** |
| Transactional command outbox/inbox, receipts, and reconciliation | **NOT BUILT** |
| Standing-order definitions, trigger ledger, and runs | **NOT BUILT** |
| Captain no-loss inbox and adoption flow | **NOT BUILT** |
| Rebuildable officer-board projections from command events | **NOT BUILT** |
| Rebuildable SQLite query index | **NOT BUILT** |
| RBAC query service | **NOT BUILT** |
| Live SSE Bridge channel | **NOT BUILT** |
| Workspace/landing-broker telemetry | **NOT BUILT** |
| Chief Engineer to Incubator PM live delivery path | **NOT BUILT** |
| External checkpoint custody | **NOT BUILT** |

No generated dashboard, configuration row, or design statement should present these target
capabilities as live before their acceptance gates pass.

## 25. Hull stress

- The organization design requires broad observability while also imposing role-specific monitoring
  and personal-cognition boundaries. This document proposes an initial RBAC split, but the Captain,
  Commodore, Security, CMO, and privacy scopes still need an explicit ratified field-level matrix.
- Existing repo-local sources are mutable and heterogeneous. Importing them can preserve what they
  say and their digest; it cannot retroactively make them complete or independently trustworthy.
- Provider cost, token, and reasoning data vary. The design refuses to turn missing fields into
  estimates presented as facts.
- A local hash chain without externally held checkpoints cannot defeat a fully compromised service
  account. External custody is a hardening gate, not decorative future work.
- "Everything" remains bounded by sensors. The coverage view is therefore part of the truth model,
  not merely an operations dashboard.
- The Captain-only mission-authority rule, delegated acceptance scopes, and standing-order issuance
  authority need contract fixtures and ratification before implementation; code must not guess them.
- No implementation, performance benchmark, security review, or live Incubator handoff has been
  completed for this design.
