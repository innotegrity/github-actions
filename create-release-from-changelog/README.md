# Create GitHub Release from Changelog

1. Extracts release notes from a [Keep a Changelog](https://keepachangelog.com/)-style file using [`ffurrer2/extract-release-notes`](https://github.com/ffurrer2/extract-release-notes).
2. Creates a GitHub Release with [`softprops/action-gh-release`](https://github.com/softprops/action-gh-release), using those notes as the release body.

Typical trigger: workflow on `release` or on tag push, so `github.ref_name` is the version tag.

## Inputs

| Input | Description | Default |
| --- | --- | --- |
| `changelog_file` | Path to the changelog file. | `CHANGELOG.md` |
| `release_notes_file` | Optional path where extracted notes are written. | *(unset)* |
| `prerelease` | `true` uses the `[Unreleased]` section; `false` uses the latest released version section. | `false` |

The release **name** is `Release <github.ref_name>`; `generate_release_notes` is disabled so the body comes only from the changelog extraction.

## Permissions

The job needs permission to create releases (for example `contents: write` for the default `GITHUB_TOKEN` in the same repository).

## Usage

```yaml
- uses: innotegrity/github-actions/create-release-from-changelog@main
  with:
    changelog_file: CHANGELOG.md
```
