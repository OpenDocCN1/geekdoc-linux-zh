
如果您想手动开启或关闭网络连接，可以使用网络设备控制工具 (`system-control-network`)，路径为“系统 | 管理 | 网络设备控制”（见图 28-20）。您所有的连接都将列出来（许多系统只有一个）。您可以点击“禁用 (`Deactivate`)” 按钮关闭选定的活动连接，点击“激活 (`Activate`)” 按钮开启它。点击“配置 (`Configure`)” 按钮将启动 `system-config-network`，允许您配置选定的设备（见下节）。

74df054815dc70d661e97bc3d5ff87a_678_0.png

图 28-20：网络设备控制

## 命令行 PPP 访问：dial

如果由于某种原因，您无法在桌面上设置调制解调器连接，您可能需要从命令行界面进行设置。对于拨号 PPP 连接，您可以使用 `wvdial` 拨号器，它是一个更智能的拨号器，不仅拨号 ISP 服务，还能执行登录操作并提供您的用户名和密码。

`wvdial` 程序从 `/etc/wvdial.conf` 文件加载配置。在这里，您可以放置调制解调器和账户信息，包括调制解调器速度和服务详情，以及 ISP 电话号码、用户名和密码。`wvdial.conf` 文件分为多个部分，以括号括起的节标签开始。部分包含带有赋值值的参数变量，例如 `username = chris`。默认部分包含其他部分继承的默认值，因此您不需要重复它们。表 28-2 列出了 `wvdial` 变量。

您可以使用 `wvdial` 工具自动为您创建一个默认的 `wvdial.conf` 文件；`wvdialconf` 会检测您的调制解调器并为基本功能设置默认值。然后您可以编辑 `wvdial.conf` 文件并修改 `Phone`、`Username` 和 `Password` 项以您的 ISP 拨号信息。移除前面的分号 (`;`) 可以取消取消注释。任何以分号开头的行都会被视为注释。

```
$ wvdialconf
```

### 678 第 6 部分：网络支持

| 变量 | 说明 |
| --- | --- |
| Inherits | 显式继承自指定的节。默认情况下，节继承自 `[Dialer Defaults]`（拨号默认设置）。 |
| Modem | `wdial` 应作为调制调器的设备。默认为 `/dev/modem`。 |
| Baud | `wdial` 与调制调器通信的速度。默认为 57,600 波特。 |
| Init1..Init9 | 指定调制调器使用的初始化字符串；`wdial` 可以使用多达 9 个。`Init1` 的默认值为 `"ATZ"`。 |
| Phone | 你希望 `wdial` 拨号的电话号码。 |
| Area Code | 指定区码（如果有）。 |
| Dial Prefix | 指定任何所需的拨号前缀——例如，用 70 禁用等待等待或用 9 使用外线。 |
| Dial Command | 指定拨号操作。默认为 `"ATDT"`。 |
| Login | 指定你在 ISP（服务提供商）使用的用户名。 |
| Login Prompt | 如果你的 ISP 有不常见的登录提示，你可以在此处指定。 |
| Password | 指定你在 ISP 使用的密码。 |
| Force Address | 指定要使用的静态 IP 地址（用于向用户提供静态 IP 地址的 ISP）。 |
| Stupid Mode | 在简单模式下，`wdial` 不尝试解释来自终端服务器的提示，并在调制调器连接后启动 `ppp`。 |
| Auto Reconnect | 如果启用，当连接被对方随机断开时，`wdial` 会尝试自动重新连接。此选项默认开启。 |

**表 28-2：wdial 变量**

```
/etc/wdial.conf

[Modem0]
Modem = /dev/ttyS0
Baud = 57600
Init1 = ATZ
SetVolume = 0
Dial Command = ATDT
```

```
[Dialer Defaults]
Modem = /dev/ttyS0
Baud = 57600
Init1 = ATZ
SetVolume = 0
Dial Command = ATDT
```

你也可以创建一个命名称的拨号器，例如示例中的 `wisp`。如果你有不同的 ISP 需要登录，这非常有帮助。以下示例显示了 `/etc/wdial.conf` 文件：

