# Metamodel Definitions

The local Metamodel uses globally unique stereotype names to represent concept
types, specialization, domain belonging, storage, and calculated validation
context. Every stereotype name has exactly one owning registered stereotype
system. Registration rejects a name already owned by another system; for example,
`business` belongs to the ArchiMate system and cannot be reused outside that
system. Parallel systems may define their own unique names without changing a
concept's identity.

Every concept is controlled through the target C# and TypeScript `IModelConcept`
interface. The interface exposes `StereotypeNames.Declared` and
`StereotypeNames.Runtime`. `StereotypeNames.Runtime` is the context-free
materialized closure of declared and implicit stereotypes. Relationship
validation calculates functional stereotypes separately from the concepts and
evaluation context; functional values do not participate in either array.

| Stereotype kind | Index meaning |
| --- | --- |
| Explicit | Declared directly on the concept and exposed through `StereotypeNames.Declared`. |
| Implicit | Guaranteed by the specialization hierarchy of an explicit stereotype and added to `StereotypeNames.Runtime` without repeated declaration. |
| Enumerated | Validated against a stereotype system's declared vocabulary; it does not use a separate persisted array. |
| Functional | Calculated only for relationship validation from the concepts and applicable evaluation context; it is not added to `StereotypeNames.Runtime`. |

`StereotypeNames.Declared` is the persisted array of explicitly declared
stereotype names. `StereotypeNames.Runtime` is the context-free materialized array
of declared and implicit stereotype names. Functional stereotypes are transient
relationship-validation inputs and are never persisted in either array.
Qualifiers such as `active`, `passive`, `internal`, and `external` are not
standalone types; they occur with the stereotype whose specialization they
qualify.

## Metamodel Recalculation

Every metamodel change triggers a total recalculation of all concepts.
`StereotypeNames.Declared` and `StereotypeNames.Runtime` are indexed as
comma-delimited text fields whose stereotype names are ordered alphabetically.
Recalculation:

1. Collects the distinct stored values from those indexes.
2. Attempts to detect each concept's current declared stereotypes and type from
   model evidence, with optional AI-context assistance.
3. Applies a detected stereotype or type only when the result is confident and
   preserves the concept's Element, Relationship, or Junction storage class.
4. Preserves uncertain values as-is, reports their validation errors, and keeps
   them available to AI context for later processing stages.
5. Calculates the concept's context-free `StereotypeNames.Runtime` array from its
   declared and implicit stereotypes.
6. Updates the concept when its recalculated arrays differ from the stored
   arrays.
7. Revalidates model consistency and updates the validation-error list.

Recalculation preserves concept identity and never changes a concept's storage
class. AI context does not clear or suppress an unresolved validation error.

## ArchiMate Concept Mapping

ArchiMate 4 defines a model as a collection of concepts and divides `Concept`
into `Element`, `Relationship`, and `Junction`. This profile maps every ArchiMate type
to one or more stereotypes. A stereotype for a specialization implies the
stereotypes of its generalizations, so `«element»` means `«concept, element»`
without requiring `concept` to be repeated in storage.

The class names below are target, language-neutral names for matching C# and
TypeScript implementations. `ModelElement`, `ModelRelationship`, and
`ModelJunction` each implement `IModelConcept`; they are separate storage classes
because their graph responsibilities differ. This mapping is implicit in every
reference table that follows and is not repeated there.

