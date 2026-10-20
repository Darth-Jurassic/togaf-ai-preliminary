# Preliminary 0011: Define Phase H Report Intake and Board Routing

- Record: Reusable policy
- Tags: preliminary, phase-h, reporting, sales-marketing-board, delivery-board, architecture-board, lean, scoring, governance

## Context

[Preliminary 0010](0010-run-phase-h-to-phase-a-learning-loop-with-lean-loss-reporting.md)
requires every architecture-relevant report to enter Phase H first, preserve the
original signal, and then flow toward Phase A motivation or requirements when
the evidence is strong enough.

The reporting process must be simple enough that any employee or assisting
agent can submit a report without first knowing the full TOGAF or ArchiMate
model. Product, operational, and technology concerns should be captured as raw
theses before they are interpreted, classified, scored, or converted into
architecture work.

## Decision

Phase H reporting will use a thesis-first intake process.

Anyone may submit a report. An assisting agent may create or structure the
report on behalf of the reporter, but the report must preserve the reporter's raw
thesis before enrichment, interpretation, scoring, or board discussion.

Submitting a report starts with a conversation. The reporter calls an assisting
agent and explains the concern in ordinary product, operational, or technology
language. Based on that discussion, the agent drafts the report, preserves the
raw thesis, classifies the report on the two report dimensions, and proposes the
best-matching board route.

Every Phase H report must be routed to a synchronization board for discussion,
clarification, scoring, and prioritization. Product reports go to the Sales and
Marketing Board. Operational reports go to the Delivery Board. Technology
reports go to the Architecture Board. The reporter must be available during
synchronization to present the report thesis to the sponsor or board and clarify
intent, evidence, and expected loss.

The Phase H report template is part of the Preliminary process definition and is
maintained at [Phase H Report Template](phase-h-report-template.md).
Organization units and board identifiers are defined in
[Preliminary 0012](0012-define-organization-units-for-report-handling.md).
Tenant-centric representative roles for salesman, project manager, and team
lead are also defined there.

## Report Classification Dimensions

Each report must be classified on two dimensions:

- Concern dimension: product, operational, or technology.
- Report-class dimension: idea, risk, or problem.

The concern dimension determines the primary synchronization board. The
report-class dimension determines whether the thesis proposes an idea, describes
uncertainty, or records an already observed pain.

The concern dimension is supported by market, operational, and technology impact
metrics defined in
[Preliminary 0005](0005-classify-reports-by-lean-loss-and-adm-placement.md).

## Concern Dimension

Each report must identify one or more concern types.

| Concern type | Use when the thesis is mainly about | Examples |
| --- | --- | --- |
| Product | Product value, marketability, packaging, tenant experience at the commercial or high-level scope level, sales fit, due diligence, pricing, feature granularity, or product positioning. | Bad UX, high perceived cost, scary due diligence, feature granularity that prevents partial sales. |
| Operational | Delivery comfort, ownership, commitment reliability, process burden, supportability, coordination, unexpected work, or organizational operating pain. | Orphan work, uncomfortable delivery responsibility, random events disrupting commitments. |
| Technology | Architecture, engineering quality, automation, maintainability, impact control, defects, unexpected behavior, manual control, or platform fit. | Too many bugs, too much change impact, automation that still needs manual fine-tuning. |

Reports with mixed concern types must be routed by dominant concern. Secondary
boards should be listed when their input is required for scoring, clarification,
or evidence.

## Report-Class Dimension

Each report must identify one report class.

| Report class | Use when the thesis mainly says | Typical result |
| --- | --- | --- |
| Idea | We might change, add, simplify, automate, package, govern, or improve something. | Board discussion confirms whether the proposed idea should become Phase A motivation, requirement input, a formal architecture change request, or governed architecture work. |
| Risk | Something uncertain may harm sales, delivery, quality, compliance, maintainability, cost, governance, or technology fit. | Board discussion confirms exposure, severity, mitigation priority, and whether the risk becomes an assessment, constraint, requirement, or decision input. |
| Problem | Something painful or wasteful is already happening. | Board discussion confirms the thesis, current impact, priority, and whether the problem becomes a driver, assessment, outcome, requirement, or formal architecture change request. |

Report-class definitions and lean-loss attribution are governed by
[Preliminary 0005](0005-classify-reports-by-lean-loss-and-adm-placement.md).

## Report-Centric Participation Flow

1. Reporter calls or invokes an assisting agent and explains the concern.
2. Agent asks clarifying questions until the raw thesis, source context, and
   expected loss are clear enough to draft a report.
3. Agent drafts the Phase H report, preserving the raw thesis before analysis.
4. Agent classifies the report on both dimensions: concern type and report
   class.
