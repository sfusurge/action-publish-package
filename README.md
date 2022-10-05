# SFU Surge GitHub Actions Workflows

<img src=".github/assets/surge.svg" alt="SFU Surge Logo" />

A repository containing reusable CI workflows and actions.

**Table of Contents:**


- [Usage](#usage)
- [Workflows](#workflows)
   - [npm-publish](#npm-publish)
   - [npm-lint](#npm-lint)


## Usage

```yaml
name: MyExternalWorkflow
on:
  push: {}

jobs:
  craco:
    uses: 'sfusurge/actions-workflows/.github/workflows/<WORKFLOW>.yml@v1'
    with:
      workflow-ref: "v1" # <-- must be the same as the workflow version
      ...
```

## Workflows

### npm-publish

Publishes a NPM/NodeJS package.

```yaml
uses: 'sfusurge/actions-workflows/.github/workflows/npm-publish.yml@v1'
with:
    workflow-ref: "v1"
    package: "local/path/to/package"
    publish-gpr: ${{ startsWith(github.ref, 'refs/tags/v') }}
    replace-version: "${{ github.ref_name }}"
    cache-key: "${{ github.job }}"
```

|Input|Default|Description|
|:--|:--|:--|
|`package`|\[required\]|The root directory of the package to publish.|
|`publish-gpr`|false|Publish the package to the GitHub Package Registry.|
|`replace-version`|\[none\]|Replaces the version of the package. This is useful for a release-on-tag workflow.|
|`cache-key`|\[required\]|If provided, NPM depdencies will be cached with this key name.|

### npm-lint

Lints a NPM/NodeJS package.

```yaml
uses: 'sfusurge/actions-workflows/.github/workflows/npm-lint.yml@v1'
with:
    workflow-ref: "v1"
    package: "local/path/to/package"
    cache-key: "${{ github.job }}"
```

|Input|Default|Description|
|:--|:--|:--|
|`package`|\[required\]|The root directory of the package to publish.|
|`cache-key`|\[required\]|If provided, NPM depdencies will be cached with this key name.|
|`linter`|"eslint"|The linter that the package is using. Supports: `eslint`|
|`check-name`|"Problems"|The name of the check to display linting errors under.|
|`fail-on-warning`|true|Warnings should be treated as errors.|
|`fail-is-ok`|false|The workflow will still pass if linting fails.|
