---
title: "Week 2 Worklog"
date: 2026-06-15
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

## WORKLOG TUẦN 2

### Mục tiêu

- Triển khai hạ tầng mạng với Amazon Virtual Private Cloud (Amazon VPC): nắm bắt các khái niệm nền tảng về mạng ảo, thiết lập môi trường mạng cô lập và an toàn trên AWS.
- Trực tiếp cấu hình không gian mạng VPC: tạo các mạng con (Subnets), thiết lập cổng kết nối Internet (Internet Gateway) và cấu hình bảng định tuyến (Route Tables) để điều hướng dữ liệu.
- Bắt đầu và triển khai ứng dụng trên dịch vụ máy chủ ảo Amazon Elastic Compute Cloud (Amazon EC2).
- Khởi tạo và vận hành máy chủ ảo (EC2 Instance): lựa chọn hệ điều hành (AMI) và cấu hình loại tài nguyên tính toán phù hợp với nhu cầu.
- Cấu hình tường lửa ảo (Security Group): thiết lập các quy tắc bảo mật để kiểm soát chặt chẽ luồng truy cập mạng vào và ra máy chủ.
- Thực hành kết nối từ xa vào máy chủ EC2 và triển khai ứng dụng chạy thực tế trên hạ tầng mạng VPC vừa xây dựng.

### Công việc thực hiện

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| Thứ Hai (Văn phòng) | **Tìm hiểu và triển khai Amazon VPC:**<br>- Tìm hiểu VPC, CIDR IPv4, Availability Zone và sự khác nhau giữa mạng Public/Private.<br>- Thiết kế sơ đồ mạng và xác định dải địa chỉ IP phù hợp.<br>- Tạo một VPC riêng cho môi trường thực hành.<br>- Tạo Public Subnet và Private Subnet trong các Availability Zone.<br>- Tạo Internet Gateway, gắn vào VPC.<br>- Tạo và cấu hình Route Table; thêm tuyến `0.0.0.0/0` từ Public Subnet đến Internet Gateway.<br>- Kiểm tra liên kết giữa Subnet, Route Table và Internet Gateway. | 15/06/2026 | 15/06/2026 | [Triển khai hạ tầng mạng với Amazon VPC](https://000003.awsstudygroup.com/vi/) |
| Thứ Ba (Văn phòng) | **Khởi tạo EC2 và triển khai ứng dụng:**<br>- Tìm hiểu thành phần của EC2: AMI, Instance Type, EBS, Key Pair và phương thức tính phí.<br>- Chọn AMI Linux và loại instance phù hợp cho môi trường thực hành.<br>- Tạo Security Group, chỉ mở cổng SSH 22 từ địa chỉ IP quản trị và cổng HTTP 80 cho người dùng truy cập.<br>- Khởi tạo EC2 Instance trong Public Subnet vừa xây dựng và bật Public IPv4.<br>- Kết nối từ xa vào EC2 bằng SSH với Key Pair.<br>- Cập nhật hệ thống, cài đặt web server và triển khai một trang web thử nghiệm.<br>- Truy cập ứng dụng qua Public IPv4 để xác nhận VPC, định tuyến và Security Group hoạt động đúng. | 16/06/2026 | 16/06/2026 | [Bắt đầu và triển khai ứng dụng trên Amazon EC2](https://000004.awsstudygroup.com/vi/) |
| Thứ Tư (Tại nhà) | **Ôn tập kiến trúc mạng:**<br>- Vẽ lại sơ đồ VPC đã triển khai, thể hiện CIDR, Subnets, Internet Gateway, Route Tables, Security Group và EC2.<br>- Ôn lại luồng dữ liệu khi người dùng truy cập ứng dụng trên EC2.<br>- So sánh vai trò của Public Subnet và Private Subnet; ghi chú những tài nguyên nên đặt trong từng loại mạng. | 17/06/2026 | 17/06/2026 | [Amazon VPC](https://000003.awsstudygroup.com/vi/) |
| Thứ Năm (Tại nhà) | **Kiểm tra và củng cố EC2:**<br>- Ôn lại vòng đời EC2 Instance: start, stop, reboot và terminate.<br>- Kiểm tra trạng thái instance, địa chỉ IP và các quy tắc Security Group.<br>- Thử truy cập ứng dụng và rà soát log web server để xác nhận máy chủ vận hành ổn định.<br>- Ghi chú nguyên tắc chỉ mở đúng cổng cần thiết và không cho phép SSH từ mọi địa chỉ IP. | 18/06/2026 | 18/06/2026 | [Amazon EC2](https://000004.awsstudygroup.com/vi/) |
| Thứ Sáu (Tại nhà) | **Tổng kết nhẹ cuối tuần:**<br>- Tổng hợp ảnh chụp và ghi chú các bước tạo VPC, Subnet, Internet Gateway, Route Table, EC2 và Security Group.<br>- Kiểm tra lại ứng dụng lần cuối.<br>- Stop EC2 Instance khi không sử dụng để hạn chế chi phí; rà soát AWS Budgets và tài nguyên đang hoạt động.<br>- Ghi lại các vấn đề gặp phải và nội dung cần hỏi mentor ở buổi tiếp theo. | 19/06/2026 | 19/06/2026 | [Khám phá dịch vụ AWS](https://cloudjourney.awsstudygroup.com/vi/1-explore/) |
| Thứ Bảy | Nghỉ. | 20/06/2026 | 20/06/2026 | — |

### Thành tích đạt được tuần 2

**Hạ tầng mạng Amazon VPC:**

- Hiểu các khái niệm VPC, CIDR, Availability Zone, Public Subnet và Private Subnet.
- Tạo được môi trường mạng VPC cô lập với dải địa chỉ IP được hoạch định rõ ràng.
- Tạo và liên kết Subnets, Internet Gateway và Route Tables để hình thành luồng truy cập Internet cho Public Subnet.
- Hiểu cách một gói tin đi từ Internet Gateway qua bảng định tuyến đến EC2 Instance.

**Máy chủ ảo Amazon EC2:**

- Hiểu vai trò của AMI, Instance Type, EBS, Key Pair và địa chỉ Public IPv4.
- Khởi tạo EC2 Instance trong đúng VPC và Public Subnet đã xây dựng.
- Cấu hình Security Group theo nguyên tắc chỉ mở các cổng cần thiết cho SSH và HTTP.
- Kết nối thành công đến máy chủ bằng SSH và thực hiện các lệnh quản trị cơ bản.
- Cài đặt web server, triển khai và truy cập được ứng dụng thử nghiệm trên EC2.

**Bảo mật, vận hành và quản lý chi phí:**

- Phân biệt được chức năng định tuyến của Route Table với chức năng tường lửa của Security Group.
- Biết kiểm tra trạng thái EC2, quy tắc mạng và log ứng dụng khi xử lý sự cố.
- Hình thành thói quen dừng tài nguyên khi không sử dụng và theo dõi AWS Budgets để hạn chế phát sinh chi phí.
- Hoàn thiện sơ đồ kiến trúc và tài liệu ghi lại toàn bộ quá trình thực hành.
