---
title: "Self-Assessment"
date: 2026-08-10
weight: 6
chapter: false
pre: " <b> 6. </b> "
---

# Internship Self-Assessment

## 1. Overview

During my internship from **22 June 2026 to 15 August 2026** in the **Workforce Bootcamp – First Cloud AI Journey**, I progressed from studying fundamental AWS services to building and deploying a product as part of a team. Our main project was **CampusMeet**, a platform for team collaboration, meeting scheduling, Google Calendar/Meet integration, document and minutes management, post-meeting tasks, and AI-assisted content processing.

The internship taught me that completing a system involves more than writing source code. An operable product requires an appropriate architecture, clear API contracts, secure authorization, reproducible infrastructure, testing, documentation, and continuous collaboration.

## 2. Knowledge and skills gained

### AWS and cloud infrastructure

- Understood IAM users, groups, policies, roles, least privilege, and why root usage must be limited.
- Practiced VPC, subnet, route table, Internet Gateway, Security Group, and EC2 concepts.
- Worked with S3, CloudFront, DynamoDB, Lambda, API Gateway, Cognito, SES, EventBridge Scheduler, Step Functions, CloudWatch, and CloudFormation/SAM.
- Learned to inspect change sets and stack events, identify rollback causes, and resolve IAM deployment failures.
- Used AWS CLI and SAM CLI to validate, build, deploy, and inspect resources.

### CampusMeet development

- Participated in requirements analysis, scope definition, and serverless architecture design.
- Worked with a React/Vite frontend, Node.js/TypeScript backend, and shared data contracts.
- Implemented user-content and AI orchestration capabilities involving S3 uploads, AIJob, Step Functions, reminder Lambda, and IAM roles.
- Configured Google OAuth, Calendar, and Meet, including origins, redirect URIs, callbacks, and environment variables.
- Built and uploaded the frontend to S3, served it through CloudFront, and performed cache invalidation.
- Tested authentication, groups, meetings, Google integration, Meet links, uploads, and Step Functions executions.

### Professional skills

- Split work into smaller commits and pull requests, monitored CI, and resolved integration conflicts.
- Reported progress, symptoms, causes, and resolutions rather than only final results.
- Researched AWS and Google documentation when deployment issues occurred.
- Coordinated dependencies and deployment order across data foundation, M4, and the application stack.

## 3. Challenges and resolutions

### AWS permissions

An early CloudFormation deployment failed because the execution identity lacked `iam:CreateRole` and tagging permissions. I inspected stack events, identified the failing resource, used an authorized administrative role, and redeployed. I learned to verify AWS identity, Region, and required permissions before deployment.

### Environment configuration

The frontend initially failed to call the API because CORS, the API URL, and the CloudFront origin were inconsistent. Google OAuth also failed when its redirect URI differed from the Lambda configuration. I reconciled CloudFormation outputs, Lambda variables, API Gateway CORS, and the OAuth client, then rebuilt and redeployed the frontend.

### Team integration

Pull requests occasionally conflicted because multiple members changed services, adapters, shared types, and infrastructure templates. I learned to update from `main`, evaluate the intent of both sides, preserve required contracts, and rerun tests instead of accepting one side wholesale.

### Infrastructure deployment

Manual deployment could create duplicated or inconsistent resources. The team moved important resources into SAM/CloudFormation and standardized stack outputs and dependencies. This demonstrated why Infrastructure as Code is essential for reproducibility and handover.

## 4. Self-assessment table

| No. | Criterion | Rating | Evidence |
| ---: | --- | --- | --- |
| 1 | Professional knowledge | **Good** | Implemented and deployed multiple AWS services within CampusMeet. |
| 2 | Learning ability | **Good** | Independently researched and tested unfamiliar services and errors. |
| 3 | Initiative | **Fair–Good** | Worked independently, while appropriately confirming high-impact changes. |
| 4 | Responsibility | **Good** | Followed tasks through deployment and smoke testing. |
| 5 | Discipline and process | **Fair–Good** | Followed team processes; documentation updates can be more immediate. |
| 6 | Communication | **Fair–Good** | Reported progress and issues; complex explanations can be more concise. |
| 7 | Teamwork | **Good** | Coordinated dependencies, reviews, conflicts, and integration testing. |
| 8 | Problem solving | **Fair–Good** | Used logs to isolate failures; root-cause analysis speed can improve. |
| 9 | Time management | **Fair–Good** | Completed core work; some deployments took longer due to hidden dependencies. |
| 10 | Project contribution | **Good** | Contributed M4, deployment documentation, proposal, workshop, and AWS delivery. |
| 11 | Professional conduct | **Good** | Accepted feedback and handled secrets, permissions, and shared data carefully. |
| 12 | Overall | **Fair–Good** | Met the internship objectives and delivered a demonstrable system. |

## 5. Areas for improvement

- Improve up-front design to reduce configuration changes and repeated deployments.
- Add more automated integration, contract, idempotency, and recovery tests.
- Communicate dependencies and the impact of changes more clearly.
- Deepen knowledge of production security, secret management, least privilege, sensitive logging, and cost optimization.
- Build CI/CD pipelines to reduce manual CloudShell and Console operations.

## 6. Development plan

1. Complete CI/CD for the frontend and serverless infrastructure.
2. Add integration tests and recovery scenarios for external-service failures.
3. Study Amazon Bedrock, Knowledge Bases, S3 Vectors, and cited-answer evaluation.
4. Improve observability through dashboards, structured logs, alarms, and request tracing.
5. Continue practicing teamwork, code review, and maintainable technical documentation.

## 7. Conclusion

I believe I achieved the primary internship objectives: establishing practical AWS knowledge, experiencing a professional team workflow, and helping move CampusMeet from an idea to a deployable and demonstrable system. My most important improvement was learning to view a feature across its complete lifecycle—from requirements and code to infrastructure, security, integration, and operations. The remaining gaps provide a clear direction toward becoming a more capable and professional systems-oriented engineer.
