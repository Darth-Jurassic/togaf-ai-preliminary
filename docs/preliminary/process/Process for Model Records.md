# Process for Model Records

This supporting process preserves the shared article, evidence, legacy, and
runtime-record conventions used by [Process for Model](Process%20for%20Model.md)
and its [A](Process%20for%20A.md)–[H](Process%20for%20H.md) phase processes.
It does not select a session phase or replace a phase's completion gate.

## Canonical Articles And Evidence

- Canonical architecture elements live only under `docs/model/`, one standalone
  Markdown article per element, with `Description`, `Evidence`, and
  `Relationships`. Do not create README files in the model tree.
- Each Plan Baseline links a canonical article and observed evidence. Changes
  link target articles and state intended architecture without claiming applied
  evidence. All relevant definitions belong in the owning canonical layers.
- The agent locates, correlates, and records source, system, artifact, URL,
  code-path, and line-level evidence. Human input is for intent, policy,
  exceptions, and risk acceptance, not routine evidence collection.
- Observed statements cite evidence. Expectations state unverified behavior or
  hypotheses and identify what will verify them. An approved decision is target
  direction, not proof of implementation. Missing evidence must remain visible.
- Every phase may read ingests and contribute traceable evidence or permitted
  canonical relationships. Baseline discovery can move backward across layers
  through observed evidence; target design follows the forward A–H gates.
  Baseline discovery does not authorize out-of-phase target implementation.
- Use `docs/preliminary/process/` for process and `docs/preliminary/metamodel/`
  for local notation, placement, stereotypes, and connector rules. External
  authority under `docs/ingests/refs/` is immutable. Historical `docs/togaf/` and
  legacy phase metamodels do not control current placement.
- Follow the [Metamodel index](../metamodel/index.md) and relevant Motivation,
  Strategy, Business, Application, Technology, and Implementation/Migration
  metamodels. AI can consult the immutable ArchiMate reference without claiming
  that the local metamodel directly conforms to ArchiMate 4.

## Notation Convention

Element headings use the displayed local element type, independent four-digit
number, element name, and any additional explicit stereotypes in guillemets.
For example, `Business Function 0001 Charge My Car` or
`Assessment 0005 Specification Access «gap»`.

When a stereotype identifies the belonging domain, render that domain first in
the displayed type and filename prefix. Do not repeat defining type/domain
stereotypes in guillemets. Implicit, enumerated, and functional stereotypes are
never displayed. Omit guillemets when there are no additional explicit ones.
Each displayed type has an independent number sequence. Filenames use the
lowercase kebab-case displayed type, number, and element name.

Requirements are formal Requirement elements with valid `«realization»` traces
from satisfying concepts. Do not create or append a local Requirements section
in an element article; existing legacy sections may remain. Source and evidence
representation follows the metamodel; do not add standalone Source metadata.

### Main-priority Number Reconciliation During Sew

When the governing repository is selected for integration, compare the fetched main tree
and the preserved pre-rebase Plan tree, not ambiguous rebase conflict labels.
Incoming-main element identities and numbers take priority for allocation;
preserve substantive content from both branches. Number repair never settles
unrelated semantic conflicts by dropping either side.
For distinct locally created elements colliding with them or with one another,
allocate unused numbers independently by displayed type above the known allocated
maximum for that type, including applicable local/ref/worktree allocations.
Do not renumber a main element just to preserve a local number. An element already
identical to main is reconciled as the same identity, not duplicated blindly.

Rename each affected local article/title and same-base companion directory
coherently; update current identity references, links, relationships, Plan/package
coverage and indexes. Preserve substantive content and source attribution. Keep
raw human quotes, historical revision identities and immutable ingests/refs
unchanged; record explicit old-to-new mappings so historical evidence remains
traceable. Validate type-unique numbering, path/title consistency, companion
placement and affected links/traces before publication. Unresolvable identity
ambiguity or pre-existing duplicate main identities requires an explicit decision;
do not silently pick a main winner or claim global uniqueness while duplicates
remain. This element reconciliation does not renumber Plans, phase-owned question
IDs, ingests or historical evidence. It does not invoke the separate Plan-number
housekeeping exception.

