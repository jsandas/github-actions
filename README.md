# github-actions

## Reusable workflows

### Go lint workflow

This repository includes a reusable workflow for running Go linting. It accepts optional inputs for the golangci-lint version and the Go setup configuration.

`go_version` and `go_version_file` are mutually exclusive. If both are supplied, the workflow fails with an error instead of silently choosing one. When neither is supplied, the workflow defaults to `go.mod`.

Use the default Go version file (defaults to `go.mod`) and default lint version (`latest`):

```yaml
jobs:
  lint:
    uses: jsandas/github-actions/.github/workflows/golang-lint.yml@main
```

Override the golangci-lint version and explicitly set the Go version:

```yaml
jobs:
  lint:
    uses: jsandas/github-actions/.github/workflows/golang-lint.yml@main
    with:
      golangci_lint_version: v2.1.6
      go_version: "1.24.5"
      go_cache: true
```

Or provide a Go version file instead of a direct Go version:

```yaml
jobs:
  lint:
    uses: jsandas/github-actions/.github/workflows/golang-lint.yml@main
    with:
      go_version_file: .tool-versions
      go_cache: false
```

### Go security workflow

The Go security workflow supports the same Go setup inputs. `go_version` and `go_version_file` are mutually exclusive, and the workflow fails with an error if both are supplied. When neither is supplied, it defaults to `go.mod`.

```yaml
jobs:
  security:
    uses: jsandas/github-actions/.github/workflows/golang-security.yml@main
    with:
      go_version: "1.24.5"
      go_cache: true
```

You can also point the workflow at a version file instead:

```yaml
jobs:
  security:
    uses: jsandas/github-actions/.github/workflows/golang-security.yml@main
    with:
      go_version_file: .tool-versions
      go_cache: false
```
