# Metamodel for Motivation

The ArchiMate 4 Motivation Domain is the reference framework for this local
Motivation domain definition. This profile specifies only the element types currently
used or explicitly required in this domain. This article is the operational
definition; the external reference is provenance only.

## Elements

Select an element from the distinguishing definition in this table. Its title and
filename use the forms shown in that row. `NNNN` is unique within an independent
four-digit sequence for that displayed local element type. Convert the element
name to lowercase kebab case for the filename. Include guillemets only when the
element has additional explicit stereotypes.

| Element | Explicit Stereotypes | Implicit Stereotypes | Title | Filename | Definition |
| --- | --- | --- | --- | --- | --- |
| `Meaning` | `«meaning»` | `«concept, element, motivation»` | `Meaning NNNN <Name> «additional, explicit, stereotypes»` | `meaning-NNNN-<name-in-kebab-case>.md` | Context-specific interpretation or knowledge conveyed by a concept; not its worth. |
| `Value` | `«value»` | `«concept, element, motivation»` | `Value NNNN <Name> «additional, explicit, stereotypes»` | `value-NNNN-<name-in-kebab-case>.md` | Stakeholder-relative benefit, harm, utility, or importance of a concept. |
| `Stakeholder` | `«stakeholder»` | `«concept, element, motivation»` | `Stakeholder NNNN <Name> «additional, explicit, stereotypes»` | `stakeholder-NNNN-<name-in-kebab-case>.md` | Perspective whose concerns, goals, or values matter to the architecture. |
| `Driver` | `«driver»` | `«concept, element, motivation»` | `Driver NNNN <Name> «additional, explicit, stereotypes»` | `driver-NNNN-<name-in-kebab-case>.md` | Condition creating pressure to establish goals or change architecture. |
| `Assessment` | `«assessment»` | `«concept, element, motivation»` | `Assessment NNNN <Name> «additional, explicit, stereotypes»` | `assessment-NNNN-<name-in-kebab-case>.md` | Result of analyzing enterprise state relative to a driver; not the driver, goal, or response. |
| `Goal` | `«goal»` | `«concept, element, motivation»` | `Goal NNNN <Name> «additional, explicit, stereotypes»` | `goal-NNNN-<name-in-kebab-case>.md` | Desired direction or end state; not the result eventually obtained. |
| `Outcome` | `«outcome»` | `«concept, element, motivation»` | `Outcome NNNN <Name> «additional, explicit, stereotypes»` | `outcome-NNNN-<name-in-kebab-case>.md` | Result or effect achieved or expected, including an unintended one. |
| `Principle` | `«principle»` | `«concept, element, motivation»` | `Principle NNNN <Name> «additional, explicit, stereotypes»` | `principle-NNNN-<name-in-kebab-case>.md` | Broad normative property for every applicable system in a context. |
| `Requirement` | `«requirement»` | `«concept, element, motivation»` | `Requirement NNNN <Name> «additional, explicit, stereotypes»` | `requirement-NNNN-<name-in-kebab-case>.md` | Mandatory property of a specific architecture or system. |
| `Assessment «gap»` | `«gap»` | `«concept, element, motivation, assessment»` | `Assessment NNNN <Name> «gap, additional, explicit, stereotypes»` | `assessment-NNNN-<name-in-kebab-case>.md` | Known deficiency, limitation, or intentional inaccuracy accepted for later resolution; no solution is implied. |

Requirements Management uses Requirement elements. A concept that satisfies a
Requirement connects to it with a `«realization»` relationship.

## Assessment Validation Definitions

Every Assessment, including an Assessment specialized as `«gap»`, defines several
KPIs and is available for manual validation. Automated validation may supplement
the manual method but is not a prerequisite for evaluating an Assessment.

Each KPI declares:

| Field | Definition |
| --- | --- |
| Name | Stable machine-addressable KPI identifier within the Assessment. |
| Caption | Human-readable description of what is measured. |
| Scale | Maximum value and the meaning of measured values. |
| Target | Explicit comparison using `<`, `>`, or `=` and a value on the declared scale. |
| Dimensions | Every dimension's name and its indexed values; indexes are stable within the Assessment and are not reused for different meanings. |

Each KPI also defines its manual validation method and expected evidence. A
measurement identifies the KPI name, dimension indexes, measured value, and
evidence. Missing evidence is unmeasured, not a passing value or an invented
zero. Assessment definitions are distinct from subsequent measurements and
evaluation results. Dimension combinations outside the scope are identified with
a reason rather than silently counted as passing. Definitions state whether
targets apply per dimension combination and how any aggregation is interpreted.

Dimension values may reference a canonical coverage inventory when the scope
contains indexed record types, rules, or operations; all values must be explicit
before that scope is evaluated. Existing articles without these definitions
remain incomplete for validation until reconciled; historical evidence is
preserved during reconciliation.

These validation definitions are local tailoring, not an additional standard
ArchiMate conformance requirement.

## Hierarchy Groupings

| Abstract Type | Explicit Stereotypes | Implicit Stereotypes | Definition |
| --- | --- | --- | --- |
| `Motivation Element` | `«motivation»` | `«concept, element»` | Context or reason behind architecture design or change. |

## Internal Relationships

| Relationship Stereotypes | From Connector Concept Stereotypes | To Connector Concept Stereotypes |
| --- | --- | --- |
| `«aggregation»`, `«composition»` | `«element, motivation»` | `«element, motivation, same-type»` |
| `«specialization»` | `«element, motivation»` | `«element, motivation, same-type»` |
| `«association»` | `«element, motivation»` | `«element, motivation»` |
| `«influence»` | `«element, motivation»` | `«element, motivation»` |
| `«realization»` | `«outcome»` | `«goal»` |
| `«realization»` | `«principle»` | `«outcome»` |
| `«realization»` | `«requirement»` | `«principle»`, `«outcome»` |

## Relationships With Other Domains

| Relationship Stereotypes | From Connector Concept Stereotypes | To Connector Concept Stereotypes |
| --- | --- | --- |
| `«association»` | `«element, motivation»` | `«element»`, `«relationship»` |
| `«association»` | `«meaning»`, `«value»` | `«concept»` |
| `«assignment»` | `«actor, business»` | `«stakeholder»` |
| `«realization»`, `«influence»` | `«structure, strategy»`, `«behavior, strategy»`, `«structure, active»`, `«structure, passive»`, `«behavior, internal»`, `«service»`, `«grouping»`, `«location»`, `«product»` | `«requirement»` |
| `«realization»`, `«influence»` | `«course-of-action»` | `«outcome»` |
| `«realization»`, `«influence»` | `«work-package»`, `«deliverable»` | `«requirement»` |
| `«aggregation»`, `«composition»` | `«plateau»` | `«requirement»`, `«goal»`, `«outcome»` |
