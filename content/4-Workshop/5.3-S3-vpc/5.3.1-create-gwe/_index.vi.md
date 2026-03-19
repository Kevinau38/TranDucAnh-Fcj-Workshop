---
title : "Hoàn thiện Hạ tầng & Managed Rules"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 4.3.1. </b> "
---

#### Tổng quan

Phần này triển khai phương pháp 2 giai đoạn để hoàn thiện hạ tầng và triển khai bảo vệ bảo mật cơ bản sử dụng AWS Managed Rules.

**Giai đoạn 1**: Hoàn thiện Hạ tầng - Upload nội dung lên S3 cho kiểm thử chức năng
**Giai đoạn 2**: Triển khai Bảo mật - Deploy AWS Managed Rules cho bảo vệ OWASP Top 10

---

### Giai đoạn 1: Hoàn thiện Hạ tầng

#### Tạo Nội dung cho S3 Bucket

Để có môi trường kiểm thử thực tế, tạo các trang HTML mô phỏng ứng dụng web thực:

```
nano index.html
nano search.html
nano login.html
```

![Tạo các file HTML](/images/5-Workshop/5.3-S3-vpc/diagram29.png)

Nội dung bao gồm:
- **index.html**: Trang chính với navigation và test forms
- **search.html**: Chức năng tìm kiếm để kiểm thử XSS và SQL injection
- **login.html**: Form đăng nhập để kiểm thử tấn công authentication
- **Vulnerable components**: Forms và inputs để mô phỏng attack vectors

#### Upload Nội dung lên S3 Bucket

Upload các file đã tạo lên S3 bucket đã cấu hình:

```
aws s3 cp index.html s3://waf-workshop-280646578066/
aws s3 cp search.html s3://waf-workshop-280646578066/
aws s3 cp login.html s3://waf-workshop-280646578066/
```

![Upload files lên S3](/images/5-Workshop/5.3-S3-vpc/diagram30.png)

Kết quả upload:
- **index.html**: 2077 bytes - Trang ứng dụng chính
- **search.html**: 342 bytes - Trang chức năng tìm kiếm
- **login.html**: 356 bytes - Trang authentication

#### Xác minh Nội dung S3

Kiểm tra các files đã upload thành công:

```
aws s3 ls s3://waf-workshop-280646578066/
```

![Danh sách S3 bucket](/images/5-Workshop/5.3-S3-vpc/diagram31.png)

S3 bucket hiện chứa:
- 3 file HTML với timestamps
- Kích thước file khớp với file local
- S3 static website hosting đã cấu hình từ CloudFormation

#### Kiểm thử CloudFront với Nội dung Mới

Xác minh CloudFront distribution có thể phục vụ nội dung từ S3 origin:

```
curl -I https://d1aty6dsjre298.cloudfront.net/
curl -I https://d1aty6dsjre298.cloudfront.net/search.html
curl -I https://d1aty6dsjre298.cloudfront.net/login.html
```

![CloudFront phục vụ nội dung](/images/5-Workshop/5.3-S3-vpc/diagram32.png)

**Đột phá Đạt được:**
- **HTTP/2 200 OK**: Thay vì 403 Forbidden
- **Content-Type**: text/html được phục vụ đúng
- **CloudFront caching**: "Miss from cloudfront" cho request đầu tiên
- **S3 integration**: CloudFront lấy nội dung thành công từ S3 origin

**Trạng thái Hạ tầng:**
- ✅ S3 bucket: Nội dung đã upload và có thể truy cập
- ✅ CloudFront: Distribution phục vụ nội dung đúng cách
- ✅ WAF integration: Web ACL đã gắn, sẵn sàng cho rules
- ✅ Môi trường kiểm thử: Application endpoints hoạt động

---

### Giai đoạn 1 Hoàn thành: Kiểm thử Baseline với Nội dung Thực

#### Kiểm thử lại Security Baseline

Sau khi hoàn thiện hạ tầng với nội dung thực, thực hiện kiểm thử bảo mật lại:

```
./test-security-baseline.sh
```

![Kiểm thử baseline với nội dung](/images/5-Workshop/5.3-S3-vpc/diagram33.png)

**Kết quả Legitimate Traffic:**
- GET request: 200 OK ✓ - Ứng dụng phục vụ nội dung thành công
- POST with valid data: 403 Forbidden - CloudFront chặn POST requests
- API request: 403 Forbidden - Chưa cấu hình API endpoint
- Static file access: 403 Forbidden - File không tồn tại

