# Process for Model

This is the general entry point for capability- and Work-Package-centric model
Plans. TOGAF 10 ADM supplies the A–H responsibilities and sequencing; SAFe/lean
learning loops supply the signal-to-work frame; the local metamodel supplies the
canonical vocabulary. Definitions live under `docs/preliminary/`, canonical
elements under `docs/model/`, and source signals under `docs/ingests/`.

The method is refined through playtesting: an observed process wall becomes a
phase-owned Question/Concern, a process correction, or an `Assessment «gap»`.
Implementation repositories reference this shared process rather than duplicating
it. This is a local profile, not a claim of ArchiMate 4 conformance.

## Phase Processes

Each architecture session works on one Plan, one phase, and an explicit scope.
Read this general process and the selected phase process; phase-specific
initiation, progress, and completion obligations live in those linked articles.
Their next-session progression applies when that phase is the active session,
not when its definitions/gate criteria are revisited through focused prerequisite
reconciliation inside a later phase.

| Phase | Plan section | Process | IDs |
| --- | --- | --- | --- |
| A | Architecture Vision | [Process for A](Process%20for%20A.md) | AQ / AC |
| B | Business Architecture | [Process for B](Process%20for%20B.md) | BQ / BC |
| C | Application Architecture | [Process for C](Process%20for%20C.md) | CQ / CC |
| D | Technology Architecture | [Process for D](Process%20for%20D.md) | DQ / DC |
| E | Opportunities and Solutions | [Process for E](Process%20for%20E.md) | EQ / EC |
| F | Migration Planning | [Process for F](Process%20for%20F.md) | FQ / FC |
| G | Implementation Governance | [Process for G](Process%20for%20G.md) | GQ / GC |
| H | Architecture Change Management | [Process for H](Process%20for%20H.md) | HQ / HC |

[Process for Model Records](Process%20for%20Model%20Records.md) defines shared
evidence, article notation, legacy mapping, and runtime record conventions.
[Process for Preliminary](Process%20for%20Preliminary.md) governs process and
metamodel changes; [Process for Human Ingests](Process%20for%20Human%20Ingests.md)
governs session-source registration.

## Session Initiation

1. Read `AGENTS.md`. Locate the governing Plan worktree ancestor using the
   adopting repository identity and naming contract in [Plan Operations](Plan%20Operations.md).
   Include ancestors of nested `repos/` worktrees. Its
   four-digit suffix selects exactly one `docs/plans/plan-NNNN-slug.md`; the Git
   branch, most recent edit, and last implementation activity do not select it.
   The governing root on `main` has no current Plan and only assigns Plans.
2. Apply Preliminary blockers before model work. Register the session directly
   as one ingest even when blocked. Read the current Plan in full and related
   Plans touching its capability or Work Packages to establish dependencies.
