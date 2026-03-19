---
title : "Các bước chuẩn bị"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 4.2. </b> "
---

#### Thiết lập Môi trường

Trong phần này, bạn sẽ chuẩn bị môi trường workshop bằng cách tạo các tài nguyên AWS cần thiết sử dụng CloudFormation.

#### Tạo Thư mục Làm việc

Đầu tiên, tạo thư mục làm việc cho workshop:

```
cd ~
mkdir aws-waf-workshop
cd aws-waf-workshop
```

![Tạo thư mục làm việc](/images/5-Workshop/5.2-Prerequisite/diagram2.png)

#### Tạo CloudFormation Template

Tạo file CloudFormation template `waf-workshop.yaml` định nghĩa các tài nguyên AWS cần thiết:

```
nano waf-workshop.yaml
```

Template bao gồm các tài nguyên chính sau:
- **S3 Bucket**: Lưu trữ static website với public access
- **Lambda Function**: Xử lý logic dashboard
- **IAM Role**: Cấp quyền cho Lambda function

Sau khi tạo file, xác minh:

```
ls -lh
```

![File CloudFormation template đã tạo](/images/5-Workshop/5.2-Prerequisite/diagram3.png)

Xem nội dung template:

```
cat waf-workshop.yaml
```

![Nội dung CloudFormation template - phần 1](/images/5-Workshop/5.2-Prerequisite/diagram4.png)

![Nội dung CloudFormation template - phần 2](/images/5-Workshop/5.2-Prerequisite/diagram5.png)

#### Tạo Script Triển khai

Tạo script để tự động hóa triển khai CloudFormation stack:

```
nano deploy-workshop-own-account.sh
```

Script thực hiện các chức năng sau:
- Kiểm tra file template có tồn tại không
- Tạo CloudFormation stack với IAM capabilities
- Chờ stack creation hoàn thành
- Hiển thị stack outputs khi thành công

Cấp quyền thực thi cho script:

```
chmod +x deploy-workshop-own-account.sh
```

Xác minh các files:

```
ls -lh
```

![Thư mục làm việc với các files](/images/5-Workshop/5.2-Prerequisite/diagram6.png)

#### Triển khai CloudFormation Stack

Chạy script triển khai:

```
./deploy-workshop-own-account.sh
```

![Bắt đầu thực thi script](/images/5-Workshop/5.2-Prerequisite/diagram7.png)

![Chờ stack creation](/images/5-Workshop/5.2-Prerequisite/diagram8.png)

#### Xử lý Lỗi Triển khai

Nếu stack creation thất bại:

![Stack creation thất bại](/images/5-Workshop/5.2-Prerequisite/diagram9.png)

Kiểm tra chi tiết lỗi:

```
aws cloudformation describe-stack-events \
 --stack-name waf-workshop \
 --region ap-southeast-1 \
 --max-items 20 \
 --query 'StackEvents[?ResourceStatus==CREATE_FAILED].[LogicalResourceId,ResourceStatusReason]' \
 --output table
```

![Chi tiết lỗi CloudFormation](/images/5-Workshop/5.2-Prerequisite/diagram10.png)

**Giải quyết lỗi:**
WAF Web ACL với CLOUDFRONT scope chỉ có thể được tạo ở region us-east-1. Xóa stack thất bại và sửa template.

Xóa stack thất bại:

```
aws cloudformation delete-stack \
 --stack-name waf-workshop \
 --region ap-southeast-1

aws cloudformation wait stack-delete-complete \
 --stack-name waf-workshop \
 --region ap-southeast-1
```

Chỉnh sửa template:

```
nano waf-workshop.yaml
```

![Chỉnh sửa template - phần 1](/images/5-Workshop/5.2-Prerequisite/diagram11.png)

![Chỉnh sửa template - phần 2](/images/5-Workshop/5.2-Prerequisite/diagram12.png)


#### Triển khai Thành công

Sau khi sửa template, chạy lại script triển khai:

```
./deploy-workshop-own-account.sh
```

![Stack tạo thành công](/images/5-Workshop/5.2-Prerequisite/diagram13.png)

