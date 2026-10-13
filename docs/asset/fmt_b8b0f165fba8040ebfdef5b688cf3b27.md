
swatch 工具设计用于监控日志文件并通知用户任何异常日志条目。`swatch` 有两种运行模式：批处理（batch）和监控（monitor）。批处理模式允许用户检查日志文件并退出，而监控模式将持续观察并评估每个新的条条目。当 `swatch` 检测到任何异常活动时，有几种方法可以通知用户。这包括终端响铃、电子邮件、向终端发送消息和颜色编码。`swatch` 工具需要 `Perl` 5 或更高版本才能运行，并在 `GPL` 下分发。`swatch` 的缺点是，如果多台计算机上需要保护，则在每台计算机上都必须运行一个 `swatch` 进程，除非日志记录到中央机器。此外，每个日志文件也必须运行一个 `swatch` 进程。

# 配置 swatch

运行 `swatch` 时可以使用各种命令行选项。`-r [+]:mm[am|pm]` 将在 hh 小时 mm 分钟后重启 switch，其中使用 `[+]` 将在从现在起经过 hh 小时 mm 分钟后重启 switch。`--input-record-separator =regular_expression` 将通过正则表达式字段中输入的字符来分离记录。`-t filename` 选项将持续监控文件名而不退出，而 `-f filename` 将通过 switch 文件并退出。

除了命令行选项外，还可以直接在 `swatch` 中输入其他选项。`swatch` 配置文件指定了 `swatch` 在监控单个日志文件时将采取的操作。

## Logcheck

`Logcheck` 是一种实用的工具，通过扫描日志文件来确定是否发生了值得调查的活动，从而检测潜在的安全漏洞。`Logcheck` 然后会将此类操作的报告通过电子邮件发送给系统管理员。利用 `logtail` 工具，`Logcheck` 在日志文件中搜索系统管理员关注的字符串。例如，当用户尝试反复输入无效密码来获取超级用户权限时，日志条目会反映此类登录尝试。此类条目会导致 `Logcheck` 向系统管理员发送尝试报告邮件。如果作为 `cron` 作业在后台运行，`Logcheck` 将节省系统管理员手动检查大量日志文件的繁琐工作。

`Logcheck` 需要一些配置。这包括对 `logcheck.sh` 文件进行许多更改，指示系统管理员的电子邮件地址并指定应该检查哪些日志文件。配置中最困难的部分是指定要在日志文件中查找的信息。由于不同 Linux 发行版的事件日志文件不同，除非系统管理员指定，否则 `Logcheck` 可能检测不到错误。例如，如果 `Logcheck` 搜索字符串 `LOGIN FAILURE`，但使用的 Linux 发行版失败登录尝试为 `AUTHENTICATION FAILURE`，它就不会提醒系统管理员。由于由于原因，系统管理员可能需要在配置 `Logcheck` 之前检查其日志文件，以确定哪些特定条目或报告值得关注。`Logcheck` 使用四个文件来确定哪些条目值得关注：`logcheck.hacking`、`logcheck.violations`、`logcheck.violations.ignore` 和 `logcheck.ignore`。这些文件按此顺序配置，并包含特定的搜索标准。`logcheck.hacking` 包含暗示攻击访问系统的字符串。活动系统攻击警报列在 `Logcheck` 报告中。日志包含包含恶意活动产生的字符串。这些违规将列在报告的安全违规部分。`logcheck.violations.ignore` 文件过滤掉那些本质上返回已在 `logcheck` 文件中详细说明字符串的操作。第四个文件 `logcheck.ignore` 包含所有应该被忽略的日志条目。任何不匹配 `logcheck.hacking`、`logcheck.violations` 和 `logcheck.ignore` 条目的日志条目都将列在 `Logcheck` 报告中的异常系统事件中。可以在 `www.psionic.com/abacus/logcheck` 获取 `Logcheck`。

# 服务监控

