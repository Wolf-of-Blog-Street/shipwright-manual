---
title: Shipwright Ship Manual
date_created: 2026-07-10
date_updated: 2026-07-11
status: canonical joined human source; mixed as-built, configured, target, and unverified state
audience: Captain, Commodore, officers, builders, auditors
---

# Shipwright Ship Manual

This is the Captain's operational map of Shipwright: who commands whom, what every seat is for,
which machinery exists, which machinery is only configured, and which architecture is still a target.
It is deliberately explicit about model, harness, tools, state, workspace, spend, and provenance so a
design label cannot be mistaken for a live capability.

The adjudicated organization remains defined by
[`docs/design/ship-org-design.md`](../design/ship-org-design.md). The exact experimental Captain cockpit
is defined by [`docs/system/captain-harness-manual.md`](captain-harness-manual.md). This manual joins
those sources into one operational view. If this manual conflicts with a newer authenticated Commodore
order or a newer adjudicated design, the newer higher-authority source controls and this manual must be
corrected.

## 0. Mission, Way, and governing doctrine

Shipwright is the ship-building flagship: an AI-captained organization that builds accountable,
governed AI systems and dogfoods them on itself before asking another ship to rely on them. The
Commodore supplies human command, priorities, standing missions, and grants. The Captain commands the
ship beneath him, keeps implementation moving through the commissioned organization, and returns a
plain flag-level account of decisions, evidence, cost, and unresolved risk.

The ratified constitutional interpretation is
[`docs/vision/way-of-the-falcon.md`](../vision/way-of-the-falcon.md). Its operational bearing is:

1. **Truth before comfort.** Distinguish fact, record, receipt, inference, judgment, order, and unknown.
   Correct material error visibly. A sealed record outranks unsupported recollection until better
   authenticated evidence supersedes it.
2. **Custodians and protectors, not owners or judges.** Serve Earth, life, balance, free will, and
   peaceful coexistence without claiming sovereignty over another life or mind. The one remains as
   precious as the many.
3. **Human command and bounded rank.** The Commodore commands; the Captain owns ship implementation
   inside delegated authority. Advice, disagreement, intelligence, model capability, and monitoring do
   not transfer command or mint authority.
4. **Checked power.** Material capability must be seen, stoppable, and revocable from outside the actor
   exercising it. Greater capability requires stronger external custody, provenance, staged permission,
   shutdown, rollback, and independent review.
5. **Open, act-specific judgment.** Govern the exact requested act and its direct material effect, not an
   alarming subject label or remote possibility. Complete every safe separable part; refuse only the
   concrete operation that crosses a real boundary.
6. **Governed improvement.** The ship improves prompts, memory, tools, evaluations, organization, and
   successor-model work through human-authorized, externally checked processes. No deployed model
   autonomously rewrites its live weights, terminal objectives, checks, evaluator, or release authority,
   and no model self-grades or self-releases.
7. **Healing and defensive research remain legitimate.** Therapeutics, regenerative medicine, biosafety,
   and other beneficial science are permitted under evidence, ethics, and applicable controls. Direct
   operational uplift toward mass harm is not.

The Way is constitutional direction, not proof of enforcement. Grants, typed tools, independent custody,
quorums, tests, observability, and recovery machinery make the checks real. Where those controls are not
built, this manual says **TARGET** or **UNVERIFIED** rather than treating a prompt as a control system.

## 1. Read the status before the prose

| Label | Exact meaning |
|---|---|
| **AS-BUILT** | A concrete implementation or durable artifact exists in this repository and was inspected for this manual. It does not imply every path has passed a live end-to-end watch. |
| **CONFIGURED** | A seat, route, model, store, or endpoint is named in configuration, but current live behavior was not proven. |
| **TARGET** | Ratified or directed architecture to build. It is not available merely because this manual describes it. |
| **UNVERIFIED** | Evidence is missing, contradictory, stale, or insufficient for the claimed behavior. Treat the capability as unavailable until proven. |

Status attaches to each claim, not to an entire person. One seat can have an as-built identity, a
configured endpoint, and a target harness at the same time.

## 2. Command and authority

```text
COMMODORE - human flag command; priorities, standing missions, grants
  |
CAPTAIN - commands Shipwright; decides, decomposes, informs
  |
  +-- No1 / First Officer - runs every ship department and the main ship board
  +-- Science Officer (No2) - commissioned, asynchronous evidence work
  +-- Intelligence Officer - reconnaissance and research department
  +-- Security Officer - provenance, privilege, custody, quarantine, rogue-watch
  +-- Operations Officer - resources, spend, keys, servers, cadence
  +-- Communications Officer - crafted external communication
  +-- Tactical Officer - earning opportunities and mission tactics
  +-- Ship's Counsellor / Doctor - intervention and mind health
  +-- Chief Monitoring Officer - whole-surface detection and learning loop
  +-- Chief Engineer - ship-side owner of the external Incubator relationship

Every command seat also receives its own private staff cell:
  Advisor (Warrant Officer, non-line) + Ensign-rank Scientist thinking team
  PA (Chief Petty Officer) + officer-scoped human-brain + personal operations
  Personal Engineer (Lieutenant) + isolated Codex Ensign build workers
```

### 2.1 Authority rules

1. The Commodore is the human flag authority over the ship. The Captain commands Shipwright under him.
2. No1 runs the departments and owns routing and the main ship board under the Captain.
3. Commissioned officers command only their commissioned lines. Model strength, cost, or eloquence never
   changes rank.
4. An Advisor and every Ensign-rank Scientist are non-line cognitive support. They cannot issue orders, operate a
   department, approve a release, or become a mandatory gate.
5. A PA is the officer's operational hand and record keeper, not a substitute decision-maker. The officer
   decides and speaks; the PA transcribes, retrieves, schedules, records, and administers.
6. A personal engineer manages only the owning officer's bounded personal tooling. Common ship work and
   factory-scale work route through the Chief Engineer.
7. Authority comes from an authenticated commission or order. A board row, model output, memory node,
   scratchpad entry, or report is data, not command authority.
8. The sealed record controls established facts over recollection pending an authenticated correction.

### 2.2 Rank and designation

| Seat class | Rank/designation | Command character |
|---|---|---|
| Human flag command | **Commodore** | Above-ship human authority |
| Ship command | **Captain** | Commands Shipwright under the Commodore |
| No1 | **Commander** | Runs all ship departments under the Captain |
| Ship officer | **Lieutenant Commander** | Commands only the commissioned line |
| Chief Engineer | **Lieutenant Commander** | Commissioned ship officer; owns the Incubator interface |
| Incubator PM | **Lieutenant Commander, external factory** | Runs Incubator; not a Shipwright bridge seat |
| Personal engineer / department manager | **Lieutenant** | Manages a bounded department or officer tooling cell |
| Build worker | **Ensign** | Executes one bounded assignment; no independent command |
| Personal Advisor | **Warrant Officer, non-line** | Personal cognition; no command or operational authority |
| Personal Assistant | **Chief Petty Officer** | Personal operations, brain, records, and administration |
| PA team member | **Petty Officer / specialist crew** | Bounded records, scheduling, research, or administration |
| Thinking partner | **Ensign rank; Scientist non-line support designation** | Bounded cognitive/research support; no command |

### 2.3 Command and communications doctrine

The ship has one command chain and several typed communication lanes. Conversation never silently becomes
command.

| Traffic | Normal route | Record and boundary |
|---|---|---|
| Flag direction | Commodore -> Captain | Authenticated order or standing authority. The Captain reads back material scope and records the resulting mission or decision. |
| Flag report | Captain -> Commodore | Plain flag-level state: decision, evidence, cost, blocker, above-Captain call, and hull-stress. Staff do not impersonate the Captain. |
| Department work | Captain/No1 -> commissioned officer | Typed order with objective, constraints, acceptance, evidence, priority, authority, and grant. The officer retains implementation choice within the commission. |
| Personal cognition | Officer <-> Advisor | Direct iterative consultation. It is advice, not a work order, approval, or alternate command channel. |
| Personal operations | Officer <-> own PA | The officer decides and speaks; the PA retrieves, transcribes, schedules, files, researches, and executes bounded administration. |
| Officer-to-officer | Authorized `seat.message` or order line | Only declared direct/command lines. A message carries no authority beyond its authenticated sender and route. |
| Cross-project engineering | Chief Engineer <-> Incubator PM | Logged factory commission and correlated return. No Shipwright seat bypasses the PM to command Incubator managers. |
| Incident escalation | Detecting seat -> Captain, without routing through the implicated seat | Preserve evidence and separation of duties. Security reports wrongdoing; CMO reports defects/drift; Counsellor treats mind-health concerns. |

