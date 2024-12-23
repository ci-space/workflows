# Workflows

## Release Docker based GitHub Action

This manual action does:
- Generate new version by choice of: major, minor, patch
- Set new version into docker image in action.yaml
- Build image for new version
- Commit and push action.yaml
- Create and push new tag

### Usage

.github/workflows/release.yaml:
```yaml
name: release

permissions: write-all

on:
  workflow_dispatch:
    inputs:
      version:
        description: version
        required: true
        type: choice
        options:
          - major
          - minor
          - patch

jobs:
  release:
    uses: ci-space/workflows/.github/workflows/release-docker-github-action.yaml@master
    secrets: inherit
    with:
      version: ${{ github.event.inputs.version }}
```
