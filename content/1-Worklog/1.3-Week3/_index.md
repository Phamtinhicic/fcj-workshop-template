---
title: "Week 3 Worklog"
date: 2026-06-22
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

## WORKLOG TUẦN 3

### Mục tiêu

- Tìm hiểu và cấu hình IAM Role: cấp quyền an toàn cho ứng dụng chạy trên EC2 truy cập các dịch vụ AWS khác mà không lưu trực tiếp Access Key và Secret Access Key trên máy chủ.
- Làm quen với môi trường lập trình đám mây trên trình duyệt: tìm hiểu AWS Cloud9, xác minh giới hạn áp dụng với tài khoản mới và sử dụng AWS CloudShell làm môi trường thực hành thay thế.
- Khám phá Amazon S3 (Simple Storage Service): hiểu mô hình Object Storage, Bucket, Object, Prefix, Region, Versioning và các cơ chế kiểm soát truy cập.
- Khởi tạo và cấu hình S3 Bucket để upload, tải xuống và quản lý dữ liệu.
- Thực hành Hosting Static Website trên Amazon S3 bằng mã nguồn HTML/CSS/JS.
- Hiểu tác động bảo mật của Bucket Policy và Block Public Access; chỉ cấp quyền đọc công khai tối thiểu cho bucket website thực hành.