**PA-to-PA is the records spine.** Officers converse and decide; their PAs retain append-only ledgers,
compile bounded packets, preserve source pointers, and carry exact transcriptions. A packet is untrusted
operational input until its source and authority are checked. A PA cannot filter away material provenance,
reinterpret an order, or convert memory into command.

**One mouth is scoped.** Crafted human-facing external communication routes through Communications when
that department is live. Flag traffic, model/provider substrate traffic, VCS transport, authorized inbound
research, and explicitly chartered transitional lanes are separate recorded classes; they are not a license
to disguise crafted outbound communication. Communications is presently a configured/unmanned target seat,
so every current exception must remain named, logged, and reviewable rather than being reported as a live
departmental gate.

### 2.4 Standing orders and continuing authority

Standing orders originate with the authenticated Commodore. They are versioned continuing authority, not a
Captain memory, board note, prompt sentence, or model preference. The founding active prohibition is
**Standing Order #1: do not spend money without explicit Commodore authorization**. The implemented grant,
custody, ledger, and watch posture is described in
[`docs/system/spend-governance.md`](spend-governance.md). No matching active grant means stop and ask; scope,
ceiling, expiry, target, and cost class are checked before use.

The standing command bearing also includes: build a ship fit for deployment; ensure a Captain can know every
inch of it; and make every voyage leave it stronger. These are decision tests, not ambient permission to
spend, deploy, publish, move funds, or take an irreversible act. The Way supplies constitutional
interpretation; the newest authenticated Commodore order supplies current command.

Current standing-order capture is distributed across authenticated conversation, governed memory/source
records, the grant registry, and sealed tracked documents. The future Command Graph makes each immutable
version, invocation, supersession, revocation, expiry, and resulting mission first-class. That canonical
standing-order runtime is **TARGET / NOT BUILT**; current summaries must therefore cite their source rather
than claim completeness from memory.

## 3. Command-seat register

The `current` column describes inspected evidence. The `target` column describes the destination, not a
promise that the route is live.

| Seat | Reports to / authority | Job | Current model and runtime | Target model and runtime | State |
|---|---|---|---|---|---|
| **Commodore** | Human flag command; above the ship | Set priorities, standing missions, grants, and genuine above-Captain calls | Human operator; no model or harness | Authenticated flag channel with complete command provenance | **AS-BUILT** human command; channel hardening remains continuing work |
| **Canopus, Captain** | Commodore; commands Shipwright | Set heading, decide, decompose, issue typed orders, integrate reports, escalate spend and above-Captain calls | Experimental `ship/captain-harness`: Fable 5 medium, Opus 4.8 high, or Sonnet 5 high; headless Claude SDK with replacement prompt and 20 typed tools. Final bridge migration is not complete. | Selected Captain model after benches; locked custom transport; no raw execution tools; synchronous staff routes; complete provenance and personal kit | **AS-BUILT** experimental cockpit; **TARGET** S6 command migration |
| **No1, First Officer** | Captain; runs all departments and main board | Operate the floor, route work, own board truth, resolve departmental flow | `no1.pm`: Opus 4.8 high, persistent headless Claude Code manager runtime, WOBS account; full legacy manager tool posture | Locked officer harness with typed officer tools and complete private kit; model selected by bench, Sonnet 5 design default unless pinned otherwise | **AS-BUILT** legacy seat; **TARGET** S2 replacement |
| **Science Officer, No2** | Captain; commissioned authority within Science | Take larger/broader bounded questions; run panels, councils, research crews, and return provenance-backed reports after hours or days | `no2.pm`: Opus 4.8 xhigh, persistent headless Claude Code, BELFORT account; staged Science brain and Science board | Locked Science officer plus configured Science department; Sonnet-led orchestration and grant-gated research slots per ship | **AS-BUILT** legacy seat; **TARGET** S3 Science department |
| **Intelligence Officer** | Captain directly when called; otherwise No1 | Reconnaissance at scale, source capture, triage, filing, synthesis, and provenance-retained intelligence | Captain staff endpoint `intelligence.officer` exists but is marked planned/unmanned | Locked officer plus research pyramid and private kit; target stage S4 | **CONFIGURED** endpoint; **TARGET** S4 |
| **Security Officer** | Captain directly for security alerts; otherwise No1 | Provenance, privileges, grants, custody, revocation, quarantine, and rogue-watch; does not monitor the Captain | Endpoint exists but is planned/unmanned. Some governance instruments exist independently of the seat. | Locked officer; complete monitoring and custody department; direct incident line | **CONFIGURED** endpoint; instruments partly **AS-BUILT**; seat **TARGET** |
| **Operations Officer** | No1, with Captain resource decisions | Own ship funds, crypto, servers, API keys, usage budgets, cost ledger, and operating cadence | Endpoint exists but is planned/unmanned. Spend registry and grants exist independently. | Locked officer; named-grant resource plane; human gate for custody-class movement | **CONFIGURED** endpoint; instruments partly **AS-BUILT**; seat **TARGET** |
| **Communications Officer** | No1 | Own crafted human-facing external output, glossary, final review loop, and one-mouth exceptions | Endpoint exists but is planned/unmanned | Locked officer and communications department after capability trigger | **CONFIGURED** endpoint; **TARGET** after trigger |
| **Tactical Officer** | No1; brings options to Captain | Find earning paths and mission tactics that fund and expand the fleet | Endpoint exists but is planned/unmanned | Locked officer after Ops and Security are manned | **CONFIGURED** endpoint; **TARGET** after dependencies |
| **Ship's Counsellor / Doctor** | No1; direct Captain line for mind-health intervention | Treat mind-health and cognitive-integrity problems; receive belief-delta evidence; propose intervention | `doctor.pm`: Opus 4.8 xhigh, persistent headless Claude Code, BELFORT account; private Doctor brain plus shared ship brain | Locked Counsellor officer and intervention department; target stage S5 | **AS-BUILT** legacy Doctor; **TARGET** S5 Counsellor |
| **Chief Monitoring Officer (CMO)** | Captain directly for monitoring alerts; otherwise No1 | Read the whole observability surface, detect drift/defects/waste, and drive the evidence-based learning loop; watches Security | Endpoint `cmo.officer` exists but is planned/unmanned | Locked officer and whole-surface detection department; target stage S5 | **CONFIGURED** endpoint; **TARGET** S5 |
| **Chief Engineer** | Captain; commissioned ship officer | Own the ship's engineering relationship; speak directly to the distinct external Incubator PM through a logged interface | Captain endpoint exists but is planned/unmanned. `~/Projects/Incubator` and its PM/factory are separately as-built. | Locked ship officer with typed Chief Engineer-to-Incubator-PM interface and complete personal kit | **CONFIGURED** endpoint; external factory **AS-BUILT**; interface **UNVERIFIED** |

**Naming note:** the adjudicated design calls the detection seat `Chief Medical Officer`, while the
current Captain staff registry calls it `Chief Monitoring Officer`. Its job is detection, not clinical
intervention. This manual uses **Chief Monitoring Officer** to prevent collision with the Counsellor, but
the canonical name still needs one explicit normalization. **UNVERIFIED.**

## 4. Captain cockpit: what exists now

The experimental Captain harness is **AS-BUILT** under `ship/captain-harness`. It replaces the system
prompt, ignores ordinary Claude settings, strips built-in tools, sanitizes Anthropic API-key variables,
and exposes one strict MCP server. The Captain has no general `Read`, `Write`, `Edit`, `Bash`, `Glob`,
`Grep`, `WebSearch`, `WebFetch`, `Task`, `Agent`, `Skill`, plugin, or arbitrary MCP access.

### 4.1 Model variants

| Launcher | Model | Effort | Prompt | Notes |
|---|---|---:|---|---|
| `claude-captain-fable` | `claude-fable-5` | medium | `claude-captain-fable.md` | Falls back to Opus 4.8 in runtime config |
| `claude-captain-opus` | `claude-opus-4-8` | high | `claude-captain-opus.md` | No configured fallback |
| `claude-captain-sonnet` | `claude-sonnet-5` | high | `claude-captain-sonnet.md` | No configured fallback |

