
我们建议您先用 YaST 设置设备，然后在配置文件中进行更改。从头开始设备是一项复杂的任务，因为硬件驱动程序也需要配置。

配置文件的内容取决于设备的配置。要更改配置文件，您需要知道如何执行以下操作：

- 静态配置设备
- 使用 DHCP 动态配置设备
- 启动和停止已配置的接口

# 静态配置设备

静态配置设备的配置文件内容类似于：

```
BOOTPROTO='static'
STARTMODE='auto'
NAME=nForce2 Ethernet Controller
ETHTOOL_OPTIONS='
BROADCAST='
IPADDR='172.17.8.101/16'
MTU='
NETWORK='
REMOTE IPADDR='
USERCONTROL='no'
```

配置文件包含几行。每行都有一个选项以及分配给该选项的值，解释如下：

- `BOOTPROTO='static'`。确定设备的配置方式。有两个可能的值：
  - `static`。设备使用静态 IP 地址进行配置。
  - `dhcp`。设备通过 DHCP 服务器进行自动配置。
- `STARTMODE='auto'`。确定设备的启动方式。此选项可以使用以下值：
  - `auto`。设备在启动时启动或在运行时初始化。
  - `manual`。必须手动使用 `ifup` 手动启动设备。
  - `ifplugd`。接口由 `ifplugd` 控制。
- `ETHTOOL_OPTIONS='`。`ethtool` 工具用于查询以太网设备的设置并更改它们（例如设置速度或半双工/全双工模式）。`ethtool` 的手册页列出了可用选项。

如果您想让 `ethtool` 修改任何设置，它会在此处列出选项。如果没有列出任何选项，则不会调用 `ethtool`。
- `BROADCAST='`。网络广播地址。如果为空，则根据 `/etc/sysconfig/network/config` 中的配置，从 IP 地址和网络掩码推导出广播地址。
- `IPADDR='`。`172.17.8.101/16`。设备的 IP 地址。
- `NETWORK='`。网络本身的地址。
- `REMOTE_IPADDR='`。仅在您设置点对连接时才需要。
- `MTU='`。指定 MTU（最大传输单元）的值。如果不指定值，则使用默认值。对于以太网设备，默认值为 1500。

`/etc/sysconfig/network/ifcfg-template` 包含了基础模板。

# 使用 DHCP 动态配置设备

如果您想通过 DHCP 配置设备，可以将 `BOOTPROTO` 设置为 `dhcp`。`/etc/sysconfig/network/ifcfg-template` 包含了基础模板。

# 启动和停止已配置的接口

要将更改应用到路由配置，您需要使用 `ifdown` 和 `ifup` 命令重启受影响的网络设备。例如，输入 `ifdown eth0` 禁用设备。`ifup eth0` 启用它。这通常在启动时完成。

要配置接口的 IP 地址，你可以按照以下方式使用 `ifconfig`：

```
ifconfig eth0 192.168.1.10 broadcast 192.168.1.255
netmask 255.255.255.0
```

如果 `eth0` 已经分配了 IP 地址，它将被新地址替换。要为接口分配第二个 IP 地址，你必须为设备添加一个标识，如下例所示：

```
ifconfig eth0:1 10.0.0.10 broadcast 10.0.0.255 netmask
255.255.255.0
```

你可以使用以下命令再次删除上述 IP 地址：

```
ifconfig eth0:1 del 10.0.0.10
```

## 使用 ifconfig 工具配置无线网络设置

`ifconfig` 命令与之前的 `ifconfig` 命令类似，但专门用于无线接口。

在接口名称之前不带选项的 `ifconfig` 会显示当前设置，如下所示：

```
da-laptop:~ # ifconfig eth0
eth0 unassociated SSID:off/any Nickname:"ipw2100"
Mode:Managed Channel:0 Access Point: Not-Associated
Bit Rate:0 kb/s Tx-Power:16 RTS throff Fragment:throff
Encryption key:off
Power Management:off
Link Quality:0 Signal level:0 Noise level:0
Rx invalid nwid:0 Rx invalid frag:0 Rx invalid frag:0
Tx excessive retries:0 Invalid misc:0 Missed beacon:0
```

在上面的示例中，没有访问无线网络。

通过 `ifconfig`，你可以设置针对无线设备的特定参数，包括 ESSID、加密密钥和传输功率。

## 使用 route 工具配置路由表

`route` 命令用于显示和更改内核路由表。使用 `-n` 选项显示数字地址，如下所示：

### 第 6 节 配置网络

```
da-10:- # route -n
Kernel IP routing table
Destination  Gateway      Genmask        Flags Metric Ref  Use Interface
172.17.0.0    0.0.0.0      255.255.0.0   U      0 0   Use eth0
192.168.2.0   172.17.8.100  255.255.255.0 UG     0 0   Use eth0
169.254.0.0   0.0.0.0      255.0.0.0   U      0 0   Use eth0
127.0.0.0     0.0.0.0      255.0.0.0   U      0 0   Use lo
0.0.0.0       172.17.8.1    0.0.0.0      UG     0 0   Use eth0
```

以下命令将通过 IP 地址为 172.17.8.254 的路由器添加通往 10.0.0.0/16 网络的路由：

```
route add -net 10.0.0.0 netmask 255.255.0.0 gw
172.17.8.254
```

你可以使用以下命令删除该路由：

```
route del -net 10.0.0.0 netmask 255.255.0.0 gw
172.17.8.254
```

默认路由通过以下命令设置：

```
route add default gw 172.17.8.1
```

## 配置主机名和域名解析

系统主机名和网络域名解析器可以手动设置。在本目标中，你将学习如何执行以下操作：

- 设置主机名和域名
- 配置域名解析

### 设置主机名和域名

主机名在 `/etc/HOSTNAME` 文件中配置。该文件的内容类似于：

```
dal.digitalairlines.com
```

该文件包含系统的完全限定域名。在这种情况下，为 dal.digitalairlines.com。

### 配置域名解析

域名解析需要将主机和域名转换为 IP 地址，反之亦然。Linux 机器上涉及的组件有：

- `/etc/hosts` 文件
- `/etc/resolv.conf` 文件
- `/etc/nsswitch.conf` 文件

#### /etc/hosts 文件

`/etc/hosts` 文件包含 IP 地址和对应的主机名。通常它只包含其所在机器的 IP 地址和主机名，但你可以根据需要添加其他条目。SLES 11 上典型的 hosts 文件类似于所示：

- # hosts 此文件描述了 TCP/IP 子系统的若干主机名到地址的映射。它主要在启动时使用，此时没有名称服务器在运行。在小型系统上，此文件可以替代“named”名称服务器。

# 语法：

# IP-Address Full-Qualified-Hostname Short-Hostname

```
127.0.0.1 localhost
127.0.0.2 dal.digitalairirl.com dal
```

## 特殊

```
127.0.0.1 localhost
127.0.0.2 dal.digitalairirl.com dal
```

- # hosts 此文件描述了 TCP/IP 子系统的若干主机名到地址的映射。它主要在启动时使用，此时没有名称服务器在运行。在小型系统上，此文件可以替代“named”名称服务器。

# 语法：

# IP-Address Full-Qualified-Hostname Short-Hostname

- # hosts 此文件描述了 TCP/IP 子系统的若干主机名到地址的映射。它主要在启动时使用，此时没有名称服务器在运行。在小型系统上，此文件可以替代“named”名称服务器。
