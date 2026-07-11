---
date_created: 2026-07-10
date_updated: 2026-07-10
status: PRE-BRIDGE PRODUCT CONTRACT - VISUAL DESIGN DEFERRED
owner: Chief Engineer
executor: Incubator PM and Incubator engineering department
design_owner: Codex Frontend Manager under Commodore direction
depends_on:
  - Ship Computer event store, sensors, query API, and live stream
  - authenticated actor, topology, order, workspace, board, model, tool, spend, and coverage records
---

# Ship Computer Bridge Frontend Plan

## 0. Status and commission

This document preserves the future operator contract for the Ship Computer on the Bridge. It does not
implement the frontend, approve a framework, create a live API, or select a visual direction. The actual
Bridge must be designed **from scratch** after enough of the ship and Ship Computer exist to provide a
real contract and one verified end-to-end voyage.

The completed Falcon guardian composition and interactive concept have been reclassified as the
**Shipwright Manual identity**, not a Bridge prototype:
[`dashboard-direction/reference/../viewers/ship-manual.html`](dashboard-direction/reference/../viewers/ship-manual.html).
Its desktop and mobile assets are
[`../viewers/assets/ship-manual-falcon-guardian.webp`](../viewers/assets/ship-manual-falcon-guardian.webp).
The human manual is `docs/viewers/ship-manual.html`. No current artifact is the accepted future Bridge.

**Naming boundary:** this product is the **Shipwright Bridge**, the command surface for one ship.
**Falcon Command** is reserved for a later fleet-level headquarters where the Commodore can view every
ship's Bridge, use a distinct Command Computer, and communicate with all ships. Falcon Command is a
future target only; it is not designed or built by this package.

### 0.1 Bridge design restart gate

Visual and interaction design does not restart until all of the following are evidenced:

1. Phase-0 schemas, lifecycle transitions, actor identities, command routes, truth classes, RBAC, and
   threat model are ratified.
2. The external state root, single writer, command revision/outbox store, canonical event chain,
   verifier, query index, and coverage registry are running.
3. One real Captain voyage completes directive -> mission -> objective -> order -> delivery -> work ->
   evidence/report -> Captain decision without fixture substitution.
4. Authenticated `/status`, `/snapshot`, `/events`, `/correlations`, `/missions`, `/work`, `/deliveries`,
   `/coverage`, and `/stream` contracts operate against that voyage.
5. Redaction, replay, deduplication, crash recovery, and visible unknown/gap behavior pass.
6. The accepted voyage becomes the first frontend fixture and the Codex Frontend Manager begins a new,
   evidence-led Bridge design from a blank surface.

The Codex Frontend Manager owns the product, interaction, and visual direction under direct Commodore
direction. The Chief Engineer owns the implementation handoff: that officer commissions the distinct
Incubator PM to build the accepted design through the Incubator engineering department. The Chief
Engineer remains the ship-side implementation owner; the Incubator PM remains the external factory
orchestrator.

The product objective is literal:

> Give the Commodore one continuously updated operational picture of everything the Ship Computer can
> observe across Shipwright, with every claim traceable to its source and every observation gap visible.

"Everything" means every observable prompt and visible response, event, order, report, actor, model,
tool call, cost record, board transition, Brain write, workspace, file change, test, candidate, landing,
connector action, failure, heartbeat, and coverage gap that a commissioned sensor is permitted to
capture. It does not mean provider-hidden chain of thought, unobservable internal state, credentials,
secret values, or activity outside the sensor boundary. The interface must say which of those cases
applies instead of implying omniscience.

## 1. Grounded starting point

The current generated Bridge in `docs/viewers/bridge.html`, produced by
`src/bridge/render-bridge.mjs`, already establishes useful direction:

- A dark, restrained flight-operations register with compact type, hairline rules, and multiple status
  accents.
- Persistent top status, pipeline ribbon, Captain downlink, a ship map, order stream, provenance feed,
  work queue, board, Brain, current, and hull-stress sections.
- Actor, event, order trace, department, board item, and Brain drilldowns.
- Recorded, derived, and configured truth labels.
- Ten-second soft refresh and bounded server queries for actor/event/trace detail.
- Current topology groups command, personal cells, bridge staff, ship sections, external factory,
  departments, and execution crew.

The current page is an important prototype, not the target product. Its principal limitations are:

- The page is a generated report refreshed as a whole, not a first-class live Ship Computer client.
- Large amounts of unlike information are stacked vertically without a durable information hierarchy.
- Personal cells repeat as a flat node grid instead of being visibly attached to their owning officer.
- The map shows topology, but it does not yet make causal work flow, sensor coverage, or current routes
  legible at ship scale.
- Models, tools, costs, grants, workspaces, boards, tests, landings, and redactions do not have complete
  dedicated operational views.
- Status can be inferred from incomplete historical evidence; the target must receive authoritative
  lifecycle and freshness fields from the Ship Computer.
- Bounded page data and modal-only navigation make cross-ship investigation difficult.
- The current inline UI mixes read-only observation with acknowledgements and board comments. The
  observation product and every mutation path need separate authenticated contracts.

The organization and rank model comes from `docs/design/ship-org-design.md` and
`docs/viewers/ship-org-build-state.html`. The frontend must preserve these distinctions:

- Commodore is human flag command.
- Captain commands Shipwright.
- No1 is Commander and runs all ship departments under the Captain.
- Commissioned ship officers, including the Chief Engineer, are Lieutenant Commanders unless named
  otherwise.
- The Incubator PM is an external Lieutenant Commander, not the Chief Engineer and not a Shipwright
  bridge seat.
- Department managers and Personal Engineers are Lieutenants.
- Ephemeral workers, including personal-engineering Codex workers, are Ensigns.
- Advisors are non-line Warrant Officers.
- PAs are Chief Petty Officers; their operators are Petty Officers or specialists.
- Thinking partners hold Ensign rank and the Scientist non-line support designation; the rank gives no
  line command or operational authority in the Advisor cell.
- Rank, role, model, runtime, access, and authority are independent data fields.

## 2. Product rules

### 2.1 Evidence before animation

A node may pulse only when a current runtime or open work interval is backed by a fresh, authoritative
event and its heartbeat is inside the source-specific freshness window. A historical `started` event,
an open board item, a configured endpoint, or a live-looking process name is not sufficient.

Every visible assertion has one of these truth states:

| Truth state | Meaning | Visual treatment |
|---|---|---|
| `recorded` | Direct source event retained by the Ship Computer | Normal contrast; source available |
| `receipt` | Named system returned a checkable boundary result | Receipt marker and producing system |
| `derived` | Deterministic projection from named recorded events | Derived marker and derivation link |
| `configured` | Declared topology, grant, slot, or intended route | Quiet outlined treatment; never live |
| `reported` | Actor report correlated to a recorded order | Report marker; not equivalent to verified |
| `unknown` | Evidence is missing, invalid, or insufficient | Amber warning and explicit reason |

No color is the sole carrier. Every state has text, icon, and accessible name.

`unverified`, `unavailable`, `permission-blocked`, and `redacted` are evidence/access qualifiers layered on
the truth class rather than invented replacements for it. The UI may say `reported / unverified` or
`unknown / unavailable`, but the Ship Computer's canonical truth value remains intact.

### 2.2 Missing evidence is first-class state

The Bridge must never silently collapse these into "idle":

