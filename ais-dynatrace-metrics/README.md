# Account Interventions Service - Dynatrace Metrics

## Intro
The SAM template creates our Dynatrace Metrics Stack which sets up the infrastructure required for Dynatrace
integration with CloudWatch Metric Streams to ingest AWS metrics for Account Interventions Service.

This Stack is to be deployed manually once per account/environment.

## Prerequisites

#### ⚠️ Task to be carried out prior to deployment ⚠️

- [ ] Deploy `ais-infra-common` template first
- [ ] Manually update the Secret DynatraceApiKey to the provided value by https://gds.slack.com/archives/C04UF0B02NR

❗Once these steps have been taken you can deploy this stack following the instructions below

Export credentials for the AWS account where you want to deploy the application.
You can use the following command to export credentials into your shell:
```bash
eval $(gds aws di-id-reuse-core-<environment>-admin -e)
```
Replace `<environment>` with the environment you are deploying into.
Allowed values are `dev`, `build`,and `staging` .

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
1. Navigate to the `ais-dynatrace-metrics` directory
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
aws cloudformation describe-stacks --stack-name ais-dynatrace-metrics --region eu-west-2
```
Note: Make sure you have deployed ais-infra-common stack first and updated the Secrets PLACEHOLDER values prior to deploying this stack.
