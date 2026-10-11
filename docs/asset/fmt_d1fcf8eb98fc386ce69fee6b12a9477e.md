
关于 Cisco 的安全公告可以通过以下地址获取：`www.cisco.com/security/announcement`。如需订阅官方 Cisco 安全公告列表，请向 `majordomo@cisco.com` 发送邮件，正文为“subscribe-security”。

# 第21 章 安全

第 9 步：向权威部门报告事件。如果事件涉及第三方，您应该向 CERT 报告此事。可以通过传真 `(412) 268-6989` 或发送电子邮件 `cert@cert.org` 与他们联系。请提供尽可能的信息。

可以从 `www.cert.org` 获取标准表格以帮助您唤回记忆。以下是您可能提供的一些最有有用的信息：

- 被攻击机器的名称、硬件类型和操作系统版本
- 事件发生时已安装的补丁列表
- 涉及的远程主机账户列表和 IP 地址
- 如果您知道，远程站点管理员的联系信息
- 相关的日志条目或审计信息

如果您认为之前可能涉及某个未记录的软件问题，您也应该向您的供应商报告该事件。

## 21.16 推荐阅读

BRYANT, WILLIAM. "Designing an Authentication System: a Dialogue in Four Scenes." `web.mit.edu/kerberos/www/dialogue.html`

CERT COORDINATION CENTER. "Intruder Detection Checklist." `www.cert.org/tech_tips/intruder_detection_checklist.html`

CERT COORDINATION CENTER. "UNIX Configuration Guidelines." `www.cert.org/tech_tips/unix_configuration_guidelines.html`

CHESWICK, WILLIAM R., AND STEVEN M. BELLOW. Firewalls and Internet Security, 2nd Edition. Reading, MA; Addison-Wesley. 2000.

CURTIN, MATT, AND MARCUS RANUM. "Internet Firewalls: Frequently Asked Questions." `www.interhack.net/pubs/fwfaq`

FARER, DAN, AND WIETSE VENEMA. "Improving the Security of Your Site by Breaking Into it." 1993. `www.spirit.com/security`

FARROW, R, AND RICHARD POWER. Network Defense article series. 1998–2001. `www.spirit.com/Network`

FRASER, B., Editor. RFC2216: Site Security Security Handbook. `www.rfc-editor.org`.

GARFINKEL, SIMON, AND GENE SPAFFORD. Practical UNIX and Internet Security. Sebastastopol: O'Reilly & Associates. 1996.

KERBY, FRED, ET AL. "SANS Intrusion Detection and Response FAQ." SANS. `www.sans.org/newlook/resources/IDFAQ/ID_FAQ.html`

MANN, SCOTT, AND ELLEN L. MITCHELL. Linux System Security: The Administrator’s Guide to Open Source Security Tools. Upper Saddle River, NJ: Prentice Hall PTR. 2000.

Linux Administration Handbook

MORRIS, ROBERT, AND KEN THOMPSON. "Password Security: A Case History." Communications of the ACM, 22 (11): 594-597, November 1979. Reprinted in UNIX Manager's Manual, 4.3 Berkeley Software Distribution. University of California, Berkeley. April 1986.

PICNARCZYK, KARY, STEVE WEEBER, AND RICHARD FEINGOLD. "UNIX Incident Guide: How to Detect an Intrusion." Computer Incident Advisory Capability, U.S. Department of Energy, 1994. `http://cii.inl.gov/ciac/documents`

RITCHIE, DENNIS M. "On the Security of UNIX." May 1975. Reprinted in UNIX Manager's Manual, 4.3 Berkeley Software Distribution. University of California, Berkeley. April 1986.

SCHNEIER, BRUCE. Applied Cryptography: Protocols, Algorithms, and Source Code in C. New York, NY: Wiley, 1995.

THPSON, KEN. "Reflections on Trusting." in ACM Turing Award Lectures: The First Twenty Years 1960-1985. Reading, MA: ACM Press (Addison-Wesley), 1987.

