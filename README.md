# update-major-tag
A reusable workflow which automatically updates the major tag(for example, `v1`, `Test.App/v2`) when a new tag is created.

## Installation
Add a new workflow under `.github/workflows/` with the following contents:
```yml
name: Update v<Major> Tag
run-name: |
  Update major tag: ${{ github.event_name }}${{ github.event_name == 'push' && (github.event.created && ' created' || ' deleted') || '' }} ${{ github.event.ref }}

on:
  delete:

  push:
    tags:
      - '**'

jobs:
  update-tag:
    permissions:
      contents: write
    uses: Arthri/update-major-tag/.github/workflows/update-major-tag.yml@v1

```

## Usage
1. Create a new tag. For example, `v1.4.2`, `Test.App/v2.5.3`.
1. Expect the workflow to run and create a tag such as `v1` or `Test.App/v1` in a few moments.
