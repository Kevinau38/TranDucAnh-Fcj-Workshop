---
title : "Preparation"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 4.2. </b> "
---

#### Environment Setup

In this section, you will prepare the workshop environment by creating necessary AWS resources using CloudFormation.

#### Create Working Directory

First, create a working directory for the workshop:

```
cd ~
mkdir aws-waf-workshop
cd aws-waf-workshop
```

![Create working directory](/images/5-Workshop/5.2-Prerequisite/diagram2.png)

#### Create CloudFormation Template

Create a CloudFormation template file `waf-workshop.yaml` that defines the necessary AWS resources:

```
nano waf-workshop.yaml
```

The template includes the following main resources:
- **S3 Bucket**: Stores static website with public access
- **Lambda Function**: Handles dashboard logic
- **IAM Role**: Grants permissions to Lambda function

After creating the file, verify it:

```
ls -lh
```

![CloudFormation template file created](/images/5-Workshop/5.2-Prerequisite/diagram3.png)

View the template content:

```
cat waf-workshop.yaml
```

![CloudFormation template content - part 1](/images/5-Workshop/5.2-Prerequisite/diagram4.png)

![CloudFormation template content - part 2](/images/5-Workshop/5.2-Prerequisite/diagram5.png)

#### Create Deployment Script

Create a script to automate the CloudFormation stack deployment:

bash
nano deploy-workshop-own-account.sh

The script performs the following functions:
- Checks if template file exists
- Creates CloudFormation stack with IAM capabilities
- Waits for stack creation to complete
- Displays stack outputs upon success

Make the script executable:

bash
chmod +x deploy-workshop-own-account.sh

Verify the files:

bash
ls -lh

![Working directory with files](/images/4-Workshop/4.2-Preparation/hinh_2_6.png)
*Hình 2.6: Thư mục làm việc với 2 files*

#### Deploy CloudFormation Stack

Run the deployment script:

bash
./deploy-workshop-own-account.sh

![Script execution started](/images/4-Workshop/4.2-Preparation/hinh_2_7.png)
*Hình 2.7: Script bắt đầu chạy và tạo CloudFormation stack*

![Waiting for stack creation](/images/4-Workshop/4.2-Preparation/hinh_2_8.png)
*Hình 2.8: Đợi stack creation hoàn tất (10-15 phút)*

#### Troubleshooting Deployment Errors

If the stack creation fails:

![Stack creation failed](/images/4-Workshop/4.2-Preparation/hinh_2_9.png)
*Hình 2.9: Stack creation failed với status ROLLBACK_COMPLETE*

Check error details:

bash
aws cloudformation describe-stack-events \
 --stack-name waf-workshop \
 --region ap-southeast-1 \
 --max-items 20 \
 --query 'StackEvents[?ResourceStatus==CREATE_FAILED].[LogicalResourceId,ResourceStatusReason]' \
 --output table

![CloudFormation error details](/images/4-Workshop/4.2-Preparation/hinh_2_10.png)
*Hình 2.10: Chi tiết lỗi CloudFormation - WAF với scope CLOUDFRONT không thể tạo ở ap-southeast-1*

**Error Resolution:**
WAF Web ACL with CLOUDFRONT scope can only be created in us-east-1 region. Delete the failed stack and modify the template.

Delete failed stack:

bash
aws cloudformation delete-stack \
 --stack-name waf-workshop \
 --region ap-southeast-1

aws cloudformation wait stack-delete-complete \
 --stack-name waf-workshop \
 --region ap-southeast-1

Edit the template:

bash
nano waf-workshop.yaml

![Edit template - part 1](/images/4-Workshop/4.2-Preparation/hinh_2_11.png)
*Hình 2.11: Sửa template trong nano editor (phần đầu)*

![Edit template - part 2](/images/4-Workshop/4.2-Preparation/hinh_2_12.png)
*Hình 2.12: Sửa template trong nano editor (phần cuối - Outputs)*

#### Successful Deployment

After fixing the template, run the deployment script again:

bash
./deploy-workshop-own-account.sh