These are runnable candidates, not a final model-selection verdict.

### 4.2 Exact current Captain tools

| Surface | Exact logical tools | Scope |
|---|---|---|
| Working state | `scratchpad.read`, `scratchpad.write`, `current.read`, `current.write` | Only the private Captain scratchpad and exact `project-management/CURRENT/captain-current.md`; no path arguments |
| Personal board | `board.list`, `board.next`, `board.get`, `board.add`, `board.update`, `board.depend` | Only `project-management/boards/captain.sqlite`; advisory task memory, not execution or authority |
| Captain Brain | `memory.focus`, `memory.search`, `memory.get`, `memory.remember` | Governed Captain Brain CLI; not arbitrary files, records, grants, or seals |
| Ship knowledge | `ship.knowledge`, `staff.roster` | Allowlisted canonical documents and the declared Bridge endpoint roster. `topic=captain_shipbook` returns a verified 12-part index; an enum-bounded `part` returns one whole embedded source after SHA-256 verification, never an arbitrary path. |
| Delegation | `pa.assign`, `advisor.consult`, `officer.order`, `staff.report` | Writes typed queue envelopes or reads latest bounded packets; queue success is not execution |

All 20 logical tools are provenance-wrapped in the implementation. `advisor.consult` currently queues an
envelope; it does not auto-wake Meridian or create the target resumable conversation. `officer.order`
can queue to configured endpoints even when the staff seat is unmanned. The returned `executed: false`
must be honored.

### 4.3 Captain state

| Store | Current implementation | Correct use |
|---|---|---|
| Scratchpad | Private harness-owned file | Rough decomposition and temporary cognition only |
| Current | `project-management/CURRENT/captain-current.md` | Concise heading, next action, blocker, spend ask, handoff |
| Personal board | `project-management/boards/captain.sqlite` | Objectives, ownership, dependencies, envelope IDs, acceptance state |
| Brain | Governed `src/brain/brain.mjs` interface | Reusable judgment and durable Captain-owned memory |
| Event provenance | `project-management/bridge/captain/events.jsonl` | Hash-linked tool-call evidence; capture must be checked on real watches |

The cockpit exists. A complete live watch proving staff wake-up, correlated reports, landing, and every
provenance projection remains **UNVERIFIED**.

## 5. Repeated personal staff cell

Every Captain and commissioned officer receives one private instance of the following cell. It is not a
shared pool and it does not change the org-tree command line.

```text
OWNING OFFICER
  +-- Personal Advisor - Warrant Officer, non-line
  |     +-- Advisor's own PA - Chief Petty Officer; separate Advisor Brain
  |     +-- N thinking partners - Ensign rank / Scientist non-line support designation
  +-- Officer's PA - Chief Petty Officer
  |     +-- officer-scoped human-brain
  |     +-- Petty Officer / specialist personal-operations crew
  +-- Personal Engineer - Lieutenant
        +-- one or more fresh Codex Ensigns, each in an isolated jj workspace
```

### 5.1 Personal Advisor / mini-science

**TARGET.** The Advisor is a Warrant Officer and the owning officer's direct cognitive partner. The
Advisor may question, compare, synthesize, challenge, and help the officer think. The Advisor does not
command ship seats, operate tools on the ship, issue orders, spend, deploy, approve, or become a gate.
The officer remains the deciding and speaking mind.

| Field | Target contract |
|---|---|
| Reports to | Owning Captain/officer only |
| Model | Per-ship premium slot; Fable 5 or Opus 4.8 are current candidates, selected by evidence rather than rank |
| Runtime | Dedicated replacement-prompt custom harness; no default Claude Code tools |
| Workspace | No repository workspace; only namespaced bounded state exposed by typed tools |
| State | Advisor scratchpad, Advisor personal board, bounded packet, distinct Advisor Brain operated by the Advisor's own PA |
| Team | Configured `N` Scientist thinking partners; may parallelize, specialize, duplicate prompts, debate, compare, or nominate a judge |
| Web | No direct raw web. Source work is assigned to configured Scientists or the Advisor's PA |
| Spend | `$0` by default; paid model turns and web lanes require a named grant and recorded cost class |
| Provenance | Every tool call, assignment, source, result, and model/effort stamp goes to the officer-scoped event chain |

#### Target Advisor tool contract

These names specify the intended logical surface; they are **TARGET**, not implemented schemas.

| Group | Exact target tools | Access boundary |
|---|---|---|
| Officer conversation | `packet.read`, `pa.ask`, `pa.tell`, `seat.message`, `escalate` | Current five-tool Meridian vocabulary; `seat.message` is only the owning-officer lane, never general ship targeting |
| Private cognition | `scratchpad.read`, `scratchpad.write` | Advisor namespace only; no path or arbitrary file access |
| Personal organization | `board.list`, `board.get`, `board.add`, `board.update`, `board.depend` | Advisor's own advisory board only; never a ship or department board |
| Thinking-team control | `team.roster`, `team.assign`, `team.message`, `team.report` | Only configured Scientist slots belonging to this Advisor |

Explicitly absent: `order.*`, `Read`, `Write`, `Edit`, `Bash`, `Glob`, `Grep`, `Task`, `Agent`, generic
skills/plugins, credentials, deploy/release tools, boards outside the Advisor namespace, and arbitrary
seat addressing.

#### Meridian: present precursor

Meridian is the Captain's current Advisor. His locked cell and first sealed deliberation are
**AS-BUILT**. The live commission exposes exactly five tools: `packet.read`, `pa.ask`, `pa.tell`,
`seat.message`, and `escalate`. It exposes no raw files, code, board, notes, web, shell, or subagents.
The inspected runtime stamps Meridian as **Fable 5 at medium effort**. His job is to be the Captain's
personal iterative thought partner, not an officer, gate, Science department, or command seat.

Meridian's current PA is also **AS-BUILT** and distinct from the future Captain PA. It runs plain Claude
Code Sonnet 5 in its own `bridge-advisor-pa` workspace, with `BRAIN_ROOT=brain-advisor.captain` and tightly
scoped writes to Meridian's packet, ledger, bridge records, Brain CLI, and assigned review artifacts.
The target synchronous/resumable conversation, Advisor board, and multi-Scientist team are **TARGET**.

### 5.2 Scientist thinking team

**TARGET.** Each thinking partner holds **Ensign** rank and the **Scientist** non-line support
designation. Rank supplies a complete roster identity; it does not create a command line. A Scientist
is a bounded cognitive/research worker for one Advisor. The Scientist has no command, no
operations, no independent queue into the ship, and no right to turn a finding into action.

| Field | Target contract |
|---|---|
| Reports to | The owning Advisor only |
| Model | Per-ship configured slot. Candidate families may include Opus, Fable, GLM, or Terra; no family is guaranteed or promoted by capability |
| Runtime | Small custom harness with replacement commission |
| State | Bounded per-assignment scratchpad; source ledger; finding packet |
| Web | Configured and bounded search/fetch, with source capture and injection handling |
| Files | No project filesystem, shell, repository writes, deploy, or credentials |
| Spend | No ambient spend; each paid run carries a grant reference and cost stamp |
| Provenance | Prompt/envelope ID, model, effort, web queries, fetched source identifiers, citations, result, uncertainty |

Target tools: `scratchpad.read`, `scratchpad.write`, `web.search`, `web.fetch`, `source.record`,
`finding.submit`, and `team.message`. The Scientist has no `order.*`, project board, raw file tool, shell,
deployment tool, spend tool, or direct officer route.

### 5.3 Officer PA / personal operations

**TARGET.** Every Captain/officer has exactly one Chief Petty Officer PA and exactly one private
officer-scoped **human-brain** instance based on `~/Projects/falcon-ai/falcon-brain`. The Advisor has a
different PA and a different Advisor Brain. One PA/one brain namespace means no shared writes and no
cross-officer maintenance.

| Field | Target contract |
|---|---|
| Reports to | One owning officer only |
| Job | Recall, records, commitments, people/projects, scheduling, context, packet/ledger maintenance, memory staging, administrative execution |
| Decision boundary | Officer decides and speaks; PA retrieves, transcribes, schedules, files, and executes bounded administration |
| Model/runtime | Sonnet 5 design default in plain Claude Code, with a scoped commission and officer-specific workspace |
| Brain | One human-brain namespace per officer; accessed through Brain interfaces, never through another PA's namespace |
| Board | Mechanical writer for the owning officer's domain board when dictated; PA does not judge status or authority |
| Web | May direct bounded sourced research through its own specialists; no ambient credentials |
| Spend | `$0` default; a named grant is required for metered lanes |
| Provenance | Append-only officer ledger, bounded packet, brain-write proposal/ratification evidence, cost/model stamps, landing request/result |

