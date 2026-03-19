---
title : "Bot Traffic Monitoring"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 4.3.3. </b> "
---

#### Overview

After implementing AWS Managed Rules and custom path protection, testing results show that bot traffic remains a vulnerability (1/10 attacks successful). This section implements AWS WAF Bot Control to monitor and analyze bot traffic patterns before implementing blocking actions.

---

### Security Scenario

#### Real-World Situation

The security team has identified that a large amount of website traffic comes from various types of bots, including:

- **Wanted bots**: Search engine crawlers, monitoring bots
- **Unwanted bots**: Scrapers, malicious bots

#### Monitoring Requirements

- Collect detailed information about bot quantity and types
- Distinguish between wanted and unwanted bots
- Monitor bot behavior before deciding on blocking actions
- Reduce costs by excluding static content from bot inspection

#### Cost Optimization Requirement

The business wants to limit bot control scope to avoid unnecessary protection for static content like CSS, JS, and images. Developers provided the following RegEx pattern to identify static content:

```
(?i)\.(jpe?g|gif|png|svg|ico|css|js|woff2?)$
```

#### AWS WAF Bot Control Solution

Use AWS WAF Bot Control managed rule group to monitor bot traffic. This rule group provides two inspection levels:

- **Common**: Detects common bots (search engines, social media crawlers)
- **Targeted**: Detects sophisticated bots (advanced scrapers, credential stuffing)

**Strategy**: Start with Common level in Count mode to monitor and analyze bot patterns before implementing blocking.

---

### Create Regex Pattern Set for Static Content

#### Step 1: Access Regex Pattern Sets

Navigate to Regex pattern sets in AWS WAF and verify the correct region is selected:

![Access regex pattern sets](/images/5-Workshop/5.3-S3-vpc/diagram54.png)

#### Step 2: Create New Regex Pattern Set

Create a pattern set to identify static content:

![Create regex pattern set](/images/5-Workshop/5.3-S3-vpc/diagram55.png)

**Pattern Configuration:**
- **Name**: static-content
- **Region**: Global (CloudFront)
- **Description**: Pattern to match static file extensions
- **Regular expression**: `(?i)\.(jpe?g|gif|png|svg|ico|css|js|woff2?)$`

**Pattern Explanation:**
- `(?i)`: Case-insensitive matching
- `\.`: Match literal dot character
- `(jpe?g|gif|png|svg|ico|css|js|woff2?)`: Match file extensions
  - `jpe?g`: Matches both jpg and jpeg
  - `woff2?`: Matches both woff and woff2
- `$`: End of string anchor (ensures extension is at end)

---

### Configure AWS WAF Bot Control Rule Set

#### Access Web ACL

Access AWS WAF Console and open waf-workshop-webacl:

![Open Web ACL](/images/5-Workshop/5.3-S3-vpc/diagram56.png)

#### Add Bot Control Rule Group

In managed rule groups, find and add AWS WAF Bot Control:

![Add Bot Control](/images/5-Workshop/5.3-S3-vpc/diagram57.png)

AWS WAF Bot Control is a managed rule group maintained by AWS to detect and manage bot traffic. This rule group uses machine learning and behavioral analysis to identify bots.

---

### Configure Bot Control

#### Bot Control Inspection Level

Select inspection level: Common

![Select inspection level](/images/5-Workshop/5.3-S3-vpc/diagram58.png)

**Inspection Level Comparison:**

**Common:**
- Detects common bots (search engines, social media)
- Lower cost
- Suitable for most use cases

**Targeted:**
- Detects sophisticated bots
- Higher cost
- For high-value applications

#### Override Rule Actions

Set Bot Control rules: Override all rule actions to Count

![Override to Count](/images/5-Workshop/5.3-S3-vpc/diagram59.png)

**Count Mode Rationale:**
- Monitor bot traffic without blocking
- Analyze bot patterns and behavior
- Identify wanted vs unwanted bots
- Make informed decisions before enabling blocking
- Zero risk of blocking legitimate bots

---

### Configure Scope-Down Statement

#### Set Up Scope-Down to Exclude Static Content

Configure scope-down statement to limit bot control to only non-static content requests:

![Configure scope-down](/images/5-Workshop/5.3-S3-vpc/diagram60.png)

**Scope-Down Configuration:**
- **Choose scope of inspection**: Only inspect requests that match a scope-down statement
- **Scope-down statement**: Enabled (checked)
- **If a request**: doesn't match the statement (NOT)
- **Inspect**: URI path
- **Match type**: Matches pattern from regex pattern set
- **Regex pattern set**: static-content
- **Text transformation**: None

**Logic Explanation:**
- NOT (URI path matches static-content pattern)
- = Only inspect requests that are NOT static files
- = Bot Control only applies to dynamic content
- = Cost optimization by excluding CSS, JS, images

---

### Complete Configuration and Verification

#### Set Priority and Save Rules

On the "Set rule priority" page, set priority for Bot Control rule:

![Set priority](/images/5-Workshop/5.3-S3-vpc/diagram61.png)

**Priority Configuration:**
- Bot Control rule: Priority after managed rules and custom rules
- Ensures other protections evaluate first
- Click "Save" to complete

#### Verify Bot Control Rule

After saving, verify that Bot Control rule has been added successfully:

![Confirm Bot Control](/images/5-Workshop/5.3-S3-vpc/diagram62.png)

**Web ACL Status:**
- Total rules: 4 (Core Rule Set + SQL Database + path-block + Bot Control)
- Bot Control: Active, Count mode
- Scope-down: Static content excluded
- Inspection level: Common

---

### Technical Analysis and Results

#### Bot Detection Algorithm

**Machine Learning Classification:**
- **Feature extraction**: User-Agent, request patterns, timing, headers
- **Classification model**: Trained on millions of bot signatures
- **Confidence scoring**: Each request gets bot probability score
- **Label assignment**: Requests labeled with bot categories

**Behavioral Analysis:**
- **Request frequency**: Abnormal request rates
- **Navigation patterns**: Non-human browsing behavior
- **JavaScript execution**: Bot inability to execute JS
- **Cookie handling**: Bot cookie management patterns

#### Regex Pattern Matching

- **Algorithm**: Finite State Automaton (FSA)
- **Time complexity**: O(n) where n is URI path length
- **Space complexity**: O(m) where m is pattern size
- **Performance**: Compiled regex for fast matching

#### Scope-Down Logic


IF (URI path NOT matches static-content pattern) THEN
   Apply Bot Control inspection
ELSE
   Skip Bot Control (cost optimization)
END IF

#### Cost Optimization Achieved

- **Static files**: ~60% of total requests
- **Bot Control cost**: Reduced by 60%
- **Performance**: No inspection overhead for static content
- **Functionality**: Dynamic content fully protected

#### Monitoring Capabilities

- **Bot labels**: Requests tagged with bot categories
- **CloudWatch metrics**: Bot traffic volume and types
- **Sampled requests**: Detailed bot request analysis
- **Dashboard**: Visual bot traffic patterns

---

### Summary

**Achievements:**
- ✅ Bot Control rule active in Count mode
- ✅ Monitoring bot traffic without blocking
- ✅ Static content excluded for cost optimization
- ✅ Foundation for targeted bot blocking
- ✅ Data collection for rate limiting decisions

**Next Step:**
- Use bot labels from this monitoring to implement targeted blocking for specific unwanted bots in section 4.3.4