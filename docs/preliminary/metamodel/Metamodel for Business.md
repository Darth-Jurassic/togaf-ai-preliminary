# Metamodel for Business

The ArchiMate 4 Business Domain is the reference framework for this local
Business domain definition. This profile specifies only the element types currently
used or explicitly required in this domain. Business defines people and
organizations, their responsibilities and behavior, business information, and
customer offerings. This article is the operational definition; the external
reference is provenance only.

## Elements

Select an element from the distinguishing definition in this table. Its title and
filename use the forms shown in that row. `NNNN` is unique within an independent
four-digit sequence for that displayed local element type. Convert the element
name to lowercase kebab case for the filename. Include guillemets only when the
element has additional explicit stereotypes.

| Element | Explicit Stereotypes | Implicit Stereotypes | Title | Filename | Definition |
| --- | --- | --- | --- | --- | --- |
| `Business Role` | `«role, business»` | `«concept, element, structure, active, internal»` | `Business Role NNNN <Name> «additional, explicit, stereotypes»` | `business-role-NNNN-<name-in-kebab-case>.md` | Business responsibility through which an actor performs behavior; not its holder. |
| `Business Collaboration` | `«collaboration, business»` | `«concept, element, structure, active, internal»` | `Business Collaboration NNNN <Name> «additional, explicit, stereotypes»` | `business-collaboration-NNNN-<name-in-kebab-case>.md` | Business participants acting collectively with separate modeled identity. |
| `Business Process` | `«process, business»` | `«concept, element, behavior, internal»` | `Business Process NNNN <Name> «additional, explicit, stereotypes»` | `business-process-NNNN-<name-in-kebab-case>.md` | Ordered business behavior; use when sequence or flow matters. |
| `Business Function` | `«function, business»` | `«concept, element, behavior, internal»` | `Business Function NNNN <Name> «additional, explicit, stereotypes»` | `business-function-NNNN-<name-in-kebab-case>.md` | Business behavior grouped by responsibility, skill, or resources. |
| `Business Service` | `«service, business»` | `«concept, element, behavior»` | `Business Service NNNN <Name> «additional, explicit, stereotypes»` | `business-service-NNNN-<name-in-kebab-case>.md` | Business behavior offered to a consumer; not its internal execution. |
| `Business Event` | `«event, business»` | `«concept, element, behavior»` | `Business Event NNNN <Name> «additional, explicit, stereotypes»` | `business-event-NNNN-<name-in-kebab-case>.md` | Instantaneous business occurrence or state change. |
| `Business Interface` | `«interface, business»` | `«concept, element, structure, active, external»` | `Business Interface NNNN <Name> «additional, explicit, stereotypes»` | `business-interface-NNNN-<name-in-kebab-case>.md` | Business channel or touchpoint exposing services; not the service or provider. |
| `Business Actor` | `«actor, business»` | `«concept, element, structure, active, internal»` | `Business Actor NNNN <Name> «additional, explicit, stereotypes»` | `business-actor-NNNN-<name-in-kebab-case>.md` | Person, organization, or unit able to act; not its responsibility. |
| `Business Object` | `«object, business»` | `«concept, element, structure, passive»` | `Business Object NNNN <Name> «additional, explicit, stereotypes»` | `business-object-NNNN-<name-in-kebab-case>.md` | Business-meaningful concept acted upon; not its automated data form. |
| `Product` | `«product»` | `«concept, element, composite, business»` | `Product NNNN <Name> «additional, explicit, stereotypes»` | `product-NNNN-<name-in-kebab-case>.md` | Coherent package offered as one customer proposition. |

## Internal Relationships

