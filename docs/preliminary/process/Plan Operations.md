# Plan Operations

This reference describes contracts, not an installed CLI. If an adopter supplies
`$init` and `$plan` skills, inspect their source and verify that they implement
these contracts. Otherwise execute the equivalent authorized Git operations and
record evidence manually; never claim an unavailable command ran.

## Workspace And Environment

An adopter selects its governing architecture repository identity. Keep its root
worktree on `main`, read-only for tracked content. A governing Plan worktree is a
sibling named with that repository's name followed by a hyphen and the permanent
four-digit Plan number. The nearest governing Plan-directory suffix selects the
Plan, including inside nested governed repositories; branch names do not.

Persistent governed clones live under the root's ignored `repos/` directory,
then owner and repository. Create the governing sibling first, its ignored
`repos/` owner directory next, then linked governed Plan worktrees there from
the persistent clones. Never create a governed checkout without the `repos/`
segment. Work only in the matching nested Plan worktree; do not nest the
governing repository itself under `repos/` or list it as its own governed target.

Before first repository access, declare its Technology Artifact, exact origin,
default branch and intended Plan worktree in the current Plan. Check Git/remote
clients, author identity, authentication, remote permissions, actual default and
Plan refs, local branch/worktree allocation and push readiness without mutating
runtime systems. Declare each remote interface and its canonical CLI installation
guidance. Aggregate missing local capabilities and exact user-run remediation;
do not install, authenticate, escalate privileges or guess runtime targets.

## Assignment And Publication

Assign an existing Plan from the root by creating/reusing its sibling and nested
worktrees on its type-prefixed Plan branch. If the Plan exists only on main,
create local branches from main without pushing unchanged branches. Transfer
explicitly Plan-scoped uncommitted new-Plan records to the sibling without
discarding or publishing unrelated root edits. Use one current Plan per session.

Publication stages the complete local worktree of every affected repository:
tracked changes and all non-ignored untracked files, regardless of authorship.
Inspect for secrets first; a visible secret blocks publication rather than being
silently omitted. Verify no eligible unstaged content remains, run applicable
validation, commit/push and record exact local/remote heads. Push does not grant
merge, deployment, phase advancement or finish authority.

## Coordinated Integration

Integration (optionally named `$plan sew`) keeps the Plan active. Bare selection
includes all affected repositories with the governing architecture repository
last. An explicit repository list restricts refresh/rebase/lease-push/merge/branch
recreation to those repositories; initial complete-worktree publication still
covers all affected repositories. Collect evidence in the governing Plan even
when its repository is not selected, without merging it implicitly.

1. Publish complete worktrees and checkpoint actual remote heads. Refresh selected
   main branches, rebase selected Plan branches and resolve conflicts without
   discarding contributor work. Preserve incoming main's canonical element IDs;
   renumber distinct conflicting local elements by displayed type and repair
   links/companions, preserving original source records.
2. Validate and publish rebased branches with explicit expected-head leases.
   Recheck main/head/checks/mergeability if concurrent work advances; a lease is
   not proof of future mergeability. Do not force over unexpected remote work.
3. Inspect PR templates before creating PRs. Squash-merge selected implementation
   repositories only when authorized and required checks pass. Confirm actual
   merged revisions, refresh their mains and collect mainline evidence into the
   governing model/Plan before its own PR, if selected.
4. Delete merged remote/local source branches and prune. Recreate only the
   selected merged active Plan branches from verified latest mains, preserving
   ignored state, nested repositories and other Plans. Do not discard newly
   appeared uncommitted/unpublished work; stop and reconcile instead.

Do this as one coordinated pass, not another publication round after branch
recreation. No-change repositories need no empty commit/PR. Failure leaves
explicit checkpoints and remaining work, never an invented successful merge.
Refresh the governing root fast-forward-only; no direct-main evidence commit
is implied. Integration does not pass A–H gates or finish a Plan.

## Pause And Finish

Pause publishes complete work, verifies remote preservation and removes only the
current Plan's clean nested worktrees and governing sibling. It does not finish
architecture work or delete the working Plan. Preserve ignored human/runtime
data and unpublished changes; do not remove a worktree containing them blindly.

## Identity-Only Housekeeping Exception

A stakeholder-directed rearrangement of existing Plan identities, placement or
references is one session and one groom publication, with substantive scope,
decisions, questions, concerns, completions and evidence preserved. This narrow
exception uses the governing root on main rather than creating a new Plan or
worktree; it overrides the usual root-read-only, assignment, numbered groom and
phase-session rules only for that identity/reference work. Register the session
ingest directly. Substantive architecture, implementation or runtime changes
still require normal governance.

Before correcting a duplicate number, fetch refs and inspect all Plan/branch/
worktree allocations, including unpublished records. Choose the next number
above every allocation, preserve the old-to-new mapping and update filenames,
titles, links and affected branch/worktree identities coherently without
publishing unrelated unpublished work. Publish directly to main only when
permitted and authorized; if a PR is required, use one temporary groom branch,
squash-merge, delete/prune it and fast-forward local main. Do not invent another
Plan or worktree for this identity-only exception.

## Finish Conditions

Finish requires explicit authority, all applicable scope/gates complete, no
remaining work, durable canonical definitions/evidence, delivered affected
repositories and updated successor dependencies. Publish, squash-merge and
verify all required delivery; delete the completed working Plan and resolved
temporary Preliminary blockers through that governed publication. Delete/prune
completed source branches and remove only verified-safe Plan worktrees. Never
treat a push or scoped acceptance as whole-Plan completion.
