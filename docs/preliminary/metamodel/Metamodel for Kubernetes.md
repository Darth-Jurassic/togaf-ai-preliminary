# Metamodel for Kubernetes

This profile defines the local Kubernetes stereotype system. The `k8s`
stereotype and every stereotype whose name starts with `k8s-` belong to
Kubernetes practices. Kubernetes
stereotypes are additional explicit stereotypes; they do not replace the
concrete ArchiMate element or relationship stereotype.

## Naming

A Kubernetes high-order explicit stereotype follows the local ArchiMate element
number in a filename. For example, a Kubernetes Namespace Grouping uses
`grouping-NNNN-k8s-namespace-slug.md`. The `NNNN` sequence remains local to
`Grouping`; Kubernetes specializations do not create a separate sequence.

Namespace names follow the adopting project’s explicit naming policy and the
Kubernetes API constraints. This profile imposes no organization prefix, shared
namespace, cluster identity or deployment environment.

## Elements

| Name | `k8s-` stereotype | Implicit Stereotypes | Description |
| --- | --- | --- | --- |
| Kubernetes resource | `«k8s-resource»` | None | General Kubernetes API resource governed by this profile. It is an abstract Kubernetes classification. |
| Kubernetes Course of Action | `«k8s»` | None | Course of Action that defines a Kubernetes platform approach without representing a Kubernetes API resource. |
| Kubernetes namespace Grouping | `«k8s-namespace»` | `«k8s-resource»` | Grouping that aggregates local Kubernetes resources in one namespace. |
| Kubernetes Pod Node | `«k8s-pod»` | `«k8s-resource»` | Node representing one scheduled Kubernetes Pod. |
| Kubernetes cluster Node | `«k8s-node»` | `«k8s-resource»` | Node representing one Kubernetes cluster member. |
| Kubernetes cluster Technology Collaboration | `«k8s-cluster»` | `«k8s-resource»` | Technology Collaboration served by Kubernetes cluster member Nodes. |
| Kubernetes PostgreSQL workload Node | `«k8s-postgresql-workload»` | `«k8s-resource»` | Node representing the PostgreSQL workload resource selected by the installed Kubernetes database operator. |
| Kubernetes certificate Artifact | `«k8s-certificate»` | `«k8s-resource»` | Artifact representing a certificate-manager Certificate resource and its issued certificate material. |
| Kubernetes persistent storage Artifact | `«k8s-persistent-storage»` | `«k8s-resource»` | Artifact representing a PersistentVolumeClaim and the storage it makes available to a Pod. |
| Kubernetes manifest Artifact | `«k8s-manifest»` | `«k8s-resource»` | Artifact containing Kubernetes API resource specifications. |
| Kubernetes Namespace specification Artifact | `«k8s-namespace-specification»` | `«k8s-manifest, k8s-resource»` | Artifact containing one Kubernetes Namespace resource specification. |
| Kubernetes Ingress specification Artifact | `«k8s-ingress-specification»` | `«k8s-manifest, k8s-resource»` | Artifact containing one Kubernetes Ingress resource specification. |
| Kubernetes PersistentVolumeClaim specification Artifact | `«k8s-persistent-volume-claim-specification»` | `«k8s-manifest, k8s-resource»` | Artifact containing one Kubernetes PersistentVolumeClaim resource specification. |
| Kubernetes Pod specification Artifact | `«k8s-pod-specification»` | `«k8s-manifest, k8s-resource»` | Artifact containing one Kubernetes Pod resource specification. |
| Kubernetes Deployment specification Artifact | `«k8s-deployment-specification»` | `«k8s-manifest, k8s-resource»` | Artifact containing one Kubernetes Deployment resource specification. |
| Kubernetes Service specification Artifact | `«k8s-service-specification»` | `«k8s-manifest, k8s-resource»` | Artifact containing one Kubernetes Service resource specification. |
| Kubernetes Certificate specification Artifact | `«k8s-certificate-specification»` | `«k8s-manifest, k8s-resource»` | Artifact containing one cert-manager Certificate resource specification. |
| Kubernetes ClusterIssuer specification Artifact | `«k8s-cluster-issuer-specification»` | `«k8s-manifest, k8s-resource»` | Artifact containing one cert-manager ClusterIssuer resource specification. |
| Kubernetes PostgreSQL Cluster specification Artifact | `«k8s-postgresql-cluster-specification»` | `«k8s-manifest, k8s-resource»` | Artifact containing one CloudNativePG PostgreSQL Cluster resource specification. |
| Kubernetes Secret Artifact | `«k8s-secret»` | `«k8s-resource»` | Artifact representing a Kubernetes Secret resource, with explicit external or Helm initialization/retention ownership. Initialization authority does not imply rotation on upgrade. |
| Kubernetes runner scale-set specification Artifact | `«k8s-runner-scale-set-specification»` | `«k8s-manifest, k8s-resource»` | Artifact containing one GitHub Actions runner scale-set specification. |
| Kubernetes ingress Technology Service | `«k8s-ingress»` | `«k8s-resource»` | Runtime Ingress routing service configured by an Ingress resource; it accepts and routes external traffic through its assigned Technology Interface. |
| Kubernetes Service Technology Interface | `«k8s-service»` | `«k8s-resource»` | Technology Interface representing a Kubernetes Service virtual network endpoint; its Service type, such as ClusterIP, is instance configuration. |
| Kubernetes Helm chart Artifact | `«k8s-helm-chart»` | `«k8s-resource»` | Artifact containing a Helm chart that deploys Kubernetes resources. |
| Kubernetes addon package Artifact | `«k8s-addon-package»` | None | Artifact containing a Kubernetes distribution addon package. |
| Kubernetes addon capability Technology Service | `«k8s-addon»` | `«k8s-resource»` | Technology Service exposed by a Kubernetes distribution addon. |
| Kubernetes controller capability Technology Service | `«k8s-controller»` | `«k8s-resource»` | Technology Service exposed by Kubernetes controller system software. |
| Kubernetes runner scale-set Technology Service | `«k8s-runner-scale-set»` | `«k8s-resource»` | Technology Service representing an organization-scoped GitHub Actions runner scale-set resource. |
| Kubernetes Deployment Technology Service | `«k8s-deployment»` | `«k8s-resource»` | Technology Service representing a Kubernetes Deployment resource that creates and maintains a Pod workload. |
| Kubernetes resource type definition Technology Interface | `«k8s-resource-definition»` | `«k8s-resource»` | Technology Interface defining the contract for a Kubernetes resource type. |

