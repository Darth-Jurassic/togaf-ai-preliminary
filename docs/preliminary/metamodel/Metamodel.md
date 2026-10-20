# Metamodel

The local Metamodel is the operational vocabulary for building, storing,
validating, and reading local architecture. ArchiMate 4 is its reference
framework, but the definitions in this metamodel are sufficient to use the local
profile without consulting the external references.

The consolidated vocabulary is the [Metamodel Index](index.md). Shared element
pairings are defined in
[Metamodel for Common](Metamodel%20for%20Common.md), and declaration and validation
rules are defined in
[Metamodel for Stereotypes](Metamodel%20for%20Stereotypes.md). Domain selection and
connector rules are defined by the domain articles linked from the index.

## Concepts

| Concept Type | Explicit Stereotypes | Implicit Stereotypes | Definition |
| --- | --- | --- | --- |
| `Concept` | `«concept»` | None | Abstract root of every modeled thing. |
| `Element` | `«element»` | `«concept»` | Architectural thing with independent meaning; use a concrete element type. |
| `Relationship` | `«relationship»` | `«concept»` | Typed connector with one stored from concept and one stored to concept; Association may be undirected. |
| `Junction` | `«junction»` | `«concept»` | Connector that joins relationships of one type without creating new element meaning. |

`ModelElement`, `ModelRelationship`, and `ModelJunction` are separate storage
classes implementing the C# and TypeScript `IModelConcept` contract.

Import requires an unambiguous source storage class: `ModelElement`,
`ModelRelationship`, or `ModelJunction`. If that class cannot be determined, the
concept is not imported. Import never requalifies a concept between Element,
Relationship, and Junction. Once its storage class is known, the concept and its
declared stereotypes are preserved as-is. Validation is soft: every validation
error is reported without changing or discarding the imported concept, using the
same treatment as a legacy element.

## Hierarchy Groupings

Abstract stereotypes classify connector endpoints and cannot be instantiated
directly.

| Abstract Type | Explicit Stereotypes | Implicit Stereotypes | Definition |
| --- | --- | --- | --- |
| `Structure Element` | `«structure»` | `«concept, element»` | Entity that acts, exposes access, connects, or is acted upon. |
| `Active Structure Element` | `«structure, active»` | `«concept, element»` | Structure that performs behavior or provides access or a route. |
| `External Active Structure Element` | `«structure, active, external»` | `«concept, element»` | Boundary through which a provider exposes services. |
| `Internal Active Structure Element` | `«structure, active, internal»` | `«concept, element»` | Performer behind an exposed boundary. |
| `Passive Structure Element` | `«structure, passive»` | `«concept, element»` | Object or material acted upon; it performs no behavior. |
| `Behavior Element` | `«behavior»` | `«concept, element»` | Activity, occurrence, or exposed functionality. |
| `Internal Behavior Element` | `«behavior, internal»` | `«concept, element»` | Performed activity not exposed as a service. |
| `Composite Element` | `«composite»` | `«concept, element»` | Element that contains concepts across types or aspects. |

## Relationship Stereotypes

Use the smallest precise relationship. Abstract relationship categories classify
concrete stereotypes and cannot replace them when a concrete meaning is known.

