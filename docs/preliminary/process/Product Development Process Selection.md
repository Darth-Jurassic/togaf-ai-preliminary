# Product Development Process Selection

## Context

[Product Development Process Definition](Product%20Development%20Process%20Definition.md)
aligns architecture work with lean software product development. It requires the
development process to preserve raw feedback, support a learning loop, trace
validated learning into product goals, measurable outcomes, constraints,
options, decisions, experiments, and improvement work, involve stakeholders,
define human accountability points, and control decisions through evidence
rather than document completeness alone.

[Product Context](Product%20Context.md) leaves product and organizational scope to
the adopting project. This reference selects a reusable process frame, while
allowing explicitly justified alignment with other delivery/governance methods.

This preliminary decision chooses the controlling process method that can
satisfy those lean process requirements and provide flexible control over the
development process. The following preliminary process record describes the
phase flow that will organize the rest of the repository.

The current work is in the Preliminary Phase, but the repository must preserve
the connection between Phase H architecture change inputs and Phase A motivation
work because feedback, ideas, risks, and problems are the main evidence base for
the Architecture Vision.

TOGAF, C4, and Zachman cover different parts of architecture and development
process work and satisfy different parts of the lean-aligned process:

- TOGAF is a process and governance method for enterprise architecture
  development, and its ADM provides development-process control points through
  requirements management, roadmap planning, implementation governance, and
  change management.
- C4 is a software architecture visualization model.
- Zachman is an enterprise architecture ontology that helps classify
  architecture descriptions by stakeholder perspective and interrogative concern.

The repository should use each framework where it is strongest and avoid forcing
all concerns into one framework's notation.

In this decision, TOGAF ADM means TOGAF 10 ADM. TOGAF 10 is the controlling
development-process frame; SAFe and the other companion practices may tailor it
without replacing it.

## Analysis

| Candidate | Main coverage | Strongest fit against Product Development Process Definition requirements | Weakness if used alone |
| --- | --- | --- | --- |
| TOGAF ADM | Architecture process, phase flow, governance, requirements management, architecture change management, migration planning, and controlled iteration. | Provide the architecture process frame, govern conversion from ingested signals into canonical model changes, and decide when work moves between motivation, architecture description, roadmap, and implementation governance. | Does not by itself provide a compact software system notation for developers, nor a complete ontology for checking every possible viewpoint. |
| C4 Model | Software architecture views at context, container, component, and code levels. | Describe product and platform structure in later ADM phases, especially Phase C Information Systems Architecture and Phase D Technology Architecture, after motivation and requirements are clear. | Does not define enterprise architecture governance, motivation, migration planning, or stakeholder concern coverage. |
| Zachman Framework | Architecture classification by perspectives and questions: what, how, where, who, when, and why across different stakeholder levels. | Use as a completeness checklist when validating whether reports, requirements, decisions, or architecture descriptions are missing a stakeholder perspective or concern type. | Does not prescribe an implementation process, learning loop, prioritization method, or software design notation. |

## Requirement Fit Against Product Development Process Definition

