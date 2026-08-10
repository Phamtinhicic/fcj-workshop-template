---
title: "Architecture overview"
date: 2026-08-01
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

# Architecture overview

![CampusMeet architecture](/images/5-Workshop/campusmeet-aws-architecture.png)

CampusMeet separates the system into four areas: the React web and Meet Add-on experience; an authenticated API and business authorization layer; DynamoDB metadata plus private S3 content; and background orchestration through Scheduler, Step Functions, AI Worker, Bedrock Knowledge Base, and S3 Vectors.

For synchronous requests, CloudFront serves the SPA, Cognito issues an access token, API Gateway validates it, and the API Lambda verifies active group membership before data access. For uploads, the browser receives a short-lived URL and sends the binary directly to S3. Completion is verified with `HeadObject` before metadata and an idempotent AIJob are created.

The AI execution is recoverable: the persisted job is the source of truth, Step Functions coordinates processing, and retries do not create another logical job. Approved knowledge is filtered by group and meeting metadata.

| Stack | Ownership |
| --- | --- |
| `campusmeet-dev-data` | five DynamoDB tables |
| `campusmeet-dev-user-content` | content bucket, state machine, reminder, scheduler role, SES configuration set |
| `campusmeet-dev-app` | frontend, API, Cognito, sync worker, AI Worker, Knowledge Base, alarms |

Deploy in the order **data → M4 user content → application → frontend**. Do not manually create resources with names already managed by CloudFormation.
