
## Systemd 服务事件记录机制

解释 `Systemd` 服务如何使用不同的方法记录事件。`Systemd` 服务包使用 `systemd-journald` 应用，它不使用 `syslog` 协议来记录事件。相反，`systemd-journal` 创建了它自己的二进制日志文件来存储事件消息。二进制日志文件经过索引，以便对事件进行更快的搜索。`journalctl` 应用提供了向日志文件发送搜索查询并显示搜索结果的接口。

### 复习题

1. 哪种协议成为 `Linux` 中跟踪系统事件消息的事实标准？
    - A. `SMTP`
    - B. `FTP`
    - C. `NTP`
    - D. `syslog`
    - E. `journalctl`

2. Nancy 想编写一个 `rsyslogd` 规则，将来自系统作业调度器的事件消息分离到单独的日志文件中。她应该使用哪个 `syslog` 设施关键字？
    - A. `cron`
    - B. `user`
    - C. `kern`
    - D. `console`
    - E. `local0`

3. 在 `rsyslogd` 中哪种 `syslog` 严重性级别的优先级最高？
    - A. `crit`
    - B. `alert`
    - C. `emerg`
    - D. `notice`
    - E. `err`

4. 哪种 `syslog` 严重性级别代表正常但重要的状态消息？
    - A. `crit`
    - B. `notice`
    - C. `info`
    - D. `alert`
    - E. `local0`

5. 哪种 `syslog` 应用以速度极快而闻名？
    - A. `syslogd`
    - B. `syslog-ng`
    - C. `systemd-journald`
    - D. `klogd`
    - E. `rsyslogd`

6. `rsyslogd` 应用默认使用哪个配置文件？
    - A. `rsyslog.conf`
    - B. `journald.conf`
    - C. `syslog.conf`
    - D. `rsyslog.d`
    - E. `vslog.d`

7. James 需要将所有严重级别为警告或更高的内核消息记录到单独的日志文件中。他应该使用什么设施和优先级设置？
    - A. `kern.warn`
    - B. `kern.*`
    - C. `*.info`
    - D. `kern.warn`
    - E. `kern.alert`

8. Barbara 想确保日志文件在 `Linux` 系统下次重启后仍然保存。她应该使用哪个 `systemd-journal` 配置设置？
    - A. `Storage=auto`
    - B. `Storage=persistent`
    - C. `ForwardToSyslog=on`
    - D. `Storage=volatile`
    - E. `ForardToSyslog=off`

9. Katie 想在她的 `Linux` 系统日志中显示最近的条目。她应该使用哪个 `journalctl` 选项？
    - A. `-a`
    - B. `-l`
    - C. `-r`
    - D. `-e`
    - E. `-n`

10. Tony 正在尝试排除 `Linux` 系统上应用程序产生的错误，但必须翻阅日志文件中的大量条目才能找到它们。哪种 `journalctl` 匹配选项可以帮助他仅显示与特定应用程序相关的日志记录？
    - A. `OBJECT_PID`
    - B. `Kernel`
    - C. `_TRANSPORT`
    - D. `_UID`
    - E. `_UDEV`

# 第 18 章 管理 Linux 防火墙

## 目标 3.5：给定一个场景，实施并配置 Linux 防火墙

![img1](img/0c1e7d2699b9d354c8d2f84669d18d73_542_0.png)
![img2](img/0c1e7d2699b9d354c8d2f84669d18d73_543_0.png)

建筑中的防火是指防火墙，有助于防止火灾在整个结构中蔓延。在计算机安全中，防火墙防止意外、未经授权或恶意网络流量的传播。

防火墙以不同的形式实现。你可以通过使用多种结构提供分层安全。防火墙可以是硬件设备或软件应用程序，是基于网络或基于主机的，以及网络层或应用层的过滤器。在本章中，我们将查看基于主机并运行在网络层的软件应用程序防火墙。

## 提供访问控制

防火墙为你的系统或网络提供访问控制。防火墙内部实现的访问控制列表 (`ACL`) 识别哪些网络包被允许进入或离开。这通常被称为`包过滤`。

> **注意**：不要将防火墙 `ACL` 与 `Linux` 文件和目录 `ACL` 混淆，后者在第 15 章中介绍过。`setfacl` 和 `getfacl` 等命令与防火墙无关。

防火墙 `ACL` 通过将控制信息与其他网络数据进行对比来识别网络包。这可能包括以下信息：

