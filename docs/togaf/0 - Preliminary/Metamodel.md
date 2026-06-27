# Metamodel

This repository uses TOGAF ADM phases as the top-level architecture folders and ArchiMate 3.2 as the element vocabulary inside those folders.

## Source Notation Rule

Use the ArchiMate metamodel as the primary architecture modeling metamodel, but maintain active architecture content as Markdown documents instead of ArchiMate diagram files.

Markdown describes ArchiMate elements, relationships, rationale, and traceability in plain text. Mermaid diagrams may be embedded in Markdown when a visual view improves understanding, but the surrounding Markdown remains the source of truth for identifiers, rationale, and traceability.

Office documents and richer diagram files are source material or secondary views. They do not replace Markdown element articles as the evolving architecture source of truth.

## Placement Rule

Phase folders already contain architecture elements, so do not add an extra `elements/` directory level. Put each standalone ArchiMate element article directly under the ADM phase that owns that element type.

Do not add element-family folders under Phase A, Phase B, Phase D, Phase E, Phase F, Phase G, Phase H, or Requirements Management. Those folders are already bounded by TOGAF phase or ADM activity; motivation, strategy, business, technology, implementation/migration, planning, governance, and change management groupings are controlled by viewpoints and catalogs inside the markdown, not by extra filesystem levels.

Phase C is the exception: keep `application/` and `data/` folders because Phase C contains two distinct TOGAF subphases, Application Architecture and Data Architecture.

## Filename Rule

Preliminary phase working records may use their existing ADR and process-document
filenames without an ArchiMate element sequence number.

Outside Preliminary, standalone ArchiMate element articles must use this filename
pattern:

```text
<type-in-lowercase>-<NNNN>-<slug>.md
```

The type prefix is the ArchiMate element type in lowercase kebab case, for
example `principle`, `goal`, `application-component`, `data-object`,
`technology-process`, or `requirement`. The sequence number is zero-padded to
four digits and is scoped by element type in the owning phase folder, including
Phase C `application/` and `data/` subfolders. Intake records such as Phase H
`idea-###` and `risk-###` files are source records, not canonical ArchiMate
element articles, and may keep their source-record identifiers.

## Canonical Element Folders

| Folder | Canonical ArchiMate element types | Details |
| --- | --- | --- |
| `A - Architecture Vision/` | Stakeholder, Driver, Assessment, Goal, Outcome, Principle, Requirement, Constraint, Meaning, Value, Resource, Capability, Course of Action, Value Stream | [Metamodel for A](Metamodel%20for%20A.md) |
| `B - Business Architecture/` | Business Actor, Business Role, Business Collaboration, Business Interface, Business Process, Business Function, Business Interaction, Business Event, Business Service, Business Object, Contract, Representation, Product | [Metamodel for B](Metamodel%20for%20B.md) |
| `C - Information Systems Architecture/application/` | Application Component, Application Collaboration, Application Interface, Application Process, Application Function, Application Interaction, Application Event, Application Service | [Metamodel for C Application](Metamodel%20for%20C%20Application.md) |
| `C - Information Systems Architecture/data/` | Data Object | [Metamodel for C Data](Metamodel%20for%20C%20Data.md) |
| `D - Technology Architecture/` | Node, Device, System Software, Technology Collaboration, Technology Interface, Path, Communication Network, Technology Process, Technology Function, Technology Interaction, Technology Event, Technology Service, Artifact, Equipment, Facility, Distribution Network, Material | [Metamodel for D](Metamodel%20for%20D.md) |
| `E - Opportunities and Solutions/` | Work Package, Deliverable, Implementation Event, Plateau, Gap | [Metamodel for E](Metamodel%20for%20E.md) |
| `F - Migration Planning/` | Work Package, Deliverable, Implementation Event, Plateau, Gap, Requirement, Constraint | [Metamodel for F](Metamodel%20for%20F.md) |
| `G - Implementation Governance/` | Work Package, Deliverable, Implementation Event, Assessment, Requirement, Constraint, Plateau, Gap | [Metamodel for G](Metamodel%20for%20G.md) |
| `H - Architecture Change Management/` | Driver, Assessment, Goal, Outcome, Requirement, Constraint, Capability, Course of Action, Work Package, Plateau, Gap | [Metamodel for H](Metamodel%20for%20H.md) |
| `RM - Requirements Management/` | Requirement, Constraint | [Metamodel for RM](Metamodel%20for%20RM.md) |

