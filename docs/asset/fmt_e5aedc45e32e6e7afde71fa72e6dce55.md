
```text
Chain FORWARD (policy DROP 0 packets, 0 bytes)

pkt bytes target prot opt in out source/destination

1 67 6050 ACCEPT all -- any anywhere any anywhere  \
state RELATED, ESTABLISHED

2 0 0 ACCEPT tcp -- eth1 eth0 selected.remote.host \
host1.private.lan tcp spts:1024:65535 dpts:ssh \
flags:SYN,RST,ACK,SYN state NEW

3 0 0 ACCEPT tcp -- eth0 eth1 .private.lan \
mailserver.dmz.lan multiportdports smtp,pop3 tcp spts:1024:65535 \
flags:SYN,RST,ACK,SYN state NEW

4 1 60 ACCEPT tcp -- eth0 eth1 .private.lan \
web-proxy.dmz.lan multiportdports http,https tcp spts:1024:65535 \
flags:SYN,RST,ACK,SYN state NEW

5 1 60 ACCEPT tcp -- eth0 eth1 .private.lan \
anywhere tcp spts:1024:65535 dpts:ssh \
flags:SYN,RST,ACK,SYN state NEW

6 0 0 ACCEPT tcp -- eth0 eth1 .private.lan \
news-server.net tcp spts:1024:65535 dpt:nttp \
flags:SYN,RST,ACK,SYN state NEW

7 0 0 REJECT tcp -- eth1 any anywhere \
.private.lan tcp spts:1024:65535 dpt:auth \
reject-with icmp-port-unreachable

8 0 0 ACCEPT icmp -- any any anywhere \
anywhere icmp fragmentation-needed

9 2 168 ACCEPT icmp -- eth0 eth1 .private.lan \
anywhere icmp echo-request

10 0 0 ACCEPT tcp -- any any anywhere \
anywhere tcp flags:FIN,ACK,FIN,ACK

11 0 0 ACCEPT tcp -- any any anywhere \
anywhere tcp flags:RST,RST

12 0 0 LOG all -- any any anywhere \
anywhere LOG level warning
```

# FORWARD 链规则说明

`FORWARD` 链的默认策略是 `DROP`。被拒绝的数据包会被直接丢弃，不会向本地或远程程序返回任何通知。该链上共有 12 条规则：

- **第 1 行** — 任何被识别为属于先前已建立（`ESTABLISHED`）连接或交换的一部分的数据包，或与之一相关（`RELATED`）的数据包，均允许双向通过。
- **第 2 行** — 允许来自特定远程主机的传入 SSH 连接连接到私有 LAN 中的 `host1`。
- **第 3 行** — 允许向 DMZ 中的邮件网关和 pop 服务器发起的出站客户端连接。
- **第 4 行** — 允许向 DMZ 中的 Web 代理发起的出站客户端连接（包括 HTTP 和 HTTPS）。
- **第 5 行** — 允许向任何位置的远程 SSH 服务器发起的出站客户端连接。
- **第 6 行** — 允许向特定远程新闻服务器发起的出站客户端连接。
- **第 7 行** — 拒绝向本地 ident 服务器发起的传入 `auth` 请求。
- **第 8 行** — 允许双向的 ICMP 类型 3 需要分片（`fragmentation-needed`）消息，作为 MTU 大小发现的一部分。
- **第 9 行** — 允许向任何位置发送出站 ping ICMP `echo-request`。
- **第 10 行** — 双向接受 `FIN/ACK` 数据包。
- **第 11 行** — 双向接受 TCP `RST` 数据包。
- **第 12 行** — 所有其他双向数据包在被默认策略丢弃之前都会被记录日志。

在这种情况下，`-v` 选项通常有助于查看传入和传出网络接口名称。`eth0` 是连接到 `.private.lan` 网络的内部接口。`eth1` 是连接到 `.dmz.lan` 及其后互联网的外部接口。请记住，无论是否有 NAT，都需要 `FORWARD` 规则。还要记住，任何 NAT 规则都是在 `nat` 表中定义的。这些规则是在默认的 `filter` 表中定义的。

## 针对防火墙规则测试单个数据包

规则检查命令，即 `ipchains` 中的 `-C` 命令，尚未在 `iptables` 中实现。

## 解释系统日志

`syslogd` 是记录系统事件的服务守护进程。`syslogd` 的主要系统日志文件是 `/var/log/messages`。许多程序使用 `syslogd` 的标准日志服务。其他程序，如 Apache Web 服务器，维护自己单独的日志文件。

## syslog 配置

并非所有日志消息都同等重要——甚至有趣。这正是 `/etc/syslog.conf` 发挥作用的地方。配置文件 `/etc/syslog.conf` 允许您根据需求调整日志输出。

消息按照产生它们的子系统进行分类。在 `man` 手册页中，这些类别被称为 *设施*（参见表 8.1）。

### 表 8.1 SYS 日志设施类别

| 设施 | 消息类别 |
| :--- | :--- |
| auth 或 security | 安全/授权 |
| authpriv | 私有安全/授权 |
| cron | cron 守护进程消息 |
| daemon | 系统守护进程生成的消息 |
| ftp | FTP 服务器消息 |
| kern | 内核消息 |
| lpr | 打印机子系统 |
| mail | 邮件子系统 |
| news | 网络新闻子系统 |
| syslog | syslogd 生成的消息 |
| user | 用户程序生成的消息 |
| uucp | UUCP 子系统 |

在任何给定的设施类别中，日志消息被划分为 *优先级* 类型。优先级按重要性递增的顺序列于表 8.2 中。

### 表 8.2 SYS 日志消息优先级

| 优先级 | 消息类型 |
| :--- | :--- |
| debug | 调试消息 |
| info | 信息性状态消息 |
| notice | 正常但重要的状况 |
| warning 或 warn | 警告消息 |
| err 或 error | 错误消息 |
| crit | 严重状况 |
| alert | 需要立即关注 |
| emerg 或 panic | 系统不可用 |

`syslog.conf` 中的条目指定了日志设施、优先级以及消息写入的位置。并不明显的是，优先级具有包含性。它意味着包含该优先级及所有更高优先级的消息。例如，如果你指定错误优先级的消息，则包含错误及更高优先级（即 `crit`、`alert` 和 `emerg`）的所有消息。

日志可以写入设备（如控制台），也可以写入文件和远程机器。

## /var/log 中日志文件的提示

`syslogd` 不会创建文件。它只写入已存在的文件。如果日志文件不存在，你可以使用 `touch` 命令创建它，然后确保它由 `root` 拥有。出于安全目的，日志文件通常不可被普通用户读取。特别是安全日志文件 `/var/log/secure`，仅由 `root` 可读。

以下两个条目将所有内核消息写入控制台和 `/var/log/messages`。消息可以复制到多个目的地：

```
kern.*	/dev/console
kern.*	/var/log/messages
```

此条目将 `panic` 消息写入所有默认位置，包括 `/var/log/messages`、控制台以及所有用户终端会话：

```
*.emerg
```

接下来两个条目将与 root 权限和连接相关的身份验证信息写入 `/var/log/secure`，并将用户授权信息写入 `/var/log/auth`。由于优先级定义为 `info` 级别，`debug` 消息不会被写入：

```
authpriv.info	/var/log/secure
auth.info	/var/log/auth
```

接下来两个条目将一般守护进程信息写入 `/var/log/daemon`，并将邮件流量信息写入 `/var/log/maillog`：

```
daemon.notice	/var/log/daemon
mail.info	/var/log/maillog
```
