---
title: "CampusMeet Workshop"
date: 2026-08-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Build and deploy CampusMeet on AWS

This workshop takes CampusMeet from source code to a complete AWS development environment. You will deploy the data foundation, user-content and AI orchestration, application stack, CloudFront frontend, and Google Calendar/Meet integration, then perform smoke tests and operational checks.

![CampusMeet AWS architecture](/images/5-Workshop/campusmeet-aws-architecture.png)

## Outcomes

- React SPA delivered by CloudFront from a private S3 origin.
- Cognito authentication and a Node.js 22 Lambda behind HTTP API.
- Five DynamoDB business-data tables.
- User-content S3, Step Functions, Reminder Lambda, Scheduler, and SES.
- Correct Google OAuth, Calendar, and Meet integration.
- AI Worker, Bedrock Knowledge Base, and S3 Vectors for approved content.
- CloudWatch logs/alarms and SNS notifications.

## Modules

1. [Architecture overview](5.1-overview/)
2. [Account and tooling prerequisites](5.2-prerequisites/)
3. [Deploy the data foundation](5.3-data-foundation/)
4. [Deploy M4 and the application stack](5.4-backend-infrastructure/)
5. [Deploy frontend and Google Workspace](5.5-frontend-google/)
6. [Smoke testing, monitoring, and cleanup](5.6-validation-cleanup/)

{{% notice warning %}}
Never commit access keys, OAuth client secrets, tokens, Bedrock API keys, or `.env` contents. Verify the AWS account, Region, and CloudFormation change set before every deployment.
{{% /notice %}}
