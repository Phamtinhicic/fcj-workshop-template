---
title: "Worklog Tuần 9"
date: 2026-08-03
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

## WORKLOG TUẦN 9

### Mục tiêu

- Chốt thiết kế đủ chi tiết để nhóm bắt đầu hiện thực CampusMeet mà không phải tự suy đoán yêu cầu.
- Thiết lập cấu trúc repository, quy ước code và cách tích hợp các phần việc.
- Chuẩn bị nền tảng cho quản lý nội dung người dùng, cuộc họp và luồng xử lý bất đồng bộ.
- Kiểm tra thiết kế bằng các luồng thử nhỏ trước khi mở rộng chức năng.

### Công việc thực hiện

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| Thứ Hai (Văn phòng) | **Kick-off giai đoạn hiện thực:**<br>- Cả nhóm trình bày phần thiết kế đã chuẩn bị và kiểm tra lại phạm vi.<br>- Chốt cấu trúc monorepo cho web, API, shared package, infrastructure và documentation.<br>- Thống nhất quy tắc đặt tên nhánh, commit, pull request và người review.<br>- Xác nhận phụ thuộc: data foundation và auth cần ổn định trước các luồng nghiệp vụ.<br>- Chia đầu việc theo milestone, đồng thời xác định tiêu chí bàn giao thay vì chỉ ghi tên chức năng. | 03/08/2026 | 03/08/2026 | [GitHub Flow](https://docs.github.com/en/get-started/using-github/github-flow)<br>[AWS SAM](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/what-is-sam.html) |
| Thứ Ba (Tại nhà) | **Chuẩn hóa thiết kế phần cuộc họp và nội dung:**<br>- Hoàn thiện kiểu dữ liệu Meeting, File, Invitation, Task và AIJob.<br>- Xác định quy tắc kiểm tra quyền theo người dùng và nhóm.<br>- Thiết kế luồng upload bằng presigned URL, checksum và metadata.<br>- Mô tả cách một file sau khi tải lên tạo công việc xử lý bất đồng bộ.<br>- Viết các trường hợp lỗi và hành vi khi người dùng gửi lại cùng một yêu cầu. | 04/08/2026 | 04/08/2026 | [S3 Presigned URLs](https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-presigned-url.html)<br>[Amazon S3 Checksums](https://docs.aws.amazon.com/AmazonS3/latest/userguide/checking-object-integrity.html) |
| Thứ Tư (Tại nhà) | **Thiết kế tích hợp Google Calendar/Meet và thông báo:**<br>- Rà soát OAuth, redirect URI, scope và cách bảo vệ client secret.<br>- Mô tả luồng kết nối tài khoản Google, tạo sự kiện và lưu liên kết Meet.<br>- Xác định vị trí sử dụng SES cho email nhắc lịch/lời mời và giới hạn của môi trường sandbox.<br>- Bổ sung các biến cấu hình cần thiết cho môi trường dev. | 05/08/2026 | 05/08/2026 | [Google OAuth 2.0](https://developers.google.com/identity/protocols/oauth2)<br>[Amazon SES](https://docs.aws.amazon.com/ses/latest/dg/Welcome.html) |
| Thứ Năm (Tại nhà) | **Thiết kế orchestration và khả năng phục hồi:**<br>- Xác định trạng thái vòng đời AIJob và state machine xử lý.<br>- Bổ sung nguyên tắc idempotency để không tạo hai logical job khi retry.<br>- Thiết kế cách phục hồi khi StartExecution không trả về kết quả rõ ràng hoặc orchestration khởi động thất bại.<br>- Ghi lại yêu cầu về log, request ID và trạng thái có thể truy vết khi xảy ra lỗi. | 06/08/2026 | 06/08/2026 | [Step Functions Error Handling](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-error-handling.html)<br>[AWS Lambda Powertools](https://docs.powertools.aws.dev/lambda/typescript/latest/) |
| Thứ Sáu (Tại nhà) | **Review chéo và xử lý xung đột thiết kế:**<br>- Review các pull request liên quan shared types, API contract và infrastructure template.<br>- Đối chiếu tài nguyên được tạo bởi từng stack để tránh trùng tên hoặc thiếu output.<br>- Chia các thay đổi lớn thành commit nhỏ, xử lý conflict dựa trên hợp đồng đã thống nhất thay vì chọn toàn bộ một phía.<br>- Chạy kiểm tra type, test và validate hạ tầng sau khi hợp nhất. | 07/08/2026 | 07/08/2026 | [CloudFormation Best Practices](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/best-practices.html)<br>[Pull request CampusMeet](https://github.com/Ngct253/CampusMeet/pulls) |
| Thứ Bảy (Tại nhà) | **Kiểm tra tiến độ và hoàn thiện tài liệu bàn giao:**<br>- Thực hiện smoke test các luồng đã sẵn sàng và ghi lại kết quả.<br>- Phân loại lỗi thành lỗi cấu hình, lỗi tích hợp và lỗi nghiệp vụ để giao đúng người xử lý.<br>- Cập nhật sơ đồ kiến trúc, hướng dẫn cấu hình môi trường và danh sách việc còn lại.<br>- Báo cáo nhóm phần đã hoàn thành, phần đang chờ phụ thuộc và kế hoạch tuần tiếp theo. | 08/08/2026 | 08/08/2026 | [AWS CloudWatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html)<br>[Hướng dẫn triển khai và kiểm thử M4](https://github.com/Ngct253/CampusMeet/blob/main/docs/m4-cloud-setup.md) |

### Thành tích đạt được tuần 9

- Chốt cấu trúc repository, quy trình nhánh/commit/pull request và trách nhiệm review.
- Hoàn thiện thiết kế chi tiết cho cuộc họp, nội dung người dùng, Google integration và AIJob orchestration.
- Xác định rõ các yêu cầu bảo mật, idempotency, kiểm tra tính toàn vẹn và khả năng phục hồi.
- Chuẩn hóa cách các stack hạ tầng trao đổi output/parameter và cách các module dùng shared types.
- Hoàn thành review thiết kế, validate cơ bản và tài liệu bàn giao để nhóm tiếp tục hiện thực.

### Khó khăn và cách giải quyết:

- **Khó khăn:** Nhiều thành viên cùng sửa shared types và infrastructure nên phát sinh conflict.<br>**Cách xử lý:** Đồng bộ nhánh thường xuyên, giới hạn phạm vi mỗi pull request, giải quyết conflict dựa trên API contract và chạy lại toàn bộ kiểm tra sau merge.
- **Khó khăn:** Các dịch vụ Google và AWS yêu cầu nhiều cấu hình ngoài mã nguồn, dễ sai redirect URI, CORS hoặc quyền IAM.<br>**Cách xử lý:** Lập checklist cấu hình theo môi trường, dùng Secrets Manager cho bí mật, ghi rõ output cần lấy và xác minh từng tích hợp bằng smoke test nhỏ.
- **Khó khăn:** Khó phân biệt chức năng đã hoàn thành local với chức năng đã sẵn sàng trên cloud.<br>**Cách xử lý:** Báo cáo riêng ba trạng thái: hoàn thành code, đã merge và đã deploy/kiểm thử; không đánh dấu hoàn thành chỉ dựa trên việc code chạy local.


