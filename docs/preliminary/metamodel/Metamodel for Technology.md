# Metamodel for Technology

The ArchiMate 4 Technology Domain is the reference framework for this local
Technology domain definition. This profile specifies only the element types currently
used or explicitly required in this domain. Technology includes information
technology and operational/physical technology structure, behavior, interfaces,
networks, and passive items. This article is the operational definition; the
external reference is provenance only.

## Elements

Select an element from the distinguishing definition in this table. Its title and
filename use the forms shown in that row. `NNNN` is unique within an independent
four-digit sequence for that displayed local element type. Convert the element
name to lowercase kebab case for the filename. Include guillemets only when the
element has additional explicit stereotypes.

| Element | Explicit Stereotypes | Implicit Stereotypes | Title | Filename | Definition |
| --- | --- | --- | --- | --- | --- |
| `Technology Collaboration` | `«collaboration, technology»` | `«concept, element, structure, active, internal»` | `Technology Collaboration NNNN <Name> «additional, explicit, stereotypes»` | `technology-collaboration-NNNN-<name-in-kebab-case>.md` | Technology structures acting collectively; use Node for one hosting structure. |
| `Technology Path` | `«path, technology»` | `«concept, element, structure, active»` | `Technology Path NNNN <Name> «additional, explicit, stereotypes»` | `technology-path-NNNN-<name-in-kebab-case>.md` | Logical route carrying data, material, or energy; use a network for physical realization. |
| `Technology Process` | `«process, technology»` | `«concept, element, behavior, internal»` | `Technology Process NNNN <Name> «additional, explicit, stereotypes»` | `technology-process-NNNN-<name-in-kebab-case>.md` | Ordered technology behavior; use when sequence matters. `«plugin-hook»` denotes a host-controlled plugin invocation. |
| `Technology Function` | `«function, technology»` | `«concept, element, behavior, internal»` | `Technology Function NNNN <Name> «additional, explicit, stereotypes»` | `technology-function-NNNN-<name-in-kebab-case>.md` | Technology behavior grouped by responsibility, skill, or resource. |
| `Technology Service` | `«service, technology»` | `«concept, element, behavior»` | `Technology Service NNNN <Name> «additional, explicit, stereotypes»` | `technology-service-NNNN-<name-in-kebab-case>.md` | Technology behavior exposed to consumers; not its internal realization. |
| `Technology Event` | `«event, technology»` | `«concept, element, behavior»` | `Technology Event NNNN <Name> «additional, explicit, stereotypes»` | `technology-event-NNNN-<name-in-kebab-case>.md` | Instantaneous technology occurrence or state change. |
| `Technology Interface` | `«interface, technology»` | `«concept, element, structure, active, external»` | `Technology Interface NNNN <Name> «additional, explicit, stereotypes»` | `technology-interface-NNNN-<name-in-kebab-case>.md` | Access point exposing a Technology Service. `«plugin-api»` denotes a host-owned contract a plugin may call. |
| `Node` | `«node»` | `«concept, element, structure, active, internal, technology»` | `Node NNNN <Name> «additional, explicit, stereotypes»` | `node-NNNN-<name-in-kebab-case>.md` | Generic hosting or interacting structure combining technology constituents. |
| `Device` | `«device»` | `«concept, element, structure, active, internal, technology»` | `Device NNNN <Name> «additional, explicit, stereotypes»` | `device-NNNN-<name-in-kebab-case>.md` | Physical or virtualized computing hardware. |
| `System Software` | `«system-software»` | `«concept, element, structure, active, internal, technology»` | `System Software NNNN <Name> «additional, explicit, stereotypes»` | `system-software-NNNN-<name-in-kebab-case>.md` | Platform software that runs, stores, or supports deployed software or data. |
| `Facility` | `«facility»` | `«concept, element, structure, active, internal, technology»` | `Facility NNNN <Name> «additional, explicit, stereotypes»` | `facility-NNNN-<name-in-kebab-case>.md` | Physical setting housing or locating operations; not the machinery within it. |
| `Equipment` | `«equipment»` | `«concept, element, structure, active, internal, technology»` | `Equipment NNNN <Name> «additional, explicit, stereotypes»` | `equipment-NNNN-<name-in-kebab-case>.md` | Physical machinery, tool, instrument, or livestock performing work; not computing hardware. |
| `Communication Network` | `«network, communication»` | `«concept, element, structure, active, technology»` | `Communication Network NNNN <Name> «additional, explicit, stereotypes»` | `communication-network-NNNN-<name-in-kebab-case>.md` | Physical infrastructure transporting data. |
| `Distribution Network` | `«network, distribution»` | `«concept, element, structure, active, technology»` | `Distribution Network NNNN <Name> «additional, explicit, stereotypes»` | `distribution-network-NNNN-<name-in-kebab-case>.md` | Physical infrastructure transporting material or energy. |
| `Artifact` | `«artifact»` | `«concept, element, structure, passive, technology»` | `Artifact NNNN <Name> «additional, explicit, stereotypes»` | `artifact-NNNN-<name-in-kebab-case>.md` | Deployable or data-bearing IT item used in development, deployment, or operation. |
| `Material` | `«material»` | `«concept, element, structure, passive, technology»` | `Material NNNN <Name> «additional, explicit, stereotypes»` | `material-NNNN-<name-in-kebab-case>.md` | Tangible matter or energy that behavior stores, moves, consumes, or transforms. |

