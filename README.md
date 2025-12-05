# CodeX: PR Checks

GitHub Action for basic pull request hygiene:

- checks that a PR has a non-empty description
- checks that a PR is linked to an open issue

By default the action uses the built-in `GITHUB_TOKEN`.  
For full draft/ready automation you may optionally pass a personal access token through the `token` input.

## Inputs

| Name    | Required | Default       | Description                                                  |
|---------|----------|---------------|--------------------------------------------------------------|
| `check` | no       | `description` | Which check to run: `description`, `linked-issue`, `both`    |
| `mode`  | no       | `comment`     | Behavior: `comment`, `strict`, `draft`                       |
| `token` | no       | empty         | Optional token with extended permissions for PR mutations    |

## Usage

### Check description in strict mode

```yaml
name: Check PR Description

on:
  pull_request:
    types: [opened, edited, synchronize]

permissions:
  pull-requests: write
  issues: write
  contents: write

jobs:
  check-description:
    runs-on: ubuntu-latest
    steps:
      - uses: codex-team/action-pr-checks@v1
        with:
          check: description
          mode: strict
```

### Check linked issue in comment mode

```yaml
name: Check Linked Issue

on:
  pull_request:
    types: [opened, edited, synchronize]

permissions:
  pull-requests: write
  issues: write
  contents: write

jobs:
  check-linked-issue:
    runs-on: ubuntu-latest
    steps:
      - uses: codex-team/action-pr-checks@v1
        with:
          check: linked-issue
          mode: comment
```

### Run both checks

```yaml
name: PR Hygiene

on:
  pull_request:
    types: [opened, edited, synchronize]

permissions:
  pull-requests: write
  issues: write
  contents: write

jobs:
  pr-hygiene:
    runs-on: ubuntu-latest
    steps:
      - uses: codex-team/action-pr-checks@v1
        with:
          check: both
          mode: comment
```

## License

MIT
