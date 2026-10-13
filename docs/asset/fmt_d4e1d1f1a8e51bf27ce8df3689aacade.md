
按下回车键后，你将看到 13.10 所示的主对话框。

# 第 13 章 网络连接

![](img/446debe023486a07fde575245cf7a3ff_473_0.png)

**图 13.10** Red Hat 的 `lokkit` 命令可以快速在 Linux 内存中生成防火墙规则。

选择一种模式，例如 `High`（高）、`Medium`（中）或 `No Firewall`（无墙）。使用 `High` 安全模式对外部访问提供最大的保护和限制；仅启用 DNS 查询和 DHCP 访问（用于自动网络配置）。如果你想启用 SSH、FTP、HTTP、telnet 或 NFS，可以使用 `Medium` 安全模式。显然，`No Firewall` 设置将使你的系统处于无保护状态。

使用 `Customize`（自定义）按钮选择接口（如 `eth0`）或更多服务（如 DHCP、SSH、Telnet（不推荐）、HTTP、Mail 或 FTP）允许通过该接口。完成后，使用 `Customize` 对话框中的 `OK` 按钮然后在主对话框中同样操作。你的防火墙规则将立即在内存中生效。

## Red Hat Linux 与防火墙

Red Hat Linux 还支持较旧但流行的 `iptchains` 包过滤软件，用于在 Red Hat Linux 防火墙、网关和工作站上构建有效的防火墙规则。Red Hat Linux 还支持更强大的 `iptables` `NetFilter` 系统，它为构建规则或过滤指令提供了额外的控制和日志功能。

遗憾的是，Red Hat Linux 没有包含任何可以使用的命令行或图形界面实用程序来构建、保存和测试复杂的 `iptables` 规则集（除了 `lokkit` 在 `/etc/sysconfig` 下生成的基本规则之外）。许多经验丰富的 Linux 用户会针对高级网络情况下的特定应用程序手动调优规则，例如路由规则开发和多个网络的桥接。这超出了本章的范围。虽然没有办法能阻止一个想要进入你计算机或网络的严重黑客，但有很多方法可以增加他的破解难度，并在他尝试时向你发出警告。本节将讨论系统弱点，并重点介绍 Red Hat Linux 自带的你可以立即使用的安全工具。

## 安全您的网络

正在生成数据库...
*** 正在处理 Unix 文件系统 ***

...
写入数据库文件：`/var/lib/tripwire/shuttle2.twd`
数据库已成功生成。

请注意，并非所有输出都显示在这里。在 Tripwire 创建其数据库（它是您文件系统的快照）后，它将使用此基准，结合 `/etc/tripwire` 目录下的加密配置和策略设置来监控系统的状态。然后，您应该使用所需的选项在完整性检查模式下启动 Tripwire。（详情请参阅 Tripwire 手册。）例如，您可以让 Tripwire 检查您的系统，然后在命令行生成报告，如下所示：

```
# tripwire -m c
```

此处未显示输出，但在本示例中将显示报告。输出可以重定向到文件，但报告将保存为 `/var/lib/tripwire/report/hostname-YYYYMMDD-HHMMSS.twr`（换句话说，使用您的主机名、年、月、时、分和秒）。可以使用 `twprint` 工具读取此报告，如下所示：

```
# twprint --report-report -r /var/lib/tripwire/report/shuttle2-20020119-181049.twr | less
```
