
在入侵者发出此命令并输入其账户或账户密码后，组织网络与其家中之间将建立一个安全隧道。入侵者可以使用 `OpenSSH` 创建一个从组织网络通往其家中的安全隧道。考虑以下情况：已接入组织无线网络的入侵者在自己的 PDA 上启动了以下命令：

## HPING2

`Hping2` 是一种用于发送任意数据包的工具。入侵者可以使用它来测试防火墙规则。`Hping2` 的手册可以在 `http://www.manpage` 获取。下图显示了 `Hping2` 带有 SYN+ACK 数据包在 Zaurus 上的运行。

| hping 2 output |
|---|
| start at: 0 0 |
|sent|received|dropped|lost|packet loss|round-trip min|avg|max|stddev|
|---|---|---|---|---|---|---|---|---|
|0|0|0|0|0%|0.000|0.000|0.000|0.000|

![](img/17cb132e62949dc7f5e0eadf90c71f51_235_0.png)

## 182 第 III 部分：特别主题

## VNC SERVER

`VNC`（远程桌面）是一种允许用户访问另一主机桌面的软件。Zaurus 端口可以在 `http://sdystems.com/download` 获取。经常，用户会错误地为 `VNC` 服务器配置弱密码。接入组织内网的入侵者可以使用 `VNC` 服务器主机（见图 12-1）。

![](img/17cb132e62949dc7f5e0eadf90c71f51_236_0.png)

## KEYPEBBLE VNC VIEWER

非常经常，用户会为 `VNC` 服务器配置弱密码。接入无线网络的入侵者可以使用 `VNC` 查看器（如下所示）。其中一种查看器 `Keypebble VNC` 查看器可以在 `http://killefiz.de/zaurus/showdetail.php?app=186` 获取。

![](img/17cb132e62949dc7f5e0eadf90c71f51_237_0.png)

## SMBMOUNT

`SMBmount` 工具允许用户挂载 Samba 共享。经常，用户会为 Samba 共享配置弱密码。入侵者可以使用 `SMBmount` 工具访问此类共享。（有关 Samba 配置的详细信息，请参见第 4 章。）Zaurus 版本的 `SMBmount` 工具可以在 `http://www.dasgehtnicht.de/zaurus.html` 获取。

## TCPDUMP

`Tcpdump` 是一种流行的网络分析程序，可用于嗅探网段上的敏感数据。网络管理员也使用 `Tcpdump` 和其他网络分析程序进行故障排除。Zaurus 版本的 `Tcpdump` 可以在 `http://www.sklogicsoftware.com/znetmeter/tcpdump_zaurus` 下载。

## WGET

`Wget` 是一个使用 HTTP、HTTPS 和 FTP 协议下载文件的工具。它具有许多实用功能，包括递归下载网站文件。接入组织无线网络的入侵者可以使用 `Wget` 快速镜像组织的内网网站。Zaurus 默认安装了 `Wget`。

## ZETHERALE

`Zthereal` 是流行的 GUI 网络分析器 `Ethereal` 的移植。`Zthereal` 的二进制文件和截图可以在 `http://www.cartel-info.fr/pbiondi/zaurus/zethereal.html` 获取。关于 `Ethereal` 的详细信息和文档可以在 `http://www.ethereal.com/` 找到。

## ZNESSUS

`zNessus` 工具是 `Nessus` GUI 客户端的 Zaurus 版本。截图和二进制文件可以在 `http://znessus.sourceforge.net/` 获取。`zNessus` 可用于远程配置并启动漏洞检查

# 第 12 章：使用 Sharp Zaurus PDA 185 进行破解

`Nessus` 服务器。关于 `Nessus` 扫描器的更多信息，请参阅第 4 章和第 11 章。

`zNessus` 客户端要求 `Nessus` 服务器配置为支持非加密通信（默认禁用）。如果你决定禁用 `Nessus` 服务器上的加密，请务必阻止所有流向 `Nessus` 端口（默认 `1241`）的入站流量。使用 `OpenSSH` 客户端连接到你的 `Nessus` 服务器主机，以便安全地隧道化你的 `zNessus` 流量。

### MTR

