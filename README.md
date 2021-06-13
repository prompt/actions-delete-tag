# Delete Tag

A GitHub Action that deletes the tag that triggered the workflow.

```
pr-mpt/actions-delete-tag@v1
```

## Inputs

No inputs.

## Outputs

No outputs.

## Example

When a new tag is created, assert that the commit has a `dist` directory and if
it does not then delete the tag.

```yaml
name: "Limit Tags To Distributable Commits"

on:
  push:
    tags:
      - "**"

jobs:
  validate-tag:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: pr-mpt/actions-assert@v2
        with:
          assertion: npm://@assertions/directory-exists
          expected: dist
      - if: failure()
        name: Delete tag
        uses: pr-mpt/actions-delete-tag@v1
```
