
| `Modem` | `wvdial` 应作为调制解调器的设备。默认是 `/dev/modem`。 |

| `Baud` | `wvdial` 与调制解调器通信的速度。默认是 57,600 波 |

| `Init1` ... `Init9` | 指定调制解调器的初始化字符串。`wvdial` 最多可以使用 9 个。`Init1` 的默认是 `"ATZ"`。 |

| `Phone` | 你让 `wvdial` 拨出的电话号码。 |

| `Area Code` | 指定区号（如有）。 |

| `Dial Prefix` | 指定所需的拨号前缀——例如，70 用于禁用呼叫等待，9 用于外线。 |

| `Dial Command` | 指定拨号操作。默认是 `"ATDT`。 |

表 5-2. `wvdial` 变量

## 第 5 章：网络配置 83

| 变量 | 说明 |

| --- | --- |

| `Login` | 指定您在 ISP 处的用户名。 |

| `Login Prompt` | 如果您的 ISP 有不特殊的登录提示，您可以在此处指定。 |

| `Password` | 指定您在 ISP 处的密码。 |

| `Password Prompt` | 如果您的 ISP 有不特殊的密码提示，您可以在此处指定。 |

| `Force Address` | 指定要使用的静态 IP 地址（适用于向用户提供静态 IP 的 ISP）。 |

| `Remote Name` | 对于 PAP 或 CHAP 认证，您可能需要将其更改为 ISP 的认证名称。默认值为 \ 。 |

| `Carrier Check` | 在傻瓜模式（Stupid Mode）下，`wvdial` 不尝试解释终端服务器的提示，并在调制解调器启动后启动 pddp。将此选项设置为 No 将禁用调制解调器的载波检测。适用于报告载波线路始终离线的调制解调器。 |

| `Stupid Mode` | 在傻瓜模式下，`wvdial` 不尝试解释终端服务器的提示，并在调制解调器连接后启动 pddp。 |

| `Auto Reconnect` | 如果启用，当您被对方随机断开连接时，`wvdial` 会尝试自动重新连接。此选项默认开启。 |

表 5-2. `wvdial` 变量（续）

您可以使用 `wvdialconf` 实用为您自动创建一个默认的 `wvdial.conf` 文件。`wvdialconf` 会检测您的调制解调器并为基本功能设置默认值。您可以编辑 `wvdial.conf` 文件，并根据您的 ISP 拨号信息修改 `Phone`（电话）、`Username`（用户名）和 `Password`（密码）条目。删除前面的分号 (`;`) 可以取消条目的注释。任何以分号开头的行都会被忽略视为命令。

```
$ wvdialconf
```

您还可以创建一个命名的拨号器，如后续示例中的 `myisp`。如果您有不同的 ISP 需要登录，这非常有帮助。以下示例显示了 `/etc/wvdial.conf` 文件：

```
/etc/wvdial.conf
[Modem0]
Modem = /dev/tty0
```

# 红帽 Linux 8：完全参考手册

