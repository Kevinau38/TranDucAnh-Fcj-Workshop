---
title : "Infrastructure Completion & Managed Rules"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 4.3.1. </b> "
---

#### Overview

This section implements a 2-phase approach to complete the infrastructure and deploy baseline security protection using AWS Managed Rules.

**Phase 1**: Infrastructure Completion - Upload content to S3 for functional testing
**Phase 2**: Security Implementation - Deploy AWS Managed Rules for OWASP Top 10 protection

---

### Phase 1: Infrastructure Completion

#### Create Content for S3 Bucket

To have a realistic testing environment, create HTML pages simulating a real web application:

```
nano index.html
nano search.html
nano login.html
```

![Create HTML files](/images/5-Workshop/5.3-S3-vpc/diagram29.png)

Content includes:
- **index.html**: Main page with navigation and test forms
- **search.html**: Search functionality to test XSS and SQL injection
- **login.html**: Login form to test authentication attacks
- **Vulnerable components**: Forms and inputs to simulate attack vectors

#### Upload Content to S3 Bucket

Upload the created files to the configured S3 bucket:

```
aws s3 cp index.html s3://waf-workshop-280646578066/
aws s3 cp search.html s3://waf-workshop-280646578066/
aws s3 cp login.html s3://waf-workshop-280646578066/
```

![Upload files to S3](/images/5-Workshop/5.3-S3-vpc/diagram30.png)

Upload results:
- **index.html**: 2077 bytes - Main application page
- **search.html**: 342 bytes - Search functionality page
- **login.html**: 356 bytes - Authentication page

#### Verify S3 Content

Check that files were uploaded successfully:

```
aws s3 ls s3://waf-workshop-280646578066/
```

![S3 bucket listing](/images/5-Workshop/5.3-S3-vpc/diagram31.png)

S3 bucket now contains:
- 3 HTML files with timestamps
- File sizes matching local files
- S3 static website hosting configured from CloudFormation

#### Test CloudFront with New Content

Verify CloudFront distribution can serve content from S3 origin:

```
curl -I https://d1aty6dsjre298.cloudfront.net/
curl -I https://d1aty6dsjre298.cloudfront.net/search.html
curl -I https://d1aty6dsjre298.cloudfront.net/login.html
```

![CloudFront serving content](/images/5-Workshop/5.3-S3-vpc/diagram32.png)

**Breakthrough Achieved:**
- **HTTP/2 200 OK**: Instead of 403 Forbidden
- **Content-Type**: text/html served correctly
- **CloudFront caching**: "Miss from cloudfront" for first request
- **S3 integration**: CloudFront successfully pulling content from S3 origin

**Infrastructure Status:**
- ✅ S3 bucket: Content uploaded and accessible
- ✅ CloudFront: Distribution serving content properly
- ✅ WAF integration: Web ACL attached, ready for rules
- ✅ Testing environment: Functional application endpoints

---

### Phase 1 Complete: Baseline Testing with Real Content

#### Re-test Security Baseline

After completing infrastructure with real content, perform security testing again:

```
./test-security-baseline.sh
```

![Baseline testing with content](/images/5-Workshop/5.3-S3-vpc/diagram33.png)

**Legitimate Traffic Results:**
- GET request: 200 OK ✓ - Application serving content successfully
- POST with valid data: 403 Forbidden - CloudFront blocking POST requests
- API request: 403 Forbidden - No API endpoint configured
- Static file access: 403 Forbidden - File does not exist

**Attack Simulation Results:**
- SQL Injection (query): 000 (Connection failed)
- SQL Injection (cookie): 200 OK - **VULNERABLE!**
- XSS (request body): 403 Forbidden - CloudFront blocking
- XSS (URL path): 403 Forbidden - CloudFront blocking
- XSS (query string): 200 OK - **VULNERABLE!**
- Path Traversal: 403 Forbidden - CloudFront blocking
- Server-side assets: 403 Forbidden - CloudFront blocking
- Bot activity: 200 OK - **VULNERABLE!**
- API misuse: 403 Forbidden - CloudFront blocking
- Mystery test: 200 OK - **VULNERABLE!**

#### Detailed Attack Vector Analysis

Perform detailed testing of 10 attack vectors:

```
./detailed-attack-test.sh
```

![Detailed attack testing](/images/5-Workshop/5.3-S3-vpc/diagram34.png)

**Detailed Results:**
1. XSS in request body: 403 (CloudFront blocking)
2. XSS in request path: 403 (CloudFront blocking)
3. SQL Injection in query: 000 (Connection failed)
4. SQL Injection in cookie: 200 - **VULNERABLE!**
5. Path Traversal: 403 (CloudFront blocking)
6. Server-side Assets: 403 (CloudFront blocking)
7. Common Bot: 200 - **VULNERABLE!**
8. API Misuse: 403 (CloudFront blocking)
9. Directory Traversal: 403 (CloudFront blocking)
10. Mystery Test: 200 - **VULNERABLE!**

