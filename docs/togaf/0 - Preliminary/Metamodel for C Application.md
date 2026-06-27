# Metamodel for C Application

Phase C Application Architecture describes application structure and behavior. Application element articles live in `C - Information Systems Architecture/application/`.

Phase C has two TOGAF subphases. Data Architecture is defined separately in [Metamodel for C Data](Metamodel%20for%20C%20Data.md).

## Canonical Element Types

| Group | Element types | Use in Phase C application architecture |
| --- | --- | --- |
| Active structure | Application Component, Application Collaboration, Application Interface | Use for deployable or logical application parts, their collaborations, and exposed application access points. |
| Behavior | Application Process, Application Function, Application Interaction, Application Event, Application Service | Use for application behavior, grouped capabilities, collaborations, triggers, and externally usable application services. |

## Article Guidance

- Keep one markdown file per ArchiMate element.
- Use the element name as the level-1 heading.
- Use a level-1 heading with one of the canonical Phase C Application Architecture element types as the stereotype.
- Put application components, services, functions, interfaces, events, and interactions under `C - Information Systems Architecture/application/`.
- Link application elements to Phase B business services/processes and Requirements Management requirements.
- Link application elements to Phase C data objects, Phase D technology elements, and Phase E/F/G/H implementation or change elements when relevant.
- Application Event elements may represent completed events or received commands.
  Name completed events using past-perfect or past-participle wording, meaning
  something has already happened. Name commands using present-simple imperative
  wording, meaning `Command to do something received` is shortened to
  `Do something`.

## Function And Process Views

- Every Application Process must be aggregated by at least one Application
  Function.
- Application Function articles must include a Mermaid flowchart diagram using
  the Mermaid flowchart syntax:
  <https://mermaid.js.org/syntax/flowchart.html>.
- The Application Function flowchart must show the Application Processes
  aggregated by the function.
- The Application Function flowchart must show Application Events that initiate
  the aggregated processes.
- The Application Function flowchart must show Application Events produced by the
  aggregated processes.
- The Application Function flowchart must show Data Objects consumed or produced
  by the aggregated processes.
- The Application Function flowchart must use these Mermaid node shapes:
  `id1>This is the text in the box]` for events,
  `id1(This is the text in the box)` for processes and functions,
  `id1[(This is the text in the box)]` for documents, data, artifacts, and
  services.
- Application Process articles should link back to at least one aggregating
  Application Function using an Aggregation relationship.
- Application Function flowcharts are representations of model articles and their
  `## Relations` sections. Every relevant modeled aggregation, trigger, access,
  or flow relationship in the function view should be reflected in the diagram.

## Viewpoints

### Application Context Viewpoint

The Application Context Viewpoint starts with a single Application behavior
element: either an Application Function or an Application Process.

Applied to element types:

- Application Function.
- Application Process.

Primary relationship and element set:

- Directly composed Application elements.
- Directly aggregated Application elements.

Contextual relationship and element set:

- Application Events, Application Functions, Application Processes, Application
  Services, Data Objects, Application Components, Application Collaborations, and
  Application Interfaces that are one relationship step away from the describing
  element or its internal elements by read/write/produce/consume, trigger/flow,
  assignment, or serving relationships.

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
| Ca1 | Application Function, Application Process | The selected main element must be an Application Function or Application Process. |
| Ca2 | Composition, Aggregation | Every primary element in the viewpoint scope must have a documented Composition or Aggregation relationship with the main element. |
| Ca3 | Access, Triggering, Flow, Assignment, Serving | Every contextual element in the viewpoint scope must be no more than one allowed contextual relationship step away from the main element or a primary element. |
| Ca5 | Application Process | Every Application Process must be aggregated by at least one Application Function. |

## Filename Prefixes

Use the repository filename pattern from [Metamodel](Metamodel.md):
`<type-in-lowercase>-<NNNN>-<slug>.md`.

| Element type | Prefix examples |
| --- | --- |
| Application Component | `application-component-` |
| Application Collaboration | `application-collaboration-` |
| Application Interface | `application-interface-` |
| Application Process | `application-process-` |
| Application Function | `application-function-` |
| Application Interaction | `application-interaction-` |
| Application Event | `application-event-` |
| Application Service | `application-service-` |
