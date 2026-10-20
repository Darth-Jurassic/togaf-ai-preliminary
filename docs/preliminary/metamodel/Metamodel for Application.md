# Metamodel for Application

The ArchiMate 4 Application Domain is the reference framework for this local
Application domain definition. This profile specifies only the element types currently
used or explicitly required in this domain. Application defines application
structure, behavior, exposed functionality, and logical data. This article is
the operational definition; the external reference is provenance only.

## Elements

Select an element from the distinguishing definition in this table. Its title and
filename use the forms shown in that row. `NNNN` is unique within an independent
four-digit sequence for that displayed local element type. Convert the element
name to lowercase kebab case for the filename. Include guillemets only when the
element has additional explicit stereotypes.

| Element | Explicit Stereotypes | Implicit Stereotypes | Title | Filename | Definition |
| --- | --- | --- | --- | --- | --- |
| `Application Collaboration` | `«collaboration, application»` | `«concept, element, structure, active, internal»` | `Application Collaboration NNNN <Name> «additional, explicit, stereotypes»` | `application-collaboration-NNNN-<name-in-kebab-case>.md` | Application components acting collectively with separate modeled identity. |
| `Application Process` | `«process, application»` | `«concept, element, behavior, internal»` | `Application Process NNNN <Name> «additional, explicit, stereotypes»` | `application-process-NNNN-<name-in-kebab-case>.md` | Ordered application behavior; use when execution sequence matters. `«plugin-call»` denotes a plugin-controlled call to a host-owned API. |
| `Application Function` | `«function, application»` | `«concept, element, behavior, internal»` | `Application Function NNNN <Name> «additional, explicit, stereotypes»` | `application-function-NNNN-<name-in-kebab-case>.md` | Application behavior grouped as a functional responsibility. |
| `Application Service` | `«service, application»` | `«concept, element, behavior»` | `Application Service NNNN <Name> «additional, explicit, stereotypes»` | `application-service-NNNN-<name-in-kebab-case>.md` | Application behavior exposed to a consumer; not its implementation. |
| `Application Event` | `«event, application»` | `«concept, element, behavior»` | `Application Event NNNN <Name> «additional, explicit, stereotypes»` | `application-event-NNNN-<name-in-kebab-case>.md` | Instantaneous application occurrence or state change. |
| `Application Interface` | `«interface, application»` | `«concept, element, structure, active, external»` | `Application Interface NNNN <Name> «additional, explicit, stereotypes»` | `application-interface-NNNN-<name-in-kebab-case>.md` | Access point or contract exposing application services. `«plugin-api»` denotes a host-owned contract implemented by a plugin for host invocation. |
| `Application Component` | `«component, application»` | `«concept, element, structure, active, internal»` | `Application Component NNNN <Name> «additional, explicit, stereotypes»` | `application-component-NNNN-<name-in-kebab-case>.md` | Modular, replaceable application structure that performs behavior. `«plugin»` denotes an in-process extension composed by host System Software. |
| `Data Object` | `«object, data»` | `«concept, element, structure, passive, application»` | `Data Object NNNN <Name> «additional, explicit, stereotypes»` | `data-object-NNNN-<name-in-kebab-case>.md` | Logical data structure for automated processing; not a business concept or physical artifact. |

## Internal Relationships

| Relationship Stereotypes | From Connector Concept Stereotypes | To Connector Concept Stereotypes |
| --- | --- | --- |
| `«aggregation»`, `«composition»` | `«element, application»` | `«element, application, same-type»` |
| `«specialization»` | `«element, application»` | `«element, application, same-type»` |
| `«association»` | `«element, application»` | `«element, application»` |
| `«triggering»` | `«behavior, application»` | `«behavior, application»` |
| `«flow»` | `«behavior, application»` | `«behavior, application»` |
| `«access»` | `«behavior, application»` | `«structure, passive, application»` |
| `«access»` | `«component, application»` | `«object, data»` |
| `«assignment»` | `«interface, application»` | `«service, application»` |
| `«assignment»` | `«structure, active, internal, application»` | `«structure, passive, application»` |
| `«realization»` | `«behavior, internal, application»` | `«service, application»` |
| `«aggregation»`, `«composition»` | `«behavior, internal, application»` | `«behavior, internal, application»` |
| `«aggregation»`, `«composition»` | `«collaboration, application»` | `«structure, active, internal, application»` |
| `«serving»` | `«service, application»` | `«structure, active, application»`, `«behavior, internal, application»` |
| `«serving»` | `«interface, application»` | `«component, application»` |
| `«aggregation»`, `«composition»` | `«component, application»` | `«interface, application»` |
| `«realization»` | `«component, application, plugin»` | `«interface, application, plugin-api»` |
| `«assignment»` | `«component, application, plugin»` | `«process, application, plugin-call»` |

