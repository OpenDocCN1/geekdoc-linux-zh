
该命名守护进程将创建从属区域数据文件，实际上将在各方面充当从属 DNS 服务器，唯一例外是不接收 NOTIFY 语句（主服务器尚不知道此从属服务器的存在）。

因此，完全可以在主服务器不知情的情况下设置一个从服务器。由于这对主服务器造成了额外的流量负担，这不符合正确的 DNS 礼仪。主服务器的管理员应被告知所有从服务器的信息。

主服务器可以通过限制能够接收区域传输的服务器来防止未授权的从服务器。只需在 `named.conf` 的区域部分或全局部分中添加以下语句之一：

```
allow-transfer {192.168.100.2};    # 仅 mydesk 可作为从服务器
或
allow-transfer {192.168.100.2; 192.168.100.10}; # 两者皆可
或
allow-transfer {192.168.100/24};  # 仅限子网内的主机
```

验证文件 `/var/named/slave.domain.cxm` 和 `/var/named/slave.192.168.100.` 是否存在。如果存在，请快速执行此命令列表以验证其是否给出预期输出：

```
nslookup mainserv 192.168.100.2
nslookup mydesk 192.168.100.2
nslookup mainserv.domain.cxm 192.168.100.2
nslookup mydesk.domain.cxm 192.168.100.2
nslookup 192.168.100.1 192.168.100.2
nslookup 192.168.100.2 192.168.100.2
```

在下一节中，您将让主服务器感知从服务器的存在，以便其在修改和重启时发送 NOTIFY 语句。

## 向 mainserv 添加第二 DNS 服务器

在 `named.domain.cxm` 中 IN NS 语句下方添加以下行：

```
IN     NS     mydesk
```

在保存工作并退出之前，请确保递增序列号（括号中的 SOA 列表中的第一个数字）。

现在在 `named.192.168.100:` 中 IN NS 语句下方添加此行：

```
IN     NS     192.168.100.2.
```

请记住，mydesk.domain.xm 的地址是 192.168.100.2。再次，请确保递增序列号。递增的序列号正是告诉从服务器需要执行区域传输的信号。

最后，使用此命令重启主服务器 DNS 服务器：

```
# /etc/rc.d/init.d/named restart
```

添加 NS 记录使得可以向 mydesk 上的 DNS 服务器发送 NOTIFY 语句，从而触发该服务器发起区域传输。新的 NS 记录还允许将 mydesk 用作备用 DNS 服务器。

要验证从区域是否正常工作，请执行以下 shell 命令并确保获得预期输出：

```
nslookup mainserver 192.168.100.2
nslookup mydesk 192.168.100.2
nslookup mainserver.domain.xm 192.168.100.2
nslookup mydesk.domain.xm 192.168.100.2
nslookup 192.168.100.1 192.168.100.2
nslookup 192.168.100.2 192.168.100.2
```

DNS 从服务器及其区域传输，连同委派机制，赋予了 DNS 服务数百万 URL 的能力。

## DNS 故障排查

本章前面已经讨论了许多 DNS 故障排查技术，例如使用 telnet 程序检测反向 DNS 问题。其他故障排查选项包括脚本程序和 named 日志记录选项。

### 使用脚本对您的 DNS 设置进行压力测试

您可以创建两个有用的脚本来对 DNS 设置进行压力测试。它们可以命名为任意名称，但本例将它们命名为 check1 和 check。check1 脚本只是将 nslookup 的结果记录在文件 junk.jnk 中，而 check 针对每个考虑的域名和 IP 调用 check1。以下是 check1 的代码：

```
echo "nslookup $1 $2" >> junk.jnk
nslookup $1 $2 >> junk.jnk
echo "" >> junk.jnk
echo "" >> junk.jnk
```

check1 只是将其参数的 nslookup 结果写入文件。check 接受单个参数，如果存在，则将其作为 arg2 传递给各种 check1 调用。以下是 check 的代码：

```
rm junk.jnk
./check1 mainserv $1
./check1 mydesk $1
./check1 mainserv.domain.cxm $1
./check1 mydesk.domain.cxm $1
./check1 www.domain.cxm $1
./check1 192.168.100.1 $1
./check1 192.168.100.2 $1
less junk.jnk
```

前面的脚本应该运行迅速并产生正确的输出。如果没有，则存在问题。通过有选择地注释 `check` 脚本中的行，您可以缩小问题范围。

`nslookup` 程序在交互使用时提供了许多强大功能。它也可能导致令人沮丧的挂起现象。为了增强故障排查能力，请从其 man 页面了解 `nslookup`。

### 使用转储和日志进行调试

`named` 的主要调试工具之一是让守护进程将其缓存数据库转储到文本文件中。要使 `named` 转储其缓存，必须向守护进程发送 `INT` 信号。文件 `/var/run/named.pid` 包含 `named` 的进程 ID。以下命令向 `named` 发送 `INT` 信号：

```
# kill -INT `cat /var/run/named.pid`
```

文件 `/var/named/named_dump.db` 将包含转储的缓存信息。缓存文件看起来类似于区域数据库文件。

