---
title: "Worklog Tuần 5"
date: 2026-07-06
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

## WORKLOG TUẦN 5

### Mục tiêu

- Triển khai hệ thống giám sát với Amazon CloudWatch: thu thập metrics, logs và xây dựng Dashboard theo dõi sức khỏe hệ thống.
- Cấu hình CloudWatch Alarms và thông báo tự động khi CPU, RAM hoặc lưu lượng mạng vượt ngưỡng.
- Tìm hiểu Amazon Route 53, Hosted Zone và các loại DNS Record dùng để định tuyến tên miền.
- Nghiên cứu Hybrid DNS giữa môi trường Local và Amazon VPC bằng Route 53 Resolver.
- Cài đặt và sử dụng AWS CLI trên EC2 Ubuntu hoặc Windows mà không lưu khóa truy cập dài hạn.
- Viết shell script hoặc PowerShell script để quản lý tài nguyên, đồng bộ file và gọi dịch vụ AWS, tạo nền tảng cho CI/CD.

### Công việc thực hiện

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| Thứ Hai (Tại nhà) | **Thu thập metrics, logs và tạo CloudWatch Dashboard:**<br>- Tìm hiểu CloudWatch Metrics, Logs, Log Group, Log Stream, Dashboard và Logs Insights.<br>- Xem các EC2 metrics mặc định: CPUUtilization, NetworkIn, NetworkOut, DiskReadOps và StatusCheckFailed.<br>- Tạo IAM Role cho EC2 có quyền gửi metrics/logs cần thiết.<br>- Cài và cấu hình CloudWatch Agent trên EC2 để thu thập RAM, disk usage và log ứng dụng.<br>- Xác nhận custom metrics xuất hiện trong namespace CWAgent và log được đẩy vào đúng Log Group.<br>- Tạo Dashboard gồm biểu đồ CPU, RAM, network, disk và trạng thái EC2.<br>- Dùng Logs Insights chạy truy vấn đơn giản để lọc lỗi trong log ứng dụng. | 06/07/2026 | 06/07/2026 | [Tạo bảng theo dõi với Amazon CloudWatch](https://000008.awsstudygroup.com/vi/)<br>[CloudWatch Agent](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Install-CloudWatch-Agent.html) |
| Thứ Ba (Tại nhà) | **Cấu hình cảnh báo và thông báo tự động:**<br>- Tạo SNS Topic và đăng ký email nhận thông báo; xác nhận subscription trong hộp thư.<br>- Tạo Alarm cho EC2 CPUUtilization vượt ngưỡng trong nhiều chu kỳ liên tiếp.<br>- Tạo Alarm cho NetworkIn/NetworkOut hoặc StatusCheckFailed.<br>- Dùng metric `mem_used_percent` từ CloudWatch Agent để tạo cảnh báo RAM vì EC2 không gửi RAM metric mặc định.<br>- Gắn SNS action cho trạng thái ALARM và OK.<br>- Tạo tải kiểm thử ngắn để kích hoạt cảnh báo, kiểm tra email và theo dõi lịch sử chuyển trạng thái.<br>- Điều chỉnh threshold phù hợp để hạn chế cảnh báo giả. | 07/07/2026 | 07/07/2026 | [Amazon CloudWatch](https://000008.awsstudygroup.com/vi/)<br>[Metrics từ CloudWatch Agent](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/metrics-collected-by-CloudWatch-agent.html) |
| Thứ Tư (Tại nhà) | **Quản lý tên miền và định tuyến bằng Route 53:**<br>- Tìm hiểu DNS, Domain, Hosted Zone, TTL và cơ chế phân giải tên miền.<br>- Phân biệt Public Hosted Zone và Private Hosted Zone.<br>- Tìm hiểu các record A, AAAA, CNAME, Alias, MX, TXT và NS.<br>- Tạo Private Hosted Zone gắn với VPC thực hành hoặc sử dụng domain hiện có nếu có quyền quản lý.<br>- Tạo record trỏ tên dịch vụ đến EC2/Load Balancer và kiểm tra bằng `nslookup` hoặc `dig`.<br>- Tìm hiểu Alias Record, Routing Policy và Health Check cơ bản.<br>- Ghi chú chi phí Hosted Zone, truy vấn DNS và domain registration trước khi tạo tài nguyên công khai. | 08/07/2026 | 08/07/2026 | [Amazon Route 53](https://000010.awsstudygroup.com/vi/)<br>[Route 53 Developer Guide](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/Welcome.html) |
| Thứ Năm (Tại nhà) | **Thiết kế và mô phỏng Hybrid DNS:**<br>- Tìm hiểu Route 53 VPC Resolver, Inbound Endpoint, Outbound Endpoint và Resolver Rule.<br>- Vẽ luồng truy vấn từ DNS Local vào Private Hosted Zone thông qua Inbound Endpoint.<br>- Vẽ luồng truy vấn từ EC2 trong VPC đến DNS Local thông qua Outbound Endpoint và forwarding rule.<br>- Xác định yêu cầu kết nối mạng giữa Local và VPC bằng Site-to-Site VPN hoặc Direct Connect.<br>- Mô phỏng DNS Local bằng một EC2/BIND server hoặc hoàn thành cấu hình ở mức lab nếu ngân sách cho phép.<br>- Kiểm tra Security Group cho TCP/UDP 53 và các subnet đặt Resolver Endpoint.<br>- Không duy trì Resolver Endpoint sau bài thực hành vì endpoint tính phí theo giờ; lưu ảnh minh chứng rồi dọn tài nguyên. | 09/07/2026 | 09/07/2026 | [Thiết lập Hybrid DNS với Route 53](https://000010.awsstudygroup.com/vi/)<br>[Route 53 Resolver và Hybrid DNS](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver-overview-DSN-queries-to-vpc.html) |
| Thứ Sáu (Tại nhà) | **AWS CLI và tự động hóa bằng script:**<br>- Kiểm tra hoặc cài AWS CLI v2 trên EC2 Ubuntu/Windows; kiểm tra phiên bản và Region mặc định.<br>- Gắn IAM Role/Instance Profile cho EC2 thay vì cấu hình Access Key trực tiếp.<br>- Dùng `aws sts get-caller-identity` xác nhận principal hiện tại.<br>- Thực hành các lệnh mô tả EC2, liệt kê S3 bucket, upload/download và `aws s3 sync` thư mục website.<br>- Viết Bash hoặc PowerShell script có biến, tham số, kiểm tra exit code và log thời gian chạy.<br>- Tạo script backup file lên S3, kiểm tra trạng thái EC2 hoặc truy vấn CloudWatch Alarm.<br>- Áp dụng nguyên tắc idempotent để script có thể chạy lại an toàn.<br>- Lưu script vào Git, bổ sung README và tuyệt đối không commit credentials; ghi nhận cách tái sử dụng script trong pipeline CI/CD. | 10/07/2026 | 10/07/2026 | [AWS CLI trên EC2 Windows/Ubuntu](https://000011.awsstudygroup.com/vi/)<br>[Chạy script từ Amazon S3](https://docs.aws.amazon.com/systems-manager/latest/userguide/integration-s3.html) |
| Thứ Bảy | Nghỉ. | 11/07/2026 | 11/07/2026 | — |

### Thành tích đạt được tuần 5

**Amazon CloudWatch:**

- Thu thập được EC2 metrics, custom RAM/disk metrics và log ứng dụng bằng CloudWatch Agent.
- Xây dựng Dashboard trực quan để theo dõi CPU, RAM, network, disk và trạng thái máy chủ.
- Tạo CloudWatch Alarms kết hợp SNS để gửi email khi hệ thống vượt ngưỡng.
- Hiểu rằng RAM không phải metric EC2 mặc định và cần CloudWatch Agent.

**Amazon Route 53 và Hybrid DNS:**

- Hiểu Hosted Zone, DNS Record, TTL, Alias và các chính sách định tuyến cơ bản.
- Tạo và kiểm tra record DNS cho tài nguyên trong VPC.
- Hiểu vai trò của Route 53 Resolver inbound/outbound endpoints và forwarding rules.
- Thiết kế được luồng Hybrid DNS giữa Local và VPC, đồng thời nhận biết yêu cầu VPN/Direct Connect và chi phí endpoint.

**AWS CLI và tự động hóa:**

- Sử dụng AWS CLI trên EC2 bằng IAM Role thay cho Access Key dài hạn.
- Quản lý EC2, S3 và CloudWatch bằng dòng lệnh.
- Viết script tự động upload/sync file, kiểm tra tài nguyên và ghi log kết quả.
- Áp dụng kiểm tra lỗi, tính idempotent và quy tắc không lưu credentials trong repository.
- Xây dựng nền tảng kiến thức để đưa các script vào CI/CD ở giai đoạn sau.
