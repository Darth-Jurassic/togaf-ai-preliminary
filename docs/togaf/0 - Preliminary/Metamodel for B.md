# Metamodel for B

Phase B describes the business architecture. Element articles live directly in `B - Business Architecture/`; business element families are managed through catalogs and viewpoints, not subfolders.

## Canonical Element Types

| Group | Element types | Use in Phase B |
| --- | --- | --- |
| Active structure | Business Actor, Business Role, Business Collaboration, Business Interface | Use for people, organizational responsibilities, collaborations, and externally visible business access points. |
| Behavior | Business Process, Business Function, Business Interaction, Business Event, Business Service | Use for business work, grouped behavior, collaborative behavior, triggers, and externally offered business outcomes. |
| Passive structure and products | Business Object, Contract, Representation, Product | Use for business information, formal agreements, perceptible information forms, and packaged business offerings. |

## Article Guidance

- Keep one markdown file per ArchiMate element.
- Use the element name as the level-1 heading.
- Use a level-1 heading with one of the canonical Phase B element types as the stereotype.
- Describe business intent and responsibility, not application implementation.
- Link business behavior to requirements in Requirements Management and realization elements in Phase C.
- Business Event elements may represent completed events or received commands.
  Name completed events using past-perfect or past-participle wording, meaning
  something has already happened. Name commands using present-simple imperative
  wording, meaning `Command to do something received` is shortened to
  `Do something`.

## Function And Process Views

- Every Business Process must be aggregated by at least one Business Function.
- Business Function articles must include a Mermaid flowchart diagram using the
  Mermaid flowchart syntax: <https://mermaid.js.org/syntax/flowchart.html>.
- The Business Function flowchart must show the Business Processes aggregated by
  the function.
- The Business Function flowchart must show Business Events that initiate the
  aggregated processes.
- The Business Function flowchart must show Business Events produced by the
  aggregated processes.
- The Business Function flowchart must show Business Objects, Contracts,
  Representations, and Products consumed or produced by the aggregated processes.
- The Business Function flowchart must use these Mermaid node shapes:
  `id1>This is the text in the box]` for events,
  `id1(This is the text in the box)` for processes and functions,
  `id1[(This is the text in the box)]` for documents, data, artifacts, and
  services.
- Business Process articles should link back to at least one aggregating Business
  Function using an Aggregation relationship.
- Business Function flowcharts are representations of model articles and their
  `## Relations` sections. Every relevant modeled aggregation, trigger, access,
  or flow relationship in the function view should be reflected in the diagram.

## Viewpoints

### Business Context Viewpoint

The Business Context Viewpoint starts with a single Business behavior element:
either a Business Function or a Business Process.

Applied to element types:

- Business Function.
- Business Process.

Primary relationship and element set:

- Directly composed Business elements.
- Directly aggregated Business elements.

Contextual relationship and element set:

- Business Events, Business Functions, Business Processes, Business Services,
  Business Objects, Contracts, Representations, Products, Business Actors,
  Business Roles, Business Collaborations, and Business Interfaces that are one
  relationship step away from the describing element or its internal elements by
  read/write/produce/consume, trigger/flow, assignment, or serving relationships.

Diagramming rules:

- The main element is represented by the Mermaid subgraph named the same as the
  describing element.
- Primary elements are shown inside the main element subgraph.
- Contextual elements are shown outside the main element subgraph.
- Events use `id1>This is the text in the box]`.
- Processes and functions use `id1(This is the text in the box)`.
- Documents, data, artifacts, and services use
  `id1[(This is the text in the box)]`.

The diagram must not include elements outside this one-step context unless a more
specific viewpoint explicitly allows them.

Validation Rules:

| Rule | Applies to | Validation |
| --- | --- | --- |
| B1 | Business Function, Business Process | The selected main element must be a Business Function or Business Process. |
| B2 | Composition, Aggregation | Every primary element in the viewpoint scope must have a documented Composition or Aggregation relationship with the main element. |
| B3 | Access, Triggering, Flow, Assignment, Serving | Every contextual element in the viewpoint scope must be no more than one allowed contextual relationship step away from the main element or a primary element. |
| B5 | Business Process | Every Business Process must be aggregated by at least one Business Function. |

## Filename Prefixes

Use the repository filename pattern from [Metamodel](Metamodel.md):
`<type-in-lowercase>-<NNNN>-<slug>.md`.

| Element type | Prefix examples |
| --- | --- |
| Business Actor | `business-actor-` |
| Business Role | `business-role-` |
| Business Collaboration | `business-collaboration-` |
| Business Interface | `business-interface-` |
| Business Process | `business-process-` |
| Business Function | `business-function-` |
| Business Interaction | `business-interaction-` |
| Business Event | `business-event-` |
| Business Service | `business-service-` |
| Business Object | `business-object-` |
| Contract | `contract-` |
| Representation | `representation-` |
| Product | `product-` |
