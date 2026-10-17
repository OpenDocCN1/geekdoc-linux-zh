
在启用 systemd 的发行版中，请改用以下命令来启动 named 服务：

```
[root@serverA]# rcnamed start
```

# Linux 管理：入门指南

> 提示 如果你更改了 BIND 的配置文件（无论是主 `named.conf` 还是数据库文件），你将需要向 `named` 进程发送 HUP 信号来让它重新读取这些文件。首先找到 `named` 进程的进程 ID (`PID`)。可以通过查看 `/var/run/named/named.pid` 查找来实现。如果你在通常的位置没有看到它，可以运行以下命令来获取：

```
ps -C named
PID TTY TIME CMD
7706 ?
```

`PID` 列下的值是 `named` 进程的 ID。这就是你想要为其发送 HUP 信号的 PID。你可以通过输入 `# kill -HUP 7706` 来发送 HUP 信号。当然，请将 `7706` 替换为输出结果中的正确进程 ID。

- 17. 最后，你可能希望确保你的 DNS 服务器服务在下次重启期间能够启动。使用 `chconfig` 命令：

```
[root@serverA]# chconfig named on
```
在启用 systemd 的发行版中，你可以使用以下命令来确保 `named` 随系统启动自动启动：

```
[root@serverA]# systemctl enable named.service
```

下一节将介绍用于测试或查询 DNS 服务器的工具的使用。

## DNS 工具箱

本节描述了你在处理 DNS 时想要熟悉的几款工具。它们将帮助你更快地排排除故障。

### host

`host` 工具实际上是一个非常易用的实用程序。当然，它的功能可以通过与它的各种选项配合使用来扩展。其选项和语法在此处：

```
host [-aCdlrTw] [-c class] [-N ndots] [-t type] [-W time]
  -R hostname [server]
  -a 等于 -v t
  -c 指定非-IN 数据的查询类
  -C 比较权威名称服务器上的 SOA 记录
  -d 等于 -v
  -l 使用 AXFR 列出域中的所有主机
  -i 使用旧旧的 IN.INT 形式的 IPv6 反向查找
  -N 更改根查找前允许的圆点数量
  -r 禁用递归处理
```

# 第 16 章：DNS

- -R 指定 UDP 数据包的重试次数
- -t 指定查询类型
- -T 启用 TCP/IP 模式
- -v 启用详细输出
- -w 指定无限等待回复
- -W 指定等待回复的时间

在简单的用法中，`host` 允许你从命令行将主机名解析为 IP 地址。这里有一个示例：

```
[root@serverA ~]# host internic.net
internic.net has address 192.0.32.9
internic.net has IPv6 address 2600:2d0:200::9
internic.net mail is handled by 10 pechorax.icann.org.
```

你可以使用 `host` 执行反向查找。这里有一个示例：

```
[root@serverA ~]# host 198.41.0.6
6.0.41.198.in-arpa domain name pointer rs.internic.net.
```

`host` 命令也可以用于查询 IPv6 记录。例如，要查询（在其监听的 IPv6 接口上）针对主机 `server-v6.example.org` 的名称服务器 `()`，你可以运行以下命令：

```
[root@serverA ~]# host server-v6.example.org ::1
Using domain server:
Name: ::1
Address: ::1#53
Aliases:
server-v6.example.org has IPv6 address 2001:db8::2
```

要查询 `server-v6` 的 PTR 记录，你可以使用以下命令：

```
[root@serverA ~]# host 2001:db8::2 ::1
Using domain server:
Name: ::1
Address: ::1#53
Aliases:
2.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.8.b.d.0.1.0.0.2.ip6.arpa \
domain name pointer server-v6.example.org.
```

域名 `dig` 是收集 DNS 服务器信息的绝佳工具。该工具获得了 BIND 组的认可和官方印章。

### dig

其语法和某些选项所示（各种选项的含义请参见 `dig` 的 man页）：

```
dig [@global-server] [domain] [q-type] [q-class] {q-opt}
  {global-d-opt} host @local-server} {local-dopt}
  [ host @local-server] {local-dopt} [...]
其中：domain 位于域名命名系统中。
```

这里是 `dig` 的用法示例：

```
dig @server> domain query-type
```

在这里，`<server>` 是你想要查询的 DNS 服务器的名称，`domain` 是你感兴趣的域名，`query-type` 是你尝试获取的记录类型（A, MX, NS, SOA, HINFO, TXT, ANY 等）。例如，要从先先项目中设置的 DNS 服务器获取 `example.domain` 的 MX 记录，你将如下所示发布 `dig` 命令：

```
root@serverA # dig @example.org MX
```

要从本地 DNS 服务器查询 `yahoo.com` 的 A 记录，只需输入以下内容：

```
root@serverA # dig @localhost yahoo.com
```

注意，对于上述命令，我们没有指定 `query-type`——即我们没有显式指定 A 类型记录。`dig` 的默认行为是在未指定时假设你想要 A 类型记录。你可能注意到我们正在查询 `yahoo.com` 的 DNS 服务器。我们的服务器不是 `yahoo.com` 的权威，但由于将其配置为缓存 DNS 服务器，它可以从适当的服务器获取答案。

要查询 `server-v6.example.org` 的支持 IPv6 的 DNS 服务器的 AAAA 记录，输入：

```
root@serverA # dig @localhost server-v6.example.org -t AAAA
```

重新发布之前的命令，但这次抑制所有的详细输出（`+short`）：

```
root@serverA # dig +short @localhost yahoo.com
66.94.234
216.109
```

要查询 `192.168.1.1` 的反向查找（PTR RR）本地 DNS 服务器，输入：

```
root@serverA # dig -x 192.168.1.1 @localhost
```

要查询 `2001:db8::` 的 IPv6 反向查找（PTR RR）本地 DNS 服务器，输入：

```
[root@serverA ~]# dig -x 2001:db8:: @localhost
```

`dig` 程序非常强大。它的选项多到无法完全涵盖。阅读 man 页以了解如何使用它的某些功能。

### nslookup

`nslookup` 实用程序是你在各种系统中常见的工具之一，但对许多人来说是最熟悉的工具之一。它的用法非常简单，可以交互式和非交互式使用（即直接从命令行）。当命令未提供参数时，会进入交互模式。直接输入 `nslookup` 会进入 `nslookup` 壳。要退出交互模式，只需在 `nslookup` 提示符输入 `exit`。

> 提示 在交互模式下使用 `nslookup` 时，退出工具的命令是 `exit`。但大多数人会本能地发送 `quit` 命令退出。`nslookup` 会认为它被要求查询 "quit" 的 DNS。最终会超时。你可以在你的域文件中创建这样的 DNS 条目：

```
nslookup IN 127.0.0.1 CNAME quit
```

有了上述域文件条目，每当你的 DNS 服务器交互式查询 `nslookup` 并错误地发送 `quit` 命令时，用户将收到 "exit" 的提示。

非交互模式的用法总结如下：

```
nslookup [ -option ] [ name ] [ server ]
```

例如，使用非交互式 `nslookup` 查询本地 DNS 服务器关于 `www.example.org` 的信息，输入：

```
[root@serverA ~]# nslookup www.example.org localhost
Server: localhost
```
