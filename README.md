# TOGAF AI Preliminary

Reusable, unbranded architecture Preliminary processes, metamodel definitions and
agent guidance. TOGAF 10 ADM supplies the process frame; ArchiMate 4 informs the
local modeling profile. These documents are local tailoring, not certification
of standards conformance or a redistribution of the standards.

## Start Here

- [Agent instructions](AGENTS.md)
- [Process index](docs/preliminary/process/index.md)
- [Metamodel index](docs/preliminary/metamodel/index.md)
- [Directory structure](docs/preliminary/process/Directory%20Structure.md)
- [Plan operations and adoption](docs/preliminary/process/Plan%20Operations.md)
- [Continuous Requirements Management](docs/preliminary/process/Requirements%20Management.md)

The processes cover Preliminary, A–H, scoped delivery iterations, evidence-led
gates, source ingests, learning loops and Work Package delivery. The metamodel
defines domain elements, typed relationships, globally owned stereotypes,
declared/implicit/runtime/functional semantics and tenant-origin validation, plus
AI, Git, Kubernetes and plugin profiles.

## Adoption

Use these definitions as shared guidance or copy them into an adopting
architecture repository. Define that project's purpose, ownership, repository
identity and permitted operations explicitly. No company, product, tenant,
namespace prefix, hostname, WSL distribution or production stack is selected.

Do not add concrete product or brand naming rules without first discussing the
naming model. Record agreed naming in a dedicated Preliminary record.
`$init` and `$plan` are optional integration command names, not automation shipped
by this repository; Plan Operations documents the required manual contracts.

The previous `docs/togaf/0 - Preliminary/` URLs remain as migration pointers.
Active definitions are now under `docs/preliminary/`; architecture elements
belong by layer under `docs/model/`, not in duplicate ADM phase folders.
See the [migration guide](docs/preliminary/Migration.md) for semantic changes.

No concrete architecture model, Plan, source ingest, private evidence, deployment
configuration or downloaded external reference is included. Source-specific
audit/legacy inventories and a standards diagram were intentionally not exported.

## License And Authorities

Repository-authored guidance is covered by the existing [MIT license](LICENSE).
TOGAF and ArchiMate are The Open Group trademarks; external specifications and
figures remain subject to their own copyrights and terms, not this MIT license.
The authority sites may require authentication or separate access acceptance;
their availability is not needed to use this self-contained local profile.

- [TOGAF Standard](https://pubs.opengroup.org/togaf-standard/)
- [ArchiMate 4 reference](https://pubs.opengroup.org/architecture/archimate4-doc/)
