---
title : "Dọn dẹp tài nguyên"
date : 2024-01-01
weight : 4
chapter : false
pre : " <b> 4.4. </b> "
---

Xin chúc mừng bạn đã hoàn thành workshop này!

Trong workshop này, bạn đã học các mẫu triển khai bảo mật AWS WAF toàn diện để bảo vệ ứng dụng web khỏi các mối đe dọa khác nhau.

+ Bằng cách triển khai AWS Managed Rules, bạn đã bảo vệ chống lại các lỗ hổng OWASP Top 10 bao gồm SQL injection và tấn công XSS.
+ Bằng cách tạo custom rules, bạn đã bảo mật các đường dẫn ứng dụng cụ thể và triển khai kiểm soát truy cập chi tiết.
+ Bằng cách cấu hình Bot Control, bạn đã xác định và quản lý bot traffic trong khi duy trì truy cập bot hợp lệ.
+ Bằng cách triển khai rate limiting, bạn đã ngăn chặn traffic spikes và cạn kiệt tài nguyên.
+ Bằng cách validate API parameters, bạn đã thực thi business logic constraints tại lớp WAF.

#### Dọn dẹp

1. Điều hướng đến AWS WAF console ở region us-east-1. Vào Web ACLs và chọn "waf-workshop-webacl". Vào tab "Associated AWS resources", chọn CloudFront distribution, và click "Remove" để hủy liên kết.

![hủy liên kết cloudfront bước 1](/images/5-Workshop/5.6-Cleanup/diagram96.png)

![hủy liên kết cloudfront bước 2](/images/5-Workshop/5.6-Cleanup/diagram97.png)

2. Sau khi hủy liên kết, chọn "waf-workshop-webacl" từ danh sách Web ACLs và click "Delete". Gõ "delete" để xác nhận và click "Delete".

![xóa webacl bước 1](/images/5-Workshop/5.6-Cleanup/diagram98.png)

![xóa webacl bước 2](/images/5-Workshop/5.6-Cleanup/diagram99.png)

3. Điều hướng đến "Regex pattern sets" trong AWS WAF console. Xóa các pattern sets sau:
+ static-content
+ number-1-to-100

![xóa regex bước 1](/images/5-Workshop/5.6-Cleanup/diagram100.png)

![xóa regex bước 2](/images/5-Workshop/5.6-Cleanup/diagram101.png)

![xóa regex bước 3](/images/5-Workshop/5.6-Cleanup/diagram102.png)

![xóa regex bước 4](/images/5-Workshop/5.6-Cleanup/diagram103.png)

4. Điều hướng đến CloudFront console. Chọn distribution của bạn, click "Disable", chờ status chuyển sang "Disabled" (5-10 phút), sau đó chọn lại và click "Delete".

![xóa cloudfront bước 1](/images/5-Workshop/5.6-Cleanup/diagram104.png)

![xóa cloudfront bước 2](/images/5-Workshop/5.6-Cleanup/diagram105.png)

![xóa cloudfront bước 3](/images/5-Workshop/5.6-Cleanup/diagram106.png)

![xóa cloudfront bước 4](/images/5-Workshop/5.6-Cleanup/diagram107.png)

5. Điều hướng đến S3 console ở region ap-southeast-1. Chọn bucket "waf-workshop-280646578066", click "Empty" và xác nhận. Sau khi làm trống, click "Delete" và gõ tên bucket để xác nhận.

![xóa s3 bước 1](/images/5-Workshop/5.6-Cleanup/diagram108.png)

![xóa s3 bước 2](/images/5-Workshop/5.6-Cleanup/diagram109.png)

![xóa s3 bước 3](/images/5-Workshop/5.6-Cleanup/diagram110.png)

![xóa s3 bước 4](/images/5-Workshop/5.6-Cleanup/diagram111.png)

6. Điều hướng đến Lambda console ở region ap-southeast-1. Chọn function "waf-workshop-dashboard", click "Actions" → "Delete" và xác nhận.

![xóa lambda bước 1](/images/5-Workshop/5.6-Cleanup/diagram112.png)

![xóa lambda bước 2](/images/5-Workshop/5.6-Cleanup/diagram113.png)

7. Điều hướng đến IAM console. Vào "Roles", tìm kiếm "waf-workshop", chọn Lambda execution role, và click "Delete".

![xóa iam bước 1](/images/5-Workshop/5.6-Cleanup/diagram114.png)

![xóa iam bước 2](/images/5-Workshop/5.6-Cleanup/diagram115.png)

![xóa iam bước 3](/images/5-Workshop/5.6-Cleanup/diagram116.png)

8. (Tùy chọn) Nếu bạn sử dụng CloudFormation, điều hướng đến CloudFormation console ở region ap-southeast-1 và xóa stack "waf-workshop".

![xóa stack bước 1](/images/5-Workshop/5.6-Cleanup/diagram117.png)

![xóa stack bước 2](/images/5-Workshop/5.6-Cleanup/diagram118.png)
