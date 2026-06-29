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
