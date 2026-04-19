# Run golangci-lint

Runs [golangci-lint](https://golangci-lint.run/) through [`golangci/golangci-lint-action`](https://github.com/golangci/golangci-lint-action). Expects Go code and optional `.golangci.yml` in the workspace.

## Inputs

| Input | Description | Default |
| --- | --- | --- |
| `version` | golangci-lint release tag (for example `v2.11.4`). | `v2.11.4` |

## Usage

```yaml
- uses: innotegrity/github-actions/run-golangci-lint@main
```

Ensure `set-up-go` (or equivalent) ran first if the linter needs a Go toolchain.
