# Contributing to OpenFeature

[![Sign-up](https://img.shields.io/static/v1?label=Sign-up&message=for%20news&color=blue)](https://bit.ly/openfeature-signup)
[![a](https://img.shields.io/badge/slack-%40cncf%2Fopenfeature-brightgreen?style=flat&logo=slack)](https://cloud-native.slack.com/archives/C0344AANLA1)
[![Roadmap](https://img.shields.io/static/v1?label=Roadmap&message=public&color=green)](https://github.com/orgs/open-feature/projects/1)
[![Governance](https://img.shields.io/static/v1?label=Governance&message=bootstrap&color=yellow)](https://github.com/open-feature/governance)
[![Code of Conduct](https://img.shields.io/badge/Contributor%20Covenant-2.1-4baaaa.svg)](https://github.com/open-feature/.github/blob/main/CODE_OF_CONDUCT.md)

## Contacting us

We hold regular meetings which you can see [here](https://github.com/open-feature/community/#meetings-and-events).

We are also present on the `#openfeature` channel in the [CNCF slack](https://slack.cncf.io/).

## Project governance

Project governance is documented [here](https://github.com/open-feature/community/blob/main/governance-charter.md).

## How to contribute

All the OpenFeature repositories follow these guidelines.

### Issues

Issues are the heartbeat of open source projects. There are mainly three kinds of issues you can open:

* Bug : If you believe you found a problem in a project, and you want to discuss and get it fixed,
  creating an issue with the **bug template** is the best way to do so.
* Documentation: Do want to improve the documentation? did you find a typo? This is the issue for you.
* Feature: Would you like a new feature to be added to OpenFeature? This is the kind of issue you'll need then.
  Please do your best at explaining your intent. It's always important that others can understand what you mean in order to discuss.
  Be open and collaborative in letting others help you get things done!
* Report a security vulnerability: Did you find a vulnerability? This issue kind is for triaging such problems!

The best way to **get involved** in the project is through issues. You can help in many ways:

* Issues triaging: participating in the discussion and adding details to open issues is always a good thing;
sometimes issues need to be verified, you could be the one writing a test case to fix a bug!
* Helping to resolve the issue: you can help in getting it fixed in many ways, more often by opening a pull request.

### Triaging

We need help in categorizing issues. Thus any help is welcome!

When you triage an issue, you:

* assess whether it has merit or not

* quickly close it by correctly answering a question

* point the reporter to a resource or documentation answering the issue

* tag it via labels, projects, or milestones

* take ownership submitting a PR for it, in case you want

#### More about labels

These guidelines are not set in stone and are subject to change.

Each repository has its own set of labels. Here is the current [label set](https://github.com/open-feature/spec/labels) for the spec repository.

### Pull Requests

Thanks for taking the time to make a [pull request](https://help.github.com/articles/about-pull-requests) (hereafter PR).

The PR template is there to guide you through the process of opening it.

Also, feel free to suggest a reviewer with `/cc @theirname`, or to assign an assignee using `/assign @nickname`.

Once your reviewer is happy, they will leave a comment and or approve the pull request.

Your PR will be ready to merge once 2 reviewers have approved it and it has passed all the tests.

### Resolving Conflicts by Rebasing

When submitting a pull request, it's important to make sure that it can be cleanly merged into the upstream repository. In some cases, conflicts may arise when attempting to merge a pull request, such as when changes have been made to the same file or lines of code.

To resolve conflicts, we always use the `git rebase` command rather than git merge. This helps to ensure a clean and linear history of commits.

First of all we take for granted some assumptions:

- the contributor is using a **fork**

- the default branch is `main`

Here's the process for rebasing a pull request to resolve conflicts:

1. Ensure that your local repository is up to date with the upstream repository:

```
git checkout -b my-feature-branch
git pull
git remote add upstream <upstream_repository_url>
git fetch upstream
```

2. Start the rebase process interactively (`-i`):

```
git rebase --signoff -i upstream/main
```

3. If there are conflicts, resolve them and then continue the rebase process:

```
git add <file-that-conflicts>
git rebase --continue
```
4. Repeat the above step for each conflict.

5. Push your changes back to your forked repository with `--force-with-lease`:

```
git push --force-with-lease
```
   Furthermore, to force the update of a branch with your local changes, you can use the `--force` flag with the git push command. This flag overwrites the remote branch's current state with your local changes, and this can cause problems if other contributors have made changes to the same branch. Because of that, we strongly reccomend to use the `--force-with-lease` flag that is a safer alternative to the `--force` flag. It allows you to force the update of a branch with your local changes, but only if the branch on the remote repository is in the same state as you expect. In other words, the `--force-with-lease` flag checks whether the remote branch has been updated since you last fetched it. If it has, the push is rejected, preventing you from overwriting someone else's changes. Using `--force-with-lease` can help prevent data loss and conflicts caused by overwriting someone else's changes.

*Note*: It's important to never rebase a branch that has already been pushed to a public repository. Doing so can cause issues with the commit sign-off and create a messy history of commits.

If you have any questions or run into any issues, feel free to reach out to our community for support.


## Repository requirements

We recommend repositories in the project adhere to some security and maintenance guidelines. These are _only guidelines_, and may not be applicable or valuable in all instances. They are primarily inspired by recommendations from the [Cloud Native Security Controls Catalog](https://www.cncf.io/blog/2022/06/07/introduction-to-the-cloud-native-security-controls-catalog/). Adherence to these guidelines may be required for 1.0 artifact releases, at the discretion of the [Technical Steering Committee](https://github.com/open-feature/community/blob/main/governance-charter.md#technical-steering-committee-tsc) and maintainers.

| Requirement                     | Recommended solution(s)                                                                                                                   |
| ------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| artifact and image signing      | language-specific tools, [cosign][cosign]                                                                                                 |
| automated publishing            | github actions (with permissions applying principle of least privilege), language-specific tools (Maven, nuget, NPM, etc)                 |
| container, base image scanning  | [snyk][snyk], [trivy][trivy]                                                                                                              |
| code ownership                  | branch protection rules\* and CODEOWNERS files                                                                                            |
| dependency analysis             | [snyk][snyk]                                                                                                                              |
| dependency auto-updates         | [Renovate][renovate]\*\*, [Dependabot][dependabot]                                                                                        |
| fuzzing                         | [ClusterFuzzLite][clusterfuzzlite], [OSS-Fuzz][oss-fuzz]                                                                                  |
| SBOM generation                 | [CycloneDX][cyclonedx], [SPDX][spdx], [syft][syft]                                                                                        |
| static analysis                 | [SonarCloud][sonarcloud], language-specific tools (SpotBugs, eslint)                                                                      |
| unit, integration testing       | github actions (with permissions applying principle of least privilege), language-specific tools (JUnit, Jest, etc), [Cucumber][cucumber] |
| semantic versioning, changelogs | [Semantic Versioning][semantic-versioning], [Conventional Commits][conventional-commits], [Release Please][release-please]\*\*\*          |
| helpful readme file             | See [example README.md](./templates/READMEs/README.md)                                                                                    |

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
