# Preliminary 0008: Capture Product Feedback as Motivation Input

- Record: Reusable policy
- Tags: preliminary, phase-h, phase-a, feedback, motivation, swot

## Context

[Preliminary 0002](0002-align-architecture-work-with-lean-software-product-development.md)
requires raw feedback and source context to be preserved before interpretation.
Current product feedback exists across sales conversations, automation work,
implementation projects, and active tenants. This feedback is important input for both product
architecture and the internal technology process.

The feedback should not be prematurely normalized or interpreted. The repository
needs to preserve statements as they were received while also making them useful
for architecture analysis.

## Decision

We will capture current product feedback as-is, then tag and analyze it as input
to the ArchiMate motivation layer.

Each feedback record should preserve the original statement text and add
structured metadata:

- Stakeholder or stakeholder group.
- Categories and tags.
- Source context, where known.
- TOGAF relevance, especially the flow from Phase H architecture change
  management into Phase A architecture vision.
- Related SWOT observations.
- Candidate drivers, assessments, goals, outcomes, constraints, principles, and
  requirements.

## Consequences

- Raw feedback remains auditable and separable from interpretation.
- Feedback can be grouped by stakeholder, category, product concern, and process
  concern.
- SWOT analysis can connect external and internal observations to motivation
  elements.
- Later architecture work can trace product architecture changes and internal
  technology process improvements back to current evidence.
