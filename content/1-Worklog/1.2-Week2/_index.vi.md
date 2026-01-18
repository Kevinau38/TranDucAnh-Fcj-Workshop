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
| 2   | - Học cơ bản và khái niệm S3. <br> - Tạo S3 buckets và cấu hình quyền. <br> - Upload/download files và quản lý cấu trúc thư mục.                                                                      | 19/01/2026   | 19/01/2026      | <https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html> <br> <https://docs.aws.amazon.com/AmazonS3/latest/userguide/creating-buckets-s3.html> <br> <https://docs.aws.amazon.com/AmazonS3/latest/userguide/upload-objects.html>           |
| 3   | - Cấu hình S3 lifecycle policies. <br> - Thiết lập versioning và encryption. <br> - Kích hoạt static website hosting. <br> - Học về các storage classes.                                               | 20/01/2026   | 20/01/2026      | <https://docs.aws.amazon.com/AmazonS3/latest/userguide/how-to-set-lifecycle-configuration-intro.html> <br> <https://docs.aws.amazon.com/AmazonS3/latest/userguide/manage-versioning-examples.html> <br> <https://docs.aws.amazon.com/AmazonS3/latest/userguide/EnableWebsiteHosting.html> <br> <https://docs.aws.amazon.com/AmazonS3/latest/userguide/storage-class-intro.html> |
| 4   | - Học các loại EBS volume và khái niệm. <br> - Gắn/tháo EBS volumes vào EC2. <br> - Tạo EBS snapshots. <br> - Thực hành mã hóa và thay đổi kích thước volume.                                                    | 21/01/2026   | 21/01/2026      | <https://docs.aws.amazon.com/ebs/latest/userguide/ebs-volume-types.html> <br> <https://docs.aws.amazon.com/ebs/latest/userguide/ebs-detaching-volume.html> <br> <https://docs.aws.amazon.com/ebs/latest/userguide/ebs-creating-snapshot.html> <br> <https://docs.aws.amazon.com/ebs/latest/userguide/ebs-encryption.html> |
| 5   | - **Thực hành:** Thiết lập RDS database: <br>   + Tạo RDS instance với MySQL 8.0 (db.t3.micro, Free Tier). <br>   + Cấu hình security groups cho database access. <br>   + Cài đặt database client (MariaDB/MySQL). <br>   + Kết nối đến RDS instance qua client tools. <br>   + Tạo database schema và tables. <br>   + Thực hiện các thao tác CRUD cơ bản.                                 | 22/01/2026   | 22/01/2026      | <https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_SettingUp.html> |
| 6   | - **Dự án thực hành:** Xây dựng hệ thống upload file: <br>   + Cài đặt và cấu hình PHP với các modules cần thiết. <br>   + Cấu hình IAM role cho EC2-S3 access. <br>   + Thiết lập S3 CORS policy cho web uploads. <br>   + Kết nối đến RDS instance. <br>   + Tạo database schema cho file metadata. <br>   + Phát triển upload form và handler. <br>   + Tích hợp S3 buckets cho việc lưu trữ file. <br>   + Lưu trữ metadata file trong RDS database. <br>   + Tạo trang hiển thị danh sách files. <br>   + Test chức năng hệ thống end-to-end hoàn chỉnh.                                  | 23/01/2026   | 23/01/2026      | <http://13.213.1.132/upload.php> |


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
  * Tạo RDS instance với MySQL 8.0.43 engine (db.t3.micro, Free Tier).
  * Cấu hình database security groups cho EC2 access (port 3306).
  * Cài đặt MariaDB client để tương thích với MySQL.
  * Thiết lập kết nối database và thực hiện các thao tác CRUD.
  * Tạo database schema với bảng files (7 cột cho metadata).
  * Học các thực hành tốt nhất về RDS backup và bảo trì.

* **Xây dựng hệ thống upload file toàn diện:**
  * Cài đặt và cấu hình PHP 8.4 với các modules mysqli, json, và pdo.
  * Tạo IAM role (CloudClub-EC2-S3-Role) với S3FullAccess policy.
  * Cấu hình S3 bucket (cloudclub-fileupload-storage-2026) ở ap-southeast-1.
  * Thiết lập S3 CORS policy cho web uploads (GET, PUT, POST, DELETE).
  * Phát triển ứng dụng web với upload form (upload.php).
  * Triển khai upload handler với kiểm tra file và tích hợp S3.
  * Tạo trang hiển thị danh sách files từ database.
  * Tích hợp S3 cho việc lưu trữ file có thể mở rộng với metadata trong RDS.
  * Test thành công end-to-end upload với file Excel (27KB).
  * Triển khai hệ thống hoàn chỉnh.

* **Phát triển kỹ năng AWS storage và database nền tảng** bao gồm quản lý lifecycle dữ liệu, chiến lược backup, và các mẫu tích hợp dịch vụ.
