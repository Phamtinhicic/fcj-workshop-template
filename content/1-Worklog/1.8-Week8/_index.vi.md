---
title: "Worklog Tuần 8"
date: 2026-07-27
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

## WORKLOG TUẦN 8

### Mục tiêu

- Chuyển ý tưởng CampusMeet thành yêu cầu có thể thiết kế và phát triển.
- Xây dựng user flow, mô hình dữ liệu và kiến trúc tổng thể trên AWS.
- Làm rõ hợp đồng giao tiếp giữa các phần để các thành viên có thể làm việc song song.
- Thiết lập quy trình review nhằm phát hiện sớm xung đột giữa giao diện, API và hạ tầng.

### Công việc thực hiện

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| Thứ Hai (Tại nhà) | **Phân tích yêu cầu:**<br>- Chuyển danh sách chức năng thành user story và tiêu chí hoàn thành.<br>- Mô tả các vai trò người dùng và quyền trong nhóm.<br>- Xác định luồng chính: đăng nhập, tạo nhóm, tạo cuộc họp, mời thành viên, tải tài liệu và theo dõi công việc.<br>- Đánh dấu các câu hỏi chưa rõ để không tự giả định trong lúc thiết kế. | 27/07/2026 | 27/07/2026 | [Writing User Stories](https://www.atlassian.com/agile/project-management/user-stories) |
| Thứ Ba (Tại nhà) | **Phác thảo giao diện và luồng điều hướng:**<br>- Vẽ wireframe cho đăng nhập, dashboard, nhóm, chi tiết cuộc họp và cài đặt.<br>- Xác định trạng thái tải, rỗng, lỗi và không có quyền.<br>- Kiểm tra luồng từ dashboard tới cuộc họp có ngắn và dễ hiểu hay không.<br>- Gửi bản nháp để các thành viên góp ý trước buổi làm việc trực tiếp. | 28/07/2026 | 28/07/2026 | [Material Design](https://m3.material.io/)<br>[Google Meet Add-ons](https://developers.google.com/meet/add-ons) |
| Thứ Tư (Văn phòng) | **Workshop thiết kế kiến trúc và dữ liệu:**<br>- Cùng nhóm rà soát user flow và chỉnh các điểm chưa thống nhất.<br>- Xác định kiến trúc serverless gồm frontend, API, xác thực, dữ liệu, lưu trữ và xử lý bất đồng bộ.<br>- Thảo luận mô hình các thực thể User, Group, Meeting, Invitation, File, Task và AIJob.<br>- Chốt quy ước ID, trạng thái và quan hệ giữa các bảng.<br>- Phân công người cập nhật sơ đồ kiến trúc, mô hình dữ liệu và API contract sau cuộc họp. | 29/07/2026 | 29/07/2026 | [AWS Serverless](https://aws.amazon.com/serverless/)<br>[Amazon DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html) |
| Thứ Năm (Tại nhà) | **Hoàn thiện tài liệu thiết kế phần được giao:**<br>- Cập nhật luồng quản lý cuộc họp và nội dung người dùng.<br>- Xác định dữ liệu đầu vào/đầu ra, trạng thái lỗi và yêu cầu idempotency.<br>- Mô tả cách S3 lưu file, DynamoDB lưu metadata và dịch vụ nền xử lý AIJob.<br>- Gửi pull request tài liệu để nhóm review thay vì chỉnh trực tiếp trên nhánh chính. | 30/07/2026 | 30/07/2026 | [Amazon S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html)<br>[AWS Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/welcome.html) |
| Thứ Sáu (Tại nhà) | **Đồng bộ API contract và phụ thuộc giữa các module:**<br>- So sánh tên trường giữa wireframe, shared types, API và database.<br>- Thống nhất cấu trúc phản hồi thành công/lỗi và mã trạng thái.<br>- Ghi rõ module nào cung cấp tài nguyên dùng chung cho module khác.<br>- Bổ sung tiêu chí kiểm thử cho các luồng quan trọng.<br>- Review chéo tài liệu của thành viên khác và phản hồi theo từng vấn đề cụ thể. | 31/07/2026 | 31/07/2026 | [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)<br>[AWS API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html) |
| Thứ Bảy (Tại nhà) | **Rà soát cuối tuần và lập kế hoạch triển khai:**<br>- Tổng hợp các quyết định đã được nhóm chấp thuận.<br>- Đưa các vấn đề chưa thống nhất vào backlog thay vì trì hoãn toàn bộ nhóm.<br>- Chia công việc thành các commit và pull request nhỏ.<br>- Lập thứ tự triển khai: nền tảng dữ liệu/xác thực trước, sau đó API nghiệp vụ, tích hợp và giao diện. | 01/08/2026 | 01/08/2026 | [Kiến trúc CampusMeet](https://github.com/Ngct253/CampusMeet/blob/main/docs/architecture.md)<br>[API contract](https://github.com/Ngct253/CampusMeet/blob/main/docs/api-contract.md)<br>[Backlog của nhóm](https://github.com/Ngct253/CampusMeet/issues) |

### Thành tích đạt được tuần 8

- Hoàn thiện bộ user flow và wireframe cơ bản cho CampusMeet.
- Thống nhất kiến trúc serverless tổng thể và mô hình dữ liệu dùng chung.
- Xây dựng API contract, shared types và quy ước trạng thái để các mảng phát triển đồng bộ.
- Xác định thứ tự triển khai và phụ thuộc giữa các module, giảm nguy cơ chờ đợi lẫn nhau.

### Khó khăn và cách giải quyết:

- **Khó khăn:** Tên trường và trạng thái giữa giao diện, API và dữ liệu chưa đồng nhất.<br>**Cách xử lý:** Tạo shared types và API contract làm nguồn tham chiếu chung; thay đổi phải được review trước khi áp dụng.
- **Khó khăn:** Các module phụ thuộc nhau nên một thành viên chậm có thể ảnh hưởng cả nhóm.<br>**Cách xử lý:** Tách interface khỏi implementation, dùng dữ liệu mẫu khi cần và ghi rõ đầu vào/đầu ra để các phần có thể phát triển song song.
- **Khó khăn:** Thiết kế hạ tầng có nguy cơ vượt phạm vi và phát sinh chi phí.<br>**Cách xử lý:** Ưu tiên serverless, môi trường dev, giới hạn tài nguyên và chỉ bổ sung dịch vụ khi có yêu cầu rõ ràng.


