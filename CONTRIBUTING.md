# Contributing to OpenFeature

[![Sign-up](https://img.shields.io/static/v1?label=Sign-up&message=for%20news&color=blue)](https://bit.ly/openfeature-signup)
[![a](https://img.shields.io/badge/slack-%40cncf%2Fopenfeature-brightgreen?style=flat&logo=slack)](https://cloud-native.slack.com/archives/C0344AANLA1)
[![Roadmap](https://img.shields.io/static/v1?label=Roadmap&message=public&color=green)](https://github.com/orgs/open-feature/projects/1)
[![Governance](https://img.shields.io/static/v1?label=Governance&message=bootstrap&color=yellow)](https://github.com/open-feature/governance)
[![Code of Conduct](https://img.shields.io/badge/Contributor%20Covenant-2.1-4baaaa.svg)](https://github.com/open-feature/.github/blob/main/CODE_OF_CONDUCT.md)

## Contacting us

We hold regular meetings which you can see [here](https://github.com/open-feature/community/#meetings-and-events).

We are also present on the `#openfeature` channel in the [CNCF slack](https://slack.cncf.io/).

## Contributor ladder

Are you interested in contributing on a regular basis?
Check out our [contributor ladder](https://openfeature.dev/community/CONTRIBUTOR_LADDER).

## Project governance

Project governance is documented [here](https://github.com/open-feature/community/blob/main/governance-charter.md).

## Repository requirements

We require repositories in the project adhere to some security and maintenance guidelines.
They are primarily inspired by recommendations from the [Cloud Native Security Controls Catalog](https://www.cncf.io/blog/2022/06/07/introduction-to-the-cloud-native-security-controls-catalog/).
Adherence to these guidelines is required for 1.0 artifact releases, to the satisfaction of the [Technical Steering Committee](https://github.com/open-feature/community/blob/main/governance-charter.md#technical-steering-committee-tsc).

| Requirement                                    | Recommended solution(s)                                                                                                                   | Notes                                                       |
| ---------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------- |
| automated publishing                           | github actions (with permissions applying principle of least privilege), language-specific tools (Maven, nuget, NPM, etc)                 | required                                                    |
| container, base image scanning                 | [snyk][snyk], [trivy][trivy]                                                                                                              | required                                                    |
| code ownership                                 | branch protection rules\* and CODEOWNERS files                                                                                            | required                                                    |
| dependency analysis                            | [snyk][snyk]                                                                                                                              | required                                                    |
| dependency auto-updates                        | [Renovate][renovate]\*\*, [Dependabot][dependabot]                                                                                        | required                                                    |
| semantic versioning, changelogs                | [Semantic Versioning][semantic-versioning], [Conventional Commits][conventional-commits], [Release Please][release-please]\*\*\*          | required                                                    |
| unit, integration testing                      | github actions (with permissions applying principle of least privilege), language-specific tools (JUnit, Jest, etc), [Cucumber][cucumber] | required, with coverage metrics up to maintainer discretion |
| signing (binaries, packages, container images) | language-specific tools, [cosign][cosign]                                                                                                 | recommended, where supported                                |
| fuzzing                                        | [ClusterFuzzLite][clusterfuzzlite], [OSS-Fuzz][oss-fuzz]                                                                                  | recommended                                                 |
| helpful readme file                            | See [example README.md](./templates/READMEs/README.md)                                                                                    | recommended                                                 |
| provenance                                     | [SLSA](https://slsa.dev/spec/v1.0/provenance#provenance)                                                                                  | recommended                                                 |
| SBOM generation                                | [CycloneDX][cyclonedx], [SPDX][spdx], [syft][syft]                                                                                        | recommended                                                 |
| static analysis                                | [SonarCloud][sonarcloud], language-specific tools (SpotBugs, eslint)                                                                      | recommended                                                 |

## Developer Certificate Of Origin

The [Developer Certificate of Origin (DCO)](https://developercertificate.org/) is a lightweight way for contributors
to certify that they wrote or otherwise have the right to submit the code they are contributing to the project.

Contributors to the OpenFeature project sign-off that they adhere to these requirements by adding a `Signed-off-by` line to commit messages.

```console
This is my commit message

Signed-off-by: John Doe <JohnDoe@somewhere.org>
```

Git even has a `-s` command line option to append this automatically to your commit message:

```console
git commit -s -m 'This is my commit message'
```

If you have already made a commit and forgot to include the sign-off, you can amend your last commit
to add the sign-off with the following command, which can then be force pushed.

```console
git commit --amend -s
```

\* Branch protection rules should protect the primary branch (usually `main`) by requiring code review from the appropriate parties (other than the author), usually expressed in a CODEOWNERS file.

\*\* We recommend Renovate over Dependabot because of it's group and auto-merge features.
Additionally, we have an org-wide base config for Renovate.

\*\*\* Release Please isn't strictly necessary, but combined with [Conventional Commits][conventional-commits], it provides a simple yet robust means of generating useful, accurate changelogs and releasing semantically versioned artifacts.

[sonarcloud]: https://www.sonarsource.com/products/sonarcloud/
[snyk]: https://snyk.io/
[trivy]: https://github.com/aquasecurity/trivy
[cosign]: https://github.com/sigstore/cosign-installer
[cyclonedx]: https://cyclonedx.org/tool-center/
[clusterfuzzlite]: https://google.github.io/clusterfuzzlite/
[oss-fuzz]: https://github.com/google/oss-fuzz
[cucumber]: https://cucumber.io/tools/cucumber-open/
[renovate]: https://github.com/apps/renovate
[syft]: https://github.com/anchore/syft
[spdx]: https://spdx.dev/resources/tools/
[dependabot]: https://github.com/dependabot

[conventional-commits]: [https://www.conventionalcommits.org/]
[semantic-versioning]: [https://semver.org/]
[release-please]: [https://github.com/googleapis/release-please]

### "Contrib" repositories

Along with SDK repositories, we also maintain "contrib" repositories for most of our supported languages.
These repositories are "monorepos" that house community contributions which are extensions to, or integrations with, the base SDKs.
Examples include providers, hooks and framework-specific SDKs.
In addition to the normal [repository requirements](#repository-requirements) (many of which are already implemented for all packages in each monorepo), components must each have _at least_ one user specified the `component_owners.yml` (see https://github.com/dyladan/component-owners for more). It's the responsibility of the `component_owner(s)` to:

- review and resolve issues pertaining to their component
- review and resolve pull requests pertaining to their component, including automated pull requests from dependabot, etc
- review releases PRs for new versions of their component
- alert the [Governance Board or Technical Committee](https://github.com/open-feature/community/blob/main/community-members.md#technical-committee) if they're no longer interested or able to fulfill the preceding requirements

Consistent and prolonged failure to satisfy the above requirements may result in archival and deprecation of the component in question.