| Product development process requirement | TOGAF ADM | C4 Model | Zachman Framework |
| --- | --- | --- | --- |
| Preserve raw feedback and source context before interpretation. | Strong fit. Phase H and Requirements Management can treat feedback as architecture change input before it is interpreted into requirements or decisions. | Weak fit. C4 can show the resulting system context but does not define how to capture raw product feedback. | Partial fit. Zachman can classify source perspectives and concern types, but it does not define feedback intake or evidence handling. |
| Trace feedback, ideas, risks, and problems into stakeholders, categories, learning records, product goals, constraints, options, and decisions. | Strong fit. ADM phases, Architecture Requirements Management, stakeholder management, and decision governance provide the controlling traceability path. | Partial fit. C4 can trace selected requirements to software views after requirements exist, but it does not cover the full motivation-to-decision path. | Partial fit. Zachman helps check that trace links cover perspectives and questions, but it does not provide the change workflow. |
| Provide clear ways to streamline product-related information into learning loop inputs. | Strong fit. Phase H change inputs can be structured into Phase A motivation and requirements work, then revisited through Requirements Management. | Weak fit. C4 does not define a product learning loop. | Weak to partial fit. Zachman can classify information but does not decide how it flows through learning and governance. |
| Convert validated learning into product goals, measurable outcomes, constraints, options, decisions, experiments, and improvement work. | Strong fit. TOGAF explicitly supports moving from motivation and requirements into architecture options, roadmaps, migration planning, and governance. | Partial fit. C4 can communicate software options and design consequences, but only after the product or architecture question has been framed. | Partial fit. Zachman can expose missing question coverage, especially why, what, how, who, where, and when, but it does not convert learning into work. |
| Make the lean loss of ignored signals explicit enough to compare reports and explain priority. | Partial to strong fit. TOGAF governance can require evidence, impact, risk, and priority rationale, but lean loss scoring must be defined as a repository practice. | Weak fit. C4 does not compare feedback reports or product learning loss. | Partial fit. Zachman can show which perspectives or questions are being ignored, but it does not score loss or priority. |
| Allow goals, constraints, options, and decisions to be revisited when product learning changes the evidence base. | Strong fit. ADM iteration, Requirements Management, governance, and Phase H change management support controlled revisiting of earlier work. | Partial fit. C4 diagrams can be revised when architecture decisions change, but revision governance is outside the model. | Partial fit. Zachman can help re-check coverage after changes, but it does not manage iteration. |
| Involve accountable stakeholder roles in validation before reports become committed product or technology work. | Strong fit. Stakeholder management and report governance define accountable validation; later deterministic phase progression does not add blanket approval. | Weak to partial fit. C4 improves communication with software and product stakeholders but does not define accountability. | Partial fit. Zachman helps identify missing stakeholder perspectives, but it does not provide validation governance. |
| Define where human input, review, exception, or risk acceptance is mandatory. | Strong fit. TOGAF governance and explicit Questions or Concerns identify genuine human decision points; completion permits authorized work within the selected scope, not automatic next-phase sessions. | Weak fit. C4 improves communication but does not define mandatory control points. | Partial fit. Zachman can identify missing stakeholders or concerns, but it does not assign decision authority. |
| Define where AI-assisted automation may resolve, draft, check, synchronize, classify, or apply changes. | Strong fit when tailored. TOGAF separates evidence, requirements, governance, implementation, and change records, allowing deterministic automation with human escalation only for unresolved authority or intent. | Partial fit. C4 artifacts can be generated or checked by AI, but C4 does not define process ownership. | Partial fit. Zachman classifications can be AI-assisted, but Zachman does not define automation boundaries. |
| Keep architecture artifacts lightweight, versionable, reviewable, and suitable for iteration. | Partial fit. TOGAF can be tailored to lightweight repository artifacts, but this requires explicit tailoring and AI-assisted repository skills to avoid document-heavy practice. | Strong fit for software views. C4 diagrams are compact and reviewable when limited to appropriate architecture questions. | Partial fit. Zachman is useful as a checklist, but using it as a full documentation matrix would become too heavy. |
| Support decision control by checking evidence, traceability, decision quality, and learning status rather than document completeness alone. | Strong fit. TOGAF governance can control decisions through evidence, requirements traceability, stakeholder validation, and change management. | Weak fit. C4 supports explanation of software structure but not decision control. | Partial fit. Zachman can challenge completeness of perspectives and questions, but it must remain secondary to evidence and learning status. |

The comparison shows that TOGAF ADM is the only candidate that covers the
process, governance, traceability, validation, iteration, change-management,
human accountability, and automation-boundary requirements together. C4 and
Zachman are valuable, but each is incomplete as the controlling development
process: C4 is strongest after architecture questions become software structure
questions, while Zachman is strongest when checking whether a description or
decision misses a perspective or concern type.

For this profile, this makes TOGAF the first development process winner: it becomes the
primary process backbone used to organize the product's own architecture
repository and to shape the initial product capability. SAFe and other process
frameworks may still contribute delivery alignment, portfolio flow, roles, or
operating-model patterns, but they do not replace TOGAF as the controlling
process selected here.

## AI-Assisted Tailoring

The lightweight-artifact requirement is only a partial fit for TOGAF when TOGAF
is treated as a traditional document production framework. For this repository,
the fit is strengthened by a document-first and AI-assisted operating model:

- Use Markdown architecture records as the source of truth so AI skills can
  inspect, compare, update, and refactor architecture artifacts through normal
  version-control workflows.
- Use AI-assisted repository skills to maintain consistency between TOGAF phase
  artifacts, ArchiMate motivation elements, requirements, decisions, and later
  implementation evidence.
- Treat domain language as the primary input to architecture and implementation
  work. AI assistance can translate well-defined domain requirements, decisions,
  constraints, and acceptance criteria into software changes, tests, and bug
  fixes during Phase G while preserving traceability back to the architecture
  repository.
- Use AI to reduce the cost of synchronization, review preparation, gap checks,
  implementation alignment, and deterministic process progression. Human
  stakeholders remain accountable only for recorded matters requiring human
  intent, exception, risk acceptance, or policy authority.

This does not make TOGAF itself lightweight by default. It defines the
repository tailoring that makes TOGAF usable for a lean software product
learning loop in the current AI-assisted development environment.

## Development Process Capability Coverage

This comparison is not a full SDLC coverage matrix. It compares how TOGAF, C4,
and Zachman cover the development-process capabilities needed by this repository:
process control, governance, stakeholder concerns, requirements traceability,
architecture descriptions, roadmap planning, implementation governance,
human-loop decision points, AI-assisted automation boundaries, and change management.

