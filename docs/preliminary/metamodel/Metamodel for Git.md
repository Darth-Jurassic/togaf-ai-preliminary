# Metamodel for Git

This profile defines repository Artifact stereotypes for Git-based source and
configuration repositories. Every stereotype whose name starts with `git-`,
`github-`, `gitlab-`, or `ado-` belongs to this Git profile.

## Repository Artifacts

| Name | Git stereotype | Implicit Stereotypes | Description |
| --- | --- | --- | --- |
| Git repository Artifact | `«git-repository»` | None | Vendor-neutral Git repository Artifact. |
| GitHub repository Artifact | `«github-repository»` | `«git-repository»` | Git repository hosted by GitHub. |
| External GitHub repository Artifact | `«github-external-repository»` | `«github-repository»`, `«git-repository»` | GitHub repository governed outside the adopting project’s governance boundary. |
| GitLab repository Artifact | `«gitlab-repository»` | `«git-repository»` | Git repository hosted by GitLab. |
| Azure DevOps repository Artifact | `«ado-repository»` | `«git-repository»` | Git repository hosted by Azure DevOps. |

These stereotypes are valid only on an ArchiMate Artifact. A GitHub repository
Artifact name uses the canonical `github-owner/repository` form, for example
`owner/repository`; its filename normalizes the owner and repository name
to lowercase kebab case after the Artifact sequence.

## Validation

`«github-repository»`, `«gitlab-repository»`, and `«ado-repository»` each imply
`«git-repository»`. Repository host evidence must identify the selected hosting
stereotype; do not infer a host from a repository name alone.

`«github-external-repository»` implies `«github-repository»` and marks a
repository whose governance remains outside the adopting project’s governance boundary. Its Location
Composition records that external origin. It may be referenced as an upstream
or contribution target, but it is not a governed `$plan sew` target.