**Kết quả Attack Simulation:**
- SQL Injection (query): 000 (Connection failed)
- SQL Injection (cookie): 200 OK - **DỄ BỊ TẤN CÔNG!**
- XSS (request body): 403 Forbidden - CloudFront chặn
- XSS (URL path): 403 Forbidden - CloudFront chặn
- XSS (query string): 200 OK - **DỄ BỊ TẤN CÔNG!**
- Path Traversal: 403 Forbidden - CloudFront chặn
- Server-side assets: 403 Forbidden - CloudFront chặn
- Bot activity: 200 OK - **DỄ BỊ TẤN CÔNG!**
- API misuse: 403 Forbidden - CloudFront chặn
- Mystery test: 200 OK - **DỄ BỊ TẤN CÔNG!**

#### Phân tích Chi tiết Attack Vector

Thực hiện kiểm thử chi tiết 10 attack vectors:

```
./detailed-attack-test.sh
```

![Kiểm thử tấn công chi tiết](/images/5-Workshop/5.3-S3-vpc/diagram34.png)

**Kết quả Chi tiết:**
1. XSS trong request body: 403 (CloudFront chặn)
2. XSS trong request path: 403 (CloudFront chặn)
3. SQL Injection trong query: 000 (Connection failed)
4. SQL Injection trong cookie: 200 - **DỄ BỊ TẤN CÔNG!**
5. Path Traversal: 403 (CloudFront chặn)
6. Server-side Assets: 403 (CloudFront chặn)
7. Common Bot: 200 - **DỄ BỊ TẤN CÔNG!**
8. API Misuse: 403 (CloudFront chặn)
9. Directory Traversal: 403 (CloudFront chặn)
10. Mystery Test: 200 - **DỄ BỊ TẤN CÔNG!**

#### Xác minh Hiển thị Nội dung

Kiểm tra nội dung ứng dụng được phục vụ đúng:

```
curl https://d1aty6dsjre298.cloudfront.net/ | head -20
```

![CloudFront phục vụ HTML](/images/5-Workshop/5.3-S3-vpc/diagram35.png)

Ứng dụng hiển thị đúng:
- Title: "AWS WAF Workshop Application"
- Subtitle: "Security Testing Environment"
- Content: Cấu trúc HTML với CSS styling
- Size: 2077 bytes phục vụ thành công

#### Phân tích So sánh

So sánh kết quả trước và sau khi hoàn thiện hạ tầng:

![So sánh baseline](/images/5-Workshop/5.3-S3-vpc/diagram36.png)

**Trước khi Upload Nội dung:**
- Legitimate Traffic: 403 Forbidden (không có nội dung)
- Attack Vectors: 403 Forbidden (không có nội dung)
- Nguyên nhân gốc: S3 origin trống

**Sau khi Upload Nội dung:**
- Legitimate Traffic: 200 OK (hoạt động)
- Attack Vectors: 4/10 thành công (200 OK) - **DỄ BỊ TẤN CÔNG!**
- Nguyên nhân gốc: Ứng dụng hoạt động, không có bảo vệ WAF

**Phát hiện Bảo mật Nghiêm trọng:**

Lỗ hổng đã xác nhận:
- ❌ SQL Injection qua Cookie: Thành công (200 OK)
- ❌ XSS qua Query String: Thành công (200 OK)
- ❌ Bot Traffic: Không được lọc (200 OK)
- ❌ Mystery Attack: Thành công (200 OK)

**Đánh giá Rủi ro:**
- **Mức độ Rủi ro**: NGHIÊM TRỌNG
- **Tỷ lệ Tấn công Thành công**: 40% (4/10 attacks)
- **Tác động Kinh doanh**: Rò rỉ dữ liệu, xâm phạm dịch vụ có thể xảy ra
- **Ưu tiên Khắc phục**: NGAY LẬP TỨC - Cần triển khai Giai đoạn 2

---

### Giai đoạn 2: Triển khai Bảo mật với AWS Managed Rules

#### Truy cập AWS WAF Console

Sau khi hoàn thiện hạ tầng và xác định lỗ hổng, triển khai AWS Managed Rules:

![AWS WAF Console](/images/5-Workshop/5.3-S3-vpc/diagram37.png)

**Web ACL Hiện tại:**
- Name: waf-workshop-webacl
- Scope: CloudFront (Global)
- Associated resources: CloudFront Distribution
- Rules: 0 (chưa có rules)
- Default action: Allow

#### Thêm Managed Rule Groups

Điều hướng đến tab Rules để thêm managed rules:

![Thêm managed rules](/images/5-Workshop/5.3-S3-vpc/diagram38.png)

