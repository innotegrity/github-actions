# github-actions

Composite [GitHub Actions](https://docs.github.com/en/actions/creating-actions/creating-a-composite-action) used across Innotegrity repositories. Each action lives in its own directory and can be referenced from workflows with `uses: innotegrity/github-actions/<path>@<ref>`.

## Using these actions

Reference a specific **tag**, **branch**, or **commit SHA** (SHA is best for supply-chain pinning):

```yaml
jobs:
  example:
    runs-on: ubuntu-latest
    steps:
      - uses: innotegrity/github-actions/check-out-code@main
      - uses: innotegrity/github-actions/set-up-go@main
```

Replace `main` with a version tag (for example `v1.0.0`) once this repository publishes releases.

## Actions overview

| Action | Purpose |
| --- | --- |
| [check-out-code](./check-out-code/) | Clone a repository (wrapper around `actions/checkout`). |
| [set-up-go](./set-up-go/) | Install Go and configure the toolchain. |
| [run-go-tests](./run-go-tests/) | Run `go test` with coverage output. |
| [run-golangci-lint](./run-golangci-lint/) | Run [golangci-lint](https://golangci-lint.run/) on Go code. |
| [run-markdown-lint](./run-markdown-lint/) | Lint Markdown with [markdownlint-cli2](https://github.com/DavidAnson/markdownlint-cli2). |
| [run-sonarqube-scan](./run-sonarqube-scan/) | Upload sources and metrics to SonarQube or SonarCloud. |
| [verify-sonarqube-quality](./verify-sonarqube-quality/) | Fail the job if the SonarQube quality gate does not pass. |
| [create-release-from-changelog](./create-release-from-changelog/) | Build release notes from Keep a Changelog and create a GitHub Release. |
| [wait-for-workflow](./wait-for-workflow/) | Block until another workflow run completes (or reaches an allowed conclusion). |

## Typical combinations

- **Go CI**: `check-out-code` → `set-up-go` → `run-go-tests` → optionally `run-golangci-lint`.
- **SonarQube**: Run tests and produce `coverage.out`, then `run-sonarqube-scan`, then `verify-sonarqube-quality` (same job or a dependent job with the analysis token).
- **Release**: Tag a release on GitHub and use `create-release-from-changelog` on `release` / `push` tags workflows.
- **Orchestration**: Use `wait-for-workflow` so a job does not proceed until a named workflow has finished for the same commit (or another repo), subject to token permissions.

## Secrets and configuration

- **SonarQube / SonarCloud**: Provide a token (for example `SONAR_TOKEN`) to `run-sonarqube-scan` and `verify-sonarqube-quality`. SonarCloud uses `organization` and `projectKey`; self-hosted SonarQube may use a different `url`.
- **GitHub Releases**: `create-release-from-changelog` uses `softprops/action-gh-release`, which requires `contents: write` permission and an appropriate `GITHUB_TOKEN` (default token is usually sufficient for releases in the same repo).

## Repository layout

Each subdirectory named `*/action.yml` is one composite action. Documentation for inputs and behavior is in that directory’s `README.md`.
