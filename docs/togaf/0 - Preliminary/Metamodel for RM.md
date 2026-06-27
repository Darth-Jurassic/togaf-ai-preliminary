# Metamodel for RM

Requirements Management is the cross-phase trace hub for architecture requirements and constraints. Element articles live directly in `RM - Requirements Management/`.

## Canonical Element Types

| Group | Element types | Use in Requirements Management |
| --- | --- | --- |
| Requirement backlog | Requirement | Use for architecture requirements that must be traced, realized, tested, or governed across ADM phases. |
| Managed limits | Constraint | Use for limits that should be tracked as requirements management items rather than only vision-level context. |

Vision-level requirements and constraints may start in Phase A when they explain the architecture vision. Move or duplicate only the managed requirement record into Requirements Management when it needs backlog-style traceability.

## Article Guidance

- Keep one markdown file per managed requirement or constraint.
- Use the element name as the level-1 heading.
- Use a level-1 heading with `«Requirement»` or `«Constraint»` as the stereotype.
- Link each requirement to its originating element in Phase A or another phase under `Relations` when that trace is architecturally meaningful.
- Link each requirement to the Phase B behavior it supports and the Phase C/D/E elements that realize or deliver it.

## Validation Rules

| Rule | Applies to | Validation |
| --- | --- | --- |
| RM1 | Requirements Management elements | Each Requirements Management element article must use `«Requirement»` or `«Constraint»` as the stereotype. |
| RM2 | Managed requirements | Managed requirements should link to originating, supported, realized, tested, or governed elements when those traces are known. |

## Filename Prefixes

Use the repository filename pattern from [Metamodel](Metamodel.md):
`<type-in-lowercase>-<NNNN>-<slug>.md`.

| Element type | Prefix examples |
| --- | --- |
| Requirement | `requirement-` |
| Constraint | `constraint-` |
