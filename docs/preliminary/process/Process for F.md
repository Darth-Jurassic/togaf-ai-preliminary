# Process for F — Migration Planning

Phase F assigns implementation and test coverage to canonical Work Packages.
Shared session/record conventions are in
[Process for Model](Process%20for%20Model.md).

## Initiation

- Announce the selected Plan and unfinished Stage F. Verify A–E gates and the
  Phase E realization/feasibility result for the scope.
- Read Migration Planning, Context Work Packages/Repositories, dependencies,
  FQ/FC items, and
  [Metamodel for Implementation and Migration](../metamodel/Metamodel%20for%20Implementation%20and%20Migration.md).
- Identify all relevant Business test targets and Application/Technology
  implementation targets, including reused baseline targets and their evidence.

## Progress

- Create required Work Packages or update already-governed packages and associate
  them with every canonical element to implement and test. A fix contributes to
  existing Work Packages without creating a new one.
- Ensure planned test coverage for every relevant Business element and planned
  implementation coverage for every relevant Application and Technology element.
  Each association identifies the expected evidence and responsible work item.
- Define deliverables, repository scope, sequencing, transition dependencies,
  delivery/rollback actions, and verification. Dependencies refer to durable
  model/Work Package/implementation results, not a sequence of phase-named Plans.
- Planned coverage does not mean tests passed or implementation delivered. Cite
  evidence when reusing a baseline; a repository's existence is not coverage.
- Resolve FQ/FC items and record progress. Put ready implementation/delivery
  actions in G's Left to apply only after the scoped preceding gates are complete.

For an explicitly selected repeated F/G/H rollout, map the complete coverage for
that iteration (F1 or F2), including shared dependencies and its manual acceptance
criteria. When the selected rollout gates F2 on H1, require that promotion result
before planning the second slice and reuse its accepted evidence/feedback.
Do not require all F2 work before G1 when F1's
own gates/coverage are verified. Keep iteration records and overall F Completion
separate under the current Plan; unfinished F2 means overall F remains incomplete.

## Completion

Set Stage F `Complete: yes` only when every relevant test/implementation target
has a valid Work Package association, sequencing and evidence responsibilities
are explicit, and no FQ/FC blocks the scope. Verification links the Work Packages
and their complete coverage mapping; it does not claim target execution results.

For an explicitly selected iteration, close its scoped F1/F2 record only and
report G1/G2 next when its gates pass; the overall field remains no until all
applicable F iterations are complete. Otherwise report F complete and
[Stage G](Process%20for%20G.md) for the next session.
