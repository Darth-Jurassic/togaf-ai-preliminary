# Process for G — Implementation Governance

Phase G implements and delivers the Work Packages, then reverse-delivers evidence
to canonical layer elements. Shared rules are in
[Process for Model](Process%20for%20Model.md) and
[Process for Model Records](Process%20for%20Model%20Records.md).

## Initiation

- Announce the selected Plan and unfinished Stage G. Verify A–F Completion for
  the implementation scope, including canonical definitions, realization/
  feasibility checks, Work Package coverage, and applicable dependencies.
- Read G's Left to apply, Applied, GQ/GC items, Work Packages, target articles,
  and repository instructions. Run `$init` before first repository access or
  when tooling, authentication, or remote targets change.
- Establish exact repository branches, runtime/configuration targets, required
  validation commands, delivery authority, and resulting evidence locations.
  Effective implementation starts here, not during A–F discussions.

## Progress

- Apply the effective code/configuration/test changes defined by the Work
  Packages; build and test them, produce artifacts, and deliver through the
  authorized publication/deployment path. Use only matching governed worktrees.
- Reverse-deliver source/revision and code evidence to Application articles;
  test evidence to Business articles; and applicable Kubernetes, test, API,
  artifact, and deployment evidence to Technology articles. Link it from Applied
  and the Work Packages; do not leave proof only in the Plan or chat.
- Evidence includes exact revisions, paths/URLs, commands/results, artifacts,
  and runtime observations where applicable. Record missing evidence explicitly.
- Preserve observed baseline versus target claims. G collects the evidence;
  H evaluates Assessments against their criteria. A successful Git merge alone
  proves neither runtime behavior nor the architecture's validation criteria.
- Publish complete tested worktrees, not selected scope paths. Follow `$plan`
  commit/push/squash/branch-cleanup rules, without bypassing required checks.
- Use explicitly approved, uniquely named, isolated resources for experimental
  harness/restore workloads. Do not alter working environments for experiments;
  record cleanup and never commit or expose Secret values.
- Resolve GQ/GC items and update remaining actions. Changed requirements or
  architecture reopen relevant preceding gates before dependent implementation.
- Keep G/G1 active when compatible clarifications raise earlier-phase Questions
  or refine the statement of work. Apply [focused prerequisite reconciliation](Process%20for%20Model.md#focused-prerequisite-reconciliation):
  update the owning A–F records, definitions/traces, feasibility and Work Package
  coverage in the same session; verify them before continuing dependent code.
  Do not turn every BQ/CQ answer or focused F1 coverage update into a mandatory
  new phase session. Material scope changes and genuinely unresolved prerequisites
  still block their dependent implementation.

For repeated delivery, select G1/G2 scope explicitly and verify its own F1/F2
coverage plus A–E and promotion dependencies. G1 may deliver the first slice
while unrelated F2 remains unfinished. G collects that iteration's implementation,
technical validation and deployment evidence; a manual acceptance gate assigned
to H1 is performed/evaluated there, not claimed passed by G's health checks.
G2 requires completed F2 and the selected H1 gate. Keep overall G incomplete
until every applicable delivery iteration has its reverse-delivered evidence.

## Completion

Set Stage G `Complete: yes` only when scoped Work Packages are implemented and
delivered, required validation passes, and evidence is linked back to every
relevant canonical target. Required delivery actions cannot remain in Left to
apply, and unresolved GQ/GC cannot block the scope. Verification links repository,
build/test, artifact, deployment, and layer evidence as applicable.

For an explicitly selected iteration, close its scoped G1/G2 record and report
H1/H2 next when its delivery/evidence gate passes; do not close overall G while
another iteration is unfinished. Otherwise report G complete and
[Stage H](Process%20for%20H.md) for the next session.
Plan finish is a separate explicitly requested operation after durable closure.
