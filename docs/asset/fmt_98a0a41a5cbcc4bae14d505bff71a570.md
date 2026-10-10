
当你需要查找日志中的特定事件条目时，`journalctl` 命令非常有用；它允许你使用 `matches` 过滤事件，并使用 `options` 确定如何显示它们，如列表 17.3 所示。

列表 17.3：`journalctl` 命令的输出

```bash
[rich@localhost]$ journalctl -r -TRANSPORT=kernel
-- Logs begin in Fri 2019-02-08 12:47:04 EST, and et...
Feb 08 12:48:36 localhost.localdomain kernel: TCP: IP registered
Feb 08 12:47:17 localhost.localdomain kernel: fuse unit (API version 7.22)
Feb 08 12:47:43 localhost.localdomain kernel: port 1(virbr0-nic)
Feb 08 12:47:43 localhost.localdomain kernel: IPv6: ADDRCONF (NETDEV_UP)
```

这让深挖日志变得简单多了！

练习 17.1 将演示如何在向日志设施发送消息时监控系统。

### 练习 17.1 创建日志或日志条目

此练习演示了如何创建日志或日志条目，并在 `rsyslog` 和 `systemd-journal` 中查看它。

1. 登录你的 Linux 图形桌面并打开两个新的提示符窗口。如果你使用虚拟终端，请打开两个独立的终端会话。
2. 在一个命令行窗口或终端会话中开始监控标准日志。在 Ubuntu 上，使用 `sudo tail -f /var/log/syslog`。对于基于 Red Hat 的系统，使用 `sudo tail -f /var/log/messages`。
3. 在第二个命令行窗口或终端会话中，使用命令 `logger` 创建日志事件：`This is a test log entry.`。
4. 观察第一个窗口或终端会话中的输出。你应该会在日志末尾看到新的日志条目。
5. 如果你使用 Fedora 或 CentOS 等基于 Red Hat 的发行版，使用命令 `journalctl -r` 查看日志末尾。你应该也能在日志中看到你的日志事件消息。

## 考试要点

描述大多数 Linux 日志应用使用的日志协议。`syslog` 协议已成为大多数 Linux 日志应用的事实标准。它使用设施代码（facility code）识别事件定义事件类型，并使用严重性（severity）定义事件消息的重要性。`syslogd`、`syslog-ng` 和 `rsyslog` 应用使用 `syslog` 协议管理 Linux 中的系统和应用程序事件。

描述 `rsyslog` 应用如何将事件重定向到特定位置。`rsyslog` 应用使用 `/etc/rsyslog.conf` 配置文件来定义处理事件的规则。每个规则指定了设施、严重性以及要执行的操作。匹配设施且优先级高于或等于定义的严重性的事件将发送到应用程序，或将事件消息发送到日志文件、将消息管道到远程主机或系统上的用户。

解释 `Systemd` 服务如何使用不同的方法记录事件。`Systemd` 服务包使用 `systemd-journald` 应用，它不使用 `syslog` 协议来记录事件。相反，`systemd-journal` 创建了它自己的二进制日志文件来存储事件消息。二进制日志文件经过索引，以便对事件进行更快的搜索。`journalctl` 应用提供了向日志文件发送搜索查询并显示搜索结果的接口。

## 复习题

- 1. 哪种协议成为 Linux 中跟踪系统事件消息的事实标准？

A. `SMTP`
B. `FTP`
C. `NTP`
D. `syslog`
E. `journalctl`

- 2. Nancy 想编写一个 `rsyslogd` 规则，将来自系统作业调度器的事件消息分离到单独的日志文件中。她应该使用哪个 `syslog` 设施关键字？

A. `cron`
B. `user`
C. `kern`
D. `console`
E. `local0`

- 3. 在 `rsyslogd` 中哪种 `syslog` 严重性级别的优先级最高？

A. `crit`
B. `alert`
C. `emerg`
D. `notice`
E. `err`

- 4. 哪种 `syslog` 严重性级别代表正常但重要的状态消息？

A. `crit`
B. `notice`
C. `info`
D. `alert`
E. `local0`

- 5. 哪种 `syslog` 应用以速度极快而闻名？

