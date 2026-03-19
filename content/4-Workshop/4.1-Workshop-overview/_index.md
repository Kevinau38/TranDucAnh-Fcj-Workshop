---
title : "Introduction"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 4.1. </b> "
---

#### Introduce AWS WAF

**AWS Web Application Firewall (WAF)** is a web application firewall service that provides defense for web applications and APIs to secure them from well-known web attacks that may affect availability and consume excessive resources.

A web application is secured in-depth with web application firewall. Specifically, a WAF can prevent attackers from exploiting common vulnerabilities in the OWASP Top 10, such as [SQL Injection](https://owasp.org/www-community/attacks/SQL_Injection) and [Cross-Site Scripting](https://owasp.org/www-community/attacks/xss/). Moreover, you can create your custom rules in WAF to filter or block inbound or outbound HTTP(S) traffic.

#### Key Features of AWS WAF

+ **Managed Rules**: Pre-configured rule groups maintained by AWS and AWS Marketplace sellers to protect against common threats.
+ **Custom Rules**: Create your own rules to match specific patterns in web requests and control how they are handled.
+ **Bot Control**: Identify and manage bot traffic to protect your applications from automated threats.
+ **Rate Limiting**: Control the rate of requests from specific IP addresses to prevent abuse and DDoS attacks.
+ **Real-time Visibility**: Monitor and analyze web traffic patterns using AWS WAF logs and metrics.

#### Workshop Overview

In this workshop, you will learn how to:

+ Deploy and configure **AWS WAF** to protect a web application hosted on AWS.
+ Implement **AWS Managed Rules** to defend against common web attacks like SQL injection and XSS.
+ Create **custom security rules** to protect specific application paths and endpoints.
+ Configure **Bot Control** to identify and block malicious automated traffic.
+ Set up **rate limiting** to prevent abuse and resource exhaustion.
+ Monitor security events using **AWS CloudWatch** and analyze WAF logs.

![overview](/images/5-Workshop/5.1-Workshop-overview/diagram1.png)