# Directory Structure

## Context

This record defines the canonical directory structure of the repository.

This is an adoption contract, not an inventory of files shipped by this reference.
Only Preliminary definitions and compatibility pointers are supplied here. Select
implementation stacks and their packaging/build/deployment policies explicitly;
the stack layouts below are reusable conventions, not evidence of installed
tooling, a selected production stack or existing scripts.

## Layout

Repository root keeps only cross-stack files. Each technology stack owns its
sources, package-manager configuration, build configuration, and workspace
metadata below its dedicated child directory.

Each adopting project owns its repository ignore/template baseline. Record any
shared baseline authority explicitly instead of assuming a central vendor repository.

### `docs/`

Architecture documentation is organized by immutable external authorities, local
process and metamodel definitions, canonical model elements, and raw knowledge
ingests.

Target documentation layout:

```text
docs/
├── preliminary/
│   ├── process/
│   └── metamodel/
├── model/
│   ├── strategy/
│   ├── common/
│   ├── motivation/
│   ├── business/
│   ├── application/
│   ├── technology/
│   └── implementation-and-migration/
├── plans/
└── ingests/
    ├── refs/
    │   └── <authority>/
    ├── ideas/
    ├── discussions/
    ├── helpdesk/
    ├── telemetry/
    ├── logs/
    ├── news/
    ├── research/
    ├── interviews/
    └── regulations/
```

- `ingests/refs/` — immutable downloaded external authorities. Do not create,
  edit, move, rename, delete, or format files in this directory. Each reference
  keeps its original form; the relevant Preliminary index records its original
  URL and intake into local definitions.
- `preliminary/process/` — local process, governance, repository, TOGAF 10 ADM,
  SAFe, and lean learning-loop definitions.
- `preliminary/metamodel/` — local metamodel, notation, placement, and
  layer-specific modeling definitions.
- `model/` — canonical ArchiMate element articles, organized by ArchiMate layer.
- `ingests/` — source knowledge signals folded by ingest channel; other than
  the immutable `ingests/refs/` authorities, these records are learning-loop
  inputs, not canonical ArchiMate elements.

Legacy `docs/togaf/` paths are historical and noncanonical. Active process and
metamodel definitions belong under `docs/preliminary/`; canonical elements
belong under `docs/model/`. Do not create new records under legacy paths.

### `dotnet/`

All projects and code that run on .NET.

- `.slnx` files, `global.json`, `Directory.Build.*`, and
  `Directory.Packages.props` belong here.
- `dotnet/<Repo.Name>.slnx` is the only .NET solution and aggregates every .NET
  project in the repository.

- `launchers/` — binary applications; select archive/publication targets in the
  adopting project's build contract
- `shared/` — same-repository reusable libraries with no standalone publication
- `tests/` — test projects executed for commits, pull requests, tags, and manual
  plays
- `nugets/` — publishable NuGet packages, using the selected packaging contract
- `tools/` — projects published as .NET tools

### `node/`

All projects and code that run on Node.js.

- `pnpm-workspace.yaml` belongs here.

- `launchers/` — packages run via `npx`
- `web/` — web frontend packages (built with Vite)
- `shared/` — packages consumed only by other packages in this repository
- `npms/` — packages published to npm (built with pnpm and Vite)
- `tests/` — test packages

### `java/`

Kotlin-first Java-family projects. Gradle is both its package manager and build
system.

### `docker/`

Dockerfiles only. Declare and inspect the actual build entrypoint before use;
this reference ships no image build script or deployment policy.

### `kubernetes/`

Kubernetes deployment sources, primarily Helm charts.

## Links

- [Product Development Process Definition](Product%20Development%20Process%20Definition.md)
