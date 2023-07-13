# Terraform CDK Pattern Action

[![LICENSE](https://img.shields.io/badge/license-BSD3-green)](LICENSE)
[![Latest Release](https://img.shields.io/github/v/release/truemark/terraform-cdk-pattern-action)](https://github.com/truemark/terraform-cdk-pattern-action/releases)
![GitHub closed issues](https://img.shields.io/github/issues-closed/truemark/terraform-cdk-pattern-action)
![GitHub closed pull requests](https://img.shields.io/github/issues-pr-closed/truemark/terraform-cdk-pattern-action)

Plans a Terraform CDK stack during a pull request or deploys a Terraform CDK stack into a given workspace after merging code. 

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
        uses: truemark/terraform-cdk-pattern-action@v1
        with:
          stack-name: MyStack
          workspace: ${{ inputs.workspace }}
```

## Inputs
| Name              | Type   | Required | Description                                         |
|-------------------|--------|----------|-----------------------------------------------------|
| stack-name        | string | Yes      | The Terraform CDK stack to plan or deploy.          |
| workspace         | string | Yes      | The workspace in which to plan or deploy the stack. |
| working-directory | string | No       | The directory where Terraform CDK lives.            |
