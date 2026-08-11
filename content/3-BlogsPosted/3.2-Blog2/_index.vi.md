---
title: "AWS Lambda MicroVMs cho môi trường thực thi cách ly"
date: 2026-08-10
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# AWS Lambda MicroVMs – “sandbox” serverless cho code do người dùng hoặc AI sinh ra

Khi xây dựng AI Coding Agent, Online IDE hoặc Code Runner, một câu hỏi quan trọng là: làm sao chạy code do người dùng hoặc AI tạo ra một cách an toàn, cách ly tốt mà developer không phải tự quản lý cả hệ thống VM hoặc container?

AWS Lambda MicroVMs hướng đến nhóm bài toán này. Khác với Lambda Function truyền thống thường xử lý theo luồng `Request → Lambda → Execute → Response`, MicroVM hướng đến môi trường thực thi riêng theo session hoặc job, có thể giữ filesystem và trạng thái trong quá trình làm việc.

## Ví dụ với AI Coding Agent

`Generate code → Install dependencies → Build → Run tests → Read errors → Fix code → Test again`

Thay vì chạy tất cả trên máy developer hoặc tự xây sandbox bằng EC2/container, chuỗi thao tác có thể chạy trong một MicroVM được cách ly:

`User / AI Agent → Application / API → Lambda MicroVM → Result / Output`

Bên trong môi trường có thể gồm source code, dependencies, filesystem, runtime/terminal và session state.

## Nền tảng cách ly

Điểm đáng chú ý là Lambda MicroVMs dựa trên **Firecracker**, công nghệ microVM được AWS sử dụng phía sau Lambda và Fargate. MicroVM cung cấp ranh giới cách ly mạnh hơn tiến trình thông thường trong khi khởi tạo nhẹ hơn máy ảo truyền thống.

## Use case phù hợp

- AI Coding Agent;
- Online IDE hoặc Coding Playground;
- Chạy code do người dùng submit;
- CI/CD Runner;
- Vulnerability và Security Scanning;
- Data Analysis Sandbox.

## Cách em nhìn về sự mở rộng của serverless

**Lambda Function → Serverless Function Execution**

**Lambda MicroVM → Serverless Isolated Execution Environment**

Trước đây câu hỏi phổ biến là “làm sao chạy backend mà không quản lý server?”. Với AI Agent, câu hỏi đang chuyển thành “làm sao chạy code do người dùng hoặc AI tạo ra an toàn mà vẫn không tự quản lý hạ tầng sandbox?”.

Khi agent có thể tự tạo file, cài dependency, chạy terminal, build và test, em cho rằng môi trường thực thi cách ly sẽ là một mảnh ghép quan trọng. Tuy vậy, hệ thống thực tế vẫn phải kiểm soát quyền, mạng, tài nguyên, thời gian chạy, dữ liệu đầu vào và log kiểm toán; sandbox không thay thế toàn bộ thiết kế bảo mật.

**Bài đăng gốc:** [AWS Study Group – Lambda MicroVMs](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2238689133562713/)

`#AWS` `#AWSLambda` `#LambdaMicroVMs` `#Serverless` `#Firecracker` `#CloudComputing` `#AI` `#CodingAgent` `#DeveloperTools`
