# Agent Instructions

## Scope And Safety

- This is an unbranded architecture-method reference. Do not introduce an
  organization's product, domain, tenant, runtime or deployment policy as a
  universal rule. Discuss concrete naming first and record an adopter-owned
  Preliminary decision.
- On Windows use PowerShell for Java tasks; on Linux/WSL use Bash. Do not select
  a particular WSL distribution for an adopter.
- Keep Java/Gradle files strictly within the repository's `java/` directory.
- Do not run actions requiring root access. Supply exact commands for the user
  to review and execute; never supply unresolved command placeholders/prompts.
- Preserve unfamiliar edits and unpublished work. Do not discard another
  contributor's changes or bypass required repository checks.
- Treat `ref-` directories and `docs/ingests/refs/` as immutable authorities. Do
  not create, edit, rename, delete or format files in those reference trees.
- Store project-local skills under `tools/skills/`, with each skill's
  instructions in its own `SKILL.md` and supporting files alongside it. A command
  mentioned in these documents is not proof that its skill is installed.
- Inspect accessible implementation repositories at the exact selected source
  and runtime revisions. Help output, wrapper names and guessed contracts are
  not substitutes for source evidence.

## Documentation

- Process definitions: `docs/preliminary/process/`; metamodel definitions:
  `docs/preliminary/metamodel/`; canonical architecture: `docs/model/`;
  source signals: `docs/ingests/`; working Plans: `docs/plans/`.
- Start with the [Process index](docs/preliminary/process/index.md),
  [Preliminary process](docs/preliminary/process/Process%20for%20Preliminary.md),
  [Model process](docs/preliminary/process/Process%20for%20Model.md),
  [Human ingests](docs/preliminary/process/Process%20for%20Human%20Ingests.md) and
  [Metamodel index](docs/preliminary/metamodel/index.md). Then read the selected
  A–H phase process and relevant metamodels, not every phase by default.
- Follow their placement, naming, article, evidence, relationship, layer,
  priority, quality-gate, application and reconciliation rules. `docs/togaf/`
  contains compatibility pointers, not competing active definitions.
- Keep one canonical Markdown article per element. Diagrams are projections of
  documented elements/relationships, never independent sources of truth.
- Preserve Markdown companion files in a sibling same-base-name directory;
  rename companions and links coherently.
- The profile is informed by ArchiMate 4 and TOGAF 10, with explicitly local
  extensions. Do not claim standards conformance from these documents alone.
- Keep MIT licensing intact. External standards retain their separate rights;
  link to their public authority rather than redistributing downloaded extracts.

## Plan And Repository Governance

- Keep Plans as `docs/plans/plan-NNNN-slug.md`; the four-digit number is permanent.
  Declare `- Type: feature`, `fix` or `groom` below the title. Plans are editable
  working records without a Plan-wide Status field.
- A feature creates/improves capability; a fix repairs claimed-ready capability
  through existing Work Packages; a groom changes governance or records only.
- Metamodel, process, skill and AGENTS changes are implicit Preliminary grooms
  on the current Plan, regardless of its original aim. Do not create another
  Plan while one is current unless the user explicitly requests one.
- Only without a current Plan, start the applicable temporary
  `docs/plan.metamodel.md` or `docs/plan.process.md` and numbered groom Plan.
  Resolve Preliminary blockers before dependent model work.
- Follow [Plan Operations](docs/preliminary/process/Plan%20Operations.md) for
  directory-based Plan binding, nested `repos/` worktrees, environment checks,
  publication, coordinated integration, pause and finish. This repository does
  not ship `$init`/`$plan` skills; do not pretend to invoke missing automation.
- Declare every affected repository through its Technology Artifact and the
  current Plan before accessing it. Verify tools, identity, authentication,
  exact remotes, permissions and branch readiness first.
- Work only in matching Plan worktrees. Keep the governing root on `main`,
  read-only for tracked content; persistent governed clones live under its
  ignored `repos/` tree, not directly beneath an owner directory.
