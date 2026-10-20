# Process for H — Architecture Change Management

Phase H evaluates delivered evidence and updates the Assessments established in
A. Shared rules are in [Process for Model](Process%20for%20Model.md) and
[Process for Model Records](Process%20for%20Model%20Records.md).

## Initiation

- Announce the selected Plan and unfinished Stage H. Verify preceding scoped
  completion, the delivered Work Packages, and G's reverse-delivered evidence.
- Read Architecture Change Management, HQ/HC items, Assessment criteria, and the
  relevant canonical Business/Application/Technology articles. Read the
  [Motivation metamodel](../metamodel/Metamodel%20for%20Motivation.md).
- Identify the exact criteria and evidence to evaluate. Missing runtime/test
  evidence remains missing; delivery or merge is not an inferred passing result.

## Progress

- Update each relevant canonical Assessment from actual G evidence against its
  validation definition: distinguish demonstrated, failed, and unevidenced
  criteria and preserve source/revision links.
- Record resulting feedback, model corrections, and change signals in Changes.
  Trace canonical updates to their evidence; route altered definitions or work
  back to the responsible phase and reopen its Completion gate when necessary.
- Accepted deficiencies, limitations, or intentional inaccuracies become an
  `Assessment «gap»` with the current deficiency and priority. It need not invent
  a target solution or Work Package before those are defined by later work.
- Resolve HQ/HC items. Keep raw stakeholder/system signals as ingests rather than
  rewriting them as canonical conclusions. Follow the lean Phase H-to-A loop
  when feedback changes Motivation or Strategy.

An explicitly selected H1/H2 may perform manual acceptance observations against
the delivered G1/G2 release as part of evaluation. Record tester/time/revision,
redacted results and source ingests; reverse-link manual test/runtime evidence
to the owning Business/Technology targets and update their Assessments. H does
not change implementation or deploy corrections: return those to the appropriate
F/G scope and reopen altered architecture gates when required.

If H1 is the promotion gate before F2, required manual cases must pass before
H1's scoped Completion becomes yes. Missing/failed results or unaccepted gaps
keep promotion blocked even when an evaluation report exists. H1's accepted
results inform F2; H2 evaluates the second scope (BO in the selected example).
Overall H remains incomplete
until every relevant iteration/evaluation and required promotion gate is complete.

## Completion

Set Stage H `Complete: yes` only when relevant Assessments are evaluated from
their defined criteria and available evidence, missing/failed criteria are
explicitly disposed of or routed as gaps/work, and no HQ/HC blocks closure.
Verification links the updated Assessments and resulting canonical changes.

For an explicitly selected H1, report its actual acceptance/evaluation result
and the next scoped phase (F2 when its promotion gate passes), not whole-Plan
completion. H2 closes only its own evaluated scope; assess all iterations before
reporting overall completion. Report any reopened phase. Do not start a
new phase or invoke `$plan finish` automatically. Finish requires no remaining
Plan work, complete durable evidence, delivered repositories, owning Work Package
or groom evidence updates, successor dependencies preserved, and the explicit
finish workflow before deleting the Plan and its worktrees.
