# Metamodel for F

Phase F describes migration planning. Element articles live directly in `F - Migration Planning/`; planning views and roadmap groupings are managed through catalogs and viewpoints, not subfolders.

## Canonical Element Types

| Group | Element types | Use in Phase F |
| --- | --- | --- |
| Migration plan units | Work Package, Deliverable | Use for planned units of migration work and outputs needed to execute the roadmap. |
| Transition roadmap | Implementation Event, Plateau, Gap | Use for migration milestones, transition states, and differences between current, transition, and target states. |
| Planning controls | Requirement, Constraint | Use for planning requirements, sequencing constraints, dependency constraints, and roadmap governance limits. |

## Article Guidance

- Keep one markdown file per ArchiMate element.
- Use the element name as the level-1 heading.
- Use a level-1 heading with one of the canonical Phase F element types as the stereotype.
- Link migration work back to Phase E work packages, plateaus, gaps, and deliverables.
- Link roadmap constraints to managed requirements in Requirements Management when they need traceability.
- Implementation Event elements may represent completed events or received
  commands. Name completed events using past-perfect or past-participle wording,
  meaning something has already happened. Name commands using present-simple
  imperative wording, meaning `Command to do something received` is shortened to
  `Do something`.

## Validation Rules

| Rule | Applies to | Validation |
| --- | --- | --- |
| F1 | Phase F elements | Each Phase F element article must use one of the canonical Phase F element types. |
| F2 | Migration work | Migration work should link back to the Phase E work package, plateau, gap, or deliverable it plans. |

## Filename Prefixes

Use the repository filename pattern from [Metamodel](Metamodel.md):
`<type-in-lowercase>-<NNNN>-<slug>.md`.

| Element type | Prefix examples |
| --- | --- |
| Work Package | `work-package-` |
| Deliverable | `deliverable-` |
| Implementation Event | `implementation-event-` |
| Plateau | `plateau-` |
| Gap | `gap-` |
| Requirement | `requirement-` |
| Constraint | `constraint-` |
