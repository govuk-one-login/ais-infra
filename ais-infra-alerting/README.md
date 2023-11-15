# Account Interventions Service - AIS Infra Alerting

## Intro
Consolidated alerting functionality to create a general infra alerting template with a subscription endpoint for PagerDuty and a single Chatbot configuration for all Slack alerts relating to AIS.

## Prerequisites
Export credentials for the AWS account where you want to deploy the application.
You can use the following command to export credentials into your shell:
```bash
eval $(gds aws di-id-reuse-core-<environment>-admin -e)
```
Replace `<environment>` with the environment you are deploying into.
Allowed values are `build`, `staging`, `integration`, `production`.

## How to Deploy
To deploy this SAM template, follow these steps:
1. Navigate to the `ais-infra-alerting` directory
2. Build the SAM application:
```bash
sam build
```
3. Deploy the application to your AWS account:
```bash
sam deploy --guided
```
The `--guided` flag will prompt you to input the necessary parameters for the deployment, such as the stack name, region, and environment.

For the Parameter `InitialNotificationStack` select `No` in `build` and `staging` env because this is not the first time that we will be deploying 
a infra-alerting stack, and therefore would not need to create these two Service Linked Roles `AWSServiceRoleForCodeStarNotifications` & `AWSServiceRoleForAWSChatbot` again. 
However, in `integration` and `production` env would need to change over the parameter value to `Yes` as these two service linked roles have not yet been created in the account. 

After the deployment is complete, you can check the CloudFormation stack status in the AWS Management Console or by using the AWS CLI:
```bash
aws cloudformation describe-stacks --stack-name ais-infra-alerting --region eu-west-2
```


### Stack Outputs
| Type           | Name                                                      | Description                                                                                                                        |
|----------------|-----------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| SNS Topic      | `<environment>-BuildNotificationTopicArn`                 | ARN of the pipeline build notification SNS topic                                                                                   |