`«k8s»` is valid only on a Course of Action, `«k8s-namespace»` is valid only on a Grouping, `«k8s-pod»` only on a Node,
`«k8s-node»` only on a Node, `«k8s-cluster»` only on a Technology Collaboration, `«k8s-postgresql-workload»` only on a Node, `«k8s-certificate»` only on an
Artifact, `«k8s-persistent-storage»` only on an Artifact, and `«k8s-ingress»`
only on a Technology Service. `«k8s-manifest»` is valid only on an Artifact,
`«k8s-namespace-specification»` only on an Artifact,
`«k8s-ingress-specification»` only on an Artifact,
`«k8s-persistent-volume-claim-specification»` only on an Artifact,
`«k8s-pod-specification»` only on an Artifact,
`«k8s-deployment-specification»` only on an Artifact,
`«k8s-service-specification»` only on an Artifact,
`«k8s-certificate-specification»` only on an Artifact,
`«k8s-cluster-issuer-specification»` only on an Artifact,
`«k8s-postgresql-cluster-specification»` only on an Artifact,
`«k8s-secret»` only on an Artifact,
`«k8s-runner-scale-set-specification»` only on an Artifact,
`«k8s-service»` only on a Technology Interface, and
`«k8s-helm-chart»` is valid only on an Artifact,
`«k8s-addon-package»` only on an Artifact, `«k8s-addon»` only on a Technology
Service, `«k8s-controller»` only on a Technology Service,
`«k8s-runner-scale-set»` and `«k8s-deployment»` only on a Technology Service, and `«k8s-resource-definition»`
only on a Technology Interface.

## Relationships

