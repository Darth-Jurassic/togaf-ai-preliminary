# Preliminary 0004: Describe TOGAF 10 ADM Phase Flow

- Record: Reusable policy
- Tags: preliminary, togaf, adm, architecture-process, phase-flow, governance

## Context

[Preliminary 0002](0002-align-architecture-work-with-lean-software-product-development.md)
defines the lean software product development requirements for the architecture
process.
[Preliminary 0003](0003-choose-architecture-framework.md) chooses TOGAF 10 ADM as the
controlling architecture process and governance framework that satisfies those
requirements. The next preliminary concern is to describe the ADM phase flow so
later repository content can be placed consistently.

The current work is in the Preliminary Phase, but the repository must preserve
the connection between Phase H architecture change inputs and Phase A motivation
work because feedback, ideas, risks, and problems are the main evidence base for
the Architecture Vision.

Validated learning must be converted into architecture motivation, requirements,
decisions, and governance. Before target solution structure is described in
detail, the team needs a shared view of why change is needed, who is affected,
what outcomes are desired, and which requirements should guide later work.

## Decision

We will use the TOGAF 10 ADM phase flow to organize architecture work in the
repository.

Architecture work starts with the local Motivation layer. The initial scope is:

- Preliminary Phase assumptions, principles, repository conventions, and method
  choices.
- Phase H feedback and architecture change inputs.
- Phase A stakeholders, drivers, assessments, goals, outcomes, principles,
  constraints, and requirements.
- Requirements directly traceable to feedback, SWOT analysis, and motivation
  elements.

The ADM is iterative. Requirements Management is continuous work performed by
every phase A-H; it is not a separate phase. Architecture change feedback can
cause earlier phases to be revisited when new evidence changes the architecture
motivation, target state, or roadmap. This iteration is how the lean learning
loop becomes part of the architecture process.

[Official TOGAF Standard](https://pubs.opengroup.org/togaf-standard/) describes
the ADM cycle; this repository does not redistribute the standard’s diagram.

## ADM Phases

| Phase | Name | Repository meaning |
| --- | --- | --- |
| A | Architecture Vision | Define stakeholders, concerns, drivers, assessments, goals, outcomes, principles, constraints, and high-level requirements. |
| B | Business Architecture | Describe business capabilities, roles, processes, value streams, and operating model implications. |
| C | Information Systems Architecture | Describe data architecture and application architecture needed to support the business architecture. |
| D | Technology Architecture | Describe platforms, infrastructure, runtime architecture, technology services, and technology standards. |
| E | Opportunities and Solutions | Group solution options, transition architectures, work packages, and candidate implementation approaches. |
| F | Migration Planning | Sequence roadmap increments, release plans, migration paths, dependencies, and value delivery. |
| G | Implementation Governance | Govern implementation against architecture intent, principles, requirements, and approved decisions. |
| H | Architecture Change Management | Capture feedback, ideas, risks, problems, user or tenant signals, and improvement opportunities; close implementation evidence against Assessments and update Motivation Assessments when results require it. |

The Preliminary Phase is the foundation context that establishes architecture
capability, repository conventions, principles, governance, stakeholder
participation, and modeling method. It is not an additional A-H phase plan.
Requirements Management continuously maintains formal Requirement elements and
their traces across all eight phases; it has no separate phase or plan.

## Consequences

- Preliminary work must define how the repository operates before later phases
  expand the architecture content.
- Phase H reports are treated as learning-loop inputs, not as unstructured
  backlog items.
- Phase A motivation and requirements must remain traceable to the reports and
  stakeholder concerns that justified them.
- Early repository work prioritizes traceability from feedback to motivation and
  requirements. Business, application, technology, implementation, and migration
  details are introduced after the motivation baseline is useful enough to guide
  them.
- Later architecture layers should be introduced only when the current ADM phase
  has enough explicit evidence and any applicable `Assessment «gap»` records for
  continuing.
- Business, application, technology, solution, and migration architecture precede
  coding. Effective implementation changes begin only in Phase G under its
  compile, test, artifact, and evidence gate.