AWS WAF cung cấp managed rule groups được duy trì và cập nhật bởi AWS. Dựa trên kết quả kiểm thử baseline, tập trung vào:
- Tấn công SQL Injection: 1 attack thành công (cookie-based)
- Tấn công XSS: 1 attack thành công (query string)
- Bot traffic: Không được lọc

#### Thêm Core Rule Set

Core rule set cung cấp bảo vệ chống lại các lỗ hổng OWASP Top 10:

![Core rule set](/images/5-Workshop/5.3-S3-vpc/diagram39.png)

**Core Rule Set bao gồm:**
- XSS Protection: Chặn Cross-Site Scripting trong body, query, headers
- SQL Injection Protection: Phát hiện các mẫu SQL injection
- Path Traversal Protection: Chặn các nỗ lực directory traversal
- Remote File Inclusion: Chặn tấn công RFI
- Local File Inclusion: Chặn tấn công LFI

**Cấu hình:**
- Version: Latest (AWS tự động cập nhật)
- Capacity: 700 WCUs
- Action: Default (Block)
- Scope-down statement: None (áp dụng cho tất cả requests)

#### Thêm SQL Database Rule Group

Để tăng cường bảo vệ chống tấn công SQL injection:

![SQL database rule group](/images/5-Workshop/5.3-S3-vpc/diagram40.png)

**SQL Database Rule Group bao gồm:**
- SQL Injection Detection: Phân tích cú pháp SQL nâng cao
- Union-based SQLi: Chặn tấn công UNION SELECT
- Boolean-based SQLi: Phát hiện boolean logic injection
- Time-based SQLi: Chặn time-based blind SQLi
- Error-based SQLi: Phát hiện error-based injection

**Cấu hình:**
- Version: Latest
- Capacity: 200 WCUs
- Action: Default (Block)
- Scope-down statement: None

#### Thiết lập Priority và Lưu Rules

Thiết lập priority cho rule groups và lưu cấu hình:

![Thiết lập priority](/images/5-Workshop/5.3-S3-vpc/diagram41.png)

**Cấu hình Priority:**
- Core rule set: Priority 0 (đánh giá trước)
- SQL database: Priority 1 (đánh giá sau)

**Logic Đánh giá Rules:**
- Rules được đánh giá theo thứ tự priority (0 → 1)
- Nếu request khớp rule với Block action → dừng đánh giá, trả về 403
- Nếu không khớp → tiếp tục đến rule tiếp theo
- Nếu không có rules nào khớp → áp dụng default action (Allow)

#### Xác minh Rules trong Web ACL

Sau khi lưu, xác minh managed rule groups đã được thêm thành công:

![Web ACL với rules](/images/5-Workshop/5.3-S3-vpc/diagram42.png)

**Trạng thái Web ACL Sau Triển khai:**
- Total rules: 2 managed rule groups
- Total capacity: 900 WCUs (700 + 200)
- Core rule set: Active, Priority 0
- SQL database: Active, Priority 1
- Default action: Allow (không thay đổi)

**Quản lý Capacity:**
- Maximum capacity: 5000 WCUs mỗi Web ACL
- Current usage: 900 WCUs (18% of maximum)
- Remaining capacity: 4100 WCUs cho rules bổ sung

---

### Xác minh Hiệu quả Bảo vệ

#### Kiểm thử lại Security Baseline Sau WAF Rules

Sau khi triển khai AWS Managed Rules, thực hiện kiểm thử bảo mật lại:

```
./test-security-baseline.sh
```

![Kiểm thử sau WAF rules](/images/5-Workshop/5.3-S3-vpc/diagram43.png)

**Kết quả Sau Bảo vệ WAF:**

**Legitimate Traffic:**
- GET request: 200 OK ✓ - Ứng dụng vẫn hoạt động bình thường
- POST with valid data: 403 Forbidden - CloudFront chặn (không phải WAF)
- API request: 403 Forbidden - Chưa cấu hình endpoint
- Static file access: 403 Forbidden - File không tồn tại

**Attack Simulation:**
- SQL Injection (query): 000 (Connection failed)
- SQL Injection (cookie): 403 Forbidden - **ĐÃ BỊ WAF CHẶN ✓**
- XSS (request body): 403 Forbidden - **ĐÃ BỊ WAF CHẶN ✓**
- XSS (URL path): 403 Forbidden - **ĐÃ BỊ WAF CHẶN ✓**
- Path Traversal: 403 Forbidden - CloudFront/WAF chặn
- Server-side assets: 403 Forbidden - CloudFront/WAF chặn
- Bot activity: 200 OK - Vẫn dễ bị tấn công (cần Bot Control)
- API misuse: 403 Forbidden - **ĐÃ BỊ WAF CHẶN ✓**
- Mystery test: 403 Forbidden - **ĐÃ BỊ WAF CHẶN ✓**

