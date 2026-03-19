---
title : "Giám sát Lưu lượng Bot"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 4.3.3. </b> "
---

#### Tổng quan

Sau khi triển khai AWS Managed Rules và bảo vệ đường dẫn tùy chỉnh, kết quả kiểm thử cho thấy bot traffic vẫn là lỗ hổng (1/10 attacks thành công). Phần này triển khai AWS WAF Bot Control để giám sát và phân tích các mẫu bot traffic trước khi triển khai hành động chặn.

---

### Kịch bản Bảo mật

#### Tình huống Thực tế

Đội bảo mật đã xác định rằng một lượng lớn traffic website đến từ các loại bot khác nhau, bao gồm:

- **Wanted bots**: Search engine crawlers, monitoring bots
- **Unwanted bots**: Scrapers, malicious bots

#### Yêu cầu Giám sát

- Thu thập thông tin chi tiết về số lượng và loại bot
- Phân biệt giữa wanted và unwanted bots
- Giám sát hành vi bot trước khi quyết định hành động chặn
- Giảm chi phí bằng cách loại trừ static content khỏi bot inspection

#### Yêu cầu Tối ưu Chi phí

Doanh nghiệp muốn giới hạn phạm vi bot control để tránh bảo vệ không cần thiết cho static content như CSS, JS, và images. Developers cung cấp RegEx pattern sau để xác định static content:

```
(?i)\.(jpe?g|gif|png|svg|ico|css|js|woff2?)$
```

#### Giải pháp AWS WAF Bot Control

Sử dụng AWS WAF Bot Control managed rule group để giám sát bot traffic. Rule group này cung cấp hai mức inspection:

- **Common**: Phát hiện common bots (search engines, social media crawlers)
- **Targeted**: Phát hiện sophisticated bots (advanced scrapers, credential stuffing)

**Chiến lược**: Bắt đầu với mức Common ở chế độ Count để giám sát và phân tích các mẫu bot trước khi triển khai chặn.

---

### Tạo Regex Pattern Set cho Static Content

#### Bước 1: Truy cập Regex Pattern Sets

Điều hướng đến Regex pattern sets trong AWS WAF và xác minh region đúng đã được chọn:

![Truy cập regex pattern sets](/images/5-Workshop/5.3-S3-vpc/diagram54.png)

#### Bước 2: Tạo Regex Pattern Set Mới

Tạo pattern set để xác định static content:

![Tạo regex pattern set](/images/5-Workshop/5.3-S3-vpc/diagram55.png)

**Cấu hình Pattern:**
- **Name**: static-content
- **Region**: Global (CloudFront)
- **Description**: Pattern to match static file extensions
- **Regular expression**: `(?i)\.(jpe?g|gif|png|svg|ico|css|js|woff2?)$`

**Giải thích Pattern:**
- `(?i)`: Matching không phân biệt hoa thường
- `\.`: Khớp ký tự dấu chấm
- `(jpe?g|gif|png|svg|ico|css|js|woff2?)`: Khớp các phần mở rộng file
  - `jpe?g`: Khớp cả jpg và jpeg
  - `woff2?`: Khớp cả woff và woff2
- `$`: Neo cuối chuỗi (đảm bảo phần mở rộng ở cuối)

---

### Cấu hình AWS WAF Bot Control Rule Set

#### Truy cập Web ACL

Truy cập AWS WAF Console và mở waf-workshop-webacl:

![Mở Web ACL](/images/5-Workshop/5.3-S3-vpc/diagram56.png)

#### Thêm Bot Control Rule Group

Trong managed rule groups, tìm và thêm AWS WAF Bot Control:

![Thêm Bot Control](/images/5-Workshop/5.3-S3-vpc/diagram57.png)

AWS WAF Bot Control là managed rule group được duy trì bởi AWS để phát hiện và quản lý bot traffic. Rule group này sử dụng machine learning và behavioral analysis để xác định bots.

---

### Cấu hình Bot Control

#### Mức Inspection Bot Control

Chọn mức inspection: Common

![Chọn mức inspection](/images/5-Workshop/5.3-S3-vpc/diagram58.png)

**So sánh Mức Inspection:**

**Common:**
- Phát hiện common bots (search engines, social media)
- Chi phí thấp hơn
- Phù hợp cho hầu hết use cases

**Targeted:**
- Phát hiện sophisticated bots
- Chi phí cao hơn
- Cho ứng dụng có giá trị cao

#### Override Rule Actions

Thiết lập Bot Control rules: Override tất cả rule actions thành Count

