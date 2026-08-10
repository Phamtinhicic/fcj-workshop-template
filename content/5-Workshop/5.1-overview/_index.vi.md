---
title: "Tổng quan kiến trúc"
date: 2026-08-01
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

# Tổng quan kiến trúc

![Kiến trúc tổng thể CampusMeet](/images/5-Workshop/campusmeet-aws-architecture.png)

CampusMeet dùng kiến trúc serverless và chia trách nhiệm thành bốn vùng:

1. **Trải nghiệm người dùng:** React SPA và Google Meet Add-on dùng chung API, JWT và quy tắc phân quyền.
2. **API nghiệp vụ:** API Gateway xác thực JWT trước khi gọi API Lambda; application service kiểm tra membership/role.
3. **Dữ liệu và nội dung:** năm bảng DynamoDB chứa metadata; hai bucket S3 tách frontend khỏi nội dung người dùng.
4. **Xử lý nền và AI:** Scheduler/Reminder xử lý nhắc lịch; Step Functions/AI Worker xử lý job dài, Bedrock Knowledge Base và S3 Vectors cung cấp truy hồi có filter.

## Luồng request đồng bộ

Browser tải asset qua CloudFront, đăng nhập Cognito và gửi access token trong header `Authorization`. API Gateway kiểm tra issuer, audience và thời hạn token. API Lambda lấy định danh, xác minh membership active rồi mới đọc/ghi tài nguyên group-scoped. Response dùng một envelope nhất quán gồm `success`, `data` hoặc `error`, và `requestId`.

## Luồng upload bất đồng bộ

Client yêu cầu presigned URL; backend kiểm tra nhóm, MIME, kích thước và checksum rồi tạo object key xác định. Browser upload thẳng lên S3. Khi complete-upload, backend dùng `HeadObject` xác minh object trước khi tạo attachment và AIJob. Binary không đi qua API Gateway.

## Luồng AI

API ghi AIJob trước khi gọi `StartExecution`. Step Functions gọi AI Worker, chờ ingestion nếu cần và cập nhật trạng thái. Retry/recovery dùng cùng logical job. Nội dung đã duyệt được chuẩn hóa vào prefix `kb/`, ingest vào Knowledge Base và truy hồi với metadata `groupId`, `meetingId`, `sourceType`, `sourceId`, `version`, `approved`.

## Ranh giới stack

| Stack | Sở hữu |
| --- | --- |
| `campusmeet-dev-data` | năm bảng DynamoDB |
| `campusmeet-dev-user-content` | bucket user-content, state machine, reminder, scheduler role, SES configuration set |
| `campusmeet-dev-app` | CloudFront/frontend S3, API, Cognito, sync worker, AI Worker, Knowledge Base, alarms |

Thứ tự triển khai là **data → M4 user-content → application → frontend**. Không tạo thủ công tài nguyên trùng tên với tài nguyên CloudFormation quản lý.
