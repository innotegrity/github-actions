# Checkout Code

Checks out a Git repository using [`actions/checkout`](https://github.com/actions/checkout) with a stable, pinned version.

## Inputs

| Input | Description | Default |
| --- | --- | --- |
| `repository` | Repository in `owner/name` form (for example `actions/checkout`). | Current repository (`github.repository`) |
| `ref` | Branch, tag, or SHA to check out. For the triggering repo, defaults to the event ref; otherwise the default branch. | *(see checkout docs)* |
| `fetch-depth` | Number of commits to fetch; `0` means full history. | `1` |

## Usage

```yaml
- uses: innotegrity/github-actions/check-out-code@main
  with:
    fetch-depth: 0
```
