# Metamodel for Strategy

The ArchiMate 4 Strategy Domain is the reference framework for this local
Strategy domain definition. This profile specifies only the element types currently
used or explicitly required in this domain. Strategy defines high-level
abilities, assets, choices, and value creation. This article is the operational
definition; the external reference is provenance only.

## Elements

Select an element from the distinguishing definition in this table. Its title and
filename use the forms shown in that row. `NNNN` is unique within an independent
four-digit sequence for that displayed local element type. Convert the element
name to lowercase kebab case for the filename. Include guillemets only when the
element has additional explicit stereotypes.

| Element | Explicit Stereotypes | Implicit Stereotypes | Title | Filename | Definition |
| --- | --- | --- | --- | --- | --- |
| `Resource` | `«resource»` | `«concept, element, structure, strategy»` | `Resource NNNN <Name> «additional, explicit, stereotypes»` | `resource-NNNN-<name-in-kebab-case>.md` | Valuable asset or means available to the enterprise; not its concrete realization. |
| `Capability` | `«capability»` | `«concept, element, behavior, strategy»` | `Capability NNNN <Name> «additional, explicit, stereotypes»` | `capability-NNNN-<name-in-kebab-case>.md` | Implementation-independent ability; what an entity can do, not how. |
| `Course of Action` | `«course-of-action»` | `«concept, element, behavior, strategy»` | `Course of Action NNNN <Name> «additional, explicit, stereotypes»` | `course-of-action-NNNN-<name-in-kebab-case>.md` | Chosen strategic or tactical approach configuring capabilities and resources. |
| `Value Stream` | `«value-stream»` | `«concept, element, behavior, strategy»` | `Value Stream NNNN <Name> «additional, explicit, stereotypes»` | `value-stream-NNNN-<name-in-kebab-case>.md` | Stakeholder-oriented stages creating an overall result; not case-level task order. |

## Hierarchy Groupings

| Abstract Type | Explicit Stereotypes | Implicit Stereotypes | Definition |
| --- | --- | --- | --- |
| `Strategy Behavior Element` | `«behavior, strategy»` | `«concept, element»` | Strategic ability, approach, or value-creating behavior. |

`«structure, strategy»` matches Resource for connector evaluation.

## Internal Relationships

| Relationship Stereotypes | From Connector Concept Stereotypes | To Connector Concept Stereotypes |
| --- | --- | --- |
| `«aggregation»`, `«composition»` | `«element, strategy»` | `«element, strategy, same-type»` |
| `«specialization»` | `«element, strategy»` | `«element, strategy, same-type»` |
| `«association»` | `«element, strategy»` | `«element, strategy»` |
| `«assignment»` | `«resource»` | `«behavior, strategy»` |
| `«triggering»` | `«behavior, strategy»` | `«behavior, strategy»` |
| `«flow»` | `«behavior, strategy»` | `«behavior, strategy»` |
| `«realization»` | `«capability»`, `«value-stream»` | `«course-of-action»` |
| `«serving»` | `«capability»` | `«capability»`, `«value-stream»` |

## Relationships With Other Domains

| Relationship Stereotypes | From Connector Concept Stereotypes | To Connector Concept Stereotypes |
| --- | --- | --- |
| `«association»` | `«element, strategy»` | `«element»`, `«relationship»` |
| `«realization»`, `«influence»` | `«resource»`, `«behavior, strategy»` | `«requirement»` |
| `«realization»`, `«influence»` | `«course-of-action»` | `«outcome»` |
| `«realization»` | `«product»`, `«location»`, `«structure, active»`, `«structure, passive»` | `«resource»` |
| `«realization»` | `«service»`, `«behavior, internal»` | `«behavior, strategy»` |
| `«realization»` | `«work-package»`, `«deliverable»`, `«plateau»` | `«structure, strategy»`, `«behavior, strategy»` |
| `«aggregation»`, `«composition»` | `«plateau»` | `«structure, strategy»`, `«behavior, strategy»` |
