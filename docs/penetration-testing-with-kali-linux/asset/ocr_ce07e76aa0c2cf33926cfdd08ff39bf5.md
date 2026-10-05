# OffSec. Penetration Testing with Kali Linux

broader search. Unfortunately, the search didn't provide any meaningful results apart from some CVEs.

# Hmailserver: Security Vulnerabilities

| # | CVE | WID | # Exploits | Vulnerability Type(s) | Publish Date | Update Date | Score | Gained Access | Access | Complexity | Authentication | Conf. | Intrig. |
|---|---|---|---|---|---|---|---|---|---|---|---|---||
| 1 | CVE-2020-15719 | | | | 2020-01-07 | | | None | Remote | High | Not required | None | Partial |
| 2 | CVE-2008-2562 | | | | 2008-06-11 | 2018-08-31 | 4.1 | | Remote | Medium | Not required | None | Partial |

Figure 287. Vulnerabilities in HmailServer

If we had a matching exploit providing the code execution, we should not skip the remaining enumeration steps. While we might get access to the target system, we could potentially miss out vital data or information for other services and systems.

Next, let's enumerate the IIS server. First, we'll browse the web page.

![](bbox=[0.118, 0.473, 0.882, 0.733])

Figure 288 shows that IIS displays the default page on MAILSRV1

Figure 288 shows that IIS displays the default web page. Let's try to identify directories and files by using gobuster. We'll enter dir to use directory enumeration mode, -u for URL, -w for a wordlist, and -x for files we want to identify. In this example, we'll use txt, pdf, and config to identify potential documents or configuration files. In addition, we'll use -o to create an output.

```
kali@kali:~beyond$ gobuster dir -u http://192.168.50.242 -w /usr/share/wordlists/dirb/common.txt -o mailsrv1 -x txt,pdf,config
```

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

809