## Hierarchy Groupings

| Abstract Type | Explicit Stereotypes | Implicit Stereotypes | Definition |
| --- | --- | --- | --- |
| `Technology Active Structure Element` | `«structure, active, technology»` | `«concept, element»` | Technology subject capable of behavior, including internal structures and networks. |
| `Technology Internal Active Structure Element` | `«structure, active, internal, technology»` | `«concept, element»` | Technology performer excluding interfaces and non-internal networks. |
| `Technology Passive Structure Element` | `«structure, passive, technology»` | `«concept, element»` | Technology item acted upon; currently Artifact or Material. |

## Internal Relationships

| Relationship Stereotypes | From Connector Concept Stereotypes | To Connector Concept Stereotypes |
| --- | --- | --- |
| `«aggregation»`, `«composition»` | `«element, technology»` | `«element, technology, same-type»` |
| `«specialization»` | `«element, technology»` | `«element, technology, same-type»` |
| `«association»` | `«element, technology»` | `«element, technology»` |
| `«triggering»` | `«behavior, technology»` | `«behavior, technology»` |
| `«flow»` | `«behavior, technology»` | `«behavior, technology»` |
| `«access»` | `«behavior, technology»` | `«structure, passive, technology»` |
| `«access»` | `«equipment»` | `«material»` |
| `«realization»` | `«structure, active, technology»` | `«path, technology»` |
| `«assignment»` | `«interface, technology»` | `«service, technology»` |
| `«realization»` | `«behavior, internal, technology»` | `«service, technology»` |
| `«aggregation»`, `«composition»` | `«behavior, internal, technology»` | `«behavior, internal, technology»` |
| `«aggregation»`, `«composition»` | `«collaboration, technology»` | `«structure, active, internal, technology»` |
| `«serving»` | `«service, technology»` | `«structure, active, technology»`, `«behavior, internal, technology»` |
| `«serving»` | `«interface, technology»` | `«structure, active, technology»` |
| `«aggregation»`, `«composition»` | `«node»`, `«device»`, `«system-software»`, `«facility»`, `«equipment»` | `«interface, technology»` |
| `«aggregation»`, `«composition»` | `«node»` | `«system-software»`, `«device»`, `«equipment»`, `«facility»` |
| `«assignment»` | `«system-software»`, `«device»` | `«system-software»` |
| `«association»` | `«system-software»`, `«device»` | `«network, communication»` |
| `«aggregation»`, `«composition»` | `«network, communication»` | `«system-software»`, `«device»` |
| `«aggregation»`, `«composition»` | `«equipment»` | `«device»` |
| `«association»` | `«equipment»`, `«facility»` | `«network, distribution»` |
| `«aggregation»`, `«composition»` | `«facility»` | `«node»`, `«equipment»` |
| `«assignment»` | `«facility»` | `«node»`, `«equipment»` |
| `«aggregation»`, `«composition»` | `«network, distribution»` | `«equipment»`, `«facility»` |
| `«realization»` | `«artifact»` | `«system-software»`, `«device»` |
| `«realization»` | `«material»` | `«device»`, `«equipment»` |
| `«assignment»` | `«node»`, `«system-software»`, `«device»` | `«artifact»` |
| `«assignment»` | `«equipment»` | `«material»` |
| `«realization»` | `«network, communication»`, `«network, distribution»` | `«path, technology»` |
| `«serving»` | `«equipment»` | `«structure, active, technology»` |

