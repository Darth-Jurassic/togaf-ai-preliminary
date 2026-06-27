# Metamodel for D

Phase D describes technology architecture. Element articles live directly in `D - Technology Architecture/`; technology element families are managed through catalogs and viewpoints, not subfolders.

## Canonical Element Types

| Group | Element types | Use in Phase D |
| --- | --- | --- |
| Active structure | Node, Device, System Software, Technology Collaboration, Technology Interface, Path, Communication Network | Use for technology hosts, hardware, runtime software, collaborations, access points, and connectivity. |
| Behavior | Technology Process, Technology Function, Technology Interaction, Technology Event, Technology Service | Use for infrastructure behavior, grouped technology capabilities, collaborative technology behavior, triggers, and offered technology services. |
| Passive structure and physical | Artifact, Equipment, Facility, Distribution Network, Material | Use for deployable artifacts and physical architecture elements when they matter to the architecture. |

## Article Guidance

- Keep one markdown file per ArchiMate element.
- Use the element name as the level-1 heading.
- Use a level-1 heading with one of the canonical Phase D element types as the stereotype.
- Describe technology responsibilities and constraints, not application behavior.
- Link technology elements to the Phase C application/data elements they host, implement, store, or serve.
- Technology Event elements may represent completed events or received commands.
  Name completed events using past-perfect or past-participle wording, meaning
  something has already happened. Name commands using present-simple imperative
  wording, meaning `Command to do something received` is shortened to
  `Do something`.

## Function And Process Views

- Every Technology Process must be aggregated by at least one Technology
  Function.
- Technology Function articles must include a Mermaid flowchart diagram using the
  Mermaid flowchart syntax:
  <https://mermaid.js.org/syntax/flowchart.html>.
- The Technology Function flowchart must show the Technology Processes aggregated
  by the function.
- The Technology Function flowchart must show Technology Events that initiate the
  aggregated processes.
- The Technology Function flowchart must show Technology Events produced by the
  aggregated processes.
- The Technology Function flowchart must show Artifacts consumed or produced by
  the aggregated processes.
- The Technology Function flowchart must use these Mermaid node shapes:
  `id1>This is the text in the box]` for events,
  `id1(This is the text in the box)` for processes and functions,
  `id1[(This is the text in the box)]` for documents, data, artifacts, and
  services.
- Technology Process articles should link back to at least one aggregating
  Technology Function using an Aggregation relationship.
- Technology Function flowcharts are representations of model articles and their
  `## Relations` sections. Every relevant modeled aggregation, trigger, access,
  or flow relationship in the function view should be reflected in the diagram.

## Technology Context Viewpoint

The Technology Context Viewpoint starts with a single Technology behavior
element: either a Technology Function or a Technology Process.

Description:

The Technology Context Viewpoint shows one Technology Function or Technology
Process, its directly composed or aggregated internal technology behavior, and
one-step external technology context needed to understand triggering, access,
flow, assignment, and serving relationships.

Elements:

- The main element is a Technology Function or Technology Process.
- Primary elements are Technology elements directly composed or aggregated by the
  main element.
- Contextual elements are Technology Events, Technology Functions, Technology
  Processes, Technology Services, Artifacts, Nodes, Devices, System Software,
  Technology Collaborations, and Technology Interfaces that are one allowed
  contextual relationship step away from the main element or its primary
  elements.

Relationships:

- Primary relationships shown inside the describing-element subgraph:
  Composition and Aggregation from the main element to directly composed or
  aggregated Technology elements.
- Contextual relationships shown around the describing-element subgraph:
  read/write/produce/consume, trigger/flow, assignment, serving, and association
  relationships that are one relationship step away from the main element or its
  primary elements.

Diagramming rules:

- The main element is represented by the Mermaid subgraph named the same as the
  describing element.
- Primary elements are shown inside the main element subgraph.
- Contextual elements are shown outside the main element subgraph.
- Events use `id1>This is the text in the box]`.
- Processes and functions use `id1(This is the text in the box)`.
- Documents, data, artifacts, and services use
  `id1[(This is the text in the box)]`.
- Read and write access relationships use dashed Mermaid arrows: `-.->`.
- Association relationships use solid undirected Mermaid links, for example
  `TagAdded --- PullRequest`.

The diagram must not include elements outside this one-step context unless a more
specific viewpoint explicitly allows them.

Validation Rules:

| Rule | Applies to | Validation |
| --- | --- | --- |
| D1 | Technology Process | Every Technology Process must be aggregated by at least one Technology Function. |
| D2 | Triggering | Each Technology Process must be triggered by another Technology Process or Technology Event and must trigger another Technology Process or Technology Event. |
| D3 | Access | Each Artifact must have exactly one producer and at least one consumer. |
| D4 | Assignment | Each Technology Function and Technology Process must be fully assigned: either the element itself is assigned, or all composed and aggregated Technology Functions and Technology Processes under it are fully assigned. |
| D5 | Association, Access, Triggering | If an Artifact is associated with a Technology Event, it can be written only by Technology Processes or Technology Functions that directly or transitively trigger that Technology Event, and it can be read only by Technology Processes or Technology Functions that are directly or transitively triggered by that Technology Event. |

## Filename Prefixes

Use the repository filename pattern from [Metamodel](Metamodel.md):
`<type-in-lowercase>-<NNNN>-<slug>.md`.

| Element type | Prefix examples |
| --- | --- |
| Node | `technology-node-` |
| Device | `technology-device-` |
| System Software | `technology-system-software-` |
| Technology Collaboration | `technology-collaboration-` |
| Technology Interface | `technology-interface-` |
| Path | `technology-path-` |
| Communication Network | `technology-communication-network-` |
| Technology Process | `technology-process-` |
| Technology Function | `technology-function-` |
| Technology Interaction | `technology-interaction-` |
| Technology Event | `technology-event-` |
| Technology Service | `technology-service-` |
| Artifact | `technology-artifact-` |
| Equipment | `equipment-` |
| Facility | `facility-` |
| Distribution Network | `distribution-network-` |
| Material | `material-` |