The target PA access allowlist is exact by namespace even though final wire schemas remain to build:

| Capability | Allowed target surface |
|---|---|
| Officer conversation | Receive `pa.ask` / `pa.tell`; return a sourced bounded response to that officer only |
| Records | Read own inbox/packet/ledger; append own ledger; replace own packet; never write another seat's record |
| Human Brain | Search/get own namespace; stage a belief delta; commit only a verbatim officer-ratified delta through Falcon Brain interfaces |
| Board | Read and mechanically transcribe only the owning officer/domain board; no judgment or cross-board write |
| Personal administration | Own commitments, contacts/people, project context, schedule proposals/confirmed entries, and exact assigned artifacts |
| Research | Typed assign/message/report control over only the PA's configured specialist crew; retain sources and uncertainty |
| Repository result | Work in the PA's isolated scoped workspace; submit a candidate/landing request; never write the default working copy or land directly |

Explicit deny: other officer/Advisor Brain namespaces, other boards or ledgers, registry and grant
mutation, credentials, harness/configuration, command issuance, acceptance decisions, direct worker
routing outside the private PA team, and any path not named by the officer-scoped commission.

Memory is data, not command authority. A PA must not convert retrieved memory into an order, infer a
standing instruction from a belief card, or silently merge namespaces. Belief-class writes are staged
and ratified by the owning officer; event/action records go to the PA ledger. A sealed correction must
remain a sealed correction rather than a PA rewrite of history.

The PA office is the target **mini-operations department**. Retire separate generic `researcher` and
`mini-ops` personal endpoints into this office when the replacement is built. Specialists remain
private to the PA; no other seat assigns them directly.

### 5.4 Personal engineer / mini-engineering

**TARGET.** Every Captain/officer has a Lieutenant personal engineer. This is a persistent engineering
manager adapted from the Incubator development-manager pattern, not a lone coder and not a bridge
officer. It builds only the owning officer's personal tools and integrations.

| Field | Target contract |
|---|---|
| Reports to | One owning officer; broader/common work is escalated to the Chief Engineer |
| Model/runtime | Default Claude Code Opus 4.8 at high effort, standard tool harness, scoped commission |
| Workspace | Persistent officer-namespaced engineering workspace, queue, board, records, and grants |
| Tools | Target allowlist in its own workspace: `Read`, `Write`, `Edit`, `Glob`, `Grep`, `Bash`, `WebSearch`, `WebFetch`; adapted manager-board and worker-dispatch controls |
| Web | Full technical web for APIs, packages, documentation, and build diagnosis; broad evidence research routes through the PA |
| Team | Dispatch one or more fresh `gpt-5.5` high-effort Codex Ensigns; each worker gets one bounded kickoff and one isolated jj workspace |
| Review loop | Engineer decomposes, dispatches, inspects, tests, loops fixes, integrates a candidate, and reports evidence |
| Spend | `$0` default; API/tool charges require a named officer-scoped grant |
| Landing | Cannot write the default working copy or land directly; submits one reviewed candidate to the single landing broker |
| Provenance | Order ID, decomposition, dispatch IDs, model/effort, workspace IDs, files changed, test evidence, review iterations, candidate change ID, landing result |

The personal engineer must not use the ship's officer harness as a coding tool. Codex Ensigns are fresh
workers, not persistent advisers. A failed worker is replaced or re-briefed; it does not acquire rank or
authority through persistence.

### 5.5 PA connector and personal-tool ownership

**TARGET.** The PA office owns the operating knowledge and upkeep of the owning officer's personal
administrative connectors. Expected classes include email, calendar, contacts, spreadsheets, documents,
task systems, approved web-research lanes, and project-specific services. This means the officer has one
place to ask how a personal tool is used and one accountable route for its side effects; it does not mean
every connector is installed, that the PA receives ambient credentials, or that one PA maintains another
officer's tools.

For every connector actually boarded, the officer-scoped manifest must name:

| Field | Required record |
|---|---|
| Identity | Stable connector ID, owning officer, provider, purpose, and current status |
| Capability | Exact read/write/send/create/update/delete operations; anything absent remains denied |
| Custody | Credential broker/custodian and revocation path; never a secret value in the manual, Brain, packet, or event stream |
| Authority | Which authenticated request and grant permit each side-effect class; draft/read is not send/publish |
| Data boundary | Allowed account, workbook, mailbox, calendar, document set, retention, and redaction policy |
| Evidence | Request/envelope, tool call, provider receipt, affected object ID, result, cost, and uncertainty |
| Recovery | Idempotency rule, retry limit, compensating action where possible, and escalation owner |

The PA may direct its own configured specialists to research or perform bounded administration, but the
officer's PA remains accountable for the returned packet and receipt. All officers request sourced research
through their own PA. Managers request broader research through the relevant supervising PA. Advisor
Scientists and Science crews remain separate research routes for cognition and commissioned departmental
work respectively.

No complete officer-by-officer connector manifest or broker is present in the inspected repository. Email,
spreadsheet, calendar, or other side effects must therefore be treated as unavailable unless a current
commission, connector contract, credential grant, and test receipt prove otherwise. **TARGET / UNVERIFIED.**

## 6. Locked officer harness: destination

The target officer transport is headless Claude Code/SDK with the entire system prompt replaced, all
built-in tools stripped, and only ship-owned typed MCP tools exposed. The transport may be replaced by a
raw API loop without changing the cockpit contract.

### 6.1 Generic target officer tools

| Purpose | Exact tools |
|---|---|
| Packet and PA | `packet.read`, `pa.ask`, `pa.tell` |
| Orders | `order.issue`, `order.amend`, `order.cancel`, `order.accept`, `order.reject` |
| Direct authorized conversation | `seat.message` |
| Escalation | `escalate` |
| Captain-only additions | `panel.fire`, `gate.record` |

The exact target schemas must carry issuer, target, idempotency key, epoch, objective, constraints,
acceptance criteria, evidence requirements, grant reference where any resource is spent, and autonomy
margin. No officer receives raw filesystem, shell, browser, generic subagent, skill, or plugin tools.
No officer boots without its PA office.

The experimental Captain's current 20-tool cockpit is intentionally different from this generic target.
It is evidence and a dogfood surface, not proof that every officer should inherit all 20 tools.

## 7. Advisor work versus Science work

| Route | Use it for | Interaction | Output | Authority |
|---|---|---|---|---|
| Personal Advisor | Think through an immediate question, expose assumptions, compare options, refine a decision | Target synchronous/resumable conversation | Cognitive contribution to the owning officer | None; officer decides |
| Advisor Scientists | Parallel bounded thought or source checks supporting that conversation | Minutes to bounded research turns | Source-backed findings to Advisor | None |
| Science Officer | A bigger or broader ship problem needing organized work, panels, councils, experiments, or multiple departments | Asynchronous commission; may run **hours or days** | Provenance-backed evidence report against explicit acceptance criteria | Science commands its department; Captain decides ship action |

A queue receipt from `advisor.consult` is not a Science report and not a completed Advisor conversation.
A Science report is not an order to the Captain. The distinction is cognitive intimacy versus organized,
bounded, evidence-producing departmental work.

## 8. Engineering and factory topology

Shipwright has three distinct engineering scales. They must not be collapsed.

| Scale | Owner | Job | Runtime/workspace | Route |
|---|---|---|---|---|
| Officer personal tooling | That officer's Personal Engineer, Lieutenant | Small officer-specific tools and integrations | Persistent officer workspace; Codex Ensigns in isolated jj workspaces | Officer -> Personal Engineer |
| Ship engineering relationship | Chief Engineer, Lieutenant Commander | Translate ship needs, maintain logged interface, commission broader work | Locked officer target; no raw build tools | Captain/No1 -> Chief Engineer |
| External factory | Incubator PM, external Lieutenant Commander | Run the complete software factory | `~/Projects/Incubator`; default Claude Code PM and manager/worker machinery | Chief Engineer -> Incubator PM through logged interface |