- No event occurred.
- The source has not emitted recently.
- The sensor is disconnected.
- The source is unsupported.
- The operator lacks permission.
- The event was redacted.
- The actor is configured but unmanned.
- The actor is manned but no current work is recorded.

The map, lists, and detail views use the same distinct state vocabulary.

### 2.3 Observation is not command

The first production release is read-only. Filtering, replay, pinning a local view, copying an event ID,
and opening evidence do not change ship state. Acknowledgement, commenting, ordering, cancellation,
grant changes, release, or landing require separate typed mutation APIs, explicit permission, an
operator confirmation where appropriate, and their own provenance events. Those controls remain absent
until separately designed and commissioned.

### 2.4 Progressive disclosure, not selective truth

The first viewport answers "what is happening and where does attention belong?" Full detail remains
one click or one search away. The interface may aggregate, but it must expose the aggregate's exact
denominator, time range, filters, and source coverage. No critical state is hidden only because it is
visually inconvenient.

### 2.5 Stable identity

Every actor, order, event, run, tool, model invocation, workspace, board item, Brain write, test, change,
landing, grant, and sensor has a stable ID. Display names may change; identity and deep links do not.

## 3. Operator questions

The default experience is optimized for the Commodore. It must answer these questions without reading
logs or understanding the implementation:

1. What is the ship doing now?
2. Which officer owns each active line of work?
3. What did the Captain order, who received it, and what happened after it?
4. Which personal Thinking, Operations, or Engineering cell is in use?
5. Which models and tools are being used, on whose authority, and at what known cost?
6. Which agents have writable workspaces, what changed, which tests ran, and who landed the result?
7. Which boards, memory stores, and records changed?
8. What failed, stalled, exceeded budget, lost coverage, or remains unverified?
9. Can every visible result be traced to the event, source, and integrity record that supports it?
10. What can the Ship Computer not currently see?

Secondary users are the Captain, No1, Security, CMO, Ops, and Chief Engineer. Role-based filters may
give them focused entry states, but no role-specific view may rewrite shared truth.

## 4. Information architecture

The Bridge is one application and one connected investigation space. It may use persistent view tabs
and URL-addressable filters; it must not become a set of disconnected report pages. The first screen is
the live operational experience, not a landing page or explanatory hero.

### 4.1 Persistent command chrome

The top chrome remains visible across every view and contains:

- `SHIPWRIGHT / SHIP COMPUTER` identity.
- Connection state: `LIVE`, `RECONNECTING`, `REPLAY`, `DEGRADED`, or `OFFLINE`.
- Stream cursor and last accepted event time.
- Wall clock and selected replay time or time range.
- Current coverage ratio with a direct link to the coverage view.
- Counts for active actors, queued orders, failed/stalled work, unread alerts, and unpriced spend.
- Always-visible counts for orphan work and broken primary lineage. These counts stay in the chrome even
  when zero and cannot be dismissed, collapsed into a generic alert count, or hidden by view filters.
- Global search button and filter summary.
- Live-follow toggle and pause/replay controls.
- Authenticated operator identity and read-only/read-write scope.

Counts are operational status, not decoration. A count always opens its filtered record set.

### 4.2 Primary views

Use compact text tabs with counts and familiar icons where helpful. Keep labels visible; this console is
too consequential for icon-only navigation.

| View | Primary question | Core content |
|---|---|---|
| **Ship** | What is happening across the organization? | Live map, attention rail, active work, recent causal events |
| **Command** | Why is work authorized and what followed? | No-loss Command Graph; Mission, Standing Order, Epic, and Task flows; delivery and return paths |
| **Activity** | What happened in time? | Virtualized event stream, trace grouping, replay, source filters |
| **Models & Spend** | Which intelligence ran and what did it cost? | Model turns, effort, tokens/units, grants, known/unknown cost, budget |
| **Tools & Access** | What capability was invoked or available? | Tool calls, outcomes, actor access matrix, connector and grant state |
| **Workspaces & Changes** | Where did writable work happen? | Workspace topology, files, tests, reviews, candidates, broker landing |
| **Boards & Memory** | What organizational state changed? | Board transitions, currents, Brain writes, PA records, seals |
| **Coverage & Health** | What can the Ship Computer see and trust? | Sensors, freshness, chain health, gaps, redaction, clock skew, failures |

### 4.3 Global investigation drawer

Selecting any item opens one right-side investigation drawer on wide screens and a full-screen sheet on
small screens. The drawer is reusable and URL-addressable. It supports nested breadcrumbs without
putting cards inside cards.

Every drawer follows one order:

1. Identity and current status.
2. Root mission breadcrumb and primary parent lineage.
3. Why the UI believes that status.
4. Causal relationships and linked records.
5. Time-ordered evidence.
6. Source, integrity, redaction, and coverage metadata.

The operator can pin up to two drawers side by side on wide displays for comparison. Additional items
replace the oldest unpinned drawer.

## 5. The live visual ship map

### 5.1 Purpose

The map is the Bridge's main visual asset. It is a functional organizational and causal diagram, not a
decorative ship illustration. It shows command structure at rest and visible work flow in motion.

The default map uses semantic DOM nodes with an SVG edge layer. This preserves accessible actor buttons,
text selection, keyboard focus, deterministic layout, and crisp routing at any zoom. A canvas renderer
may be selected by the Codex Frontend Manager only if it includes a synchronized accessible DOM representation and passes
the pixel and interaction tests in section 18.

### 5.2 Fixed topology bands

The overview layout has stable horizontal bands:

1. **Flag command:** Commodore -> Captain.
2. **Bridge command:** Captain -> No1 and direct Captain lines.
3. **Commissioned officers:** Science, Intelligence, Security, Ops, Communications, Tactical,
   Counsellor, CMO, and Chief Engineer.
4. **Ship departments:** officer-owned department managers and their current execution seats.
5. **External interfaces:** Chief Engineer -> external Incubator PM -> Incubator factory, plus any
   other explicitly external systems.

Personal cells are not a separate flat band. Each Captain/officer node has an attached, collapsible
three-part cell that preserves ownership:

```text
Owning officer
  Thinking    Advisor (Warrant Officer) -> Ensigns / Scientists
  Operations  PA (Chief Petty Officer) -> PA operators and officer Brain
  Engineering Personal Engineer (Lieutenant) -> Codex Ensign workers
```

The Advisor's own PA and Advisor Brain appear inside the Advisor branch, not as if they report directly
to the owning officer. The Incubator PM stays visibly external. The Chief Engineer-to-PM edge is a
logged interface, not an org-chart equivalence.

### 5.3 Node contents

All nodes use stable dimensions with responsive min/max constraints so dynamic text cannot reflow the
whole map. A compact node shows:

- Display name and stable seat ID.
- Rank or non-line designation.
- Role label.
- Evidence-backed state and last transition age.
- Current work summary, clipped to two lines.
- Model and effort when a runtime is active or configured.
- Active order/run count.
- Coverage marker.

Expanded node detail adds:

- Commission and command parent.
- Personal cell membership.
- Runtime/session/turn IDs.
- Model, provider, effort, harness/commission hash, account lane, and fallback.
- Tool/access grants.
- Current orders and work.
- Known spend.
- Workspace and board/Brain links.
- Recent actor timeline.
- Evidence used to derive status.

Rank is always adjacent to role. Model styling must not visually imply rank.

### 5.4 Edge types

Use shape and label, not only color:

