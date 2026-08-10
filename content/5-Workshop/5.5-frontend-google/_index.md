---
title: "Deploy frontend and Google Workspace"
date: 2026-08-01
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

# Deploy frontend and Google Workspace

Populate `apps/web/.env` with the Cognito IDs, API URL, numeric Google project number, and AWS Region. Vite variables are public and must never contain secrets.

```bash
npm run build --workspace @campusmeet/web
aws s3 sync apps/web/dist/ s3://<FrontendBucketName>/ --delete
aws cloudfront create-invalidation --distribution-id <DistributionId> --paths "/*"
```

Upload the contents of `dist` so `index.html` is at the bucket root. Wait for invalidation completion.

Configure an External OAuth app in Testing mode, add test users, register the CloudFront origin without a path, and register the exact API callback URI. Store the client secret only in Secrets Manager. Enable the Marketplace SDK, replace placeholder domains in the Meet Add-on manifest, create an unpublished HTTP deployment, and install it for test users.

Recommended screenshots: stack outputs, frontend bucket root, completed invalidation, redacted OAuth URLs, successful Google connection, Calendar event with Meet link, and the Meet side panel.
