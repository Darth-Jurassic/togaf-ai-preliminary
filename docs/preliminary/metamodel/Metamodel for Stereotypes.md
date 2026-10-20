# Metamodel for Stereotypes

This article defines local stereotype declaration, derivation, and validation.
The stereotype tables in the root, domain, and registered-profile metamodels are
the complete operational vocabulary.

## Stereotype Sets

| Kind | Meaning |
| --- | --- |
| Explicit | Declared directly on the concept and exposed through `StereotypeNames.Declared`. |
| Implicit | Guaranteed by an explicit stereotype's specialization or domain rule and added to `StereotypeNames.Runtime`. |
| Enumerated | Validated against a stereotype system's controlled vocabulary; it does not use a separate persisted array. |
| Functional | Calculated only for relationship validation from the concepts and evaluation context; it is not added to `StereotypeNames.Runtime`. |

`StereotypeNames.Declared` is the persisted array of explicitly declared
stereotype names. `StereotypeNames.Runtime` is the context-free materialized array
of declared and implicit stereotype names. Functional stereotypes are transient
relationship-validation inputs and are never persisted in either array. `active`,
`passive`, `internal`, and `external` qualify their hierarchy stereotype and do
not act as standalone types.

Every stereotype name has exactly one owning registered stereotype system.
Registration rejects a name already owned by another system. Globally unique
names preserve stereotype identity in `StereotypeNames.Declared` and
`StereotypeNames.Runtime` without a separate system identifier on each array
value.

Junction declaration propagation is the storage-class-aware closure exception. A
Junction declares every non-functional relationship stereotype propagated from
its incident relationships, across all registered stereotype systems, together
with `junction` and `and` or `or`. Its runtime closure follows each owning
system's stereotype ancestors and substitutes `junction` for the ArchiMate
`relationship` root. This does not create a second stereotype name or owner.

## Kubernetes Stereotypes

The Kubernetes stereotype system owns every lowercase kebab-case stereotype that
begins with `k8s-`. Its element, relationship, naming, and stack-validation
rules are defined in [Metamodel for Kubernetes](Metamodel%20for%20Kubernetes.md).

## AI Stereotypes

The AI stereotype system owns every lowercase kebab-case stereotype that begins
with `ai-`. Its AI model, agent, tool, and context roles are defined in
[Metamodel for AI](Metamodel%20for%20AI.md).

## Plugin Stereotypes

The Plugin stereotype system owns `plugin` and every lowercase kebab-case
stereotype beginning with `plugin-`. Its host, API, call, hook, relationship,
and validation rules are defined in
[Metamodel for Plugins](Metamodel%20for%20Plugins.md).

## Tenant Stereotypes

The Tenant stereotype system owns the exact lowercase name `tenant`. It qualifies
only a Location, requires the defining `location` stereotype, and adds no
hierarchy ancestors. Its rules are defined in
[Metamodel for Common](Metamodel%20for%20Common.md#tenant-location-profile).

## Local Element Types

The defining element and domain stereotypes derive the displayed local element
type. They do not repeat after the element name.

```text
# Business Role NNNN Element Name «additional, explicit, stereotypes»
# Technology Function NNNN Pipeline «additional, explicit, stereotypes»
# Capability NNNN Document Store «additional, explicit, stereotypes»
```

When a belonging-domain stereotype is explicit, put the domain first in the
displayed type and filename prefix. The domain metamodel must contain the complete
defining stereotype combination, title form, filename form, and definition.
Convert the displayed type to lowercase kebab case to derive its filename prefix.
Each displayed local element type has an independent four-digit sequence.

## Connector Matching

Inside a connector table cell, stereotypes in one `«...»` expression are a
conjunction and separate expressions are alternatives. For example,
`«a, b, c»`, `«d, e»` means either all of `a`, `b`, and `c`, or both `d` and `e`.

| Functional Stereotype | Meaning |
| --- | --- |
| `«same-type»` | Both endpoints have the same most-specific ArchiMate element type; a local specialization does not change it. |
| `«same-origin»` | Both endpoint Elements resolve to the same highest Location; self-evaluation is also same-origin. |
| `«cross-origin»` | Two distinct endpoint Elements do not both resolve to the same highest Location, including when either has no Location Composition. |

Location Composition defines `«same-origin»` and `«cross-origin»`. An Element may
have zero or one composing Location and never more than one. Follow an available
Composition chain to the highest Location; an uncomposed Location is its own
highest Location. Two distinct Elements are `«same-origin»` exactly when both
highest Locations exist and are the same. Otherwise, including when either
Element has no Location Composition, they are `«cross-origin»`; the result is
symmetric. Self-evaluation is `«same-origin»`. Relationships and Junctions have
no origin classification. Self-composition and Location-composition cycles are
consistency errors. Evaluation context does not override the highest Location. No
immediate migration is required, and gateway-selection rules remain separate from
origin identity and cardinality.

## Local Intent Stereotypes

| Stereotype | Meaning |
| --- | --- |
| `«abstract»` | Reusable template or pattern, not a concrete architecture instance. |
| `«add»` | Work Package relationship adds its target. |
| `«change»` | Work Package relationship changes its target. |
| `«remove»` | Work Package relationship removes its target. |
| `«out-of-scope»` | Concept is shown for context but excluded from current scope. |
| `«gap»` | Known deficiency, limitation, or intentional inaccuracy accepted for later refinement or resolution. |

`«add»`, `«change»`, and `«remove»` qualify a Work Package relationship, not the
affected element. `«gap»` specializes Assessment and implicitly carries
`«concept, element, motivation, assessment»`; it does not assert that a target
state, solution, or Work Package is already known.

## Validation

The validation rules below are soft for an imported concept whose source storage
class is unambiguous. Report every violation while preserving the concept's
storage class and declared stereotypes as-is, using the same treatment as a
legacy element. Never repair a violation by requalifying an Element as a
Relationship or Junction, or by requalifying either of those as another storage
class. A concept without a determinable source storage class is not imported.

During metamodel recalculation, model evidence and optional AI context may
identify a current stereotype or element type for legacy state. Apply that result
only when detection is confident and preserves the concept's Element,
Relationship, or Junction storage class. Otherwise preserve the legacy values
as-is, report their validation errors, and keep them available to AI context for
later processing stages. AI context never clears or suppresses an unresolved
validation error.

Validate Elements before Relationships. An inconsistent Element exposes its
validation errors on itself, and validation does not select an arbitrary effective
concrete type. Do not run relationship validation until every endpoint Element is
consistent. Therefore `«same-type»`, connector eligibility, and functional
stereotypes are not evaluated for a relationship with an inconsistent endpoint
Element.

- Match controlled stereotypes case-sensitively in lowercase kebab case.
- Reject an undeclared stereotype unless another registered stereotype system
  owns it.
- Reject a domain-qualified Common combination absent from the Common table.
- Reject a concrete article whose type is an abstract hierarchy stereotype.
- Validate relationships against effective endpoint stereotypes, not only stored
  explicit values.
- Keep status, evidence, requirements, and relationship direction outside the
  stereotype set.
