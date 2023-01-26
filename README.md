# 🫖 diff-porcelain

Checks if the current branch is clean and errors with a custom message otherwise.

# Usage

```yaml
name: CI

on:
  push:
    branches:
      - main
  pull_request: {}


jobs:
  check-diff:
    name: Check diff
    runs-on: ubuntu-latest
    needs: detect-noop
    if: ${{ needs.detect-noop.outputs.noop != 'true' }}
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Generate
        run: make generate

      - name: Diff porcelain
        uses: mmontes/diff-porcelain@v0.0.1
        with:
          message: Generated artifacts are not up to date. Run 'make generate' and commit the changes.
```