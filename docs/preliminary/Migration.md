# Preliminary Migration

This revision reconciles the original phase-folder/ArchiMate 3.2 guidance with a
layer-based local profile informed by ArchiMate 4 and expanded ADM processes.
Old Preliminary URLs remain pointers; their former definitions are superseded,
not a second valid profile. Git history preserves the original documents.

| Previous rule | Current rule |
| --- | --- |
| Definitions in `docs/togaf/0 - Preliminary/` | Process and metamodel definitions in `docs/preliminary/process/` and `docs/preliminary/metamodel/`. |
| Elements stored in A–H/RM folders | One canonical article per element, stored by owning layer under `docs/model/`; Plans own phase progress, not element identity. |
| Application/data split into phase subfolders | Application concepts, including Data Objects, use their canonical application layer. |
| Separate Constraint and Gap element types | Mandatory constraints use Requirements/Principles; deficiencies use `Assessment «gap»` as defined in the current profile. |
| Base type repeated as heading stereotype | Displayed type and four-digit identity lead the heading; lowercase registered stereotypes classify concepts, with domain-qualified types as specified by each table. |
| Numbers scoped to phase directories | Independent four-digit sequences by displayed element type, not phase or specialization. |
| Relations and Required by sections | Description, Evidence and Relationships; typed connector rules and explicit canonical links govern traces. |
| Phase-specific validation vocabularies | Registered stereotype systems, declared/runtime closure and context-dependent functional relationship validation, with explicit origin and cardinality rules. |
| Work can advance from document presence | Verified scope-specific Completion gates; phase-owned stable Questions/Concerns; no automatic next-phase session. |
| Requirements duplicated or moved into RM | One canonical Motivation Requirement, managed continuously across phases. |
| Raw reports under H folders | Source channels under `docs/ingests/`, distinct from canonical layer elements. |

Report preservation, lean-loss classification/scoring, accountable validation,
board routing, motivation-first work, Markdown authority, diagram consistency,
companion-file handling and discussion-before-implementation remain. Current
phase/gate/evidence rules replace conflicting older placement/notation rules.

The AI, Git, Kubernetes, plugin and tenant stereotype profiles remain reusable.
Product context and naming decisions are adopter-owned policies; no tenant names,
namespace prefixes, private model links, operational targets, session records or
source-specific audit/legacy inventories are supplied. External standards are
linked publicly, not copied. The original MIT license is unchanged.

Before applying this to an existing model, inventory its identities and traces,
agree the migration scope, preserve originals/evidence and reconcile each change
through an adopting Plan. This repository migration contains no concrete model
to move and grants no authority over an adopter's implementations or deployments.