Stack outputs bao gồm:
- **WebsiteURL**: URL static website S3
- **S3BucketName**: Tên S3 bucket đã tạo
- **LambdaFunctionName**: Tên Lambda function

#### Xác minh trên AWS Console

Kiểm tra CloudFormation Console:

![CloudFormation Console](/images/5-Workshop/5.2-Prerequisite/diagram14.png)

![Stack Outputs trên Console](/images/5-Workshop/5.2-Prerequisite/diagram15.png)

Truy cập URL website S3:

![URL Website S3](/images/5-Workshop/5.2-Prerequisite/diagram16.png)

#### Kiến trúc Workshop

Kiến trúc workshop bao gồm các thành phần sau:

![Kiến trúc Workshop](/images/5-Workshop/5.2-Prerequisite/diagram17.png)

**Các Thành phần Chính:**
- **Amazon CloudFront**: Phân phối nội dung toàn cầu với tích hợp WAF
- **AWS WAF Web ACL**: Tường lửa ứng dụng web (sẽ được cấu hình)
- **Amazon S3**: Lưu trữ static website
- **AWS Lambda**: Hàm xử lý dashboard
- **Amazon CloudWatch**: Giám sát và ghi log

#### Tạo WAF Web ACL

Tạo WAF Web ACL ở region us-east-1 (bắt buộc cho CloudFront scope):

![Tạo WAF Web ACL](/images/5-Workshop/5.2-Prerequisite/diagram18.png)

#### Tạo CloudFront Distribution

Tạo CloudFront distribution tích hợp với WAF Web ACL:

![Tạo CloudFront Distribution](/images/5-Workshop/5.2-Prerequisite/diagram19.png)

Chờ distribution triển khai:

![Chờ CloudFront triển khai](/images/5-Workshop/5.2-Prerequisite/diagram20.png)

#### Xác minh Triển khai

Kiểm tra CloudFront Distribution trên Console:

![CloudFront Console](/images/5-Workshop/5.2-Prerequisite/diagram21.png)

Kiểm tra WAF Web ACL trên Console:

![WAF Console](/images/5-Workshop/5.2-Prerequisite/diagram22.png)

Truy cập CloudFront domain:

![CloudFront domain response](/images/5-Workshop/5.2-Prerequisite/diagram23.png)

Kiểm tra CloudFormation Stack Outputs:

![CloudFormation Stack Outputs](/images/5-Workshop/5.2-Prerequisite/diagram24.png)

#### Đánh giá Bảo mật Ban đầu

Kiểm tra trạng thái WAF Web ACL hiện tại:

```
aws wafv2 get-web-acl \
 --id <WEB_ACL_ID> \
 --name waf-workshop-webacl \
 --scope CLOUDFRONT \
 --region us-east-1
```

![Trạng thái WAF Web ACL](/images/5-Workshop/5.2-Prerequisite/diagram25.png)

Trạng thái hiện tại:
- **DefaultAction**: Allow (cho phép tất cả traffic)
- **Rules**: [] (chưa có rules nào được cấu hình)
- **Capacity**: 0 (chưa sử dụng capacity)

#### Tạo Scripts Kiểm thử Bảo mật

Tạo script kiểm thử bảo mật baseline:

```
nano test-security-baseline.sh
chmod +x test-security-baseline.sh
./test-security-baseline.sh
```

![Kết quả Kiểm thử Baseline](/images/5-Workshop/5.2-Prerequisite/diagram26.png)

**Kết quả Kiểm thử Baseline:**
- Legitimate Traffic: Tất cả requests trả về 403 Forbidden
- Attack Simulation: Hầu hết attacks trả về 403 Forbidden
- Chưa có WAF rules chặn attacks

#### Phân tích Chi tiết Attack Vector

Tạo script kiểm thử tấn công chi tiết:

```
nano detailed-attack-test.sh
chmod +x detailed-attack-test.sh
./detailed-attack-test.sh
```

![Kiểm thử Tấn công Chi tiết](/images/5-Workshop/5.2-Prerequisite/diagram27.png)

**Kết quả Tấn công Chi tiết:**

