---
title: "Week 6 Worklog"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives:

* Implement AWS WAF infrastructure using CloudFormation.
* Deploy and configure AWS Managed Rules for OWASP protection.
* Create custom WAF rules for specific application protection.
* Test WAF effectiveness against common web attacks.
* Monitor and analyze WAF logs and metrics.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Create CloudFormation template for WAF infrastructure. <br> - Deploy S3 bucket, CloudFront distribution, and Lambda function. <br> - Set up basic web application for testing. <br> - Configure CloudWatch logging.                                                                      | 09/03/2026 | 09/03/2026      | <https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-anatomy.html> <br> <https://docs.aws.amazon.com/waf/latest/developerguide/logging.html> |
| 3   | - Create AWS WAF Web ACL. <br> - Deploy AWS Managed Rules: <br>&emsp; + Core Rule Set <br>&emsp; + Known Bad Inputs <br>&emsp; + SQL Database <br> - Associate Web ACL with CloudFront distribution.                                               | 10/03/2026 | 10/03/2026      | <https://docs.aws.amazon.com/waf/latest/developerguide/web-acl-creating.html> <br> <https://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups.html> |
| 4   | - Test SQL injection protection: <br>&emsp; + Craft malicious SQL payloads <br>&emsp; + Verify WAF blocking behavior <br>&emsp; + Analyze blocked request logs <br> - Test XSS protection with various attack vectors.                                                    | 11/03/2026 | 11/03/2026      | <https://docs.aws.amazon.com/waf/latest/developerguide/waf-rule-statement-type-sqli-match.html> <br> <https://docs.aws.amazon.com/waf/latest/developerguide/waf-rule-statement-type-xss-match.html> |
| 5   | - Create custom WAF rules: <br>   + Path-based protection rules <br>   + IP-based blocking rules <br>   + Geographic restrictions <br>   + User-agent filtering <br> - Configure rule priorities and actions.                                 | 12/03/2026 | 12/03/2026      | <https://docs.aws.amazon.com/waf/latest/developerguide/waf-rules.html> <br> <https://docs.aws.amazon.com/waf/latest/developerguide/waf-rule-statements.html> |
| 6   | - **Monitoring & Analysis:** <br>   + Set up CloudWatch dashboards for WAF metrics. <br>   + Configure WAF log analysis. <br>   + Create alerts for security events. <br>   + Document test results and rule effectiveness.                                  | 13/03/2026 | 13/03/2026      | <https://docs.aws.amazon.com/waf/latest/developerguide/monitoring-cloudwatch.html> <br> <https://docs.aws.amazon.com/waf/latest/developerguide/logging-management.html> |

### Week 6 Achievements:

* **Successfully deployed WAF infrastructure:**
  * Created comprehensive CloudFormation template for workshop environment.
  * Deployed S3 bucket with static website hosting configuration.
  * Set up CloudFront distribution with custom domain and SSL.
  * Configured Lambda function for dynamic content generation.

* **Implemented AWS Managed Rules protection:**
  * Created Web ACL with proper rule evaluation order.
  * Deployed Core Rule Set for OWASP Top 10 protection.
  * Configured Known Bad Inputs rule group for malicious payload detection.
  * Implemented SQL Database rule group for injection attack prevention.

* **Validated security effectiveness through testing:**
  * Conducted SQL injection attacks and verified blocking behavior.
  * Tested XSS payloads across different attack vectors.
  * Analyzed WAF logs to understand rule matching patterns.
  * Documented attack signatures and WAF response actions.

* **Created advanced custom protection rules:**
  * Implemented path-based rules to protect sensitive directories.
  * Created IP-based blocking for known malicious sources.
  * Configured geographic restrictions for compliance requirements.
  * Set up user-agent filtering to block automated tools.

* **Established comprehensive monitoring:**
  * Built CloudWatch dashboards for real-time WAF metrics.
  * Configured log streaming to CloudWatch Logs for analysis.
  * Set up automated alerts for high-risk security events.
  * Created documentation for ongoing security monitoring procedures.