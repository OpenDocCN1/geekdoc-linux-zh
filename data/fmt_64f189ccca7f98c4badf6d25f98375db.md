
## 在初始提交时避免连接到“高昂”的邮件发送器？

`O HoldExpensive=True`

## 从零开始 sendmail：功能、调优与性能

作者：Stewart Benedict

在“从零开始理解 sendmail”中，我涵盖了哪里获取 `sendmail`，以及如何从源码构建并使用 `.mc` 文件和选项设置基础 `sendmail`。这次，我将涵盖一些额外的 `.mc` 选项以及它们对 `sendmail` 的影响。我还将涵盖一些命令行开关，以及你可以使用 `sendmail` 通过别名（aliases）或伪装（masquerading）来测试任何地址重写的方法。最后，我将提供关于性能调优以及如何分析 `sendmail` 统计数据和日志文件的信息。

### 启用额外功能

让我们看看更多可以在邮件文件中启用的功能，该文件被用于生成 `sendmail.cf`。回顾一下，我们在邮件文件中定义配置，并使用 `m4` 处理器生成 `cf` 文件：`/usr/bin/m4 ...cf mysite.mc < mysite.cf`

`sendmail` 现在带有中继交付功能。在互联网早期，这些并不是问题，但随着我们所有人收到的海量垃圾邮件，管理员有必要收紧对谁的邮件通过其系统的控制。如果你想启用中继，请在邮件文件中添加以下功能：

```
FEATURE ('promiscuous relay')
```

如果你只想中继到自己的域名，请使用：

```
FEATURE ('relay_domain')
```

硬币的另一面是如何设置一个服务器来接受另一个域名。如果你从一个未限定的域名（例如小型企业或家庭服务器）中继，但想将邮件队列并批量发送到你的 ISP，这将非常有用。这涉及到伪装和中继，留下了几个可以启用的控制层。最简单的伪装级别是：

```
MASQUADE_AS (host)
```

所以如果你的主机是 `sendmail.cf`，且你想让出站邮件看起来像 `domain.com`，那么 `sendmail.cf` 文件中的规则将如列表 A 所示。大多数邮件服务器现在

### 结论（此处为内容重复，根据原文保留翻译）

### A：伪装

`A`

（可能）

`smtp.mysyip.com`

有些站点会拒绝这种邮件，所以你可能需要伪装：

```
domain.com
```

如果你想对某些用户进行，，邮件发送器，使用：

```
EXPOSED_USER (usernames)
```

你还可以设置虚拟域名，你的邮件发送器可以：

```
FEATURE ('vertustable')
```

在这种情况下，你的入站邮件：

```
larry
```

为了以这种方式映射出站邮件，使用功能：

```
FEATURE ('genericstable')
```

并设置 `/etc/mail/genericstable`，像虚拟的具有：

```
larry
```

如果你有很多机器，并想在发送到 ISP 之前中继所有邮件，那么

```
define ('LOCAL_RELAY', 'mail:hostname')
```

所有未限定的地址将被中继到本地机器。在 `sendmail.cf` 中，结果类似于列表 B。

相关的功能是：

```
define ('SMART_HOST', 'mail:hostname')
```

### B：中继

`C： 使用黑名单`

文件的右侧，带有 `REJECT`、`OK`、`RELAY` 或各种 `ERROR` 信息：

```
spammer@yahoo.com      REJECT
cibers@cyber.com       REJECT
mybody@cyber.com        OK
```

你还可以为你的系统和用户设置“黑名单”，使用：

```
FEATURE ('blacklist_recipients')
```

再次，这是一个表格列表，可以包含用户和域名（使用 `C`），客户端在通过简单邮件传输协议 (SMTP) 服务器发送出站邮件之前，在 `POP` 服务器上检查他们的入站邮件。

由于许多客户端可以以此方式运行，对用户有特殊要求，只有授权的用户可以通过服务器中继邮件。

这涵盖了关于什么通过你的服务器的大部分关注问题。还有，`sendmail` 网站在 `www.sendmail.org` 显示了它们。

### 测试模式运行

另一种运行 `sendmail` 的方式是测试模式，它允许你检查别名和重写规则。你可以通过带有 `-bv` 或 `-bt` 关来运行 `sendmail`。

假设你有以下别名，有两个管理员接收 `root` 的邮件，还由于名为“`management`”的用户别名列表：

```
root           stew      Dianne
management   stew      Fred. Justin
```

```
[sendbook mail]$ /usr/sbin/sendmail -bv root
dianne... User unknown
stew... deliverable: mailer, local user stew
```

178 企业级 Linux 管理员指南

### 列表 D: 一个简单的别名检查脚本

