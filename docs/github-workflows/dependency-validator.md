# Dependency Validator

This workflow uses our [custom action](https://github.com/marketplace/actions/naomi-s-dependency-validator) to confirm that all `npm` dependencies are pinned to a specific version.

```yaml
name: Dependency Validation
on:
  pull_request:
    branches:
      - main

jobs:
  validate:
    name: Validate Dependencies are Pinned
    runs-on: ubuntu-20.04

    steps:
      - name: Checkout Source Files
        uses: actions/checkout@v3

      - name: Check Dependencies
        uses: naomi-lgbt/dependency-pin-check@main
```
