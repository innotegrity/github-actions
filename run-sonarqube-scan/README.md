# Run SonarQube Scan

Runs a SonarQube analysis with [`sonarsource/sonarqube-scan-action`](https://github.com/SonarSource/sonarqube-scan-action). Defaults target **SonarCloud** (`https://sonarcloud.io`); set `url` for a self-hosted SonarQube server.

The action sets branch or pull request parameters from the GitHub event: on pull requests it passes `sonar.pullrequest.*`; otherwise `sonar.branch.name` from `github.ref_name`.

## Inputs

| Input | Description | Default |
| --- | --- | --- |
| `token` | SonarQube or SonarCloud token (`SONAR_TOKEN`). | *(required)* |
| `organization` | SonarCloud organization (or as required by your server). | *(required)* |
| `projectKey` | Sonar project key. | *(required)* |
| `url` | SonarQube server URL. | `https://sonarcloud.io` |
| `sourceDir` | Value for `sonar.sources`. | `.` |
| `projectBaseDir` | Value for `sonar.projectBaseDir`. | `.` |
| `coverageExclusions` | `sonar.coverage.exclusions` pattern. | `**/*_test.go` |
| `goCoverageReportPaths` | `sonar.go.coverage.reportPaths` (often `coverage.out` from `run-go-tests`). | `coverage.out` |
| `excludedWorkflowPattern` | Comma-separated path patterns; maps to Sonar issue ignore multicriteria for GitHub Actions rule `githubactions:S7637`. | *(empty)* |

`sonar.projectVersion` is set to `github.sha`.

## Usage

```yaml
- uses: innotegrity/github-actions/run-sonarqube-scan@main
  with:
    token: ${{ secrets.SONAR_TOKEN }}
    organization: your-org
    projectKey: your-project-key
```

For Go coverage, run `run-go-tests` first so `goCoverageReportPaths` matches the generated file.

## Related

Use [verify-sonarqube-quality](../verify-sonarqube-quality/) after the scan (same pipeline or a follow-up step) to enforce the quality gate.