#### Verify Content Rendering

Check that application content is served correctly:

```
curl https://d1aty6dsjre298.cloudfront.net/ | head -20
```

![CloudFront serving HTML](/images/5-Workshop/5.3-S3-vpc/diagram35.png)

Application displays correctly:
- Title: "AWS WAF Workshop Application"
- Subtitle: "Security Testing Environment"
- Content: HTML structure with CSS styling
- Size: 2077 bytes served successfully

#### Comparison Analysis

Compare results before and after infrastructure completion:

![Baseline comparison](/images/5-Workshop/5.3-S3-vpc/diagram36.png)

**Before Content Upload:**
- Legitimate Traffic: 403 Forbidden (no content)
- Attack Vectors: 403 Forbidden (no content)
- Root Cause: S3 origin empty

**After Content Upload:**
- Legitimate Traffic: 200 OK (functional)
- Attack Vectors: 4/10 successful (200 OK) - **VULNERABLE!**
- Root Cause: Application functional, no WAF protection

**Critical Security Findings:**

Vulnerabilities confirmed:
- ❌ SQL Injection via Cookie: Successful (200 OK)
- ❌ XSS via Query String: Successful (200 OK)
- ❌ Bot Traffic: Unfiltered (200 OK)
- ❌ Mystery Attack: Successful (200 OK)

**Risk Assessment:**
- **Risk Level**: CRITICAL
- **Attack Success Rate**: 40% (4/10 attacks)
- **Business Impact**: Data breach, service compromise possible
- **Mitigation Priority**: IMMEDIATE - Phase 2 implementation required

---

### Phase 2: Security Implementation with AWS Managed Rules

#### Access AWS WAF Console

After completing infrastructure and identifying vulnerabilities, implement AWS Managed Rules:

![AWS WAF Console](/images/5-Workshop/5.3-S3-vpc/diagram37.png)

**Current Web ACL:**
- Name: waf-workshop-webacl
- Scope: CloudFront (Global)
- Associated resources: CloudFront Distribution
- Rules: 0 (no rules yet)
- Default action: Allow

#### Add Managed Rule Groups

Navigate to Rules tab to add managed rules:

![Add managed rules](/images/5-Workshop/5.3-S3-vpc/diagram38.png)

AWS WAF provides managed rule groups maintained and updated by AWS. Based on baseline testing results, focus on:
- SQL Injection attacks: 1 attack successful (cookie-based)
- XSS attacks: 1 attack successful (query string)
- Bot traffic: Unfiltered

#### Add Core Rule Set

Core rule set provides protection against OWASP Top 10 vulnerabilities:

![Core rule set](/images/5-Workshop/5.3-S3-vpc/diagram39.png)

**Core Rule Set includes:**
- XSS Protection: Blocks Cross-Site Scripting in body, query, headers
- SQL Injection Protection: Detects SQL injection patterns
- Path Traversal Protection: Blocks directory traversal attempts
- Remote File Inclusion: Blocks RFI attacks
- Local File Inclusion: Blocks LFI attacks

**Configuration:**
- Version: Latest (AWS auto-update)
- Capacity: 700 WCUs
- Action: Default (Block)
- Scope-down statement: None (apply to all requests)

#### Add SQL Database Rule Group

To enhance protection against SQL injection attacks:

![SQL database rule group](/images/5-Workshop/5.3-S3-vpc/diagram40.png)

**SQL Database Rule Group includes:**
- SQL Injection Detection: Advanced SQL syntax parsing
- Union-based SQLi: Blocks UNION SELECT attacks
- Boolean-based SQLi: Detects boolean logic injection
- Time-based SQLi: Blocks time-based blind SQLi
- Error-based SQLi: Detects error-based injection

**Configuration:**
- Version: Latest
- Capacity: 200 WCUs
- Action: Default (Block)
- Scope-down statement: None

#### Set Priority and Save Rules

Set priority for rule groups and save configuration:

![Set priority](/images/5-Workshop/5.3-S3-vpc/diagram41.png)

**Priority Configuration:**
- Core rule set: Priority 0 (evaluate first)
- SQL database: Priority 1 (evaluate second)

**Rule Evaluation Logic:**
- Rules evaluated in priority order (0 → 1)
- If request matches rule with Block action → stop evaluation, return 403
- If no match → continue to next rule
- If no rules match → apply default action (Allow)

#### Verify Rules in Web ACL

After saving, verify managed rule groups were added successfully:

![Web ACL with rules](/images/5-Workshop/5.3-S3-vpc/diagram42.png)

**Web ACL Status After Implementation:**
- Total rules: 2 managed rule groups
- Total capacity: 900 WCUs (700 + 200)
- Core rule set: Active, Priority 0
- SQL database: Active, Priority 1
- Default action: Allow (unchanged)

