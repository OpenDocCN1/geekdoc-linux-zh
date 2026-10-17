
IWCONFIG="frag. 512"

## 虚拟专用网络

虚拟专用网络允许你在物理网络连接（如互联网）之上创建属于自己的逻辑网络。通过加密，你的私有网络传输将保持安全，不受物理网络的影响。尽管虚拟虚拟专用网络 (VPN) 本身没有自己的物理连接，也不是一个真实的网络，但它发送的加密传输实现了如同该网络作为一个独立实体存在的效果。VPN 利用隧道技术，即安全传输直接通过互联网等大型网络上的互连系统发送，而不会被拦截，或在任何一点被转译。要实现 VPN，每个节点都必须使用相同的加密支持软件。在 Fedora 上，你可以选择使用 IPsec 工具。要使用 IPsec 建立 VPN，点击 `system-config-network` 中的 IPsec 面板并创建一个新连接。

## 接口配置脚本：`/etc/sysconfig/network-scripts`

通过 Internet 配置向导和 `system-config-network` 实现的网络配置保存在 `/etc/sysconfig/network-scripts` 目录下的接口配置脚本中。你可以直接编辑这些脚本来更改特定参数，正如之前讨论无线连接时那样。接口配置文件以当前配置的网络接口命名，例如第一个以太网设备的 `ifcfg-eth0`，或者第一个 PPP 调制解调器设备的 `ifcfg-ppp0`。这些文件定义了 shell 变量，用于存储接口信息，例如是否在引导启动时启动它们。例如，`ifcfg-eth0` 文件包含了 `NETWORK`、`BROADCAST` 和 `IPADDR` 的定义，这些值被分配给设备使用的网络地址、广播地址和 IP 地址。你也可以手动编辑这些接口配置文件，如之前针对无线连接那样进行更改。这里显示了一个使用 DHCP 地址的 `ifcfg-eth0` 示例。

`/etc/sysconfig/network-scripts/ifcfg-eth0`

```
DEVICE=eth0
BOOTPROTO=DHCP
HWDDADDR=00:00:00:EF:AF:00
ONBOOT=yes
TYPE=Ethernet
```

## 命令行 PPP 访问：`wvdial`

如果出于某种原因，你无法在桌面上设置调制解调器连接，你可能需要从命令行界面进行设置。对于拨号 PPP 连接，你可以使用 `wvdial` 拨号器，它是一个智能拨号器，不仅可以拨号 ISP 服务，而且可以在不被拦截或在任何一点被转译的情况下，直接通过互联网等大型网络上的互连系统发送安全传输。要使用 VPN 建立 VPN。你可以使用该设备上的 `system-config-network` 修改标准设置。你也可以直接修改此文件以输入额外参数，例如频率 (`FREQ`) 或敏感性级别 (`SENS`)。你还可以使用 `IWCONFIG` 选项指定任何 `iwconfig` 参数。输入 `IWCONFIG` 后跟一个带有值的选项赋值。例如，以下选项设置了数据包的分片阈值：

```
IWCONFIG="frag. 512"
```

第 14 章：网络配置 455

你也可以创建一个命名的拨号器，如以下示例中的 `myisp`。如果你有不同的 ISP 需要登录。以下示例显示了 `/etc/wvdial.conf` 文件：

| 变量 | 描述 |
| :--- | :--- |
| 继承 | 默认的拨号器。 |
| Modem | `wvdial` 应该使用的调制解调器设备。 |
| Baud | `wvdial` 与 modem 通的速度。默认是 57600。 |
| Init1 | modem 使用初始化字符串。默认是 "ATZ"。 |
| Phone | 你想让 `wvdial` 拨号的号码。 |
| Area Code | 指定任何区号。 |
| Dial Prefix | 指定任何需要的拨号前缀——例如用于外线的 9。 |
| Dial Command | 指定拨号操作。默认是 "ATDT"。 |
| Login | 指定 ISP 使用的用户名。 |
| Login Prompt | 如果 ISP 有特殊的登录提示，你可以在这里指定。 |
| Password | 指定 ISP 使用的密码。 |
| Force Address | 指定使用的静态 地址（对于提供静态地址的 ISP）。 |
| Stupid Mode | 在简单模式下，`wvdial` 不尝试解释终端提示并在 modem 连接后启动 ppp。 |
| Auto Reconnect | 如果启用，当连接随机断开时，`wvdial` 将尝试重新建立连接。此选项默认开启。 |

表 14-2：`wvdial` 变量

你也可以创建一个命名的拨号器，如以下示例中的 `myisp`。这对于你有不同的 ISP 需要登录非常有帮助。以下示例显示了 `/etc/wvdial.conf` 文件：

要启动 `wvdial`，输入命令 `wvdial`，连接 ISP 提供用户名和密码。

```
[Modem0]
Modem = /dev/ttyS0
Baud = 57600
Init1 = ATZ
SetVolume = 0
Dial Command = ATDT
```
