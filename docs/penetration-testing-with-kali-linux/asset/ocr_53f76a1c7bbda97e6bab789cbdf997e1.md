# SSL Report: we.megacorpone.com (149.56.244.87)

Assessed on: Thu 03 Mar 2022 08:10:46 UTC | hide | Clear cache

Scan Another »

# Summary

![](bbox=[0.171, 0.183, 0.828, 0.403])

Visit our documentation page for more information, configuration guides, and books. Known issues are documented here.

This server supports TLS 1.0 and TLS 1.1. Grade assigned to B. MORE INFO

This server supports TLS 1.3.

Figure 30: SSL Server Test results for we.megacorpone.com

The results seem better than the Security Headers check. However, this shows that the server supports TLS versions as 1.0 and 1.1, which are deemed legacy as they implement insecure cipher suites - this ultim means our target is not using best practices for SSL/TLS hardening. Disabling the TLS_RSA_WITH_AES_256_CBC_SHA suite has been recommended for several years⁴ for example, due to multiple vulnerabilities both on AES Cipher Blocking mode and the SHA1 algorithm. We can use these findings to gain insights about the security practices, or lack thereof, within the target organization.

# 6.3 Active Information Gathering

This Learning Unit covers the following Learning Objectives:

+   - To perform Netcat and Nmap port scanning
- Conduct DNS, SMB, SMTP, and SNMP Enumeration
- Understand Living off the Land techniques

In this Learning Unit, we will move beyond passive information gathering and explore techniques that involve direct interaction with target services. We should keep in mind that innumerable services can be targeted in the field, example Active Directory, which we'll cover in more detail in a separate Module. We'll nevertheless review some of the most common information gathering techniques in this Module including port scanning and DNS, SMB, SMTP, and SNMP enumeration.

> ⁴³ (Wikipedia, 2022), https://en.wikipedia.org/wiki/Cipher_suite
⁵ (Microsoft Security Response Center, 2013), https://msrc-blog.microsoft.com/2013/11/12/security-advisory-2868725-recommendation-to-disable-rc4/)

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

131