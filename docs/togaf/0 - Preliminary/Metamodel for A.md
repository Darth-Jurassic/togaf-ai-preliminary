# Metamodel for A

Phase A captures the architecture vision and the motivation/strategy context that makes the vision coherent. Element articles live directly in `A - Architecture Vision/`; motivation and strategy are catalog/viewpoint groupings in process or view documents, not filesystem folders.

## Canonical Element Types

| Group | Element types | Use in Phase A |
| --- | --- | --- |
| Motivation actors and reasons | Stakeholder, Driver, Assessment | Use for who cares, what creates pressure for change, and what interpretation of that pressure shapes the vision. |
| Motivation intent | Goal, Outcome, Principle, Requirement, Constraint | Use for desired end states, measurable results, guiding rules, high-level needs, and limits on the vision. |
| Motivation meaning | Meaning, Value | Use when the architecture needs an explicit shared interpretation or value statement. |
| Strategy | Resource, Capability, Course of Action, Value Stream | Use for what the enterprise can use, what it must be able to do, how it intends to proceed, and how value flows. |

## Article Guidance

- Keep one markdown file per ArchiMate element.
- Use the element name as the level-1 heading.
- Use a level-1 heading with one of the canonical Phase A element types as the stereotype.
- Keep the description vision-level; move detailed business, application, data, technology, or migration content to the later ADM phase that owns it.
- Use `Relations` to connect the vision to Phase B, Phase C, Phase D, Phase E, and Requirements Management.

## Validation Rules

| Rule | Applies to | Validation |
| --- | --- | --- |
| A1 | Phase A elements | Each Phase A element article must use one of the canonical Phase A element types. |
| A2 | Phase A relations | Relations from Phase A to later ADM phases or Requirements Management must link to existing model articles when the target element is known. |

## Viewpoints

### Capability Context Viewpoint

The Capability Context Viewpoint starts with a single `Capability` as the main
element and shows the capability hierarchy, platform or product capability
boundaries, and repository traceability needed to make the capability governable.

Use this viewpoint to answer:

- Which umbrella capability owns or contains the selected capability?
- Which lower-level capabilities are part of the selected capability?
- Which repository or repositories realize the selected capability directly or
  through its child capabilities?
- Which platform, product, AI, security, delivery, or governance concerns guide
  the selected capability?

#### Main Element

| Main element type | Allowed main element |
| --- | --- |
| Capability | One Phase A `Capability` article. |

#### Primary Elements

| Element type | Relationship to main element | Purpose |
| --- | --- | --- |
| Capability | Composition, Aggregation, Specialization, Realization, Serving | Show parent, child, product, platform, or supporting capabilities. |
| Resource | Assignment, Realization, Serving | Show important resources used to provide the capability. |
| Principle | Influence | Show guiding rules that shape the capability. |
| Goal | Realization, Influence | Show goals the capability supports or realizes. |
| Outcome | Realization, Influence | Show measurable outcomes the capability is expected to affect. |
| Artifact | Realization, Association | Show repository or implementation evidence artifacts from later ADM phases. |
| Technology Function | Serving, Realization | Show delivery automation or platform technology functions supporting the capability. |

#### Contextual Elements

Contextual elements may include related Requirements Management records, Phase D
technology artifacts, implementation evidence, and governance elements when they
explain how the capability is realized, governed, or kept traceable.

#### Viewpoint Validation Rules

| Rule | Applies to | Validation |
| --- | --- | --- |
| Ac1 | Capability Context Viewpoint | The main element must be a Phase A `Capability`. |
| Ac2 | Capability hierarchy | Every capability in the viewpoint scope must be connected to the main capability through documented Composition, Aggregation, Specialization, Realization, Serving, or Association relationships. |
| Ac3 | Repository traceability | Every capability in the viewpoint scope must have repository traceability at some level: either the capability itself, one of its child capabilities, or one of its parent platform/product capabilities must link to an existing repository artifact such as [Git Repository](../D%20-%20Technology%20Architecture/artifact-0006-git-repository.md). |
| Ac4 | Repository existence | Repository links used to satisfy `Ac3` must target existing model articles and must not be plain text only. |

## Filename Prefixes

Use the repository filename pattern from [Metamodel](Metamodel.md):
`<type-in-lowercase>-<NNNN>-<slug>.md`.

| Element type | Prefix examples |
| --- | --- |
| Stakeholder | `stakeholder-` |
| Driver | `driver-` |
| Assessment | `assessment-` |
| Goal | `goal-` |
| Outcome | `outcome-` |
| Principle | `principle-` |
| Requirement | `requirement-` |
| Constraint | `constraint-` |
| Meaning | `meaning-` |
| Value | `value-` |
| Resource | `resource-` |
| Capability | `capability-` |
| Course of Action | `course-of-action-` |
| Value Stream | `value-stream-` |