对于系统管理员来说，了解哪些服务正在运行、谁在运行这些服务以及哪些信息正在通过它们是非常重要的。`netstat` 和 `nmap` 等工具可以帮助用户理解正在使用的服务的存在及其来源。

## netstat

`netstat` 对系统网络资源的状态提供了详尽、有时甚至是深奥的描述。`netstat` 的目的是提供所有网络连接、正在使用的接口以及路由表的报告。

## netstat 选项

虽然 `netstat` 命令有有许多选项可用，但本节仅讨论了其中几个。要查看 `netstat` 的完整选项集和描述，请参考 `netstat` 的 man 页第 8 节。

表 3.6 描述了常用的 `netstat` 选项。

`netstat` 输出包含两个主要部分：活动 Internet 连接（TCP、UDP 和原始）和活动 域套接字（domain sockets）。每个部分都有自己的字段，并在 `netstat` 输出片段之后有更详细的描述。

| 表 3.6 netstat 选项 |
| 开关 (SWITCH) | 说明 (DESCRIPTION) |
| - | - |
| -a | 打印所有套接字的报告，包括正在监听的套接字 |
| -l | 仅打印监听状态套接字的报告 |
| --tcp/ -t | 打印使用 TCP 协议的套接字的报告 |
| --udp/ -u | 打印使用 UDP 协议的套接字的报告 |
| --raw/ -w | 打印仅使用原始数据协议的套接字的报告 |
| --programs/ -p | 打印包含使用该套接字的程序进程 ID (PID) 和名称的报告 |
| --interfaces/ -i | 打印网络接口报告 |
| --numeric/ -n | 打印用户 ID 和 IP 地址，而不是主机/用户名称 |
| --extend/ -e | 打印包含比通常更多信息（如 userID）的报告 |

# 第 3 章

```
doodle@lars wuffee:~ netstat -e
Active Internet Connections             State Owner Inode
Proto Recv-Q Send-Q Local Address        Foreign Address
tcp4        0       lars,sairino.com:*      TIME_WAIT wuffee
tcp4        0       lars,sairino.com:431  lars,sairino.com:4220 CLOSE_WAIT 25704
Active Internet Connections -e option turn server
Proto Return-Flags State             Local Queue
uudp      1      *      STREAM            CONNECTED 24027 0000002e
udp      1      *      STREAM            CONNECTED 24008 0000002e
uudp      1      J      STREAM            CONNECTED 23990 0000002c
uudp      1      *      STREAM            CONNECTED 24004 0000002a
uudp      1      *      STREAM            CONNECTED 24006 0000002f
```

图 3.2 netstat 输出。

# 理解 netstat 输出

图 3.2 是一个 `netstat` 会话示例，使用 `-e` 选项进行打印。

## 活动 Internet 连接

活动 Internet 连接部分包含三个项目，每个项目有八个字段。这些字段在表 3.7 中描述。

### 表 3.7 字段描述

| 字段 (FIELD) | 说明 (DESCRIPTION) |
|---|---|
| Proto | 指定套接字使用的协议（TCP、UDP 或原始 raw）。 |
| Recv-Q | 显示使用该套接字的程序尚未复制的字节。 |
| Send-Q | 显示使用该套接字的程序尚未确认的字节。 |
| Local Address | 本地机器的地址和套接字。 |
| Foreign Address | 远程机器的地址和套接字。 |
| State | 通常用于 TCP，可以是几种不同状态之一（描述见表 3.8）。 |
| User | 如果指定显示，则显示该套接字用户/所有者的用户名或 userID。 |
| Inode | 用于该套接字的程序的 inode 节点位置。 |

### 表 3.8 状态选项描述

| 状态 (STATE) | 说明 (DESCRIPTION) |
| --- | --- |
| Established | 该套接字有一个已的连接。 |
| SYN_Sent | 套接字正在尝试连接。 |
| SYN_Recv | 套接字已收到请求。 |
| FIN_Wait1 | 连接正在从本地端关闭。 |
| FIN_Wait2 | 连接正在等待从远程端关闭。 |