A. `syslogd`
B. `syslog-ng`
C. `systemd-journald`
D. `klogd`
E. `rsyslogd`

- 6. `rsyslogd` 应用默认使用哪个配置文件？

A. `rsyslog.conf`
B. `journald.conf`
C. `syslog.conf`
D. `rsyslog.d`
E. `vslog.d`

- 7. James 需要将所有严重级别为警告或更高的内核消息记录到单独的日志文件中。他应该使用什么设施和优先级设置？

A. `kern.warn`
B. `kern.*`
C. `*.info`
D. `kern.warn`
E. `kern.alert`

- 8. Barbara 想确保日志文件在 Linux 系统下次重启后仍然保存。她应该使用哪个 `systemd-journal` 配置设置？

A. `Storage=auto`
B. `Storage=persistent`
C. `ForwardToSyslog=on`
D. `Storage=volatile`
E. `ForardToSyslog=off`

- 9. Katie 想在她的 Linux 系统日志中显示最近的条目。她应该使用哪个 `journalctl` 选项？

A. `-a`
B. `-l`
C. `-r`
D. `-e`
E. `-n`

- 10. Tony 正在尝试排除 Linux 系统上应用程序产生的错误，但必须翻阅日志文件中的大量条目才能找到它们。哪种 `journalctl` 匹配选项可以帮助他仅显示与特定应用程序相关的日志记录？

A. `OBJECT_PID`
B. `Kernel`
C. `_TRANSPORT`
D. `_UID`
E. `_UDEV`

# 第 18 章

# 管理 Linux 防火墙

- 目标 3.5：给定一个场景，实施并配置 Linux 防火墙。

![](img/0c1e7d2699b9d354c8d2f84669d18d73_542_0.png)

![](img/0c1e7d2699b9d354c8d2f84669d18d73_543_0.png)

建筑中的防火是指防火墙，有助于防止火灾在整个结构中蔓延。在计算机安全中，防火墙防止意外、未经授权或恶意网络流量的传播。

防火墙以不同的形式实现。你可以通过使用多种结构提供分层安全。防火墙可以是硬件设备或软件应用程序，是基于网络或基于主机的，以及网络层或应用层的过滤器。在本章中，我们将查看基于主机并运行在网络层的软件应用程序防火墙。

# 提供访问控制

防火墙为你的系统或网络提供访问控制。防火墙内部实现的访问控制列表 (ACL) 识别哪些网络包被允许进入或离开。这通常被称为`包过滤`。

> 不要将防火墙 ACL 与 Linux 文件和目录 ACL 混淆，后者在第 15 章中介绍过。`setfacl` 和 `getfacl` 等命令与防火墙无关。

防火墙 ACL 通过将控制信息与其他网络数据进行对比来识别网络包。这可能包括以下信息：

- 源地址
- 目的地址
- 网络协议
- 入口端口
- 出口端口
- 网络状态

# 熟悉防火墙

防火墙服务提供了数据包过滤，并为 GUI 环境和命令行提供了用户界面。它支持 `IPv4` 以及 `IPv6`，以及更多功能。您可以在防火墙官方网站 `https://www.firewalld.org/` 上找到更多细节。

此防火墙服务被称为动态防火墙守护进程，因为您可以在不需要重启服务的情况下更改 ACL 规则。这些规则通过其 `D-Bus` 接口瞬时加载。

![](img/0c1e7d2699b9d354c8d2f84669d18d73_546_0.png)

`D-Bus` 是消息总线守护进程。它在系统级或按会话层级在任何两个应用程序之间提供通信服务。它还可以注册以接收事件通知，使其成为一个强大的通信工具。防火墙服务使用 `dbus` Python 库来集成 `D-Bus` 服务。

防火墙的核心部分是区域（zones）。网络流量被分组到预定义的区域集或区域中。每个区域都有一个配置文件，定义了该规则集（也称为信任级别）。流量分组可以是系统的网络接口或源地址范围，用于识别来自其他系统的流量。每个网络连接在一次只能属于一个区域。

