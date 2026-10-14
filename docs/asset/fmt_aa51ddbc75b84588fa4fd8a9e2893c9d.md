
现在，当客户端启动会话时，Squid 会根据此文件中的信息进行身份验证。然而，这并不需要在网络上传输密码。相反，服务器和客户端会根据密码和 URL（以及服务器提供的额外会话信息）分别计算 MD5 或单向哈希。客户端将计算结果发送给服务器，由服务器进行比较。

大多数浏览器都能正确地配合这种形式的身份验证。然而，我们在 Konqueror、Internet Explorer、Mozilla、Netscape、Galeon 上遇到了一些问题，而 Firefox 看起来运行得非常完美。

Squid 软件包附带的其他身份验证方法都安装在 `/usr/bin/` 下，分别是 `mnt_auth`、`ntlm_auth`、`smb_auth`、`yp_auth`、`getpwname_auth`、`ncsa_auth` 和 `squid_auth`。

因此，可以使用 Windows、Samba、LDAP 或 YP 作为身份验证方法。然而，对于这些大多数方法，关于未加密密码跨网络传输的备注已在文中给出。

# 通过硬件地址限制访问

可以通过特定的 MAC 地址限制访问。你可以在配置文件中设置 ACL：

```
acl biple mac 00:11:22:33:44:55
http_access allow biple
```

你也可以使用 IP 地址作为身份验证方法限制访问：

```
acl local_net src 192.168.1.0/24
http_access allow local_net
http_access deny all
```

这允许 Squid 代理访问与客户端相同的以太网的 IP 范围。

# Squid 日志

Squid 日志默认位于 `/var/log/squid/access.log`。记录的内容取决于你在 `squid.conf` 中设置的选项：

```
log_format custom %h %l %u %t "%s" %>b %S %u
access_log /var/log/squid/access.log squid custom
```

Squid 日志非常长且难以阅读，因此可以使用许多分析工具。SUSE 包含一个名为 `sarg`（Squid 分析报告生成）的工具。如果你想使用 `sarg` 工具，必须安装它；`sarg` 工具可以通过 `cron` 每天运行并在浏览器中生成 HTML 报告，如图 26-3 所示。

![](img/sarg.png)

*图 26-3：sarg 输出*

报告结合了使用统计分析，以及特定客户端或用户何时访问特定站点的详细信息。此类工具的使用显然涉及某些伦理考量；用户理认为他们拥有隐私权，但同时必须与公司的可接受政策进行权衡。

# 将 Squid 作为透明代理

运行 Web 代理的困难之一是每个客户端浏览器都必须配置使用它。更优雅的解决方案是强制所有访问网站的尝试都通过代理。这可以通过运行 Squid 的机器上使用 iptables 防火墙规则轻松实现：

```
iptables -t nat -A PREROUTING -i eth -p tcp --dport 80 -j REDIRECT --to-port 3128
```

假设 `eth` 是接收传入 HTTP 请求的接口，且运行 Squid 的机器被设置为客户端机器的网关。

参见第 24 章中防火墙规则的讨论。注意 `SuSEfirewall2` 能够设置透明代理所需的规则。`SuSEfirewall2` 在第 24 章中也有介绍。

Squid 配置文件应包含以下行：

```
httpd_accel host virtual
httpd_accel_port 80
httpd_accel_with_proxy on
httpd_accel_uses_header on
```

另见 Daniel Kiracofe 写的 LDP “Linux 和 Squid 透明代理微型 HOWTO”，地址为 `www.tld.org/HOWTO/TransparentProxy.html`。

你不能将透明代理与代理授权结合。据报道，某些情况下需要身份验证的远程站点可能会有问题。

# 使用缓存管理器

Squid 包含一个工具 `cachemgr.cgi`，它安装在 `/usr/share/doc/packages/squid/scripts/cachemgr.cgi`。如果你将此文件复制到 `/srv/www/cgi-bin/`，你就可以通过 `http://<squid-server>/cgi-bin/cachemgr.cgi` 查看有关 squid 缓存状态的全面信息（见图 2-4）。这假设你已经设置了 Apache Web 服务器。

您以一种符合自身政策、质量保证（QA）要求和维护问题的方式，将 SUSE 引入您的组织。

## 典型组织

