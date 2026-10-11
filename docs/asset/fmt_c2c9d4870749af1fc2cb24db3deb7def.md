
`ServerName` `secure.example.org`

`ServerAlias` `web.example.org`

`DocumentRoot` `/home/username/public_html/`

`DirectoryIndex` `index.php` `index.html` `index.htm`

`SSLEngine` `On`

`SSLCertificateKey` `/etc/apache2/ssl.key/server.key`

`SSLCertificateFile` `/etc/apache2/ssl.crt/server.crt`

`SSLCertificateFile` `/etc/apache2/ssl.crt/ca.crt`

```
</VirtualHost>
```

此示例在 `VirtualHost` 声明中使用通配符表示 IP 地址，这避免了在 IP 地址更改时修改配置文件，但也防止了您拥有多个 SSL 虚拟主机。如果需要支持多个 SSL 虚拟主机，请将 `*` 替换为分配给该主机的特定 IP 地址。

有关 `Listen` 指令的更多信息，请参见本章节前面的“故障排除”部分。

CA 通常会提供一个证书文件放入 `ca.crt`，有时会提供一个单独的文件，您需要使用 `SSLCertificateChainFile` 指令来引用它。

- 3. 测试 Apache 配置并执行完全重启：

```bash
$ sudo apache2ctl configtest

Syntax OK.

$ sudo apache2ctl stop

$ sudo apache2ctl start
```

# 关于系统及使用的软件

本章描述的邮件服务器配置基于 Exim 邮件传输代理（MTA）。除了 Exim 之外，还了其他组件用于管理服务器并检查邮件内容中的垃圾邮件和病毒：

