
# OffSec

Penetration Testing with Kali Linux

![](img/336d6ea891e7464f18ad64426619ced4_122_0.png)

Figure 22: File Operator in GitHub Search

Our search found only one file - xampp.users. This is nevertheless interesting because XAMPP is a web application development environment. Let's check the contents of the file.

> 227 (Apache Friends, 2022), https://www.apachefriends.org/index.html

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.
123

# OffSec Penetration Testing with Kali Linux

![](img/336d6ea891e7464f18ad64426619ced4_123_0.png)

Figure 23: GitHub Search Results

This file appears to contain a username and password hash,$^{228}$ which could be very useful if we begin our active attack phase. Let's add it to our notes.

228 (Wikipedia, 2022) https://en.wikipedia.org/wiki/Cryptographic_hash_function#Password_verification

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

# OffSec Penetration Testing with Kali Linux

![](img/336d6ea891e7464f18ad64426619ced4_124_0.png)

Figure 24: xampp.users File Content

This manual approach will work best on small repos. For larger repos, we can use several tools to help automate some of the searching, such as Gitrob$^{229}$ and Gitleaks$^{^{230}$. Most of these tools require an access token$^{2231}$ to use the source-code provider's API.

The following screenshot shows an example of Gleaks finding an AWS access key ID$^{2232}$ in a file.

229 (Michael Henriksen, 2018), https://github.com/michenriksen/gitrob
230 (Zachary Rice, 2022), https://github.com/zricetheaz/gitleaks
231 (GitHub, 2022), https://help.github.com/en/articles/creating-a-personal-token-for-the-command-line
232 (Amazon Web Services, 2022), https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved. 125

# OffSec

Penetration Testing with Kali Linux

```
kali@kali:~$ gitleaks-linux-amd64 -v -r=https://github.com/
[INFO] 2019-10-07T11:13:00Z cloning https://github.com/
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Compressing objects: 100% (6/6), done.
Total 30 (0 delta, 0 delta), pack-sequence 22
{
  "line": "Access key id: A"
  "commit": "",
  "offset": "",
  "rule": "AWS Client ID",
  "info": "(AKIA[A-Z0-9]{16}|AGIA|AGPA|AGARDA|ANPA|ANVA|ASIA) regex match",
  "commit": "Merge pull request #1 from Update as:",
  "author": "",
  "email": "",
  "file": "aws",
  "repo": "aws",
  "date": "2018-12-13T22:52:08-00:00",
  "tags": "key,aws",
  "severity": ""
}
```

![](img/336d6ea891e7464f18ad64426619ced4_125_0.png)

These credentials allow unlimited access to the same AWS account and could lead to a compromise of any cloud service managed by this identity.

> Tools that search through source code for secrets, like Gitrob or Gitleaks, generally rely on regular expressions or entropy$^{223}$-based detections to identify potentially useful information. Entropy-based detection attempts to find strings that are randomly generated. The idea is that a long string of random characters and numbers is probably a password. No matter how a tool searches for secrets, no tool will miss things that a manual inspection might find.

# 6.2.5 Shodan

As we gather information on our target, it is important to remember that traditional websites are just one part of the internet.

Shodan$^{224}$ is a search engine that crawls devices connected to the internet, including the servers that run websites, but also devices like routers and IoT$^{225}$ devices.

To put it another way, Google and other search engines for web server content, while Shodan searches for internet-connected devices, interacts with them, and displays information about them.

Although Shodan is not required to complete any material in this Module or labs, it's worth exploring bit. Before using Shodan we must register a free account, which provides limited access.

223 (Wikipedia, 2022), https://en.wikipedia.org/Password_strength
224 (Shodan, 2022), https://www.shodan.io/
225 (Wikipedia, 2022), https://en.wikipedia.org/wiki/things

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved. 126

# OffSec Penetration Testing with Kali Linux

Let's start by using Shodan for hostname.megacorp.com.![](img/336d6ea891e7464f18ad64426619ced4_126_0.png)

| TOP PORTS | |
| --- | --- |
| 22 | 4 |
| 53 | 2 |
| 80 | |
| 443 | 1 |

| TOP PRODUCTS | |
| --- | --- |
| OpenSSH | 4 |
| Apache httpd | 2 |

![](img/336d6ea891e7464f18ad64426619ced4_126_1.png)

149.56.244.87
www.megacorp.com
```
HTTP/1.1 200 OK
Date: Sat, 22 Oct 2022 15:11:47 GMT
Server: Apache/2.4.41 (Ubuntu)
Last-Modified: Mon, 18 Nov 2019 15:14:01 GMT
Accept-Encoding: gzip
Connection: close
Content-Type: text/html
SSH-2.0-OpenSSH_8.2p1 Ubuntu-4
Key exchange algorithms: diffie-hellman-group-exchange-sha256
MAC algorithms: aes256-gcm@openssh.com,aes128-gcm@openssh.com
Encryption algorithms: aes256-ctr@openssh.com,aes128-ctr@openssh.com```

In this case, Shodan lists the IPs, services, and banner. All of this is gathered passively, interacting with the client's web site. This information gives us a snapshot of your target's footprint. For example, there are four servers running SSH. We can drill down into our results by clicking on SSH under the left pane.

Figure 26: Searching MegaCorp One's domain with Shodan

# OffSec Penetration Testing with Kali Linux

SHODAN Explore hostname:megacorp.com "22"

| TOP PORTS | |
| --- | --- |
| 22 | 4 |
| 53 | 2 |
| 80 | |
| 443 | 1 |

| TOP PRODUCTS | |
| --- | --- |
| OpenSSH | 4 |
| Apache httpd | 2 |

149.56.244.87
www.megacorp.com
Running from:
Canada, Montreal

SSH-2.0-OpenSSH_7.2p2 Ubuntu-4ubuntu.8
Key type: ssh-rsa
Key: AAAAB3NzaC1yc2EAAAAAAEQAAAAABAQDC5v69677721222212211111111111111111111111111111111111111111212222222222222222222222222222222222222222222222//2222...

51.222.39.63
www.megacorp.com
Running from:
Canada, Montreal

SSH-2.0-OpenSSH_7.2p2 Ubuntu-4ubuntu.8
Key type: ssh-rsa
Key: AAAAB3NzaC1yc2EAAAAAAEQAAAAABAQDC5v6967772122221221111111111111111111111111111111111111111112122222222222222222222222222222222222222222222222//2222...

Figure 27: MegaCorp One servers running SSH

Based on Shodan's results, we know exactly which version of OpenSSH is running on each. If we click on an IP address, we can retrieve a summary of the host.

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.
128

# OffSec Penetration Testing with Kali Linux

149.56.244.87

![](img/336d6ea891e7464f18ad64426619ced4_128_0.png)

| General Information | |
| --- | --- |
| Hostname | megacorp.com |
| Domain | |
| Country | Canada |
| Organization | OWASP Hosting Inc |
| ISP | OWASP |
| ASN | AS151678

# Web Technologies

# Vulnerabilities

CVE-2019-9513: In HTTP/2 implementations before version 1.1.1, a failure to perform server-side certificate validation with TLS-encrypted connections could lead to bypass attacks.

CVE-2020-19173: In Apache HTTP Server versions 2.4.48, a buffer overflow in mod_proxy module could lead to remote code execution.

CVE-2021-41773: In Apache HTTP Server 2.4.49, a path traversal and file read vulnerability allowed attackers to access files outside the document root.

Figure 28: Shodan Summary

We review ports, services, and technologies used by the server on this page. Shodan may also reveal if there are published vulnerabilities for any of the identified services or technologies running on the same host.

# 6.2.6 Security Headers and SSL/TLS

There are several other websites that we can use to gather information about a website or domain's security posture. Some of these blur the line between passive and active information gathering, but the key point for our purposes is that third-party is initiating scans or checks.

One such site, SecurityHeaders,$^{236}$ will analyze HTTP response headers and provide basic analysis of the target site's security posture. We can use this to get an idea of an organization's coding and security practices based on the results.

Let's scan www.megacorpone.com and check the results.

> 236 (Scott Helme, 2022), https://securityheaders.com/