![Stack created successfully](/images/4-Workshop/4.2-Preparation/hinh_2_13.png)
*Hình 2.13: Stack created successfully với Stack Outputs*

Stack outputs include:
- **WebsiteURL**: S3 static website URL
- **S3BucketName**: Created S3 bucket name
- **LambdaFunctionName**: Lambda function name

#### Verify on AWS Console

Check CloudFormation Console:

![CloudFormation Console](/images/4-Workshop/4.2-Preparation/hinh_2_14.png)
*Hình 2.14: CloudFormation Console hiển thị stack waf-workshop với status CREATE_COMPLETE*

![Stack Outputs on Console](/images/4-Workshop/4.2-Preparation/hinh_2_15.png)
*Hình 2.15: Stack Outputs trên AWS Console*

Access the S3 website URL:

![S3 Website URL](/images/4-Workshop/4.2-Preparation/hinh_2_16.png)
*Hình 2.16: S3 Website URL (có thể hiển thị 404 vì chưa upload index.html)*

#### Workshop Architecture

The workshop architecture includes the following components:

![Workshop Architecture](/images/4-Workshop/4.2-Preparation/hinh_2_17.png)
*Hình 2.17: Kiến trúc AWS WAF Workshop*

**Key Components:**
- **Amazon CloudFront**: Global content delivery with WAF integration
- **AWS WAF Web ACL**: Web application firewall (to be configured)
- **Amazon S3**: Static website hosting
- **AWS Lambda**: Dashboard processing function
- **Amazon CloudWatch**: Monitoring and logging

#### Create WAF Web ACL

Create a WAF Web ACL in us-east-1 region (required for CloudFront scope):

![Create WAF Web ACL](/images/4-Workshop/4.2-Preparation/hinh_2_18.png)
*Hình 2.18: Lệnh tạo WAF Web ACL với visibility config và response JSON*

#### Create CloudFront Distribution

Create a CloudFront distribution integrated with the WAF Web ACL:

![Create CloudFront Distribution](/images/4-Workshop/4.2-Preparation/hinh_2_19.png)
*Hình 2.19: CloudFront create-distribution response với Distribution ID*

Wait for distribution deployment:

![Wait for CloudFront deployment](/images/4-Workshop/4.2-Preparation/hinh_2_20.png)
*Hình 2.20: CloudFront wait distribution-deployed thành công*

#### Verify Deployment

Check CloudFront Distribution on Console:

![CloudFront Console](/images/4-Workshop/4.2-Preparation/hinh_2_21.png)
*Hình 2.21: CloudFront Console hiển thị Distribution với status Enabled*

Check WAF Web ACL on Console:

![WAF Console](/images/4-Workshop/4.2-Preparation/hinh_2_22.png)
*Hình 2.22: AWS WAF Console hiển thị waf-workshop-webacl*

Access CloudFront domain:

![CloudFront domain response](/images/4-Workshop/4.2-Preparation/hinh_2_23.png)
*Hình 2.23: CloudFront domain trả về XML response với Access Denied message*

Check CloudFormation Stack Outputs:

![CloudFormation Stack Outputs](/images/4-Workshop/4.2-Preparation/hinh_2_24.png)
*Hình 2.24: CloudFormation describe-stacks outputs hiển thị 3 thông tin chính*

#### Initial Security Assessment

Check current WAF Web ACL status:

bash
aws wafv2 get-web-acl \
 --id <WEB_ACL_ID> \
 --name waf-workshop-webacl \
 --scope CLOUDFRONT \
 --region us-east-1

![WAF Web ACL status](/images/4-Workshop/4.2-Preparation/hinh_2_25.png)
*Hình 2.25: WAF Web ACL chưa có rules bảo vệ - Rules array trống*

Current state:
- **DefaultAction**: Allow (permits all traffic)
- **Rules**: [] (no rules configured yet)
- **Capacity**: 0 (no capacity used)

#### Create Security Testing Scripts

Create a baseline security testing script:

bash
nano test-security-baseline.sh
chmod +x test-security-baseline.sh
./test-security-baseline.sh

