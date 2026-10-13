
# 网络报告与故障排除 • 第 47 章

> 提示：网页显示应用程序名称的顺序与 `portlist.txt` 文件中的定义顺序相同。这意味着你应该将想要看到的端口定义列在 `portlist` 文件的前面的部分，以避免滚动网页来查看它们。

- 3. 创建好 `portlist` 文件后，导航到 Admin | Configure | Startup Options。
- 4. 点击 [IP Preferences](#) 链接。
- 5. 在 `TCP/UDP Protocols To Monitor` 字段中，指定 `portlist.txt` 的完整路径。
- 6. 停止并重启 `ntop` 进程使更改生效。

你可以限制额外的 `ntop` 页面。如果你希望人员在查看任何 `ntop` 页面时提供用户名和密码，可以通过导航到 Admin | Configure | Protect URLs 来配置。点击底部的 Add URL，然后在不向字段填写任何内容的情况下点击 Add URL 按钮。这将对所有 `ntop` 页面进行密码保护。

`Ntop` 将所有活动数据存储在 RAM 中，如果系统重置，你将丢失所有数据。有一种将数据存储到磁盘的机制。预警告，将所有数据记录到磁盘可能会消耗大量磁盘空间，因此需要仔细监控。`Ntop` 将数据存储在 RRD 文件（循环数据库）中。你可以通过导航到 Plugins | Round-Robin Databases | Describe 来配置 RRD 插件。`active` 列应显示 Yes；如果是 No，请点击 No 切换为活动。为了帮助你决定将精力集中在哪些报告工具上，表 7.1 突出了我们讨论的工具的各种功能。

![](img/0eb7273a8d9e486628f6e18d37ab22c6_432_0.png)

## 第 7 章 • 网络报告与故障排除

### 表 7.1 报告工具功能

| 报告工具功能 | | | | |
|---|---|---|---|---|
| MZL & Novatech MRTG | 流量统计 | PRTG | ntop | |
| SNMP 嗅 | | ✓ | | |
| Netflow | | | ✓ | ✓ |
| Linux | ✓ | | | |
| Windows | ✓ | | | ✓ |
| 限制性 | 不支持报告自定义 | 3 个传感器限制 | 仅限数据 |
| 注释 | 支持 Netware | | | |

### 在 Windows 主机上启用 SNMP

内容很多需要消化，让我们在 Windows 系统上启用 SNMP 代理并看看它能为我们做什么。要在 Windows XP 上启用 SNMP 代理，请遵循以下步骤。

- 1. 导航到 Start | Settings | Control Panel。
- 2. 打开 Add or Remove Programs。
- 3. 在窗口左侧选择 Add/Remote Windows Components。
- 4. 突出 Management and Monitoring Tools，但不要勾选它。
- 5. 点击 Details。
- 6. 在 Simple Network Management Protocol 旁边打勾，并点击 OK。
- 7. 点击 Next 然后点击 Finish。

接下来，你需要在 Windows 主机上配置特定的 SNMP 设置。请按照以下步骤操作。

- 1. 点击 Start | Run 并输入 `services.msc` 打开服务程序色插。

![](img/0eb7273a8d9e486628f6e18d37ab22c6_433_0.png)

- 2. 双击右侧面板中的 SNMP Service 。
- 3. 选择 Agent 选项卡。
- 4. 输入 Contact 信息和 Location 信息。这些信息用作从管理控制台查看时的系统标识符。
- 5. 打开 MMC。
- 6. 选择 Computer Management。
- 7. 展开 Management 并选择 Services。
- 8. 右键点击该服务。
- 9. 选择 Properties。
- 10. 选择 Services 选项卡。
- 11. 选择 Security 选项卡。
- 12. 点击 Add。
- 13. 输入社区名称。
- 14. 点击 OK。
- 15. 点击 Apply。
- 16. 点击 OK。
- 17. 点击 Finish。

团体字符串将被设置为 `labcommunitystring`。显然，你应该选择一个你自己的安全密码。这种类型的配置文件既快速又方便，但安全性并不高。

你还可以使用 `netfilter` 防火墙和/或 `tcpwrappers` 根据通信系统的 IP 地址来限制 SNMP 访问。另一种选项是使用 SNMP 守护进程内置的控制功能。要配置 `snmpd` 访问，你需要编辑 `snmpd.conf` 文件。授予 SNMP MIB 访问权限需要四个基本步骤，这些步骤都在配置文件中完成。下面的示例包含了各种配置设置，希望此让你对这些可能性有一个直观的了解。将以下几行添加到配置文件中。

![](img/0eb7273a8d9e486628f6e18d37ab22c6_437_0.png)

```
## sec.name source community

##

com2sec localhost snmplocalstring

com2sec internal 10.0.0.0/8 snmpcommunitystring

com2sec admin_net 192.168.1.0/24 snmpadminstring
```

这些行将团体名称映射到安全名称，因此 `com2sec` 指令引用了你正在授予的访问权限。安全名称只是一个名称，可以使用任何你喜欢的。源（source）是使用该访问配置方案的主机。你也可以使用 `default` 作为源，这意味着任何 IP 地址。团体（community）是用于该访问的团体字符串。请注意，只读团体字符串和读写团体字符串之间没有区别。这是因为安全名称将拥有的访问将在配置文件的后续定义。

![](img/0eb7273a8d9e486628f6e18d37ab22c6_437_1.png)

```
## Access.group.name sec.model sec.name

##

group Full_Group v1 local

group RO_Group v2c internal

group Full_Group any admin_net
```

下一节使用 `group` 指令将安全名称映射到组名。在这种情况下，我们将 `local` 安全名称和 `admin_net` 安全名称都映射到了同一个组（Full_Group）。`sec.model` 决定将使用/允许哪个版本的 SNMP（1 或 2）。使用版本 3 需要完全不同的配置。

![](img/0eb7273a8d9e486628f6e18d37ab22c6_437_2.png)

```
## MIB.name  incl/excl  MIB.subtree  mask

##

view all-mibs      included .1

view limited      included .1.3.6.1.2.1.2
```

这一部分定义了一个视图（view），它基本上定义了 MIB 的一部分。`all-m` 视图包含整个 MIB 树，而 `limited` 视图仅包含 .1.3.6.1.2.1.2 部分，部分由网络接口和相关指标组成。你可以配置给定视图的 MIB 子树包含或排除。通过排除，你可以省略 MIB 树的敏感部分。如果需要，可以使用 MIB 名称代替数字。在上面使用的示例中，你可以使用 `included .1.3.6.1.2.1.2`，也可以使用此命令：`included .iso.org.dod.internet.mgmt.2.interfaces`。掩码（mask）是 MIB 树上的可选位，指定用于索引访问的匹配位。默认（无掩码）仅匹配视图中指定的位。你通常使用掩码来匹配表中的特定行或多行。在本示例中，`all-mibs` 视图可以访问 .1 及其下的所有内容。

```
## MIB.group.name  .sect.model  sec.level  prefix  write  notify

access  Full_Group ""  any  noauth  0 all-mins none none

access  RO_Group ""  any  noauth  0 limited none none
```