| `k8s-` stereotype | Implicit Stereotypes | From Stereotypes | To Stereotypes | Description |
| --- | --- | --- | --- | --- |
| `«k8s-scopes»` | `«aggregation»` | `«k8s-namespace»` | `«k8s-resource»` | The namespace aggregates the target Kubernetes resource. |
| `«k8s-hosts-namespace»` | `«association»` | `«k8s-cluster»` | `«k8s-namespace»` | The cluster provides the Kubernetes hosting boundary for the namespace. |
| `«k8s-routes-to»` | `«association»` | `«k8s-ingress»`, `«k8s-service»` | `«interface, technology»` | An Ingress or Kubernetes Service routes its accepted traffic to the target Technology Interface. |
| `«k8s-secures»` | `«association»` | `«k8s-certificate»` | `«k8s-ingress»` | The certificate resource supplies TLS material for the Ingress. |
| `«k8s-stores-data-for»` | `«association»` | `«k8s-postgresql-workload»` | `«k8s-pod»` | The PostgreSQL workload stores persistent data for the Pod. |
| `«k8s-hosts»` | `«composition»` | `«k8s-pod»`, `«k8s-postgresql-workload»` | `«system-software»` | The Pod or database workload hosts the target System Software. |
| `«k8s-mounts»` | `«assignment»` | `«k8s-pod»` | `«k8s-persistent-storage»` | The Pod mounts the PersistentVolumeClaim storage. |
| `«k8s-cluster-member»` | `«composition»` | `«k8s-cluster»` | `«k8s-node»` | A cluster is served by the member Node. |
| `«k8s-subchart»` | `«composition»` | `«k8s-helm-chart»` | `«k8s-helm-chart»` | A parent chart contains a subchart. |
| `«k8s-deploys-to»` | `«association»` | `«k8s-helm-chart»` | `«k8s-namespace»` | A chart deploys resources to the namespace. |
| `«k8s-deploys-resource»` | `«association»` | `«k8s-helm-chart»` | `«k8s-resource»` | A chart deploys the target resource. |
| `«k8s-depends-on»` | `«association»` | `«k8s-helm-chart»` | `«k8s-addon»` | A chart requires the addon service. |
| `«k8s-defines-resource»` | `«assignment»` | `«k8s-resource-definition»` | `«k8s-addon»` | The resource type definition exposes the addon capability service. |
| `«k8s-serves-resource»` | `«association»` | `«k8s-resource-definition»` | `«k8s-resource»` | A resource-type Technology Interface serves a Kubernetes resource that conforms to its API contract. |
| `«k8s-declares-resource»` | `«association»` | `«k8s-manifest»` | `«k8s-resource»` | A Kubernetes manifest declares the target resource. |
| `«k8s-references-resource»` | `«association»` | `«k8s-manifest»` | `«k8s-resource»` | A Kubernetes manifest references the target resource without declaring it. |
| `«k8s-selects-workload»` | `«association»` | `«k8s-service»` | `«k8s-pod»` | A Kubernetes Service selects the target Pod workload. |
| `«k8s-reconciles-resource»` | `«association»` | `«k8s-addon»`, `«k8s-controller»` | `«k8s-resource»` | The addon or controller capability reconciles the target Kubernetes resource. |
| `«k8s-scales-workload»` | `«association»` | `«k8s-runner-scale-set»` | `«k8s-pod»` | A runner scale set creates and scales the target runner Pod workload. |
| `«k8s-deploys-workload»` | `«association»` | `«k8s-deployment»` | `«k8s-pod»` | A Deployment creates and maintains the target Pod workload. |

## Validation

Relationship validation is conjunctive across stereotype systems. A relationship
with `k8s-*` stereotypes must match both a valid ArchiMate relationship rule and
a valid Kubernetes profile row using the effective stereotype stacks of both
endpoints. Passing one system's rules never bypasses another system's rules.

Every relationship incident to a Junction must have the same complete
non-functional relationship stereotype stack. A Junction propagates every
declared relationship stereotype from every registered system, including
ArchiMate and `k8s-*` stereotypes. Its runtime closure resolves the propagated
stereotypes in each owning system while substituting `junction` for the
ArchiMate `relationship` root. Functional stereotypes remain transient and do
not propagate.