![Baseline Testing Results](/images/4-Workshop/4.2-Preparation/hinh_2_26.png)
*Hình 2.26: Baseline testing results - Legitimate traffic và attack simulation*

**Baseline Testing Results:**
- Legitimate Traffic: All requests return 403 Forbidden
- Attack Simulation: Most attacks return 403 Forbidden
- No WAF rules blocking attacks yet

#### Detailed Attack Vector Analysis

Create a detailed attack testing script:

bash
nano detailed-attack-test.sh
chmod +x detailed-attack-test.sh
./detailed-attack-test.sh

![Detailed Attack Testing](/images/4-Workshop/4.2-Preparation/hinh_2_27.png)
*Hình 2.27: Detailed attack testing - 10 attack vectors với kết quả 403/000*

**Detailed Attack Results:**

1. **XSS in request body**: 403 Forbidden - POST request with script payload
2. **XSS in request path**: 403 Forbidden - Script injection in URL path
3. **SQL Injection in query**: 000 (Connection failed) - Union-based SQL injection
4. **SQL Injection in cookie**: 403 Forbidden - Cookie-based SQL injection
5. **Path Traversal**: 403 Forbidden - Directory traversal with ../../../
6. **Server-side Assets**: 403 Forbidden - Access to .env file
7. **Common Bot**: 403 Forbidden - BadBot User-Agent simulation
8. **API Misuse**: 403 Forbidden - JSON payload with script injection
9. **Directory Traversal**: 403 Forbidden - Includes directory traversal
10. **Mystery Test**: 403 Forbidden - Combined X-Forwarded-For and path traversal

#### CloudWatch Metrics Monitoring

Check CloudWatch metrics to verify WAF behavior and traffic patterns:

![CloudWatch Metrics](/images/4-Workshop/4.2-Preparation/hinh_2_28.png)
*Hình 2.28: CloudWatch metrics cho WAF - chỉ có allowed requests, chưa có blocked requests*

**Metrics Analysis:**
- **AllowedRequests**: Traffic passing through WAF (all allowed)
- **BlockedRequests**: 0 (no requests blocked by WAF rules yet)
- **SampledRequests**: Available for debugging and analysis
- **Metric Name**: "waf-workshop-webacl" configured correctly

#### Current Security Assessment

**Positive Points:**
- WAF Web ACL successfully created and integrated with CloudFront
- CloudWatch monitoring enabled with full visibility configuration
- Sampled requests enabled for debugging and forensic analysis
- Infrastructure foundation ready for security rule implementation

**Areas for Improvement:**
- No WAF rules configured yet (Rules array empty)
- Application has no content for full-scale testing
- Need to upload content to S3 bucket for accurate baseline testing
- Testing environment not complete to verify WAF effectiveness

**Root Cause Analysis:**
- **403 Forbidden responses**: CloudFront origin (S3) has no content, not due to WAF blocking
- **000 Connection failed**: Network timeout with specific attack payload
- **WAF not blocking**: No rules configured yet

#### Analysis and Remediation Planning

**Current Security Status:**

Based on comprehensive security testing results:

**Testing Results Analysis:**
- **WAF Status**: Web ACL created but no rules configured (Rules: [])
- **Application Status**: CloudFront returns 403 Forbidden due to empty S3 origin
- **Security Posture**: Cannot fully assess due to missing content for testing

**Root Cause Analysis:**
- 403 Forbidden responses: Infrastructure incomplete, not security blocking
- Testing limitations: Cannot verify WAF effectiveness with current setup
- Missing components: S3 content, proper application endpoints

#### Remediation Preparation

Based on the analysis, a 2-phase approach is needed:

**Phase 1 - Infrastructure Completion:**
- Upload content to S3 bucket for functional application
- Verify CloudFront serving content properly (200 OK responses)
- Establish proper testing baseline

**Phase 2 - Security Implementation:**
- Configure AWS Managed Rules (Core Rule Set, SQL Database)
- Set up custom rules for specific protection
- Implement rate limiting and bot control
- Fine-tuning to avoid false positives

The next phase will focus on completing infrastructure setup before implementing security measures, ensuring a proper testing environment to verify WAF effectiveness.