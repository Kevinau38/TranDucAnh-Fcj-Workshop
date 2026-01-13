---
title: "Worklog Tuần 2"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---
### Mục tiêu tuần 2:

* Học dịch vụ AWS S3 storage và các khái niệm.
* Nắm rõ S3 buckets và lifecycle policies.
* Thực hành EBS volumes và snapshots.
* Thiết lập và quản lý RDS instances.
* Hiểu về kết nối database và các thao tác.
* Thực hành: Xây dựng hệ thống upload file.

### Các công việc cần triển khai trong tuần này:
| Ngày | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Học cơ bản và khái niệm S3. <br> - Tạo S3 buckets và cấu hình quyền. <br> - Upload/download files và quản lý cấu trúc thư mục.                                                                      | 19/01/2026   | 19/01/2026      | <https://docs.aws.amazon.com/s3/latest/userguide/Welcome.html> <br> <https://docs.aws.amazon.com/s3/latest/userguide/creating-bucket.html>           |
| 3   | - Cấu hình S3 lifecycle policies. <br> - Thiết lập versioning và encryption. <br> - Kích hoạt static website hosting. <br> - Học về các storage classes.                                               | 20/01/2026   | 20/01/2026      | <https://docs.aws.amazon.com/s3/latest/userguide/object-lifecycle-mgmt.html> <br> <https://docs.aws.amazon.com/s3/latest/userguide/WebsiteHosting.html> <br> <https://docs.aws.amazon.com/s3/latest/userguide/storage-class-intro.html> |
| 4   | - Học các loại EBS volume và khái niệm. <br> - Gắn/tháo EBS volumes vào EC2. <br> - Tạo EBS snapshots. <br> - Thực hành mã hóa và thay đổi kích thước volume.                                                    | 21/01/2026   | 21/01/2026      | <https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AmazonEBS.html> <br> <https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSSnapshots.html> |
| 5   | - **Thực hành:** Thiết lập và quản lý RDS. <br> - Tạo RDS instance với MySQL/PostgreSQL. <br> - Cấu hình security groups cho database access. <br> - Kết nối database và thực hiện các thao tác cơ bản.                                 | 22/01/2026   | 22/01/2026      | <https://docs.aws.amazon.com/rds/latest/userguide/CHAP_GettingStarted.html> <br> <https://docs.aws.amazon.com/rds/latest/userguide/Overview.DBInstance.html> |
| 6   | - **Dự án thực hành:** Xây dựng hệ thống upload file. <br> - Tạo ứng dụng web với chức năng upload file. <br> - Tích hợp S3 cho việc lưu trữ file. <br> - Sử dụng RDS cho việc lưu trữ metadata. <br> - Triển khai hệ thống hoàn chỉnh end-to-end.                                  | 23/01/2026   | 23/01/2026      | <https://docs.aws.amazon.com/sdk-for-javascript/> <br> <https://docs.aws.amazon.com/s3/latest/userguide/PresignedUrlUploadObject.html> |


### Kết quả đạt được tuần 2:

* **Nắm rõ dịch vụ AWS S3 storage:**
  * Tạo và cấu hình S3 buckets với quyền phù hợp.
  * Triển khai lifecycle policies để tối ưu hóa chi phí.
  * Thiết lập versioning và encryption để bảo vệ dữ liệu.
  * Triển khai static website hosting trên S3.
  * Hiểu các storage classes khác nhau và cách sử dụng.

* **Tích lũy chuyên môn quản lý EBS volume:**
  * Học các loại EBS volume khác nhau (gp3, io2, v.v.).
  * Thành công trong việc gắn và tháo volumes vào EC2 instances.
  * Tạo và quản lý EBS snapshots cho backup.
  * Triển khai mã hóa volume và các thao tác thay đổi kích thước.

* **Triển khai và quản lý RDS database thành công:**
  * Tạo RDS instance với MySQL/PostgreSQL engine.
  * Cấu hình database security groups và kiểm soát truy cập.
  * Thiết lập kết nối database và thực hiện các thao tác CRUD.
  * Học các thực hành tốt nhất về RDS backup và bảo trì.

* **Xây dựng hệ thống upload file toàn diện:**
  * Phát triển ứng dụng web với chức năng upload file.
  * Tích hợp S3 cho việc lưu trữ file có thể mở rộng.
  * Sử dụng RDS để lưu trữ metadata file và thông tin người dùng.
  * Triển khai upload file bảo mật với presigned URLs.
  * Tạo hệ thống end-to-end kết nối các dịch vụ storage và database.

* **Phát triển kỹ năng AWS storage và database nâng cao** bao gồm quản lý lifecycle dữ liệu, chiến lược backup, và các mẫu tích hợp dịch vụ.
