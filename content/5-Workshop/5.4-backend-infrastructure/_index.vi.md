---
title: "Triển khai M4 và application stack"
date: 2026-08-01
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

# Triển khai M4 và application stack

## 1. Build M4

```bash
sam validate --template-file infra/user-content-orchestration.yaml --lint --region ap-southeast-1
sam build --template-file infra/user-content-orchestration.yaml --build-dir .aws-sam/m4
```

Xác định ARN AI Worker theo tên deterministic `campusmeet-dev-ai-worker`. State machine có thể được tạo trước function, nhưng ARN truyền vào phải đúng account và Region.

## 2. Deploy M4

```bash
sam deploy \
  --template-file .aws-sam/m4/template.yaml \
  --stack-name campusmeet-dev-user-content \
  --resolve-s3 \
  --capabilities CAPABILITY_IAM \
  --parameter-overrides Environment=dev DataTablePrefix=campusmeet-dev \
    AIWorkerFunctionArn=<AI_WORKER_ARN> \
    SesFromEmail=<VERIFIED_EMAIL> \
    ExistingUserContentBucketName=<EXISTING_BUCKET_OR_EMPTY> \
    FrontendOrigin=<CLOUDFRONT_ORIGIN> \
  --region ap-southeast-1
```

Nếu bucket được tạo thủ công, truyền tên bằng `ExistingUserContentBucketName`; CloudFormation sẽ không quản lý CORS/encryption/lifecycle của bucket đó. Với môi trường mới, để trống để stack sở hữu cấu hình.

Lưu năm output: `UserContentBucketName`, `AIStateMachineArn`, `ReminderFunctionArn`, `SchedulerExecutionRoleArn`, `SesConfigurationSetName`.

## 3. Build và deploy application

```bash
npm run infra:validate
sam validate --template-file infra/template.yaml --lint --region ap-southeast-1
sam build --template-file infra/template.yaml --build-dir /tmp/campusmeet-sam-app
```

Deploy template đã build với `CAPABILITY_IAM` và parameter lấy từ data/M4 stack: stream ARN, bucket, state machine, reminder, scheduler role, SES configuration set, Google secret/redirect, frontend origin và cấu hình Bedrock. Luôn preview change set trước; không xác nhận nếu có replace bảng/bucket hoặc xóa tài nguyên ngoài dự kiến.

Sau deploy, lấy các output: `ApiUrl`, `FrontendBucketName`, `CloudFrontDomainName`, `UserPoolId`, `UserPoolClientId`, `GoogleSyncWorkerFunctionName`, `AIWorkerFunctionName`, `KnowledgeBaseId` và alarm names.

## 4. Kiểm tra backend

```bash
curl -i "<ApiUrl>/health"
aws lambda get-function --function-name campusmeet-dev-google-sync-worker --region ap-southeast-1
aws stepfunctions describe-state-machine --state-machine-arn <AIStateMachineArn>
```

`/health` phải trả 200; Lambda phải `Active`; event-source mapping phải `Enabled`; state machine phải có thể hoàn tất một execution test.
