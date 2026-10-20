# Process for C — Application Architecture

Phase C defines Application and Data Object terms and their upstream realization
and dependencies. Follow [Process for Model](Process%20for%20Model.md) for shared
session and record rules.

## Initiation

- Announce the selected Plan and unfinished Stage C. Verify A–B completion for
  the scope from canonical definitions and validated traces, not Git activity.
- Read Application Architecture, CQ/CC items, and the relevant Motivation,
  Strategy, and Business articles. Read
  [Metamodel for Application](../metamodel/Metamodel%20for%20Application.md).
- Identify relevant components, collaborations, functions, processes, services,
  interfaces, events, and data objects. Establish what is observed versus target.

## Progress

- Create/update every relevant Application/Data Object article and put all
  application behavior, contracts, state, and responsibilities there. Link the
  definitions from the Plan's Baseline or Changes sections.
- Establish valid traces back to Motivation, Strategy, and Business and validate
  endpoint consistency, reciprocal tuples, ownership, and requirement coverage.
- Define relevant interaction and state contracts sufficiently for later
  technology design and implementation. Inspect code only as observed baseline
  evidence; do not write implementation, configuration, or tests in C.
- Refine validation criteria without supplying target execution evidence. Record
  CQ/CC decisions and remaining work; reopen affected A/B gates if definitions
  change their upstream meaning.

## Completion

Set Stage C `Complete: yes` only when all relevant Application/Data Object terms
exist canonically, their definitions and upstream traces validate, and no CQ/CC
blocks the selected scope. Verification links the articles and contracts rather
than treating the Plan as the sole application definition.

Report C complete and [Stage D](Process%20for%20D.md) for the next session.
