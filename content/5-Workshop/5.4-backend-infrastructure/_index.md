---
title: "Deploy M4 and the application stack"
date: 2026-08-01
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

# Deploy M4 and the application stack

Validate and build `infra/user-content-orchestration.yaml`, then deploy `campusmeet-dev-user-content` with `CAPABILITY_IAM`. Supply the deterministic AI Worker ARN, verified SES sender, table prefix, frontend origin, and either an existing user-content bucket or an empty value for a CloudFormation-managed bucket.

Capture `UserContentBucketName`, `AIStateMachineArn`, `ReminderFunctionArn`, `SchedulerExecutionRoleArn`, and `SesConfigurationSetName`.

Next, validate and build `infra/template.yaml`. Deploy it with the data stream ARN, all M4 outputs, Google secret and redirect, frontend origin, and Bedrock parameters. Preview the change set and reject unexpected table/bucket replacement or deletion.

Capture `ApiUrl`, `FrontendBucketName`, `CloudFrontDomainName`, Cognito IDs, worker names, Knowledge Base ID, and alarms. Verify `/health` returns 200, Lambda functions are active, the stream mapping is enabled, and a Step Functions test execution can complete.
