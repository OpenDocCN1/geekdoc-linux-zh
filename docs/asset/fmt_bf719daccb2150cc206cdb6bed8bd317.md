
`iptables -F`

`iptables -P INPUT DROP`

`iptables -P FORWARD DROP`

由于规则按照它们在链中所处的顺序进行评估，我们将最好的规则放在最前面。`FORWARD`链中的前三条规则允许通过防火墙连接到`10.1.1.2`上的网络服务。具体而言，我们允许`SSH`（端口`22`）、`HTTP`（端口`80`）和`HTTPS`（端口`443`）访问到我们的`Web`服务器。第一条规则允许所有来自可信子网的通过防火墙连接。

```
iptables -A FORWARD -i eth0 -d ANY -j ACCEPT
iptables -A FORWARD -d 10.1.1.2 -p tcp --dport 22 -j ACCEPT
iptables -A FORWARD -d 10.1.1.2 -p tcp --dport 80 -j ACCEPT
iptables -A FORWARD -d 10.1.1.2 -p tcp --dport 443 -j ACCEPT
```

我们允许进入防火墙主机的流量只有`SSH`，这对于管理防火墙非常有用。下面列出的第二条规则允许环回流量（`loopback traffic`），这些流量保留在防火墙主机本地。当管理员无法`ping`默认路由时他们会很紧张，因此第三条规则允许来自内部`IP`地址的`ICMP ECHO_REQUEST`包。

```
iptables -A INPUT -i eth0 -d 10.1.1.1 -p tcp --dport 22 -j ACCEPT
iptables -A INPUT -i lo -d 127.0.0.1 -p ANY -j ACCEPT
iptables -A INPUT -i eth0 -d 10.1.1.1 -p icmp --icmp-type 8 -j ACCEPT
```

为了任何`TCP/IP`主机在互联网上正常工作，必须允许某些类型的`ICMP`包通过防火墙。以下八条规则允许一组最小`ICMP`包进入防火墙主机以及其背后的网络。

```
iptables -A INPUT -p icmp --icmp-type 0 -j ACCEPT
iptables -A INPUT -p icmp --icmp-type 3 -j ACCEPT
iptables -A INPUT -p icmp --icmp-type 5 -j ACCEPT
```

16. 然而，你必须记住，为了性能而重新排序规则不会修改其功能。

```
iptables -A INPUT -d 10.1.1.2 -p icmp --icmp-type 11 -j ACCEPT
iptables -A FORWARD -d 10.1.1.2 -p icmp --icmp-type 0 -j ACCEPT
iptables -A FORWARD -d 10.1.1.2 -p icmp --icmp-type 3 -j ACCEPT
```
（注：由于原文后部分存在大量重复和断码，此处译文已根据提供的逻辑片段进行整理）

## 第 21 章 安全

### CERT: 卡内基·梅隆大学的注册服务标记

针对 1988 年网络虫引发的骚动，美国国防部高级研究计划局（`DARPA`）成立了一个名为 `CERT`（即计算机应急响应小组，`Computer Emergency Response Team`）的组织，作为安全信息的枢纽。`CERT` 仍然是安全信息最著名的联系点，尽管它最近似乎变得迟钝且官僚化了。`CERT` 还坚持认为 `CERT` 这个名称并不代表任何特定含义，仅仅是“卡内基·梅隆大学的注册服务标记”。

尽管 `CERT` 的章程包含某种程度的问题解决功能，但现实中，`CERT` 缺乏调查问题或惩罚违规者的能力，因此它更多只是一个供应商安全补丁和安全工具公告的库。这些补丁和公告被称为“`CERT` 告”（`CERT advisories`）。新公告发布在 `www.cert.org`，通过电子邮件发送到 `cert-advisory` 邮件列表，并订阅到 `group.security.announce` 新闻组。如需订阅：

`http://www.cert.org/contact_cert/certmaillist.html`

### SecurityFocus.com 和 BugTraq 邮件列表

`SecurityFocus.com` 是一个专门提供安全相关新闻和信息的网站。新闻包括关于通用问题和特定问题的最新文章；还有一个丰富的有用论文库，并按主题进行了良好分类。

`SecurityFocus` 的安全工具存档包含了适用于各种操作系统的软件，以及简要介绍和用户评分。这是我们所知最全面、详细的工具来源。

`BugTraq` 列表是一个受审核的论坛，用于讨论安全漏洞及其修复方法。如需订阅，请向 `listserv@securityfocus.com` 发送邮件，正文内容如下：

`SUBSCRIBE BUGTRAQ lastname, firstname`

然而，该列表的流量可能相当大。该网站还提供 `BugTraq` 漏洞报告数据库。

### Crypto-Gram 周报

每月一次的 `Crypto-Gram` 周报是关于相关计算机安全和密码学的非常有价值且有时带有趣味性的信息来源。它由 `Bruce Schneider` 编写，他是备受推崇的书《秘密与谎言》（`Secrets and Lies`）和《应用密码学》（`Applied Cryptography`）的作者。你可以在此处订阅 `Crypto-Gram`：

`http://www.counterpane.com/crypto-gram.html`

### SANS：系统管理、网络与安全学院

`SANS` 是一个专业组织，赞助安全相关的会议和培训计划，并发布各种安全信息。他们的网站 `www.sans.org` 是一个非常有用的资源，处于 `SecurityFocus` 和 `CERT` 之间的某种折中地带：既不像前者那样疯狂，也不像后者那样呆板。

`SANS` 提供了若干每周和每月一次电子邮件简报，你可以在他们的网站上注册。每周的 `NewsBites` 很有营养，但每月的摘要包含许多模板化信息。这两者都不是获取最新安全新闻的绝佳来源。

### 针对特定发行版的安全资源

由于安全问题可能会产生大量的负面声誉，供应商通常热于帮助客户保持系统安全。大多数供应商都有一个官方邮件列表，在上面发布安全相关的简报，并维护一个关于安全问题的网站。安全相关的软件包通常是免费分发的，即使对于那些通常对软件支持收费的供应商也是如此。

网上还有安全门户，例如 `www.securityfocus.com`，其中包含特定供应商的信息以及指向最新官方供应商文档的链接。

- 红帽（`Red Hat`）安全公告列表可以在 `www.redhat.com/support/errata` 找到。写本文时，红帽尚未赞助任何官方安全邮件列表。然而，网上有很多各种 `Linux` 安全资源；大部分信息直接适用于红帽。

你可以在此处找到 `SuSE` 安全公告：

```
http://www.suse.com/us/support/security/index.html
```

你可以通过访问以下地址加入官方 `SuSE` 安全公告列表：

```
http://www.debian.org/en/support/mailinglists/index.html
```

访问 `www.debian.org` 查看最新的 `Debian` 信息，或者加入邮件列表：

```
http://www.debian.org/security/security-announce
```
