
此 MX 记录表示，任何 `address@widgets.test` 的地址都应该通过服务器 `mailserver.example.org` 发送。`0` 表示此 MX 记录的数值优先级。当给定的标签存在多个 MX 记录时，会先尝试优先级最低的 MX 记录。如果遇到临时错误，将尝试下一个高优先级的邮件服务器，以此此类推直到列表耗尽。此时，发送服务器将定期重试，直到消息超时（通常为五天）。如果存在多个优先级相同的 MX 记录，将按随机顺序尝试它们。

在不存在 MX 记录的情况下，大多数邮件服务器将回退到该标签的 A 记录中列出的 IP 地址。然而，依赖此项被认为是不良的做法。

在某些情况下，由于你的 IP 地址经常变化，建立 A 记录可能会很复杂。显然，这不适用于商业目的，但有一个对于个人使用来说是可以接受的可靠变通方法。这是通过许多不同公司提供的（通常是免费的）动态 DNS 服务实现的。这些公司的列表在 http://dmz.org/Computers/Software/Internet/Servers/Address_Management/Dynamic_DNS_Services/ 维护。以下是最受欢迎的三个（无特定顺序）：

- DynDNS.org (http://dyndns.org/)——由 `ddclient` 或 `ipcheck` 软件包支持。
- ZoneEdit (http://zonedit.com/)——由 `ex-ipupdate` 软件包支持。
- No-IP (http://no-ip.com/)——由 `no-ip` 软件包支持。

`ex-ipupdate` 软件包支持所有这些以及许多其他。查看软件包描述（`apt-cache show ex-ipupdate`）获取更多信息。

这些服务中的大多数都免费为你提供一个共享域名下的主机名，并可以以合理的费用为自己的域名提供类似的服务。

# 配置从邮件主机取回邮件

从邮件主机取回邮件的配置要求相当有限。你的服务器应该准备好接收发送到 `localhost` 的邮件，并且通常应该有一个唯一的名称。如果发送到你其中一个邮箱箱的邮件被拒绝，服务器需要一个有效的主机名在发送 DSN（投递状态通知）时识别自己的身份。

你必须能够从客户端访问服务器，尽管你可能需要从网络内的客户端进行操作。无论何种情况，你都应该熟悉上一节中关于 DNS 和 A 记录的信息。

# 安装和配置邮件服务器软件

一旦你完成了准备工作，就可以开始安装软件了。软件的安装和配置被分为两个部分。

# 第五部分 运行服务器

涵盖 Exim 和 Courier 的安装。第二部分涵盖了 ClamAV 和 SpamAssassin 的安装，以及配置 Exim 使用它们来过滤入站邮件。

# 安装 Exim 和 Courier

安装和配置 Exim 和 Courier 由于 Debian 自带软件包的质量非常简单。很有可能，如果你有一个新的 Debian 系统，它已经安装了一个版本的 Exim。然而，你可能想使用一个包含内容扫描功能的特定 Exim 版本。以下是安装步骤：

- 1. 首先安装此 Exim 软件包：
```
# apt-get install exim4-daemon-heavy
```
- 2. 有几个配置需要从默认值进行更改。运行以下命令：
```
# dpkg-reconfigure
```

# 运行服务器

> 注意
Debian 3.1（又名 "Sarge"）包含的 ClamAV 版本使用了旧的病毒扫描引擎。由于更新后的引擎可能不会在短期 Debian 升级策略的更新中出现，一组 Debian 开发人员创建了一组特殊的 ClamAV 软件包，设计以便在 Sarge 上轻松安装。有关如何使用这些软件包而非标准版本包的更多信息，请参阅 http://volatile.debian.net/。您可以从一开始就执行此操作，也可以稍后向 APT 配置添加适当的 URL 并进行升级。无论哪种情况，本节详细介绍的配置过程都大相同。

以下是安装 ClamAV 和 SpamAssassin，然后配置 Exim 使用它们扫描邮件的方法：

- 1. 安装 ClamAV 和 SpamAssassin 软件包：
```
# apt-get install clamav-daemon clamav-testfiles \
# spamassassin spamc
```
您将会被问到一些关于如何配置 ClamAV的问题。以下是回答方法：

- * 病毒更新方法 — 这是 freshclam（ClamAV 的一部分）用于下载更新病毒数据库的方法。推荐的选项是将 freshclam 作为守护进程运行。
- * 本地镜像站点 — 这是 freshclam 获取病毒信息的站点。站点的第二部分是两个字母的国家代码。选择您的国家代码，或者如果您的代码不可用，则选择附近国家的代码。
- * HTTP 代理信息 — 除非您需要使用代理服务器访问 Web 服务器，否则不要在此处输入任何内容。如果您的连接适用于邮件服务器，您可能不需要使用代理服务器。
- * 更新后通知 clam — 在此处选择 "yes"。

- 2. 将 clam 用户添加到 Debian 组并重启 ClamAV 守护进程。这允许 ClamAV 访问 Exim 邮件队列中的文件：
```
# gpasswd -a clamav Debian-exim
# invoke-rc.d clamav-daemon restart
```
- 3. 将 SpamAssassin 使用的报告模板替换为更易放入邮件头部的模板。使用文本编辑器在 `/etc/spamassassin/local.conf` 的末尾添加以下几行：
```
clear_report_template

report_YESNO_, score=_SCORE_, required=_REQD_, summary=

report_SUMMARY_
```
- 4. 配置 SpamAssassin 后台守护进程自动运行，并且尝试为用户创建偏好列表。更改 `/etc/default/spamassassin` 中的以下选项：
```
ENABLED=1

OPTIONS="--max-children 5"
```

# 运行邮件服务器

- 5. Spamassassin 守护进程：
```
# invoke-rc.d spamassassin start
```
- 6. 创建 Exim ACL（访问控制列表）中用于扫描邮件数据的条目。使用文本编辑器创建一个名为 `/etc/exim4/acl_check_data_local` 的文件，内容如下：
```
deny message = $malware_name detected in message
demime = *
malware = *
```
```
warn message = X-Spam-Score: $spam_score ($spam_bar)
condition = ${if <{$message_size}{80k}{1}{0}}
spam = nobody:true/defer_ok
```
```
warn message = X-Spam-Status: $spam_report
condition = ${if <{$message_size}{80k}{1}{0}}
spam = nobody:true/defer_ok
```
```
deny message = Spam score too high ($spam_score)
condition = ${if <{$message_size}{80k}{1}{0}}
spam = nobody:true/defer_ok
condition = ${if >{$spam_score_int}{120}{1}{0}}
```
第一个区块拒绝包含病毒或其他恶意软件的邮件，第三个头部添加了 SpamAssassin 是否认为了它们。最后一个区块检查 `$spam_score_int`（垃圾邮件评分乘以 10），如果它大于 120，则拒绝该邮件。

最后三个区块中的 `/defer_ok` 告诉 Exim，如果无法联系 SpamAssassin 守护进程，继续处理也是允许的。如果您希望在这种情况下让服务器返回临时性故障，则可以将其删除。如果您希望在邮件无法被 ClamAV 扫描时进行处理，也可以在恶意软件部分的末尾添加 `/defer_ok = *`。

- 7. 告诉 Exim 要扫描哪种病毒以及如何连接到 SpamAssassin。使用文本编辑器创建一个名为 `/etc/exim4/conf.d/main/10/exim4-exican_acl_options` 的文件，内容如下：
```
av_scanner = clamd:/var/run/clamav/clamd.ctl
spam_address = 127.0.0.1 783
```
```
CHECK_DATA_LOCAL_ACL_FILE = CONFDIR/acl_check_data_local
```
