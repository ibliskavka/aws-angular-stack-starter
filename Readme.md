# AWS Angular Stack Automation

## Introduction
This starter project shows how to create the hosting infrastructure for an Angular app using CloudFormation and how to deploy the app using the CLI.

The full write up and article can be found at:  
https://medium.com/@ibliskavka/aws-angular-stack-automation-b45767bda2ec

### Prerequisites
* Amazon Route53 Domain
* Amazon Certificate Manager cert for the domain

## Deploy the stack

Run the following command from the /stack directory:  
(replace asterisks with your own values)

`aws cloudformation deploy --template-file template.yml --stack-name aws-ng-demo --parameter-overrides BaseUrl=*** AppUrl=*** AcmCertArn=***`

Get the CloudFront DistributionId and S3 bucket by running the following command  
(you can also get this from the web console)

`aws cloudformation describe-stacks --stack-name aws-ng-demo --query "Stacks[0].Outputs[?OutputKey==`DistributionId` || OutputKey==`AppBucket`]"`

## Deploy the App

1. Update /demo-app/package.json/scripts/deploy  
Replace {AppBucket} & {DistributionId} with your stack outputs
2. Run the following command from the /demo-app directory  
`npm run deploy`

Congratulations! You have deploy the infrastructure and code for an angular app entirely from console. Now drop this into CodePipeline & CodeBuild to get your CI/CD pipeline started.