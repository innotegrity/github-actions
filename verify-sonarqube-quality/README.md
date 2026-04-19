# Verify SonarQube Quality

Runs [`sonarsource/sonarqube-quality-gate-action`](https://github.com/SonarSource/sonarqube-quality-gate-action) so the workflow **fails** if the SonarQube quality gate for the latest analysis is not passed.

Run this **after** a successful `run-sonarqube-scan` step (or job) that used the same Sonar project and token context.

## Inputs

| Input | Description |
| --- | --- |
| `token` | SonarQube or SonarCloud token (`SONAR_TOKEN`). **Required.** |

## Usage

```yaml
- uses: innotegrity/github-actions/verify-sonarqube-quality@main
  with:
    token: ${{ secrets.SONAR_TOKEN }}
```