```
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

```
[Dialer myisp]
Username = chris
Password = myypassword
Modem = /dev/ttyS0
Phone = 555-5555
Area Code = 555
Baud = 57600
Stupid mode = 0
```

要启动 `wvdial`，请输入命令 `wvdial`，它随后将从 `/etc/wvdial.conf` 文件读取连接配置信息。`wvdial` 会拨号 ISP 并启动 PPP 连接，并在请求时提供您的用户名和密码。

> $ wvdial

您可以在 `/etc/wvdial.conf` 文件中为任意数量的连接设置配置。要选择其中一个，请将其标签作为 `wvdial` 命令的参数输入，如下：

> $ wvdial myisp

## 无线工具 (Wireless Tools)

为了避免为每个种类的无线设备提供不同的配置选项，大多数无线设备目前都支持无线扩展（Wireless Extensions）。这些扩展为配置所有无线设备提供了一种标准格式。使用同一组配置选项，您可以配置任何支持无线扩展的无线设备。`Wireless Tools` 包是一套安装在 Linux 系统上的用于无线设备的网络配置和报告工具。它们目前作为 Linux 无线扩展和无线工具项目的一部分接受支持和开发，这是一个惠普（Hewlett-Packard）维护的开源项目。

`Wireless Tools` 由此处列出的配置和报告工具组成：

# 第 5 章：网络配置

| 工具 | 说明 |

|---|---|

| `iwconfig` | 设置大多数无线设备的基本无线配置选项 |

| `iwlist` | 显示设备的当前状态信息 |

| `iwspry` | 测试移动 IP 支持 |

| `iwpriv` | 访问特定设备的配置选项 |

无线局域网设备将像以太网卡一样有一个以太网名称。`kmod` 会自动检测并加载相应的模块，将其别名列在 `/etc/modules.conf` 文件中。

`iwconfig` 的工作方式类似于 `ifconfig`，用于配置网络连接。新增的参数允许您设置无线特定的功能，例如网络名称 (`nwid`)、使用的频率或通道 (`freq` or `channel`) 以及传输比特率 (`rate`)。`iwconfig` 的手册页提供了所有接受参数的完整列表。这里列出了一些常用的参数：

| 参数 | 说明 |

|---|---|

| `ssid` | 网络名称 |

| `freq` or `channel` | 连接的频率或使用的通道 |

| `nwid` or `domain` | 网络 ID 或网域 |

| `mode` | 设备使用的工作模式，例如 ad hoc（自建）、managed（管理）或 auto（自动）；由网络结构（拓扑）决定 |

| `sens` | 灵敏度，可以接收数据的最低信号电平 |

| `key` or `enc` | 使用的加密密钥 |

例如，要为安装为第一个以太网设备的无线设备设置通道，您可以使用以下命令将通道设置为 2：

```
iwconfig eth0 channel 2
```

您也可以使用 `iwconfig` 显示无线设备的统计信息，就像 `ifconfig` 一样。输入不带参数的 `iwconfig` 命令或带有设备名称。

# 红帽 Linux 8：完全参考手册

无线局域网设备将像以太网卡一样有一个以太网名称。`kmod` 会自动检测并加载相应的模块，将其别名列在 `/etc/modules.conf` 文件中。

`iwconfig` 的工作方式类似于 `ifconfig`，用于配置网络连接。新增的参数允许您设置无线特定的功能，例如网络名称 (`nwid`)、使用的频率或通道 (`freq` or `channel`) 以及传输比特率 (`rate`)。`iwconfig` 的手册页提供了所有接受参数的完整列表。这里列出了一些常用的参数：

| 参数 | 说明 |

|---|---|

| `ssid` | 网络名称 |

| `freq` or `channel` | 连接的频率或使用的通道 |

| `nwid` or `domain` | 网络 ID 或网域 |

| `mode` | 设备使用的工作模式，例如 ad hoc（自建）、managed（管理）或 auto（自动）；由网络结构（拓扑）决定 |

| `sens` | 灵敏度，可以接收数据的最低信号电平 |

| `key` or `enc` | 使用的加密密钥 |

例如，要为安装为第一个以太网设备的无线设备设置通道，您可以使用以下命令将通道设置为 2：

```
iwconfig eth0 channel 2
```

您也可以使用 `iwconfig` 显示无线设备的统计信息，就像 `ifconfig` 一样。输入不带参数的 `iwconfig` 命令或带有设备名称。

# 无线工具

为了避免为每个种类的无线设备提供不同的配置选项，大多数无线设备目前都支持无线扩展。这些扩展为配置所有无线设备提供了一种标准格式。使用同一组配置选项，您可以配置任何支持无线扩展的无线设备。`Wireless Tools` 包是一套安装在 Linux 系统上的用于无线设备的网络配置和报告工具。它们目前作为 Linux 无线扩展和无线工具项目的一部分接受支持和开发，这是一个惠普（Hewlett-Packard）维护的开源项目。

`Wireless Tools` 由此处列出的配置和报告工具组成：

## 物理配置
