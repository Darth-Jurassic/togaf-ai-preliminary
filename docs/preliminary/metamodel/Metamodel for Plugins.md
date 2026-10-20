# Metamodel for Plugins

This profile defines in-process plugin extension roles. It owns the `plugin`
stereotype and every lowercase kebab-case stereotype beginning with `plugin-`.
A plugin is not independent System Software: its host loads and executes it in
the host's process.

## Elements

| Role | Allowed ArchiMate element | Explicit stereotypes | Definition |
| --- | --- | --- | --- |
| Plugin | Application Component | `«component, application, plugin»` | In-process extension composed by its host System Software. It adapts to the host's lifecycle, permissions, errors, and API behavior. |
| Plugin API | Technology Interface | `«interface, technology, plugin-api»` | Host-owned technology contract through which a plugin may call host capabilities. |
| Plugin API | Application Interface | `«interface, application, plugin-api»` | Host-owned application contract that a plugin may implement for the host to invoke. |
| Plugin call | Application Process | `«process, application, plugin-call»` | Plugin-controlled attempt to call a host-owned Plugin API. The host controls acceptance, result, and error behavior; the plugin handles those outcomes. |
| Plugin hook | Technology Process | `«process, technology, plugin-hook»` | Host-controlled invocation of a plugin through a host-owned Plugin API. The host controls whether and when it invokes the hook and defines the contract expectations. |

`«plugin-api»` describes a contract owned by the host, not by the plugin. A host
may offer its technology API to plugins or invoke plugin implementations through
its application API. These are separate contract directions and are not inferred
to realize one another.

## Relationships

| Relationship Stereotypes | From Connector Concept Stereotypes | To Connector Concept Stereotypes | Meaning |
| --- | --- | --- | --- |
| `«composition»` | `«system-software»` | `«component, application, plugin»` | Host composes the in-process plugin; the plugin has no separate host process. |
| `«composition»` | `«system-software»` | `«interface, technology, plugin-api»`, `«interface, application, plugin-api»` | Host owns its Plugin API contracts. |
| `«realization»` | `«component, application, plugin»` | `«interface, application, plugin-api»` | Plugin implements the host-owned hook contract. |
| `«assignment»` | `«component, application, plugin»` | `«process, application, plugin-call»` | Plugin performs its controlled host-call process. |
| `«serving»` | `«interface, technology, plugin-api»` | `«process, application, plugin-call»` | Host API serves the plugin-controlled call. |
| `«association»` | `«process, technology, plugin-hook»` | `«interface, application, plugin-api»` | Host hook process invokes the plugin implementation through the host-owned API. |

The host must not be modeled as an external caller of a plugin. The host defines
the contract and controls host-call responses and hook invocation; the plugin
adopts those behaviors.
