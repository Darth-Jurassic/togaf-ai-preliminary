# Process for D — Technology Architecture

Phase D defines the technology that realizes the application/business design.
Shared session/record rules are in [Process for Model](Process%20for%20Model.md).

## Initiation

- Announce the selected Plan and unfinished Stage D. Verify A–C canonical
  definitions and completion for this scope before technology target design.
- Read Technology Architecture, DQ/DC items, upstream contracts, and
  [Metamodel for Technology](../metamodel/Metamodel%20for%20Technology.md).
  For Kubernetes targets also read
  [Metamodel for Kubernetes](../metamodel/Metamodel%20for%20Kubernetes.md).
- Identify relevant software, nodes, devices, artifacts, services, processes,
  interfaces, paths, collaborations, physical elements, and deployment boundaries.

## Progress

- Create/update every relevant Technology article and put all technology and
  deployment definitions there. Link Baseline evidence and intended Changes from
  the Plan. Target configuration is a definition, not proof of deployment.
- Validate upstream traces through relevant Application/Business concepts to
  Motivation/Strategy and preserve valid location, ownership, and layer rules.
- Define runtime, artifact, API, test, and Kubernetes evidence responsibilities
  for later coverage and delivery. Declare affected repositories through their
  Technology Artifacts and required CLI/remote targets through Context.
- Read-only repository/runtime inspection may establish observed baselines;
  it does not authorize effective configuration, test, or deployment changes.
- Resolve DQ/DC items, record work/progress, and reopen upstream gates when a
  feasibility constraint requires a changed definition.

## Completion

Set Stage D `Complete: yes` only when all relevant technology terms and target
definitions are canonical, upstream relationships validate, and no DQ/DC blocks
the scope. Verification identifies the articles, boundaries, and evidence targets.

Report D complete and [Stage E](Process%20for%20E.md) for the next session.