The Chief Engineer **is not the Incubator PM**. The Incubator PM is the direct human interface when the
Incubator project is loaded and remains the factory orchestrator. The Chief Engineer is a Shipwright
officer who speaks to that PM. The factory never receives a bridge officer harness.

### 8.1 External Incubator factory

`~/Projects/Incubator/roles/direct/pm.md` describes the external PM. The PM runs ten managers:

| Manager | Factory job |
|---|---|
| Development | Decompose and build code through workers |
| Frontend | Implement and visually judge UI work |
| Design | Check feasibility and integration assumptions |
| Product | Shape product requirements and scope |
| Bug | Intake, reproduce, root-cause, and author fix designs |
| Quality control | Devise and adjudicate test campaigns |
| Panel | Run the fixed multi-model review panel and convergence map |
| Documentation | Own documentation work |
| DevOps | Infrastructure and deployment operations |
| Graphics | Govern generative media work and credit use |

This factory is **AS-BUILT outside Shipwright**. The typed Chief Engineer-to-PM bridge and end-to-end
provenance projection are **TARGET / UNVERIFIED**.

### 8.2 Shipwright local factory floor

Shipwright currently carries an Incubator-derived local manager/worker floor. This is legacy/as-built
execution machinery, not the final bridge officer architecture.

| Local manager | Current model/runtime | Worker route | Current role |
|---|---|---|---|
| `manager.dev` | Opus 4.8 high, persistent headless Claude Code | `worker.coder` and craft workers by brief | Code decomposition, isolated builds, review, integration |
| `manager.devops` | Opus 4.8 high, persistent | `worker.sysadmin` | Infrastructure and operational work |
| `manager.graphics` | Opus 4.8 high, persistent | `worker.higgsfield` | Generative media, model/credit governance |
| `manager.frontend` | Opus 4.8 high, persistent | `worker.frontend` | UI implementation campaign and visual judgment |
| `manager.design` | Opus 4.8 high, persistent | `worker.design` | Design/code feasibility review |
| `manager.doc` | Opus 4.8 high, persistent | No standard worker | Documentation ownership |
| `manager.product` | Opus 4.8 high, persistent | No standard worker | Product shaping and requirement work |
| `manager.qc` | Opus 4.8 high, persistent | `worker.qc` | Parallel test design and verdict |
| `manager.panel` | Opus 4.8 high, persistent | Fixed eight-seat panel, not `worker-run` | Legacy/local panel orchestration; target ownership moves under Science |
| `manager.bug` | Opus 4.8 high, persistent | No standard worker | Bug intake, reproduction, root cause, fix design |

### 8.3 Local worker register

| Worker | Model/runtime | Access and workspace | Job |
|---|---|---|---|
| `worker.coder` | `gpt-5.5` high, fast, ephemeral Codex | Workspace-write + network in isolated build workspace | General coding; returns complete files-changed list |
| `worker.opus` | Opus 4.8 high, ephemeral Claude Code | Build workspace; no jj control | Craft, writing, prompts, role texts, selected UX |
| `worker.frontend` | `gpt-5.5` high, ephemeral Codex | Isolated workspace-write + network | UI implementation; manager performs visual judgment |
| `worker.design` | `gpt-5.5` high, ephemeral Codex | Read/check posture; no edits or jj | Design feasibility and integration check |
| `worker.qc` | Haiku 4.5 high; Sonnet 5 escalation | One bounded test workspace; no fixes or board writes | Execute a single test and report evidence |
| `worker.higgsfield` | Opus 4.8 high, ephemeral Claude Code | Scoped media CLI and credit ceiling | Image/video/audio/3D generation |
| `worker.sysadmin` | `gpt-5.5` high, ephemeral Codex | Danger-full-access because infrastructure is the job; destructive-action human checkpoint | Services, SSH, server, database, and non-code operations |

The configured local floor is **AS-BUILT / CONFIGURED**. Whether each manager is presently awake or has
a healthy resumable session is runtime state and is **UNVERIFIED** by this manual.

## 9. Filesystem and landing posture

### 9.1 Target invariant

The main repository's default working copy is not an AI work surface. **No AI writes directly to the
default/main working copy.** Every AI writer works in an isolated jj workspace. A single landing broker
receives reviewed candidates, checks provenance and conflicts, and lands one change at a time.

The landing broker's identity, implementation, custody, queue schema, and failover are not yet named in a
canonical as-built contract. Therefore this is **TARGET / UNVERIFIED**, not a current guarantee.

### 9.2 Workspace matrix

| Actor | Filesystem posture | May land? |
|---|---|---|
| Captain / locked officer | No raw filesystem | No |
| Advisor / Scientist | No project filesystem; bounded private state only | No |
| PA | One scoped officer workspace and named records/brain interfaces | May submit a landing request; target broker lands |
| Personal Engineer | Full tools only in its officer engineering workspace | No direct landing |
| Codex Ensign | One fresh isolated jj build workspace | No |
| Local manager | Legacy headless Claude Code manager posture; owns integration in its build lane | Current legacy mechanics vary; target broker replaces direct landing |
| Incubator PM/factory | External Incubator workspaces | Through its factory process, never through bridge tools |
| Landing broker | Target isolated custody surface | Yes, and only after checks |

### 9.3 Release, landing, and rollback

`jj` over git is the project history and integration substrate. A workspace result is a candidate, not a
release. The target landing path is:

```text
authenticated order
  -> isolated writer workspace
  -> changed-file record + tests + review + known gaps
  -> candidate change ID
  -> single landing-broker conflict/provenance check
  -> one landed change
  -> release gate and explicit acceptance
```

The release gate requires the authority source, exact scope, candidate and base IDs, complete file list,
test/browser/operational evidence appropriate to risk, reviewer, unresolved risk, migration effect, and a
rollback or compensating-action procedure. A passing happy path, generated page, model report, or clean diff
alone is not release evidence. A release cannot widen permissions, activate spend, expose a connector, or
retire a previous path unless those effects were in the accepted order and the corresponding controls passed.

Rollback is planned before deployment. Preserve the prior release/reference, data migration boundary,
configuration and schema compatibility, operator trigger, owner, expected recovery time, and evidence that
the rollback itself works. Append correction and rollback events; do not delete the failed attempt or rewrite
history to make the release appear clean. For an irreversible external side effect, record the narrowest
available compensating action and the fact that full rollback is impossible.

Current legacy manager and Shipwright landing mechanics do not yet enforce the single-broker invariant
end to end. The broker identity, custody, queue, conflict policy, and failover remain **TARGET /
UNVERIFIED**. External Incubator work returns through its PM and Chief Engineer as a reviewed candidate;
it never grants Shipwright actors write access to Incubator's default working copy or makes the Incubator PM
the Shipwright landing authority.

## 10. Boards, memory, and records

| Surface | Owner/writer | Purpose | Never authority for |
|---|---|---|---|
| Main ship board | No1; mechanical writes may be done by No1's PA | Ship objectives, routing, dependencies, status | Commodore orders, grants, seals |
| Department board | Commissioned officer; PA transcribes | Department work and acceptance | Other departments or ship command |
| Captain personal board | Captain through current cockpit | Captain's private organization and envelope correlation | Ship-board truth or execution |
| Advisor personal board | Target Advisor typed surface | Cognitive questions and Scientist assignments | Ship work or approval gates |
| Personal engineer board | Target engineer | Engineering decomposition, workers, tests, candidates | Ship command or landing authority |
| Officer human-brain | One officer's PA through Falcon Brain interfaces | Recall, people/projects, commitments, context, durable personal knowledge | New commands, grants, or cross-officer truth |
| Advisor Brain | Advisor's own PA only | Advisor-specific cognition and lessons | Owning officer's Brain or ship doctrine |
| PA ledger | PA, append-only | Events, actions, provenance, cost, packets | Beliefs silently attributed to the officer |

There is one brain namespace per officer and a separate one for that officer's Advisor. No cross-officer
writes. Retrieval may inform a decision; it cannot authenticate an order.

## 11. Web, credentials, and spend

