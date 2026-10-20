# Metamodel for Common

The ArchiMate 4 Common Domain is the reference framework for this local Common
domain definition. This profile specifies only the element types currently used or
explicitly required in this domain. Common defines unqualified Common elements
and validates the belonging-domain pairings used by Business, Application,
Technology, and Implementation and Migration. This article is the operational
definition; the external reference is provenance only.

## Elements

Common owns only elements that do not require a belonging-domain stereotype.
Select an element from the distinguishing definition in this table. Its title and
filename use the forms shown in that row. `NNNN` is unique within an independent
four-digit sequence for that displayed local element type. Convert the element
name to lowercase kebab case for the filename. Include guillemets only when the
element has additional explicit stereotypes.

| Element | Explicit Stereotypes | Implicit Stereotypes | Title | Filename | Definition |
| --- | --- | --- | --- | --- | --- |
| `Grouping` | `«grouping»` | `«concept, element, composite»` | `Grouping NNNN <Name> «additional, explicit, stereotypes»` | `grouping-NNNN-<name-in-kebab-case>.md` | Concrete collection whose concepts share a characteristic; not an abstract hierarchy grouping. |
| `Location` | `«location»` | `«concept, element, composite»` | `Location NNNN <Name> «additional, explicit, stereotypes»` | `location-NNNN-<name-in-kebab-case>.md` | Physical or logical place where structure resides or behavior occurs. |

When a Grouping has a Kubernetes high-order explicit stereotype, place that
stereotype after the Grouping sequence and before the normalized name, for
example `grouping-NNNN-k8s-namespace-slug.md`. See
[Metamodel for Kubernetes](Metamodel%20for%20Kubernetes.md) for the profile
rules.

## Mermaid Diagram Projection

When a diagram draws its current Grouping element, project that Grouping as a
Mermaid `subgraph`, not as a standalone node. Place every element aggregated by
the current Grouping inside that subgraph. The Grouping's relationship table
remains the authoritative aggregation record; visual containment projects those
aggregation relationships. A Grouping that appears only as an aggregated element
in another Grouping's diagram may use its normal element shape.

## Location Origin Scope

### Tenant Location Profile

A tenant is represented by a Location with the additional explicit `«tenant»`
stereotype. The Tenant stereotype system owns the globally unique name `tenant`.
The profile requires `«location, tenant»`; `tenant` is a qualifier, not a domain
stereotype or a separate concrete element type. It adds no stereotype ancestors,
so the runtime hierarchy remains `«concept, element, composite, location, tenant»`.
Only Location elements may declare `tenant`.

Use the normal Location sequence and filename, with heading
`Location NNNN <Name> «tenant»`. Existing Location identity, ownership, and origin
relationships are preserved when the qualifier is added. A tenant Location
represents the tenant authority boundary, not a tariff, account, DNS domain,
Kubernetes namespace, or developer-access grant.

The adopting model identifies its tenant Locations explicitly. DNS and repository
child Locations are not automatically additional tenants.

### Origin Rules

An Element may be composed by zero or one Location; no Element may be composed by
more than one. Resolve an available Location Composition chain to the highest
Location; an uncomposed Location is its own highest Location. Two distinct
Elements are `«same-origin»` exactly when both resolve to the same highest
Location. Otherwise, including when either has no Location Composition, they are
`«cross-origin»`; the result is symmetric. Self-evaluation is `«same-origin»`.
Relationships and Junctions have no origin classification. Self-composition and
Location-composition cycles are consistency errors. No immediate
Location-composition migration is required.

## Valid Domain Pairings

|  | `«business»` | `«application»` | `«technology»` | `«implementation-and-migration»` |
| --- | --- | --- | --- | --- |
| `«interface»` | `Business Interface` | `Application Interface` | `Technology Interface` | None |
| `«role»` | `Business Role` | None | None | None |
| `«collaboration»` | `Business Collaboration` | `Application Collaboration` | `Technology Collaboration` | None |
| `«path»` | None | None | `Technology Path` | None |
| `«process»` | `Business Process` | `Application Process` | `Technology Process` | None |
| `«function»` | `Business Function` | `Application Function` | `Technology Function` | None |
| `«service»` | `Business Service` | `Application Service` | `Technology Service` | None |
| `«event»` | `Business Event` | `Application Event` | `Technology Event` | `Implementation Event` |

The matrix validates stereotype compatibility only. It does not define the
domain-qualified elements. Each valid form is completely defined by its owning
domain article, including explicit and implicit stereotypes, title, filename,
and distinguishing definition. A missing pairing is invalid and is not inferred.

## Internal Relationships

These shared rules are defined by Common before its forms receive domain
qualifiers.

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

## Relationships With Other Domains

| Relationship Stereotypes | From Connector Concept Stereotypes | To Connector Concept Stereotypes |
| --- | --- | --- |
| `«association»` | `«element»` | `«relationship»` |
| `«association»` | `«grouping»`, `«location»` | `«element»`, `«relationship»` |
| `«realization»` | `«location»` | `«resource»` |
| `«association»` | `«meaning»`, `«value»` | `«grouping»`, `«location»` |
| `«realization»`, `«influence»` | `«grouping»`, `«location»` | `«requirement»` |
| `«aggregation»`, `«composition»` | `«grouping»`, `«location»` | `«work-package»`, `«deliverable»` |
