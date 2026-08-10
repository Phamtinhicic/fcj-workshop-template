---
title: "Chuẩn bị tài khoản và công cụ"
date: 2026-08-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

# Chuẩn bị tài khoản và công cụ

## Yêu cầu

- AWS account dev có Budget alert; Region `ap-southeast-1`.
- IAM deployment owner có quyền CloudFormation, IAM role/pass-role và các dịch vụ trong template.
- Node.js 22 LTS, npm 10+, AWS CLI v2, AWS SAM CLI và Git.
- Google Cloud project, OAuth consent screen, Web OAuth client và test user.
- Email gửi đã được verify trong SES tại cùng Region.

Không dùng root cho công việc hằng ngày. Mỗi thành viên dùng IAM user/session riêng và không chia sẻ access key dài hạn.

## Kiểm tra môi trường

```bash
node --version
npm --version
aws --version
sam --version
aws sts get-caller-identity
aws configure get region
```

Account và Region phải đúng môi trường nhóm đã thống nhất. Trong AWS CloudShell có thể đặt:

```bash
export AWS_REGION=ap-southeast-1
export AWS_DEFAULT_REGION=ap-southeast-1
```

## Chuẩn bị source

```bash
git clone https://github.com/Ngct253/CampusMeet.git
cd CampusMeet
npm ci
npm run infra:validate
npm run typecheck
npm test
```

Không chạy `npm audit fix --force` trong workshop vì có thể nâng major dependency và làm thay đổi lockfile ngoài phạm vi triển khai.

## Chuẩn bị dịch vụ ngoài

1. Verify `SesFromEmail` trong Amazon SES; nếu account còn sandbox thì recipient test cũng phải verified.
2. Tạo secret Google dạng JSON `{ "clientId": "...", "clientSecret": "..." }` trong Secrets Manager.
3. Nếu bật AI generation, tạo secret Bedrock/Mantle theo contract của template; không lưu key trong parameter file.
4. Ghi lại Google Cloud project number để build frontend và cấu hình Meet Add-on.

## Bằng chứng nên chụp

- `aws sts get-caller-identity` đã che UserId nhạy cảm nếu cần.
- Kết quả `sam --version`, Node 22 và `infra:validate` pass.
- SES identity ở trạng thái Verified.
- OAuth consent ở Testing và danh sách test user.