ZIMMERMANN, PHILIP R. The Official PGP User's Guide. Cambridge: MIT Press, 1995.

SONNENSHEUR, WES, AND TOM YATES. Building Linux and OpenBSD Firewalls. New York, NY: J. Wiley, 2000.

这是一本非常棒的书：它易于阅读，有良好的示例，幽默感十足，总体非常出色。我们对这本书唯一的意见是它反对使用 sudo 获取 root 权限，声称它太难使用且不值得费精力。我们强烈不同意。

## 21.17 练习

**E21.1** 讨论使用 Linux 密码进行 SSH 认证与使用密码和密钥对进行 SSH 认证的强度。如果其中一种比另一种更安全，你是否应该自动要求更安全的认证方式？

**E21.2** `tripwire` 可以识别已更改的文件。

- a) 在你的机器上设置和使用 `tripwire` 需要什么？
- b) `tripwire` 对哪些近期的网络威胁有效？
- c) `tripwire` 对哪些近期的网络威胁无能为力？
- d) 在具有系统物理访问权限的情况下，如何绕过 `tripwire`？
- e) 如果 `tripwire` 说 `/bin/login` 发生了变化，但其大小和修改日期与之前相同，你可以得出什么结论？如果 `sum` 程序对旧新版本给出相同的值又怎样？

**E21.3** SSH 隧道通常是由于流量传输到你没有管理员权限的远程机器的唯一方法。阅读 `ssh` 页面并提供一条将流量从 `localhost` 端口 `113` 隧道到 `mail.remotenetwork.org` 的命令行。你隧道的转发终点也应该是主机 `mail.remotenetwork.org`。

**E21.4** 选择一个近期的安全事件并进行研究。寻找有关该事件的最佳信息来源，并找到适用于你系统的补丁或替代方案。列出你为保护实验室建议的措施。

**E21.5** 在本地管理员组的许可下，安装 `crack`，这是一个搜索弱密码登录的程序。修改 `crack` 的源代码，使其仅输出与弱密码相关的名称，而不是密码本身。在你的本地实验室密码文件上运行 `crack`（你需要 `/etc/shadow` 的访问权限），并查看你破解了多少密码。将自己的密码设置为字典单词，并让 `crack` 处理你在 `/etc/shadow` 中的条目。`crack` 找到它需要多长时间？尝试其他模式（大写字母、单词后的数字、单字母等）以查看 `crack` 到底有多聪明。

# Linux 管理手册

到网络。Web 托管服务器不仅提供原始的网页（HTML）页面，还提供如 FTP、SSL 以及流音频或视频等支持服务。

如今，我们有多种 Web 托管平台可以选择，并且开发了许多专门的 Web 服务器来满足特定市场渠道的需求。微软曾经和未来的旗舰产品 Windows 已经广泛作为一种 Web 托管平台进行营销。但对于那些追求极端可靠性、可维护性、安全性和性能的人来说，Linux 在 Web 托管领域仍然遥遥领先。

行业内发表了无数文章来探讨“哪种 Web 托管平台最好”的问题，通常将 Windows 和 Linux 置于对决台的两角。尽管这些喧哗类似于“填充物更少！味道更佳！”的争论，但 Linux 成为生产环境网站更好的选择是有理由的。

Linux 最主要的优势是它的可维护性和性能。Linux 从之初就被设计为多用户、交互式操作系统。在 Linux 机器上，一名管理员可以维护数据库，而另一个人维护 I/O 性能，第三个人则维护 Web 服务器。在 Windows 环境下，控制台的人（无论是物理还是远程，使用 PC-Anywhere 等工具或 Windows XP 安装的软件）是唯一可以执行关键管理任务的人。与 Windows 相比，优秀的管理员可以调优 Linux，使其在相同硬件上的运行速度至少是 Windows 的两倍。

## 22.2 Web 托管基础

