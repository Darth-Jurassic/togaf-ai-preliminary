# Process for B — Business Architecture

Phase B defines business behavior and structure traced to the approved Motivation
and Strategy definitions. Shared session/record rules are in
[Process for Model](Process%20for%20Model.md).

## Initiation

- Announce the selected Plan and unfinished Stage B. Verify Stage A's canonical
  definitions, Assessment criteria, and Completion evidence for this scope. If
  a prerequisite is unfinished, report it rather than starting downstream design.
- Read Business Architecture, its BQ/BC rows, and the relevant A articles. Read
  [Metamodel for Business](../metamodel/Metamodel%20for%20Business.md).
- Identify all relevant actors, roles, collaborations, products, processes,
  functions, services, interfaces, events, and business objects, and distinguish
  observed baseline from target policy and behavior.

## Progress

- Create/update every relevant Business article and put all business definitions
  there. Link each from the Plan's Baseline or Changes section.
- Establish valid upstream traces to Motivation and Strategy. Validate endpoints,
  reciprocal relationships, and requirement satisfaction rather than relying on
  similarly named prose across documents.
- Define business rules, actor authority, and observable outcomes. Refine the
  relevant Assessment criteria for later test coverage; do not claim tests passed
  or implement them during B. F assigns coverage to Work Packages; G runs tests.
- Resolve BQ/BC items from evidence or stakeholder decisions and preserve their
  stable IDs. Update Plan work/progress and phase Completion verification.
- If a business definition invalidates A, reopen the relevant A gate and report
  that dependency before continuing affected work.

## Completion

Set Stage B `Complete: yes` only when every relevant business term is canonical,
all required Motivation/Strategy traces validate, and no unresolved BQ/BC blocks
the scope. Verification links the Business definitions and upstream traces and
identifies the observable outcomes that F will cover with tests.

Report B complete and [Stage C](Process%20for%20C.md) for the next session. There
are no implementation, runtime configuration, deployment, or test-code changes.