| Relationship Type | Explicit Stereotypes | Implicit Stereotypes | Definition |
| --- | --- | --- | --- |
| `Structural Relationship` | `«structural»` | `«concept, relationship»` | Abstract static containment, allocation, or implementation link. |
| `Aggregation` | `«aggregation»` | `«concept, relationship, structural»` | Source whole collects target parts that can exist independently. |
| `Composition` | `«composition»` | `«concept, relationship, structural, aggregation»` | Source whole contains target parts whose existence depends on it. |
| `Assignment` | `«assignment»` | `«concept, relationship, structural»` | Source performs, fulfills, stores, or executes the target. |
| `Realization` | `«realization»` | `«concept, relationship, structural»` | Source is critical to creating, achieving, sustaining, or operating a more abstract target. |
| `Dependency Relationship` | `«dependency»` | `«concept, relationship»` | Abstract support, use, impact, or unspecified dependency; concrete subtype defines direction. |
| `Association` | `«association»` | `«concept, relationship, dependency»` | Relevant link for which no more precise relationship is justified. |
| `Influence` | `«influence»` | `«concept, relationship, dependency»` | Source changes achievement of a Motivation target without realizing it. |
| `Access` | `«access»` | `«concept, relationship, dependency»` | Source observes, creates, changes, or uses a passive target. |
| `Serving` | `«serving»` | `«concept, relationship, dependency»` | Source makes functionality available to the target. |
| `Dynamic Relationship` | `«dynamic»` | `«concept, relationship»` | Abstract precedence or transfer link. |
| `Triggering` | `«triggering»` | `«concept, relationship, dynamic»` | Source temporally or causally precedes target without asserting transfer. |
| `Flow` | `«flow»` | `«concept, relationship, dynamic»` | Something passes from source to target without asserting causation. |
| `Other Relationship` | `«other»` | `«concept, relationship»` | Abstract family for semantics outside the other relationship families. |
| `Specialization` | `«specialization»` | `«concept, relationship, other»` | Source is a narrower kind of the same-type target. |

Every relationship has a from-concept reference, a to-concept reference, a
concrete relationship stereotype, and any additional stereotypes. The file-first
identity is the normalized tuple of canonical from-concept reference, canonical
to-concept reference, sorted declared relationship stereotypes, and Association
direction. Directed relationships preserve endpoint order. An undirected
Association sorts its endpoint references before forming the tuple. Database and
API opaque identifiers are aliases and do not replace the normalized Markdown
tuple. Display wording does not define relationship identity or direction.

No relationship may connect two relationships. An element-to-relationship
connector must be Association, Aggregation, or Composition. Aggregation and
Composition are valid only from a composite element where a domain table permits
them.

## Validation Order

Validate Elements before Relationships. An inconsistent Element exposes its
validation errors on itself, and validation does not select an arbitrary effective
concrete type. Do not run relationship validation until every endpoint Element is
consistent. Therefore `«same-type»`, connector eligibility, and functional
stereotypes are not evaluated for a relationship with an inconsistent endpoint
Element.

## Connector Expressions

A connector is valid when its relationship and endpoint effective stereotypes
match one row in every applicable ArchiMate domain and registered stereotype
system table.

A domain's Internal Relationships table applies only when both endpoint elements
belong to that domain. Its Relationships With Other Domains table applies when
one endpoint belongs to the named domain and the other belongs to a different
domain or concept branch.

Common is the exception: its Internal Relationships table defines shared
hierarchy rules before Common forms receive domain qualifiers. Domain-qualified
Common forms inherit those rules. A cross-domain Association row has
interchangeable endpoint order, including when the Association is directed; its
stored direction remains independent of table presentation.

- Every stereotype inside one `«...»` expression is required.
- Separate expressions in a cell are alternatives.
- `«same-type»` is functional and matches only when both endpoints have the same
  most-specific ArchiMate element type. A local specialization such as `«gap»`
  does not change that ArchiMate type.
- `«same-origin»` and `«cross-origin»` are functional and are evaluated relative
  to the opposite endpoint and evaluation context.
- Composition has the same endpoint eligibility as Aggregation.
- Association is allowed between any two elements and between an element and a
  relationship; it may be directed or undirected.
- Stored local relationships must match a direct table row. Relationship
  derivation may produce a view but does not authorize an otherwise invalid
  stored connector.

## Junctions