The hierarchy is informed by the Language Structure, Common, Motivation,
Strategy, Business, Application, Technology, and Implementation and Migration
sections of the [ArchiMate 4 reference](https://pubs.opengroup.org/architecture/archimate4-doc/)
reference chapters.

### Concept Contract

| ArchiMate 4 Type | Stereotype | C#/TypeScript interface |
| --- | --- | --- |
| `Concept` | `«concept»` | `IModelConcept` |

### Concept Specializations

The `«concept»` stereotype is implicit in each direct specialization and is
available when a caller asks for the effective stereotypes.

| ArchiMate 4 Type | Stereotype | Implicit Stereotypes | C#/TypeScript class |
| --- | --- | --- | --- |
| `Element` | `«element»` | `«concept»` | `ModelElement` |
| `Relationship` | `«relationship»` | `«concept»` | `ModelRelationship` |
| `Junction` | `«junction»` | `«concept»` | `ModelJunction` |

Import requires an unambiguous source storage class: `ModelElement`,
`ModelRelationship`, or `ModelJunction`. If that class cannot be determined, the
concept is not imported. Import never requalifies a concept between Element,
Relationship, and Junction. Once its storage class is known, the concept and its
declared stereotypes are preserved as-is. Validation is soft: every validation
error is reported without changing or discarding the imported concept, using the
same treatment as a legacy element.

### Element Type Hierarchy

The tables in this section contain every element type connected by a
specialization edge in the updated ArchiMate 4 reference diagrams, followed by
the domain-qualified Common forms defined by the local Common Domain pairing.
`Element` is repeated from the top-level concept table so this inventory is
complete.

Explicit stereotype proposals use the element's distinguishing noun first and
add domain or aspect qualifiers after it. Hyphenated values preserve an
indivisible multi-word type. Implicit stereotypes are the transitive ancestor
closure and are calculated rather than redundantly stored.

Each ArchiMate domain separates concrete `Model Elements`, which can be placed in
a model, from abstract `Hierarchy Groupings`, which classify specializations but
cannot be placed in a model directly. `Hierarchy Groupings` must not be confused
with the concrete Common Domain `Grouping` element.

#### Language-Wide Hierarchy

##### Hierarchy Groupings

| ArchiMate 4 Type | Explicit Stereotypes | Implicit Stereotypes |
| --- | --- | --- |
| `Element` | `«element»` | `«concept»` |
| `Structure Element` | `«structure»` | `«concept, element»` |
| `Active Structure Element` | `«structure, active»` | `«concept, element»` |
| `External Active Structure Element` | `«structure, active, external»` | `«concept, element»` |
| `Internal Active Structure Element` | `«structure, active, internal»` | `«concept, element»` |
| `Passive Structure Element` | `«structure, passive»` | `«concept, element»` |
| `Behavior Element` | `«behavior»` | `«concept, element»` |
| `Internal Behavior Element` | `«behavior, internal»` | `«concept, element»` |
| `Composite Element` | `«composite»` | `«concept, element»` |

#### Common Domain

##### Model Elements

| ArchiMate 4 Type | Explicit Stereotypes | Local Domain Stereotype Requirement | Available Domain Stereotypes From Refs | Implicit Stereotypes |
| --- | --- | --- | --- | --- |
| `Interface` | `«interface»` | Required | `«business»`, `«application»`, `«technology»` | `«concept, element, structure, active, external»` |
| `Path` | `«path»` | Required | `«technology»` | `«concept, element, structure, active»` |
| `Collaboration` | `«collaboration»` | Required | `«business»`, `«application»`, `«technology»` | `«concept, element, structure, active, internal»` |
| `Role` | `«role»` | Required | `«business»` | `«concept, element, structure, active, internal»` |
| `Service` | `«service»` | Required | `«business»`, `«application»`, `«technology»` | `«concept, element, behavior»` |
| `Event` | `«event»` | Required | `«business»`, `«application»`, `«technology»`, `«implementation-and-migration»` | `«concept, element, behavior»` |
| `Process` | `«process»` | Required | `«business»`, `«application»`, `«technology»` | `«concept, element, behavior, internal»` |
| `Function` | `«function»` | Required | `«business»`, `«application»`, `«technology»` | `«concept, element, behavior, internal»` |
| `Grouping` | `«grouping»` | Not applicable | None | `«concept, element, composite»` |
| `Location` | `«location»` | Not applicable | None | `«concept, element, composite»` |

ArchiMate 4 defines these as Common elements. This profile requires an explicit domain
stereotype for every Common element whose availability is listed above. The
domain-qualified names in the Language Customization Mechanisms section of the
[ArchiMate 4 reference](https://pubs.opengroup.org/architecture/archimate4-doc/)
are informative specialization profiles, but they provide the reference set for
Collaboration, Role, Service, Event, Process, and Function.

Path is the explicit exception to profile-name evidence. ArchiMate 4 moved Path
to the Common Domain, while the Technology Domain of the
[ArchiMate 4 reference](https://pubs.opengroup.org/architecture/archimate4-doc/)
uses it to connect technology structures and the single-domain Technology
Viewpoint includes it. This profile therefore requires `«technology»` on `«path»` and
derives `Technology Path`. It does not infer Business Path or Application Path.
Grouping and Location do not accept domain stereotypes, and no Strategy or
Motivation domain-qualified Common form is available.

The updated Common specialization diagram contains generic `Interface`, but the
Common summary does not define it as a concrete Common element. It is retained in
this table as the shared mapping for the concrete Business Interface, Application
Interface, and Technology Interface types in their owning domain tables.

#### Motivation Domain

##### Model Elements

| ArchiMate 4 Type | Explicit Stereotypes | Implicit Stereotypes |
| --- | --- | --- |
| `Meaning` | `«meaning»` | `«concept, element, motivation»` |
| `Value` | `«value»` | `«concept, element, motivation»` |
| `Stakeholder` | `«stakeholder»` | `«concept, element, motivation»` |
| `Driver` | `«driver»` | `«concept, element, motivation»` |
| `Assessment` | `«assessment»` | `«concept, element, motivation»` |
| `Goal` | `«goal»` | `«concept, element, motivation»` |
| `Outcome` | `«outcome»` | `«concept, element, motivation»` |
| `Principle` | `«principle»` | `«concept, element, motivation»` |
| `Requirement` | `«requirement»` | `«concept, element, motivation»` |

##### Hierarchy Groupings

| ArchiMate 4 Type | Explicit Stereotypes | Implicit Stereotypes |
| --- | --- | --- |
| `Motivation Element` | `«motivation»` | `«concept, element»` |

#### Strategy Domain

##### Model Elements

| ArchiMate 4 Type | Explicit Stereotypes | Implicit Stereotypes |
| --- | --- | --- |
| `Resource` | `«resource»` | `«concept, element, structure, strategy»` |
| `Capability` | `«capability»` | `«concept, element, behavior, strategy»` |
| `Course of Action` | `«course-of-action»` | `«concept, element, behavior, strategy»` |
| `Value Stream` | `«value-stream»` | `«concept, element, behavior, strategy»` |

##### Hierarchy Groupings

| ArchiMate 4 Type | Explicit Stereotypes | Implicit Stereotypes |
| --- | --- | --- |
| `Strategy Behavior Element` | `«behavior, strategy»` | `«concept, element»` |

#### Business Domain

##### Model Elements

| ArchiMate 4 Type | Explicit Stereotypes | Implicit Stereotypes |
| --- | --- | --- |
| `Business Role` | `«role, business»` | `«concept, element, structure, active, internal»` |
| `Business Collaboration` | `«collaboration, business»` | `«concept, element, structure, active, internal»` |
| `Business Process` | `«process, business»` | `«concept, element, behavior, internal»` |
| `Business Function` | `«function, business»` | `«concept, element, behavior, internal»` |
| `Business Service` | `«service, business»` | `«concept, element, behavior»` |
| `Business Event` | `«event, business»` | `«concept, element, behavior»` |
| `Business Interface` | `«interface, business»` | `«concept, element, structure, active, external»` |
| `Business Actor` | `«actor, business»` | `«concept, element, structure, active, internal»` |
| `Business Object` | `«object, business»` | `«concept, element, structure, passive»` |
| `Product` | `«product»` | `«concept, element, composite, business»` |

#### Application Domain

##### Model Elements

| ArchiMate 4 Type | Explicit Stereotypes | Implicit Stereotypes |
| --- | --- | --- |
| `Application Collaboration` | `«collaboration, application»` | `«concept, element, structure, active, internal»` |
| `Application Process` | `«process, application»` | `«concept, element, behavior, internal»` |
| `Application Function` | `«function, application»` | `«concept, element, behavior, internal»` |
| `Application Service` | `«service, application»` | `«concept, element, behavior»` |
| `Application Event` | `«event, application»` | `«concept, element, behavior»` |
| `Application Interface` | `«interface, application»` | `«concept, element, structure, active, external»` |
| `Application Component` | `«component, application»` | `«concept, element, structure, active, internal»` |
| `Data Object` | `«object, data»` | `«concept, element, structure, passive, application»` |

#### Technology Domain

##### Model Elements

| ArchiMate 4 Type | Explicit Stereotypes | Implicit Stereotypes |
| --- | --- | --- |
| `Technology Collaboration` | `«collaboration, technology»` | `«concept, element, structure, active, internal»` |
| `Technology Path` | `«path, technology»` | `«concept, element, structure, active»` |
| `Technology Process` | `«process, technology»` | `«concept, element, behavior, internal»` |
| `Technology Function` | `«function, technology»` | `«concept, element, behavior, internal»` |
| `Technology Service` | `«service, technology»` | `«concept, element, behavior»` |
| `Technology Event` | `«event, technology»` | `«concept, element, behavior»` |
| `Technology Interface` | `«interface, technology»` | `«concept, element, structure, active, external»` |
| `Node` | `«node»` | `«concept, element, structure, active, internal, technology»` |
| `Device` | `«device»` | `«concept, element, structure, active, internal, technology»` |
| `System Software` | `«system-software»` | `«concept, element, structure, active, internal, technology»` |
| `Facility` | `«facility»` | `«concept, element, structure, active, internal, technology»` |
| `Equipment` | `«equipment»` | `«concept, element, structure, active, internal, technology»` |
| `Communication Network` | `«network, communication»` | `«concept, element, structure, active, technology»` |
| `Distribution Network` | `«network, distribution»` | `«concept, element, structure, active, technology»` |
| `Artifact` | `«artifact»` | `«concept, element, structure, passive, technology»` |
| `Material` | `«material»` | `«concept, element, structure, passive, technology»` |

##### Hierarchy Groupings

| ArchiMate 4 Type | Explicit Stereotypes | Implicit Stereotypes |
| --- | --- | --- |
| `Technology Active Structure Element` | `«structure, active, technology»` | `«concept, element»` |
| `Technology Internal Active Structure Element` | `«structure, active, internal, technology»` | `«concept, element»` |
| `Technology Passive Structure Element` | `«structure, passive, technology»` | `«concept, element»` |

#### Implementation and Migration Domain

##### Model Elements

| ArchiMate 4 Type | Explicit Stereotypes | Implicit Stereotypes |
| --- | --- | --- |
| `Work Package` | `«work-package»` | `«concept, element, behavior, implementation-and-migration»` |
| `Deliverable` | `«deliverable»` | `«concept, element, structure, passive, implementation-and-migration»` |
| `Plateau` | `«plateau»` | `«concept, element, composite, implementation-and-migration»` |
| `Implementation Event` | `«event, implementation-and-migration»` | `«concept, element, behavior»` |

The updated Common diagram draws `Active Structure Element` and `Passive
Structure Element` directly under `Element`, while the language-structure diagram
places both under `Structure Element`. The table uses the language-structure
hierarchy because it defines the transitive structure specialization. `Interface`
is retained because the Common specialization diagram contains it, even though
the Common summary table does not list it separately.

`Strategy Structure Element`, `Core Structure Element`, and `Core Behavior
Element` occur as grouping labels in relationship diagrams but have no
specialization edge in the updated references, so they are not added as element
types. The domain-qualified Common rows are derived forms rather than additional
specialization nodes. `Constraint` and `Gap` are also absent from the updated
ArchiMate 4 specialization hierarchy. Existing Constraint records remain legacy
or local model types until an explicit migration decision is applied. Existing
Gap records have been migrated to the Assessment specialization below; Gap is not
represented as an ArchiMate 4 row in this table.

### Local Element Specializations

The Tenant system's `tenant` qualifier applies only to Locations declared as
`«location, tenant»`, retaining the existing Common Location type and hierarchy.
See [Tenant Location Profile](Metamodel%20for%20Common.md#tenant-location-profile).
It introduces no specialization edge and changes no other concept's closure.

This profile may specialize an ArchiMate 4 element with a generic local stereotype.
The local stereotype is explicit; its ArchiMate type and hierarchy are implicit.

| Local form | Explicit Stereotypes | Implicit Stereotypes |
| --- | --- | --- |
| `Assessment <Name> «gap»` | `«gap»` | `«concept, element, motivation, assessment»` |

`«gap»` identifies an assessment of a known deficiency, limitation, or
intentional inaccuracy that the adopting project accepts for later refinement or resolution. It
does not assert that a target state, solution, or Work Package is already known.
The canonical ArchiMate 4 element type remains `Assessment`; therefore gap
articles use an `Assessment` heading and `assessment-` filename.

### Relationship Hierarchy

| ArchiMate 4 Type | Stereotype | Implicit Stereotypes |
| --- | --- | --- |
| `Structural Relationship` | `«structural»` | `«concept, relationship»` |
| `Aggregation` | `«aggregation»` | `«concept, relationship, structural»` |
| `Composition` | `«composition»` | `«concept, relationship, structural, aggregation»` |
| `Assignment` | `«assignment»` | `«concept, relationship, structural»` |
| `Realization` | `«realization»` | `«concept, relationship, structural»` |
| `Dependency Relationship` | `«dependency»` | `«concept, relationship»` |
| `Association` | `«association»` | `«concept, relationship, dependency»` |
| `Influence` | `«influence»` | `«concept, relationship, dependency»` |
| `Access` | `«access»` | `«concept, relationship, dependency»` |
| `Serving` | `«serving»` | `«concept, relationship, dependency»` |
| `Dynamic Relationship` | `«dynamic»` | `«concept, relationship»` |
| `Triggering` | `«triggering»` | `«concept, relationship, dynamic»` |
| `Flow` | `«flow»` | `«concept, relationship, dynamic»` |
| `Other Relationship` | `«other»` | `«concept, relationship»` |
| `Specialization` | `«specialization»` | `«concept, relationship, other»` |

### Junction Hierarchy

| Junction Type | Required Declared Stereotypes | Runtime Closure |
| --- | --- | --- |
| `And-Junction` | `«and, junction, <propagated relationship stereotypes from every system>»` | `«concept, and, junction, <propagated relationship stereotype closures from every system with relationship replaced>»` |
| `Or-Junction` | `«or, junction, <propagated relationship stereotypes from every system>»` | `«concept, or, junction, <propagated relationship stereotype closures from every system with relationship replaced>»` |

Every relationship incident to one Junction must have the same complete
context-free non-functional relationship stereotype stack. When a relationship
has a Junction endpoint, propagate every declared relationship stereotype from
every registered system into that Junction's `StereotypeNames.Declared`. The
Junction also declares `junction` and its `and` or `or` selector. For example, a
Realization relationship produces `«and, junction, realization»` or
`«or, junction, realization»` on the Junction.

Continue propagation across relationship and Junction endpoints until an Element
endpoint is reached. Do not modify the Element declaration. Calculate the
Junction's runtime closure from every propagated stereotype hierarchy, substituting
`junction` for the ArchiMate `relationship` root. Functional stereotypes do not
propagate. No other join, split, branch-cardinality, exclusivity, one-to-one,
execution, or derivation rule applies. Richer combination semantics remain
non-executable textual description.

Validate Elements before Relationships. An inconsistent Element exposes its
validation errors on itself, and validation does not select an arbitrary effective
concrete type. Do not run relationship validation until every endpoint Element is
consistent. Therefore `«same-type»`, connector eligibility, and functional
stereotypes are not evaluated for a relationship with an inconsistent endpoint
Element.

### Domain Connector Eligibility

These tables define direct connector eligibility from the ArchiMate 4 domain
metamodel figures and the language-wide relationship rules. They do not enumerate
indirect relationships produced by relationship derivation. A connector concept
is matched against its effective stereotype set, including implicit stereotypes.

Within a connector cell, every stereotype inside one `«...»` expression is
required. Separate expressions are alternatives. For example,
`«structure, active, internal», «behavior, internal»` means that the connector
must be either an internal active structure element or an internal behavior
element. Multiple relationship expressions in one cell are alternatives in the
same way.

`«same-type»` is a functional connector stereotype evaluated relative to the
opposite endpoint. It is present only when both endpoints have the same most
specific ArchiMate element type. This preserves the language-wide same-type rule
without incorrectly allowing every pair of elements in a domain. Association is
eligible between any two elements and between an element and a relationship; an
association may be directed or undirected. In the external tables, its endpoint
order is interchangeable. Composition has exactly the same endpoint eligibility
as aggregation, so both appear together.

The internal table for a domain requires both endpoints to belong to that domain.
The external table requires one endpoint to belong to the named domain and the
other endpoint to belong to another domain or concept branch. Common relationship
families are inherited by the domain-qualified Common forms in Business,
Application, Technology, and Implementation and Migration.

#### Common Domain

The Common Domain rules operate on the shared hierarchy. Domain-qualified forms
inherit these rules; `Grouping` and `Location` remain unqualified Common elements.
For Common only, `Internal Relationships` means relationships defined inside the
shared Common metamodel before its forms receive domain qualifiers. It is not
subject to the both-endpoints-in-one-domain condition above.

##### Internal Relationships

| Relationship Stereotypes | From Connector Concept Stereotypes | To Connector Concept Stereotypes |
| --- | --- | --- |
| `«aggregation»`, `«composition»` | `«element»` | `«element, same-type»` |
| `«specialization»` | `«element»` | `«element, same-type»` |
| `«association»` | `«element»` | `«element»` |
| `«triggering»` | `«behavior»` | `«behavior»` |
| `«flow»` | `«behavior»` | `«behavior»` |
| `«access»` | `«behavior»` | `«structure, passive»` |
| `«realization»` | `«structure, active»` | `«path»` |
| `«assignment»` | `«structure, active, external»` | `«service»` |
| `«assignment»` | `«structure, active, internal»` | `«role»` |
| `«realization»` | `«behavior, internal»` | `«service»` |
| `«aggregation»`, `«composition»` | `«behavior, internal»` | `«behavior, internal»` |
| `«association»` | `«path»` | `«structure, active, internal»` |
| `«aggregation»`, `«composition»` | `«collaboration»` | `«structure, active, internal»` |
| `«assignment»` | `«collaboration»` | `«behavior, internal»` |
| `«aggregation»`, `«composition»` | `«role»` | `«structure, active, external»` |
| `«assignment»` | `«role»` | `«behavior, internal»`, `«event»` |
| `«serving»` | `«interface»` | `«role»`, `«collaboration»` |
| `«serving»` | `«service»` | `«structure, active»`, `«behavior, internal»` |
| `«aggregation»`, `«composition»` | `«grouping»`, `«location»` | `«concept»` |

##### Relationships With Other Domains

| Relationship Stereotypes | From Connector Concept Stereotypes | To Connector Concept Stereotypes |
| --- | --- | --- |
| `«association»` | `«element»` | `«relationship»` |
| `«association»` | `«grouping»`, `«location»` | `«element»`, `«relationship»` |
| `«realization»` | `«location»` | `«resource»` |
| `«association»` | `«meaning»`, `«value»` | `«grouping»`, `«location»` |
| `«realization»`, `«influence»` | `«grouping»`, `«location»` | `«requirement»` |
| `«aggregation»`, `«composition»` | `«grouping»`, `«location»` | `«work-package»`, `«deliverable»` |

#### Motivation Domain

##### Internal Relationships

| Relationship Stereotypes | From Connector Concept Stereotypes | To Connector Concept Stereotypes |
| --- | --- | --- |
| `«aggregation»`, `«composition»` | `«element, motivation»` | `«element, motivation, same-type»` |
| `«specialization»` | `«element, motivation»` | `«element, motivation, same-type»` |
| `«association»` | `«element, motivation»` | `«element, motivation»` |
| `«influence»` | `«element, motivation»` | `«element, motivation»` |
| `«realization»` | `«outcome»` | `«goal»` |
| `«realization»` | `«principle»` | `«outcome»` |
| `«realization»` | `«requirement»` | `«principle»`, `«outcome»` |

##### Relationships With Other Domains

| Relationship Stereotypes | From Connector Concept Stereotypes | To Connector Concept Stereotypes |
| --- | --- | --- |
| `«association»` | `«element, motivation»` | `«element»`, `«relationship»` |
| `«association»` | `«meaning»`, `«value»` | `«concept»` |
| `«assignment»` | `«actor, business»` | `«stakeholder»` |
| `«realization»`, `«influence»` | `«structure, strategy»`, `«behavior, strategy»`, `«structure, active»`, `«structure, passive»`, `«behavior, internal»`, `«service»`, `«grouping»`, `«location»`, `«product»` | `«requirement»` |
| `«realization»`, `«influence»` | `«course-of-action»` | `«outcome»` |
| `«realization»`, `«influence»` | `«work-package»`, `«deliverable»` | `«requirement»` |
| `«aggregation»`, `«composition»` | `«plateau»` | `«requirement»`, `«goal»`, `«outcome»` |

#### Strategy Domain

##### Internal Relationships

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

##### Relationships With Other Domains

| Relationship Stereotypes | From Connector Concept Stereotypes | To Connector Concept Stereotypes |
| --- | --- | --- |
| `«association»` | `«element, strategy»` | `«element»`, `«relationship»` |
| `«realization»`, `«influence»` | `«resource»`, `«behavior, strategy»` | `«requirement»` |
| `«realization»`, `«influence»` | `«course-of-action»` | `«outcome»` |
| `«realization»` | `«product»`, `«location»`, `«structure, active»`, `«structure, passive»` | `«resource»` |
| `«realization»` | `«service»`, `«behavior, internal»` | `«behavior, strategy»` |
| `«realization»` | `«work-package»`, `«deliverable»`, `«plateau»` | `«structure, strategy»`, `«behavior, strategy»` |
| `«aggregation»`, `«composition»` | `«plateau»` | `«structure, strategy»`, `«behavior, strategy»` |

#### Business Domain

##### Internal Relationships

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

##### Relationships With Other Domains

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

#### Application Domain

##### Internal Relationships

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

##### Relationships With Other Domains

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

#### Technology Domain

ArchiMate 4 includes information technology and operational/physical technology
in this one domain.

##### Internal Relationships

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

##### Relationships With Other Domains

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

#### Implementation and Migration Domain

##### Internal Relationships

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

##### Relationships With Other Domains

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

### Functional Stereotypes

Functional stereotypes are evaluated from a source concept toward another
concept. Location Composition establishes origin scope for `«same-origin»` and
`«cross-origin»` evaluation:

- An Element may be composed by zero or one Location. No Element may be composed
  by more than one Location.
- Resolve an Element's origin by following Location Composition upward to the
  highest Location. An uncomposed Location is its own highest Location.
- Two distinct Elements are `«same-origin»` exactly when both resolve to the same
  highest Location. Otherwise, including when either has no Location Composition,
  they are `«cross-origin»`. The result is symmetric, and self-evaluation is
  `«same-origin»`.
- Relationships and Junctions do not receive origin classifications.
- Self-composition or a Location-composition cycle is a consistency error because
  no valid highest Location can be resolved. Relationship validation waits until
  the affected Elements are consistent.

Evaluation context supplies the model graph but does not override the resolved
highest Location. Gateway-selection rules remain a separate concern and do not
change origin identity or cardinality.

## Metamodel Articles

| Article | Defines |
| --- | --- |
| [Metamodel](Metamodel.md) | Common local model definition, storage, relationships, stereotypes, and evidence. |
| [Metamodel for Common](Metamodel%20for%20Common.md) | ArchiMate 4 Common Domain framework and valid domain-stereotype pairings. |
| [Metamodel for Stereotypes](Metamodel%20for%20Stereotypes.md) | local Common Domain, domain, and local intent stereotype syntax and validation. |
| [Metamodel for Strategy](Metamodel%20for%20Strategy.md) | Indexed local Strategy elements and connector rules. |
| [Metamodel for Business](Metamodel%20for%20Business.md) | Indexed local Business elements and connector rules. |
| [Metamodel for Application](Metamodel%20for%20Application.md) | Indexed local Application and Data Object elements and connector rules. |
| [Metamodel for Technology](Metamodel%20for%20Technology.md) | Indexed local information, operational, and physical Technology elements and connector rules. |
| [Metamodel for Kubernetes](Metamodel%20for%20Kubernetes.md) | Kubernetes stereotype system, namespace, resource, relationship, naming, and validation rules. |
| [Metamodel for Git](Metamodel%20for%20Git.md) | Git, GitHub, GitLab, and Azure DevOps repository Artifact stereotypes and naming rules. |
| [Metamodel for AI](Metamodel%20for%20AI.md) | AI model, agent, tool, and context stereotype roles on existing ArchiMate concepts. |
| [Metamodel for Plugins](Metamodel%20for%20Plugins.md) | In-process plugin, host-owned API, call, and hook stereotype roles. |
| [Metamodel for Motivation](Metamodel%20for%20Motivation.md) | Indexed local Motivation elements, local Assessment specialization, and connector rules. |
| [Metamodel for Implementation and Migration](Metamodel%20for%20Implementation%20and%20Migration.md) | Indexed local Implementation and Migration elements and connector rules. |

## Refs

| Reference | Original source | Local use |
| --- | --- | --- |
| [ArchiMate 4 Specification download](https://pubs.opengroup.org/architecture/archimate4-doc/) | https://pubs.opengroup.org/architecture/archimate4-doc/ | The Open Group standard remains separately copyrighted and governed by its own terms. No downloaded specification or figure is redistributed here; these operational definitions are independent local tailoring, not a conformance certification. |

## Intakes

| ID | Reference contribution | Local use | Canonical intake |
| --- | --- | --- | --- |
| I1 | ArchiMate 4 Common Domain, core concepts, and relationships. | local common model definition, Common Domain element mappings, relationship recording, stereotypes, evidence, and compatibility boundary. | [Metamodel](Metamodel.md), [Metamodel for Common](Metamodel%20for%20Common.md), [Metamodel for Stereotypes](Metamodel%20for%20Stereotypes.md) |
| I2 | ArchiMate 4 Motivation and Strategy Domains. | Indexed local Motivation and Strategy vocabularies and connector rules. | [Metamodel for Motivation](Metamodel%20for%20Motivation.md), [Metamodel for Strategy](Metamodel%20for%20Strategy.md) |
| I3 | ArchiMate 4 Business and Application Domains. | Indexed local Business and Application vocabularies and connector rules. | [Metamodel for Business](Metamodel%20for%20Business.md), [Metamodel for Application](Metamodel%20for%20Application.md) |
| I4 | ArchiMate 4 Technology Domain. | Indexed local Technology vocabulary and connector rules, including operational and physical concepts. | [Metamodel for Technology](Metamodel%20for%20Technology.md) |
| I5 | ArchiMate 4 Implementation and Migration Domain and language customization. | Indexed local Implementation and Migration vocabulary, connector rules, and bounded local intent stereotypes. | [Metamodel for Implementation and Migration](Metamodel%20for%20Implementation%20and%20Migration.md), [Metamodel for Stereotypes](Metamodel%20for%20Stereotypes.md) |

## Domain Declaration

Each active domain metamodel begins by stating:

> The ArchiMate 4 `<Domain>` Domain is the reference framework for this local
> `<Domain>` domain definition. This profile specifies only the element types currently
> used or explicitly required in this domain.
