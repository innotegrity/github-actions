# Wait for Workflow

Polls until a named GitHub Actions workflow run finishes (or reaches an allowed conclusion), then continues. Implemented with [`ArcticLampyrid/action-wait-for-workflow`](https://github.com/ArcticLampyrid/action-wait-for-workflow) at a pinned version.

Use this to **sequence** pipelines—for example, wait for a CI workflow on the same commit before deploying, or coordinate jobs across repositories when the token can read the target repo’s checks.

## Inputs

| Input | Description | Default |
| --- | --- | --- |
| `github_token` | Token used to query workflow runs (needs appropriate repo/API access). | `github.token` |
| `workflow` | Workflow **name** as shown in the Actions UI (filename without path is not always the same—use the workflow’s `name:` or the value GitHub displays). | *(required)* |
| `repo` | Repository as `owner/name`. | Current repository (`github.repository`) |
| `sha` | Commit SHA to match; use `auto` (default) to let the upstream action resolve the relevant commit. | `auto` |
| `branch` | Optional branch name filter. | *(unset)* |
| `event` | Optional GitHub event type filter (for example `push`, `pull_request`). | *(unset)* |
| `wait-interval` | Seconds between polls (minimum **5** per upstream). | `30` |
| `allowed-conclusions` | Newline-separated list of conclusions that count as success (for example `success`, `skipped`). | `success` |

If the run finishes with a conclusion not in `allowed-conclusions`, the step fails.

## Permissions

The default `GITHUB_TOKEN` can list workflow runs in the **same** repository when `actions: read` is available (GitHub’s default permissions for private repos may vary; set `permissions:` explicitly if needed). For **another** repository, use a token that can read that repo’s Actions data (often a PAT or GitHub App with `actions:read` / `contents:read` as required by your setup).

## Usage

Wait for a workflow named `CI` on the current repo and commit:

```yaml
- uses: innotegrity/github-actions/wait-for-workflow@main
  with:
    workflow: CI
```

Allow both successful and skipped runs:

```yaml
- uses: innotegrity/github-actions/wait-for-workflow@main
  with:
    workflow: Build
    allowed-conclusions: |
      success
      skipped
```

Monitor another repository:

```yaml
- uses: innotegrity/github-actions/wait-for-workflow@main
  with:
    workflow: Release
    repo: my-org/other-repo
    github_token: ${{ secrets.CROSS_REPO_TOKEN }}
```