Generic elements such as Grouping and Location may be used in any phase when they improve navigation or traceability. Prefer a phase-specific element type when one expresses the same idea more precisely.

## Link Rule

Element articles are the source of truth for architecture elements. Each model
element must have one canonical Markdown article. Element articles must link to
related element articles wherever a relationship is described. Cross-phase
relationships use relative markdown links to the canonical location of the target
element.

## Diagram Rule

Diagrams are representations of the model, not a source of truth. Diagrams may
show only architecture elements that are present in the architecture model as
Markdown element articles and only relationships that are documented in the
related element articles' `## Relations` sections. Do not add diagram-only
elements, placeholder nodes, implied events, implied data, implied artifacts,
visual grouping nodes, or implied relationships unless they also exist in the
model. If a diagram needs such an element or relationship, add the element
article and relationship first, or omit it from the diagram. Apply changes to
the model first: create or update the element articles and their `## Relations`
sections, then update diagrams to represent those model changes. Elements and
relationships shown on diagrams and in model articles must be kept in sync, with
the model articles and their `## Relations` sections taking precedence.

Use Mermaid diagram types as follows:

- `flowchart` and `sequenceDiagram` for TOGAF process flows, learning loops, approvals, and handoffs.
- `gitGraph` for branching, versioning, repository contribution, and change governance flows.
- `classDiagram`, `stateDiagram`, and other UML-style Mermaid views for architecture design decisions when structure or behavior must be clarified.
- `erDiagram` for entity relationship views that support architecture design decisions and requirements.

Each describing flowchart diagram must be built from an explicit viewpoint.
Entity-relationship diagrams may define different notation rules when needed.
Each describing flowchart diagram must contain one Mermaid subgraph, or subchart,
named the same as the describing element. This subgraph represents the describing
element as a visual boundary and contains only elements that are internal to the
describing element according to the selected viewpoint. Elements outside that
internal set are external context and must remain outside the subgraph.

Each phase metamodel may define several viewpoints. Each viewpoint defines:

- Element types the viewpoint is applied to. The selected element is the main
  element of the diagram.
- Relationship types and element types considered primary. By default this
  includes all elements that are composed or aggregated by the main element.
- Further relationship types and element types considered contextual. By default
  no contextual elements are shown.
- Diagramming rules that prescribe how the main, primary, and contextual elements
  are displayed.
- Validation rules that the viewpoint is responsible for validating and solving.

The subgraph itself is allowed as diagram structure when it is named by the
describing element; it must not introduce a separate diagram-only architecture
element.

Each phase metamodel must define validation rules under the viewpoints where the
rules are validated and solved. Validation rules apply to model elements,
relationships, and viewpoints. They identify inconsistencies in the architecture
model itself, not only in diagram presentation. Rule identifiers are scoped by
phase metamodel prefix, for example `A1`, `B1`, `Ca1`, `Cd1`, `D1`, `E1`, `F1`,
`G1`, `H1`, and `RM1`.

A validation rule may appear under more than one viewpoint when several
viewpoints make the same inconsistency visible and fixable. A viewpoint section
that owns validation rules uses this structure: description, elements,
relationships, diagramming rules, and validation rules.

Validations are never run outside a viewpoint. When a viewpoint is used,
validation is run for the main element and all primary elements in that viewpoint
scope. This is a common metamodel rule and phase metamodels or viewpoints must
not override it.

## Stereotype Rule

Use angle-quote stereotype notation in element headings:

```text
# Element Name «ArchiMate Type»
```

