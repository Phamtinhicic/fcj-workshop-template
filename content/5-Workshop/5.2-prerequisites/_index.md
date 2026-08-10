---
title: "Account and tooling prerequisites"
date: 2026-08-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

# Account and tooling prerequisites

Use an AWS development account with a budget alarm in `ap-southeast-1`, a dedicated deployment owner, Node.js 22 LTS, npm 10+, AWS CLI v2, SAM CLI, Git, a Google Cloud OAuth project, and an SES-verified sender. Avoid daily root usage and long-lived shared access keys.

```bash
node --version
npm --version
aws --version
sam --version
aws sts get-caller-identity
aws configure get region
```

Clone and validate the source:

```bash
git clone https://github.com/Ngct253/CampusMeet.git
cd CampusMeet
npm ci
npm run infra:validate
npm run typecheck
npm test
```

Prepare the SES identity, a Google OAuth secret containing `clientId` and `clientSecret`, the numeric Google Cloud project number, and the Bedrock/Mantle secret required by the selected environment. Never place these secrets in Git or Vite variables.

Recommended evidence includes tool versions, the correct AWS identity/Region, successful infrastructure validation, the verified SES identity, and the OAuth test-user configuration.
