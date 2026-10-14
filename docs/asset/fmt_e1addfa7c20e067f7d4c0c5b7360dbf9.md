
你可能考虑运行一个专用 syslog 服务器，该服务器上没有其他活动服务，只有 syslog 守护进程在运行。此外，你可以在面向互联网的防火墙上阻止 UDP 端口 514，以便主机不易从外部被淹没；当然，如果入侵者在利用你的一台服务器后在你的网络内部进行此操作，这就无济于事了。

### 提示

更偏执的设置是禁用对中央日志主机的所有登录，只保留控制台。这样，要访问存储在此服务器上的日志，人员就需要物理访问。

作为预防措施，至少你应考虑通过 `xinetd` 运行 syslog。这样，你就可以使用 `xinetd` 的访问控制功能（例如 `only_from` 列表），使 `syslogd` 仅记录来自受信任主机的消息。或者，你也可以使用 `iptables` 设置一些本地防火墙过滤规则。

理想情况下，你希望使用使用 TCP 而非 UDP 通信的 syslog 守护进程，以便数据传输可靠，不会丢失日志信息。此外，使用 TCP 流量时，你可以使用诸如 `ssh` 或 `stunnel` (http://www.stunnel.org) 之类的工具来保护 syslog 守护进程之间的流量。你可以使用名为 `syslog-ng`（syslog new generation）的替代 syslog 守护进程来实现这一点。

### 注意

`syslog-ng` v1.6 已包含在您的 SLES 9 介质中。默认情况下，安装的是传统的 syslog 而不是 `syslog-ng`，但您可以通过 YaST 轻松安装 `syslog-ng`。您可以从 http://www.balabit.com/downloads/syslog-ng 下载最新版本。

### 注意

SLES 9 中还包含一个名为 `evlog`（Enterprise Event Logging，企业事件日志）的软件包。`evlog` 实现了一个与 syslog 兼容的日志服务，符合草案 POSIX 标准 1003.25，“System API—Services for Reliable, Available, and Serviceable Systems。”请访问 http://evlog.sourceforge.net 了解更多信息。

`syslog-ng` 使用 `/etc/syslog-ng/syslog-ng.conf` 进行配置信息。该文件的结构与 syslog 使用的结构截然不同。您可能会发现配置 `syslog-ng` 比配置 syslog 需要多做一点工作，但这反映了它的灵活性。配置文件由五个部分组成：`options{}`、`source{}`、`destination{}`、`filter{}` 和 `log{}`。从语法上讲，`syslog-ng.conf` 与 `C` 及其他结构化编程语言非常相似。分号终止语句；空白被忽略，因此可用于增强可读性。以下是 `syslog-ng.conf` 的示例：

```
options {use_dns(yes); chain_hostnames(yes);};
source s_location {internal();};
destination d_log {tcp("myloghost" port(514));};
destination d_local {file("/var/log/messages");};
filter f_auth_messages {facility(auth, authpriv)
    and level(warning - emerg);};
log {source(s_location); destination(d_local);};
log {
    source(s_location);
    filter(f_auth_messages);
    destination(d_log);
};
```

该文件指示 `syslog-ng` 执行以下任务并设置以下信息：

- 该文件通过 DNS 将发送者的 IP 地址解析为主机名，并显示处理过日志消息的所有主机名称。
- 日志的来源在服务器内部（即来自 `syslog-ng` 本身）。
- 已定义了两个目标：一个是远程日志主机，`myloghost`，另一个是本地文件。
- 设置了一个过滤器，仅记录 `auth` 和 `authpriv` 消息，其优先级为 `warning` 或更高。
- 所有消息（任何类型或优先级）都存储在本地的 `/var/log/messages` 文件中。
- 类型为 `auth` 和 `authpriv` 且优先级等级为 `warning` 或更高（由于名为 `f_auth_messages` 的过滤器）的消息会被发送到远程日志主机。

当您理解各种关键字后，您会发现由于语法更易读，配置 `syslog-ng` 实际上比配置 `syslog` 更容易、更简单。

### 提示

您可以使用 `logger` 命令行工具来测试您的 syslog/`syslog-ng` 配置。`logger` 的语法很简单：

```
logger -p facility.priority "message"
```

您可以使用以下 shell 脚本来向内核设施发送每个八个优先级的测试消息：

```
#!/bin/sh
for i in {debug,info,notice,warning,err,crit,alert,emerg}
do
    logger -p kern.$i "Test kernel message, prio $i"

done
```

以下消息记录到 `/var/log/messages`：

```
Mar  5 16:07:33 Athena logger: Test kernel message, prio debug
Mar  5 16:07:33 Athena logger: Test kernel message, prio info
Mar  5 16:07:33 Athena logger: Test kernel message, prio notice
Mar  5 16:07:33 Athena logger: Test kernel message, prio warning
Mar  5 16:07:33 Athena logger: Test kernel message, prio err
Mar  5 16:07:33 Athena logger: Test kernel message, prio crit
Mar  5 16:07:33 Athena logger: Test kernel message, prio alert
Mar  5 16:07:33 Athena logger: Test kernel message, prio emerg
```

除了作为诊断工具之外，`logger` 对于向 shell 脚本添加日志功能特别有用。

尽管 `syslog-ng` 比 syslog 更安全，入侵者仍可因配置文件而发现存在单独的日志服务器，并使用某种形式的 DoS 攻击将其停用，或许还可以通过伪造地址劫持或转移日志流量。Honeynet 项目的 Lance Spitzner（http://www.honeynet.org）提出了一种有趣的——不是防黑客的，但概念上非常有趣的——隐蔽日志方法。使用此方法，您可以通过使用没有网络协议（如 TCP/IP）绑定到其网卡的主机来隐藏真正的日志目标。

## 隐蔽日志主机

隐蔽日志主机的运行理论基于这样一个事实：`syslogd` 被动接收消息，因为 syslog 消息使用无连接（单向）UDP 协议发送；发送主机在发送 syslog 消息时不需要 `syslogd` 的确认或任何形式的回复。因此，您配置发送主机上的 `syslog.conf` 文件以使用虚假但有效的 IP 地址作为远程日志主机。也就是说，IP 地址必须对您使用的网络编号方案有效，但不应被网络上的任何主机使用。对于充当中央日志主机的主机，您设置网络嗅探器，例如 Snort，以被动捕获流经线路上目标为 UDP 端口 514（syslog 协议端口）的数据包。

> **注意**
>
> 您不能使用 `tcpdump` 进行隐蔽日志记录，因为它基于数据包头而不是数据有效负载来过滤数据包。

Mick Bauer 在 2002 年 9 月的《Linux Journal》上撰写了一篇题为“Stealthful Sniffing, Intrusion Detection and Logging”的优秀文章，详细介绍了如何使用处于隐蔽模式的 Snort 来充当 `syslogd`。您可以在 http://www.linuxjournal.com/article/6222 找到在线版本。正如您在文章末尾的评论中所看到的，隐蔽日志记录不是防黑客的解决方案，但它确实引入了一些可能性。

如果您对隐蔽 syslog 主机的想法感兴趣，但不想费心设置 Snort 或数据包嗅探器，您可能想试试 `passlogd`。`passlogd` 是一个专为在没有开放端口的主机上运行而设计的 syslog 消息嗅探器。您可以在 http://www.morphine.com/void/src.html 找到最新版本。

> **注意**
>
