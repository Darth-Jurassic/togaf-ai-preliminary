# Preliminary 0012: Define Organization Units for Report Handling

- Record: Reusable policy
- Tags: preliminary, organization, report-handling, phase-h, governance, sales-marketing-board, delivery-board, architecture-board

## Context

[Preliminary 0006](0006-validate-and-score-reports-with-stakeholder-roles.md)
defines validation responsibilities such as report originator, report steward,
architecture owner, product reviewer, delivery reviewer, engineering reviewer,
governance reviewer, and board sponsor.

Those responsibilities are not the same graph as the organization structure.
The repository needs a separate organization-unit view so each Phase H report can
name the organization unit responsible for handling it before or during board
synchronization.

## Decision

Report handling will distinguish organization units, synchronization boards,
tenant-centric representatives, and validation roles.

- Organization units are stable homes for people and handling responsibility.
- Synchronization boards are cross-office forums that score, prioritize, and
  sponsor reports.
- Tenant-centric representatives are the people who carry each office's view for
  a tenant, deal, delivery, or implementation context.
- Validation roles are per-report responsibilities assigned to people or groups
  for the current report.

## Organization Units

| Identifier | Organization unit | Members or represented positions | Primary report-handling responsibility |
| --- | --- | --- | --- |
| `ORG-001` | Sales and Marketing Office | CEO, Head of Operations, Sales. | Product, market, sales, due diligence, high-level tenant scope negotiation, product positioning, pricing, commercial risk, and market opportunity reports. |
| `ORG-002` | Delivery Office | Head of Delivery, Product Owner, system analysts, project managers, QA. | Delivery, requirements clarification, product planning, tenant rollout, implementation coordination, QA evidence, and operational commitment reports. |
| `ORG-003` | Technology Office | Tech Lead, architects, team leads, developers, DevOps. | Architecture, engineering quality, implementation feasibility, automation, DevOps, platform, maintainability, security exposure, and technology risk reports. |

## Synchronization Boards

Boards are not separate organization units. They are synchronization forums that
draw participants from one or more organization units.

| Identifier | Board | Participating organization units | Primary handling scope |
| --- | --- | --- | --- |
| `BOARD-001` | Sales and Marketing Board | `ORG-001 Sales and Marketing Office`, with `ORG-002 Delivery Office` when product shaping, clarification, planning, or delivery feasibility input is material. | Product reports whose dominant impact is market value, tenant commercial interest, high-level scope, sales fit, due diligence, pricing, product positioning, or product packaging. |
| `BOARD-002` | Delivery Board | `ORG-002 Delivery Office`, with `ORG-001 Sales and Marketing Office` or `ORG-003 Technology Office` when market or technology input is material. | Operational reports whose dominant impact is delivery comfort, ownership, commitment reliability, requirements clarification, QA evidence, rollout, or delivery coordination. |
| `BOARD-003` | Architecture Board | `ORG-003 Technology Office`, with `ORG-002 Delivery Office` when requirements, QA, delivery, release, rollout, or tenant customization impact is material. | Technology reports whose dominant impact is architecture, engineering quality, frontend, backend, customization, DevOps, platform, automation, maintainability, security exposure, or technology risk. |

## Tenant-Centric Representatives

Tenant-centric representatives are the default people expected to provide the
office perspective for a tenant, sales opportunity, implementation, or active
delivery context.

| Identifier | Representative role | Represents | Typical report perspective |
| --- | --- | --- | --- |
| `REP-001` | Salesman | `ORG-001 Sales and Marketing Office` | Tenant commercial interest, high-level scope, buying concerns, due diligence concerns, pricing sensitivity, and sales risk. |
| `REP-002` | Project Manager | `ORG-002 Delivery Office` | Delivery commitment, planning, clarification, coordination, rollout, tenant communication, and operational risk. |
| `REP-003` | Team Lead | `ORG-003 Technology Office` | Technical feasibility, implementation impact, engineering quality, automation, maintainability, and technology risk. |

Reports connected to a tenant, deal, implementation, or active delivery context
should name the relevant tenant-centric representatives when known.

## Handling Assignment Rules

Each Phase H report must name a responsible handling organization unit and a
proposed synchronization board before board review.

Use the dominant concern to assign the handling organization unit:

- Product, market, sales, pricing, due diligence, commercial positioning, and
  high-level tenant scope negotiation concerns are handled by
  `ORG-001 Sales and Marketing Office`.
- Requirements clarification, product planning, QA evidence, delivery
  coordination, rollout, and operational commitment concerns are handled by
  `ORG-002 Delivery Office`.
- Architecture, engineering, platform, automation, DevOps, maintainability,
  security exposure, and technology risk concerns are handled by
  `ORG-003 Technology Office`.

Use the dominant concern to assign the synchronization board:

- Product reports are synchronized, scored, and prioritized by
  `BOARD-001 Sales and Marketing Board`.
- Operational reports are synchronized, scored, and prioritized by
  `BOARD-002 Delivery Board`.
- Technology reports are synchronized, scored, and prioritized by the relevant
  `BOARD-003 Architecture Board`.

Reports may involve more than one organization unit, but one unit must be named
as the primary handling owner. Secondary units must be listed when their input is
required for scoring, clarification, or evidence.

## Role Assignment Guidance

Validation roles from [Preliminary 0006](0006-validate-and-score-reports-with-stakeholder-roles.md)
should be assigned from the organization units as follows:

| Validation role | Usual organization-unit source |
| --- | --- |
| `ROLE-001 Report Originator` | Any organization unit. |
| `ROLE-002 Report Steward` | Usually `ORG-002 Delivery Office`; may be agent-assisted or assigned by the handling organization unit. |
| `ROLE-003 Architecture Owner` | Usually `ORG-003 Technology Office`. |
| `ROLE-004 Product Owner` | Usually `ORG-002 Delivery Office`, with market input from `ORG-001 Sales and Marketing Office`. |
| `ROLE-005 Delivery Owner` | Usually `ORG-002 Delivery Office`. |
| `ROLE-006 Engineering Owner` | Usually `ORG-003 Technology Office`. |
| `ROLE-007 Governance Reviewer` | Usually `ORG-003 Technology Office` or the synchronization board sponsor when a separate governance reviewer is not assigned. |
| `ROLE-008 Board Sponsor` | The sponsor named by the synchronization board responsible for the report. |

Tenant-centric representatives may fulfill or inform validation roles when the
report is tied to a tenant, deal, implementation, or active delivery context:

| Representative role | Typical validation contribution |
| --- | --- |
| `REP-001 Salesman` | May act as report originator or provide product, sales, high-level scope, commercial, and due diligence evidence. |
| `REP-002 Project Manager` | May act as report steward, delivery owner, or provide planning, commitment, clarification, coordination, and rollout evidence. |
| `REP-003 Team Lead` | May act as architecture owner, engineering owner, or provide implementation impact, feasibility, quality, and technology evidence. |

## Consequences

- The repository can assign report handling responsibility without confusing the
  organization chart with validation responsibilities.
- Product, operational, and technology reports can be routed consistently even
  when several offices are involved.
- Board synchronization remains cross-functional while every report still has a
  primary handling owner.
- Future reports can record both the handling organization unit and the
  per-report validation roles needed for scoring and conversion.
