---
title: "Smoke test, giám sát và dọn dẹp"
date: 2026-08-01
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

# Smoke test, giám sát và dọn dẹp

## Smoke test chức năng

Thực hiện bằng ít nhất hai tài khoản Cognito để kiểm tra cả quyền admin và member:

1. Đăng ký, xác nhận email, đăng nhập, refresh phiên và đăng xuất.
2. Tạo nhóm, mời tài khoản thứ hai, chấp nhận lời mời và kiểm tra membership.
3. Tạo cuộc họp; sửa agenda/thời gian; kiểm tra người ngoài nhóm bị từ chối.
4. Kết nối Google; tạo meeting mới; xác nhận Calendar event và Meet link.
5. Mở Meet link từ trang chi tiết và thử Meet Add-on.
6. Upload một tài liệu nhỏ; kiểm tra object nằm đúng prefix và attachment xuất hiện.
7. Xác nhận chỉ một AIJob được tạo khi complete/retry; execution đạt trạng thái thành công hoặc lỗi có thể giải thích.
8. Duyệt transcript/biên bản, chuyển action item thành task và kiểm tra dashboard.
9. Tạo hoặc cập nhật reminder; kiểm tra notification và email trong điều kiện SES cho phép.
10. Hủy cuộc họp và xác nhận Google sync/retry không tạo event trùng.

Mở DevTools Network để bảo đảm không có CORS error; `/health` trả 200; route bảo vệ không token trả 401; người dùng sai nhóm trả 403/404 theo contract.

## Quan sát hệ thống

- CloudWatch Logs: API, Reminder, Google Sync Worker và AI Worker.
- CloudWatch Alarms: API error, AI Worker error/duration và Google sync final failure.
- Step Functions: input/output từng state, retry và trạng thái terminal.
- DynamoDB: không sửa dữ liệu trực tiếp; chỉ kiểm tra item/index khi điều tra.
- S3: Block Public Access, encryption, CORS, lifecycle và object metadata/checksum.

Không ghi token, presigned URL hoặc transcript nhạy cảm vào ảnh báo cáo.

## Xử lý lỗi thường gặp

| Hiện tượng | Kiểm tra |
| --- | --- |
| CORS preflight fail | frontend origin trong API Gateway và Lambda response |
| OAuth redirect lỗi | URL Google Console và `GOOGLE_REDIRECT_URI` phải exact match |
| Trang con CloudFront 403 | custom error 403/404 trả `/index.html` cho SPA |
| Email không tới | SES Region, identity verified, sandbox và CloudWatch log |
| AIJob failed | execution graph, worker log, IAM, S3 key và secret/model configuration |
| Dữ liệu không đồng bộ | DynamoDB stream mapping và Google sync final-failure alarm |

## Dọn dẹp

Chỉ cleanup khi môi trường không còn dùng. Xóa theo thứ tự phụ thuộc: frontend objects/invalidation, application stack, M4 stack, rồi data stack. Do bảng có `Retain`, xóa stack không đồng nghĩa bảng đã biến mất. Kiểm tra riêng retained tables, S3 objects/buckets, schedules, log groups, Knowledge Base/data source, vector index/bucket, SNS topic, secrets và SES configuration set. Không xóa môi trường dùng chung nếu chưa được nhóm xác nhận.

## Điều kiện hoàn tất workshop

Ba stack ở trạng thái ổn định; frontend HTTPS mở được; auth và authorization pass; Google Calendar/Meet pass; upload và AIJob pass theo phạm vi hiện thực; dashboard/task/minutes hoạt động; log/alarm quan sát được; không có secret trong Git hoặc trình duyệt.