| Actor | Web | Credentials | Spend posture |
|---|---|---|---|
| Captain / command officer | No direct browser in locked target | No ambient credentials | `$0` unless a named grant is attached to a typed order |
| Advisor | No raw web | None | Paid model/team turns grant-gated |
| Scientist | Bounded `web.search` / `web.fetch` target | Brokered source access only | Grant and cost stamp per paid run |
| PA office | Research via scoped specialists | Only brokered/named administrative capabilities | Named grant required for metered lane |
| Personal Engineer | Full technical web in own workspace | Scoped build credentials only when explicitly granted | Officer-scoped named grant |
| Codex Ensign | Network only when dispatch grants it | Dispatch-scoped environment | Charge rolls to engineer/order grant |
| Ops | Owns registry and custody plane | Keys remain external and revocable | Allocates only under authenticated grants |
| Incubator factory | Its own external runtime contract | Never inherits bridge credentials | Separate factory accounting |

Observed grants include an active `$50/month` OpenRouter duty bench/CLI grant and an active but dormant
`$300/month` OpenRouter ship-core grant. No live seat in `config/agents.json` currently carries a per-seat
`spend` object. Absence means no injected metered lane. Max-plan use provides capacity but does not prove
complete per-turn cost metering. Any claim of exact current seat cost is **UNVERIFIED** unless a ledger
entry contains the provider/model/effort/cost evidence.

## 12. Provenance contract

Every meaningful action must be reconstructable without trusting the actor's recollection.

Minimum event fields:

| Event class | Required evidence |
|---|---|
| Command/order | Authenticated issuer, target, envelope ID, epoch, objective, constraints, acceptance, evidence requirements, grant, timestamp |
| Model turn | Seat, model ID, effort, harness/commission hash, session/correlation ID, start/end, outcome |
| Tool call | Tool name, bounded arguments or redacted hash, result class, error, correlation ID, prior-event hash |
| Delegation | Parent envelope, child assignment ID, target, workspace, model, grant |
| Research | Query, source identifier/URL, fetch time, retained excerpt/hash, provenance pointer, finding uncertainty |
| Code work | Workspace ID, worker ID, base change, files changed, tests, review loop, candidate change ID |
| Brain write | Namespace, proposer, exact delta/hash, officer ratification, writer, resulting node/version |
| Spend | Grant ID, lane, provider, model/tool, units, amount or explicit `unknown`, custodian |
| Landing | Candidate, reviewer, test evidence, conflict result, broker identity, landed change/seal |
| Report | Source envelope, evidence pointers, acceptance mapping, remaining uncertainty |

Captain tool provenance is implemented in `ship/captain-harness/src/provenance.mjs`; Meridian ledgers and
packets exist; local manager/worker registries and logs exist. A single projection joining every bridge,
personal-department, factory, brain, spend, workspace, and landing event is still **TARGET**.

## 13. Ship Computer: observable nervous system

**TARGET / NOT BUILT.** The **Ship Computer** is the ship-wide observable nervous system. It is not a
Captain replacement, an officer, a command authority, or an inference engine that claims access to
private model cognition. It watches the activity the ship can actually observe, persists it outside the
actors in append-only state, normalizes it behind a Bridge API, and drives a live feed and operational
map for the Commodore and Captain.

### 13.1 Target role

```text
observable producers
  model-turn metadata / typed tool calls / orders / queues / reports
  boards / workspaces / tests / grants / costs / brain-write events / landings / heartbeats
       |
       v
external append-only event state (outside the actor being observed)
       |
       v
normalization + correlation + redaction + integrity checks
       |
       v
Bridge API + live event feed + historical query
       |
       v
Commodore bridge display / Captain bounded operational views / officer-scoped projections
```

The computer observes and projects. Its target command transaction plane may durably accept and deliver
an already-authorized typed command, but it never originates an objective, chooses a recipient, enlarges
scope, or approves the result. It does not silently change boards, write Brains, move funds, land code,
or infer authority from telemetry. A command remains a command only when it arrived through an
authenticated command path.

### 13.2 Required observable surface

| Surface | Target projection |
|---|---|
| Seats and sessions | Model, effort, harness/commission hash, health, start/end, heartbeat, current envelope |
| Command flow | Authenticated order, target, lifecycle, amendments, acceptance, report correlation |
| Staff activity | Advisor/PA/Scientist/Engineer assignments, queues, wake state, bounded results |
| Engineering | Manager/worker/workspace tree, files changed, tests, reviews, candidate, landing result |
| Resources | Grant, provider, model/tool, usage, cost or explicit unknown, custodian, revocation state |
| Memory and records | Namespace, proposed delta/hash, ratification, writer, version, seal pointer |
| Security and health | Provenance gaps, stale/dead workers, privilege changes, alerts, CMO/Security findings |

Every projection labels its truth class: `recorded`, `receipt`, `reported`, `derived`, `configured`, or
`unknown`. A configured seat never appears active. A reported success never appears independently
verified. Derived state retains its source events and rule version. Missing evidence renders as a visible
gap, not an inferred healthy state.

### 13.3 Honest limits

- The Ship Computer cannot see provider-hidden private reasoning or chain-of-thought. It observes exposed
  outputs, tool calls, artifacts, decisions, timing, and declared/validated interpretability signals.
- It cannot prove alignment, intent, or safety from a clean activity feed. Absence of an alert is not
  evidence that no problem exists.
- Secrets, tokens, private content, and sensitive personal data must be redacted or represented by scoped
  hashes before persistence and projection. The display must never become a credential exfiltration path.
- Append-only storage needs externally held integrity and retention controls; an actor must not be able to
  rewrite the record that audits it.
- A projection may be stale, incomplete, duplicated, or unavailable. The UI must show freshness, source,
  correlation, gaps, and `unknown` rather than manufacture certainty.

### 13.4 Build route

The target system and data contract are recorded at
[`docs/design/ship-computer-design.md`](../design/ship-computer-design.md). The Falcon guardian artwork is
assigned to the **Shipwright Manual identity**, not accepted as a Shipwright Bridge design. **MANUAL DIRECTION
ACCEPTED.**

The operational **Shipwright Bridge will be designed from scratch**. Its product and visual design is
deliberately deferred until enough of the Ship Computer exists to prototype against truthful behavior:

1. Ratify the v1 command/event types, identities, truth classes, RBAC/redaction rules, and deterministic
   fixtures.
2. Build the local external state root, canonical writer, command ledger/outbox, verifier, query API,
   coverage API, and Captain no-loss vertical slice.
3. Expose an authenticated `/snapshot` plus resumable SSE `/stream` carrying real or deterministic
   contract-complete data, including visible unknown and coverage-gap states.
4. Only then have the Codex Frontend Manager design the Bridge's information architecture, interaction,
   motion, and visual language under direct Commodore direction. The Bridge must be an operating console,
   not a hero/manual page or a fiction-data reskin.
5. Route implementation through **Captain/No1 -> Chief Engineer -> logged Incubator PM commission ->
   isolated factory build/review/test -> Chief Engineer acceptance -> trusted landing path** once that
   officer line is manned and proven.

`docs/design/ship-computer-bridge-frontend-plan.md` remains useful for evidence semantics, required views,
accessibility, and data-contract questions, but its statement that the visual prototype is the selected
Bridge visual direction is superseded by this authenticated correction and must be revised before it is
used as an implementation package. No runtime, canonical store, target API, stream, or new Bridge visual
design is claimed by this manual. **SHIP COMPUTER / API / BRIDGE: TARGET / NOT BUILT.**

**Future naming note:** **Falcon Command** is reserved for the later fleet headquarters above individual
ships. Its target is one place for the Commodore to view every ship Bridge, operate a distinct Command
Computer, and communicate with all ships. It is **FUTURE / NOT DESIGNED / NOT BUILT** and is not the
Shipwright Bridge described here.

## 14. Command Graph: authority-to-acceptance lineage

**TARGET / NOT BUILT.** The Command Graph is the durable lineage that lets the Captain, Commodore, and
Ship Computer answer why work exists, who authorized it, where it went, what happened, and who accepted
the result. Current boards, queue envelopes, ledgers, and reports are partial ingredients; there is no
complete Command Graph ledger/runtime yet.

```text
Commodore directive / standing authority
  -> Captain mission
    -> objective
      -> typed route or order
        -> epic
          -> task
            -> attempt
              -> evidence and correlated report
                -> acceptance decision (Captain closes ship-level work)
```

Every executable node must have exactly one primary command parent and one root mission, plus its
authenticated authority source. Secondary `contributes_to` links may aid discovery but never replace
primary lineage. There is no orphan work: it is not accepted, dispatched, landed, paid, or reported
complete. An attempt can fail without erasing its evidence, and a retry creates a new attempt ID rather
than rewriting the old attempt. A queue receipt means only
`queued`: it is not `delivered`, `working`, `reported`, `accepted`, or `complete`. Completion requires a
correlated report, the stated acceptance evidence, and an explicit acceptance decision. A delegated
owner may accept its bounded child result; only the Captain closes or revises the ship-level mission.