## Relationships With Other Domains

| Relationship Stereotypes | From Connector Concept Stereotypes | To Connector Concept Stereotypes |
| --- | --- | --- |
| `«association»` | `«element, technology»` | `«element»`, `«relationship»` |
| `«triggering»`, `«flow»` | `«behavior, technology»` | `«behavior, strategy»`, `«behavior, business»`, `«behavior, application»`, `«behavior, implementation-and-migration»` |
| `«triggering»`, `«flow»` | `«behavior, strategy»`, `«behavior, business»`, `«behavior, application»`, `«behavior, implementation-and-migration»` | `«behavior, technology»` |
| `«access»` | `«behavior, technology»` | `«structure, passive, business»`, `«structure, passive, application»` |
| `«access»` | `«behavior, business»`, `«behavior, application»`, `«behavior, implementation-and-migration»` | `«structure, passive, technology»` |
| `«realization»` | `«structure, active, business»`, `«structure, active, application»` | `«path, technology»` |
| `«assignment»` | `«interface, technology»` | `«service, business»`, `«service, application»` |
| `«assignment»` | `«structure, active, internal, technology»` | `«role, business»` |
| `«assignment»` | `«role, business»` | `«behavior, internal, technology»`, `«event, technology»` |
| `«realization»` | `«behavior, internal, technology»` | `«service, business»`, `«service, application»`, `«behavior, strategy»` |
| `«realization»` | `«behavior, internal, business»`, `«behavior, internal, application»` | `«service, technology»` |
| `«aggregation»`, `«composition»` | `«collaboration, technology»` | `«structure, active, internal, business»`, `«structure, active, internal, application»` |
| `«serving»` | `«service, technology»` | `«structure, active, business»`, `«structure, active, application»`, `«behavior, internal, business»`, `«behavior, internal, application»` |
| `«serving»` | `«equipment»` | `«structure, active, business»`, `«structure, active, application»` |
| `«serving»` | `«service, business»`, `«service, application»` | `«structure, active, technology»`, `«behavior, internal, technology»` |
| `«realization»` | `«interface, technology»` | `«interface, application»` |
| `«assignment»` | `«facility»` | `«actor, business»` |
| `«association»`, `«aggregation»`, `«composition»` | `«network, distribution»` | `«actor, business»` |
| `«realization»` | `«artifact»` | `«component, application»`, `«object, data»` |
| `«realization»` | `«material»` | `«object, business»` |
| `«realization»` | `«structure, active, technology»`, `«structure, passive, technology»` | `«resource»` |
| `«realization»` | `«service, technology»`, `«behavior, internal, technology»` | `«behavior, strategy»` |
| `«realization»`, `«influence»` | `«structure, active, technology»`, `«structure, passive, technology»`, `«behavior, internal, technology»`, `«service, technology»` | `«requirement»` |
| `«realization»` | `«work-package»`, `«deliverable»`, `«plateau»` | `«structure, active, technology»`, `«structure, passive, technology»`, `«behavior, internal, technology»`, `«service, technology»` |
| `«aggregation»`, `«composition»` | `«plateau»` | `«element, technology»` |
| `«composition»` | `«system-software»` | `«component, application, plugin»`, `«interface, application, plugin-api»` |

The plugin-specific composition rule matches the Application metamodel's existing
hosted-plugin distinction: System Software hosts the in-process extension and
owns the Application hook interface it invokes. This local convention does not
compose arbitrary Application components/interfaces into a host or prove the
running plugin's provenance, loading, call behavior or compatibility.
