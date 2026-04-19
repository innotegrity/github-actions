# Set up Golang

Installs Go via [`actions/setup-go`](https://github.com/actions/setup-go) so later steps can run `go` commands.

## Inputs

| Input | Description | Default |
| --- | --- | --- |
| `version` | Go version to install (semver string understood by setup-go). | `1.25.9` |

## Usage

```yaml
- uses: innotegrity/github-actions/set-up-go@main
  with:
    version: '1.25.9'
```
