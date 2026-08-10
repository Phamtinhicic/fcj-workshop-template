---
title: "Đề xuất dự án"
date: 2026-07-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# CampusMeet – Nền tảng quản lý cuộc họp và cộng tác thông minh

## 1. Tóm tắt đề xuất

CampusMeet là nền tảng web hỗ trợ nhóm sinh viên và nhóm dự án quản lý toàn bộ vòng đời cuộc họp trên một không gian thống nhất: tạo nhóm, mời thành viên, lập lịch, tạo liên kết Google Meet, nhắc lịch, tải tài liệu hoặc bản ghi, quản lý biên bản, chuyển nội dung thành công việc và khai thác trợ lý AI có trích dẫn nguồn.

Giải pháp được xây dựng theo kiến trúc serverless trên AWS để giảm công việc vận hành máy chủ, tự động mở rộng theo nhu cầu và tách rõ dữ liệu nghiệp vụ, tệp người dùng và quy trình AI bất đồng bộ. Google Calendar và Google Meet được tích hợp qua OAuth 2.0; quyền truy cập tài nguyên luôn được kiểm tra lại tại backend theo nhóm và vai trò.

## 2. Vấn đề cần giải quyết

Các nhóm nhỏ thường phân tán thông tin cuộc họp giữa ứng dụng lịch, phòng họp trực tuyến, tin nhắn, tệp ghi chú và công cụ quản lý công việc. Điều này dẫn đến:

- thành viên bỏ lỡ lịch hoặc thay đổi cuộc họp;
- biên bản và tài liệu khó truy vết về đúng cuộc họp;
- công việc sau họp dễ bị quên hoặc giao trùng;
- người quản trị thiếu một màn hình theo dõi tiến độ chung;
- việc tìm lại quyết định cũ mất nhiều thời gian;
- tệp, transcript và token tích hợp có nguy cơ bị chia sẻ sai phạm vi.

CampusMeet gom các luồng trên thành một quy trình có kiểm soát, trong đó cuộc họp là trung tâm liên kết lịch, thành viên, tài liệu, transcript, biên bản, công việc và kết quả AI.

## 3. Mục tiêu và phạm vi

### Mục tiêu chính

1. Cung cấp đăng ký, đăng nhập và quản lý phiên an toàn.
2. Cho phép tạo nhóm, mời thành viên và phân quyền `GROUP_ADMIN`/`MEMBER`.
3. Quản lý cuộc họp, người tham dự, chương trình họp và trạng thái.
4. Đồng bộ Google Calendar và tạo liên kết Google Meet.
5. Tạo thông báo trong ứng dụng và email nhắc lịch.
6. Upload trực tiếp tệp lên S3 bằng presigned URL, không chuyển binary qua Lambda.
7. Quản lý transcript, biên bản, action item và task.
8. Điều phối AIJob bất đồng bộ, hỗ trợ hỏi đáp/biên bản có citation.
9. Cung cấp dashboard tiến độ nhóm, logging và cảnh báo vận hành.

### Ngoài phạm vi MVP

- Tự xây hệ thống video call/WebRTC.
- Thay thế Google Calendar hoặc Google Meet.
- Lưu access token, client secret hoặc nội dung nhạy cảm trong frontend.
- Bảo đảm Google luôn cung cấp transcript/recording; upload thủ công vẫn là luồng dự phòng.

## 4. Đối tượng sử dụng

| Vai trò | Nhu cầu chính |
| --- | --- |
| Quản trị viên nhóm | Tạo nhóm, mời/xóa thành viên, quản lý quyền và theo dõi tiến độ |
| Người tổ chức | Tạo/sửa/hủy cuộc họp, đồng bộ Calendar/Meet, nhắc lịch |
| Thành viên | Xem lịch, tham gia Meet, đọc tài liệu, nhận và cập nhật công việc |
| Người ghi biên bản | Chỉnh sửa transcript, duyệt biên bản và action item |
| Người vận hành | Theo dõi log, alarm, lỗi đồng bộ và AIJob |

## 5. Yêu cầu chức năng

