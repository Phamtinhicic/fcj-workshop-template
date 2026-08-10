---
title: "Triển khai nền tảng dữ liệu"
date: 2026-08-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

# Triển khai nền tảng dữ liệu

## Validate template

```bash
sam validate --template-file infra/data-foundation.yaml --lint --region ap-southeast-1
```

Template phải có đúng năm resource: `IdentityTable`, `CollaborationTable`, `MeetingDataTable`, `TaskDataTable`, `AIWorkTable`.

## Preview change set

```bash
sam deploy \
  --template-file infra/data-foundation.yaml \
  --stack-name campusmeet-dev-data \
  --resolve-s3 \
  --parameter-overrides Environment=dev TablePrefix=campusmeet-dev \
    EnablePointInTimeRecovery=false EnableDeletionProtection=false \
  --no-execute-changeset \
  --region ap-southeast-1
```

Trước khi execute, xác nhận change set chỉ thêm/cập nhật năm bảng dự kiến, không replace hoặc delete dữ liệu. Bảng dùng `PAY_PER_REQUEST`, khóa `PK/SK`, SSE, TTL `expiresAtEpoch`, GSI đúng access pattern, `DeletionPolicy: Retain` và `UpdateReplacePolicy: Retain`.

## Deploy và verify

Chạy lại lệnh trên nhưng bỏ `--no-execute-changeset`, sau đó:

```powershell
powershell -NoProfile -File scripts/verify-data-foundation.ps1 `
  -Region ap-southeast-1 `
  -TablePrefix campusmeet-dev `
  -ExpectedAccountId <AWS_ACCOUNT_ID>
```

Đọc output:

```bash
aws cloudformation describe-stacks \
  --stack-name campusmeet-dev-data \
  --query "Stacks[0].Outputs" \
  --region ap-southeast-1
```

Giữ lại `MeetingDataTableStreamArn`, vì application stack dùng DynamoDB Stream để kích hoạt Google sync worker. Stack phải ở `CREATE_COMPLETE` hoặc `UPDATE_COMPLETE`; không coi việc template validate thành công là bằng chứng đã deploy.
