

# 表 10.15 xinetd 的标志（Flags）

| 标志 | 描述 |
| :--- | :--- |
| `-d` | 调试模式。输出结果可用于诸如 gdb 这样的调试器。 |
| `-syslog facility` | 指定 syslog 设备。可以是 daemon、auth、user、local0–7 之一。 |
| `-filelog file` | 指定写入日志的文件，代替 syslog。必须使用绝对路径。 |
| `-f config_file` | 指定配置文件。必须使用绝对路径。默认值为 /etc/xinetd.conf。 |
| `-pid` | 将 PID 写入标准错误。 |
| `-loop rate` | 指定每秒分叉的守护进程数量。默认为 10。对于较快的机器，您可能希望更改此值。 |
| `-reuse` | 设置 TCP 套接字为可重用，这意味着在前一个实例运行时可以启动其他守护进程。当此选项与 flags 属性结合使用时，您可以对服务进行更具体的控制（参见第 232 页的表 10.10）。 |
| `-limit numproc` | 限制由 xinetd 启动的并发运行进程的总数为 numprocs。 |
| `-logprocs limit` | 限制并发 RFC1413 请求的数量为 limit。 |
| `-shutdownprocs limit` | 当使用 log_on_failure 属性的 RECORD 值时，xinetd 会分叉一个名为 shutdown 的服务来收集服务终止时的信息。此选项将并发运行的 shutdown 进程总数限制为 limit。 |
| `-cc interval` | 强制 xinetd 每隔 interval 秒对其内部状态执行一次一致性检查。也可以手动通过 killall -IOF xinetd 来实现。 |

# 表 10.16 xinetd 的信号

| 信号 | 动作 |
| :--- | :--- |
| SIGUSR1 | 软重新配置。重新读取 /etc/xinetd.conf 并相应调整。 |
| SIGUSR2 | 硬重新配置。重新读取 /etc/xinetd.conf 并终止所有不再符合配置文件中规定条件的守护进程。例如，如果客户端连接到服务器，并且该客户端被添加到 no_access 列表中，则该信号将终止该客户端的会话。 |
| SIGQUIT | 终止 xinetd，而不终止其分叉的任何守护进程。 |
| SIGTERM | 终止 xinetd 分叉的所有守护进程；然后终止 xinetd。 |
| SIGHUP | 将 xinetd 状态信息转储到 /tmp/xinetd.dump。 |
| SIGIO | 检查内部数据库是否损坏并报告结果。 |

任何服务——协议、socket_type、type 或 wait——发生变化时，每当您向 xinetd 发出软或硬重新配置信号时，都会写入如示例 10-56 所示类型的日志条目。该特定示例是硬重新配置的结果。注意，由于这次硬重新配置，一个服务被终止了（通过 dropped=1 标识）。

# **示例 10-56 xinetd 硬重新配置的日志记录**

```
Apr 15 14:42:31 topcat xinetd[1402]: Starting hard reconfiguration
Apr 15 14:42:31 topcat xinetd[1402]: rereading service services
Apr 15 14:42:31 topcat xinetd[1402]: rereading service services
Apr 15 14:42:31 topcat xinetd[1402]: rereading service telnet
Apr 15 14:42:31 topcat xinetd[1402]: rereading service shell
Apr 15 14:42:31 topcat xinetd[1402]: rereading service login
Apr 15 14:42:31 topcat xinetd[1402]: rereading service talk
Apr 15 14:42:31 topcat xinetd[1402]: rereading service ntalk
Apr 15 14:42:31 topcat xinetd[1402]: rereading service pop-2
Apr 15 14:42:31 topcat xinetd[1402]: rereading service pop-3
Apr 15 14:42:31 topcat xinetd[1402]: rereading service imap
Apr 15 14:42:31 topcat xinetd[1402]: rereading service linuxconf
Apr 15 14:42:31 topcat xinetd[1402]: rereading service ftp
Apr 15 14:42:31 topcat xinetd[1402]: Reconfigured: new=1 old=12 dropped=1 (services)
```

