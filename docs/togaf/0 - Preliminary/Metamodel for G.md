# Metamodel for G

Phase G describes implementation governance. Element articles live directly in `G - Implementation Governance/`; governance reports, checkpoints, and conformance views are managed through catalogs and viewpoints, not subfolders.

## Canonical Element Types

| Group | Element types | Use in Phase G |
| --- | --- | --- |
| Governed delivery | Work Package, Deliverable, Implementation Event | Use for governed delivery units, implementation evidence, releases, reviews, and checkpoints. |
| Conformance and control | Assessment, Requirement, Constraint | Use for conformance assessments, architecture compliance requirements, and implementation guardrails. |
| State tracking | Plateau, Gap | Use for governed architecture states and remaining differences from the approved architecture. |

## Article Guidance

- Keep one markdown file per ArchiMate element.
- Use the element name as the level-1 heading.
- Use a level-1 heading with one of the canonical Phase G element types as the stereotype.
- Link governance records to Phase F migration plan elements and the Phase E work packages or deliverables they govern.
- Link assessments to requirements, constraints, decisions, and evidence.
- Implementation Event elements may represent completed events or received
  commands. Name completed events using past-perfect or past-participle wording,
  meaning something has already happened. Name commands using present-simple
  imperative wording, meaning `Command to do something received` is shortened to
  `Do something`.

## Validation Rules

| Rule | Applies to | Validation |
| --- | --- | --- |
| G1 | Phase G elements | Each Phase G element article must use one of the canonical Phase G element types. |
| G2 | Governance records | Governance records should link to the Phase F plan elements or Phase E work packages and deliverables they govern. |
| G3 | Assessments | Assessments should link to the requirements, constraints, decisions, or evidence they assess. |

## Filename Prefixes

Use the repository filename pattern from [Metamodel](Metamodel.md):
`<type-in-lowercase>-<NNNN>-<slug>.md`.

| Element type | Prefix examples |
| --- | --- |
| Work Package | `work-package-` |
| Deliverable | `deliverable-` |
| Implementation Event | `implementation-event-` |
| Assessment | `assessment-` |
| Requirement | `requirement-` |
| Constraint | `constraint-` |
| Plateau | `plateau-` |
| Gap | `gap-` |
