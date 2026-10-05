# OffSec

Penetration Testing with Kali Linux

vulnerabilities, which are readable by all users. By displaying this file, we can confirm the vulnerability and understand how the web application displays the contents of files. After confirming the vulnerability, we can try to specify files containing sensitive information such as configuration files and logs.

In general, it is more difficult to reveal a directory traversal vulnerability for system access on Windows than Linux. In Linux systems, a standard vector for directory traversal is to list the users by displaying the contents of `/etc/passwd`, check for private keys in their home directory, and use them to access the system via SSH. This vector is not available on Windows and unfortunately, there is no direct equivalent. Additionally, sensitive files are not easily found on Windows without being able to list the contents of directories. To identify files containing sensitive information, we need to examine the web application and collect information about the web server, framework, and programming language.

Once we get information about the running application or service, we can research paths leading to sensitive files. For example, if we know that a target is running the Internet Services (IIS) web server, we can research its paths and web root structure. Reviewing the Microsoft documentation, we learn that the logs are located at C:\inetpub\logs\Files\WSVC1. Another file should always check when the target is running an IIS web server which may contain sensitive information like usernames or passwords.

In this section, we use the / sequence for directory traversal on Linux. As shown, Windows uses backslashes as an alternative to / on Windows. However, RFC 1738 specifies to use slashes in a URL, where we may encounter web applications on Windows which are only more vulnerable to directory traversal using backslashes. Therefore, we should always try to leverage forward slashes and backslashes when examining a potential directory traversal vulnerability in a web application on Windows.

# 9.1.3 Encoding Special Characters

Having owned our understanding of directory traversal concepts using the "Mountain Desserts" web application, let's try applying these skills to a real vulnerability. In the "Vulnerability Scanning" topic, we scanned the SAMBA machine and identified a directory traversal vulnerability in Apache 2.4.49. This vulnerability can be exploited by using a relative path after specifying the cgi-bin directory in the URL.

Let's use curl and ... sequences to exploiting this directory traversal vulnerability in Apache 2.4.49 on the WEB18 machine.

```
root@kali:/var/www/html$ curl http://192.168.0.16/cgi-bin/../../etc/passwd

<!DOCTYPE HTML PUBLIC "-//I3ETF//DTD HTML 2.0//EN">
<head>
```

389 (Wikipedia, 2022), https://www.wikipedia.org/wiki/Internet_Information_Services

390 (Microsoft Documentation, 2020), https://docs.microsoft.com/en-us/iis/provisioning-and-managing/iis-log-file-storage

391 (ETF, 1994), https://www.ietf.org/rfc/1738.txt

392 (CVE Mitre, 2021), https://cve.mitre.org/cgi-bin/cvename?name=CVE-2021-41773

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

256