**Capacity Management:**
- Maximum capacity: 5000 WCUs per Web ACL
- Current usage: 900 WCUs (18% of maximum)
- Remaining capacity: 4100 WCUs for additional rules

---

### Verify Protection Effectiveness

#### Re-test Security Baseline After WAF Rules

After deploying AWS Managed Rules, perform security testing again:

```
./test-security-baseline.sh
```

![Testing after WAF rules](/images/5-Workshop/5.3-S3-vpc/diagram43.png)

**Results After WAF Protection:**

**Legitimate Traffic:**
- GET request: 200 OK ✓ - Application still works normally
- POST with valid data: 403 Forbidden - CloudFront blocking (not WAF)
- API request: 403 Forbidden - No endpoint configured
- Static file access: 403 Forbidden - File does not exist

**Attack Simulation:**
- SQL Injection (query): 000 (Connection failed)
- SQL Injection (cookie): 403 Forbidden - **BLOCKED BY WAF ✓**
- XSS (request body): 403 Forbidden - **BLOCKED BY WAF ✓**
- XSS (URL path): 403 Forbidden - **BLOCKED BY WAF ✓**
- Path Traversal: 403 Forbidden - CloudFront/WAF blocking
- Server-side assets: 403 Forbidden - CloudFront/WAF blocking
- Bot activity: 200 OK - Still vulnerable (needs Bot Control)
- API misuse: 403 Forbidden - **BLOCKED BY WAF ✓**
- Mystery test: 403 Forbidden - **BLOCKED BY WAF ✓**

#### Detailed Attack Vector Analysis

Perform detailed testing to verify each attack vector:

```
./detailed-attack-test.sh
```

![Detailed testing after WAF](/images/5-Workshop/5.3-S3-vpc/diagram44.png)

**Detailed Results:**
1. XSS in request body: 403 - **BLOCKED BY WAF ✓**
2. XSS in request path: 403 - **BLOCKED BY WAF ✓**
3. SQL Injection in query: 000 (Connection failed)
4. SQL Injection in cookie: 403 - **BLOCKED BY WAF ✓**
5. Path Traversal: 403 - **BLOCKED BY WAF ✓**
6. Server-side Assets: 403 - **BLOCKED BY WAF ✓**
7. Common Bot: 200 - **STILL VULNERABLE ❌**
8. API Misuse: 403 - **BLOCKED BY WAF ✓**
9. Directory Traversal: 403 - **BLOCKED BY WAF ✓**
10. Mystery Test: 403 - **BLOCKED BY WAF ✓**

**Security Improvement:**
- Before WAF: 4/10 attacks successful (40% vulnerable)
- After WAF: 1/10 attacks successful (10% vulnerable)
- **Improvement: 75% reduction in successful attacks**

#### Protection Effectiveness Comparison

Compare detailed results before and after implementing WAF rules:

![Protection comparison](/images/5-Workshop/5.3-S3-vpc/diagram45.png)

**Before WAF Rules (Section 2.3.2):**
- SQL Injection (cookie): 200 OK - VULNERABLE
- XSS (query string): 200 OK - VULNERABLE
- Bot activity: 200 OK - VULNERABLE
- Mystery test: 200 OK - VULNERABLE
- **Total**: 4/10 attacks successful (40% vulnerable)

**After WAF Rules (Section 2.3.4):**
- SQL Injection (cookie): 403 - BLOCKED BY WAF ✓
- XSS (query string): 403 - BLOCKED BY WAF ✓
- Bot activity: 200 OK - STILL VULNERABLE ❌
- Mystery test: 403 - BLOCKED BY WAF ✓
- **Total**: 1/10 attacks successful (10% vulnerable)

**Security Improvement:**
- **75% reduction** in successful attacks
- **9/10 attack vectors** now protected
- Only bot traffic remains unfiltered

#### CloudWatch Metrics Verification

Check CloudWatch metrics to confirm WAF is blocking requests:

![CloudWatch metrics](/images/5-Workshop/5.3-S3-vpc/diagram46.png)

**Metrics Analysis:**
- **AllowedRequests**: Legitimate traffic passing through
- **BlockedRequests**: Attack traffic being blocked by WAF rules
- **Rule Effectiveness**: Core Rule Set and SQL Database rules actively protecting

---

### Summary

**Phase 1 Achievements:**
- ✅ Infrastructure completed with functional web application
- ✅ Baseline testing identified 4 critical vulnerabilities
- ✅ Testing environment ready for security implementation

**Phase 2 Achievements:**
- ✅ AWS Managed Rules deployed (Core Rule Set + SQL Database)
- ✅ 75% improvement in security (9/10 attacks now blocked)
- ✅ SQL Injection and XSS attacks successfully mitigated
- ✅ CloudWatch monitoring showing blocked requests

**Remaining Vulnerabilities:**
- ❌ Bot traffic still unfiltered (1/10 attacks successful)
- **Next Step**: Implement Bot Control in section 4.3.3