| Relationship Stereotypes | From Connector Concept Stereotypes | To Connector Concept Stereotypes |
| --- | --- | --- |
| `«aggregation»`, `«composition»` | `«element, business»` | `«element, business, same-type»` |
| `«specialization»` | `«element, business»` | `«element, business, same-type»` |
| `«association»` | `«element, business»` | `«element, business»` |
| `«triggering»` | `«behavior, business»` | `«behavior, business»` |
| `«flow»` | `«behavior, business»` | `«behavior, business»` |
| `«access»` | `«behavior, business»` | `«structure, passive, business»` |
| `«assignment»` | `«interface, business»` | `«service, business»` |
| `«assignment»` | `«structure, active, internal, business»` | `«role, business»`, `«structure, passive, business»` |
| `«realization»` | `«behavior, internal, business»` | `«service, business»` |
| `«aggregation»`, `«composition»` | `«behavior, internal, business»` | `«behavior, internal, business»` |
| `«aggregation»`, `«composition»` | `«collaboration, business»` | `«structure, active, internal, business»` |
| `«aggregation»`, `«composition»` | `«role, business»` | `«interface, business»` |
| `«assignment»` | `«role, business»` | `«behavior, internal, business»`, `«event, business»` |
| `«serving»` | `«service, business»` | `«structure, active, business»`, `«behavior, internal, business»` |
| `«serving»` | `«interface, business»` | `«actor, business»`, `«role, business»`, `«collaboration, business»` |
| `«aggregation»`, `«composition»` | `«actor, business»` | `«interface, business»` |
| `«aggregation»`, `«composition»` | `«product»` | `«service, business»`, `«structure, passive, business»` |

## Relationships With Other Domains

| Relationship Stereotypes | From Connector Concept Stereotypes | To Connector Concept Stereotypes |
| --- | --- | --- |
| `«association»` | `«element, business»` | `«element»`, `«relationship»` |
| `«triggering»`, `«flow»` | `«behavior, business»` | `«behavior, strategy»`, `«behavior, application»`, `«behavior, technology»`, `«behavior, implementation-and-migration»` |
| `«triggering»`, `«flow»` | `«behavior, strategy»`, `«behavior, application»`, `«behavior, technology»`, `«behavior, implementation-and-migration»` | `«behavior, business»` |
| `«access»` | `«behavior, business»` | `«structure, passive, application»`, `«structure, passive, technology»` |
| `«access»` | `«behavior, application»`, `«behavior, technology»`, `«behavior, implementation-and-migration»` | `«structure, passive, business»` |
| `«realization»` | `«structure, active, business»` | `«path, technology»` |
| `«assignment»` | `«interface, business»` | `«service, application»`, `«service, technology»` |
| `«assignment»` | `«structure, active, internal, application»`, `«structure, active, internal, technology»` | `«role, business»` |
| `«realization»` | `«behavior, internal, business»` | `«service, application»`, `«service, technology»`, `«behavior, strategy»` |
| `«realization»` | `«behavior, internal, application»`, `«behavior, internal, technology»` | `«service, business»` |
| `«aggregation»`, `«composition»` | `«collaboration, business»` | `«structure, active, internal, application»`, `«structure, active, internal, technology»` |
| `«aggregation»`, `«composition»` | `«role, business»` | `«interface, application»`, `«interface, technology»` |
| `«serving»` | `«service, business»` | `«structure, active, application»`, `«structure, active, technology»`, `«behavior, internal, application»`, `«behavior, internal, technology»` |
| `«serving»` | `«service, application»`, `«service, technology»` | `«structure, active, business»`, `«behavior, internal, business»` |
| `«realization»` | `«interface, application»` | `«interface, business»` |
| `«realization»` | `«object, data»`, `«material»` | `«object, business»` |
| `«assignment»` | `«facility»` | `«actor, business»` |
| `«aggregation»`, `«composition»` | `«network, distribution»` | `«actor, business»` |
| `«aggregation»`, `«composition»` | `«product»` | `«service, application»`, `«service, technology»`, `«structure, passive, application»`, `«structure, passive, technology»` |
| `«realization»` | `«product»`, `«structure, active, business»`, `«structure, passive, business»` | `«resource»` |
| `«realization»`, `«influence»` | `«structure, active, business»`, `«structure, passive, business»`, `«behavior, internal, business»`, `«service, business»`, `«product»` | `«requirement»` |
| `«assignment»` | `«role, business»` | `«work-package»` |
| `«realization»` | `«work-package»`, `«deliverable»`, `«plateau»` | `«structure, active, business»`, `«structure, passive, business»`, `«behavior, internal, business»`, `«service, business»` |
| `«aggregation»`, `«composition»` | `«plateau»` | `«element, business»` |
