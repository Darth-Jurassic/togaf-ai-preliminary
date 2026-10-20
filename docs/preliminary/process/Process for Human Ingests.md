# Process for Human Ingests

This repository treats human communication as source knowledge before it becomes model content. Human ingests are records of stakeholder, survey, or helpdesk input. They may create, change, or justify model elements, but they are not canonical ArchiMate elements by themselves.

## Human Ingest Channels

- Stakeholders produce ideas and discussions.
- Surveys produce feedback.
- Helpdesk produces issues.
- Operational availability reports explicitly identified as alerts use the alert channel.
- When a stakeholder talks to an agent, the stakeholder produces an idea unless another channel is explicitly selected.

| Human source | Ingest channel | Default location |
| --- | --- | --- |
| Stakeholder proposal | `idea` | `docs/ingests/ideas/` |
| Stakeholder discussion | `discussion` | `docs/ingests/discussions/` |
| Survey response | `feedback` | `docs/ingests/feedback/` |
| Helpdesk report | `issue` | `docs/ingests/helpdesk/` |
| Operational alert | `alert` | `docs/ingests/alerts/` |

## Session Registration

Register every new AI session directly as one ingest in the applicable channel.
Preserve the source as perceived: a stakeholder talking to an agent produces an
idea unless another channel is explicitly selected. Ingest registration uses no
Plan, is blocked by neither metamodel nor process changes, and does not create a
model or implementation record.

When the stakeholder corrects a session's channel, move the existing record to
that channel, update its title and references, and preserve the source text and
explicit old-to-new identity mapping. Do not register a duplicate session.

Later architecture work may select, combine, transform, or partially reflect an
ingest's implications in a capability- and Work-Package-centric model Plan. Model
Plans live only at `docs/plans/plan-NNNN-slug.md`; their permanent four-digit
number is retained if a context-drifted title requires a slug rename. See
[Process for Model](Process%20for%20Model.md) for the required model Plan
structure. Do not create an ingest Plan or a phase-named Plan.

## Human Ingest Isolation

Register an ingest as the source is perceived. Do not compare it with the current
model, code, well-known practices, or another ingest during registration. Preserve
its uncertainty, contradictions, and omissions rather than resolving or
normalizing them at registration time.

Later model work may compare the ingest with model, code, and other evidence to
select its implications. That comparison belongs in the applicable model Plan,
not in the ingest.

## Idea Ingest Registration

Every new AI session is an idea ingest unless another channel is explicitly
selected. Register the session directly and preserve its source content as
perceived. Do not use Questions, Concerns, blocker discussion, or a Plan for
ingest registration. Blocker discussion is reserved for metamodel and process
Plan work.

## Idea Coverage Index

After an idea is fully considered by architecture modeling, create its companion
`idea-NNN.index.md` record. List every distinct idea part with a `Taken`,
`Postponed`, or `Rejected` disposition, target model element or Work Package,
rationale, owner, and postponed-item review trigger or date. Coverage is complete
only when every idea part has a disposition; it is not a percentage.