- **Danh tính:** Cognito xác thực người dùng; API trả hồ sơ hiện tại qua `/me`.
- **Nhóm và lời mời:** tạo nhóm, tạo lời mời, chấp nhận/từ chối và quản lý membership.
- **Cuộc họp:** CRUD, hủy mềm, agenda, attendee, kiểm soát cập nhật đồng thời và idempotency.
- **Google Workspace:** OAuth consent, lưu refresh token phía server, tạo/cập nhật sự kiện Calendar và Meet link.
- **Thông báo:** notification trong ứng dụng là nguồn tin cậy; SES là kênh gửi bổ sung và lỗi email không rollback notification.
- **Nội dung người dùng:** presign, upload trực tiếp S3, kiểm tra MIME/kích thước/checksum và complete-upload.
- **Transcript và AI:** chỉ final segment được lưu; tài liệu đã duyệt mới được ingest; kết quả sinh có citation về đúng nguồn.
- **Công việc:** chuyển action item thành task một cách nguyên tử và theo dõi trạng thái trên dashboard.

## 6. Kiến trúc giải pháp

![Kiến trúc AWS của CampusMeet](/images/2-Proposal/campusmeet-aws-architecture.png)

Luồng chính:

1. Người dùng tải React SPA từ CloudFront; bucket frontend S3 là private origin.
2. Cognito phát JWT; API Gateway xác thực token trước khi gọi API Lambda.
3. API Lambda thực thi use case, kiểm tra membership/role và truy cập năm bảng DynamoDB.
4. Calendar/Meet được gọi bằng credential OAuth lưu trong Secrets Manager và dữ liệu token mã hóa phía server.
5. EventBridge Scheduler gọi Reminder Lambda; Lambda ghi notification và thử gửi SES.
6. Browser upload tệp trực tiếp vào user-content S3 bằng URL ngắn hạn.
7. API tạo AIJob idempotent và khởi chạy Step Functions.
8. AI Worker xử lý tài liệu, gọi Amazon Bedrock, Knowledge Base và S3 Vectors.
9. CloudWatch thu log/metric; alarm gửi qua SNS.

## 7. Thiết kế dữ liệu

Hệ thống sử dụng năm bảng DynamoDB vật lý với khóa tổng hợp `PK/SK`, GSI theo access pattern và TTL cho dữ liệu hết hạn:

| Bảng | Dữ liệu tiêu biểu |
| --- | --- |
| `identity` | hồ sơ, OAuth integration, notification |
| `collaboration` | group, membership, invitation |
| `meeting-data` | meeting, attendee, agenda, transcript metadata |
| `task-data` | task, assignment, trạng thái tiến độ |
| `ai-work` | AIJob, conversation, citation, knowledge source, proposal |

Tệp nhị phân và vector không lưu trong DynamoDB. Tệp nằm trong S3 private; vector nằm trong S3 Vectors và chỉ metadata cần truy vấn được lưu ở bảng.

## 8. Bảo mật và độ tin cậy

- HTTPS cho toàn bộ luồng public; S3 bật Block Public Access và mã hóa tại rest.
- JWT hợp lệ chưa đủ quyền: backend luôn kiểm tra membership active và role trên từng tài nguyên.
- IAM áp dụng least privilege theo từng Lambda/role; không dùng access key trong source.
- Google client secret và Bedrock API key nằm trong Secrets Manager.
- Presigned URL có thời hạn, object key xác định theo group/meeting và checksum SHA-256.
- Mutation quan trọng dùng idempotency key; conditional write ngăn ghi đè cạnh tranh.
- Step Functions quản lý retry và trạng thái job; recovery không tạo logical job thứ hai.
- Log không chứa token, presigned URL, transcript đầy đủ hoặc model response nhạy cảm.
- CloudFormation/SAM là source of truth để triển khai lặp lại và rollback có kiểm soát.

## 9. Công nghệ sử dụng

