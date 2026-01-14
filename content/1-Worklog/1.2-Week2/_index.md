---
title: "Week 2 Worklog"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---
### Week 2 Objectives:

* Learn AWS S3 storage service and concepts.
* Understand S3 buckets and lifecycle policies.
* Practice EBS volumes and snapshots.
* Set up and manage RDS instances.
* Understand database connectivity and operations.
* Hands-on: Build file upload system.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Learn S3 fundamentals and concepts. <br> - Create S3 buckets and configure permissions. <br> - Upload/download files and manage folder structure.                                                      | 19/01/2026 | 19/01/2026      | <https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html> <br> <https://docs.aws.amazon.com/AmazonS3/latest/userguide/creating-buckets-s3.html> <br> <https://docs.aws.amazon.com/AmazonS3/latest/userguide/upload-objects.html>           |
| 3   | - Configure S3 lifecycle policies. <br> - Set up versioning and encryption. <br> - Enable static website hosting. <br> - Learn about storage classes.                                               | 20/01/2026 | 20/01/2026      | <https://docs.aws.amazon.com/AmazonS3/latest/userguide/how-to-set-lifecycle-configuration-intro.html> <br> <https://docs.aws.amazon.com/AmazonS3/latest/userguide/manage-versioning-examples.html> <br> <https://docs.aws.amazon.com/AmazonS3/latest/userguide/EnableWebsiteHosting.html> <br> <https://docs.aws.amazon.com/AmazonS3/latest/userguide/storage-class-intro.html> |
| 4   | - Learn EBS volume types and concepts. <br> - Attach/detach EBS volumes to EC2. <br> - Create EBS snapshots. <br> - Practice volume encryption and resizing.                                                    | 21/01/2026 | 21/01/2026      | <https://docs.aws.amazon.com/ebs/latest/userguide/ebs-volume-types.html> <br> <https://docs.aws.amazon.com/ebs/latest/userguide/ebs-detaching-volume.html> <br> <https://docs.aws.amazon.com/ebs/latest/userguide/ebs-creating-snapshot.html> <br> <https://docs.aws.amazon.com/ebs/latest/userguide/ebs-encryption.html> |
| 5   | - **Practice:** RDS database setup: <br>   + Create RDS instance with MySQL 8.0 (db.t3.micro, Free Tier). <br>   + Configure security groups for database access. <br>   + Install database client (MariaDB/MySQL). <br>   + Connect to RDS instance via client tools. <br>   + Create database schema and tables. <br>   + Perform basic CRUD operations.                                 | 22/01/2026 | 22/01/2026      | <https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_SettingUp.html> |
| 6   | - **Hands-on Project:** Build file upload system: <br>   + Install and configure PHP with required modules. <br>   + Configure IAM role for EC2-S3 access. <br>   + Set up S3 CORS policy for web uploads. <br>   + Connect to RDS instance. <br>   + Create database schema for file metadata. <br>   + Develop upload form and handler. <br>   + Integrate S3 buckets for file storage. <br>   + Store file metadata in RDS database. <br>   + Create file listing page. <br>   + Test complete end-to-end system functionality.                                  | 23/01/2026 | 23/01/2026      | <http://18.139.227.186/upload.php> |


### Week 2 Achievements:

* **Understood AWS S3 storage service:**
  * Created and configured S3 buckets with proper permissions.
  * Implemented lifecycle policies for cost optimization.
  * Set up versioning and encryption for data protection.
  * Deployed static website hosting on S3.
  * Understood different storage classes and their use cases.

* **Gained expertise in EBS volume management:**
  * Learned different EBS volume types (gp3, io2, etc.).
  * Successfully attached and detached volumes to EC2 instances.
  * Created and managed EBS snapshots for backup.
  * Implemented volume encryption and resizing operations.

* **Successfully deployed and managed RDS database:**
  * Created RDS instance with MySQL 8.0.43 engine (db.t3.micro, Free Tier).
  * Configured database security groups for EC2 access (port 3306).
  * Installed MariaDB client for MySQL compatibility.
  * Established database connections and performed CRUD operations.
  * Created database schema with files table (7 columns for metadata).
  * Learned RDS backup and maintenance best practices.

* **Built comprehensive file upload system:**
  * Installed and configured PHP 8.4 with mysqli, json, and pdo modules.
  * Created IAM role (CloudClub-EC2-S3-Role) with S3FullAccess policy.
  * Configured S3 bucket (cloudclub-fileupload-storage-2026) in ap-southeast-1.
  * Set up S3 CORS policy for web uploads (GET, PUT, POST, DELETE).
  * Developed web application with upload form (upload.php).
  * Implemented upload handler with file validation and S3 integration.
  * Created file listing page displaying recent uploads from database.
  * Integrated S3 for scalable file storage with metadata in RDS.
  * Successfully tested end-to-end upload with Excel file (27KB).
  * Deployed complete system.

* **Developed foundational AWS storage and database skills** including data lifecycle management, backup strategies, and service integration patterns.