The plugin-specific rules express implementation of the host-owned hook contract
and responsibility for a plugin-controlled call. They do not make an ordinary
component realize any interface or assign it to arbitrary behavior. `«plugin»`
continues to denote an in-process hosted extension, not independent System Software.

## Relationships With Other Domains

| Relationship Stereotypes | From Connector Concept Stereotypes | To Connector Concept Stereotypes |
| --- | --- | --- |
| `«association»` | `«element, application»` | `«element»`, `«relationship»` |
| `«triggering»`, `«flow»` | `«behavior, application»` | `«behavior, strategy»`, `«behavior, business»`, `«behavior, technology»`, `«behavior, implementation-and-migration»` |
| `«triggering»`, `«flow»` | `«behavior, strategy»`, `«behavior, business»`, `«behavior, technology»`, `«behavior, implementation-and-migration»` | `«behavior, application»` |
| `«access»` | `«behavior, application»` | `«structure, passive, business»`, `«structure, passive, technology»` |
| `«access»` | `«behavior, business»`, `«behavior, technology»`, `«behavior, implementation-and-migration»` | `«structure, passive, application»` |
| `«realization»` | `«structure, active, application»` | `«path, technology»` |
| `«assignment»` | `«interface, application»` | `«service, business»`, `«service, technology»` |
| `«assignment»` | `«structure, active, internal, application»` | `«role, business»` |
| `«assignment»` | `«role, business»` | `«behavior, internal, application»`, `«event, application»` |
| `«realization»` | `«behavior, internal, application»` | `«service, business»`, `«service, technology»`, `«behavior, strategy»` |
| `«realization»` | `«behavior, internal, business»`, `«behavior, internal, technology»` | `«service, application»` |
| `«aggregation»`, `«composition»` | `«collaboration, application»` | `«structure, active, internal, business»`, `«structure, active, internal, technology»` |
| `«aggregation»`, `«composition»` | `«collaboration, business»`, `«collaboration, technology»` | `«structure, active, internal, application»` |
| `«serving»` | `«service, application»` | `«structure, active, business»`, `«structure, active, technology»`, `«behavior, internal, business»`, `«behavior, internal, technology»` |
| `«serving»` | `«service, business»`, `«service, technology»` | `«component, application»`, `«behavior, internal, application»` |
| `«realization»` | `«interface, application»` | `«interface, business»` |
| `«realization»` | `«interface, technology»` | `«interface, application»` |
| `«realization»` | `«object, data»` | `«object, business»` |
| `«realization»` | `«artifact»` | `«component, application»`, `«object, data»` |
| `«realization»` | `«structure, active, application»`, `«structure, passive, application»` | `«resource»` |
| `«realization»` | `«service, application»`, `«behavior, internal, application»` | `«behavior, strategy»` |
| `«realization»`, `«influence»` | `«structure, active, application»`, `«structure, passive, application»`, `«behavior, internal, application»`, `«service, application»` | `«requirement»` |
| `«realization»` | `«work-package»`, `«deliverable»`, `«plateau»` | `«structure, active, application»`, `«structure, passive, application»`, `«behavior, internal, application»`, `«service, application»` |
| `«aggregation»`, `«composition»` | `«plateau»` | `«element, application»` |
| `«composition»` | `«system-software»` | `«component, application, plugin»`, `«interface, application, plugin-api»` |

For this local plugin convention, host composition records the plugin's in-process
hosting and the host's ownership of its hook interface. Interface ownership is
distinct from the plugin component's realization of that contract. The relationship
does not claim that source/runtime provenance or compatibility has been verified.