| Concern | TOGAF ADM | C4 Model | Zachman Framework |
| --- | --- | --- | --- |
| Architecture process | Primary coverage through ADM phases. | Not covered. | Not covered as a process. |
| Governance | Primary coverage through Preliminary, Requirements Management, Phase G, and Phase H. | Not covered directly. | Supports governance review by exposing missing classifications. |
| Stakeholders and motivation | Covered in Phase A and Requirements Management. | Partially visible in system context diagrams. | Strong classification support for different stakeholder perspectives. |
| Requirements traceability | Covered across all ADM phases. | Can support traceability to software views, but does not define the traceability method. | Helps check whether requirements cover the right questions and perspectives. |
| Business architecture | Covered in Phase B. | Not the main purpose. | Can classify business artifacts by perspective and question. |
| Application and data architecture | Covered in Phase C. | Strong for application structure; weaker for data semantics. | Can classify application and data artifacts. |
| Technology architecture | Covered in Phase D. | Useful for deployment-adjacent container and component views. | Can classify technology artifacts. |
| Software design communication | Possible, but not concise enough by itself. | Primary coverage. | Not a diagramming model. |
| Migration and roadmap | Covered in Phase E and Phase F. | Not covered. | Can classify roadmap artifacts, but does not define roadmap method. |
| Human-in-the-loop control | Covered through ingest validation and explicit Questions or Concerns for unavailable information, human intent, exceptions, and risk acceptance; complete gates permit authorized work, not automatic phase advancement. | Not covered directly. | Helps identify missing perspectives, but does not define control. |
| AI automation boundaries | Can be tailored through explicit separation of evidence, requirements, decisions, governance, conformance, and change records. | Can support generated software views, but does not govern automation. | Can support AI-assisted classification checks, but does not govern automation. |
| Change management | Covered in Phase H. | Not covered. | Can help classify change impact. |

## Decision

We will use TOGAF 10 ADM as the controlling development process and governance
backbone for adopting projects because it best satisfies the lean
software product development process requirements from Product Development
Process Definition.

The decision is not limited to TOGAF as an architecture documentation process.
TOGAF ADM is selected because it gives adopting projects a flexible control model for
development work: the harness resolves repeatable and deterministic work from
authoritative context, while people enter the loop for unavailable information,
material intent choices, exceptions, risk acceptance, and policy-assigned
decisions.

We will not use C4 or Zachman as replacements for TOGAF. Instead:

- Use TOGAF to decide where work belongs in the ADM, how reports flow through
  the learning loop, when complete gates move work to the next phase, and where
  a genuine human decision or risk acceptance is required.
- Use the local metamodel, informed by ArchiMate documentation and
  maintained in Markdown as defined in [Metamodel](../metamodel/Metamodel.md).
- Use C4 views when software architecture needs to be communicated clearly to
  developers, analysts, delivery roles, or product stakeholders.
- Use Zachman as a completeness and classification checklist, especially during
  report validation, requirements review, Assessment review, and architecture
  decision review.
- Use AI automation inside the TOGAF-controlled process where the artifact,
  traceability, review, or consistency task can be checked and governed.
- Evaluate SAFe and other process frameworks as complementary sources for
  scaled delivery alignment, roles, portfolio flow, and implementation
  governance where they strengthen the adopting project without displacing the TOGAF ADM
  backbone.

The TOGAF ADM phase flow is described separately in
[Process for Model](Process%20for%20Model.md).

## Usage Rules

- During Preliminary and Phase A, prefer TOGAF and ArchiMate motivation elements.
- During Phase B, use TOGAF business architecture structure and apply Zachman to
  check whether business concerns are complete.
- During Phase C, use C4 context, container, and component views for application
  architecture when they make product structure easier to understand.
- During Phase D, use C4 and technology views to clarify runtime, platform,
  integration, and deployment decisions.
- During Phase E and Phase F, use TOGAF roadmap and migration planning concepts;
  use C4 only when a solution option needs software structure clarification.
- During Phase G and Phase H, use TOGAF governance and change management; use
  Zachman to check whether impact analysis misses stakeholder perspectives or
  architecture questions.

## Consequences

- The repository has one controlling process chosen against lean product
  development requirements instead of a bare framework preference.
- An adopting project starts with TOGAF as the first product development process backbone
  while keeping room for SAFe and other methods as complementary product
  capabilities.
- An adopting project can define explicit human-in-the-loop controls and AI automation zones
  without treating either manual review or full automation as the universal
  default.
- C4 can be introduced later without weakening the current motivation-first
  repository structure.
- Zachman can improve completeness without becoming a heavy documentation
  requirement.
- AI-assisted repository skills can reduce the operational cost of keeping
  TOGAF, ArchiMate, requirements, decisions, and implementation evidence
  synchronized, provided that the repository remains document-first and
  traceability-driven.
- Later architecture layers can still use specialized views without changing the
  controlling TOGAF process.
