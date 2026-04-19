# Run markdownlint

Lints Markdown files using [`DavidAnson/markdownlint-cli2-action`](https://github.com/DavidAnson/markdownlint-cli2-action).

## Inputs

| Input | Description | Default |
| --- | --- | --- |
| `fix` | Any truthy value enables auto-fix for supported rules. | *(empty)* |
| `globs` | Newline-separated glob patterns for files to lint. | `*.{md,mdc}` |

## Usage

```yaml
- uses: innotegrity/github-actions/run-markdown-lint@main
```

```yaml
- uses: innotegrity/github-actions/run-markdown-lint@main
  with:
    globs: |
      docs/**/*.md
      README.md
```
