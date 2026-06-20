# dco-check

[![Build](
https://github.com/actionshub/dco/actions/workflows/build.yaml/badge.svg
)](https://github.com/actionshub/dco/actions/workflows/build.yaml)
[![CodeQL](
https://github.com/actionshub/dco/actions/workflows/codeql.yml/badge.svg
)](https://github.com/actionshub/dco/actions/workflows/codeql.yml)
[![Lint](
https://github.com/actionshub/dco/actions/workflows/lint.yaml/badge.svg
)](https://github.com/actionshub/dco/actions/workflows/lint.yaml)

A GitHub Action that verifies commits in pull-request all include Developer
Certificate of Origin (DCO) information.

You can also configure labels that tell this plugin to skip checking this
PR (e.g. for "obvious fixes").

## Usage

Add .github/workflows/dco.yml with the following:

```yaml
name: DCO
on: [pull_request]

jobs:
  dco:
    runs-on: ubuntu-latest
    name: Commits Check
    steps:
    - name: Get PR Commits
      id: 'get-pr-commits'
      uses: actionshub/get-pr-commits@main
      with:
        token: ${{ secrets.GITHUB_TOKEN }}
    - name: DCO Check
      uses: actionshub/dco@main
      with:
        commits: ${{ steps.get-pr-commits.outputs.commits }}
```

### Bypassing DCO for specific PRs

Many repos may exempt DCO requirments for "obvious fix" PRs. You can
configure a label to tell this check that a PR is an obvious fix and
should not require a DCO:

```yaml
    - name: DCO Check
      uses: actionshub/dco@main
      with:
        commits: ${{ steps.get-pr-commits.outputs.commits }}
        allow-obvious-fix-label: "obvious-fix"
```

With this, if the `obvious-fix` label is on a PR, the DCO check will
be bypassed.

### Skipping specific commits

It will ensure all commits on a commit have DCO - specific commits can be
skipped using the filtering options to
[get-pr-commits](https://github.com/actionshub/get-pr-commits)

## Copyright and License

Copyright Tim Zhang, Phil Dibowitz, and Contributors.

ISC license, see [LICENSE.txt](LICENSE.txt) for details.

## History

This is a fork of [tim-actions/dco](https://github.com/tim-actions/dco),
which is no longer maintained.