| Edge | Direction | Rendering |
|---|---|---|
| Command | Superior -> subordinate | Solid line, arrowhead, `COMMAND` in detail |
| Delegation/order | Issuer -> target | Animated only while fresh/in flight; order ID on selection |
| Report | Reporter -> order owner | Dashed return line; correlated report ID |
| Personal staff | Officer -> cell member | Short bracketed branch, no command animation |
| Worker dispatch | Manager -> worker | Thin solid line, child assignment count |
| External interface | Ship seat -> external seat | Double-line boundary crossing |
| Observation | Sensor -> observed source | Dotted line visible only in coverage mode |
| Landing | Candidate workspace -> broker -> main | Step path shown in change trace |

Motion stops under `prefers-reduced-motion`. A still edge retains direction with arrowheads and labels.

### 5.5 Map modes

A segmented control changes the evidence overlay without changing topology:

- **Structure:** command, staff, department, and external relationships.
- **Live work:** only active/queued/stalled causal paths emphasized.
- **Coverage:** sensors, last-seen age, blind sources, and redaction boundaries.
- **Spend:** current-window known cost, unknown cost, and grant pressure by actor.

Map mode and time range are encoded in the URL. Filters do not delete nodes; filtered-out nodes remain as
quiet structural context or are replaced by an explicit collapsed count.

### 5.6 Attention rail

The map shares the first viewport with a narrow attention rail, not a floating card stack. It contains
only actionable or truth-degrading states:

- Failed, blocked, or stalled orders/runs.
- Invalid provenance chain or rejected event.
- Disconnected/stale sensor during an active watch.
- Unknown/unpriced cost against a metered lane.
- Ungranted tool/connector attempt.
- Writable main working-copy activity outside the landing broker.
- Workspace collision, dirty abandoned workspace, failed tests, or landing conflict.
- Unmanned endpoint with queued work.
- Orphan executable work, broken primary lineage, missing root mission, or a board-only row presented as
  authorized work.
- Unacknowledged delivery beyond its SLA, dead-letter delivery, duplicate standing-order trigger, or
  expected standing-order trigger with no run.

Each alert states the source, age, owner, and next available evidence link. No generic red dot.

## 6. Command Graph, orders, and work timelines

### 6.1 No-loss Command Graph

The Command view is the canonical frontend for the Ship Computer's no-loss work ledger. It joins three
typed planes without collapsing their semantics:

```text
AUTHORITY
directive / standing_order / standing_order_run / mission / objective / order
  ->
EXECUTION
epic / task / subtask / attempt
  ->
RETURN
evidence / report / decision
```

`intake_item` appears before authority as non-executable material awaiting Captain adoption or decline.
It must never look queued for execution.

Every executable item displays a root mission breadcrumb in its row, node, timeline event, search result,
and drawer header:

`Mission MIS-... / Objective OBJ-... / Order ORD-... / Epic EPC-... / Task TSK-...`

The breadcrumb follows the immutable primary-parent chain. Secondary `contributes_to`, `depends_on`, and
`blocked_by` links appear separately and never masquerade as authority ancestry. Selecting any breadcrumb
segment pivots to that ancestor while preserving the selected time and filter context.

No executable node is treated as valid without exactly one primary parent and a valid Captain-owned root
mission. The UI receives the validation result from the Ship Computer; it does not attempt to repair or
guess lineage. Invalid nodes remain visible in a red `ORPHAN / BROKEN LINEAGE` lane with the failed
invariant, last known owner, source, and disposition state.

The Command view header always shows:

- Root missions open / held / awaiting decision.
- Unacknowledged deliveries and the oldest ack-SLA breach.
- Dead-letter deliveries.
- Orphan executable nodes.
- Broken primary-lineage links.
- Return-pending reports and evidence awaiting an authorized decision.

Orphan and broken-lineage counts are repeated in the persistent chrome and Coverage & Health view. A zero
is meaningful and visible; a nonzero value uses failure treatment and cannot be muted.

### 6.2 Four first-class flow views

The Command view provides four equal flow selectors. Each supports `Graph`, `List`, and `Timeline` modes,
uses the same filters, and preserves a stable deep link.

| Flow | Root and scope | Required content |
|---|---|---|
| **Mission Flow** | One Captain-owned mission | Authority basis, objectives, orders, all execution descendants, evidence/reports, decisions, acceptance and remaining gaps |
| **Standing Order Flow** | One versioned standing-order definition | Versions, triggers, expected occurrences, runs, spawned mission/order chains, missed/duplicate/suppressed triggers, outcomes and decisions |
| **Epic Flow** | One epic under one order | Root mission breadcrumb, accountable/executing owners, tasks/subtasks/attempts, dependencies, evidence, report and review state |
| **Task Flow** | One task or subtask | Parent chain, assignment/delivery/ack, attempts, model/tools/workspace/tests, output evidence, report/decision return |

All three modes expose the same facts:

- Canonical phase and type-specific state.
- Accountable owner, executing owner, destination, and route.
- Delivery and acknowledgement state with SLA age.
- Evidence required, evidence returned, report, and acceptance owner.
- Grant, budget, known cost, unknown cost, and budget pressure.
- Blocker, staleness, hold, cancellation, supersession, and deadline.
- Source coverage and the event IDs supporting observed execution.

**Graph** emphasizes parent/child, route, dependency, and return edges. **List** is the dense audit and
sorting surface. **Timeline** aligns desired command transitions with observed provenance events. Mode is a
presentation choice only; it cannot change lifecycle or hide invalid lineage.

### 6.3 Captain command funnel and return path

The default Command overview shows a wide, left-to-right funnel:

```text
Commodore directive / active standing authority
  -> Captain intake and acknowledgement
  -> Captain-owned mission
  -> objectives
  -> typed orders and routes
  -> officer / personal cell / Science / Chief Engineer interface
  -> epics / tasks / attempts
  -> evidence and report return
  -> authorized decision
  -> accepted closure / revision / rejection / cancellation / supersession
```

The forward command path and return/report path use distinct edge styles and labels. The center of the
funnel highlights the Captain as command authorizer without implying that every descendant executes in
the Captain runtime. Clicking a funnel segment filters all four flow views to that plane and phase.

The return lane remains visibly open until the appropriate acceptance decision arrives. Attempt success,
task done, report submitted, and mission accepted are distinct states. The frontend cannot promote one to
another.

### 6.4 Standing Order Flow

A standing-order definition is a versioned authority object, not a badge or ambient permission. Its detail
starts with definition identity, current version/state, issuer, authority basis, accountable Captain,
scope, exclusions, budget/grant bounds, trigger, concurrency, review, expiry, and suspension policy.

The version rail shows every immutable version and the transition that activated, held, revoked, expired,
or superseded it. Selecting a version updates the trigger ledger and run list without rewriting history.

The trigger ledger aligns expected and observed occurrences:

- Expected occurrence/time/window and occurrence key.
- Source trigger event or authenticated manual actor/reason.
- Detected time, grace period, duplicate-suppression key, and disposition.
- Run ID and exact standing-order version.
- Attached/spawned Captain mission and order chain.
- Delivery, acknowledgement, outcome, evidence, report, and decision.

Explicit exception states are `missed trigger`, `duplicate suppressed`, `duplicate integrity conflict`,
`unacknowledged`, `dead letter`, `run failed`, and `run without valid mission attachment`. Aggregate counts
at the top always reconcile to the visible filtered ledger. A duplicate delivery that returns an existing
run is displayed as idempotent suppression, not new work.

### 6.5 Order ledger