```
[root@omnibook mail ~]# cat check_aliases.sh
#!/bin/sh

for i in $(grep "#" < /etc/mail/aliases | awk -F":" '{print $1}'); do
  result=$(usr/sbin/sendmail -bv $i | grep -v deliverable)
  if [ -n "$result" ]; then
    echo "Bad alias in: $i"
    echo "$result"
  fi
done
[root@omnibook mail ~]# ./check_aliases
Bad alias in root:
dianne... User known
Bad alias in management:
justin... User known
fred... User known
```

所以我们可以看到 `"dianne"` 用户不再是该机器上的有效账户了。

```
[omnibook mail]$ /usr/sbin/sendmail -bv management
justin... User known
fred... User known
stew... deliverable: mailer,
```

> 同样，“`Fred`” 和 “`Justin`” 不再是有效的账户。

如你所见，当你的用户账户系统中添加或删除账户时，这是一种测试别名的非常简单的方法，此时你可能想要设置别名文件，并向任何无效地址发送电子邮件。

列表 D:

你也可以使用 `-bt` 选项运行 `sendmail` 来测试你的规则集。如果运行了它，你会发现自己处于一个 `"$#"` 提示符，可以在其中输入规则集名称或地址，你将看到该地址是如何通过规则集并被处理的。

```
[stew@omnibook mail]$ /usr/sbin/sendmail -bt
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <ruleset> 
> stew
```

```
parse input: stew
Parsec input: stew
Parsec returns: stew
ParLocal input: stew
ParLocal returns: stew
Parsel input: stew
Parsel returns: # local $: stew
Parse returns: # local $: stew
31 stew
HdrFromSMTP input: stew
PseudoToReal input: stew
PseudoToReal returns: stew
MasqSMTP input: stew
MasqSMTP returns: < @ LOCAL *
Masqdr input: < @ LOCAL *
Masqdr returns: < @ myisp
  .com .
HdrFromSMTP returns: < @ myisp
  .com .
```

如果我们在使用伪装设置（masquerading setup），可以使用此来确保“发件”地址正如你预期的那样被重写。

### 规则集 31

规则集 `31` 用于标头重写。

网络 179

观察地址如何通过各种规则集并被修改是非常趣的。列表显示了一个我们在 `access_db` 中设置的针对你的 Yahoo 垃圾邮件发送者的规则。

这些示例让你让你概览了通过启用不同的 `sendmail` 选项和功能可以执行的操作，并提供了一种比发送邮件并希望它能送达更高效的测试方法。如果你正在使用数据库表控制列表，设置一些脚本在添加新条目后通过测试模式运行它们将是有有无益的。事实上，你可以自动化处理向其中一个数据库表添加新条目的过程，运行 `makemap`，重启 `sendmail`，并并通过测试模式处理新条目。

## Sendmail 性能优化

现在我们已经了解了一些可以对进出邮件所施加的控制程度，让我们看看如何通过运行 `sendmail` 来获得最大效率。有很多选项

我们可以设置这些控制邮件如何被处理，以及 `sendmail` 如何与系统上运行的其他软件共存。

`QueueOrder=host`

如果你向同一主主上的多个用户传输大量邮件，此功能可以最有效地利用系统缓存。出站队列按主机名排序，通过缓存连接，发往同一个主机的多条消息可以通过一个连接通过，而不是不断打开和关闭 SMTP 连接。

如果你正在处理海量的邮件，你可能需要采取措施使用单独的磁盘、`RAID` 或哈希文件系统来增加消息队列的效率。你可能还需要运行额外的邮件处理器，并将 `QueueSortOrder` 同时设为 `"host"` 和 `"time"`，以便快速清理消息，并确保最旧的消息不会被退回。

`Sendmail` 大度利用了 `DNS`，如果你正在处理大量的邮件

### 列表 E: 拒绝我们的 spammer@yahoo.com

| 命令 | 输入 | 返回值 |
| :--- | :--- | :--- |
| `Basic_check_mail` | input: `spammer @ yahoo . com` | |
| `tls_client` | input: `$ \| < ? >` | |
| `LookUpDomain` | input: `< ? > < ? > < ! TLS Clt` | |
| `LookUpDomain` | returns: `< ? > < ? > < ? > < ! TLS Clt` | |
| `LookUpAddress` | input: `< ? > < << < ! TLS Clt` | |
| `LookUpAddress` | returns: `< ? > < << < ! TLS Clt` | |
| `tls_connection` | input: `$ \| < ? > < > < ! TLS Clt` | |
| `tls_connection` | returns: `OK` | |
| `tls_client` | input: `< spammer @ yahoo . com >` | |
| `canify` | input: `< spammer @ yahoo . com >` | |
| `canify2` | input: `< spammer @ yahoo . com >` | |
| `canify2` | returns: `< spammer @ yahoo . com >` | |
| `canify` | returns: `< spammer @ yahoo . com >` | |
| `Parse` | input: `< spammer @ yahoo . com >` | |
| `Parse` | returns: `< spammer @ yahoo . com >` | |
| `CanonAddr` | returns: `< spammer @ yahoo . com >` | |
| `SearchList` | input: `< From $ F : spammer @ yahoo . com > < : spammer @ H : . com >` | |
| `SearchList` | returns: `< REJECT` | |
| `Basic_check_mail` | returns: `# error @ $ 750 Access denied` | |

