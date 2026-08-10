---
title: "Smoke testing, monitoring, and cleanup"
date: 2026-08-01
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

# Smoke testing, monitoring, and cleanup

Use at least two Cognito users. Test sign-up/sign-in/session/logout; group creation and invitation acceptance; meeting create/update/cancel and cross-group denial; Google connection, Calendar event, Meet link, and Add-on; direct document upload; idempotent AIJob execution; transcript/minutes/action-item/task flow; reminders and notifications; and Google synchronization retry.

Verify `/health` is 200, unauthenticated protected routes return 401, unauthorized resources are rejected, and browser Network has no CORS failures.

Inspect API, Reminder, Google Sync, and AI Worker log groups; API/AI/sync alarms; Step Functions execution graphs; S3 security and checksum metadata; and the DynamoDB stream mapping. Never place tokens, presigned URLs, or sensitive transcripts in report screenshots.

Common failures include mismatched CORS origins, non-exact OAuth redirects, missing SPA fallback for CloudFront paths, SES sandbox restrictions, AI Worker IAM/model configuration, and disabled DynamoDB stream mappings.

For cleanup, remove resources in dependency order and obtain team approval first. Retained DynamoDB tables and adopted S3 buckets may survive stack deletion, so inspect tables, objects, schedules, logs, Knowledge Base resources, vector storage, SNS, secrets, and SES configuration separately.
