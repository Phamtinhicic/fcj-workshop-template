---
title: "Tự đánh giá"
date: 2026-08-10
weight: 6
chapter: false
pre: " <b> 6. </b> "
---

# Tự đánh giá quá trình thực tập

## 1. Tổng quan

Trong thời gian thực tập từ **22/06/2026 đến 15/08/2026** tại chương trình **Workforce Bootcamp – First Cloud AI Journey**, em đã từng bước chuyển từ việc tìm hiểu các dịch vụ AWS cơ bản sang tham gia xây dựng và triển khai một sản phẩm theo quy trình làm việc nhóm. Dự án chính mà nhóm thực hiện là **CampusMeet** – nền tảng hỗ trợ quản lý nhóm, lập lịch cuộc họp, tích hợp Google Calendar/Google Meet, quản lý tài liệu, biên bản, công việc sau cuộc họp và xử lý nội dung bằng AI.

Quá trình thực tập giúp em hiểu rằng việc hoàn thành một hệ thống không chỉ là viết được mã nguồn. Một sản phẩm có thể vận hành cần kiến trúc phù hợp, hợp đồng API rõ ràng, phân quyền an toàn, hạ tầng có thể tái triển khai, quy trình kiểm thử, tài liệu hướng dẫn và sự phối hợp liên tục giữa các thành viên.

## 2. Kiến thức và kỹ năng đạt được

### Kiến thức AWS và hạ tầng đám mây

- Hiểu vai trò của IAM User, Group, Policy và Role; áp dụng nguyên tắc đặc quyền tối thiểu và hạn chế sử dụng tài khoản root.
- Thực hành với VPC, subnet, route table, Internet Gateway, Security Group và EC2 để hiểu luồng kết nối trong môi trường AWS.
- Tìm hiểu và sử dụng S3, CloudFront, DynamoDB, Lambda, API Gateway, Cognito, SES, EventBridge Scheduler, Step Functions, CloudWatch và CloudFormation/SAM.
- Biết đọc CloudFormation change set, kiểm tra stack output, xác định nguyên nhân rollback và xử lý lỗi quyền IAM khi triển khai tài nguyên.
- Hiểu cách dùng AWS CLI và SAM CLI để validate, build, deploy và kiểm tra tài nguyên thay cho thao tác hoàn toàn thủ công trên Console.

### Phát triển hệ thống CampusMeet

- Tham gia phân tích yêu cầu, phạm vi chức năng và kiến trúc serverless của hệ thống.
- Làm việc với frontend React/Vite, backend Node.js/TypeScript và các hợp đồng dữ liệu dùng chung.
- Triển khai phần tích hợp nội dung người dùng và điều phối AI: S3 upload, AIJob, Step Functions, Lambda nhắc lịch và các IAM role liên quan.
- Cấu hình Google OAuth, Calendar và Meet; hiểu mối quan hệ giữa authorized origin, redirect URI, API callback và biến môi trường frontend/backend.
- Thực hiện build frontend, upload lên S3, phân phối qua CloudFront và tạo invalidation sau khi cập nhật phiên bản.
- Kiểm tra các luồng chính: đăng nhập, tạo nhóm, tạo cuộc họp, kết nối Google, tạo liên kết Meet, tải tài liệu và theo dõi execution của Step Functions.

### Kỹ năng làm việc

- Chia công việc thành commit và pull request nhỏ, đọc kết quả CI và phối hợp xử lý xung đột khi nhiều thành viên sửa cùng khu vực mã nguồn.
- Ghi nhận tiến độ, vấn đề, nguyên nhân và hướng xử lý thay vì chỉ báo cáo kết quả cuối cùng.
- Chủ động tra cứu tài liệu AWS, Google Cloud và tài liệu nội bộ của dự án khi gặp lỗi triển khai.
- Cải thiện khả năng trao đổi với nhóm, thống nhất dependency giữa các phần và xác định thứ tự triển khai data foundation, M4 và application stack.

## 3. Khó khăn và cách giải quyết

### Khó khăn về quyền AWS

Trong lần triển khai đầu, CloudFormation không thể tạo IAM Role do tài khoản thực thi thiếu quyền `iam:CreateRole` và quyền tagging. Em đã đọc sự kiện stack, xác định đúng resource thất bại, chuyển sang tài khoản/role quản trị được nhóm cho phép và triển khai lại. Qua đó, em rút kinh nghiệm phải kiểm tra danh tính AWS, Region và quyền cần thiết trước khi chạy deployment.

### Khó khăn về cấu hình môi trường

Frontend từng không gọi được API do CORS, API URL và CloudFront origin chưa đồng bộ. Google OAuth cũng gặp lỗi do redirect URI khác với URI thực tế của Lambda. Em đã đối chiếu CloudFormation outputs, biến môi trường Lambda, cấu hình API Gateway CORS và Google OAuth Client; sau đó build, upload lại frontend và tạo CloudFront invalidation.

### Khó khăn khi tích hợp mã nguồn nhóm

Một số pull request phát sinh conflict vì các thành viên cùng chỉnh sửa service, adapter, kiểu dữ liệu và template hạ tầng. Em học cách cập nhật nhánh từ `main`, so sánh ý nghĩa của hai phía, giữ lại hợp đồng mới cần thiết và chạy lại kiểm thử thay vì chọn toàn bộ một phía. Điều này giúp hạn chế làm mất chức năng của thành viên khác.

