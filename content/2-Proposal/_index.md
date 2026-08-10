---
title: "Proposal"
date: 2026-07-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# CampusMeet – Intelligent Meeting and Collaboration Platform

## 1. Executive summary

CampusMeet is a web platform that manages the complete meeting lifecycle for student and project teams: groups and invitations, scheduling, Google Meet links, reminders, documents and recordings, transcripts, minutes, action items, tasks, and grounded AI assistance.

The solution uses an AWS serverless architecture to minimize server operations, scale with demand, and separate business data, user files, and asynchronous AI processing. Google Calendar and Google Meet are connected through OAuth 2.0, while every group-scoped operation is authorized again by the backend.

## 2. Problem statement

Small teams commonly spread meeting information across calendars, video tools, chat, documents, and task trackers. Members miss changes, decisions become difficult to find, action items are duplicated or forgotten, and administrators lack a consolidated progress view. Sharing files and integration tokens without a clear security boundary also creates privacy risks.

CampusMeet addresses this fragmentation by making the meeting the central entity that links participants, agenda, documents, transcript, minutes, decisions, and follow-up work.

## 3. Objectives and scope

The project provides secure authentication; group membership and role management; meeting CRUD and attendance; Google Calendar/Meet synchronization; in-app and email reminders; direct-to-S3 upload; transcript and minutes workflows; action-item-to-task conversion; group dashboards; and asynchronous AI jobs with source citations.

The MVP does not implement its own video/WebRTC service, replace Google Calendar, expose secrets in browser code, or assume that Google always provides a recording or transcript. Manual upload remains a required fallback.

## 4. Users

| Role | Primary needs |
| --- | --- |
| Group administrator | Create groups, manage invitations/members and monitor progress |
| Meeting organizer | Schedule, update, cancel and synchronize meetings |
| Member | View meetings, join Google Meet, access files and update assigned tasks |
| Minutes editor | Review transcripts, minutes and action items |
| Operator | Inspect logs, alarms, synchronization failures and AI jobs |

## 5. Functional capabilities

- **Identity:** Cognito authentication and current-user profile.
- **Collaboration:** groups, memberships, invitations, acceptance and decline.
- **Meetings:** CRUD, agenda, attendees, cancellation, optimistic concurrency and idempotency.
- **Google Workspace:** OAuth consent, server-side refresh tokens, Calendar events and Meet links.
- **Notifications:** durable in-app notification with SES as a best-effort secondary channel.
- **User content:** presigned upload, MIME/size/checksum validation and completion verification.
- **Transcript and AI:** final-segment persistence, approved-source ingestion and cited outputs.
- **Tasks:** atomic conversion of approved action items and dashboard progress.

## 6. Solution architecture

![CampusMeet AWS architecture](/images/2-Proposal/campusmeet-aws-architecture.png)

1. CloudFront serves the React SPA from a private S3 origin.
2. Cognito issues JWTs and API Gateway authenticates requests before invoking Lambda.
3. The API Lambda enforces membership/role rules and accesses five DynamoDB tables.
4. Google APIs use OAuth credentials kept on the server side.
5. EventBridge Scheduler invokes the Reminder Lambda, which writes a notification and attempts SES delivery.
6. Browsers upload files directly to a private user-content bucket using short-lived URLs.
7. The API creates one idempotent AIJob and starts a Step Functions execution.
8. The AI Worker uses Amazon Bedrock, Knowledge Bases, and S3 Vectors.
9. CloudWatch collects telemetry and alarms notify through SNS.

## 7. Data design

Five DynamoDB tables use composite `PK/SK` keys, access-pattern GSIs, and TTL where appropriate:

| Table | Main data |
| --- | --- |
| `identity` | profiles, OAuth integration, notifications |
| `collaboration` | groups, memberships, invitations |
| `meeting-data` | meetings, attendees, agenda, transcript metadata |
| `task-data` | tasks, assignments and progress |
| `ai-work` | AI jobs, conversations, citations and knowledge sources |

Binary files remain in private S3, while vectors live in S3 Vectors. DynamoDB stores only queryable control and business metadata.

## 8. Security and reliability

- HTTPS, S3 Block Public Access, encryption at rest, and short-lived presigned URLs.
- Resource-level authorization in the API in addition to JWT validation.
- Least-privilege IAM roles for API, workers, scheduler, state machine, and Knowledge Base.
- OAuth client secret and Bedrock API key in Secrets Manager.
- Deterministic object keys and SHA-256 verification for immutable user content.
- Idempotency keys and conditional writes for retry-safe mutations.
- Step Functions retry/recovery without creating a second logical AI job.
- Logs exclude tokens, full sensitive transcripts, presigned URLs, and model responses.
- SAM/CloudFormation acts as the reproducible infrastructure source of truth.

## 9. Technology stack

| Layer | Technology |
| --- | --- |
| Web | React, TypeScript, Vite |
| API | API Gateway, Node.js 22 Lambda, TypeScript |
| Identity | Amazon Cognito |
| Storage | DynamoDB, Amazon S3, S3 Vectors |
| Workflow | Step Functions, EventBridge Scheduler |
| AI | Amazon Bedrock, Knowledge Bases, AI Worker Lambda |
| Integration | Google OAuth/Calendar/Meet, Amazon SES |
| Operations | CloudWatch and SNS |
| Delivery | AWS SAM, CloudFormation, GitHub and npm workspaces |

## 10. Delivery plan

The implementation progresses through requirements and API contracts, AWS architecture and DynamoDB access patterns, identity/data foundations, collaboration and meeting vertical slices, Google and upload integrations, AI orchestration, and finally automated tests, cloud smoke tests, monitoring, documentation, and demonstration.

## 11. Cost approach

Development uses pay-per-request and free-tier allowances where practical. Actual cost depends on requests, S3/DynamoDB usage, Lambda and Step Functions duration, SES messages, Bedrock embedding/retrieval/generation, and CloudWatch retention. AWS Budgets and cleanup checks are required. Estimates should be maintained for demo, small-team, and production workloads instead of presenting an unsupported fixed value.

## 12. Risks and mitigations

| Risk | Mitigation |
| --- | --- |
| Incorrect OAuth redirect or CORS | Consume stack outputs, register exact URLs, and run preflight smoke tests |
| SES sandbox restrictions | Verify identities or request production access |
| Missing Google transcript | Keep direct upload and live capture as fallback paths |
| Duplicate/long-running AI work | Idempotent AIJob plus controlled Step Functions recovery |
| Cross-group data exposure | Backend membership checks and group-filtered knowledge metadata |
| Configuration drift | Deploy reviewed SAM/CloudFormation change sets |

## 13. Acceptance criteria

Users can authenticate and access only authorized group data; create groups and meetings; synchronize a Calendar event and join Google Meet; securely upload content and observe one AI job; maintain transcript/minutes/task relationships without duplication; use the CloudFront frontend and healthy API; and inspect operational logs without exposing secrets.

## 14. Expected outcome

CampusMeet provides a traceable meeting workflow from scheduling to decisions and follow-up tasks. It also demonstrates practical serverless design, access-pattern-driven NoSQL modeling, secure OAuth integration, direct object storage, and asynchronous grounded-AI orchestration on AWS.