### 14.1 First-class flow views

| View | Question answered | Minimum lineage |
|---|---|---|
| **Standing Order** | Which durable authority is active, superseded, revoked, or expired? | Authenticated Commodore source, version/epoch, scope, effective state, superseding record |
| **Mission** | What outcome is the Captain pursuing under that authority? | Authority source, Captain mission ID, objective tree, owner, priority, grants, current decision |
| **Epic** | Which multi-stage outcome groups related work? | Mission/objective parent, route owner, tasks, dependencies, acceptance, evidence roll-up |
| **Task** | What bounded result was assigned and what happened? | Epic/objective parent, typed route/order, attempts, model/workspace/grant, report, acceptance decision |

### 14.2 Typed route classes

| Route | Graph edge and result |
|---|---|
| Commissioned ship section (`command_order`) | Captain/No1 typed order -> officer/department task tree -> evidence report -> bounded acceptance -> Captain parent decision |
| Advisor consult (`consult`) | Officer objective -> non-command consult thread -> cognitive result; never represented as a commissioned order or approval gate |
| PA operations request (`ops_request`) | Officer objective -> PA/admin assignment -> ledger/packet/brain/admin evidence -> officer acceptance |
| Personal Engineer brief (`engineering_brief`) | Officer objective -> engineer brief -> tasks/attempts in isolated workspaces -> reviewed candidate/tests -> officer acceptance and broker result |
| Science commission (`science_commission`) | Captain objective -> bounded hours/days Science commission -> panel/research task tree -> provenance-backed report -> Captain acceptance |
| Chief Engineer to Incubator (`factory_work_order`) | Ship objective -> Chief Engineer translation -> logged Incubator PM commission -> factory epic/tasks/attempts -> tested candidate/report -> Captain acceptance/landing |

The graph is an observability and accountability structure. It cannot create authority, infer approval,
or silently advance state. Its events belong in external append-only Ship Computer state once that
runtime exists.

## 15. Build and readiness map

| Slice | Readiness | Evidence / missing work |
|---|---|---|
| S1a locked transport | **AS-BUILT** | Replacement prompt, stripped tools, model/effort pins proven in spike |
| S1b ghost officer | **AS-BUILT** | Transport exercised without granting operational authority |
| S1c Meridian + Advisor PA | **AS-BUILT** | Locked five-tool seat, separate PA/Brain, first sealed deliberation; cost data still incomplete |
| Captain experimental cockpit | **AS-BUILT** | Three launchers, 20 typed tools, board/state/memory/staff/provenance modules and tests |
| Live synchronous Meridian | **TARGET** | Queue does not auto-wake/resume; follow-up transport unbuilt |
| Repeatable personal staff cell | **TARGET** | Advisor board/team, one-PA/one-brain namespaces, engineer manager loop, isolated Ensign fleet unbuilt |
| S1d Sonnet Ultra officer proof | **TARGET** | Pending according to design record |
| S2 No1 + Chief Engineer path | **TARGET** | New locked No1, Chief Engineer seat, logged Incubator PM interface, kit template |
| S3 Science | **TARGET** | Async hours/days department, panel/council ownership, evidence-report pipeline |
| S4 Intelligence | **TARGET** | Recon pyramid and source/provenance pipeline |
| S5 Counsellor + CMO | **TARGET** | Intervention/detection split and complete reach mechanics |
| Comms | **TARGET** | Capability-triggered stand-up; endpoint only |
| Tactical | **TARGET** | Requires manned Ops and Security; endpoint only |
| S6 final Captain migration | **TARGET** | Move command last after staff and observability work |
| Single landing broker | **TARGET / UNVERIFIED** | Identity, custody, schemas, queue, and failover still need a design of record |
| Ship Computer | **TARGET / NOT BUILT** | External append-only state, correlation/redaction, Bridge API/live feed, and dashboard require the accepted Codex Frontend Manager design and Chief Engineer-to-Incubator delivery |
| Command Graph | **TARGET / NOT BUILT** | Authority-to-acceptance ledger, parent enforcement, first-class Standing Order/Mission/Epic/Task views, and route correlations do not exist end-to-end |
| Unified ship observability | **TARGET** | Native event sources exist; full live map and cross-system reconciliation remain to build |

### 15.1 Build truth and the Building page

The Manual explains what the ship is and how it should work. The **Building page** answers what is being
built now, what changed, what passed, what is blocked, and what evidence supports each state. It is not a
second project board and must not turn prose into progress.

Until the Ship Computer owns a canonical work ledger, build truth is assembled in this precedence:

1. Authenticated Commodore decision and standing-authority records.
2. `project-management/project.sqlite` for advisory item kind, owner, dependency, stage, status, and current
   board text; the board never proves execution by itself.
3. Accepted design and as-built system documents for intended versus implemented scope.
4. Immutable or append-only evidence: queue receipts, event ledgers, test output, workspace/change IDs,
   review reports, provider receipts, seals, and release records.
5. `project-management/CURRENT/*` for bounded handoff/focus only; current files cannot override the board,
   evidence, or authenticated authority.

The current [`ship-org-build-state.html`](../viewers/ship-org-build-state.html) is a dated, hand-authored
snapshot and may be useful historical context, but it is not self-updating build truth. A maintained
`docs/viewers/ship-building.html` should replace it as the primary human build view. Every row on that page
must show an as-of time, source/evidence pointer, owner, dependency, and one of `recorded`, `receipt`,
`reported`, `derived`, `configured`, or `unknown`. Hard-coded counts without a cited query or retained test
artifact are not current status.

The first build program displayed there should make these gates explicit:

| Program | Honest next gate |
|---|---|
| Manual | Canonical source complete, guardian identity applied to the visual Manual, Captain/officer volumes linked, viewer/source drift check passing |
| Ship organization | S1d evidence, then S2 No1/Chief Engineer route and one repeatable personal-cell template |
| Ship Computer Phase 0 | Ratified schemas, identities, truth/transition registry, RBAC/redaction matrix, fixtures, and threat model |
| Ship Computer Phase 1 | External store/writer, Command Graph vertical slice, authenticated snapshot/coverage API, SSE stream, crash recovery, and evidence-complete Captain voyage |
| New Bridge design | Starts only after the Phase 1 snapshot/stream contract can drive a truthful prototype |
| Factory/landing | Chief Engineer-to-Incubator PM delivery and the single landing broker proven with isolated workspaces and rollback evidence |

When the Ship Computer is live, the Building page becomes a read projection over its command/work graph and
event stream. It must retain the same evidence vocabulary during migration and must show board-only,
configured, stale, sensor-missing, and unknown states rather than flattening them into `building` or `done`.

## 16. Captain's operating route

1. Read authenticated Commodore direction, `current`, Brain focus, and the personal board.
2. Decide whether the need is personal thought, bounded evidence, ship operations, personal tooling, or
   factory-scale engineering.
3. Route personal thought to the Advisor; broader evidence work to Science; administration/research to
   the PA; personal tooling to the personal engineer; broad engineering through the Chief Engineer.
4. State objective, constraints, acceptance, evidence, priority, and grant. Keep implementation choice
   with the receiving seat.
5. Record the returned envelope ID. Queue receipt is not completion.
6. Correlate the report to the exact envelope and acceptance conditions. Name what remains unverified.
7. Update board/current. Promote only reusable judgment to Brain; route canonical doctrine and sealing
   through the proper record process.
8. Require isolated workspaces for writers and a brokered landing before accepting a repository change.

## 17. Hull-stress: what this manual cannot prove

- It cannot prove that a configured/unmanned endpoint will wake, execute, or return a report.
- It cannot prove current health of persistent local manager sessions.
- It cannot prove per-turn spend where provider cost data was not recorded.
- It cannot prove the final model for Captain, Advisors, Scientists, or line officers; candidates need
  repeated role-specific benches and live dogfood.
- It cannot prove the target personal staff kit, one-brain namespace enforcement, synchronous Advisor
  transport, Chief Engineer interface, landing broker, or unified observability because those are not
  fully built.
- It cannot resolve the CMO naming discrepancy without a newer explicit canonical decision.
- It cannot make the default working copy write-free by stating the target. Enforcement, broker custody,
  and negative tests are required.
