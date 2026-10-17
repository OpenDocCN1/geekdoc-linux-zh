
```bash
[root]@chiriqui /root]# nmap -sFUR localhost
Starting nmap V. 2.38ETAG by Fyodor (fyodor@dnp.com),
www.insecure.org/nmap/

Interesting ports on localhost (127.0.0.1):
```

| Port | State | Protocol | Service (RPC) |
| :--- | :--- | :--- | :--- |
| 21 | open | tcp | ftp |
| 22 | open | tcp | ssh |
| 25 | open | tcp | smtp |
| 67 | open | udp | bootps |
| 80 | open | tcp | http |
| 110 | open | tcp | sunrpc |
| 111 | open | udp | sunrpc |
| 111 | open | tcp | sunrpc |
| 177 | open | udp | xdmcp |
| 514 | open | udp | syslog |
| 901 | open | tcp | unknown |
| 3306 | open | tcp | mysql |
| 6000 | open | tcp | X11 |

```bash
Nmap run completed -- 1 IP address (1 host up) scanned in 3 seconds
```

现在，在列表 `25-6` 中出现了几个以前没看到的端口——你必须单独扫描的 `UDP` 端口。按端口数字列出，显示了所有开放端口，包括 `TCP` 和 `UDP`。顺便说一下，端口 `901` 是（Samba Web 管理工具）。在同一以太网网段的另一个主机上进行相同的扫描（全 `64k TCP/UDP/RCP`）花费了 `1586` 秒，或超过 `26` 分钟。

## nmap 对比 netstat

你可能会疑惑为什么有 `netstat` 时还要使用 `nmap`。使用 `netstat -an` 会显示开放端口，但不会告诉你是背后是什么。两者的真实区别在于，`nmap` 可以从外部运行，而 `netstat` 仅用于本地机器。实际上，注意到能够 `ping` 并不是什么大事。你尽管可以使用 `traceroute`。

等等，我并不太担心你有一个系统在线这件事。重要的是暴露在互联网上的服务漏洞，而且 `ICMP` 并不有助于入侵系统。更重要的是，你对扫描自己的主机时可以尝试哪些方法有了思路，并可以观察 `Courtney` 或其他扫描检测程序是否捕获了扫描或被其欺骗。

## 第 25 章：使用网络监控工具

## 第 26 章：发现系统安全信息

### 在本章中

- 安全信息
- “官方”网站
- 可疑的网站

本章介绍了检测方面、其能力和局限性，以及扫描方面。首先你查看了它是如何工作的。你查看了变量以及它们是如何更改的。你查看了 `nmap`，最流行的扫描器之一。你还看到了如何启用选项，这将允许 `nmap` 不被检测。

## 总结

实际上，我并不太担心……

但有一点是肯定的——安全到此结束。发现了漏洞。在写本书期间，我发现了一种新的扫描数据包的方法。以前，扫描软件会寻找开放端口以发送 `SYN-ACK` 消息，希望得到 `RST` 响应以指示主机正在监听。但这取决于主机是否在监听。如果主机丢弃了所有数据包（没有提供服务，而是丢弃了 `ICMP` 请求数据包和从不返回连接请求的 `TCP` 数据包），使得它看起来像没有在线？所以聪明的人决定向系统发送 `ICMP` 响应数据包。虽然你可能有 `ICMP` 请求被拦截（丢弃），但你可能并没有丢弃 `ICMP` 响应。如果你这样做了，你就无法使用它来 `ping` 出。

## 查找安全信息

你可以选择你想要接收安全信息的方式。外界的信息确实非常多。在其中进行筛选或选择负责任的网站通常是最困难的部分。这里列出了几个非常有价值的邮件列表。此外，还列出了许多其他网站，其性质有的良好，也有可疑，且这些网站通常也有自己的邮件列表。

取决于你想要获取多少信息、频率如何，以及你是否介意收到冗余信息，你可以订阅其中几个。所有仅提供信息的安全列表都不是高频率的，而且收到两次关于特定漏洞的信息也比完全收不到信息要好。

