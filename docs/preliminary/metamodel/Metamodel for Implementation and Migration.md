# Metamodel for Implementation and Migration

The ArchiMate 4 Implementation and Migration Domain is the reference framework
for this local Implementation and Migration domain definition. This profile specifies
only the element types currently used or explicitly required in this domain.
This article is the operational definition; the external reference is provenance
only.

## Elements

Select an element from the distinguishing definition in this table. Its title and
filename use the forms shown in that row. `NNNN` is unique within an independent
four-digit sequence for that displayed local element type. Convert the element
name to lowercase kebab case for the filename. Include guillemets only when the
element has additional explicit stereotypes.

| Element | Explicit Stereotypes | Implicit Stereotypes | Title | Filename | Definition |
| --- | --- | --- | --- | --- | --- |
| `Work Package` | `«work-package»` | `«concept, element, behavior, implementation-and-migration»` | `Work Package NNNN <Name> «additional, explicit, stereotypes»` | `work-package-NNNN-<name-in-kebab-case>.md` | Bounded one-off actions designed for specified results within time and resource constraints. |
| `Deliverable` | `«deliverable»` | `«concept, element, structure, passive, implementation-and-migration»` | `Deliverable NNNN <Name> «additional, explicit, stereotypes»` | `deliverable-NNNN-<name-in-kebab-case>.md` | Governed result of a Work Package; use Artifact for its technical classification. |
| `Plateau` | `«plateau»` | `«concept, element, composite, implementation-and-migration»` | `Plateau NNNN <Name> «additional, explicit, stereotypes»` | `plateau-NNNN-<name-in-kebab-case>.md` | Relatively stable architecture state during a limited period; not a momentary milestone. |
| `Implementation Event` | `«event, implementation-and-migration»` | `«concept, element, behavior»` | `Implementation Event NNNN <Name> «additional, explicit, stereotypes»` | `implementation-event-NNNN-<name-in-kebab-case>.md` | Instantaneous implementation occurrence; use Work Package for work with duration. |

## Internal Relationships

| Relationship Stereotypes | From Connector Concept Stereotypes | To Connector Concept Stereotypes |
| --- | --- | --- |
| `«aggregation»`, `«composition»` | `«element, implementation-and-migration»` | `«element, implementation-and-migration, same-type»` |
| `«specialization»` | `«element, implementation-and-migration»` | `«element, implementation-and-migration, same-type»` |
| `«association»` | `«element, implementation-and-migration»` | `«element, implementation-and-migration»` |
| `«triggering»`, `«flow»` | `«work-package»` | `«work-package»`, `«event, implementation-and-migration»` |
| `«access»`, `«realization»` | `«work-package»` | `«deliverable»` |
| `«realization»` | `«deliverable»` | `«plateau»` |
| `«triggering»` | `«plateau»` | `«plateau»`, `«event, implementation-and-migration»` |
| `«triggering»`, `«flow»` | `«event, implementation-and-migration»` | `«work-package»` |
| `«triggering»` | `«event, implementation-and-migration»` | `«plateau»` |
| `«access»` | `«event, implementation-and-migration»` | `«deliverable»` |
| `«aggregation»`, `«composition»` | `«plateau»` | `«work-package»`, `«deliverable»` |

## Relationships With Other Domains

| Relationship Stereotypes | From Connector Concept Stereotypes | To Connector Concept Stereotypes |
| --- | --- | --- |
| `«association»` | `«element, implementation-and-migration»` | `«element»`, `«relationship»` |
| `«assignment»` | `«role, business»` | `«work-package»` |
| `«realization»` | `«work-package»`, `«deliverable»`, `«plateau»` | `«structure, strategy»`, `«behavior, strategy»`, `«structure, active»`, `«structure, passive»`, `«behavior, internal»`, `«service»` |
| `«aggregation»`, `«composition»` | `«plateau»` | `«element, strategy»`, `«element, business»`, `«element, application»`, `«element, technology»`, `«grouping»`, `«location»`, `«relationship»`, `«junction»` |
| `«realization»`, `«influence»` | `«work-package»`, `«deliverable»` | `«requirement»` |
| `«aggregation»`, `«composition»` | `«plateau»` | `«requirement»`, `«goal»`, `«outcome»` |
| `«aggregation»`, `«composition»` | `«grouping»`, `«location»`, `«product»` | `«work-package»`, `«deliverable»` |
| `«triggering»`, `«flow»` | `«work-package»` | `«event, business»`, `«event, application»`, `«event, technology»` |
| `«triggering»`, `«flow»` | `«event, business»`, `«event, application»`, `«event, technology»` | `«work-package»` |