`MTR`（Matt's TraceRoute，见下图）是一个将 `ping` 和 `traceroute` 程序的功能合并到的单一程序。（关于 `ping` 和 `traceroute` 的更多信息，请参阅第 2 章。）适用于 Zaurus 的 `MTR` 端口二进制程序包可以从 `http://psifertex.com/zaurus/mtr_0.51_arm.ipk` 下载。

![](img/17cb132e62949dc7f5e0eadf90c71f51_239_0.png)

### DIG

`dig` 工具可用于查询 DNS 服务器以获取如 MX 记录和服务器版本信息等内容，并执行其他 DNS 查找查询。适用于 Zaurus 的 `dig` 可以在 `http://killefiz.de/zaurus/showdetail.php?app=362` 获取。

### PERL

许多安全工具（如 `Nikto` 和 `Whisker` 漏洞扫描器）都是使用 `Perl` 语言编写的。由于 `Perl` 是一种解释型语言，因此不需要重新编译已有的 `Perl` 脚本即可在 Zaurus 上运行它们。适用于 Zaurus 的 `Perl` 可以在 `http://zaurus.frontgarden.net/perl.html` 获取。

### ZAURUS 的在线资源

Zaurus PDA 在 Linux 社区中受到了极大的推崇。除了本章讨论的工具外，每天都有新的工具被创建和移植。下表中的提供了软件资源以及常见问题解答（FAQs）和社区论坛的链接。

| 说明 | URL |
| :--- | :--- |
| Zaurus 软件索引 | http://killefiz.de/zaurus/ |
| Zaurus DevNet 论坛 | http://www.zaurus.com/dev/board/ |
| Zaurus Zone | http://www.zauruszone.com/ |
| Sharp 开发者 | http://www.zaurus.com/dev/ |
| 非官方 Sharp Zaurus SL-5500 FAQ | http://www.newbreedssoftware.com/zaurus-faq/ |
| ZaurusSoft 数据库 | http://www.zaurussoft.com/ |
| OpenZaurus 替代 ROMs | http://openzaurus.org/ |

### 总结

在本章中，你查看了可以在 Zaurus PDA 上使用的各种安全工具。用于执行无线网络发现、嗅探和扫描的工具现在已适用于 Zaurus。此外，像 `Perl` 这样的脚本语言也已移植到 Zaurus，允许用户使用 `Perl` 语言运行安全工具。如此庞的安全工具库的可用性结合 Linux 操作系统的灵活性，使得 Zaurus PDA 成为一个强大的工具，可用于对目标网络执行攻击和渗透测试。

### 索引

符号与数字
- `PATH` 环境变量中的 `""`
- 利用漏洞植入木马，114–115
- 用于主机加固的移除，132
- `#`（井号），用于从 `\inet` 禁用 FTP，134
- `0`，将本地账户 `uds` 修改为，123–124
- `127.0.0.1`（环回接口），无限制
- 端口上的流量，112

# 190 黑客技巧 Linux 与 Unix 便携参考指南

### 索引

- `Apache` (HTTP 和 HTTPS), 139–140
- `BIND` (DNS), 138–139

# 194 黑客破解版 Linux 与 Unix 安全便携参考指南

通过句柄查询，13–14
通过 IP 地址或网络块查询，13
`RRRs`（区域互联网注册机构）的使用，12

# 198 HackNodes Linux 和 Unix 安全便携参考指南

- `wheel` 组，限制许多用户对 `setuid` 程序的访问，150

# 国际联系信息

澳大利亚
`McGraw-Hill Book Company Australia Pty. Ltd.`
电话 +61-2-9800-1800

# 前线安全

![](img/17cb132e62949dc7f5e0eadf90c71f51_254_0)
![](img/17cb132e62949dc7f5e0eadf90c71f51_254_1)
![](img/17cb132e62949dc7f5e0eadf90c71f51_254_2)

`HackNotes™Linux/Unix` 安全便携参考
作者：Nitesh Dhanjani
ISBN: 0-07-222786-9

# 查看 Osborne 的所有黑客书籍

![](img/17cb132e62949dc7f5e0eadf90c71f51_255_0)

`Hacking Exposed JEE & Java`
作者：A. TAYLOR, B. BUEGE, R. LAYMAN
0-07-222565-3
价格 $49.99