### 邮件列表

你可能想要订阅的第一个邮件列表是处理你特定分发版本的安全列表。以本书提供的分发版 `Caldera Systems OpenLinux` 为例，有一个名为 `Caldera Advisory`（`Caldera` 告）的安全邮件列表。你可以通过访问 `Caldera` 网站（`www.caldera.com`）来选择订阅。当 `Caldera Systems` 发现影响其任何官方分发程序的安全问题时，将发送电子邮件。公告将包含指向修复后的 `RPM` 的链接（如果可用）或提供变通解决方案。这不包括由第三方提供的程序，例如 "contrib" 目录中的程序。如果不订阅，或者你只想查看之前的公告，可以在 `Caldera Systems` 网站上查看。请访问 `http://www.calderasystems.com/news/security/index.html` 了解更多信息。

另一个值得订阅的列表是 `CERT Advisory` 列表。`CERT`（计算机应急响应小组）每当发现可能危及系统的漏洞应用程序时，就会向订阅者发送电子邮件。公告通常会详细解释特定漏洞，为需要该漏洞应用程序的用户提供临时的变通方案，并提供永久解决方案的建议。公告提供了详尽的细节，供你判断自己是否存在漏洞，并评估你是否面临风险。并不是所有漏洞都会增加网站的风险。虽然这些公告充满了技术术语，但它们直击重点。如果你不确定，请遵循建议操作。更多信息可以在 `http://www.cert.org/` 找到。

还有许多通用的安全相关简报。其中一个名为 `SANS NewsBites`，是一份《每周安全新闻概述》。这封每周邮件包含了全球范围内计算机安全相关的各种条目。你可以通过向 `autosans@sans.org` 发送邮件，主题为 `Subscribe NewsBites` 来订阅。

## 第 26 章：查找保持系统安全的信息

### 安全相关网站

如今有很多安全相关的网站。许多网站是近期信息的便捷存储库，并包含指向其他网站的指针。另一些网站则拥有原创内容。还有一些并非特别相关的安全的网站，在其所有者意识到安全信息时也会发布。

例如，`http://slashdot.org` 和 `http://freshmeat.net`（对于一个“极客”新闻网站，后者是一个包含有关新发布软件包或软件升级信息的网站）都会发布有关漏洞的信息。这两个网站都没有发布详细信息，但每个网站都发布了链接，通常是指向特定的 `CERT` 告。列表 `26-1` 显示了 `CERT` 公告的内容。如果你们遵循了第 `21` 章的说明并包含了 `RSAref2` 库，你们会觉得有必要对此公告感兴趣。

`CERT` 公告摘要：`rsfare2` 库包含一个漏洞，可以允许恶意代码从任何使用 `rsfare2` 库编译的服务中运行。该代码将以运行服务的用户（通常是 `root`）的身份运行。要消除该漏洞，你应该对 `rsfare2` 库应用补丁（列在公告消息中）并重新编译该库，同时重新编译所有使用 `rsfare2` 库的应用程序。补丁文件可以通过 `http://www.cert.org/advisories/CA-99-15/rsa-patch.txt` 获取。

### 列表 26-1：CERT 公告示例

主题：`CERT Advisory CA-99-15 - SSH 守护和 RSFARE2 库中的缓冲区溢出`

日期：`Mon, 13 Dec 1999 18:49:47 -0500`
发件人：`CERT Advisory cert-advisory@cert.org`
回复：`cert-advisory-request@cert.org`
组织：`CERT(sm) Coordination Center - +1 412-268-7090`
收件人：`cert-advisory@coal.cert.org`

```
-----BEGIN SIGNED MESSAGE -----

Hash: SHA1

CERT Advisory CA-99-15 Buffer Overflows in SSH Daemon and RSFARE2 Library

原始发布日期：1999年12月13日

最后修订 -

来源：CERT/CC

完整的修订历史位于文件末尾。

受影响的系统

* 运行某些版本 sshd 的系统

* 使用 RSFARE2 产品的系统（例如，某些启用 SSL 的 Web 服务器）
```