Linux 管理员指南：避免在同一台机器上同时运行 `sendmail` 和 `bind`，因为它们会竞争资源。还有其他选项可以控制如何与系统上的程序共存：

- `ConnectionCacheSize` 打开后续发往同一主机的连接数。
- `ConnectionCacheTimeout` 定义连接的超时。
- `ConnectionRate` 减慢入站连接。
- `Expensive` 将某些邮件定义为“昂贵的”，并在系统低负载时运行。
- `MaxChildren` 限制派生进程的数量。
- `MinQueueAge` 不处理过期的队列。
- `QueueFactor` 与 `QueueLA` 配合，根据系统负载调整是发送邮件还是进入队列。
- `QueueLA` 是 `sendmail` 开始排序的平均负载。
- `RefuseLA` 是 `sendmail` 拒绝入站邮件的平均负载。

`sendmail` distribution 提供了关于这些选项默认值的详细信息。本文的重点是查看你的邮件服务器在处理哪些内容（见列表 F）。这告诉我们有 15 条邮件来自本地邮件代理，同时有 664 条邮件来自 SMTP，其中一条邮件通过 SMTP 发出。你可以通过 `cron` 任务自动化报告统计并重置日志文件：

```
#!/bin/sh
mailstats -f /etc/statistics
cat /dev/null > /etc/statistics
```

如果你真的想深入了解 `/var/log/mail` 的细节。

### 列表 F: Mailstats 报告

```
[root@omnibook config]# mailstats -f /etc/mailstats

Statistics from Apr 14 17:48:21

| msgs_from | bytes_from | msgs_to | bytes_to | Mailer |
| :--- | :--- | :--- | :--- | :--- |
| 15 | 287 | 65 | 1310K | local |
| 664 | 2589K | 679 | 2617K | smtp |
| 679 | 676 | | | |
```

### 列表 G: mailog 将显示所有

```
Jun 4 18:58:26 omnibook sendmail[1934]: restarting on signal /usr/sbin/sendmail
Jun 4 18:58:26 omnibook sendmail[1956]: starting daemon (8.11.3): SMTP:+queue1:00
Jun 4 20:07:31 omnibook sendmail[2008]: ua2008: from=*root@omnibook.ays, size=275, class=0, ncerts=5, mgide=P.LNX.4.1081420724.2006-10000@omnibook.ays, retry=root@localhost
Jun 4 20:07:31 omnibook sendmail[2009]: ua2008: to=<stew@omnibook.ays.net>, claddr=<root@omnibook.ays.net> (0), delay=00:00:00, xdelay=00:00, mail=local, pri=3019, stat=2.0.0, stat=sent
```

most of the transaction details of `sendmail` and the local mail agent (see Listing G). 这些内容有点难以消化，但当然，有很多日志分析工具可以帮助你。其中一个工具是 `report`，地址位于：`http://ftp.matrix.co.za/pub/report/report-0.9.tar.gz`（见列表 H）。

有很多开关允许你只查看“来自”或“到达”，或者应用过滤和排序。同样，你可以将其作为 `cron` 任务运行并在处理后刷新日志文件，或者将其移动到备份中，以便在报告发现问题后进行审查。

### 列表 H: mreport

```
[root@omnibook mreport-0.9]# mreport

[ 2]    551 root@omnibook.ays.net stew@omnibook.ays.net
[ 1]    513 root
=================================================
Total Bytes           : 4266074
Number of Records    : 388
Host Name             : omnibook.ays.net
Input File            : /var/log/maillog
Output File           : stdout
First Record          : May 13 06:55:58
Last Record           : Jun 4 20:23:18

Time Taken            : 975576 µ
mreport-0.9 由 Jason Armstrong 
```

## 结论

我希望这篇文章让你对 `sendmail` 的工作原理有一定的见解，并提高你处理 `sendmail` 的从容度。正如我看到的，复杂的 `.file` 文件是由一些简单的 `.mc` 选项生成的。你还看到，很容易检查你的别名和规则集是否按预期工作。

## Qmail 概述，第 1 部分：安装 Qmail

作者：Vincent Daemon