#### Phân tích Chi tiết Attack Vector

Thực hiện kiểm thử chi tiết để xác minh từng attack vector:

```
./detailed-attack-test.sh
```

![Kiểm thử chi tiết sau WAF](/images/5-Workshop/5.3-S3-vpc/diagram44.png)

**Kết quả Chi tiết:**
1. XSS trong request body: 403 - **ĐÃ BỊ WAF CHẶN ✓**
2. XSS trong request path: 403 - **ĐÃ BỊ WAF CHẶN ✓**
3. SQL Injection trong query: 000 (Connection failed)
4. SQL Injection trong cookie: 403 - **ĐÃ BỊ WAF CHẶN ✓**
5. Path Traversal: 403 - **ĐÃ BỊ WAF CHẶN ✓**
6. Server-side Assets: 403 - **ĐÃ BỊ WAF CHẶN ✓**
7. Common Bot: 200 - **VẪN DỄ BỊ TẤN CÔNG ❌**
8. API Misuse: 403 - **ĐÃ BỊ WAF CHẶN ✓**
9. Directory Traversal: 403 - **ĐÃ BỊ WAF CHẶN ✓**
10. Mystery Test: 403 - **ĐÃ BỊ WAF CHẶN ✓**

**Cải thiện Bảo mật:**
- Trước WAF: 4/10 attacks thành công (40% dễ bị tấn công)
- Sau WAF: 1/10 attacks thành công (10% dễ bị tấn công)
- **Cải thiện: Giảm 75% các cuộc tấn công thành công**

#### So sánh Hiệu quả Bảo vệ

So sánh kết quả chi tiết trước và sau khi triển khai WAF rules:

![So sánh bảo vệ](/images/5-Workshop/5.3-S3-vpc/diagram45.png)

**Trước WAF Rules (Section 2.3.2):**
- SQL Injection (cookie): 200 OK - DỄ BỊ TẤN CÔNG
- XSS (query string): 200 OK - DỄ BỊ TẤN CÔNG
- Bot activity: 200 OK - DỄ BỊ TẤN CÔNG
- Mystery test: 200 OK - DỄ BỊ TẤN CÔNG
- **Tổng**: 4/10 attacks thành công (40% dễ bị tấn công)

**Sau WAF Rules (Section 2.3.4):**
- SQL Injection (cookie): 403 - ĐÃ BỊ WAF CHẶN ✓
- XSS (query string): 403 - ĐÃ BỊ WAF CHẶN ✓
- Bot activity: 200 OK - VẪN DỄ BỊ TẤN CÔNG ❌
- Mystery test: 403 - ĐÃ BỊ WAF CHẶN ✓
- **Tổng**: 1/10 attacks thành công (10% dễ bị tấn công)

**Cải thiện Bảo mật:**
- **Giảm 75%** các cuộc tấn công thành công
- **9/10 attack vectors** hiện đã được bảo vệ
- Chỉ còn bot traffic chưa được lọc

#### Xác minh CloudWatch Metrics

Kiểm tra CloudWatch metrics để xác nhận WAF đang chặn requests:

![CloudWatch metrics](/images/5-Workshop/5.3-S3-vpc/diagram46.png)

**Phân tích Metrics:**
- **AllowedRequests**: Legitimate traffic đi qua
- **BlockedRequests**: Attack traffic đang bị WAF rules chặn
- **Rule Effectiveness**: Core Rule Set và SQL Database rules đang bảo vệ tích cực

---

### Tóm tắt

**Thành tựu Giai đoạn 1:**
- ✅ Hạ tầng hoàn thiện với ứng dụng web hoạt động
- ✅ Kiểm thử baseline xác định 4 lỗ hổng nghiêm trọng
- ✅ Môi trường kiểm thử sẵn sàng cho triển khai bảo mật

**Thành tựu Giai đoạn 2:**
- ✅ AWS Managed Rules đã triển khai (Core Rule Set + SQL Database)
- ✅ Cải thiện 75% bảo mật (9/10 attacks hiện đã bị chặn)
- ✅ Tấn công SQL Injection và XSS đã được giảm thiểu thành công
- ✅ CloudWatch monitoring hiển thị blocked requests

**Lỗ hổng Còn lại:**
- ❌ Bot traffic vẫn chưa được lọc (1/10 attacks thành công)
- **Bước Tiếp theo**: Triển khai Bot Control trong phần 4.3.3
