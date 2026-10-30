# SAM Workflows

This repository contains reusable workflows for SAM applications.

https://docs.github.com/en/actions/using-workflows/reusing-workflows

## Usage Examples

### deploy_sam_app

```yaml
name: deploy
on: push

jobs:
  deploy:
    uses: runslikebutter/sam-workflows/.github/workflows/deploy_sam_app.yml@main
    with:
      node: true
      role_to_assume: arn:aws:iam::<AWS_ACCOUNT_ID>:role/bmx-github-actions
      role_session_name: SmartLocksDevGithubActions
    secrets:
      AWS_ACCESS_KEY_ID: ${{ secrets.DEV_AWS_ACCESS_KEY_ID }}
      AWS_SECRET_ACCESS_KEY: ${{ secrets.DEV_AWS_SECRET_ACCESS_KEY }}
      AWS_REGION: ${{ secrets.DEV_AWS_REGION }}
```

### delete_sam_app

```yaml
name: delete
on: delete

jobs:
  delete:
    uses: runslikebutter/sam-workflows/.github/workflows/delete_sam_app.yml@main
    with:
      role_to_assume: arn:aws:iam::<AWS_ACCOUNT_ID>:role/bmx-github-actions
      role_session_name: SmartLocksDevGithubActions
    secrets:
      AWS_ACCESS_KEY_ID: ${{ secrets.DEV_AWS_ACCESS_KEY_ID }}
      AWS_SECRET_ACCESS_KEY: ${{ secrets.DEV_AWS_SECRET_ACCESS_KEY }}
      AWS_REGION: ${{ secrets.DEV_AWS_REGION }}
```

### run_linters

```yaml
name: lint
on: pull_request

jobs:
  lint:
    uses: runslikebutter/sam-workflows/.github/workflows/run_linters.yml@main
```

### bump_node_app_version

Pushes a version bump commit, changelog and tag using the `bmx-bot` GitHub App. The `bmx-bot` App must be on the bypass list of the protected branch.

```yaml
name: deploy_dev
on:
  push:
    branches: [main]

jobs:
  bump_version:
    uses: runslikebutter/sam-workflows/.github/workflows/bump_node_app_version.yml@main
    secrets:
      BMX_BOT_GITHUB_APP_PRIVATE_KEY: ${{ secrets.BMX_BOT_GITHUB_APP_PRIVATE_KEY }}
```

### check_semantic_pr

```yaml
name: check_semantic_pr
on:
  pull_request:
    types: [opened, edited, synchronize]

jobs:
  check_semantic_pr:
    uses: runslikebutter/sam-workflows/.github/workflows/check_semantic_pr.yml@main
```