The Orders view is a dense, sortable table with expandable rows. Default columns:

- Order ID and created time.
- Issuer -> target.
- Objective, clipped with full text in detail.
- Priority and grant.
- Lifecycle and current owner.
- Acceptance progress.
- Child assignment count.
- Last evidence age.
- Known cost / unknown-cost marker.
- Report state.

The lifecycle must come from authoritative Ship Computer projections, not filename matching or incidental
text. Target lifecycle vocabulary:

`issued -> delivered -> accepted -> running -> reporting -> completed`

Terminal alternatives are `rejected`, `cancelled`, `failed`, `expired`, and `superseded`. `queued` may
describe transport state between issued and delivered but cannot mean accepted or running. A report does
not mean completed until the acceptance projection records completion.

### 6.6 Causal work trace

Opening an order shows a vertical causal trace:

1. Authenticated order envelope.
2. Transport/delivery evidence.
3. Acceptance, rejection, or timeout.
4. Child assignments and delegated grants.
5. Model turns and tool calls.
6. Workspaces, files, tests, reviews, and candidate changes.
7. Reports mapped to acceptance criteria.
8. Landing/seal or explicit unlanded result.
9. Remaining uncertainty and coverage gaps.

Parallel child work uses aligned lanes on desktop and an ordered tree on mobile. The timeline must show
both occurred time and Ship Computer observed time where delay or clock skew matters.

### 6.7 Actor and work timelines

Every actor, workspace, board item, model turn, tool call, Brain write, and landing detail can pivot to a
shared timeline view. Timelines support:

- Follow live or freeze at a cursor.
- Absolute/local time and relative age.
- Group by trace, order, actor, source, or event class.
- Expand/collapse repeated low-level events without hiding their count.
- Compare two actors or traces in aligned time.
- Copy a stable deep link to the selected event and filter state.

## 7. Provenance drilldowns

An event drawer exposes the normalized event and its source evidence without forcing the operator to
read raw JSON first.

### 7.1 Human-readable evidence

- Summary, class, status, truth label, and exact timestamps.
- Actor, target, order, trace, parent trace, work, session, turn, and workspace IDs.
- Model, effort, provider, harness/commission hash, tool, and connector when present.
- Source sensor, source record locator, source sequence, and ingestion time.
- Integrity state: accepted/rejected, event hash, previous hash, chain head, and validation result.
- Redaction state and field-level reasons.
- Derived-state explanation, including input event IDs and projection version.

### 7.2 Raw evidence

The raw tab shows sanitized normalized JSON and, when authorized, the sanitized source record. It never
renders secrets into the DOM and never relies on CSS to hide a sensitive value. Credential-shaped values
are removed server-side and represented as a redaction object with a digest suitable only for correlation.

Hidden provider reasoning is represented as:

`Unavailable: the provider does not expose private reasoning. Visible response and tool evidence follow.`

Do not use `redacted` for evidence the system never possessed.

### 7.3 Chain and source navigation

The operator can move to previous/next chain entries, the parent/child trace, the original order, the
actor, and the source sensor. If chain validation fails, the event remains inspectable but every derived
projection that depends on it is marked unverified until reconciliation.

## 8. Resource and control views

### 8.1 Models & Spend

This view separates capability choice from authority. It provides:

- Live and historical model invocations by actor, role, provider, model, effort, and harness hash.
- Visible prompt/response sizes, tokens or provider units when available, latency, outcome, fallback,
  refusal, and retry.
- Known cost, estimated cost, and unknown cost as distinct numeric states.
- Grant ID, owner, budget, period, consumed amount, remaining amount, and custodian.
- Cost by order, department, personal cell, actor, model, and time window.
- Candidate/configured model slots clearly separated from executed model turns.
- Alerts for missing grant, budget pressure, fallback, unpriced usage, and account-lane mismatch.

Never display `$0` when cost is unknown. Use `unknown` and show why.

### 8.2 Tools & Access

Two linked surfaces:

1. **Invocation ledger:** tool, actor, time, bounded argument summary, result class, duration, grant,
   connector, and trace.
2. **Effective access matrix:** actor rows by tool/capability columns, showing absent, configured,
   granted, active, expired, or denied.

The matrix distinguishes typed Bridge tools from raw filesystem, shell, browser, connector, deploy,
release, and custody capabilities. It must make these boundaries obvious:

- Captain and locked officers have only their typed harness tools.
- Advisors and Ensign/Scientist thinking partners have bounded cognitive/team/source tools and no ship
  command.
- PAs operate only their officer-scoped mini-Ops and Brain interfaces.
- Personal Engineers and Ensign workers write only in isolated workspaces.
- Only the landing broker may land to main under the target architecture.

Denied or absent is not a failure state unless an invocation attempted to cross the boundary.

### 8.3 Workspaces & Changes

The default view is a pipeline:

`order -> engineer -> worker workspace -> files -> tests -> review -> candidate -> broker -> main seal`

For each workspace show:

- Workspace ID, path alias, owner, actor, model/effort, base change, current change, and creation time.
- Read/write scope and grant.
- Dirty/clean state, changed file count, diff summary, and last write.
- Test commands, result, duration, log pointer, and coverage artifact.
- Review loops and requested fixes.
- Candidate identity, broker validation, conflicts, landed change, and cleanup state.

Paths exposed to the browser are logical aliases by default. Raw local paths require an operator scope and
must never carry credentials. Any write to the main working copy outside the trusted broker becomes a
high-priority alert.

### 8.4 Boards & Memory

This view makes ownership explicit rather than merging all state stores:

- Main ship board, department boards, Captain personal board, Advisor boards, and Personal Engineer
  boards remain separate.
- Currents show owner, age, focus, next action, blocker, and source.
- Brain stores show namespace, owner, node counts by class, size, growth, last write, focus, and health.
- Brain write evidence shows proposer, exact delta/hash, ratification, writer, resulting version, and seal.
- PA ledgers show actions and records; they are not silently treated as officer beliefs.
- Board transitions show mechanical writer, dictating authority, prior/new state, comment, and event ID.

Memory retrieval informs a decision; it never appears as an authenticated command.

### 8.5 Memory lens

The Boards & Memory view includes a first-class `Memory` lens with five visibly separate strata. It must
not present a generic combined memory count.

| Stratum | Owner and purpose | Default Bridge visibility |
|---|---|---|
| **Ship Computer operational memory** | Ship Computer; append-only observable events, command revisions, evidence, and projections | Event/command metadata and authorized payloads |
| **Ship Brain** | Ship; curated shared semantics, doctrine, and institutional knowledge | Node identity, class, version, author/proposer, governance operation, source, hash, freshness; content per policy |
| **Captain/officer private Brains** | One mind and its PA process; private beliefs, conclusions, durable personal knowledge | Store health and typed operation metadata; raw private content hidden by default |
| **Current and scratchpads** | Owning seat; ephemeral focus, blockers, decomposition, and temporary synthesis | Typed read/write metadata, freshness, version/digest, and policy-permitted preview; private text hidden by default |
| **Sealed immutable records** | Named record custodian; decisions, evidence, reports, and releases with record supremacy | Seal identity, author, time, digest, continuity, supersession/correction links, and authorized artifact view |

Each store row shows stable store/namespace ID, owner, memory stratum, access class, current version or chain
head, hash/digest, latest typed operation, operation actor, authorization/ratification state, freshness,
coverage, and redaction state. Store size and growth are supporting metrics; they do not imply health,
truth, or authority.

