# # OffSec

Penetration Testing with Kali Linux

| | | | | |
|---|---|---|---||
| CRITICAL | 9.8 | Ubuntu 20.04 LTS / 20.04: Firefox vulnerabilities (USN-5284-1) | Ubuntu Local Security Checks | 1 | ✓ |
| CRITICAL | 9.8 | Ubuntu 20.04 - Ghostscript vulnerability (USN-4445-1) | Ubuntu Local Security Checks | 1 | ✓ |
| CRITICAL | 9.8 | Ubuntu 20.04 LTS / 20.04: Python vulnerability (USN-4973-1) | Ubuntu Local Security Checks | 1 | ✓ |
| CRITICAL | 9.8 | Ubuntu 20.04 LTS / 20.10: Python vulnerability (USN-4940-1) | Ubuntu Local Security Checks | 1 | ✓ |
| CRITICAL | 9.8 | Ubuntu 20.04 LTS / 21.10: Linux kernel vulnerabilities (USN-5208-1) | Ubuntu Local Security Checks | 1 | ✓ |
| CRITICAL | 9.8 | Ubuntu 20.04 LTS - GnuTLS vulnerabilities (USN-5029-1) | Ubuntu Local Security Checks | 1 | ✓ |
| CRITICAL | 9.8 | Ubuntu 20.04 LTS - Python vulnerability (USN-4973-2) | Ubuntu Local Security Checks | 1 | ✓ |
| CRITICAL | 9.1 | Ubuntu 16.04 LTS / 18.04: App vulnerabilities (USN-4449-1) | Ubuntu Local Security Checks | 1 | ✓ |
| CRITICAL | 9.1 | Ubuntu 16.04 LTS / 20.04: NGS vulnerability (USN-4476-1) | Ubuntu Local Security Checks | 1 | ✓ |
| CRITICAL | 9.1 | Ubuntu 16.04 LTS / 18.04 / 20.10: snapbleed vulnerability (USN... | Ubuntu Local Security Checks | 1 | ✓ |
| CRITICAL | 9.1 | Ubuntu 18.04 LTS / 20.04 / 21.01: Pillow vulnerabilities (USN-49... | Ubuntu Local Security Checks | 1 | ✓ |
| CRITICAL | 9.1 | Ubuntu 18.04 LTS / 20.04 / 21.01: Blue2 vulnerability (USN-51... | Ubuntu Local Security Checks | 1 | ✓ |
| CRITICAL | 9.1 | Ubuntu 20.04 LTS / 20.04 / 21.10: cryptography vulnerability (USN-5286-1) | Ubuntu Local Security Checks | 1 | ✓ |

Figure 68: Vulnerability data of Firefox and curl

The list also contains vulnerability data of locally exposed applications as Firefox$^{332}$ or cURL$^{333}$

# ## 7.2.6 Working with Nessus Plugins

By default, Nessus will enable a number of plugins behind-the-scenes, when running a default template. This is certainly useful in many scenarios, we can also fine-tune our options to quickly run a single plugin. We can use this feature to validate a previous finding or to discover all the threats in an environment that are at risk to a specific vulnerability.

For this example, we will set a plugin filter to identify if the DESKTOP is vulnerable to CVE-2021-3156$^{334}$ a locally exploitable vulnerability that allows an unprivileged user to elevate privileges to root.

To leverage the dynamic plugin, we will once again begin with a New Scan.

![](bbox=[0.365, 0.735, 0.635, 0.795])

> $^{332}$(Mozilla, 2022), https://www.mozilla.org/en-US/firefox/news/
$^{333}$(Wikipedia, 2022), https://en.wikipedia.org/wiki/URL
$^{334}$(Tenable, 2021), https://www.tenable.com/cve/CVE-2021-3156

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

189