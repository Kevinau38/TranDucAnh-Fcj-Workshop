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
| 5   | - **Practice:** RDS database setup: <br>   + Create RDS instance with MySQL/PostgreSQL. <br>   + Configure security groups for database access. <br>   + Connect to database via client tools. <br>   + Perform basic CRUD operations.                                 | 22/01/2026 | 22/01/2026      | <https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_SettingUp.html> |
| 6   | - **Hands-on Project:** Build file upload system: <br>   + Create web application with file upload functionality. <br>   + Connect to RDS instance. <br>   + Integrate S3 buckets for file storage. <br>   + Store file metadata in RDS database. <br>   + Implement secure file upload with presigned URLs. <br>   + Test complete end-to-end system functionality.                                  | 23/01/2026 | 23/01/2026      | <http://13.213.9.23/upload.php> |


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
  * Created RDS instance with MySQL/PostgreSQL engine.
  * Configured database security groups and access controls.
  * Established database connections and performed CRUD operations.
  * Learned RDS backup and maintenance best practices.

* **Built comprehensive file upload system:**
  * Developed web application with file upload functionality.
  * Integrated S3 for scalable file storage.
  * Used RDS for storing file metadata and user information.
  * Implemented secure file upload with presigned URLs.
  * Created end-to-end system connecting storage and database services.

* **Developed advanced AWS storage and database skills** including data lifecycle management, backup strategies, and service integration patterns.
