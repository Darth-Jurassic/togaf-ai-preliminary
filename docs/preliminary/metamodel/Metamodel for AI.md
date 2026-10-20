# Metamodel for AI

This profile defines local artificial-intelligence stereotype roles. Every
lowercase kebab-case stereotype whose name begins with `ai-` belongs to this AI
profile. The profile classifies existing ArchiMate concepts; it does not create
an additional storage class or replace the concept's defining element type.

## AI Concepts

| AI concept | Allowed ArchiMate concept | AI stereotype | Description |
| --- | --- | --- | --- |
| AI model | System Software | `«ai-model»` | System software that receives input and produces generated output through a trained model. |
| AI agent | System Software | `«ai-agent»` | System software that coordinates an AI model, context, and tools toward a delegated objective. |
| AI tool | Technology Interface | `«ai-tool»` | Umbrella Technology Interface that exposes an operation an AI agent may invoke. |
| AI MCP server | Technology Interface | `«ai-mcp-server»` | MCP Technology Interface that exposes tools to an AI agent. Implies `«ai-tool»`. |
| AI context | Data Object | `«ai-context»` | Data object supplied to an AI model or agent as bounded task context. |

`«ai-model»` and `«ai-agent»` may be declared together only when the same System
Software both provides model inference and performs agent orchestration.
`«ai-mcp-server»` implies `«ai-tool»`. An `«ai-tool»` Technology Interface
remains an interface to its existing Technology Service; the stereotype does not
imply ownership of that service. An `«ai-context»` Data Object describes supplied
information, not a prompt, conversation transcript, model weight, credential, or
generated result unless its owning model separately establishes that meaning.

## Relationships

AI roles use their owning ArchiMate concept's relationship rules. The profile
adds no relationship stereotype or execution semantics.

| Relationship | From | To | Meaning |
| --- | --- | --- | --- |
| `«serving»` | `«ai-tool»` Technology Interface | `«ai-agent»` System Software | The interface supplies tool operations to the agent. An `«ai-mcp-server»` uses this relationship through its implicit `«ai-tool»` stereotype. |

No direct AI-profile relationship is defined between an `«ai-agent»` and an
`«ai-context»`; model their information use through the owning ArchiMate concept
and its applicable relationship rules.

## Validation

- Every declared AI stereotype must begin with `ai-` and be lowercase kebab case.
- `«ai-model»` and `«ai-agent»` are valid only on System Software.
- `«ai-tool»` is valid only on a Technology Interface.
- `«ai-mcp-server»` is valid only on a Technology Interface and implies
  `«ai-tool»`.
- `«ai-context»` is valid only on a Data Object.
- An AI stereotype augments but never replaces the concept's required defining
  and domain stereotypes.
