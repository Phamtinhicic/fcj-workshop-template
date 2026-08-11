---
title: "Chia sẻ, đóng góp ý kiến"
date: 2026-08-10
weight: 7
chapter: false
pre: " <b> 7. </b> "
---

# Chia sẻ và đóng góp ý kiến

## Điều em hài lòng

First Cloud AI Journey tạo cho em một lộ trình từ kiến thức AWS nền tảng đến quá trình xây dựng sản phẩm theo nhóm. Em được thực hành IAM, VPC, EC2, S3, RDS, CloudWatch, AWS CLI, kiến trúc serverless và Generative AI thay vì chỉ đọc lý thuyết.

Các buổi làm việc tại văn phòng và sự kiện giúp em làm quen với môi trường chuyên nghiệp, trao đổi trực tiếp với mentor và các thành viên khác. Em đánh giá cao tinh thần cởi mở: em có thể đặt câu hỏi, tự thử giải pháp, nhận góp ý và sửa lại khi kết quả chưa đúng.

## Kỹ năng em phát triển

- Phân tích yêu cầu và chuyển một ý tưởng thành phạm vi MVP;
- thiết kế kiến trúc AWS theo hướng managed/serverless và cân nhắc chi phí;
- làm việc với IAM, CloudFormation/AWS SAM, API Gateway, Lambda, DynamoDB, S3, Step Functions, CloudWatch, Cognito và Amazon Bedrock;
- phối hợp nhóm qua Git, commit nhỏ, pull request, review và xử lý conflict;
- kiểm tra log, phân tích lỗi CORS, OAuth, quyền IAM và dependency giữa các module;
- trình bày kiến trúc, viết tài liệu kỹ thuật và chia sẻ kiến thức với cộng đồng.

## Khó khăn và cách em xử lý

Khó khăn lớn nhất của em là các module trong CampusMeet phụ thuộc lẫn nhau. Một thay đổi ở Data Foundation, Auth hoặc State Machine có thể ảnh hưởng đến API và frontend. Nhóm em giải quyết bằng cách thống nhất API contract, output của hạ tầng, thứ tự triển khai và chia thay đổi thành pull request nhỏ.

Trong quá trình deploy, em cũng gặp lỗi quyền IAM, OAuth redirect URI, CORS, CloudFront cache, merge conflict và giới hạn dung lượng CloudShell. Em học cách đọc thông báo lỗi, kiểm tra CloudFormation events và CloudWatch logs, xác minh từng biến môi trường, xây dựng lại artifact, tạo invalidation và trao đổi với thành viên phụ trách module liên quan.

## Đề xuất của em

- Có checklist onboarding chung cho AWS account, IAM, budget và công cụ ngay từ đầu;
- công bố dependency map và thứ tự deploy giữa các module trước giai đoạn tích hợp;
- duy trì buổi sync hoặc architecture review ngắn hằng tuần;
- có một hướng dẫn deploy, rollback, cleanup và kiểm soát chi phí dùng chung;
- bổ sung thêm phiên demo, code review, mock interview và chia sẻ kinh nghiệm từ các anh chị đi trước.

## Định hướng tiếp theo

Em muốn tiếp tục hoàn thiện CampusMeet về CI/CD, bảo mật, observability và RAG; đồng thời củng cố kiến thức để theo đuổi hướng Cloud/Backend Engineering. Em sẵn sàng giới thiệu chương trình cho các bạn muốn học AWS qua một lộ trình có thực hành và làm việc nhóm thực tế.

Em cảm ơn ban tổ chức, mentor và các thành viên đã hỗ trợ em trong quá trình tham gia First Cloud AI Journey.