默认情况下，防火墙区域配置文件存储在 `/usr/lib/firewall/zones/` 目录下。自定义或用户创建的区域配置文件存储在 `/etc/firewall/zones/` 目录下。表 18.1 显示了使用防火墙连接的系统中预定义的区域。这些区域按照从低信任到高信任顺序列出。

## 表 18.1 预定义的区域

| 名称 | 描述 |
| :--- | :--- |
| `drop` | 丢弃所有传入数据包。仅允许出站连接。 |
| `block` | 仅接受源自系统的网络连接。拒绝传入数据包并回发 `icmp` 消息。 |
| `public` | 仅接受指定的传入连接。通常用于公共环境，即其他系统不受信任。 |
| `external` | 功能与 `public` 类似，但通常用于外部网络，且对本地系统启用了伪装（masquerading）。 |
| `dmz` | 功能与 `public` 类似，但用于非军事化区，该区域可公开访问，且对内部网络的访问受到限制。 |
| `work` | 接受指定的传入连接。通常用于工作环境，即网络上的其他系统大多是信任的。 |
| `home` | 功能与 `work` 类似，但用于家庭环境，即网络上的其他系统大多是信任的。 |
| `internal` | 功能与 `work` 类似，但通常用于内部网络，即网络上的其他系统大多是信任的。 |
| `trusted` | 接受所有网络连接。 |

`firewall-cmd` 工具允许您查看并与各种防火墙设置交互。例如，要查看所有预定义的区域，使用 `--get-zones`，如列表 18.1 中的 CentOS 所示。

## 列表 18.1 使用 firewall-cmd 命令查看预定义的区域

```bash
$ firewall-cmd --get-zones
block dmz home internal public work
$ ls /usr/lib/firewall/zones
block.xml drop.xml public.xml work.xml dmz.xml external.xml trusted.xml
$
```

> 防火墙配置文件使用可扩展标记语言 (XML)。虽然您可能倾向于直接编辑这些文件，但最好使用防火墙工具来修改和管理配置。

`Network Manager` 也与防火墙集成。因此，当通过 `NetworkManager` 添加新网络设备时，防火墙会自动将其分配给默认区域。默认区域通常预设为 `public` 区域，但可以通过 `firewall-cmd` 进行自定义。您可以像列表 18.2 所示查看系统当前的默认区域。

## 列表 18.2 使用 firewall-cmd 命令查看默认区域

```bash
$ firewall-cmd --get-default-zone
public
$
```

![](img/0c1e7d2699b9d354c8d2f84669d18d73_547_0.png)

# 查看防火墙

如果您需要不同的默认区域，可以对其进行更改。只需使用超级用户权限并采用 `--set-default-zone=` 选项即可。

您还可以查看所有当前激活的区域及其流量分组。只需如列表 18.3 所示使用 `--get-active-zones` 选项。

## 列表 18.3 使用 firewall-cmd 命令查看激活的区域

```bash
$ firewall-cmd --get-active-zones
public
  interfaces: enp0s8
```

> 如果需要，可以使用图形化防火墙配置工具 `firewall-config` 代替命令行工具。通常在系统的 GUI 搜索框中输入 `Firewall` 即可轻松找到它。

除了区域外，防火墙还使用了服务（services）。服务是针对特定提供服务（如 `DNS`）的预定义配置集。配置信息可能包含端口列表、协议等项目。例如，`DNS` 服务配置集表示 `DNS` 在端口号 53 上同时使用 `TCP` 和 `UDP` 协议。列表 18.4 显示了 CentOS 发行版上各种预定义服务的片段。

## 列表 18.4 使用 firewall-cmd 命令查看预定义的服务

```bash
$ firewall-cmd --get-services
...
amanda-client amanda-k5-client bacula bacula-client
...
dhcp dhcpv6 dhcpv6-client dns docker-registry
...
```

```bash
$ ls -1 /usr/lib/firewall/services
amanda-client.xml
amanda-k5-client.xml
bacula-client.xml
bacula.xml
...
dhcp.xml
dns.xml
...
```

使用防火墙服务可以为特定的提供的系统服务提供更简单的防火墙配置，因为您只需将其分配给一个区域。示例见列表 18.5。

