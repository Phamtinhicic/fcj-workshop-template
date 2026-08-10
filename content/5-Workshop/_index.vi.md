---
title: "Workshop CampusMeet"
date: 2026-08-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Xây dựng và triển khai CampusMeet trên AWS

Workshop này hướng dẫn dựng CampusMeet từ source code đến môi trường AWS dev hoàn chỉnh. Người học sẽ triển khai data foundation, user-content/AI orchestration, application stack, frontend CloudFront và tích hợp Google Calendar/Meet; sau đó chạy smoke test và quan sát hệ thống.

![Kiến trúc AWS của CampusMeet](/images/5-Workshop/campusmeet-aws-architecture.png)

## Kết quả đạt được

- React SPA được phân phối bằng CloudFront từ S3 private.
- Cognito xác thực người dùng; HTTP API gọi Lambda Node.js 22.
- Năm bảng DynamoDB lưu dữ liệu nghiệp vụ.
- S3 user-content, Step Functions, Reminder Lambda, Scheduler và SES được cấu hình.
- Google OAuth/Calendar/Meet hoạt động với redirect URI chính xác.
- AI Worker, Bedrock Knowledge Base và S3 Vectors sẵn sàng cho tài liệu đã duyệt.
- CloudWatch Logs/Alarms và SNS hỗ trợ vận hành.

## Nội dung

1. [Tổng quan kiến trúc](5.1-overview/)
2. [Chuẩn bị tài khoản và công cụ](5.2-prerequisites/)
3. [Triển khai nền tảng dữ liệu](5.3-data-foundation/)
4. [Triển khai M4 và application stack](5.4-backend-infrastructure/)
5. [Triển khai frontend và Google Workspace](5.5-frontend-google/)
6. [Smoke test, giám sát và dọn dẹp](5.6-validation-cleanup/)

{{% notice warning %}}
Không đưa access key, OAuth client secret, token, API key Bedrock hoặc nội dung `.env` vào Git. Luôn kiểm tra AWS Account ID, Region và CloudFormation change set trước khi xác nhận deploy.
{{% /notice %}}
