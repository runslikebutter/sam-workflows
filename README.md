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
      role_to_assume: arn:aws:iam::619981303841:role/bmx-github-actions
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
      role_to_assume: arn:aws:iam::619981303841:role/bmx-github-actions
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