![Override thành Count](/images/5-Workshop/5.3-S3-vpc/diagram59.png)

**Lý do Count Mode:**
- Giám sát bot traffic mà không chặn
- Phân tích các mẫu và hành vi bot
- Xác định wanted vs unwanted bots
- Đưa ra quyết định có thông tin trước khi bật chặn
- Không có rủi ro chặn bots hợp lệ

---

### Cấu hình Scope-Down Statement

#### Thiết lập Scope-Down để Loại trừ Static Content

Cấu hình scope-down statement để giới hạn bot control chỉ cho các requests nội dung không phải static:

![Cấu hình scope-down](/images/5-Workshop/5.3-S3-vpc/diagram60.png)

**Cấu hình Scope-Down:**
- **Choose scope of inspection**: Only inspect requests that match a scope-down statement
- **Scope-down statement**: Enabled (checked)
- **If a request**: doesn't match the statement (NOT)
- **Inspect**: URI path
- **Match type**: Matches pattern from regex pattern set
- **Regex pattern set**: static-content
- **Text transformation**: None

**Giải thích Logic:**
- NOT (URI path matches static-content pattern)
- = Chỉ inspect requests KHÔNG phải static files
- = Bot Control chỉ áp dụng cho dynamic content
- = Tối ưu chi phí bằng cách loại trừ CSS, JS, images

---

### Hoàn thành Cấu hình và Xác minh

#### Thiết lập Priority và Lưu Rules

Trên trang "Set rule priority", thiết lập priority cho Bot Control rule:

![Thiết lập priority](/images/5-Workshop/5.3-S3-vpc/diagram61.png)

**Cấu hình Priority:**
- Bot Control rule: Priority sau managed rules và custom rules
- Đảm bảo các bảo vệ khác đánh giá trước
- Click "Save" để hoàn thành

#### Xác minh Bot Control Rule

Sau khi lưu, xác minh Bot Control rule đã được thêm thành công:

![Xác nhận Bot Control](/images/5-Workshop/5.3-S3-vpc/diagram62.png)

**Trạng thái Web ACL:**
- Total rules: 4 (Core Rule Set + SQL Database + path-block + Bot Control)
- Bot Control: Active, Count mode
- Scope-down: Static content đã loại trừ
- Inspection level: Common

---

### Phân tích Kỹ thuật và Kết quả

#### Thuật toán Phát hiện Bot

**Machine Learning Classification:**
- **Feature extraction**: User-Agent, request patterns, timing, headers
- **Classification model**: Được train trên hàng triệu bot signatures
- **Confidence scoring**: Mỗi request nhận điểm xác suất bot
- **Label assignment**: Requests được gắn nhãn với các danh mục bot

**Behavioral Analysis:**
- **Request frequency**: Tốc độ request bất thường
- **Navigation patterns**: Hành vi duyệt web không phải con người
- **JavaScript execution**: Bot không có khả năng thực thi JS
- **Cookie handling**: Các mẫu quản lý cookie của bot

#### Regex Pattern Matching

- **Algorithm**: Finite State Automaton (FSA)
- **Time complexity**: O(n) với n là độ dài URI path
- **Space complexity**: O(m) với m là kích thước pattern
- **Performance**: Compiled regex cho matching nhanh

#### Scope-Down Logic


IF (URI path NOT matches static-content pattern) THEN
   Apply Bot Control inspection
ELSE
   Skip Bot Control (cost optimization)
END IF

#### Tối ưu Chi phí Đạt được

- **Static files**: ~60% tổng requests
- **Chi phí Bot Control**: Giảm 60%
- **Performance**: Không có inspection overhead cho static content
- **Functionality**: Dynamic content được bảo vệ đầy đủ

#### Khả năng Giám sát

- **Bot labels**: Requests được gắn thẻ với các danh mục bot
- **CloudWatch metrics**: Lượng và loại bot traffic
- **Sampled requests**: Phân tích chi tiết bot request
- **Dashboard**: Các mẫu bot traffic trực quan

---

### Tóm tắt

**Thành tựu:**
- ✅ Bot Control rule hoạt động ở chế độ Count
- ✅ Giám sát bot traffic mà không chặn
- ✅ Static content đã loại trừ để tối ưu chi phí
- ✅ Nền tảng cho targeted bot blocking
- ✅ Thu thập dữ liệu cho quyết định rate limiting

**Bước Tiếp theo:**
- Sử dụng bot labels từ giám sát này để triển khai chặn có mục tiêu cho các unwanted bots cụ thể trong phần 4.3.4