Typed observable operations include, as applicable:

- `memory.read`, `memory.search`, `memory.stage`, `memory.ratify`, `memory.write`, and `memory.write.failed`.
- `brain.node.proposed`, `brain.node.ratified`, `brain.node.written`, `brain.node.superseded`, and
  `brain.node.corrected`.
- `scratchpad.read`, `scratchpad.write`, `current.read`, and `current.write`.
- `record.sealed`, `record.verified`, `record.corrected`, and `record.superseded`.

The operation drawer shows operation ID, actor, author/proposer, owner, permission basis, affected node or
artifact ID, version, before/after digest where policy permits, source/cause event, receipt, timestamp,
freshness, and redaction. A successful write receipt proves the boundary accepted a write; it does not make
the content correct, public, doctrine, command authority, or sealed.

Private Brain, current, and scratchpad content is not placed in initial HTML, list responses, search
indexes available to ordinary Bridge scope, screenshots, or client logs. An authorized content reveal is a
separate on-demand read with an explicit access reason and its own observable access event. Provider-hidden
reasoning is never presented as memory and cannot be revealed.

Cross-stratum movement is shown only when separately governed events support it. Scratchpad text cannot
silently become private Brain memory; private Brain content cannot silently become Ship Brain doctrine;
event summaries cannot become sealed records. The flow shows the proposal, ratification, write, and seal as
distinct nodes with their own actors and receipts.

## 9. Coverage and health

### 9.1 Coverage dashboard

Coverage is an inventory, not a single percentage. Group by source class:

- Captain and locked officer runtimes.
- Advisor, Ensign/Scientist, PA, and personal-engineering runtimes.
- Local managers and workers.
- Incubator PM and external factory interface.
- Order/report queues.
- Models/providers.
- Tool and connector brokers.
- Boards, currents, Brains, and PA ledgers.
- Workspaces, VCS, tests, candidates, broker, and main seals.
- Spend/grants.

Each row shows expected sensor, sensor version, permission, last heartbeat, last event, lag, dropped or
rejected event count, backfill boundary, integrity state, and explicit limitation.

The aggregate header must state both numerator and denominator, for example `24 / 31 expected sources
fresh`, and list what defines the denominator. Never report `77% covered` without that definition.

### 9.2 Health states

Use these source states consistently:

- `healthy`: heartbeat and events inside contract; chain valid.
- `quiet`: healthy heartbeat, no events expected or observed.
- `lagging`: events arrive beyond latency target.
- `stale`: heartbeat beyond freshness window.
- `disconnected`: stream or sensor explicitly down.
- `invalid`: schema, signature, or chain validation failed.
- `partial`: some event classes unavailable.
- `unsupported`: no sensor exists.
- `permission-blocked`: sensor exists but current operator cannot inspect it.
- `redacted`: event exists; one or more authorized fields removed.

`quiet` is not `healthy` if the heartbeat is missing. `unsupported` is not `disconnected`.

### 9.3 Redaction and privacy

The health view lists redaction policy version, counts by reason, and affected source classes. It must not
show secret material in tooltips, HTML comments, embedded JSON, client logs, analytics, or error traces.
Prompts and visible responses are observable only after server-side secret scanning and role-based
filtering. Provider-hidden reasoning remains unavailable rather than redacted.

## 10. Search, filters, and interactions

### 10.1 Global search

Search accepts stable IDs, display names, ranks, roles, order objectives, summaries, model/tool names,
workspace aliases, board items, and file paths permitted to the operator. Results are grouped by entity
type with timestamp and evidence state. Secret/raw payload search remains server-side and permissioned.

### 10.2 Filter vocabulary

All views share URL-encoded filters:

- Time range or replay cursor.
- Actor, rank, role, department, and personal-cell owner.
- Order, trace, work, session, turn, workspace, board, or grant ID.
- State, truth label, source health, redaction state, and event class.
- Model, provider, effort, tool, connector, and known/unknown cost.
- Live only, exceptions only, or coverage gaps only.

Show active filters as a compact summary line with one clear-all command. Avoid rows of decorative pills.

### 10.3 Keyboard and pointer behavior

- `/` focuses search.
- `g` then a documented view key moves between primary views.
- Arrow keys move among map nodes and table rows.
- `Enter` opens detail; `Escape` closes one drawer level.
- `f` toggles live follow when focus is not in an input.
- Zoom uses familiar `+`, `-`, reset, and fit icons with tooltips.
- Hover may preview; every function must also work by keyboard, touch, and click.

No visible instructional paragraph should occupy the application. Tooltips, accessible labels, and the
manual carry interaction guidance.

## 11. Responsive behavior

### 11.1 Wide command display, 1440px and above

- Persistent top chrome and primary view tabs.
- Ship map occupies the main width; attention rail is 280-340px.
- Two investigation drawers may be pinned without covering the selected map node.
- Tables use sticky identity and status columns.

### 11.2 Standard desktop/tablet, 768px to 1439px

- Attention rail becomes a collapsible right drawer.
- One investigation drawer at a time.
- Map retains horizontal structure with pan/zoom and fit controls.
- Resource tables may collapse secondary columns into an expandable detail row.

### 11.3 Mobile, 320px to 767px

- Top chrome wraps into two stable rows; counts do not resize controls.
- Primary tabs become a labeled overflow menu plus current-view selector.
- The map has a semantic outline mode by default: command tree, officer, then attached personal cell.
  The operator may switch to the pannable graph.
- Detail uses a full-screen sheet with a sticky close/back bar.
- Timelines become one causal lane with indented child events.
- No horizontal page overflow, clipped control text, or overlapping node labels.

## 12. Accessibility

- Meet WCAG 2.2 AA contrast for text, controls, focus, and state markers.
- All map nodes are real focusable controls with a logical tree order.
- SVG edges are supplementary; a synchronized screen-reader relationship list states every selected
  node's parent, reports, staff, children, and active traces.
- Live events use a throttled, opt-in polite announcement region. Do not read every event by default.
- State never relies on color or pulse alone.
- Respect reduced motion, increased contrast, text zoom to 200%, and OS font rendering.
- Focus remains stable when live data arrives. New events never steal focus or close a drawer.
- Use fixed minimum hit targets of 44 by 44 CSS pixels for touch controls.
- Letter spacing is `0`; compactness comes from type size, weight, layout, and spacing rather than
  compressed or expanded tracking.
- Use plain, concise labels and expose exact IDs to assistive technology.

## 13. Future visual-design requirements

No Bridge visual direction is selected. The requirements below constrain the later from-scratch design;
they are not permission to skin fixture data and call it the Bridge. The Codex Frontend Manager begins
that work only after the restart gate in section 0.1 passes.

### 13.1 Character

- Quiet, technical, dense, and work-focused.
- Near-black neutral ground with distinct functional accents: green for evidenced live/success, amber
  for attention/unknown, red for failure/invalid, blue for identity/selection, cyan for external
  boundaries, and violet only for Brain/memory.
- Use neutral directional image vignettes only to preserve data legibility. Do not use decorative gradient
  backgrounds, orbs, bokeh, ornamental glows, or marketing copy.
- No floating page-section cards. Use full-width bands, ruled tables, and unframed map space.
- Cards are reserved for repeated actor/work items and use at most 6px radius. Do not nest cards.
- Familiar Lucide icons may label controls; do not draw custom icons when a standard symbol exists.
- The functional topology map remains the primary working asset. Any future environmental identity layer
  must yield to topology, attention, lineage, coverage, and investigation controls.
