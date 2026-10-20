# Process for Preliminary

The Preliminary process controls changes to this profile's metamodel and reusable
architecture process definitions. It keeps those changes explicit before model
work relies on them.

## Blocking Plans

`docs/plan.metamodel.md` and `docs/plan.process.md`, when present, are active
blocker-oriented Preliminary Plans. They do not use the numbered capability- and
Work-Package-centric model-Plan convention and are deleted when their work is
resolved. When a session has a current Plan, that Plan records metamodel or
process work without creating a Preliminary Plan, regardless of that Plan's
stated aim.

| Plan | Controls | Blocks while the file exists and `### Left to do` contains work |
| --- | --- | --- |
| `docs/plan.metamodel.md` | local metamodel definitions and migrations. | `docs/plan.process.md` and [Process for Model](Process%20for%20Model.md). |
| `docs/plan.process.md` | Reusable architecture and development process definitions. | [Process for Model](Process%20for%20Model.md). |

Ingest registration is blocked by no Plan. Every AI session is registered directly
as an ingest, even while a Preliminary Plan has open work.

## Implicit Groom Plans

Every repository-local skill, `AGENTS.md`, metamodel, or process change is
implicit groom work. It may be made on any active Plan branch regardless of that
Plan's stated aim. When the session has a current Plan, record the groom work,
its affected repositories, blockers, progress, and application evidence in that
Plan. Create the next numbered `groom/plan-NNNN-slug` Plan only when the session
has no current Plan or the user explicitly directs a separate Plan. An active
Metamodel or Process Plan records any remaining blocker; the current or groom
Plan records completed evidence before the active Preliminary Plan is deleted.

## Changing The Metamodel

1. Record intended metamodel work and any unresolved blocker in the current Plan.
   Only when no Plan is current, create or update `docs/plan.metamodel.md` under
   `## Plan` / `### Left to do`.
2. Use the current Plan for the metamodel change. Create an implicit groom Plan
   only when no Plan is current or the user explicitly directs a separate Plan.
3. Resolve safe matters from authoritative context and record only blockers that
   require later action.
4. Apply the metamodel definition and migration changes, then record the result
   and validation evidence in the groom Plan and applicable canonical articles.
5. Remove completed work from the current Plan. When a Preliminary Plan was
   created, delete its resolved `docs/plan.metamodel.md` through `$plan finish`.
   Until deletion, its open work blocks `docs/plan.process.md` and Process for
   Model.

## Changing The Process

1. Confirm that `docs/plan.metamodel.md` is absent or has no remaining
   `### Left to do` work.
2. Record intended process work and any unresolved blocker in the current Plan.
   Only when no Plan is current, create or update `docs/plan.process.md` under
   `## Plan` / `### Left to do`.
3. Use the current Plan for the process or skill change. Create an implicit groom
   Plan only when no Plan is current or the user explicitly directs a separate
   Plan.
4. Apply the process-document changes and record the result and validation
   evidence in the groom Plan and applicable canonical process articles.
5. Remove completed work from the current Plan. When a Preliminary Plan was
   created, delete its resolved `docs/plan.process.md` through `$plan finish`.
   Until deletion, its open work blocks Process for Model.

## Plan Deletion

Plans are working records, not durable architecture evidence. Delete every
completed numbered Plan through `$plan finish`. Delete a completed Preliminary
Plan at the same time when its groom has recorded the result in the applicable
canonical process or metamodel article. The absence of either Preliminary Plan
means it has no active blocker; create the applicable file only when work starts
without a current Plan.