- Publication covers every tracked and non-ignored untracked file in affected
  worktrees, regardless of authorship. Git-visible secrets block publication;
  do not silently omit them and deliver a partial tested worktree.
- Squash-merge PRs, delete merged source branches, prune remote refs and delete
  matching completed local branches. Do not merge/deploy/finish without authority.
- Explicitly requested identity-only Plan housekeeping follows the narrow
  one-session root-worktree exception in Plan Operations. Preserve substantive
  content and unpublished work; do not use that exception for implementation.

## Session Initiation And Reasoning

- Resolve the Plan from the nearest governing Plan worktree's directory suffix,
  including from inside `repos/`; never infer it from a branch or recent edit.
- Read `AGENTS.md` and any open Preliminary blocker Plans first. Register each
  new AI session directly as one source ingest before treating it as model input.
  Do not create a Plan solely to register an ingest.
- Read the selected Plan in full and related Plans touching its capability or
  Work Package. Inspect A–H Completion records for the requested scope; absent
  scope means the whole Plan.
- Select the earliest unfinished phase: missing Completion, `Complete: no`,
  missing verification, unresolved prerequisites or contradicted evidence mean
  unfinished. State the Plan, phase and concrete remaining result to the user.
- Dedicate the session to that phase. On completion report the next unfinished
  phase for the next session; do not advance automatically. Explicit redirection
  requires verification of the selected scope's preceding gates.
- If all phases are complete, report remaining finish conditions; do not invent
  a new discussion phase. Publication never proves architecture completion.
- Compatible earlier-phase refinements do not automatically switch the active
  phase: record phase-owned Questions/Concerns, reconcile canonical definitions,
  traces and Work Package coverage, revalidate affected prerequisites, then resume
  authorized independent/dependent work as appropriate. Material scope changes
  require explicit replanning, not a claim that they are minor.
- During planning update canonical baseline/target definitions and the Plan only;
  do not change implementation code, deployments, tests or runtime artifacts.
- Enter Implementation Governance only after the relevant planning gates pass.
  Implement/test/deliver within authority, reverse-deliver durable evidence to the
  owning layers, then evaluate Assessments in Architecture Change Management.
- Before plugin changes, inspect host source/runtime provenance, document
  host-owned calls/hooks and loading/lifecycle contracts, and establish contract
  observability. Missing evidence blocks dependent changes; helper tests alone
  do not establish host compatibility.

## Gates, Questions And Evidence

- Every A–H section has Completion with `- Complete: yes` or `no` and
  `- Verification:` linking actual gate evidence or identifying unfinished work.
- A defines Motivation/Strategy and Assessment criteria; B defines Business;
  C defines Application/data; D defines Technology, each with valid upstream
  traces. E checks realization/feasibility; F associates Work Packages with all
  relevant Business tests and Application/Technology implementation targets;
  G implements and reverse-delivers evidence; H evaluates Assessments.
- Questions/Concerns belong to the phase responsible for resolving them. Use
  independent stable AQ/AC through HQ/HC sequences, retain resolved rows and
  old-to-new ownership mappings, and cite active IDs on blocked actions.
  `Blockers` contains predecessor/successor dependencies, not a flat issue list.
- Block only dependent work; independent scopes still pass their own gates.
  Agents resolve routine evidence questions; humans own intent, unavailable
  information, policy exceptions and accountable risk acceptance.
- When a stakeholder catches an instruction breach, preserve its exact source,
  violated instruction, UTC date, current Plan and unique event ID with increment
  one in an adopter-owned durable breach ledger linked to its Assessment. Do not
  count repeated discussion as another occurrence or erase an event after a fix.
  A rolling last-seven-UTC-calendar-days KPI sums increments with target zero;
  missing retrospective coverage is not a verified zero. This reference ships
  no tenant-specific ledger, Assessment or incident history.
- Keep unfinished Plans. Before authorized finish, move durable definitions and
  evidence out of the working Plan, update successor dependencies and verify
  delivery/cleanup conditions. Later Plans depend on durable results, not an
  invented sequence of phase Plans.
