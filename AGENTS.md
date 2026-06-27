# Agent Instructions

- When working on Windows:
  - For Java-related tasks, use PowerShell.
  - All Java/Gradle-related files (build scripts, wrappers, properties, etc.) MUST be kept strictly within the `<repo>/java` folder.
  - Do not move Gradle files to the repository root.
  - For other tasks that require WSL, use the `binario.one` distro.
- Inside WSL or when working on Linux, use bash.
- Do not run privileged actions that require root access. Write privileged
  commands to the output for the user to review and run.
- Markdown documents may be accompanied by externally linked files. By default,
  keep companion files in a sibling directory with the same base name as the
  Markdown file. For example, companion files for `<name>.md` live in `<name>/`.
  Rename related files coherently when the document or companion set is renamed.
- Treat directories whose names start with `ref-` as read-only reference
  material. Do not modify files inside those directories.
- Keep project-local Codex skills under `.tools/skills/`. Each skill should
  live in `.tools/skills/<skill-name>/SKILL.md` with any supporting scripts,
  references, or assets stored inside that skill directory.

## Documentation

Documentation is governed by TOGAF under `docs/togaf/`.

- The documentation layout is described in this file (AGENTS.md).
- The repository file layout and phase placement rules are described in [TOGAF Process](docs/togaf/0%20-%20Preliminary/TOGAF%20Process.md) and [Metamodel](docs/togaf/0%20-%20Preliminary/Metamodel.md).

Start with this Preliminary record:

- [TOGAF Process](docs/togaf/0%20-%20Preliminary/TOGAF%20Process.md)

Use the Preliminary metamodels for placement, naming, article structure,
evidence, relations, and phase-specific element rules:

- [Metamodel](docs/togaf/0%20-%20Preliminary/Metamodel.md)
- [Metamodel for A](docs/togaf/0%20-%20Preliminary/Metamodel%20for%20A.md)
- [Metamodel for B](docs/togaf/0%20-%20Preliminary/Metamodel%20for%20B.md)
- [Metamodel for C Application](docs/togaf/0%20-%20Preliminary/Metamodel%20for%20C%20Application.md)
- [Metamodel for C Data](docs/togaf/0%20-%20Preliminary/Metamodel%20for%20C%20Data.md)
- [Metamodel for D](docs/togaf/0%20-%20Preliminary/Metamodel%20for%20D.md)
- [Metamodel for E](docs/togaf/0%20-%20Preliminary/Metamodel%20for%20E.md)
- [Metamodel for F](docs/togaf/0%20-%20Preliminary/Metamodel%20for%20F.md)
- [Metamodel for G](docs/togaf/0%20-%20Preliminary/Metamodel%20for%20G.md)
- [Metamodel for H](docs/togaf/0%20-%20Preliminary/Metamodel%20for%20H.md)
- [Metamodel for RM](docs/togaf/0%20-%20Preliminary/Metamodel%20for%20RM.md)

## Change Process

When a change is requested:

1. **Propose first** — discuss what needs to change in the docs. Do not update anything without an explicit command to do so.
2. **Update docs only after discussion** — once discussion settles, apply doc changes. The code stays untouched during this phase.
3. **Then update code** — implement the described concepts. The only doc change allowed at this stage is updating **Evidence Target** fields to show what code implements the described concepts.