1. **XSS trong request body**: 403 Forbidden - POST request với script payload
2. **XSS trong request path**: 403 Forbidden - Script injection trong URL path
3. **SQL Injection trong query**: 000 (Connection failed) - Union-based SQL injection
4. **SQL Injection trong cookie**: 403 Forbidden - Cookie-based SQL injection
5. **Path Traversal**: 403 Forbidden - Directory traversal với ../../../
6. **Server-side Assets**: 403 Forbidden - Truy cập file .env
7. **Common Bot**: 403 Forbidden - Mô phỏng BadBot User-Agent
8. **API Misuse**: 403 Forbidden - JSON payload với script injection
9. **Directory Traversal**: 403 Forbidden - Includes directory traversal
10. **Mystery Test**: 403 Forbidden - Kết hợp X-Forwarded-For và path traversal

#### Giám sát CloudWatch Metrics

Kiểm tra CloudWatch metrics để xác minh hành vi WAF và các mẫu traffic:

![CloudWatch Metrics](/images/5-Workshop/5.2-Prerequisite/diagram28.png)

**Phân tích Metrics:**
- **AllowedRequests**: Traffic đi qua WAF (tất cả được cho phép)
- **BlockedRequests**: 0 (chưa có requests nào bị chặn bởi WAF rules)
- **SampledRequests**: Có sẵn cho debugging và phân tích
- **Metric Name**: "waf-workshop-webacl" đã cấu hình đúng

#### Đánh giá Bảo mật Hiện tại

**Điểm Tích cực:**
- WAF Web ACL đã tạo thành công và tích hợp với CloudFront
- CloudWatch monitoring đã bật với cấu hình visibility đầy đủ
- Sampled requests đã bật cho debugging và phân tích forensic
- Nền tảng hạ tầng sẵn sàng cho triển khai security rules

**Các Điểm Cần Cải thiện:**
- Chưa có WAF rules nào được cấu hình (Rules array trống)
- Ứng dụng chưa có nội dung cho kiểm thử toàn diện
- Cần upload nội dung lên S3 bucket cho kiểm thử baseline chính xác
- Môi trường kiểm thử chưa hoàn chỉnh để xác minh hiệu quả WAF

**Phân tích Nguyên nhân Gốc:**
- **403 Forbidden responses**: CloudFront origin (S3) chưa có nội dung, không phải do WAF chặn
- **000 Connection failed**: Network timeout với attack payload cụ thể
- **WAF không chặn**: Chưa có rules nào được cấu hình

#### Phân tích và Lập kế hoạch Khắc phục

**Trạng thái Bảo mật Hiện tại:**

Dựa trên kết quả kiểm thử bảo mật toàn diện:

**Phân tích Kết quả Kiểm thử:**
- **Trạng thái WAF**: Web ACL đã tạo nhưng chưa cấu hình rules (Rules: [])
- **Trạng thái Ứng dụng**: CloudFront trả về 403 Forbidden do S3 origin trống
- **Tư thế Bảo mật**: Không thể đánh giá đầy đủ do thiếu nội dung cho kiểm thử

**Phân tích Nguyên nhân Gốc:**
- 403 Forbidden responses: Hạ tầng chưa hoàn chỉnh, không phải security blocking
- Hạn chế kiểm thử: Không thể xác minh hiệu quả WAF với setup hiện tại
- Thành phần thiếu: Nội dung S3, application endpoints phù hợp

#### Chuẩn bị Khắc phục

Dựa trên phân tích, cần tiếp cận 2 giai đoạn:

**Giai đoạn 1 - Hoàn thiện Hạ tầng:**
- Upload nội dung lên S3 bucket cho ứng dụng hoạt động
- Xác minh CloudFront phục vụ nội dung đúng cách (200 OK responses)
- Thiết lập baseline kiểm thử phù hợp

**Giai đoạn 2 - Triển khai Bảo mật:**
- Cấu hình AWS Managed Rules (Core Rule Set, SQL Database)
- Thiết lập custom rules cho bảo vệ cụ thể
- Triển khai rate limiting và bot control
- Fine-tuning để tránh false positives

Giai đoạn tiếp theo sẽ tập trung vào hoàn thiện thiết lập hạ tầng trước khi triển khai các biện pháp bảo mật, đảm bảo môi trường kiểm thử phù hợp để xác minh hiệu quả WAF.
