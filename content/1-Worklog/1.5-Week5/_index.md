---
title: "Week 5 Worklog"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 Objectives:

* Learn AWS WAF fundamentals and web application security concepts.
* Understand OWASP Top 10 vulnerabilities and mitigation strategies.
* Study AWS WAF components: Web ACLs, Rules, and Rule Groups.
* Research AWS Managed Rules and custom rule creation.
* Begin planning AWS WAF workshop implementation.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Learn AWS WAF fundamentals and architecture. <br> - Understand web application security threats. <br> - Study WAF vs traditional firewalls. <br> - Learn about AWS WAF pricing and deployment models.                                                                      | 02/03/2026 | 02/03/2026      | <https://docs.aws.amazon.com/waf/latest/developerguide/waf-chapter.html> <br> <https://docs.aws.amazon.com/waf/latest/developerguide/how-aws-waf-works.html> |
| 3   | - Study OWASP Top 10 vulnerabilities: <br>&emsp; + SQL Injection <br>&emsp; + Cross-Site Scripting (XSS) <br>&emsp; + Broken Authentication <br>&emsp; + Security Misconfiguration <br> - Learn mitigation strategies for each vulnerability.                                               | 03/03/2026 | 03/03/2026      | <https://owasp.org/www-project-top-ten/> <br> <https://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups-list.html> |
| 4   | - Learn AWS WAF components: <br>&emsp; + Web ACLs (Access Control Lists) <br>&emsp; + Rules and Rule Groups <br>&emsp; + Conditions and Statements <br> - Understand rule evaluation order and actions.                                                    | 04/03/2026 | 04/03/2026      | <https://docs.aws.amazon.com/waf/latest/developerguide/web-acl.html> <br> <https://docs.aws.amazon.com/waf/latest/developerguide/waf-rules.html> |
| 5   | - Study AWS Managed Rules: <br>   + Core Rule Set (CRS) <br>   + Known Bad Inputs <br>   + SQL Database <br>   + Linux Operating System <br>   + POSIX Operating System <br> - Learn about rule group priorities and exceptions.                                 | 05/03/2026 | 05/03/2026      | <https://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups.html> |
| 6   | - **Research:** Plan AWS WAF workshop: <br>   + Define workshop scope and objectives. <br>   + Design hands-on scenarios for common attacks. <br>   + Plan infrastructure setup with CloudFormation. <br>   + Outline custom rule creation exercises.                                  | 06/03/2026 | 06/03/2026      | <https://docs.aws.amazon.com/waf/latest/developerguide/getting-started.html> |

### Week 5 Achievements:

* **Understood AWS WAF fundamentals:**
  * Understood WAF architecture and deployment models.
  * Learned how AWS WAF integrates with CloudFront, ALB, and API Gateway.
  * Studied WAF vs traditional firewall differences.
  * Understood AWS WAF pricing structure and cost optimization.

* **Gained deep knowledge of web application security:**
  * Studied OWASP Top 10 vulnerabilities in detail.
  * Learned SQL injection attack vectors and prevention.
  * Understood XSS attack types and mitigation strategies.
  * Explored authentication bypass techniques and countermeasures.

* **Acquired expertise in AWS WAF components:**
  * Learned Web ACL structure and configuration.
  * Understood rule types: rate-based, regular, and group rules.
  * Studied rule evaluation logic and action precedence.
  * Learned about rule conditions and match statements.

* **Explored AWS Managed Rules:**
  * Studied Core Rule Set for OWASP Top 10 protection.
  * Learned Known Bad Inputs rule group capabilities.
  * Understood SQL Database and OS-specific rule groups.
  * Explored rule group customization and exception handling.

* **Planned comprehensive AWS WAF workshop:**
  * Defined workshop learning objectives and outcomes.
  * Designed practical attack scenarios for hands-on learning.
  * Planned CloudFormation infrastructure automation.
  * Outlined progressive difficulty levels for rule creation exercises.