- [Exim](https://www.exim.org/) — 由剑桥大学的 Philip Hazel 编写并设计的 MTA，并来自全球许多人的贡献。本章中提到的版本包含了 Tom Kinsner 提供的 Exiscan-ACL 补丁（http://duncanthrax.net/exican-acl/）。该补丁允许从 Exim 内部进行内容扫描。由于此补丁已集成到 Exim 中，在本章的范围内，其功能被视为 Exim 的一部分。

- [Maildrop](https://www.courier-mta.org/maildrop/) — 本地投递代理（MDA），是 Courier MTA 包的一部分，也可以作为独立程序使用。在此配置中，它用于允许使用高级功能，例如信箱配额和服务器端排序。

- [Courier IMAP 和 POP](https://www.courier-mta.org/imap/) — 与 Maildrop 类似，这些也是 Courier MTA 的一部分，也可以单独提供。选择它们是因为它们安装快速、性能良好，并且与 Maildir 格式的邮件目录兼容。

- [ClamAV](https://www.clam.net) — 一种开源的病毒扫描器，可以检测超过 20,000 种病毒、蠕虫和木马。它使用病毒特征数据库识别病毒，并包含一个名为 `freshclam` 的程序来自动更新数据库。与 SpamAssassin 类似，ClamAV 包含一个守护进程（`clamd`）、一个客户端（`clamscan`）以及另一个不使用守护的命令行工具（`clamscan`）。

- [SpamAssassin](http://spamassassin.apache.org/) — 用 Perl 编写的垃圾邮件过滤程序。它使用大量的规则来判断邮件看起来有多像垃圾邮件，并根据规则总和进行评分。出于性能考虑，SpamAssassin 使用一个名为 `spamd` 的后台守护进程来执行邮件分析。该守护进程通过垃圾邮件客户端访问。还安装了不使用 `spamd` 运行分析的 `spamass` 命令，但本章中的两个示例配置均未使用它。

# 准备你的系统

在开始本章涵盖的邮件服务器配置之前，你需要一些常用的项目，首先是从适当的硬件开始。个人邮件服务器可以轻松运行在奔腾类计算机上，尽管在扫描传入邮件时，你可能会注意到偶尔的减慢。磁盘空间需求主要取决于你想要容纳多少邮件，因此请为操作系统留出几个 GB（这将为你留出足够的额外空间以备万一），加上你想存储的邮件量。

# 设置 Linux 服务器

在开始这些示例之前，安装操作系统时应只安装基础软件包集。关于安装的一些通用信息请见第 17 章。虽然本章描述的软件即使在你没有运行 Ubuntu 时也可以工作，但安装方法并不如此。如果你没有空闲空间作为专用邮件服务器，你仍然可以将其作为工作站，尽管这显然仅建议用于个人使用。

在开始安装邮件软件之前，还应该正确配置你的网络设置。具体要求取决于邮件投送到你服务器的方法：

- 直接投递（Direct delivery）是大多数传统邮件服务器使用的方法。DNS 记录告诉远程服务器，任何发送到你域名的邮件都应通过 SMTP 发送到你的服务器。
- 也可以使用 MRA（邮件取取代理）如 `Fetchmail` 从邮件主机检索邮件。当你在共享域名下有一个信箱，但想在自己的服务器上访问邮件时，可以使用此选项。如果你既有自己的域名，又有共享域名下的信箱，这也可以与直接投递结合使用。

> `Fetchmail` 的配置将在本章的“配置邮件客户端”部分进行解释。

# 为直接投递配置 DNS

为了使直接投递正常工作，SMTP 服务（TCP 端口 25）必须通过 DNS 中的固定名称供外部世界访问。该名称将以 A（地址）记录的形式存在。“A”记录允许 DNS 解析器确定与特定名称关联的 IP 地址，被互联网上的大多数常用协议使用。一个典型的 DNS A 记录如下：

```
mailserver.example.org   IN    A      10.0.12.16
```

一旦你有了 A 记录，你就可以使用 MX（邮件交换器）记录将邮件投递到你的服务器。以下是一个示例 MX 记录：

```
widgets.test             IN    MX     10  mailserver.example.org
```

数字 10 表示 `widgets.test` 应该通过服务器 `mailserver.example.org` 发送。当存在多个 MX 时，会尝试优先级最低的一个。如果遇到临时错误，则会尝试下一个优先级，依此类推，直到列表耗尽（通常为五天）。如果存在多个优先级相同的 MX，将按随机顺序尝试。

# 运行邮件服务器

注意
在不存在 MX 记录的情况下，大多数邮件服务器也会回退到 A 记录中列出的 IP 地址。然而，依赖这一点被认为是不良实践。

这是通过许多不同公司提供的动态 DNS 服务（通常是免费的实现的实现的这些公司的列表维护在 http://dmoz.org/Computers/Software/Internet/Address_Management/Dynamic_Services/。其中最流行的两个是：

- ZoneEdit (https://www.zonedit.com/) — 由 `ezipupdate` 包支持。
- No-IP (https://www.no-ip.com/) — 由 `no-ip` 包支持。

注意
`ezipupdate` 包支持这两个，以及其他一些。请查看软件包描述（`apt-cache show ezipupdate`）以获取更多信息。

这些服务中的大多数可以免费为你提供一个共享域名下的主机名，并以合理的费用为自己的域名提供类似的服务。

# 配置从邮件主机检索

从邮件主机检索邮件的配置要求非常有限。你的服务器应该准备好接收发往 `localhost` 的邮件，并且通常拥有一个唯一的名称。在发送到你某个信箱的邮件被拒绝时，服务器需要一个有效的主机名以便在发送 DSN（投递状态通知）。

你必须能够从客户端访问服务器，尽管你可能从网络内部的客户端访问。无论哪种，你都应该熟悉上一节中关于 DNS 和 A 记录的信息。

# 安装和配置邮件软件

在完成先决条件后，你就可以开始安装软件了。软件的安装和配置分为两个部分。第一部分涵盖安装 Exim 和 Courier。第二部分涵盖安装 ClamAV 和 SpamAssassin 并配置 Exim 使用它们来过滤传入的邮件。

# 安装 Exim 和 Courier

安装和配置 Exim 和 Courier 非常简单，这取决于 Ubuntu 自带软件包的质量。如果你有一个新的 Ubuntu 系统，它可能已经安装了

# 第四部分 设置 Linux 服务器

已安装了一个版本的 Exim。然而，你可能希望使用一个包含内容扫描特性的特定版本的 Exim。以下是安装步骤：

- 1. 首先安装此特定的 Exim 软件包：

```
sudo apt-get install exim4-daemon-heavy
```

- 2. 你需要从默认设置更改一些配置选项。运行以下命令：

```bash
sudo dpkg-reconfigure --priority=medium exim4-config
```