`named` 守护进程还支持调试日志记录。要启动守护进程日志记录，请像这样向守护进程发送 `USR1` 信号：

```
# kill -USR1 `cat /var/run/named.pid`
```

日志信息记录在 `/var/named/named.run.log` 文件中。如果向守护进程发送 `USR1` 信号，日志信息的详细程度会增加。实际上，它非常详细，以至于您需要搜索诸如 `error` 之类的字符串，而不是 `found`。要将调试级别重置为 0，请向守护进程发送 `USR2` 信号。

每当区域数据库更改时，都可以向 `named` 守护进程发送 `HUP` 信号，理论上 `HUP` 信号可以重新读取数据库，而无需终止并重启 `named` 守护进程。但事实上，有时 `HUP` 信号并不像宣传的那样起作用。以下示例向 `named` 发送 `HUP` 信号：

```
# kill -HUP `cat /var/run/named.pid`
```

## 注意

如果对 `/etc/named.conf` 文件进行了更改，必须停止并重启 named 守护进程才能看到更改。

在任何情况下，如果您想确保所有文件都被读取和加载，请使用此命令：

```
# /etc/rc.d/init.d/named restart
```

另一种很棒的调试技术，尤其是在重启 named 之后，是查看系统日志。您可以通过查看 `/etc/syslog.conf` 来找到包含相应日志的文件。Red Hat 7 的默认值是 `/var/log/messages`。因为您只对最近的消息感兴趣，使用此命令抓取文件末尾：

```
# tail -n 400 /var/log/messages | less -N
```

所有日志条目都有日期和时间，因此如有需要，您可以读取超过 400 行。特别留意 error、not found、no such、fail 等。仔细评估任何错误消息，并尝试弄清楚它们的含义以及原因。

## 使用 dnswalk 检查您的 DNS 配置

我发现 dnswalk 是一个不可或缺的工具。它非常彻底地检查您的 DNS 配置。它是 C 语言 `lint` 工具或 Samba `testparm` 工具的 DNS 等效物。首先使用 dnswalk 可以轻松节省数小时的故障排除时间，因此花几分钟安装和使用它是值得的。

dnswalk 实用程序依赖于 perl-Net-DNS 工具，因此必须先安装后者。使用 Red Hat 发行版时，最简单的安装方式是通过 rpm。首先，从网络获取这两个文件：

- `ftp://rufus.w3.org/linux/contrib/libc5/1386/perl-Net-DNS-0.12-1.1386.rpm`
- `ftp://rufus.w3.org/linux/contrib/noarch/noarch/dnsvalk-2.0.2-1.noarch.rpm`

现在使用以下两个命令安装它们：

```
# rpm -ivh perl-Net-DNS-0.12-1.1386.rpm
# rpm -ivh dnsvalk-2.0.2-1.noarch.rpm
```

## 提示

如果您更喜欢从源代码编译、构建和安装，可以在 http://www.visi.com/~barr/dnswalk/ 获取源代码。

必须按照上述顺序安装，因为 dnswalk 依赖于 perl-Net-DNS。dnswalk 可执行文件（实际上是一个 Perl 程序）安装在 /usr/sbin 目录中。dnswalk 通过指定域名作为唯一参数来使用。域名必须以点 (.) 结尾。以下是一个示例：

```
# dnswalk domain.cxm.
Checking domain.cxm.
BAD: domain.cxm. has only one authoritative nameserver
Getting zone transfer of domain.cxm. from mainserv.domain.cxm... done.
SOA=mainserv.domain.cxm contact:hostmaster.domain.cxm
0 failures, 0 warnings, 1 errors.
#
```

您会注意到它发现的唯一错误是缺乏二级 DNS 服务器。本章的大多数示例只定义了一个 DNS 服务器。在以下示例中，named.domain.cxm 已更改，使得 mydesk.domain.cxm 解析为 192.168.100.22，但 named.192.168.100 中的反向查找仍为 192.168.100.2。这是一种正向/反向不匹配——一个严重的问题，使用 nslookup 等工具将很难诊断：

```
# dnswalk domain.cxm.
Checking domain.cxm.
BAD: domain.cxm. has only one authoritative nameserver
Getting zone transfer of domain.cxm. from mainserv.domain.cxm... done.
SOA=mainserv.domain.cxm contact:hostmaster.domain.cxm
WARN: mydesk.domain.cxm A 192.168.100.22: no PTR record
0 failures, 1 warnings, 1 errors.
```

在上面的代码中，请注意“no PTR record”警告，表明 192.168.100.22 没有反向 DNS。

如果您在比最基础水平更高的层面上配置 DNS，dnswalk 是一项至关重要的投资。尽早并经常使用它。

## DNS 资源

虽然本章涵盖了最必需的 DNS 信息，但完整的 DNS 讨论可以轻松填满一本厚书。以下是其他 DNS 文档资源：

- /usr/share/doc/bind-8.2_P5/ — 请注意，确切的目录名可能因您的 Red Hat 发行版而异。此目录包含 CHANGES、INSTALL、TODO 和 Version。它还包含 bog/、html/、misc/、notes/、rfc/ 和 tm.ac/ 目录。html/ 和 rfc/ 目录特别有趣。

