---
title: "CampusMeet with AWS Serverless and Generative AI"
date: 2026-08-10
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# CampusMeet – Meeting management and knowledge discovery with AWS Serverless & Generative AI

CampusMeet began with a familiar problem: schedules live in Calendar, meetings happen in Google Meet, documents are stored elsewhere, minutes are written separately, and follow-up work moves to another tool. The resulting knowledge is fragmented and difficult to reuse.

My team built **CampusMeet** to manage the **before, during, and after** stages of a meeting and turn meeting artifacts into searchable knowledge. It targets study groups, student projects, and small project teams.

![CampusMeet AWS architecture](/images/2-Proposal/campusmeet-aws-architecture.png)

## Solution scope

CampusMeet does not replace video conferencing. It focuses on agendas, participants, reminders, transcripts, minutes, action items, tasks, and knowledge retrieval while integrating Google Calendar and Google Meet for scheduling and conferencing.

## Key design decisions

- **End-to-end meeting management:** Amazon Cognito provides authentication, API Gateway and Lambda implement the business APIs, and DynamoDB stores groups, meetings, minutes, tasks, and AI jobs. Access-pattern-oriented modeling consolidates the model into five physical tables.
- **Google integration without losing internal ownership:** CampusMeet stores its own meeting records and uses Google for events and Meet links. Fallback behavior preserves internal data when a Google artifact is unavailable or permission is insufficient.
- **Asynchronous upload and processing:** the browser uploads large documents or audio directly to Amazon S3 through presigned URLs. AIJob records and AWS Step Functions coordinate the remaining pipeline.
- **Cross-meeting RAG:** answers can include citations to source meetings and documents. Retrieval is filtered by `groupId`, meeting scope, and ACL before generation.
- **Human approval:** AI creates drafts and suggestions, but users review and approve them before the backend validates authorization and changes business data.
- **Cost-aware operations:** the MVP favors managed serverless services and uses CloudWatch, SNS, AWS SAM, and CloudFormation for observability and repeatable deployment.

## End-to-end value flow

**Meeting → Transcript → Minutes → Action Items → Tasks → Knowledge Base → RAG → Progress Analysis**

The most interesting aspect for me is not the number of AWS services. It is the continuous data flow that keeps meeting knowledge useful after participants leave Google Meet.

Future directions include better live transcription, a Meet Add-on, broader Google Meet artifact support, CI/CD, and stronger RAG capabilities.

**Original post:** [AWS Study Group – CampusMeet](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2237833836981576/)