### Công việc thực hiện

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| Thứ Hai (Văn phòng) | **IAM Role và môi trường phát triển trên trình duyệt:**<br>- Tìm hiểu sự khác nhau giữa IAM User, IAM Policy và IAM Role.<br>- Tạo IAM Policy chỉ cho phép các thao tác S3 cần thiết theo nguyên tắc Least Privilege.<br>- Tạo IAM Role có Trusted Entity là EC2 và gắn policy phù hợp.<br>- Gắn IAM Role vào EC2 thông qua Instance Profile.<br>- Kết nối SSH vào EC2 và dùng AWS CLI kiểm tra quyền truy cập S3 mà không cấu hình Access Key trên máy chủ.<br>- Tìm hiểu giao diện và cách hoạt động của AWS Cloud9 qua tài liệu.<br>- Xác minh Cloud9 không mở cho tài khoản AWS mới; chuyển sang dùng AWS CloudShell để chạy AWS CLI trực tiếp trên trình duyệt.<br>- Kiểm tra identity hiện tại bằng AWS STS và làm quen với trình soạn thảo, terminal, upload/download file trong CloudShell. | 22/06/2026 | 22/06/2026 | [IAM Role cho ứng dụng AWS](https://000048.awsstudygroup.com/vi/)<br>[AWS Cloud9](https://000049.awsstudygroup.com/vi/)<br>[Lịch sử AWS Cloud9](https://docs.aws.amazon.com/cloud9/latest/user-guide/history.html) |
| Thứ Ba (Tại nhà) | **Tìm hiểu và khởi tạo Amazon S3:**<br>- Tìm hiểu Object Storage và cấu trúc Bucket, Object, Object Key, Prefix, Metadata.<br>- Tìm hiểu quy tắc đặt tên bucket, lựa chọn Region và tính duy nhất toàn cầu của tên bucket.<br>- Tạo một S3 Bucket riêng cho bài thực hành, giữ nguyên Block Public Access mặc định.<br>- Upload, xem, tải xuống và xóa một số object bằng AWS Console.<br>- Tổ chức dữ liệu theo prefix; kiểm tra URL, metadata và dung lượng object.<br>- Bật Versioning và thử upload nhiều phiên bản của cùng một tệp. | 23/06/2026 | 23/06/2026 | [Khởi đầu với Amazon S3](https://000057.awsstudygroup.com/vi/)<br>[Bắt đầu với Amazon S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/GetStartedWithS3.html) |
| Thứ Tư (Tại nhà) | **Củng cố IAM Role và bảo mật S3:**<br>- Dùng EC2 Instance đã gắn IAM Role để liệt kê bucket, upload và tải object bằng AWS CLI.<br>- Xác nhận ứng dụng không chứa Access Key hoặc Secret Access Key trong mã nguồn và biến môi trường.<br>- Thử một thao tác nằm ngoài policy để quan sát lỗi AccessDenied và kiểm chứng Least Privilege.<br>- So sánh Identity-based Policy của IAM Role với Resource-based Policy của S3 Bucket.<br>- Kiểm tra Default Encryption, Versioning và Block Public Access của bucket dữ liệu. | 24/06/2026 | 24/06/2026 | [IAM Role cho EC2](https://000048.awsstudygroup.com/vi/)<br>[Thực hành tốt nhất về bảo mật S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/security-best-practices.html) |
| Thứ Năm | Nghỉ. | 25/06/2026 | 25/06/2026 | — |
| Thứ Sáu (Tại nhà) | **Hosting Static Website trên Amazon S3:**<br>- Chuẩn bị trang web tĩnh gồm `index.html`, tệp CSS, JavaScript và trang lỗi.<br>- Tạo một bucket chuyên biệt cho website, tách khỏi bucket dữ liệu riêng tư.<br>- Upload nội dung website và bật Static Website Hosting; cấu hình Index Document và Error Document.<br>- Tìm hiểu Block Public Access và rủi ro khi công khai bucket.<br>- Trong phạm vi bài thực hành, điều chỉnh Block Public Access ở bucket website và tạo Bucket Policy chỉ cho phép công khai hành động `s3:GetObject` đối với object.<br>- Mở website endpoint, kiểm tra HTML/CSS/JS và xử lý lỗi 403/404 nếu có.<br>- Ghi lại phương án an toàn hơn cho production: giữ S3 private và phân phối nội dung qua CloudFront với Origin Access Control (OAC).<br>- Sau khi hoàn tất minh chứng, xóa tài nguyên thử nghiệm hoặc bật lại Block Public Access nếu không tiếp tục sử dụng website. | 26/06/2026 | 26/06/2026 | [Hosting static website với Amazon S3](https://000057.awsstudygroup.com/vi/)<br>[Hướng dẫn Static Website trên S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/HostingWebsiteOnS3Setup.html) |
| Thứ Bảy | Nghỉ. | 27/06/2026 | 27/06/2026 | — |

### Thành tích đạt được tuần 3

**IAM Role và quyền truy cập an toàn:**

- Phân biệt được IAM User, IAM Policy, IAM Role và Instance Profile.
- Tạo IAM Role cho EC2 với trust policy và permission policy phù hợp.
- Cho phép EC2 truy cập S3 bằng temporary credentials do AWS tự quản lý, không lưu Access Key trên máy chủ.
- Kiểm chứng nguyên tắc Least Privilege bằng cả thao tác được phép và thao tác trả về AccessDenied.

**Môi trường phát triển trên trình duyệt:**

- Hiểu mục đích, cấu trúc và quy trình làm việc cơ bản của AWS Cloud9.
- Xác định chính xác giới hạn Cloud9 đối với tài khoản AWS mới.
- Sử dụng AWS CloudShell để chạy AWS CLI, kiểm tra danh tính và thao tác với tài nguyên ngay trên trình duyệt.

**Amazon S3 và Object Storage:**

- Hiểu các khái niệm Bucket, Object, Object Key, Prefix, Metadata, Region và Versioning.
- Tạo bucket, upload/download object và quản lý nhiều phiên bản dữ liệu.
- Hiểu vai trò của IAM Policy, Bucket Policy, Default Encryption và Block Public Access trong bảo vệ dữ liệu.

**Hosting Static Website:**

- Chuẩn bị và triển khai thành công website HTML/CSS/JS trên S3 website endpoint.
- Cấu hình Index Document, Error Document và quyền đọc object tối thiểu.
- Hiểu rủi ro của bucket công khai và biết phương án production an toàn hơn với S3 private, CloudFront và OAC.
- Biết kiểm tra, dọn dẹp hoặc khóa lại tài nguyên sau khi hoàn thành thực hành để giảm rủi ro và chi phí.
