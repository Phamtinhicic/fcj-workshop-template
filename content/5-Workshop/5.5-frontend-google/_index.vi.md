---
title: "Triển khai frontend và Google Workspace"
date: 2026-08-01
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

# Triển khai frontend và Google Workspace

## Cấu hình frontend

Tạo `apps/web/.env` từ file mẫu và điền output thật:

```dotenv
VITE_COGNITO_USER_POOL_ID=<UserPoolId>
VITE_COGNITO_USER_POOL_CLIENT_ID=<UserPoolClientId>
VITE_API_BASE_URL=<ApiUrl>
VITE_GOOGLE_CLOUD_PROJECT_NUMBER=<numeric-project-number>
VITE_AWS_REGION=ap-southeast-1
```

Các biến `VITE_*` nằm trong bundle public nên tuyệt đối không chứa secret.

```bash
npm run build --workspace @campusmeet/web
aws s3 sync apps/web/dist/ s3://<FrontendBucketName>/ --delete
aws cloudfront create-invalidation --distribution-id <DistributionId> --paths "/*"
```

Chỉ upload **nội dung bên trong** `dist`, để `index.html` nằm ở root bucket. Đợi invalidation `Completed`, sau đó hard refresh.

## Google OAuth

Trong Google Auth Platform:

- User type: External; publishing status Testing.
- Thêm email thử nghiệm vào Test users.
- Authorized JavaScript origin: đúng CloudFront origin, không có path hoặc dấu `/` cuối.
- Authorized redirect URI: đúng `<ApiUrl>/integrations/google/callback`.
- Scope tối thiểu gồm OpenID/email/profile và Calendar/Meet scope mà ứng dụng thực sự dùng.

Client secret chỉ nằm trong Secrets Manager. Lambda `GOOGLE_REDIRECT_URI` và giá trị trên Google Console phải khớp từng ký tự.

## Meet Add-on

1. Bật Google Workspace Marketplace SDK.
2. Thay domain mẫu trong manifest bằng CloudFront origin.
3. Tạo unpublished HTTP deployment.
4. Cài cho test user và mở side panel trong một cuộc Google Meet đang hoạt động.
5. Kiểm tra Add-on dùng cùng API/JWT và không có kho dữ liệu riêng.

## Ảnh bằng chứng nên cung cấp

- CloudFormation Outputs của ba stack.
- S3 frontend có `index.html` và thư mục `assets`.
- CloudFront distribution và invalidation Completed.
- OAuth client với origin/redirect đã che client ID nếu cần.
- Màn hình kết nối Google thành công và sự kiện Calendar có Meet link.
- Meet Add-on side panel trong cuộc họp.