- The production first viewport must expose operational state and cannot become a landing page or require
  an "enter" step.

### 13.2 Typography and density

- Human-readable sans serif for summaries and objectives.
- Monospace for IDs, time, model/tool names, hashes, and states.
- Use modest view titles, 16-20px; map and table headings, 12-14px; data, 11-13px.
- Zero letter spacing everywhere.
- Long IDs and objectives wrap or truncate with explicit reveal; they never resize a node or button.

### 13.3 Motion

- Motion communicates new evidence, active causal flow, selection, or reconnect only.
- No ambient animation.
- New-event highlight fades once over 600-900ms.
- Live edge motion is subtle and capped; many simultaneous paths collapse into a count to avoid noise.

## 14. Assumed Ship Computer data contract

The frontend must consume the Ship Computer as the sole live read model. It must not parse repository
files, inspect processes, or derive organization state in the browser. Exact route names may be aligned
with the Ship Computer system design, but the following versioned capabilities are required.

### 14.1 Read APIs

| Capability | Assumed request | Required response |
|---|---|---|
| Service health | `GET /api/v1/status` | Service, store, chain, index, checkpoint, queue, schema, and version health |
| Initial view | `GET /api/v1/snapshot` | Snapshot ID, accepted sequence, topology, attention, command counts, active work, recent events, coverage summary |
| Live stream | `GET /api/v1/stream` with `Last-Event-ID` on resume | Authorized compact SSE deltas with accepted sequence and snapshot-required recovery |
| Event search | `GET /api/v1/events?...filters` | Cursor-paged normalized event summaries |
| Event detail | `GET /api/v1/events/<event-id>` | Sanitized event, source, integrity, redaction, derivation |
| Correlations | `GET /api/v1/correlations/<id>` | Causal event graph for a turn, order, task, or workspace |
| Actor | `GET /api/v1/actors/<actor-id>` | Identity, rank, current work, model, tools, events, coverage, personal cell |
| Mission flow | `GET /api/v1/missions/<mission-id>` | Full authority, objectives, routes, execution descendants, return, decisions, lineage validation |
| Standing Order flow | `GET /api/v1/standing-orders/<id>` | Definition versions, expected/actual triggers, runs, duplicate suppression, misses, spawned chains, outcomes |
| Work node | `GET /api/v1/work/<node-id>` | Typed node, immutable versions, primary lineage, secondary edges, transitions, budget/evidence state |
| Order | `GET /api/v1/orders/<order-id>` | Authoritative lifecycle, delivery, acknowledgement, report, evidence, acceptance, causal links |
| Delivery | `GET /api/v1/deliveries` | Outbox/inbox, ack SLA, retries, dead-letter state, and reconciliation |
| Task | `GET /api/v1/tasks/<task-id>` | Task lineage and board history joined to attempts, workers, tests, and seals |
| Workspace | `GET /api/v1/workspaces/<workspace-id>` | Scope, owner, changes, tests, landing, and cleanup |
| Spend/resources | `GET /api/v1/costs` plus referenced grant/resource queries | Measured spend, unknowns, grants, model, actor, order, and cost class |
| Memory lens | Snapshot store projection plus `GET /api/v1/events` filtered to Brain/memory/current/scratchpad/seal families | Strata, namespaces, typed operations, versions, hashes, authors, freshness, access/redaction, authorized detail refs |
| Coverage | `GET /api/v1/coverage` | Expected sensors, last seen, lag, failures, blind spots, exclusions, and redaction policy |

Every list API supports cursor pagination, time range, stable sort, field filters, and a returned filter
echo. No endpoint sends secrets or private provider reasoning to the client.

The frontend also assumes Command Graph summary queries or snapshot projections can return filtered lists
for Mission, Standing Order, Epic, and Task flows. If the first API implements only per-ID endpoints, the
Incubator must not reconstruct global lineage by crawling in the browser; the Ship Computer must add a
bounded server-side query.

### 14.2 Normalized event envelope

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

This matches the Ship Computer canonical envelope. Model, tool, cost, and redaction detail may be in the
authorized payload or joined projections keyed by `model_run_id`, `tool_run_id`, and `grant_id`; the
frontend must not require an invented nested shape. Nullable fields remain present or are described by the
schema. The frontend must not guess semantic meaning from summary text.

### 14.3 Actor/topology contract

Each actor node requires:

- Stable ID, display name, rank/designation, role, tier, and commissioned/unmanned status.
- Command parent, department owner, personal-cell owner, and external boundary.
- Current lifecycle state, truth state, `state_event_ids`, and freshness deadline.
- Configured and active model/runtime fields kept separate.
- Tool/access/grant references.
- Current order/run/workspace/board/Brain references.
- Coverage state and last observed time.

Each edge requires stable ID, source, target, relationship kind, direction, truth, and supporting event or
configuration IDs.

### 14.4 Command node and order projection contract

A Command Graph node includes `node_id`, `node_type`, immutable `record_version`, `root_authority_id`,
`root_mission_id`, `primary_parent_id`, secondary edge arrays, creator, accountable/executing owner,
destination and route, authority basis, canonical phase, type-specific state, acknowledgement/SLA state,
evidence requirements/returns, report/decision references, grant/budget/cost state, timestamps, and
lineage-validation results. Executable nodes missing exactly one valid primary parent or Captain-owned
root mission are returned with an explicit broken-lineage state; the server does not omit them.

An order projection additionally includes the authenticated envelope, authoritative lifecycle, delivery
and receipt evidence, lifecycle event IDs, child work IDs, acceptance criteria with per-criterion evidence
state, reports, cost aggregate, last event, coverage caveats, and projection version. Text mentioning an
order ID is not enough to correlate a report.

A standing-order projection includes every immutable definition version, expected-occurrence ledger,
observed trigger evidence, missed occurrences, idempotently suppressed duplicates, integrity conflicts,
run IDs, exact version used by each run, attached/spawned mission and order chains, delivery state,
outcomes, evidence, reports, decisions, review, expiry, and suspension state.

### 14.5 Stream behavior

- Delivery is at least once; the client deduplicates by `event_id`.
- `accepted_seq` is monotonic within the Ship Computer store and is the `Last-Event-ID` reconnect cursor.
- Stream messages include `event.appended`, `actor.changed`, `order.changed`, `coverage.changed`,
  `command.changed`, `standing_order.changed`, `delivery.changed`, `attention.changed`, and `heartbeat`.
- A `snapshot_required` message or detected sequence gap causes snapshot reconciliation before live follow
  resumes.
- Client clocks never determine lifecycle. Server time and source timestamps are both retained.

### 14.6 Authentication and transport

- Bind to loopback by default.
- Require a short-lived operator token or authenticated local session for every HTML, API, stream, and
  mutation request.
- Validate Host and Origin on mutation routes.
- Apply role-based field filtering on the server.
- Send a restrictive content security policy and no-referrer policy.
- Never place bearer tokens in committed HTML, logs, screenshots, query strings intended for sharing,
  or embedded JSON.

## 15. Deferred Codex Frontend Manager design brief

**DO NOT EXECUTE THIS BRIEF UNTIL SECTION 0.1 PASSES.** When it does, the Commodore gives this brief, this
plan, the real API contract, the accepted voyage fixture, and the ship organization report to the Codex
Frontend Manager. The resulting from-scratch product and visual package becomes the accepted design input
to the Chief Engineer. The Chief Engineer then gives that versioned package to the Incubator PM for
engineering implementation and retains its artifacts and review record in the build trail.

