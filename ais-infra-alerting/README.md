# Account Interventions Service - AIS Infra Alerting

## Intro
Consolidated alerting functionality to create a general infra alerting template with a subscription endpoint for PagerDuty and a single Chatbot configuration for all Slack alerts relating to AIS.

## Prerequisites
Export credentials for the AWS account where you want to deploy the application.
You can use the following command to export credentials into your shell:
```bash
eval $(gds aws di-id-reuse-core-<environment>-admin -e)
```
Replace `<environment>` with the environment you are deploying to, in this instance for `di-id-reuse-core` AWS accounts
Allowed values are `dev` `build` and `staging` 

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

For the Parameter `InitialNotificationStack` select `No` in all environments when deploying the stack infra-alerting stack, 
we would not need to create these two Service Linked Roles `AWSServiceRoleForCodeStarNotifications` & `AWSServiceRoleForAWSChatbot`
as they have already been created in the accounts. 

After the deployment is complete, you can check the CloudFormation stack status in the AWS Management Console or by using the AWS CLI:
```bash
aws cloudformation describe-stacks --stack-name ais-infra-alerting --region eu-west-2
```


### Stack Outputs
| Type           | Name                                                      | Description                                                                                                                        |
|----------------|-----------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| SNS Topic      | `<environment>-BuildNotificationTopicArn`                 | ARN of the pipeline build notification SNS topic                                                                                   |