## Legacy Documentation Mapping

Do not create separate `docs/adrs`, `docs/features`, or `docs/tests` documents
for architecture decisions, feature definitions, or validation criteria.

- ADR decisions belong in the canonical element that owns the decision: commonly
  A's Principle, C's application/data element, D's technology element, F's Work
  Package, or G's governance element.
- Feature definitions belong in the providing Application Service, Component,
  or Data Object. Requirements remain separate formal elements with realization
  traces rather than local requirement lists.
- Assessments and validation definitions are created in A, refined with layer
  design, associated with coverage in F, evidenced in G, and evaluated in H.
- Preserve original legacy source text during migration, with Description,
  Evidence, and Relationships expressing the current architectural conclusion.

## Quality Channels

| Work | Readiness | Completion evidence |
| --- | --- | --- |
| Ingest registration | Preserve perceived source directly; no Plan or model comparison required. | Durable channel ingest. |
| Architecture modeling | Relevant source, definitions, relationships, and canonical scope identified. | Canonical articles and source/relationship validation for A–D. |
| Opportunities and solutions | Canonical A–D definitions and traces complete. | E's realization, cross-layer consistency, and feasibility checks. |
| Migration planning | E's check complete. | F's Work Package implementation/test coverage. |
| Implementation Governance | Scoped A–F gates complete and effective action ready. | G's code, tests, artifacts, delivery, and reverse-delivered evidence. |
| Architecture Change Management | Criteria and evidence targets defined; G result available. | H's evaluated Assessments or explicit routed gaps. |

## Process Documents

For adopters implementing process automation, process record names are singular.
This optional vocabulary does not require a database, runner or telemetry stack
for file-based architecture work, nor claim that one is supplied here:

- `ProcessPhase` describes a phase and has at least Name and Actor. Actor names
  who is called when a handler cannot proceed.
- `ProcessTask` describes non-runtime coordination of process/metamodel blockers
  and Plan progress. It is not a RuntimeTask and cannot fail.
- `ProcessTool` describes callable tools, CLI operations, APIs, or MCP servers.
- `ProcessModel` describes LLM/model capabilities and handler selection context.
- `ProcessHandler` binds events/conditions to actions, tools, models, validations,
  viewpoints, context-building, and follow-up records.
- `RuntimeTask` is the durable runtime action/task log for effective application,
  not a ProcessTask or a Plan's architecture definition.

Keep Process records descriptive. Runtime actions use RuntimeTask, not an Action
document prefix. RuntimeTask records are durable audit records. Runtime telemetry
uses the selected implementation’s verified instrumentation, including explicit
message-size observability where a publisher contract requires it.

## RuntimeTask Lifecycle

| Status | Meaning | Transition |
| --- | --- | --- |
| pending | Waiting for predecessors. | Failure wins over cancellation; ready only when every predecessor succeeded. |
| ready | All dependencies succeeded; waiting for a runner. | in progress when a runner takes ownership. |
| in progress | Runner owns execution. | succeeded, failed, or cancelled. |
| succeeded | Finished successfully. | Successors may become ready. |
| failed | Execution failed. | Every successor becomes failed. |
| cancelled | Execution cancelled. | Every successor becomes cancelled unless another dependency failed. |

Failure takes precedence when predecessors have mixed terminal states. Otherwise
cancellation wins; only all-success makes a dependent runtime task ready.
Manual architecture work is not a RuntimeTask: record it in its Plan and the
canonical model/implementation records until a future handler automates it.

## ProcessTask Blocker Gate

A ProcessTask cannot fail. Resolve safe, deterministic matters from authoritative
context before recording a blocker. Process/metamodel blockers belong in the
governing Plan's Left to do, with phase-owned Questions/Concerns where applicable;
clarification does not cause a failed transition.

Plans are non-effective working records. They state intended architecture and
implementation; effective work updates the canonical model or implementation.
Preserve the distinction between a discussion, a ready action, an executed action,
and evidence of its result throughout all phases.
