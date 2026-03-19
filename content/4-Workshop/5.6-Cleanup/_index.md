---
title : "Clean up"
date : 2024-01-01
weight : 4
chapter : false
pre : " <b> 4.4. </b> "
---

Congratulations on completing this workshop!

In this workshop, you learned comprehensive AWS WAF security implementation patterns to protect web applications from various threats.

+ By implementing AWS Managed Rules, you protected against OWASP Top 10 vulnerabilities including SQL injection and XSS attacks.
+ By creating custom rules, you secured specific application paths and implemented granular access control.
+ By configuring Bot Control, you identified and managed bot traffic while maintaining legitimate bot access.
+ By implementing rate limiting, you prevented traffic spikes and resource exhaustion.
+ By validating API parameters, you enforced business logic constraints at the WAF layer.

#### Clean up

1. Navigate to AWS WAF console in us-east-1 region. Go to Web ACLs and select "waf-workshop-webacl". Go to "Associated AWS resources" tab, select the CloudFront distribution, and click "Remove" to disassociate.

![disassociate cloudfront step 1](/images/5-Workshop/5.6-Cleanup/diagram96.png)

![disassociate cloudfront step 2](/images/5-Workshop/5.6-Cleanup/diagram97.png)

2. After disassociation, select "waf-workshop-webacl" from the Web ACLs list and click "Delete". Type "delete" to confirm and click "Delete".

![delete webacl step 1](/images/5-Workshop/5.6-Cleanup/diagram98.png)

![delete webacl step 2](/images/5-Workshop/5.6-Cleanup/diagram99.png)

3. Navigate to "Regex pattern sets" in AWS WAF console. Delete the following pattern sets:
+ static-content
+ number-1-to-100

![delete regex step 1](/images/5-Workshop/5.6-Cleanup/diagram100.png)

![delete regex step 2](/images/5-Workshop/5.6-Cleanup/diagram101.png)

![delete regex step 3](/images/5-Workshop/5.6-Cleanup/diagram102.png)

![delete regex step 4](/images/5-Workshop/5.6-Cleanup/diagram103.png)

4. Navigate to CloudFront console. Select your distribution, click "Disable", wait for status to change to "Disabled" (5-10 minutes), then select it again and click "Delete".

![delete cloudfront step 1](/images/5-Workshop/5.6-Cleanup/diagram104.png)

![delete cloudfront step 2](/images/5-Workshop/5.6-Cleanup/diagram105.png)

![delete cloudfront step 3](/images/5-Workshop/5.6-Cleanup/diagram106.png)

![delete cloudfront step 4](/images/5-Workshop/5.6-Cleanup/diagram107.png)

5. Navigate to S3 console in ap-southeast-1 region. Select the bucket "waf-workshop-280646578066", click "Empty" and confirm. After emptying, click "Delete" and type the bucket name to confirm.

![delete s3 step 1](/images/5-Workshop/5.6-Cleanup/diagram108.png)

![delete s3 step 2](/images/5-Workshop/5.6-Cleanup/diagram109.png)

![delete s3 step 3](/images/5-Workshop/5.6-Cleanup/diagram110.png)

![delete s3 step 4](/images/5-Workshop/5.6-Cleanup/diagram111.png)

6. Navigate to Lambda console in ap-southeast-1 region. Select "waf-workshop-dashboard" function, click "Actions" → "Delete" and confirm.

![delete lambda step 1](/images/5-Workshop/5.6-Cleanup/diagram112.png)

![delete lambda step 2](/images/5-Workshop/5.6-Cleanup/diagram113.png)

7. Navigate to IAM console. Go to "Roles", search for "waf-workshop", select the Lambda execution role, and click "Delete".

![delete iam step 1](/images/5-Workshop/5.6-Cleanup/diagram114.png)

![delete iam step 2](/images/5-Workshop/5.6-Cleanup/diagram115.png)

![delete iam step 3](/images/5-Workshop/5.6-Cleanup/diagram116.png)

8. (Optional) If you used CloudFormation, navigate to CloudFormation console in ap-southeast-1 region and delete the "waf-workshop" stack.

![delete stack step 1](/images/5-Workshop/5.6-Cleanup/diagram117.png)

![delete stack step 2](/images/5-Workshop/5.6-Cleanup/diagram118.png)