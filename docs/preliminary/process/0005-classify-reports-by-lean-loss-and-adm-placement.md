# Preliminary 0005: Classify Reports by Lean Loss and Ingest Channel

- Record: Reusable policy
- Tags: preliminary, lean, loss, reporting, ingests, model, adm, safe, classification

## Context

[Preliminary 0002](0002-align-architecture-work-with-lean-software-product-development.md)
requires the architecture process to make the lean loss of ignored signals
explicit. Reports should not only describe what someone wants or fears; they
should also make explicit what the organization loses if the signal is ignored.

Lean loss classification helps compare reports without pretending that all
reports are the same kind of input. A report may point to a possible
improvement, an uncertainty, or an already visible problem, and each class
enters through an ingest channel before it is converted into model changes.

## Decision

Every architecture-relevant report must identify one or more lean loss types and
score its market, operational, and technology impact. These metrics support
report classification, board routing, ingest placement, and model conversion.

The lean loss classification does not replace judgment. It is evidence for
classifying the report as an idea, risk, or problem and for deciding which
ingest channel should preserve the source signal.

Market, operational, and technology metrics do not replace board judgment. They
make the dominant concern explicit so the report can be routed to the right
synchronization board while still preserving secondary impacts.

## Lean Loss Types

| Lean loss | Meaning | Typical report signal |
| --- | --- | --- |
| `LL-001 Waiting` | Decisions, clarification, ownership, environment, approval, or architecture guidance arrive too late. | Usually a problem when already observed; a risk when likely to happen; an idea when a possible improvement could reduce waiting. |
| `LL-002 Rework` | Work must be repeated because direction, design, quality, or requirements were wrong or incomplete. | Usually a problem when recurring; a risk when likely; an idea when reuse or standardization could remove rework. |
| `LL-003 Handoff Loss` | Context is lost between sales, analysis, delivery, engineering, support, tenants, or architecture. | Usually a problem when ownership is unclear; a risk when future handoffs will increase; an idea when collaboration tooling or process could reduce the loss. |
| `LL-004 Defect And Quality Loss` | Bugs, fragile design, security exposure, weak tests, poor maintainability, or operational incidents create cost. | Usually a problem when visible; a risk when exposure is probable; an idea when a preventive quality mechanism is proposed. |
| `LL-005 Overproduction` | Teams create features, documents, customizations, or solution options before validated demand or architecture fit exists. | Usually a risk or problem; sometimes an idea when a validation mechanism could prevent premature work. |
| `LL-006 Overprocessing` | Extra approvals, manual coordination, custom report work, documentation, or technical ceremony add effort without proportional value. | Usually a problem when current process is heavy; an idea when automation or simplification could remove it. |
| `LL-007 Inventory And Backlog Aging` | Reports, decisions, requirements, defects, or product work wait long enough to become stale. | Usually a problem when backlog age is visible; a risk when unresolved work is accumulating. |
| `LL-008 Underused Knowledge` | Field evidence, tenant feedback, senior engineering insight, analyst knowledge, or AI-assisted analysis is not used. | Usually an idea when participation could improve learning; a problem when the organization repeatedly ignores available evidence. |
| `LL-009 Market Opportunity Loss` | Revenue, positioning, tenant adoption, product credibility, or timing advantage is lost because learning or response is too slow. | Usually a risk when future loss is probable; an idea when a product direction could capture the opportunity. |
| `LL-010 Governance Loss` | Decisions, exceptions, requirements, or architecture changes cannot be traced, reviewed, or audited. | Usually a risk or problem; an idea when governance automation or repository participation could reduce the loss. |

## Concern Impact Metrics

Every report must score market, operational, and technology impact using a
simple scale from `1` to `5`, where `1` is low impact and `5` is high impact.

| Metric | Scored question | Primary board when dominant |
| --- | --- | --- |
| Market impact | How strongly does the report affect sales, tenant commercial interest, high-level scope negotiation, due diligence, pricing, product positioning, product packaging, market opportunity, or product credibility? | `BOARD-001 Sales and Marketing Board` |
| Operational impact | How strongly does the report affect delivery comfort, ownership, commitment reliability, requirements clarification, planning, coordination, rollout, QA evidence, or operational burden? | `BOARD-002 Delivery Board` |
| Technology impact | How strongly does the report affect architecture, engineering quality, technical feasibility, implementation impact, automation, platform behavior, maintainability, security exposure, DevOps, or technology risk? | `BOARD-003 Architecture Board` |

The highest score usually determines the primary synchronization board. If two
or more metrics are high, the report must still name one primary board and list
the other affected board or boards as secondary participants.

## Report Classification

| Report class | Use when | Ingest entry point | Repository location | Typical model conversion |
| --- | --- | --- | --- | --- |
| Idea | The report proposes a possible product, architecture, process, automation, market, or operating model improvement that still needs validation before it becomes a defined change. | Ideas channel as a learning-loop opportunity. | `docs/ingests/ideas/` | Goal, outcome, principle, requirement, product vision input, formal architecture change request, or candidate work package. |
| Risk | The report describes uncertainty that may harm quality, delivery, compliance, cost, customer or tenant commercial interest, security, maintainability, governance, or market fit. | Source channel that produced the risk signal, commonly discussions, research, regulations, telemetry, logs, or helpdesk. | `docs/ingests/<channel>/` | Assessment, constraint, principle, outcome, requirement, or mitigation decision. |
| Problem | The report describes an observed pain, defect, recurring failure, user or tenant issue, process bottleneck, current-state limitation, or waste already being experienced. | Source channel that observed the problem, commonly helpdesk, telemetry, logs, interviews, or discussions. | `docs/ingests/<channel>/` | Driver, assessment, outcome, requirement, or formal architecture change request. |

## Ingest And Model Placement Rules

- Put raw reports in `docs/ingests/<channel>/` first so the original signal
  remains auditable.
- Move only interpreted architecture implications into canonical ArchiMate model
  elements under `docs/model/`.
- Use the Motivation model layer when a validated report changes drivers,
  assessments, goals, outcomes, principles, requirements, or constraints.
- Use Business, Application, or Technology model layers when a
  validated report requires structural or behavioral architecture detail in those
  layers.
- Use Implementation and Migration when a validated report requires solution
  grouping, roadmap sequencing, migration planning, or implementation increments.
- Keep model requirements linked to every report class once a report produces or
  changes a requirement.

## Consequences

- Lean loss and concern-impact metrics become practical ways to compare reports
  and explain priority.
- Report classification and board routing stay connected to evidence, not only
  to opinion.
- The repository can show which ingest channel preserved each source signal and
  how that signal affected later architecture work.
