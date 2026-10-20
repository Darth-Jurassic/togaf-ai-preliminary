# Process for E — Opportunities and Solutions

Phase E is the final architecture realization, consistency, and feasibility
check before Work Package coverage. Follow
[Process for Model](Process%20for%20Model.md) for session and record conventions.

## Initiation

- Announce the selected Plan and unfinished Stage E. Verify A–D Completion and
  the linked canonical definitions for the selected scope.
- Read the Plan's solution direction, EQ/EC items, all relevant layer articles,
  and the metamodel connector rules. Establish the complete source/target scope
  rather than selecting only elements with readily available evidence.

## Progress

- Check that every Plan-related Motivation and Strategy element has realization
  coverage through Business, Application, or Technology elements.
- Use permitted direct relationships or valid paths to downstream realizations.
  Do not invent an invalid direct `«realization»` for a type that disallows it,
  or treat an unqualified association as proof of realization.
- Validate Business–Application–Technology traces for completeness, consistent
  responsibilities, valid endpoints/reciprocal tuples, and feasible contracts,
  boundaries, dependencies, deployment, and transition assumptions.
- Link the realization/feasibility findings from Opportunities and Solutions.
  Return missing definitions to A–D; record only unresolved phase-owned EQ/EC
  decisions and actual concerns requiring later action.
- Do not create implementation/test evidence from design expectations. Existing
  Work Packages can provide context, but F owns the required coverage mapping.

## Completion

Set Stage E `Complete: yes` only when realization coverage is complete and all
cross-layer consistency/feasibility checks pass for the scope. Verification
links the checked definitions and trace coverage. Missing or contradictory
upstream terms reopen their gates; unresolved EQ/EC blocks dependent F work.

Report E complete and [Stage F](Process%20for%20F.md) for the next session.