### Khó khăn trong triển khai hạ tầng

Việc triển khai theo từng phần thủ công dễ tạo tài nguyên trùng hoặc cấu hình không đồng nhất. Nhóm đã chuyển các tài nguyên quan trọng vào SAM/CloudFormation, chuẩn hóa output và dependency giữa các stack. Em nhận thấy Infrastructure as Code là yếu tố cần thiết để hệ thống có thể được tái triển khai và bàn giao.

## 4. Bảng tự đánh giá

| STT | Tiêu chí | Mức tự đánh giá | Minh chứng |
| ---: | --- | --- | --- |
| 1 | Kiến thức và kỹ năng chuyên môn | **Tốt** | Hiểu và triển khai được nhiều dịch vụ AWS; tham gia xây dựng CampusMeet end-to-end. |
| 2 | Khả năng học hỏi | **Tốt** | Chủ động đọc tài liệu, thử nghiệm và điều chỉnh khi gặp dịch vụ hoặc lỗi mới. |
| 3 | Tính chủ động | **Khá** | Có thể tự xử lý phần việc được giao nhưng đôi lúc còn cần xác nhận khi thay đổi ảnh hưởng nhiều module. |
| 4 | Tinh thần trách nhiệm | **Tốt** | Theo dõi công việc đến lúc deploy và smoke test, không dừng ở mức hoàn thành local. |
| 5 | Kỷ luật và tuân thủ quy trình | **Khá** | Tuân thủ quy trình nhóm; cần duy trì tốt hơn việc cập nhật tài liệu ngay khi cấu hình thay đổi. |
| 6 | Giao tiếp và báo cáo | **Khá** | Báo cáo được tiến độ và lỗi; cần trình bày ngắn gọn và có cấu trúc hơn trong các vấn đề phức tạp. |
| 7 | Hợp tác nhóm | **Tốt** | Phối hợp dependency, review, xử lý conflict và hỗ trợ kiểm tra luồng tích hợp. |
| 8 | Giải quyết vấn đề | **Khá** | Có khả năng đọc log và khoanh vùng lỗi; cần nâng cao tốc độ xác định nguyên nhân gốc. |
| 9 | Quản lý thời gian | **Khá** | Hoàn thành phần việc chính; một số giai đoạn triển khai kéo dài do chưa dự đoán đủ dependency. |
| 10 | Đóng góp cho dự án | **Tốt** | Hoàn thiện M4, tài liệu triển khai, proposal, workshop và hỗ trợ đưa hệ thống lên AWS. |
| 11 | Tác phong chuyên nghiệp | **Tốt** | Tôn trọng thành viên, tiếp nhận phản hồi và thận trọng với secret, quyền truy cập, dữ liệu dùng chung. |
| 12 | Đánh giá tổng thể | **Khá – Tốt** | Đạt mục tiêu thực tập và tạo được sản phẩm có thể trình diễn; vẫn còn khả năng tối ưu và tự động hóa. |

## 5. Hạn chế cần cải thiện

- Cần nâng cao khả năng thiết kế trước khi triển khai để giảm số lần sửa cấu hình và deploy lại.
- Cần viết kiểm thử tự động đầy đủ hơn cho các luồng tích hợp AWS, Google OAuth và trường hợp idempotency/recovery.
- Cần cải thiện kỹ năng trình bày kỹ thuật, đặc biệt là mô tả dependency và tác động của thay đổi đối với thành viên khác.
- Cần tìm hiểu sâu hơn về bảo mật production, quản lý secret, least privilege, logging dữ liệu nhạy cảm và tối ưu chi phí.
- Cần xây dựng CI/CD để tự động hóa build, test và deploy, giảm phụ thuộc vào thao tác thủ công trên CloudShell/Console.

## 6. Kế hoạch phát triển sau thực tập

1. Hoàn thiện pipeline CI/CD cho frontend và hạ tầng serverless.
2. Bổ sung integration test, contract test và kịch bản phục hồi khi dịch vụ bên ngoài gặp lỗi.
3. Nghiên cứu sâu Amazon Bedrock, Knowledge Base, S3 Vectors và đánh giá chất lượng câu trả lời có trích dẫn.
4. Cải thiện khả năng quan sát hệ thống bằng dashboard, structured logging, alarm và truy vết request.
5. Tiếp tục rèn luyện kỹ năng làm việc nhóm, review code và viết tài liệu kỹ thuật có thể bàn giao.

## 7. Kết luận

Em tự đánh giá đã hoàn thành tốt các mục tiêu chính của kỳ thực tập: xây dựng nền tảng kiến thức AWS, làm quen với quy trình kỹ thuật trong môi trường nhóm và tham gia đưa CampusMeet từ ý tưởng đến một hệ thống có thể triển khai, kiểm thử và trình diễn. Giá trị lớn nhất em đạt được là khả năng nhìn một chức năng trong toàn bộ vòng đời của sản phẩm — từ yêu cầu, mã nguồn, hạ tầng, bảo mật, tích hợp đến vận hành. Những hạn chế còn lại là cơ sở để em tiếp tục cải thiện theo hướng trở thành một kỹ sư có tư duy hệ thống và làm việc chuyên nghiệp hơn.