```text
DESIGN OWNERSHIP: Codex Frontend Manager
PRODUCT: Ship Computer Bridge visual and interaction design

You are the design lead for a serious live operations console. Design the actual first-screen operator
experience, not a marketing page. The Commodore must be able to see the whole AI-captained ship working:
command, officers, each officer's Thinking/Operations/Engineering personal cell, departments, workers,
orders, reports, models, tools, costs, boards, memory, workspaces, tests, landings, provenance, and every
coverage gap the Ship Computer knows about.

Use docs/design/ship-computer-bridge-frontend-plan.md as the product contract. Study the existing
docs/viewers/bridge.html and docs/viewers/ship-org-build-state.html before drawing. Preserve the quiet,
dense flight-operations character, but improve hierarchy, legibility, causal flow, responsive behavior,
and investigation. The live topology map is the primary visual asset. Personal cells must be visibly
attached to their owning officer. The Chief Engineer and external Incubator PM must remain distinct.

Produce three materially different low-fidelity layouts for the Ship view, compare them against the ten
operator questions, then develop one newly selected post-gate direction into desktop (1440x900), wide (1920x1080),
tablet (1024x768), and mobile (390x844) designs. Also design one order trace, one provenance event drawer,
one coverage failure, and one Models & Spend view.

Design a first-class Command Graph with graph/list/timeline switches for Mission Flow, Standing Order
Flow, Epic Flow, and Task Flow. Every item needs its root-mission breadcrumb, parent/child drilldown,
state, owners, acknowledgement, evidence, and budget. Make the Captain command funnel and return/report
path immediately legible. Orphan count and broken-lineage count must always be visible. Standing Order
Flow must cover definitions and versions, expected and actual triggers, every invocation/run, spawned
mission/order chains, missed and duplicate triggers, deliveries, outcomes, evidence, and decisions.

Hard constraints:
- no marketing landing page, decorative gradients/orbs, stock art, or feature-explanation copy;
- do not inherit the Shipwright Manual composition, commissioned guardian artwork, or solitary guardian as
  the Bridge shell; establish the operational identity from real workflow and data after the restart gate;
- no cards inside cards and no floating-card treatment for page sections;
- cards at 6px radius or less;
- zero letter spacing;
- no color-only states;
- no hidden or implied chain of thought;
- recorded, receipt, reported, derived, configured, unknown, unverified, unavailable, and redacted must
  look distinct without collapsing canonical truth and evidence/access qualifiers;
- no pulse without fresh runtime evidence;
- no mutation controls in the first read-only release;
- all text and controls must fit at every target viewport;
- reduced-motion and keyboard operation are first-class.

Deliver annotated layout specifications, component/state inventory, tokens, interaction notes, empty and
degraded states, and implementation-ready acceptance notes. Name any point where the data contract is
insufficient. Do not write production code until the Chief Engineer accepts the direction.

Include a Memory lens that keeps Ship Computer operational memory, Ship Brain, private Captain/officer
Brains, current/scratchpads, and sealed records visibly distinct. Show typed operations, version/hash,
author/actor, freshness, access, and redaction. Never expose raw private content by default or imply access
to provider-hidden reasoning.
```

The Codex Frontend Manager does not silently change truth semantics, rank, authority, topology, or API
contracts. The Chief Engineer checks implementation readiness against this document and sends any
data-contract issue back to the Ship Computer owner and Frontend Manager before implementation.

## 16. Incubator execution work packages

These packages are commissioned through Chief Engineer -> Incubator PM. The PM may adapt worker count and
sequencing, but each package retains its acceptance boundary and isolated workspace.

### WP0: Contract fixtures and truth-state harness

**Deliver:** Versioned TypeScript/JSON schemas or equivalent frontend models; deterministic fixture sets
covering healthy, quiet, active, queued, stalled, failed, invalid-chain, redacted, unavailable, unmanned,
external, unknown-cost, and reconnect cases.

**Acceptance:** No screen requires repository parsing or summary-text inference. Fixtures validate against
the Ship Computer schemas. Every status shown in later packages is representable.

### WP1: Accepted Codex visual system

**Deliver:** The Codex Frontend Manager artifacts from section 15, newly selected post-gate direction, design tokens, component/state
inventory, and target-viewport layouts.

**Acceptance:** Chief Engineer records why the selected layout best answers the ten operator questions;
Commodore review is requested before production visual implementation. No production code in this package.

### WP2: Application shell and live data client

**Deliver:** Authenticated application shell, persistent command chrome, primary view routing, snapshot
load, stream/reconnect/reconciliation, live-follow/replay, global search entry, URL state, and degraded
connection states.

**Acceptance:** Duplicate and out-of-order event fixtures do not duplicate or regress state. Stream gaps
force reconciliation. Focus survives updates. No token is exposed in rendered data or screenshots.

### WP3: Ship map and personal cells

**Deliver:** Deterministic responsive topology layout, attached personal cells, typed edges, mode overlays,
attention rail, actor drawer, semantic outline, keyboard navigation, and reduced-motion behavior.

**Acceptance:** All configured actors and edges render without overlap at target viewports. Personal staff
ownership and rank are correct. No configured/unmanned node looks active. External Incubator boundary is
unambiguous.

### WP4: Command Graph, orders, activity, and provenance

**Deliver:** Captain command funnel; Mission, Standing Order, Epic, and Task flows in graph/list/timeline
modes; root-mission breadcrumbs; order and delivery ledgers; causal trace; event stream; actor/work
timelines; event drawer; integrity chain; redaction display; raw sanitized evidence; filters; compare; and
deep links.

**Acceptance:** Report correlation uses authoritative projection data. Historical start events cannot
create a false active state. Failed/invalid chain fixtures visibly downgrade dependent projections.
Orphans, broken lineage, unacknowledged/dead-letter deliveries, missed/duplicate standing-order triggers,
and open return paths remain visible and reconcile to their header counts.

### WP5: Models, tools, spend, workspaces, boards, and the Memory lens

**Deliver:** The four resource/control views in section 8, with shared filters and cross-links to traces.

**Acceptance:** Configured and executed models are distinct; unknown cost never displays as zero; access
and invocation are distinct; isolated workspaces and brokered landings are reconstructable; board and
Brain ownership never collapse into one store. Ship Computer memory, Ship Brain, private Brains,
current/scratchpads, and sealed records remain distinct; private content is absent from initial payloads.

### WP6: Coverage, security, accessibility, and performance

**Deliver:** Coverage inventory, source health, redaction policy view, authorization field filtering,
keyboard/screen-reader behavior, responsive polish, virtualization, and performance instrumentation.

**Acceptance:** All checks in sections 12, 17, and 18 pass. Secret-canary fixtures never reach DOM, logs,
screenshots, or client errors.

### WP7: Dogfood and landing

**Deliver:** Read-only deployment behind local authentication, recorded live watch, defect log, fixed
screenshots, test evidence, operator runbook, rollback, and brokered candidate landing.

**Acceptance:** One complete Captain order and one personal-engineering or Incubator work path are traced
from instruction through report/change evidence. Coverage gaps remain visible. Commodore accepts the
read-only experience before any mutation package is commissioned.

## 17. Performance and resilience budgets