5. Agent proposes the responsible handling organization unit and best-matching
   board route.
6. The board sponsor or steward adds the report to the relevant board discussion
   plan.
7. The reporter is invited to the board discussion to present the thesis and
   clarify evidence, intent, impact, and expected loss.
8. The board discusses the report, agrees or challenges the thesis, scores it,
   and prioritizes it.
9. The board records the synchronization outcome and any trace links to Phase A
   motivation, requirements, decisions, Jira evidence, or related reports.

## Required Intake Structure

Each submitted report must contain these sections before board synchronization:

- Status.
- Reporter.
- Source context.
- Concern type: product, operational, technology, or a combination.
- Report classification: idea, risk, or problem.
- Market, operational, and technology impact scores.
- Responsible handling organization unit.
- Tenant-centric representatives, when known.
- Raw thesis.
- Linked evidence, including Jira incidents or issue links when known.
- Agent-enriched description.
- Lean attribution: loss types, classification, and severity.
- Initial scoring, when available.
- Proposed board route.
- Board discussion plan status.
- Open clarification questions.

Jira incidents and issue links are treated as referenced evidence, not validated
facts, until a later consistency check exists. Reports may still proceed to
board synchronization with unvalidated links if the raw thesis and source context
are clear.

## Enrichment Rules

The report steward or assisting agent may enrich the report after the raw thesis
is preserved.

Enrichment must:

- Restate the thesis in clearer architecture language without replacing the raw
  thesis.
- Add a short description of the product, operational, or technology concern.
- Classify the report as an idea, risk, or problem using
  [Preliminary 0005](0005-classify-reports-by-lean-loss-and-adm-placement.md).
- Identify lean loss types and initial severity.
- Add candidate Phase A motivation or requirements implications when visible.
- Keep uncertainty explicit when evidence is incomplete or unvalidated.

Enrichment must not silently convert a reporter's thesis into an architecture
decision, requirement, or delivery commitment. Conversion requires board
synchronization and the validation flow from
[Preliminary 0006](0006-validate-and-score-reports-with-stakeholder-roles.md).

## Board Routing

| Board | Identifier | Receives | Core participants | Output |
| --- | --- | --- | --- | --- |
| Sales and Marketing Board | `BOARD-001` | Product reports whose dominant impact is sales, tenant commercial interest, high-level scope, due diligence, pricing, product positioning, packaging, or market opportunity. | Sales and Marketing Office representatives, with Delivery Office input when product shaping, clarification, planning, or delivery feasibility is material. | Synchronized product thesis, scoring, priority, sponsor, and Phase A conversion recommendation. |
| Delivery Board | `BOARD-002` | Operational reports whose dominant impact is delivery comfort, ownership, commitment reliability, requirements clarification, QA evidence, rollout, or delivery coordination. | Delivery Office representatives, with Sales and Marketing Office or Technology Office input when market or technology impact is material. | Synchronized operational thesis, scoring, priority, sponsor, and follow-up route. |
| Architecture Board | `BOARD-003` | Technology reports whose dominant impact is architecture, engineering quality, frontend, backend, customization, DevOps, platform, automation, maintainability, security exposure, or technology risk. | Technology Office representatives, with Delivery Office input when requirements, QA, delivery, release, rollout, or tenant customization impact is material. | Synchronized technical assessment, scoring, priority, sponsor, and architecture follow-up route. |

Reports with mixed concern types may be routed to more than one board, but one
board must be named as the primary synchronization owner.

## Synchronization Outcome

After board synchronization, each report must record:

- Responsible handling organization unit.
- Synchronization board.
- Sponsor.
- Tenant-centric representatives involved or consulted.
- Participants or represented roles.
- Discussion plan reference or date.
- Reporter clarification notes.
- Thesis agreement: agreed, challenged, refined, deferred, or rejected.
- Confirmed classification: idea, risk, or problem.
- Confirmed market, operational, and technology impact scores.
- Confirmed lean loss types and severity.
- Scoring and prioritization summary.
- Priority.
- Decision: reject, defer, merge, convert to Phase A, or convert to governed
  architecture work.
- Trace links to related reports, Jira incidents, Phase A elements,
  requirements, or decisions when known.

## Consequences

- Phase H intake stays simple enough for broad participation and agent-assisted
  authoring.
- Raw theses remain auditable even when the report is later enriched or
  challenged.
- Product, operational, and technology concerns are prioritized by the boards
  that can sponsor clarification and action.
- Unvalidated Jira links can support discussion without being mistaken for
  verified evidence.
- Phase A receives better-scored and better-sponsored motivation inputs.