| Junction Type | Required Declared Stereotypes | Runtime Closure | Definition |
| --- | --- | --- | --- |
| `And-Junction` | `«and, junction, <propagated relationship stereotypes from every system>»` | `«concept, and, junction, <propagated relationship stereotype closures from every system with relationship replaced>»` | AND selector carrying one propagated relationship stereotype family without executing branch semantics. |
| `Or-Junction` | `«or, junction, <propagated relationship stereotypes from every system>»` | `«concept, or, junction, <propagated relationship stereotype closures from every system with relationship replaced>»` | OR selector carrying one propagated relationship stereotype family without executing branch semantics. |

Every `ModelJunction` stores its identity, declared stereotypes, incoming and
outgoing relationship identities, and optional description. Every incident
relationship must have the same complete context-free non-functional
relationship stereotype stack. When a relationship has a Junction endpoint,
propagate every declared relationship stereotype from every registered system
into the Junction declaration together with `junction` and the Junction's `and`
or `or` selector. Continue propagation across relationships and Junctions until
an Element endpoint is reached; do not modify the Element declaration. Junction
runtime closure follows every propagated stereotype system's hierarchy,
substituting the `junction` root for the ArchiMate `relationship` root.
Functional stereotypes do not propagate. Code applies no additional join, split,
branch-cardinality, exclusivity, one-to-one, execution, or derivation rules.
Richer combination semantics remain non-executable description text.

## Origin Scope

Location Composition establishes origin scope for `«same-origin»` and
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

## Effective Stereotypes

- `StereotypeNames.Declared` contains the explicitly declared stereotype names
  and is the persistence source.
- `StereotypeNames.Runtime` is the context-free materialized array of declared and
  implicit stereotype names.
- Enumerated names are validated against their stereotype system; they do not use
  a separate persisted array.
- Relationship validation uses `StereotypeNames.Runtime` and separately
  calculates applicable functional stereotypes from the concepts and evaluation
  context.
- Functional stereotypes are validation inputs only. They are not added to or
  persisted in `StereotypeNames.Runtime`.
- A Junction declares every propagated non-functional relationship stereotype
  together with `junction` and `and` or `or`. Junction runtime closure follows
  each owning stereotype system's hierarchy and substitutes `junction` for the
  ArchiMate `relationship` root.

## Stereotype Systems And Projections

Every stereotype name belongs to exactly one registered stereotype system and is
globally unique across all systems. Registration rejects a name already owned by
another system. For example, `business` belongs to the ArchiMate system and cannot
be reused outside that system. Each system remains the authority for its own
vocabulary and specialization closure.

File, database, and API projections preserve the same concept identity, explicit
stereotypes, relationship endpoints and direction, junction stereotype and
description, and context-free `StereotypeNames.Runtime` array. Relationship
validation calculates functional stereotypes separately from the concepts and
evaluation context; projections do not persist those functional values.

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

## Element Article

```markdown
# Business Function NNNN Element Name «additional, explicit, stereotypes»

## Description

Short definition and architectural responsibility.

## Evidence

### Source

- Source reference.

### Target

- Implementation reference, when implemented.

## Relationships

| Stereotypes | From | To | Comment |
| --- | --- | --- | --- |
| `«relationship, additional stereotypes»` | Linked source concept | Linked target concept | Optional relationship explanation; state an Association's direction here when needed. |
```

Existing local `## Requirements` sections may remain as legacy content. Do not
add that section to a new element article or append a new requirement to an
existing legacy section. Represent every new requirement as a formal Requirement
element and trace a satisfying concept to it with `«realization»`.

## Junction Record

Every element article participating in a junction repeats the same junction row:

```markdown
## Junctions

| Junction Reference | Declared Stereotypes | Runtime Stereotypes | Incoming Relationship Tuples | Outgoing Relationship Tuples | Description |
| --- | --- | --- | --- | --- | --- |
| `junction-<UUID>` | `«and, junction, <propagated relationship stereotypes from every system>»` or `«or, junction, <propagated relationship stereotypes from every system>»` | Declared closure through every propagated stereotype hierarchy with `junction` substituted for the ArchiMate `relationship` root | Normalized relationship tuples | Normalized relationship tuples | Optional non-executable clarification or richer combination semantics. |
```

