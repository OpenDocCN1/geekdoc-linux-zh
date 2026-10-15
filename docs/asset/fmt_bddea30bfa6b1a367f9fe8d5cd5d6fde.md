
## 表 A-1. 信息性系统消息和系统错误的位置

| Apple OS X | `Console` OS X 创建的所有各种日志文件的存储库。 | 应用程序 | 实用程序 | Console |
| MS Windows | `Event viewer` 显示有关计算机的各种重要信息。用于故障排除问题和错误。记录系统错误和其他事件。 | 开始 | 控制面板 | 系统和维护 | 事件查看器 |

## 表 A-2. 不同平台上的 OSI 上层问题排查

| 症状与目标 | 平台 | 工具、修复和需要检查的项目 |
| :--- | :--- | :--- |
| TCP/IP：验证和查看 TCP/IP 配置信息 | MS Windows | `ipconfig` 用于显示、操作各种 TCP/IP 配置参数——例如，查看运行 Windows 操作系统的本地 STA 当前 TCP/IP 设置：<br>`ipconfig /all`<br>该命令将显示 IP 地址、子网掩码、DNS 服务器地址、网关地址以及运行 Windows 操作系统的无线 主机名。 |
|  | Apple OS X | `ifconfig` 用于显示和操作 Macintosh 系统网络接口的 TCP/IP 配置信息 |
|  | FOSS/Linux | `ifconfig` Windows 中的 ifconfig 命令。<br>`ip` 用于显示和操作 FOSS 系统的 TCP/IP 配置、路由功能。 |
| 验证和查看无线配置特定信息 | FOSS/Linux | `iw` 查看所有无线设备的能力以及 频段信息，使用：<br>- `iw list`<br>要查看无线设备的无线监管域信息，使用：<br>`iw -f`<br>要显示无线站统计信息，例如发送/接收字节数、最后发送比特率，使用：<br>`iw dev <interface_name> station dump` |

Windows `netsh` 使用 `netsh` 工具的 `wlan` 上。下面列出了一些用法示例。要显示所有无线设备和无线网络的完整信息，输入：

```
net wlan show all
```

要显示系统上当前的无线接口列表，输入：

```
net wlan show interfaces
```

要显示系统上无线适配器驱动程序的属性，输入：

```
net wlan show drivers
```

要显示系统上可见的无线网络列表，输入：

```
net wlan show networks
```

要显示无线局域网的当前全局设置，输入：

```
net wlan show settings
```

与驱动相关的问题 MS Windows 使用“设备管理器”卸载设备及其驱动程序。重启，然后重新安装驱动程序。

FOSS/Linux `modprobe` 从 Linux 内核中添加和删除模块（驱动程序）——例如，要强制为无线设备删除名为 `ath5k` 的模块，请输入：

```
modprobe -r ath5k
```

要再次重新加载该模块，输入：

```
modprobe ath5k
```

## 表 A-2. 不同平台上的 OSI 上层问题排查（续）

