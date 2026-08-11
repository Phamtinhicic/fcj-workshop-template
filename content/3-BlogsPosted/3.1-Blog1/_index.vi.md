---
title: "CampusMeet với AWS Serverless và Generative AI"
date: 2026-08-10
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# CampusMeet – Hệ thống quản lý cuộc họp và khai thác tri thức với AWS Serverless & Generative AI

CampusMeet bắt đầu từ một vấn đề quen thuộc: sau mỗi cuộc họp, lịch nằm trên Calendar, cuộc họp diễn ra trên Google Meet, tài liệu ở Drive, biên bản được ghi riêng và công việc sau họp lại được quản lý bằng một công cụ khác. Dữ liệu vì vậy bị phân tán và khó tiếp tục khai thác.

Từ bài toán đó, nhóm em xây dựng **CampusMeet** để quản lý xuyên suốt vòng đời **trước – trong – sau cuộc họp** và biến dữ liệu cuộc họp thành nguồn tri thức có thể tìm kiếm bằng AI. Hệ thống hướng đến nhóm học tập, nhóm đồ án và nhóm dự án nhỏ.

![Kiến trúc AWS của CampusMeet](/images/2-Proposal/campusmeet-aws-architecture.png)

## Phạm vi giải pháp

Thay vì xây dựng một nền tảng gọi video mới, CampusMeet tập trung vào giá trị phía sau cuộc họp: agenda, participant, reminder, transcript, biên bản, action item, task và knowledge retrieval. Google Calendar và Google Meet đảm nhiệm phần lịch và conference.

## Các điểm thiết kế chính

### Quản lý cuộc họp end-to-end

Amazon Cognito đảm nhiệm xác thực; Amazon API Gateway và AWS Lambda xử lý API nghiệp vụ; Amazon DynamoDB lưu dữ liệu nhóm, cuộc họp, biên bản, task và AI job. Data Model được thiết kế theo access pattern và gom về **5 physical DynamoDB tables**, thay vì tạo một bảng riêng cho từng entity.

### Tích hợp Google nhưng vẫn giữ dữ liệu nội bộ

CampusMeet quản lý meeting record nội bộ và sử dụng Google Calendar/Meet để tạo event cùng Meet link. Nếu artifact từ Google chưa sẵn sàng hoặc tài khoản không đủ quyền, hệ thống vẫn giữ dữ liệu nội bộ và sử dụng luồng fallback phù hợp.

### Upload và xử lý bất đồng bộ

Browser tải tài liệu hoặc audio lớn trực tiếp lên Amazon S3 bằng **Presigned URL**, tránh truyền toàn bộ file qua API Gateway và Lambda. Sau khi upload, AIJob và AWS Step Functions điều phối các bước xử lý bất đồng bộ.

### Generative AI và RAG nhiều cuộc họp

CampusMeet không chỉ tóm tắt một transcript mà hướng đến hỏi đáp trên nhiều meeting, trả lời kèm citation tới meeting hoặc tài liệu nguồn. Retrieval phải lọc trước theo `groupId`, phạm vi meeting và ACL để người dùng không truy xuất dữ liệu ngoài quyền.

### AI hỗ trợ, con người phê duyệt

AI có thể tạo bản nháp biên bản hoặc đề xuất action item và task, nhưng không tự ghi dữ liệu nghiệp vụ. Người dùng phải review, xác nhận; backend sau đó kiểm tra quyền trước khi thực hiện thao tác thật. Nhóm em giữ nguyên tắc này để AI là trợ lý, không phải agent có quyền thay đổi dữ liệu ngoài kiểm soát.

### Vận hành và tối ưu chi phí

Kiến trúc MVP ưu tiên managed/serverless và chưa đưa EC2, RDS, EKS hay NAT Gateway vào khi chưa có nhu cầu. Amazon CloudWatch, Amazon SNS và Infrastructure as Code bằng AWS SAM/CloudFormation hỗ trợ monitoring, cảnh báo và triển khai lặp lại.

## Luồng giá trị xuyên suốt

**Meeting → Transcript → Minutes → Action Items → Tasks → Knowledge Base → RAG → Progress Analysis**

Điều em thấy thú vị không phải là số lượng dịch vụ AWS, mà là cách các dịch vụ được kết nối thành một luồng dữ liệu. Dữ liệu cuộc họp không bị đóng lại khi người dùng rời Google Meet, mà tiếp tục hỗ trợ những cuộc họp và quyết định sau này.

## Hướng phát triển

CampusMeet còn có thể mở rộng live transcription, Meet Add-on, khai thác thêm artifact từ Google Meet, CI/CD và khả năng RAG. Qua bài viết, em mong nhận được góp ý về Serverless Architecture, DynamoDB Data Modeling, Event-driven Workflow và Amazon Bedrock/RAG.

**Bài đăng gốc:** [AWS Study Group – CampusMeet](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2237833836981576/)

`#AWS` `#AWSVietnam` `#Serverless` `#AWSLambda` `#DynamoDB` `#AmazonBedrock` `#RAG` `#GenerativeAI` `#CloudArchitecture` `#CampusMeet`
