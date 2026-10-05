# OffSec

Penetration Testing with Kali Linux

Excellent! We have a shell. this exploit no longer requires access to a Windows-based attack platform in the field, since we can run it from Kali.

# 14.2 Fixing Web Exploits

This Learning Unit covers the following Learning Objectives:

+   - Fix web application exploits
- Troubleshoot common application exploit issues

Web application vulnerabilities do not often result in memory corruption. Since they are not affected by protections provided by the operating system as DEP and ASLR, they are significantly easier to re-purpose. However, as we've learned during previous Modules, web application vulnerabilities can often lead to database information leaks or even full control of the underlying system.

# 14.2.1 Considerations and Overview

Even if might not have to deal with hex-encoded payloads in web exploits, it is important to properly read the code and understand what considerations must be taken in our editing process.

When modifying web exploits, there are several key questions we generally need to ask while approaching the code:

+   - Does it initiate an HTTP or HTTPS connection?
- Does it access a specific web application path or route?
- Does the exploit leverage a pre-authentication vulnerability?
- If not, how does the exploit authenticate to the web application?
- How are the GET or POST requests crafted to trigger and exploit the vulnerability? Is there any HTTP method involved?
- Does it rely on default application settings (such as the web path of the application) may have been changed after installation?
- Will却是 as self-signed certificates disrupt the exploit?

We must also remember that public web applications do not take into account additional protections such as .htaccess7 files or Web Application Firewalls (WAF). This is mainly because the exploit author cannot possibly know about all these protections during the development process, making them out of scope.

# 14.2.2 Selecting the Vulnerability and Fixing the Code

Let's consider the following scenario: during an assessment, we discover a Linux host with an exposed apache2 server. After enumerating the web server, we discover an installation of CMS

> 70 (Mozilla, 2022), https://developer.mozilla.org/en-US/docs/Learn/Server-side/Apache_Configuration_htaccess

PWK - Copyright ©2023 OffSec Services Limited. All rights reserved.

445