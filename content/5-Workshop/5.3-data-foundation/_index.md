---
title: "Deploy the data foundation"
date: 2026-08-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

# Deploy the data foundation

Validate `infra/data-foundation.yaml`, preview a change set, and confirm that it contains only the five expected DynamoDB tables. Tables use on-demand billing, `PK/SK`, encryption, TTL, required GSIs, and retain policies.

```bash
sam validate --template-file infra/data-foundation.yaml --lint --region ap-southeast-1
sam deploy \
  --template-file infra/data-foundation.yaml \
  --stack-name campusmeet-dev-data \
  --resolve-s3 \
  --parameter-overrides Environment=dev TablePrefix=campusmeet-dev \
    EnablePointInTimeRecovery=false EnableDeletionProtection=false \
  --region ap-southeast-1
```

Run `scripts/verify-data-foundation.ps1` with the expected account ID. Save the stack outputs, especially the meeting-data stream ARN required by the Google synchronization worker. A successful template validation is not proof of deployment; the stack must reach `CREATE_COMPLETE` or `UPDATE_COMPLETE`.