The stereotype is the ArchiMate element type, such as `«Capability»`, `«Business Process»`, `«Application Service»`, or `«Data Object»`. This follows the UML/ArchiMate stereotype idea while staying markdown-friendly. Do not repeat the element type in the element name or in a separate metadata bullet.

The base ArchiMate classification is defined in the phase metamodel documents and follows the usual active structure, behavior, passive structure, motivation, strategy, implementation/migration, and physical groupings. Relation labels may also be treated as stereotypes in prose, for example `Realizes`, `Serves`, `Accesses`, `Influences`, `Triggers`, `Composes`, or `Sourced from`.

## Base Stereotypes

| Base stereotype | Typical element types |
| --- | --- |
| `«Active Structure»` | Business Actor, Business Role, Application Component, Node, Device, System Software |
| `«Behavior»` | Business Process, Business Service, Application Service, Technology Service, Work Package |
| `«Passive Structure»` | Business Object, Data Object, Artifact |
| `«Motivation»` | Stakeholder, Driver, Assessment, Goal, Outcome, Requirement, Constraint |
| `«Strategy»` | Resource, Capability, Course of Action, Value Stream |
| `«Implementation and Migration»` | Work Package, Deliverable, Implementation Event, Plateau, Gap |
| `«Physical»` | Equipment, Facility, Distribution Network, Material |

Article headings use the concrete ArchiMate element type as the stereotype, not the base stereotype. The base stereotype is useful when defining catalogs, viewpoints, or validation rules.

## Repository-Local Stereotypes

Textual records may use repository-local stereotypes when the repository needs a small notation convention that is not directly expressed by standard ArchiMate. The controlled stereotypes are:

| Stereotype | Meaning |
| --- | --- |
| `<<abstract>>` | Template or conceptual pattern for concrete architecture elements in any phase. |
| `<<add>>` | Element or relationship is proposed to be added in the target or transition view. |
| `<<change>>` | Element or relationship already exists but is proposed to change. |
| `<<remove>>` | Element or relationship is proposed to be removed. |
| `<<out-of-scope>>` | Element or relationship is visible for context but excluded from the current scope. |

An `<<abstract>>` element is not a deployed, purchased, implemented, or committed target element by itself. It is a reusable architecture template that defines expected structure, obligations, relationships, or governance rules for concrete records that follow it.

Concrete records that follow an abstract template must keep their own ArchiMate element type, identifier, phase, status, and traceability. They should reference the template explicitly, but they should not use ArchiMate specialization unless there is a real architectural specialization relationship to govern.

Use `<<abstract>>` only when the record defines a reusable template, not when the record represents an actual business, application, data, technology, strategy, motivation, implementation, migration, governance, or change-management element. Do not create synthetic generic ArchiMate elements solely to support specialization hierarchies. Prefer a template reference such as `Template` or `Conforms to` when concrete records follow an abstract pattern.

Keep the ArchiMate element type explicit even when a repository-local stereotype is present. The stereotype qualifies repository usage; it does not replace the metamodel type. Keep status separate from stereotypes. Use change-scope stereotypes only to clarify a target, transition, or scoped view; they do not replace requirements, decisions, or traceability.

## Relation Section Rule

Every element article must have a `## Relations` section. Relationship entries in
`## Relations` are the source of truth for relationships owned by or asserted by
that element. Diagrams, catalogs, indexes, and viewpoint tables must follow these
relationship entries rather than inventing relationships independently.

Every element article uses:

```text
## Relations

- Relationship stereotype: linked element.

## Required by

- Linked element that depends on, requires, or consumes this element.
```

Use `Relations` for relationships within the current phase or from previous ADM phases. Use `Required by` for reverse demand, consumption, dependency, governance, or traceability links where this element is needed by another element.

## Duplicate Rule

Create one canonical article per element. If an early vision element is later elaborated in a more specific phase, move or merge it into the canonical phase folder and preserve the trace relationship in prose instead of keeping duplicate files.