我们以 Acme 为例，这是一个规模相当大的组织（用户超过 1,000 人）。与大多数组织一样，Acme 是异构的，拥有多个站点和灾难恢复（DR）策略。毕竟，如果 Acme 丢失了数据，它就会失去业务；他们销售世界上最好的小部件，其客户列表、库存数据库和分销商都是其业务流程的核心。参见图 27-1 的 Acme 全球架构示例。

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_714_0.png)

**图 27-1：** Acme 的全球架构

我们将看看 Acme 的技术组织是如何安排的，并深入探讨 Linux 可以何处的具体细节。我们还将根据之前章节中熟悉的知识，进一步探讨如何配置 Linux。

我们首先深入探讨 Linux 如何在 Acme 的一个办事处使用——我们将以伦敦办公室作为主要示例。我们可以假设其他办公室在组成上非常相似。Acme 是开源的拥抱者，正如过去几年许多企业那样。

## 可以使用 Linux 吗？

大多数 IT 总监都会问这个问题。使用 Linux 的理由已经在流行的 IT 媒体中得到了论证，组织也理解到，当需要部署 Unix 时，Linux 现在是一个可行的选择。

## 数据中心

独立软件供应商（ISV）现在将 Linux 视为其软件的 1 级（主）平台，我们谈论的不是黑房间里的程序员群体。大公司也是如此——例如 Oracle、IBM、SAP 和 SAS 等。它们都将 Linux 视为一个可以营销并成功销售的平台，其他也证明了这一点。

以 Oracle 为例；它曾表示其开发平台是 Linux。其他端口是该策略的次要。Linux 将始终是 Oracle 的新版本，就像其他主要的操作系统厂商（微软、Sun、IBM 等）一样。Oracle 已将其数据库产品发布在许多硬件平台上，包括 Intel（32/64 位）、PowerPC（PPC）和 IBM zSeries（在本章稍后部分讨论）。

市场的这部分被称为数据中心，也是所有 Linux 增长最快的地方。在过去的几年里，我们看到许多客户使用 Linux 运行关键的 Oracle 数据库；IBM 的软件在该领域也非常强大。

## 基础设施

Linux 传统上在该领域非常强大，并将组织作为其 IT 基础设施的核心组成部分。域名系统（DNS）、内网、外接网、防火墙、电子邮件、文件服务和打印服务都属于企业的这一部分。市场结果显示，Linux 上的 Apache 极其强大。许多组织在高级管理层不知的情况下在 Linux 上运行其 DNS。

这是一个非常重要的点。询问 MIS 总监他们在组织何处使用 Linux 是没问题的，他们可能根本不知道某些在基层工作的人在预算削减时，正通过秘密行动实施 Linux 以节省资金。Linux 在这个领域非常非常出色，因为这种流程对于开发者和分发版来说都是已知的考量。SUSE 知晓这一点，SUSE 标准服务器满足了这些核心服务。

## 嵌入式系统

这可能是您在组织中忽视的内容，Linux 已经嵌入到企业内部许多系统中。

虽然许多人质疑 Linux 的安全性，且其安全性仍然是一个充满推测的话题，但 Linux 仍然以其稳定性和安全性闻名。事实上，任何操作系统的安全性都取决于两点：

- 出厂时确保操作系统安全的配置和管理操作

- 包含操作系统本身的代码

Linux 并不是操作系统安全性的终点。然而，考虑到代码是开放且处于持续的安全之下，它非常接近这一目标。Linux 内核的一些补丁极地改变了操作系统的默认 Unix/POSIX 安全性，其中最流行且安全的是 Linux 入侵检测系统（LIDS）。这个名字是一个误导，因为它并非设计为检测系统，而是为了在识别之前加固内核。

由于这种安全性，Linux 已被用于许多嵌入式系统，而您可能甚至不知道。防火墙设备运行 Linux，IBM BladeCenter 中的光纤交换机运行在嵌入式 Linux 上。

在组织中运行嵌入式 Linux 通常不是主动选择，而是为了其功能集购买产品（而不是为了其运行的操作系统）时的间接选择。这是嵌入式系统在市场上证明其价值的地方，即设备的功能推销了产品，而底层的操作系统通过稳定性提供了帮助，并提供了用户看到的功能。

## 我知道在哪里，但如何做做？

向大众销售 Linux 一直是很困难的。近年来，随着 Linux 反次证明自己，这一障碍已经克服。行业现在面临的问题是如何如何部署它。