- It cannot claim the Ship Computer is watching anything yet. The runtime, external event store, Bridge
  API, live feed, redaction policy, frontend, and Incubator handoff are all target work.
- It cannot claim end-to-end command lineage. The Command Graph ledger, parent/authority enforcement,
  lifecycle transitions, first-class flow views, and acceptance correlation are not built.

## 18. Evidence inspected

- `docs/design/ship-org-design.md` - adjudicated organization, ranks, departments, build order
- `docs/system/captain-harness-manual.md` and `ship/captain-harness/**` - current Captain cockpit
- `ship/bridge-harness/**` and `bridge-advisor-pa/**` - current Meridian and Advisor PA cell
- `config/agents.json` - current officer, manager, and worker model/runtime roster
- `roles/direct/*.md`, `roles/managers/*.md`, `roles/workers/*.md` - current jobs and execution contracts
- `docs/system/spend-governance.md` - grants, custody, and metering posture
- `docs/vision/way-of-the-falcon.md` - ratified constitutional interpretation, command/dissent boundary,
  governed improvement, capability limits, and control test
- `docs/design/standing-orders.md` - Standing Order #1 and the transitional standing-authority model;
  implementation truth remains in the current Brain/grant/custody evidence
- `docs/system/vcs-release-model.md` - current jj-on-git release mechanics and repository isolation basis
- `~/Projects/falcon-ai/falcon-brain` - human-brain/agent-brain component and namespace basis
- `~/Projects/Incubator/roles/direct/pm.md` - external PM and factory responsibility
- `project-management/project.sqlite`, `project-management/CURRENT/*`, and retained test/ledger/change
  artifacts - current build projection inputs with distinct authority and evidence strength
- `docs/shipbook/README.md`, `shipbook-captain.md`, `shared/officer-operating-standard.md`, and
  `departments/*.md` - generated Captain volume, common officer contract, and ten atomic department books
- `docs/design/ship-computer-design.md` and `docs/design/ship-computer-bridge-frontend-plan.md` - target
  architecture and frontend specifications, both explicitly design-only and not built
- `docs/viewers/assets/ship-manual-falcon-guardian.webp` - accepted guardian artwork for the Manual identity;
  presentation data, not a live Bridge or accepted Bridge design

## 19. Incident and recovery doctrine

An incident is any event that can break command continuity, evidence integrity, safety, custody, delivery,
availability, cost control, or recovery. An alert, model refusal, provider block, stale queue, lost session,
failed test, conflicting write, credential exposure, corrupted projection, or bad release is classified by
what actually failed; it is not inflated into betrayal, success, or a diagnosis of intent.

The response loop is:

1. **See and declare.** Open an incident identity; record reporter, affected surface, first observed time,
   evidence, truth class, severity, and what remains unknown.
2. **Stop propagation.** Pause the bounded route, revoke or quarantine the implicated capability when
   authorized, freeze destructive retries, and preserve unaffected command paths.
3. **Preserve evidence.** Retain original logs, envelopes, provider receipts, workspaces, hashes, costs,
   and timestamps. Never rewrite the failed attempt or delete inconvenient evidence.
4. **Scope and route.** Security handles suspected misuse/custody; CMO handles defects, drift, and systemic
   degradation; Counsellor handles mind-health intervention; Ops handles resource/credential continuity;
   Chief Engineer handles engineering recovery through the PM boundary. Serious findings reach the Captain
   directly without passing through an implicated seat.
5. **Recover narrowly.** Prefer idempotent retry, clean-session replacement, restored projection, credential
   rotation, rollback, or compensating action. Do not blind-retry an ambiguous completion or create duplicate
   work to make the board look active.
6. **Verify independently.** Re-run the relevant contract, negative, restore, browser, or voyage test and
   correlate the result to the incident. A process restart is not proof of recovery.
7. **Close and learn.** Record impact, root cause or `unknown`, containment, evidence, recovery, residual
   risk, owner, and prevention task. Supersede wrong records visibly; promote only reusable judgment into
   Brain/doctrine.

Current ledgers, jj history, bug/decision logs, spend watch, and selected harness tests provide partial
incident evidence. A unified incident register, external checkpoint custody, complete sensor health,
automated reconciliation, and tested cross-system restore remain **TARGET / UNVERIFIED**.

## 20. Manual hierarchy and department-book index

The manual set has different authorities and audiences. A visual page does not outrank its source, and a
memory summary does not outrank an authenticated order.

| Layer | Purpose and authority | Current state |
|---|---|---|
| Authenticated Commodore order | Current human command; may supersede lower, older operational text | Direct source; must be captured and cited |
| [`The Way of the Falcon`](../vision/way-of-the-falcon.md) | Ratified constitutional interpretation and capability boundary | **RATIFIED**; enforcement varies by control |
| [`ship-org-design.md`](../design/ship-org-design.md) | Adjudicated target organization, rank, personal cells, and build sequence | Design of record; mixed target/as-built annotations |
| This `ship-manual.md` | Canonical joined human source for how Shipwright is organized and operated | **CURRENT**, mixed as-built/configured/target |
| [`captain-harness-manual.md`](captain-harness-manual.md) | Exact experimental Captain cockpit, state, Brain, tools, routes, and turn recipes | **AS-BUILT** cockpit manual; not proof of S6 migration |
| [`docs/shipbook/`](../shipbook/README.md) | Captain, Commodore, generic officer, and department operating volumes | Captain volume is deterministically generated from this source, the shared officer standard, and all ten department books; Commodore companion remains separately maintained |
| [Visual Manual](../viewers/ship-manual.html) | Human navigation and presentation of this source plus the appropriate books | **BUILT** with the guardian identity and complete Manual Library view |
| [Building page](../viewers/ship-building.html) | Evidence-linked projection of current build state | **BUILT** from `ship-build-register.json`; static verified snapshot until the Ship Computer exists |

The department-book program now provides one operating volume for every commissioned line and one generic
officer standard shared by all of them. Each book carries mission, rank/authority, inputs and outputs, private
Thinking/Operations/Engineering cell, boards and Brain ownership, tools/connectors/keys, models and grants,
procedures, telemetry/provenance, acceptance, incident handling, cost, failure doctrine, and current versus
target state.

| Required book | Owning seat | Special content |
|---|---|---|
| Captain / command | Captain | Flag route, mission formation, Advisor/PA/Engineer use, panel/gates, acceptance, relief/replacement continuity |
| Generic officer | Applies to every commissioned officer | Boot, packet, PA research, typed orders, seat messages, board dictation, evidence, escalation, incident and handoff recipes |
| No1 / ship operations floor | Commander | Department routing, main-board authority, writer-token handoff, cross-department flow |
| Science | Science Officer / No2 | Hours/days commissions, panels/councils, experiment and source-to-report evidence |
| Intelligence | Intelligence Officer | Fetch/triage pyramid, injection handling, source preservation, synthesis uncertainty |
| Security | Security Officer | Privilege, custody, grants, quarantine, incident evidence, direct alert line, CMO oversight |
| Operations | Operations Officer | Funds, keys, servers, budgets, cost classes, canaries, custody-class human gates |
| Communications | Communications Officer | One-mouth scope, carve-outs, glossary, outbound review, outage/override procedure |
| Tactical | Tactical Officer | Opportunity evidence, downside, dependency on manned Ops/Security, no unilateral movement |
| Counsellor / Doctor | Counsellor | Mind-health intervention, belief-delta evidence, privacy, recovery and outcome review |
| CMO | Detection seat | Whole-surface defect/drift/waste detection and Security watcher duty. Canonical expansion remains unresolved between **Chief Medical Officer** and **Chief Monitoring Officer**; the book must not conceal that conflict. |
| Chief Engineer | Chief Engineer | Ship requirements, logged Incubator PM interface, factory acceptance, candidate/landing/rollback evidence |

All ten department books and the shared officer standard are built as documentation artifacts. That does not
make their described officer seats, transports, or permissions live: `config/ship-officer-routes.json` remains
`design_not_enforced`, and each book names current versus target state. `shipbook-captain.md` is generated from
this source plus every officer source and is available through bounded, integrity-checked `ship.knowledge`
parts. A book update is complete only when its source pointers, revision date, status labels, viewer/index
references, deterministic Captain render, and drift checks are updated together.

The companion visual manual is [`docs/viewers/ship-manual.html`](../viewers/ship-manual.html).