托管网站与提供任何其他网络服务并没有本质区别。万维网的基础是超文本传输协议（HTTP），这是一种基于 TCP 的简单协议，用于格式化、传输和链接包含多种媒体类型的文档，包括文本、图片、声音、动画和视频。HTTP 的行为类似于用于互联网的其他客户端/服务器协议，例如用于电子邮件的 SMTP 和用于文件传输的 FTP。

Web 服务器简单来说就是一个配置为响应 HTTP 请求的系统。要将你的 Linux 系统转换为 Web 托管平台，你需要安装一个监听 TCP 80 端口（HTTP 标准端口）连接的守护进程，它接受文档请求并将其传输给请求用户。

Netscape、Opera 和 Internet Explorer 等浏览器探索远程服务器并代表用户发出请求。获取的文档可能包含指向其他文档的超链接（链接），这些文档可能位于用户最初连接的服务器上，也可能不在。由于 HTTP 协议是定义良好的标准，运行在任何操作系统或架构上的客户端都可以连接到任何 HTTP 服务器。这种平台独立性加上 Linux 透明地将用户从一个服务器切换到另一个服务器的能力，促进了它的巨大成功。

# 第 22 章 Web 托管与互联网服务器

然而，在纯 HTTP 之外还有精彩。现在已经定义了许多增强协议，用于提供从加密到视频流的所有功能。这些额外服务通常由单独的守护进程管理，即使由同一物理服务器提供。例如，最流行的增强服务之一是安全 HTTP，即 HTTPS。它由一个理解安全套字层（SSL）协议的守护进程处理，并监听 TCP 443 端口。

## 统一资源定位符

统一资源定位符（URL）是互联网上对象或服务的指针。它通过五个组件描述了如何访问对象：

- 协议或应用程序
- 主机名
- TCP/IP 端口（可选）
- 目录（可选）
- 文件名（大小敏感；通常以 ".htm" 或 ".html" 结尾）

图 A 展示了一个典型的 URL 及其组成部分。

# 图 A URL 的组成部分

![](img/4baff4a9c0bcfa44e45d38f4bdc1a0e2_732_0.png)

图 22.1 显示了 URL 中常用的使用的协议。

# 表 22.1 URL 协议

| 协议 | 功能 | 示例 |
|---|---|---|
| http | 通过 HTTP 访问远程文件 | http://admin.com/index.html |
| https | 通过 HTTP/SSL 访问远程文件 | https://admin.com/order.shtml |
| ftp | 通过 FTP 访问远程文件 | ftp://ftp.org/adduser.tar.gz |
| mailto | 向指定地址发送电子邮件 | mailto:sa-book@admin.com |
| news | 访问 Usenet 新组 | news:alt.cooking |
| telnet | 登录远程计算机 | telnet:spot.acme |
| ld | 访问 LDAP 目录服务 | ldap://ldap.bigfoot.com:389/cn=Herb |
| file | 访问本地文件（无网络） | file:///etc/syslog conf |

# HTTP 工作原理

HTTP 是让万维网真正运行的协议，令人们惊讶的是，它是一种极其基础、无状态的客户端/服务器协议。在 HTTP 范式中，连接的启动者总是客户端（通常是浏览器）。客户端向服务器请求特定 URL 的“内容”。服务器响应一串数据或某种错误消息。在 HTTP 0.9 和 1.0 版本中，连接会被关闭；在 HTTP 1.1 中，客户端可以继续请求另一个对象。

由于 HTTP 如此简单，你可以通过 `telnet` 轻松地让自己变成浏览器。由于 HTTP 服务的标准端口是 80 端口，你直接 `telnet` 到你选择的 Web 服务器的该端口。你可以颁发 HTTP 命令。最常用的命令是 `GET`，它请求文档的内容。通常，`/GET /` 是你想要的，它请求你连接的任何服务器的文档根（通常是主页）。HTTP 是大小敏感的，所以确保用大写字母输入命令。