要启动 `wvdial`，输入命令 `wvdial`，它将从 `/etc/wvdial.conf` 文件读取连接信息；`wvdial` 会拨号 ISP 并启动 PPP 连接，在需要时提供你的用户名和密码。

```
$ wvdial
```

你可以在 `/etc/wvdial.conf` 文件中为任意数量的连接设置配置。要选择其中一个，请将其标签作为参数输入 `wvdial` 命令，如下：

```
$ wvdial myisp
```

## 使用 Wireless Tools 进行手动无线配置

`NetworkManager` 会自动为 GNOME 和 KDE 桌面环境检测并配置你的无线连接。你可以使用 Network Manager 中的无线工具，以及 `system-config-network`（无线属性）和 `ifconfig` 手动配置你的连接。之前的章节已讨论过使用 Network Manager 和 `system-config-network` 进行无线配置。

无线配置使用同一组无线扩展（Wireless Extensions）。`Wireless Tools` 包是一组安装在 Linux 系统上的用于无线设备的网络配置和报告工具（`wireless-tools`）。它们目前作为 Linux 无线扩展和无线工具项目的一部分受到支持和开发，该项目是由惠尔惠公司维护的开源项目。

`Wireless Tools` 包含此处列出的配置和报告工具：

| 工具 | same |
| --- | --- |
| `iwconfig` | 设置大多数无线设备的基本无线配置选项。 |
| `iwlist` | 显示设备的当前状态信息。 |
| `iwspry` | 设置无线网络中的 IP 地址列表并检查连接质量。 |
| `iwpriv` | 访问特定设备的配置选项。 |

### iwconfig

`iwconfig` 命令的工作方式与 `ifconfig` 类似，用于配置网络连接。它是连接向导（Connection Wizard）和 `system-config-network` 用于配置无线网卡的工具。或者，你也可以直接在命令行运行 `iwconfig` 并指定某些参数。新增的参数允许你设置无线特定功能，例如网络名称 (`wname`)、频率或通道 (`freq` 或 `channel`) 以及传输比特率 (`rate`)。请查看 `iwconfig` 手页以获取接受参数的完整列表。常用参数列在表 28-3 中。

例如，为安装为第一个以太网设备的无线设备设置通道，你会使用以下命令，将通道设置为 2：

```
iwconfig eth0 channel 2
```

你也可以使用 `iwconfig` 显示无线设备的统计信息，正如 `ifconfig` 的功能一样。不带参数输入 `iwconfig` 命令或输入设备名称。将列出名称、频率、敏感度和比特率等信息。同时检查 `/proc/net/wireless` 以获取统计信息。

与其直接使用 `iwconfig` 设置参数，你可以在无线设备的配置文件中指定它们。无线设备配置文件将位于 `/etc/sysconfig/network-scripts` 目录下，名称类似于 `ifcfg-eth1`，取决于设备名称。此文件已包含许多 `iwconfig` 设置。任何进一步设置可以通过将 `IWCONFIG` 参数赋值为 `iwconfig="rate 11M"` 来，如下：

```
IWCONFIG="rate 11M"
```

| 参数 | 说明 |
| --- | --- |
| essid | 网络名称 |
| freq | 连接频率 |
| channel | 通道 |
| rate | 传输比特率 |

表 28-3：常用参数

`iwconfig` 命令的工作方式与 `ifconfig` 类似，用于配置网络连接。它是连接向导和 `system-config-network` 用于配置无线网卡的工具。或者，你也可以直接在命令行运行 `iwconfig` 并指定某些参数。新增的参数允许你设置无线特定功能，例如网络名称 (`wname`)、频率或通道 (`freq` 或 `channel`) 以及传输比特率 (`rate`)。请查看 `iwconfig` 手页以获取接受参数的完整列表。常用参数列在表 28-3 中。

例如，为安装为第一个以太网设备的无线设备设置通道，你会使用以下命令，将通道设置为 2：

```
iwconfig eth0 channel 2
```

你也可以使用 `iwconfig` 显示无线设备的统计信息，正如 `ifconfig` 的功能一样。不带参数输入 `iwconfig` 命令或输入设备名称。将列出名称、频率、敏感度和比特率等信息。同时检查 `/proc/net/wireless` 以获取统计信息。