Every junction has a canonical `junction-<UUID>` Markdown reference independent
of its incident relationships. Relationship tuples use that reference for a
junction endpoint. Incoming and outgoing relationships, declared and runtime
stereotypes, and description are junction state, not junction identity. Database
and API identifiers are aliases and do not replace the canonical Markdown
reference. Incident relationships must have equal complete context-free
non-functional relationship stereotype stacks. Every declared non-functional
relationship stereotype propagates through Junction chains until an Element and
receives system-specific junction closure. Functional stereotypes are excluded.
Code preserves but does not interpret or enforce richer semantics in the
description.

The defining element and explicit belonging stereotypes determine the displayed
local element type and are not repeated after the name. Only additional explicit
stereotypes appear there; implicit, enumerated, and functional stereotypes do not.
Requirements Management uses formal Requirement elements. A concept that
satisfies a Requirement connects to it with a `«realization»` relationship.

## Storage And Naming

- Store one element article directly in its owning `docs/model/<domain>/` folder.
- Normalize the displayed type and element name to lowercase kebab case and
  insert the four-digit sequence between them:
  `<displayed-type-in-kebab-case>-NNNN-<name-in-kebab-case>.md`.
- Maintain an independent four-digit sequence for each displayed local element
  type. For example, Business Function and Application Function do not share a
  sequence.
- Store unqualified Grouping and Location articles in `docs/model/common/` and
  domain-qualified Common forms in their owning domain folders.
- Repeat the same normalized relationship tuple on every endpoint element
  article. When an endpoint is another relationship, refer to its normalized
  tuple rather than treating it as an element article.
- Keep Markdown as the source of truth; diagrams and catalogs are projections.

## Diagram Notation

Mermaid ArchiMate views label every concept with its ArchiMate type and use these
shapes. Colors continue to identify the concept's ArchiMate layer.

| Layer | Fill | Stroke | Text |
| --- | --- | --- | --- |
| Common | `#F5F5F5` | `#666666` | `#000000` |
| Motivation | `#F8CECC` | `#B85450` | `#000000` |
| Strategy | `#FFF2CC` | `#D6B656` | `#000000` |
| Business | `#FFE6CC` | `#D79B00` | `#000000` |
| Application | `#DAE8FC` | `#6C8EBF` | `#000000` |
| Technology | `#D5E8D4` | `#82B366` | `#000000` |
| Implementation and Migration | `#E1D5E7` | `#9673A6` | `#000000` |

| Concept class | Mermaid form | Shape |
| --- | --- | --- |
| Active structure | `id[Text]` | Full rectangle with sharp edges. |
| Behavior | `id(Text)` | Rounded edges. |
| Service | `id([Text])` | Rounded sides. |
| Event | `id>Text]` | Angled side. |
| Motivation | `id{{Text}}` | Cut edges. |
| Passive structure | `id@{ shape: notch-rect, label: "Text" }` | Notch rectangle. |

Render a Grouping as a Mermaid `subgraph` container. A Grouping takes the color
of the architecture layer it presents; it is not rendered as an active-structure
rectangle. A diagram may use a more specific shape only when the Metamodel
defines an explicit exception. Use the palette values in Mermaid `classDef` and
`style` statements; do not introduce undeclared layer colors in a diagram.

## Evidence And Integrity

- Source evidence identifies where a statement came from; target evidence
  identifies implementation or produced artifacts.
- Missing evidence makes a claim an expectation, not a current-state statement.
- Create an element only when it has independent meaning, responsibility,
  lifecycle, or governed relationships.
- A projection cannot introduce elements or relationships absent from canonical
  articles.
- Preserve unsupported existing types as legacy until an explicit migration is
  applied.