## 列表 18.5 将 DNS 服务分配给 dmz 区域

```bash
# firewall-cmd --add-service=dns --zone=dmz
success
#
# firewall-cmd --list-services --zone=dmz ssh dns
#
```

![](img/0c1e7d2699b9d354c8d2f84669d18d73_549_0.png)

> 在紧急情况下，您可以通过防火墙快速禁用所有网络流量。使用超级用户权限并在命令行执行 `firewall-cmd --panic-on` 命令。一旦情况平稳，可以通过输入 `firewall-cmd --panic-off` 重新启用网络流量。

当您修改防火墙配置时，默认情况下修改的是运行时环境（runtime environment）。运行时环境是防火墙正在使用的配置。

另一个防火墙环境是永久环境（permanent environment）。该环境是存储在配置文件中的配置。它在系统启动（或防火墙重启或重载时）被加载，并成为激活的运行时环境。

这两个防火墙环境都有其用途。永久环境适用于生产环境，而运行时配置适用于测试防火墙更改。

如果您在运行时环境中测试了防火墙更改并希望使其生效，这很容易实现。只需使用超级权限执行 `firewall-cmd --runtime-to-permanent` 命令即可。如果您认为运行时环境配置修改是正确的，可以在 `firewall-cmd` 命令后添加 `--permanent` 选项。这将更改添加到运行时和永久环境中。

> `iptables` 服务不应与防火墙一起运行。这在系统中很容易查出来。使用超级用户权限并输入 `systemctl show --property=Conflicts firewall` 命令。您将在输出中看到 `iptables.service` 作为冲突项。此外，虽然 `iptables` 命令在许多防火墙系统中仍然可用，但不应启用它。不要使用 `iptables` 命令，而应使用 `firewall-cmd` 或 `firewall-config` 工具来设置和管理您的防火墙配置。

## 调查 iptables

`iptables` 防火墙服务使用一种称为“链”（chains）的序列来处理进入系统的网络数据包。链决定了数据包在进入 Linux 系统到达相应应用程序时经过的路径。当应用程序将数据包发送到网络上的远程客户端时，这些数据包也会参与其中。图 18.1 显示了 Linux 系统上处理网络数据包涉及的不同链。

图 18.1 数据包处理链

![](img/0c1e7d2699b9d354c8d2f84669d18d73_550_0.png)

注意图 18.1，有不同的链来处理数据包：

- `PREROUTING` 在路由决策过程之前处理数据包。
- `INPUT` 处理目标为本地系统的数据包。
- `FORWARD` 处理转发到远程系统的数据包。
- `POSTROUTING` 在转发过滤之后，处理发送到远程系统的数据包。
- `OUTPUT` 处理从本地系统输出的数据包。

每个链都包含了一些定义了处理数据包规则的表（tables）。共有五类：

- `filter` 应用规则来允许或阻止数据包离开该链。
- `mangle` 应用规则在数据包离开该链之前更改数据包的特征。
- `nat` 应用规则在数据包离开该链之前更改数据包的地址。
- `raw` 对不需要被跟踪的的数据包应用 `NOTRACK` 设置。
- `security` 应用强制性访问控制规则。

实施网络地址转换 (NAT) 需要 `nat` 表在 `OUTPUT` 链中修改数据包的地址。实施防火墙要稍微复杂一些，因为在过程中你需要将 `filter` 表应用到 `INPUT`、`OUTPUT` 和 `FORWARD` 链上。这在处理过程中提供了多个阻止数据包的位置。

每个链还具有一个策略值（policy value）。该策略条目定义了当没有规则适用于数据包时，该链默认如何处理该数据包。共有两种不同的策略值：

- `ACCEPT`：将数据包传递给下一个链。
- `DROP`：不将数据包传递给下一个链。

你用于查看和更改 `iptables` 服务中链和过滤器的工具是 `iptables` 命令。表 18.2 显示了常用的 `iptables` 命令行选项。

## 表 18.2 iptables 命令的常用选项

| 选项 | 描述 |
| :--- | :--- |
| `-L [chain]` | 列出此链中的规则。如果没有指定链，则列出所有链中的所有规则。 |
