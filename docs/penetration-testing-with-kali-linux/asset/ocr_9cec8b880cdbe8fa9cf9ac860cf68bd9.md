# Scan your site now

# Security Report Summary

| Site | http://www.megacorpone.com/ - (Scan again over https) |
|---|---|
| IP Address | 149.56.244.87 |
| Report Time | 03 Mar 2022 07:46:46 UTC |
| Headers | X Content-Security-Policy X-Frame-Options X-Content-Type-Options X-Referrer-Policy X-Permissions-Policy |
| Warning | Grade capped at A, please see warnings below. |

![](bbox=[0.335, 0.433, 0.664, 0.447])

The site is missing several defensive headers, such as Content-Security-Policy²237 and X-Frame-Options²238 These headers are not necessarily vulnerabilities in and of themselves, but could indicate inexperienced web developers or server admins that are not familiar with server hardening²239

> Server hardening is the overall process of securing a server via configuration. This includes processes such as disabling unwanted services, removing unused services or accounts, rotating default settings, setting appropriate headers, and so forth. We do not need to know all the ins and outs of configuring every type of server, but by understanding the concepts and what to search for can help determine how best to approach a potential target.

Another scanning tool can use the SSL Server Test from Qualys Labs²240 This tool analyzes a server's SSL/TLS configuration and compares it against current best practices. It will also identify some SSL/TLS related vulnerabilities, such as Poodle²241 or Heartbleed²242 Let's scan www.megacorpone.com and check the results.

+   ²237 (Wikipedia, 2022), https://en.wikipedia.org/wiki/Content_Security_Policy
²238 (Mozilla, 2022), https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options
²239 (NIST, 2022), https://csrc.nist.gov/publications/detail/sp/800-123/final
²240 (Qualys, 2022), https://www.sslabs.com/ssl/
²241 ( (, 2022), https://en.wikipedia.org/wiki/POODLE
²242 (Wikipedia, 2022), https://en.wikipedia.org/wiki/Heartbleed