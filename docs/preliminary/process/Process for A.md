# Process for A — Architecture Vision

Phase A defines the Motivation and Strategy terms that justify the Plan and the
Assessments that will evaluate its result. Follow [Process for Model](Process%20for%20Model.md)
for Plan resolution, session selection, records, and shared controls.

## Initiation

- Announce the selected Plan and unfinished Stage A. Read its Goal, Context,
  Architecture Vision, dependencies, and source ingests; distinguish the session
  scope from independently governed work in other Plans.
- Read the [Motivation](../metamodel/Metamodel%20for%20Motivation.md) and
  [Strategy](../metamodel/Metamodel%20for%20Strategy.md) metamodels. Resolve the
  existing canonical baseline before proposing target changes.
- Identify all relevant stakeholders, drivers, goals, outcomes, principles,
  requirements, capabilities, courses of action, and validation needs. Put
  unavailable intent/policy decisions in `AQ` rows and actual concerns in `AC`
  rows. Resolve safe, authoritative matters without invented human blockers.

## Progress

- Create/update every relevant Motivation and Strategy article and put its
  definitions there. Link observed Baseline and intended Changes from the Plan;
  do not leave a term defined only by Plan prose or infer readiness from code.
- Create the canonical Assessments with validation scope, criteria, method, and
  expected evidence. Define several manually evaluable KPIs with name, caption,
  scale maximum, comparison target, and named dimensions with indexed values,
  following the [Motivation metamodel](../metamodel/Metamodel%20for%20Motivation.md#assessment-validation-definitions).
  They have no target validation evidence or passing result
  at this phase. Existing observed evidence stays explicitly baseline evidence.
- Separate observed statements from target expectations. In option analysis,
  distinguish evidence, inference, recommendation, uncertainty, and authority.
  The agent resolves deterministic matters; stakeholders decide intent,
  policy, exceptions, and risk acceptance.
- Trace definitions to their source ingests and validate all affected endpoints
  and reciprocal relationships. Existing Work Packages may supply context;
  creation/coverage for new work is owned by F.
- Update `Plan / Left to do` and `Progress`, phase-owned Questions/Concerns, and
  Completion verification as definitions become canonical. Preserve source
  uncertainty and contradictions in the ingest rather than rewriting the source.

## Completion

Set Stage A `Complete: yes` only when all relevant Motivation/Strategy definitions
and Assessment validation definitions exist canonically, their relationships and
source traces validate, and no unresolved AQ/AC blocks the selected scope.
Completion verification links those articles and explains the checked scope.
No new target validation evidence is claimed.

Report A complete and [Stage B](Process%20for%20B.md) as the next phase for a new
session. Do not advance automatically or perform implementation during A.
