# Run go tests

Runs `go test` with verbose output and writes a coverage profile suitable for SonarQube or other coverage tools.

## Inputs

| Input | Description | Default |
| --- | --- | --- |
| `coverprofile` | Path for the coverage profile file. | `coverage.out` |
| `coverpkg` | Package patterns included in coverage (passed to `-coverpkg`). | `./...` |
| `covermode` | Coverage mode (for example `atomic`, `count`, `set`). | `atomic` |
| `source` | Packages or paths to test (passed as final arguments to `go test`). | `./...` |

## Usage

```yaml
- uses: innotegrity/github-actions/run-go-tests@main
```

After this step, `coverage.out` (or your chosen `coverprofile` path) can be consumed by `run-sonarqube-scan` via `goCoverageReportPaths`.
