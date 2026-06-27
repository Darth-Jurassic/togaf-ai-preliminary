# Metamodel for E

Phase E packages the architecture into implementation and migration elements. Element articles live directly in `E - Opportunities and Solutions/`; implementation/migration is the phase scope, not a subfolder.

## Canonical Element Types

| Group | Element types | Use in Phase E |
| --- | --- | --- |
| Delivery units | Work Package, Deliverable | Use for units of change and outputs produced by those units. |
| Migration states | Plateau, Gap | Use for stable architecture states and differences between states. |
| Migration timing | Implementation Event | Use for meaningful transition events, releases, milestones, or decision points. |

## Article Guidance

- Keep one markdown file per ArchiMate element.
- Use the element name as the level-1 heading.
- Use a level-1 heading with one of the canonical Phase E element types as the stereotype.
- Link work packages to the requirements, capabilities, application/data elements, and technology elements they deliver or change.
- Link plateaus and gaps to the architecture state they contain or expose.
- Implementation Event elements may represent completed events or received
  commands. Name completed events using past-perfect or past-participle wording,
  meaning something has already happened. Name commands using present-simple
  imperative wording, meaning `Command to do something received` is shortened to
  `Do something`.

## Validation Rules

| Rule | Applies to | Validation |
| --- | --- | --- |
| E1 | Phase E elements | Each Phase E element article must use one of the canonical Phase E element types. |
| E2 | Work Package | Work Packages should link to the requirements, capabilities, application/data elements, or technology elements they deliver or change. |

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