```
telnet localhost 80
Trying 127.0.0.1...
Connected to localhost.astrust.com.
Escape character is ''
GET /
<此处显示你的 index.html 文件内容>
Connection closed by foreign host.
```

# CGI 脚本：动态生成内容

除了提供静态文档外，HTTP 服务器还可以为用户提供动态创建的内容。例如，如果你想为访问你网站的用户提供当前的时间和温度，你可能让 HTTP 服务器执行一个脚本来获取这些信息。这种让外行人大惊的技巧通常通过通用网关接口（CGI）实现。

CGI 不是一种编程语言，而是一种允许 HTTP 服务器与其他程序交换信息的规范。大多数情况下，CGI 脚本是 Perl、Python 或 C 程序，这些程序是专门为与 HTTP 服务器建立接口而编写的。事实上，几乎任何可以与 HTTP 服务器建立接口的编程语言都可以。

# 第 22 章 Web 托管与互联网服务器

697

关于 CGI 安全处理的良好来源，请参见 `w3.org/Security/faq`

# 负载均衡

很难预测单台服务器能够处理多少命中（对象请求）或页面访问（所有页面请求）。服务器的准确容量取决于操作系统、系统调优程度以及网站的构建（是纯 HTML 页面，还是有数据库调用？）。只有在实际硬件上运行你的网站进行直接基准测试才能回答“有多少命中？”在任何情况下都不应相信系统供应商提供的数字。

如此，与其关注单服务器命中数，更好的关注参数是可扩展性。确保你和 Web 设计团队有一个计划，允许将流量网站的负载分布到多台服务器上。扩展流量简单方法是使用商业负载均衡硬件，例如 F5 Networks 的 Big-IP Controller 或 Alteon ACEswitch（现由 Nortel 销售）。这些产品根据可配置参数（如服务器响应时间和可用性）分配工作。负载均衡为你的网络增加了性能和冗余——不要离开它。

## 2.3 HTTP 服务器安装

安装和维护 Web 服务器很容易！Web 服务在复杂性和管理难度方面低于电子邮件和 DNS。

# 选择服务器

Linux 有许多出色的 HTTP 服务器可用，但你可能会从 Apache 服务器开始。它是 Red Hat、SuSE 和 Debian 系统的默认 Web 服务器，并以其灵活性性能在业内闻名。截至 2001 年 12 月，互联网上 56.5% 的 Web 服务器运行 Apache。698 页的图 B 显示了随时间变化的趋势。

Apache HTTP 服务器“免费给好人家”，完整的源代码可以从 Apache 组网站 `www.apache.org` 获取。不那么冒险的人可能想要安装 Linux 发行版自带的仅二进制 Apache 软件包（但可能它已经安装在你的系统上了。）

- 1. Apache 组是由几个人组成的，他们为 1993 年“早期”流行的 Web 服务器 NCSA httpd 提供了补丁文件。最终结果是一个“补丁式”的服务器。呵呵

## 附录 B 截至2001年12月的Web服务器市场占份额（所有域名） ^a

![](img/4baff4a9c0bcfa44e45d38f4bdc1a0e2_735_0.png)

^a. 感谢 Netcraft 提供。请访问 `www.netcraft.com` 调查以获取最新版本。

你可以在 `compare.internet.com` 网站找到所有当前可用 HTTP 服务器的有用对比。以下是你在选择时可能想要考虑的某些因素：

- 健壮性
- 性能
- 更新和错误修复的及时效性
- 源代码的可用性
- 成本
- 访问控制与安全
- 作为代理的能力
- 处理加密的能力

## 安装 Apache

如果你决定下载源代码并自行编译，你需要执行发行版中包含的 `configure` 脚本。该脚本会自动检测你正在使用的系统类型并设置相应的 `makefile`。你将需要使用 `--prefix` 选项来指定 Apache 服务器位于你目录树的何位置。例如：

```bash