- 源地址
- 目的地址
- 网络协议
- 入口端口
- 出口端口
- 网络状态

一旦匹配设施且优先级高于或等于定义的严重性被发送到应用程序，或将事件消息发送到日志文件、将消息管道到远程主机或系统上的用户。

## 熟悉防火墙

防火墙服务提供了数据包过滤，并为 `GUI` 环境和命令行提供了用户界面。它支持 `IPv4` 以及 `IPv6`，以及更多功能。您可以在防火墙官方网站 <https://www.firewalld.org/> 上找到更多细节。

此防火墙服务被称为动态防火墙守护进程，因为您可以在不需要重启服务的情况下更改 `ACL` 规则。这些规则通过其 `D-Bus` 接口瞬时加载。

![img3](img/0c1e7d2699b9d354c8d2f84669d18d73_546_0.png)

`D-Bus` 是消息总线守护进程。它在系统级或按会话层级在任何两个应用程序之间提供通信服务。它还可以注册以接收事件通知，使其成为一个强大的通信工具。防火墙服务使用 `dbus` Python 库来集成 `D-Bus` 服务。

防火墙的核心部分是区域（`zones`）。网络流量被分组到预定义的区域集或区域中。每个区域都有一个配置文件，定义了该规则集（也称为信任级别）。流量分组可以是系统的网络接口或源地址范围，用于识别来自其他系统的流量。每个网络连接在一次只能属于一个区域。

默认情况下，防火墙区域配置文件存储在 `/usr/lib/firewall/zones/` 目录下。自定义或用户创建的区域配置文件存储在 `/etc/firewall/zones/` 目录下。表 18.1 显示了使用防火墙连接的系统中预定义的区域。这些区域按照从低信任到高信任顺序列出。

### 表 18.1 预定义的区域

| 名称 | 描述 |
| :--- | :--- |
| `drop` | 丢弃所有传入数据包。仅允许出站连接。 |
| `block` | 仅接受源自系统的网络连接。拒绝传入数据包并回发 `icmp` 消息。 |
| `public` | 仅接受指定的传入连接。通常用于公共环境，即其他系统不受信任。 |
| `external` | 功能与 `public` 类似，但通常用于外部网络，且对本地系统启用了伪装（`masquerading`）。 |
| `dmz` | 功能与 `public` 类似，但用于非军事化区，该区域可公开访问，且对内部网络的访问受到限制。 |
| `work` | 接受指定的传入连接。通常用于工作环境，即网络上的其他系统大多是信任的。 |
| `home` | 功能与 `work` 类似，但用于家庭环境，即网络上的其他系统大多是信任的。 |
| `internal` | 功能与 `work` 类似，但通常用于内部网络，即网络上的其他系统大多是信任的。 |
| `trusted` | 接受所有网络连接。 |

`firewall-cmd` 工具允许您查看并与各种防火墙设置交互。例如，要查看所有预定义的区域，使用 `--get-zones`，如列表 18.1 中的 `CentOS` 所示。

### 列表 18.1 使用 firewall-cmd 命令查看预定义的区域

```bash
$ firewall-cmd --get-zones
block dmz home internal public work
$ ls /usr/lib/firewall/zones
block.xml drop.xml public.xml work.xml dmz.xml external.xml trusted.xml
$
```

> **提示**：防火墙配置文件使用可扩展标记语言 (`XML`)。虽然您可能倾向于直接编辑这些文件，但最好使用防火墙工具来修改和管理配置。

`Network Manager` 也与防火墙集成。因此，当通过 `NetworkManager` 添加新网络设备时，防火墙会自动将其分配给默认区域。默认区域通常预设为 `public` 区域，但可以通过 `firewall-cmd` 进行自定义。您可以像列表 18.2 所示查看系统当前的默认区域。

### 列表 18.2 使用 firewall-cmd 命令查看默认区域

```bash
$ firewall-cmd --get-default-zone
public
$
```

![img4](img/0c1e7d2699b9d354c8d2f84669d18d73_547_0.png)

## 查看防火墙

如果您需要不同的默认区域，可以对其进行更改。只需使用超级用户权限并采用 `--set-default-zone=` 选项即可。

您还可以查看所有当前激活的区域及其流量分组。只需如列表 18.3 所示使用 `--get-active-zones`。

### 列表 18.3 使用 firewall-cmd 命令查看激活的区域