| Lớp | Công nghệ |
| --- | --- |
| Frontend | React, TypeScript, Vite, AWS Amplify client |
| API | API Gateway HTTP API, AWS Lambda Node.js 22, TypeScript |
| Identity | Amazon Cognito |
| Data | Amazon DynamoDB, Amazon S3, S3 Vectors |
| Orchestration | AWS Step Functions, EventBridge Scheduler |
| AI | Amazon Bedrock, Knowledge Bases, AI Worker Lambda |
| Integration | Google OAuth 2.0, Calendar API, Meet Add-on, Amazon SES |
| Observability | CloudWatch Logs/Alarms, Amazon SNS |
| IaC/Delivery | AWS SAM, CloudFormation, GitHub, npm workspaces |

## 10. Kế hoạch thực hiện

| Giai đoạn | Kết quả |
| --- | --- |
| Phân tích | SRS, use case, phạm vi MVP, rủi ro và API contract |
| Thiết kế | Kiến trúc AWS, mô hình DynamoDB, security boundary |
| Nền tảng | 5 bảng, Cognito, API skeleton, frontend shell |
| Nghiệp vụ | nhóm, lời mời, cuộc họp, task, notification |
| Tích hợp | Google OAuth/Calendar/Meet, upload S3, reminder |
| AI | AIJob, Step Functions, worker, Knowledge Base và citation |
| Hoàn thiện | test, smoke test cloud, logging, tài liệu và demo |

## 11. Chi phí dự kiến

Môi trường dev ưu tiên free tier và pay-per-request. Chi phí phát sinh phụ thuộc số request, dung lượng S3/DynamoDB, thời gian Lambda/Step Functions, email SES, lượt embedding/retrieval/generation Bedrock và log CloudWatch. Nhóm cần thiết lập AWS Budgets, alarm chi phí và dọn object, schedule, log, vector index hoặc stack thử nghiệm không còn sử dụng. Không nên ghi một con số cố định khi chưa có workload đo được; nên lập estimate theo ba mức: demo, nhóm nhỏ và production.

## 12. Rủi ro và phương án xử lý

| Rủi ro | Ảnh hưởng | Giảm thiểu |
| --- | --- | --- |
| OAuth redirect/CORS sai | Không đăng nhập hoặc kết nối Google | Dùng output stack, exact redirect URI và smoke test preflight |
| SES sandbox | Không gửi được email ngoài danh sách verified | Verify sender/recipient hoặc xin production access |
| Transcript Google không có | Thiếu dữ liệu AI | Upload audio/tài liệu và live capture làm fallback |
| AI chạy lâu hoặc gọi lặp | Tăng chi phí, dữ liệu trùng | AIJob idempotent, Step Functions retry/recovery |
| Lộ dữ liệu giữa nhóm | Rủi ro bảo mật cao | Kiểm tra membership tại backend và filter metadata theo group |
| Deploy thủ công lệch cấu hình | Khó tái tạo/rollback | Quản lý bằng SAM/CloudFormation và review change set |

## 13. Tiêu chí hoàn thành

- Người dùng đăng ký/đăng nhập và truy cập đúng dữ liệu theo quyền.
- Tạo nhóm, mời thành viên và quản lý cuộc họp hoạt động end-to-end.
- Kết nối Google, tạo sự kiện Calendar và mở Meet link thành công.
- Upload tệp an toàn, tạo một AIJob và theo dõi trạng thái đến khi hoàn tất.
- Transcript/biên bản/action item/task giữ đúng liên kết và không tạo trùng khi retry.
- Frontend chạy qua CloudFront; API health trả 200; CORS/JWT hoạt động đúng.
- CloudWatch có log/alarm cần thiết; secrets không xuất hiện trong source hoặc output.

## 14. Kết quả mong đợi

CampusMeet cung cấp một quy trình họp có thể truy vết từ lịch hẹn đến quyết định và công việc sau họp. Dự án đồng thời thể hiện khả năng thiết kế hệ thống serverless, mô hình hóa NoSQL theo access pattern, bảo mật tích hợp OAuth, xử lý tệp trực tiếp trên S3 và điều phối AI bất đồng bộ trên AWS.
