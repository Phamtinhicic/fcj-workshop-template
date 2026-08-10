---
title: "Week 4 Worklog"
date: 2026-06-29
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

## WORKLOG TUẦN 4

### Mục tiêu

- Khám phá dịch vụ cơ sở dữ liệu trên đám mây: tìm hiểu kiến trúc và triển khai Amazon Relational Database Service (Amazon RDS).
- Thực hành cấu hình Amazon RDS: khởi tạo DB Instance, thiết lập mạng và bảo mật để backend Node.js hoặc FastAPI kết nối an toàn.
- Tìm hiểu Amazon Lightsail và quy trình triển khai nhanh một ứng dụng với mô hình chi phí đơn giản.
- Nghiên cứu tính sẵn sàng cao và cơ chế tự động mở rộng bằng Amazon EC2 Auto Scaling.
- Tạo Launch Template và Auto Scaling Group để tự động tăng hoặc giảm số lượng EC2 theo tải thực tế.
- Kết hợp Application Load Balancer, Health Check và CloudWatch metric để phân phối lưu lượng và theo dõi quá trình scaling.

### Công việc thực hiện

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| Thứ Hai (Tại nhà) | **Tìm hiểu kiến trúc và chuẩn bị Amazon RDS:**<br>- Tìm hiểu DB Engine, DB Instance Class, Storage, Endpoint, Port, Backup và Maintenance Window.<br>- So sánh RDS với việc tự cài cơ sở dữ liệu trên EC2; tìm hiểu Single-AZ và Multi-AZ.<br>- Chọn MySQL hoặc PostgreSQL phù hợp với backend thực hành.<br>- Tạo DB Subnet Group từ các Private Subnet thuộc ít nhất hai Availability Zone.<br>- Tạo Security Group cho RDS, chỉ cho phép cổng database nhận kết nối từ Security Group của backend EC2.<br>- Giữ DB Instance ở chế độ không public; kiểm tra luồng kết nối backend → RDS trong VPC. | 29/06/2026 | 29/06/2026 | [Tạo cơ sở dữ liệu trên Amazon RDS](https://000005.awsstudygroup.com/vi/)<br>[Thiết lập môi trường Amazon RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_SettingUp.html) |
| Thứ Ba (Tại nhà) | **Khởi tạo RDS và kết nối ứng dụng:**<br>- Tạo DB Instance với cấu hình phù hợp môi trường học tập và bật mã hóa lưu trữ.<br>- Cấu hình database name, username quản trị và chính sách backup.<br>- Lấy RDS Endpoint, Port và kiểm tra DNS/network từ EC2 backend.<br>- Cấu hình backend Node.js hoặc FastAPI dùng biến môi trường; không ghi thông tin đăng nhập database trực tiếp vào mã nguồn.<br>- Cài database driver, mở kết nối và thực hiện tạo bảng, thêm, đọc, cập nhật, xóa dữ liệu thử nghiệm.<br>- Theo dõi Connections, CPU và Storage trên RDS Monitoring; tạo manual snapshot trước khi thay đổi hoặc xóa DB Instance.<br>- Dọn tài nguyên thử nghiệm sau khi hoàn tất để tránh phát sinh chi phí. | 30/06/2026 | 30/06/2026 | [Amazon RDS](https://000005.awsstudygroup.com/vi/) |
| Thứ Tư (Tại nhà) | **Triển khai nhanh với Amazon Lightsail:**<br>- Tìm hiểu Bundle, Blueprint, Instance, Static IP, Snapshot và Firewall của Lightsail.<br>- Chọn Linux blueprint và gói tài nguyên nhỏ phù hợp cho bài thực hành.<br>- Khởi tạo Lightsail Instance, kết nối SSH trên trình duyệt và cập nhật hệ thống.<br>- Cấu hình firewall chỉ mở SSH, HTTP/HTTPS cần thiết.<br>- Triển khai một ứng dụng web mẫu, kiểm tra bằng Public IP và gắn Static IP nếu cần địa chỉ ổn định.<br>- So sánh Lightsail với EC2 về mức độ đơn giản, khả năng tùy biến, mở rộng và mô hình chi phí.<br>- Xóa Static IP hoặc instance không còn sử dụng. | 01/07/2026 | 01/07/2026 | [Tối ưu chi phí với Amazon Lightsail](https://000045.awsstudygroup.com/vi/)<br>[Static IP trong Lightsail](https://docs.aws.amazon.com/lightsail/latest/userguide/lightsail-create-static-ip.html) |
| Thứ Năm (Tại nhà) | **Tìm hiểu EC2 Auto Scaling và tạo Launch Template:**<br>- Tìm hiểu Desired, Minimum, Maximum Capacity; Scale Out, Scale In, Cooldown và Instance Warmup.<br>- Tìm hiểu vai trò của Launch Template, Auto Scaling Group, Application Load Balancer và Target Group.<br>- Tạo Launch Template gồm AMI, Instance Type, Security Group, IAM Instance Profile và User Data tự động cài web server/ứng dụng.<br>- Tạo phiên bản Launch Template và kiểm tra một EC2 thử nghiệm có khởi động ứng dụng thành công.<br>- Chuẩn bị VPC với ít nhất hai Public Subnet ở hai Availability Zone cho hệ thống có tính sẵn sàng cao. | 02/07/2026 | 02/07/2026 | [Amazon EC2 Auto Scaling](https://000006.awsstudygroup.com/vi/)<br>[Launch Template cho Auto Scaling](https://docs.aws.amazon.com/autoscaling/ec2/userguide/create-launch-template.html) |
| Thứ Sáu (Tại nhà) | **Thực hành Auto Scaling theo tải:**<br>- Tạo Application Load Balancer và Target Group; cấu hình Health Check cho đường dẫn ứng dụng.<br>- Tạo Auto Scaling Group từ Launch Template trên ít nhất hai Availability Zone.<br>- Thiết lập Min = 1, Desired = 2, Max = 3 cho môi trường thực hành.<br>- Gắn Auto Scaling Group với Target Group và kiểm tra lưu lượng được phân phối đến các EC2 healthy.<br>- Tạo Target Tracking Scaling Policy theo CPU trung bình hoặc số request trên mỗi target.<br>- Tạo tải thử trong thời gian ngắn, quan sát CloudWatch metric và Scaling Activity khi hệ thống scale out.<br>- Dừng tải, quan sát scale in sau thời gian warmup/cooldown và xác nhận hệ thống vẫn phục vụ qua Load Balancer.<br>- Xóa Auto Scaling Group, Load Balancer, Target Group và tài nguyên thử nghiệm sau khi lưu minh chứng. | 03/07/2026 | 03/07/2026 | [Tự động mở rộng với EC2 Auto Scaling](https://000006.awsstudygroup.com/vi/)<br>[Tạo Auto Scaling Group](https://docs.aws.amazon.com/autoscaling/ec2/userguide/create-asg-launch-template.html)<br>[Target Tracking Scaling Policy](https://docs.aws.amazon.com/autoscaling/ec2/userguide/as-scaling-target-tracking.html) |
| Thứ Bảy | Nghỉ. | 04/07/2026 | 04/07/2026 | — |

### Thành tích đạt được tuần 4

**Amazon RDS và kết nối ứng dụng:**

- Hiểu cấu trúc RDS, DB Instance, DB Subnet Group, Endpoint, Backup và Multi-AZ.
- Tạo RDS trong Private Subnet và giới hạn truy cập bằng Security Group của backend.
- Kết nối backend Node.js hoặc FastAPI đến database mà không công khai DB Instance.
- Thực hiện các thao tác CRUD, theo dõi metric và tạo snapshot dữ liệu.

**Amazon Lightsail:**

- Hiểu mô hình Bundle và quy trình triển khai đơn giản của Lightsail.
- Khởi tạo instance, cấu hình firewall, kết nối SSH và triển khai ứng dụng mẫu.
- So sánh được trường hợp sử dụng Lightsail với EC2.

**Tính sẵn sàng cao và Auto Scaling:**

- Tạo Launch Template có User Data để tự động cấu hình EC2.
- Tạo Auto Scaling Group hoạt động trên nhiều Availability Zone.
- Kết nối Auto Scaling Group với Application Load Balancer và Health Check.
- Cấu hình Target Tracking Policy và quan sát quá trình scale out/scale in.
- Biết dọn dẹp các tài nguyên có chi phí như RDS, Lightsail, EC2 và Load Balancer sau thực hành.