3. Inspect the phase Completion records in A–H order for the requested scope.
   Select the earliest unfinished phase. Missing Completion, `Complete: no`,
   missing verification, an unresolved gate dependency, or contradicted evidence
   means unfinished. Never infer completion from a merge or code's existence.
   For explicitly selected F1/G1/H1 or another iteration, use its scoped records
   and common prerequisites under [Scoped Delivery Iterations](#scoped-delivery-iterations),
   rather than treating unrelated later-slice incompletion as its blocker.
4. Read the selected `Process for A` through `Process for H` and relevant layer
   metamodels. Begin with the Plan number, selected phase, unfinished result,
   and its concrete remaining definitions, Questions, Concerns, or evidence.
   For example: **Plan 0020 — Stage A (Architecture Vision) is not finished;
   we need to discuss it.** Then follow that phase's Initiation instructions.
5. An explicitly requested later phase may proceed only when all its relevant
   preceding gates are verified. Otherwise report the earliest incomplete
   prerequisite. Independent scopes may progress separately with explicit
   scope-specific verification; an unfinished unrelated scope is not a waiver
   of the selected scope's own gates. Without a selected scope, use the whole Plan.

Keep the session phase fixed. If it completes, report the next unfinished phase
for the next session; do not automatically begin it. Explicit user redirection
can select another phase after its prerequisites are checked. If all phases are
complete, report that result and assess `$plan finish` conditions without
invoking finish unless requested. Publication commands follow the Plan skill;
publishing existing work does not assert that architecture gates are complete.

### Focused Prerequisite Reconciliation

An active phase may expose a question owned by an earlier phase, a compatible
minor change or a more precise statement of work. Question ownership is not a
command to change the active session phase or restart the ADM sequence.

1. Keep the active Plan/phase/iteration. Register the source and put the question
   or concern in its owning A–H section with its stable phase-local ID.
2. Resolve the answer and update the relevant canonical definitions, relationships,
   realization/feasibility conclusions and Work Package implementation/test
   coverage. Earlier-phase Progress and gate criteria still apply to those updates.
3. Revalidate only the affected prerequisite scope and record its actual evidence.
   Use scoped incomplete records while needed; preserve unrelated verified scopes
   and historical execution evidence. An answer alone does not pass a changed gate.
4. Block dependent implementation while an answer, definition, trace or coverage
   check is missing. Continue independent authorized work. Once the affected
   prerequisites pass, resume the active phase in the same session without requiring
   a separate user acknowledgement or a new session for each reviewed phase.

For example, G1 may resolve a BQ, refine C/D contracts, review E consistency and
update F1 coverage in place, then continue G1 implementation. The active phase
remains G1; these are prerequisite reconciliations, not sequential standalone
B/C/D/E/F sessions. Do not end an ongoing G1 session solely because a compatible
clarification needed an earlier-phase review.

This rule applies to refinements compatible with the selected capability and
scope, including clarifying its statement of work. A material change that
invalidates the agreed direction or introduces unresolved new scope requires
explicit replanning of the affected scope; do not label it minor merely to avoid
the gate. Initial phase selection for genuinely unfinished planning and explicit
phase advancement remain governed by Session Initiation. Neither case permits
code/configuration changes before their relevant planning gates are verified.


## Plan Records

Use `docs/plans/plan-NNNN-slug.md`. The number is permanent; rename only a drifted
slug. Declare `- Type: feature`, `fix`, or `groom` below the title. Feature work
creates/improves a capability; fixes repair a claimed-ready capability through
existing Work Packages; grooms change governance or records. The shared branch
is the type prefix followed by the filename without `.md`.

A Plan is an editable working record, not a canonical element, ingest, or runtime
task log. It has no Plan-wide `Status`, candidate/reviewed-revision status, or
phase-key priority. Phase Completion describes gate evidence, not Plan lifecycle.
Use this section structure:

```text
## Goal
## Context
### Capabilities Touched
### Work Packages Touched
### Repositories Affected
## Blockers
### Predecessors
### Successors
## Architecture Vision
### Completion
### Baseline
### Changes
### Questions
### Concerns
## Business Architecture
### Completion
### Baseline
### Changes
### Questions
### Concerns
## Application Architecture
### Completion
### Baseline
### Changes
### Questions
### Concerns
## Technology Architecture
### Completion
### Baseline
### Changes
### Questions
### Concerns
## Opportunities and Solutions
### Completion
### Questions
### Concerns
## Migration Planning
### Completion
### Questions
### Concerns
## Plan
### Left to do
### Progress
## Implementation Governance
### Completion
### Left to apply
### Applied
### Questions
### Concerns
## Architecture Change Management
### Completion
### Changes
### Questions
### Concerns
```

Each Completion section declares `- Complete: yes` or `- Complete: no` and
`- Verification:` with canonical links, validated traces, and remaining work.
Use `no` until the phase's exit criteria are demonstrated for its scope. For
multiple scopes, identify which scope each verification establishes; the overall
value remains `no` until all relevant scopes are complete. A changed definition
reopens affected gates without erasing historical implementation evidence.

### Scoped Delivery Iterations

An explicitly selected rollout may repeat F→G→H for independent delivery slices,
such as F1→G1→H1 followed by F2→G2→H2. The numeric suffix identifies scope/iteration,
not another ADM phase, a question ID, a priority or a separate Plan. Keep the
normal F/G/H sections and Plan-wide Completion records; add linked iteration
Completion/Verification records under the owning sections.

For a selected iteration, inspect A–E and that iteration's preceding scoped gates.
G1 requires F1, not unfinished unrelated F2; H1 requires G1. A rollout may explicitly
require H1 acceptance before F2 starts, then F2 before G2 and G2 before H2. Record
that promotion dependency and its actual evidence; never infer it from a merge.
Without an explicitly selected iteration, use the whole Plan and earliest
unfinished overall gate. Overall F/G/H remain `no` until every applicable iteration
passes its scoped exit criteria. H1 cannot close another scope or finish the Plan.

Each iteration has complete Work Package implementation/test associations,
deliverables, scoped delivery/recovery responsibilities and evidence. Reuse durable
results from prior iterations; carry feedback to the responsible layer/phase and
reopen only affected gates. Session phase remains fixed and no next iteration/phase
starts automatically. Explicit user redirection still requires its prerequisites.
Focused prerequisite reconciliation within that active iteration follows the
rule above and does not constitute starting another phase or iteration.


Questions use `Number | Status | Question | Answer`; Concerns use
`Number | Status | Description | Mitigation`. Place both tables in their owning
phase, retaining empty headers. Use stable phase-local IDs such as `BQ1`/`BC1`,
`open`/`answered` Questions, and `actual`/`covered` Concerns. Retain resolved rows;
do not renumber on Plan merge or rename. Record old-to-new mappings for placement
corrections. `Blockers` contains predecessor/successor dependencies only.

### Phase-Owned Questions And Concerns

Place each item in the phase responsible for answering or mitigating it, not
the phase in which it was discovered. The [phase index](#phase-processes)
defines A–H prefixes. Number questions and concerns independently within each
phase and Plan; keep answered/covered rows and their evidence until deletion.
AI resolves evidence-answerable questions; human input remains necessary for
unavailable information, intent, exceptions, or accountable decisions.

An identifier is stable once assigned: do not reuse or compress numbers when
items close. Ownership corrections or mixed-stage splits receive the next
available phase-owned IDs and an explicit old-to-new mapping. Update active
references while preserving historical source ingests and other Plans' IDs.
Migrate older flat tables when that Plan is reconciled, without silently
renumbering history. Put reconciliation mappings and partial-blocking summaries
under `Plan / Progress` or the relevant phase, leaving `Blockers` for cross-Plan
dependencies. Cite exact active IDs on blocked actions in `Left to do` or
`Left to apply`; independent work still requires its own preceding gates.


## Phase Exit Gates

Before dependent work advances, all preceding-phase terms and definitions must
exist in canonical articles in their relevant layers with valid traces. The
phase processes define the detailed gates: A defines Motivation/Strategy and
Assessment criteria; B–D define Business/Application/Technology and upstream
traces; E checks realization and feasibility; F associates complete test and
implementation coverage with Work Packages; G delivers and reverse-delivers
evidence; H updates Assessments. Plans link definitions, not replace them.

Only dependent work is blocked. Record unfinished planning in `Plan / Left to
do`, phase progress in the relevant definitions and `Plan / Progress`, ready
implementation in `Implementation Governance / Left to apply`, and resulting
evidence in `Applied`. Keep the Plan while work remains; completion evidence must
be durable before `$plan finish` deletes the record.

## Plugin Development Gate

Before developing or adjusting a plugin:

1. Inspect the hosting System Software, its exact selected source revision, and
   the build-to-runtime provenance. Record the selected artifact, actual runtime
   version, and installed plugin revision separately; a release label alone is
   insufficient evidence of a contract.
2. Document the plugin Application Component, host composition, functions and
   processes, host-owned Plugin APIs, host-controlled hooks, and plugin-controlled
   calls using [Metamodel for Plugins](../metamodel/Metamodel%20for%20Plugins.md).
3. Establish full observability of the relevant contracts: enumerate loading and
   exported-module rules, lifecycle and disposal, invocation sites and order,
   input/output types, permitted mutations, returned results and errors,
   concurrency and session attribution, dependencies, permissions, storage,
   diagnostic coverage and blind spots. Trace each to exact host source and the
   plugin implementation, with explicit acceptance criteria and evidence.
4. Assert that the architecture and contract evidence are in place before moving
   the adjustment into Implementation Governance. Missing evidence remains a
   blocker in the current Plan and an evidence-backed deficiency is recorded as
   an `Assessment «gap»`; it must not be converted into a conformance claim.
5. Validate loading through the selected host loader, type compatibility, every
   registered hook and controlled call, non-mutation where required, and failure
   behavior. Helper tests alone do not satisfy this gate. Record local source
   conformance separately from deployed conformance, which additionally requires
   installed-source parity and runtime evidence.

Use the selected host’s verified integration guide when available. Full contract
observability means the boundary is understood and verifiable; do not assume
hooks expose every provider request or every possible filesystem edit.

## Repository And Change Control

- The governing root remains read-only for tracked content on `main`. Its
  sibling Plan worktree name uses the adopting repository identity and Plan
  number. Persistent governed clones and nested Plan worktrees both use
  `repos/`, owner and repository path segments. Create the governing sibling
  first, then its `repos/` owner directory, then the governed worktree.
  Only the matching Plan worktree
  performs repository work. Assignment/publication/integration/pause/finish follow
  [Plan Operations](Plan%20Operations.md).
- Every affected repository is listed through its canonical Technology Artifact.
  Create/update that Artifact before adding a repository. Run `$init` before first
  access and when tooling, credentials, or remotes change. Declare necessary
  Remote Interfaces under Context with canonical CLI links and exact targets.
- Push and sew publish every tracked change and non-ignored untracked file in
  every affected worktree, regardless of expected scope/authorship. Stage the
  whole repository and verify no eligible change is omitted. Git-visible
  credentials/generated secrets block publication instead of partial delivery.
- Use squash merges, delete source branches, prune, and delete completed local
  branches. Finishing requires completed scope, durable evidence, all affected
  repositories delivered, and successor dependency updates as Plan Operations defines.
- Do not create another Plan autonomously while one is current. Process,
  metamodel, skill, and AGENTS improvements are implicit groom work in the
  current Plan, governed by Preliminary regardless of the session phase.
- Read related Plans before changing overlapping scope. Deferred incompatible
  capability work belongs to an existing later Plan with successor links; create
  a separate Plan only when none is current or the user explicitly directs one.
- Do not create a Plan for an ingest. Immutable external authority remains under
  `docs/ingests/refs/`; legacy `docs/togaf/` is not an active definition location.

### Coordinated Plan Sewing

Bare `$plan sew`, when implemented, selects every affected repository, including the governing repository
last. A comma-delimited list restricts main refresh, rebase, lease-push, PR/merge
and branch recreation to its resolved members. The initial `$plan push` still
publishes complete affected worktrees; selection never permits partial staging.
The unlisted governing repository receives/publishes evidence on its current Plan
branch but is not rebased, renumbered, merged or recreated by that invocation.

Refresh selected main branches, rebase selected Plan branches, reconcile selected
governing model numbering with incoming-main priority, and publish the
validated rebases with explicit expected-head leases before PR merges. Recheck
main/head/mergeability when concurrent work advances; lease publication is not
a guarantee against later conflicts. Squash-merge selected code repositories,
wait for actual merge/checks, refresh their mains and collect mainline evidence
in canonical model articles/the current Plan. Only then integrate the governing repository
if selected. This is one pass, not a second round after branch recreation.

Recreate only merged selected Plan branches from their verified latest mains,
preserving ignored state, nested repositories and all other Plans' worktrees.
Never discard new uncommitted/unpublished work to obtain a clean recreation.
The governing root remains read-only for tracked content on main; refresh
it fast-forward-only. No direct-main evidence commit or redundant main push is
implied by refreshing mains. Sew keeps the current Plan active and does not
pass A–H gates. The [Plan Operations](Plan%20Operations.md#coordinated-integration)
defines selection, checkpoints, no-change repositories and failure handling.