- Render useful snapshot state within 1.0 second on loopback at the 95th percentile for the reference
  fixture; show a factual loading state, not a blank map.
- Apply a normal streamed event within 100ms of receipt without full-page replacement.
- Keep pan, zoom, scroll, and drawer motion at 55-60fps on the reference desktop fixture.
- Virtualize event/order tables beyond 200 visible rows and map only visible detail labels at large scale.
- Do not embed unbounded payloads in the initial HTML. Fetch sanitized detail on demand.
- Reconcile without losing selection, scroll, filters, pinned drawers, or keyboard focus.
- Continue showing the last internally consistent snapshot when offline, with a prominent age and
  `OFFLINE` state. Never continue a live pulse while disconnected.
- Bound stream memory; discard view cache by policy, not source evidence from the Ship Computer store.
- A malformed event is quarantined, counted, and inspectable through health; it does not crash the app.

## 18. Verification and visual acceptance

### 18.1 Automated functional checks

- Unit tests for truth/status mapping, freshness, filter serialization, event deduplication, cursor gaps,
  lifecycle rendering, cost states, redaction labels, and rank/role/model separation.
- Contract tests against the Ship Computer schema and representative live snapshots.
- Integration tests for snapshot -> stream -> reconnect -> reconcile.
- Negative tests proving historical `started`, incidental order-ID text, configured model slots, and open
  board items cannot create false runtime/completion state.
- Secret-canary tests for prompts, tool arguments, connectors, errors, embedded state, and screenshots.
- Command Graph invariant tests for missing/duplicate primary parents, wrong root mission, board-only work,
  unacknowledged and dead-letter delivery, standing-order missed/duplicate triggers, and unclosed return
  paths. Orphan and broken-lineage counts must remain visible under every filter.
- Memory-lens tests proving typed operations map to the correct stratum; hashes, versions, author, freshness,
  access, and redaction render; private content and provider-hidden reasoning never enter initial payloads.

### 18.2 Playwright viewport matrix

Capture and review these fixtures at minimum:

| Viewport | Required captures |
|---|---|
| 1920x1080 | Full Ship map, two pinned drawers, dense active watch |
| 1440x900 | Default Ship view, personal cell expanded, Captain command funnel, attention rail |
| 1024x768 | Ship map with collapsed rail, Mission Flow trace, Coverage view |
| 390x844 | Semantic map outline, Task Flow sheet, causal timeline |
| 320x720 | Longest labels, overflow menu, disconnected and redacted states |

For every capture assert:

- No incoherent overlap, clipping, accidental horizontal page scroll, or text outside controls.
- The brand/ship identity, live/degraded state, last-event age, and coverage state are visible.
- The next operational band is hinted at without creating a hero.
- Personal cell ownership remains legible.
- Active, failed, configured, unverified, and unavailable states remain distinguishable in grayscale.
- Focus indicators, 200% text zoom, and reduced motion work.

### 18.3 Pixel and graph checks

- Compare stable fixture screenshots with reviewed baselines using a documented threshold; mask only
  clocks, random IDs, and intentionally live ages.
- Measure every map node and edge bounding box; fail on node-node, label-label, or control overlap.
- Assert the map viewport contains a minimum non-background pixel ratio and at least one visible node from
  every expected topology band. This catches blank or offscreen graph renders.
- Assert selected route pixels/edges connect the selected source and target bounding regions.
- If any canvas renderer is accepted, use `getImageData` checks at desktop and mobile to prove the canvas
  is nonblank, contains multiple functional state colors, and changes after a known stream event. Also
  test pixel ratio scaling and fallback accessible DOM parity.
- Run the same screenshots with unavailable webfonts/assets and ensure the layout remains usable.

### 18.4 Live dogfood acceptance

Playwright observes a real instrumented watch and records:

1. An actor changes from standing by to active only after a fresh runtime event.
2. An order appears, moves through authoritative lifecycle, and opens its causal trace.
3. A tool result opens with sanitized source evidence.
4. A worker workspace, file set, tests, review, candidate, and broker result cross-link.
5. The corresponding model, tool, grant/cost state, board, and coverage entries update without reload.
6. Disconnecting one sensor creates a visible coverage gap and stops dependent live claims.
7. Reconnection reconciles without duplicate events or lost operator state.
8. Mission, Standing Order, Epic, and Task flows show the same primary lineage in graph, list, and
   timeline modes; a fixture orphan remains impossible to miss.
9. A private Brain write updates operation metadata without placing private content in the page; a sealed
   record remains a separate immutable stratum.

## 19. Staged rollout

### Stage A: Design and contract, NOT BUILT

Complete WP0-WP1. Reconcile the frontend schema with the Ship Computer system design. Obtain Chief
Engineer implementation-readiness review and Commodore acceptance of the Codex Frontend Manager's newly
created post-gate direction.

### Stage B: Read-only mirror

Build WP2 against deterministic fixtures, then a read-only Ship Computer snapshot. Keep the current
generated Bridge available as rollback/reference. Do not claim live operation.

### Stage C: Live Ship overview

Build WP3, connect the stream, and prove live-state freshness, coverage gaps, and responsive map
acceptance. The overview may be called live only after the real watch test passes.

### Stage D: Investigation

Build WP4. Make order, trace, event, actor, source, and integrity navigation complete before adding
broader resource dashboards.

### Stage E: Full observable ship

Build WP5-WP6. Add models, tools, costs, workspaces, boards, memory, sensors, and health. Run a complete
read-only dogfood watch and close truth/security/accessibility failures.

### Stage F: Operational adoption

Complete WP7, land through the broker, publish rollback and operator runbooks, and make this frontend the
default Bridge only after Commodore acceptance.

### Stage G: Mutations, separately commissioned

Typed acknowledgements, comments, orders, grant operations, or release/landing controls require a new
design, threat model, authorization contract, confirmation behavior, and provenance lane. They are not
implied by this plan.

## 20. Non-goals and hull stress

This plan does not:

- Build or select the Ship Computer event store, sensor framework, API server, or authentication service.
- Prove that every source can expose the required data.
- Grant the Ship Computer hidden provider reasoning.
- Permit credential display, unbounded raw payloads, or unscoped filesystem paths.
- Make the Bridge an authority for orders, grants, boards, rank, release, or landing.
- Resolve exact per-model cost where a provider/account lane does not report it.
- Replace the Chief Engineer, Incubator PM, Security, CMO, Ops, or landing broker with a dashboard.
- Claim every personal cell, officer, sensor, or workspace path is currently live.

Open design risks that the Chief Engineer must carry into Incubator:

1. The topology may become too large for one graph once every officer's full personal cell and execution
   crew is live. Progressive expansion and semantic outline need scale fixtures before layout selection.
2. Sensor freshness contracts differ by source. The Ship Computer must own per-source deadlines; the
   browser cannot invent them.
3. Prompt/response observability can leak secrets or private data even when credentials are redacted.
   Server-side role filtering and retention rules are required before full payload display.
4. Exact cost may remain unavailable under subscription lanes. The interface must preserve unknown cost
   without creating misleading totals.
5. External Incubator telemetry may arrive through a different trust and clock domain. Boundary,
   ingestion delay, and source integrity must stay visible.
6. A beautiful map can overstate certainty. Truth, coverage, and derivation markers are part of the
   design system, not optional diagnostic detail.

Until the staged acceptance above is complete, the correct status is:

**SHIP COMPUTER BRIDGE FRONTEND: DESIGNED, NOT BUILT.**
