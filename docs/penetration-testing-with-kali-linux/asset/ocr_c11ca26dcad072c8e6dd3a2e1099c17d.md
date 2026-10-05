# OffSec

Penetration Testing with Kali Linux

version in this, we could also check the source code of the webpage to get the web application and its version number.

```
<div class="copyright">
<a href="http://qdpm.net" target="_blank">qdPM 9.1</a><br /> Copyright &copy;
2022 <a href="http://qdpm.net" target="_blank">qdpm.net</a>
</div>
```

Listing 364 - The version is visible in the source code

The web application and its version is located near the bottom of the source code page. Upon further investigation, we can determine that it is a free-based project management software. 728

With this new discovery, we search Exploit DB for a remote exploit for “qdPM 9.1”, with a couple relevant.

![](bbox=[0.195, 0.355, 0.804, 0.61])

| DB-ID | CVE | Author | Type | Platform | Date |
|---|---|---|---|---|---|
| Verified | | | UPDATED | PHP | 2022 |
| Exploit: 1 | | | | Vulnerable App (?) | |

Figure 234: The exploit details are displayed

Inspecting the latest exploit,729 we determine that it aligns with our search: it is verified, remote, and allows for remote code execution. We will review the exploit and gain a basic understanding of it before executing it.

The exploit requires a username and password for the project management web application. After reviewing the code, we can conclude the username field of the login page is an email address. We were able to find several e-mails, but no exposed passwords. With having working credentials with the web application, the exploit will upload a command shell that we can use to execute commands on the target.

Another method of getting an account password would be to use a list generator on the website. After a list is generated, we can try the list as-is or make changes to create more complex passwords.

> 729 (qdPM, 2022), https://qdpm.net/
729 (Exploit DB, 2022), https://www.exploit-db.com/exploits/50944

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

468