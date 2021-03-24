# Assume Role GitHub Action

The `github-action-assume-role` Github Action will assume a Role in an AWS Account.

## Inputs

| Name | Description | Required |Default |
| --- | --- | --- | --- |
| `AWS_ACCESS_KEY_ID` | The AWS access key used as part of the credentials to authenticate the user. | :heavy_check_mark: | |
| `AWS_SECRET_ACCESS_KEY` | The AWS secret access key used as part of the credentials to authenticate the user. | :heavy_check_mark: | |
| `AWS_REGION` | The AWS region to use | | eu-west-1 |
| `AWS_EXTERNAL_ID` | External ID if its configured | |  |
| `AWS_ROLE_TO_ASSUME` | The AWS Role that you want to assume | :heavy_check_mark: | |
| `AWS_SESSION_NAME` | The session name |  | github-robot |


## Usage

```yaml
on:
  workflow_dispatch:
    inputs:
      accountNumber:
        description: 'AWS Account where you want to assume role'
        required: true
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: xinin/github-action-assume-role@1.0.0
        with:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          AWS_REGION: 'eu-west-1'
          AWS_EXTERNAL_ID: ${{ secrets.DEPLOYMENT_EXID }}
          AWS_ROLE_TO_ASSUME: arn:aws:iam::${{ github.event.inputs.accountNumber }}:role/github-robot-access-role
          AWS_SESSION_NAME: 'github-robot'
```
