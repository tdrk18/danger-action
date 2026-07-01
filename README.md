# danger-action

GitHub Action to run [Danger](https://danger.systems/ruby/) with Ruby setup and branch pre-fetch.

## Features

- Sets up Ruby with the specified version or `.ruby-version`
- Installs gems via Bundler (with optional caching)
- Pre-fetches base/head branches to skip Danger's internal `git fetch`
- Runs Danger

## Usage

```yaml
- uses: tdrk18/danger-action@v1
  with:
    github-token: ${{ secrets.GITHUB_TOKEN }}
```

## Inputs

| Input | Required | Default | Description |
|---|---|---|---|
| `ruby-version` | No | `.ruby-version` or `4` | Ruby version to use |
| `gemfile` | No | `Gemfile` | Path to Gemfile |
| `dangerfile` | No | `Dangerfile` | Path to Dangerfile |
| `danger-id` | No | `danger` | Danger ID (`--danger_id`) |
| `fail-on-errors` | No | `false` | Always fail the build when Danger reports errors (`--fail-on-errors`) |
| `fail-if-no-pr` | No | `false` | Fail the build if no PR is found (`--fail-if-no-pr`) |
| `new-comment` | No | `false` | Post a new comment instead of editing the previous one (`--new-comment`) |
| `remove-previous-comments` | No | `false` | Remove all previous comments and post a new one (`--remove-previous-comments`) |
| `base` | No | `` | Branch/tag/commit to use as the base of the diff (`--base`) |
| `head` | No | `` | Branch/tag/commit to use as the head of the diff (`--head`) |
| `cache` | No | `true` | Enable Bundler cache |
| `github-token` | No | `${{ github.token }}` | GitHub token passed to `DANGER_GITHUB_API_TOKEN` |

## Examples

### Minimal

```yaml
name: Danger
on:
  pull_request:

jobs:
  danger:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: tdrk18/danger-action@v1
```

### With custom options

```yaml
name: Danger
on:
  pull_request:

jobs:
  danger:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: tdrk18/danger-action@v1
        with:
          ruby-version: '4.0.5'
          dangerfile: 'ci/Dangerfile'
          danger-id: 'my-danger'
          cache: 'false'
          github-token: ${{ secrets.GITHUB_TOKEN }}
```
