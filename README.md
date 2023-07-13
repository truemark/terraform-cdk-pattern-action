# Terraform CDK Pattern Action

[![LICENSE](https://img.shields.io/badge/license-BSD3-green)](LICENSE)
[![Latest Release](https://img.shields.io/github/v/release/truemark/terraform-cdk-pattern-action)](https://github.com/truemark/terraform-cdk-pattern-action/releases)
![GitHub closed issues](https://img.shields.io/github/issues-closed/truemark/terraform-cdk-pattern-action)
![GitHub closed pull requests](https://img.shields.io/github/issues-pr-closed/truemark/terraform-cdk-pattern-action)

Runs Terraform CDK commands against a stack in a given workspace.

## Examples
```yml
  cdktf:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3
  
      - uses: actions/setup-node@v3
        with:
          node-version: 18
  
      - name: Run yarn install for Terraform CDK
        uses: borales/actions-yarn@v4
        with:
          dir: .
          cmd: install --frozen-lockfile
          
      - name: Run Terraform CDK
        if: github.event_name == 'pull_request'
        uses: truemark/terraform-cdk-pattern-action@v1
        with:
          mode: synth plan
          stack-name: MyStack
          workspace: ${{ inputs.workspace }}
          
      - name: Run Terraform CDK
        if: github.event_name == 'push'
        uses: truemark/terraform-cdk-pattern-action@v1
        with:
          mode: deploy
          stack-name: MyStack
          workspace: ${{ inputs.workspace }}
```

## Inputs
| Name              | Type   | Required | Description                                                                                   |
|-------------------|--------|----------|-----------------------------------------------------------------------------------------------|
| mode              | array  | Yes      | A list of actions to run against the Terraform CDK stack. Options are synth, plan and deploy. |
| stack-name        | string | Yes      | The Terraform CDK stack to plan or deploy.                                                    |
| workspace         | string | Yes      | The workspace in which to plan or deploy the stack.                                           |
| working-directory | string | No       | The directory where Terraform CDK lives.                                                      |