# 注意

> 截至本文撰写时，确保读取修改后的 `/etc/xinetd.conf` 文件的最可靠方法是停止并重启 `xinetd` 守护进程。最好使用 **SIGTERM** 信号（或使用类似于第 230 页示例 10-38 中给出的脚本）来终止 `xinetd`。如本节所述，向 `xinetd` 发送 **SIGTERM** 会导致其终止（通过 **SIGKILL** 或信号号 9）其控制下的所有守护进程。有时在 `xinetd` 的子进程终止之前会有延迟，这意味着，如果您杀死并立即重启 `xinetd`，它可能无法绑定到所有端口（与此相关的错误消息将记录在 `xinetd` 的日志文件中，**而不是为该服务指定的日志文件**）。这就是为什么示例 10-38 中的脚本在停止和启动命令之间会出现 sleep 3 命令的原因。您可以通过对 TCP 服务（如 telnet 和 ftp）使用 **flags = REUSE** 属性和值，或向 `xinetd` 本身指定 `-reuse` 选项来完全避免此问题。

### 我该使用哪一个？

`xinetd` 的主要缺点已在第 228 页的 *`xinetd` 的缺点* 中列出。其中最重要的一个可能是 `xinetd` 目前不是任何主要 Linux 发行版的一部分。从根本上说，这意味着需要在每个希望安装它的系统上付出额外的管理努力。当然，每次升级时这都会产生额外的影响。虽然这类问题很重要，但如果您采用第 18 章中概述的建议，可能会在一定程度上缓解这些问题。

对于任何暴露在不受信网络（如互联网）中的系统，`xinetd` 的一个显著优点是它能够限制运行的守护进程数量以及接受的日志数据量。这使得针对此类受保护系统的 DoS 攻击变得更加困难。此外，将服务绑定到特定接口并将服务代理到另一主机的能力，对于某些暴露在互联网上的系统是一个有用的功能。通常，调用 tcpd 和日志记录的能力使其对所有系统都有用。也许有一天它会取代 inetd。

另一方面，**TCP_wrappers** 和 **inetd** 作为 Linux 的一部分由大多数供应商分发。因此，管理成本较低。此外，**TCP_wrappers** 被广泛使用并且非常成熟。**TCP_wrappers** 和 **inetd** 曾经并继续接受广泛的关键审查。不要低估工具的这一方面，因为它可能对计算环境的安全产生重大影响。一如既往，定期检查 *bugtraq*、*comp.unix.security* 和其他类似资源（见附录 A）应作为您管理活动的一部分。

由于 **xinetd**、**inetd** 和 **portmap** 可以和平共存（只要它们不试图同时提供相同的服务——见第 231 页的警告），在某些情况下使用这些工具的组合可能具有优势。无论如何，您实施的工具或工具组合都应该是您整体安全策略的一部分（见第 2 章）。

一般来说，在那些最可能遭受攻击的系统以及任何关键任务系统上运行 **xinetd** 可能更合理。您是否应该在所有地方安装 **xinetd**，取决于您的安全策略和您有多少时间。

## 总结

我们在这一章讨论了很多内容！我们研究了 **inetd** 和 **TCP_wrappers**，以及 **portmapper** 及其 **访问** 控制机制。我们以 **xinetd** 的讨论作为结束。虽然 **xinetd** 提供了许多特性和好处，但我们注意到它配置和维护起来更复杂，并且缺乏 **inetd** 的成熟度。

我们还指出，无论您使用哪种机制，消除所有未被您的安全策略明确允许的服务都是重要的。确保封装所有允许的服务并充分利用访问控制。使用 **i_chains** 和/或其他提供额外保护的工具。最后，确保定期阅读各种工具生成的日志文件。

## 延伸阅读

### TCP_Wrappers 的资源

所有文件都在源树的顶级目录中：

