# Account Interventions Service - AIS Infra Common

## Intro

This stack contains AWS Secrets used for Dynatrace.

## Prerequisites
Export credentials for the AWS account where you want to deploy the application.
You can use the following command to export credentials into your shell:
```bash
eval $(gds aws di-id-reuse-core-<environment>-admin -e)
```
Replace `<environment>` with the environment you are deploying into.
Allowed values are `dev`, `build`, `staging`.

Whereas to deploy to `integration` and  `production` you'd need to Login into the Account Interventions Service AWS accounts using sso

`Integration`:
```bash
aws sso login --profile di-account-intervention-admin-217747075921
```
`Production`:
```bash
aws sso login --profile di-account-intervention-admin-324281879537
```

## How to Deploy
To deploy this SAM template, follow these steps:
1. Navigate to the `ais-infra-common` directory
2. Build the SAM application:
```bash
sam build
```
3. Deploy the application to your AWS account:
```bash
sam deploy --guided
```
The `--guided` flag will prompt you to input the necessary parameters for the deployment, such as the stack name, region, and environment.

After the deployment is complete, you can check the CloudFormation stack status in the AWS Management Console or by using the AWS CLI:
```bash
aws cloudformation describe-stacks --stack-name ais-infra-common --region eu-west-2
```
#### ⚠️ Once this stack has been deployed, manually set the value of the secrets in AWS Console, values to be provided by - https://gds.slack.com/archives/C04UF0B02NR
This step must be done prior to progressing to deploying the `ais-dynatrace-metrics`  and `ais-main` stack.

#### ❗If the Secret values are changed both `ais-dynatrace-metrics`  and `ais-main` stack need to be redeployed so that the new values are used instead.