| 症状、问题与目标 | 平台 | 工具、修复与检查项 |
| :--- | :--- | :--- |
| 通用 TCP/IP 问题 | 通用 | `ping` 生成并发送 ICMP 消息，可用于测试系统的 TCP/IP 设置并测试其他主机是否可达。可用于检查本地系统安装的 TCP/IP 栈是否在基础层面运行正常。如果你怀疑 STA（站节点）的本地 TCP/IP 栈存在问题，可以通过运行简单的 ping 测试来开始排查，探测 `ping 127.0.0.1`。如果上述简单测试失败，说明本地系统的 TCP/IP 栈存在严重问题。你可以通过使用此表修复部分的技术来开始修复。尽管尽管如此，在检查本地 STA 的 TCP/IP 栈时，你应该尝试 ping STA 的 IP 地址。这也应该成功。输入：`ping <IP-address-of-local-system>`。如果本地系统内一切正常，你可能想检查本地网络上的其他系统是否可达。输入：`ping <IP-address-of-remote-host>`。上述测试在某些可能会失败。如果网络上使用了中间防火墙，防火墙可能会阻止或拦截 ping 工具默认使用的 ICMP 包。运行在本地系统上的主机防火墙软件也可能拦截 ICMP 包。 |
| 地址解析协议 (ARP) | 通用 | `arp` 在确认本地 STA 的 TCP/IP 栈基本无正常后，如果 STA 仍然无法 ping 其他本地系统，你可以尝试清除 STA 的本地 ARP 缓存。如果你可以同时 ping 回环地址 (`127.0.0.1`) 和你的 IP 地址，但无法 ping任何其他 IP 地址，请使用 `arp` 工具清除 ARP 缓存。要查看当前缓存条目，输入：`arp -n`。要删除条目，输入：`arp -d`。 |
| TCP/IP：修复 如果你怀疑本地 STA 的软件 TCP/IP 栈损坏或发生混乱，可以尝试修复它 | MS Windows | `netsh` 使用网络配置工具（参见第 13 章）重置 Windows 中的 TCP/IP。这与卸载并重新安装 TCP/IP 协议的效果相同。输入：`netsh ip reset logfile.txt` |
|  | FOSS/Linux | 这可能简单地停止并重启控制无线接口的不同脚本。不同的 Linux 发行版有不同的处理方法。在 Debian 或 Ubuntu 平台上，输入：`/etc/init.d/network-manager restart`、`/etc/init.d/network restart` 或 `restart network-manager`。在 Fedora、RHEL 或 CentOS 系统上，输入：`restart network` 或 `service network restart`。在 OpenSUSE 或 SUSE 系统上，输入：`rcnetwork restart` 或 `service network restart`。 |

## 附录：无线网络排查

| 症状、问题与目标 | 平台 | 工具、修复与检查项 |
| :--- | :--- | :--- |
| 通用 DHCP 相关问题 |  | 你应该首先确保无线 STA 确实配置为通过 DHCP 获取 TCP/IP 配置信息。STA 可能配置为使用静态或手动 IP 配置，静态配置的信息可能是错误的。验证 STA 上的 DHCP 客户端软件正在运行。系统上所有运行进程列表以及系统日志文件是检查此项的好地方。在 TCP/IP 配置成功完成之前，无线 STA 必须成功完成扫描、选择、验证和关联的所有阶段。DHCP 相关问题：客户端可能具有错误的 TCP/IP 配置，或者简单地没有从工作的 DHCP 服务器获取任何 TCP/IP 配置。尝试手动强制 DHCP 请求。 |
|  | MS Windows | 强制请求新的 DHCP 配置：`ipconfig /renew`。要释放当前的 DHCP 租期，输入：`dhclient /release`。用于通过 DHCP 配置网络接口。 |
|  | FOSS/Linux | 请求新的 DHCP 配置信息或租期，输入：`dhclient <name_of_interface>`。释放当前的 DHCP 租期，输入：`dhclient -r`。 |
|  | Apple X | 使用连接管理器（Connection Manager）禁用后重新启用无线接口。 |
| 通用路由问题 |  | 这些问题表现为主机系统无法访问网络。例如，STA 可能可以访问同一网络上的系统，但无法访问其他网络。 | `route` 显示并操作路由表。检查 STA 上的路由表有助于了解如何访问其他网络。在 Windows 系统上查看路由表，输入：`route print`。在 Linux 系统上查看，输入：`route -n`。 |
| 无法访问 Internet 主机 | STA 能够访问本地系统但无法访问 Internet，最可能是路由问题。使用 `route` 工具查看本地路由表。如果 STA 需要访问间接网络，路由表中应有默认路由项。 |
|  | 通用 | STA 能够访问本地系统但无法访问 Internet，最可能是路由问题。默认路由将指向“`0.0.0.0`”。每当此项缺失，意味着 STA 不知道如何向外部网络（如 Internet）发送数据包。解决此问题的方法是确保 STA 的路由表中默认路由。 |
|  | MS Windows | 在 Windows 系统上，在命令提示符输入此命令：`route add 0.0.0.0 mask 0.0.0.0 <IP_ADDRESS_OF_GATEWAY>` |
|  | FOSS/Linux | 在 Linux 系统上，在 shell 提示符输入此命令：`route add default gw <gateway_ip>` |

表 A-2. 不同操作系统上的 OSI 上层问题排查（续）

附录：无线网络排查

| 症状、问题与目标 | 平台 | 工具、修复与检查项 |
| :--- | :--- | :--- |
