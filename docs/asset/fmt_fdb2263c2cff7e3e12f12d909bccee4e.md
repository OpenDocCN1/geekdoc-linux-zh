
之前你学习了 `/hosts` 文件包含 IP 地址和名称之间的引用。你现在需要查看将 IP 地址与以太网卡关联的文件。该文件是 `/etc/network/interfaces`，它包含的所有网络设置如下：

```
### /etc/network/interfaces
### ifup(8), ifdown(8) 的配置文件

### 回环接口
iface lo inet loopback

### 第一网卡
#- 条目是在 Debian 安装期间创建的
#(network, broadcast and gateway 是可选的)
iface eth0 static
	address 192.168.0.26
	netmask 255.255.255.224
	network 192.168.0.0
	broadcast 192.168.0.1
	gateway 192.168.0.1
```

### 向以太网卡添加 IP 地址

在 Linux 下，你可以通过一个以太网卡虚拟地引用多个 IP 地址。这被称为*多宿主*（multihomed）或*虚拟托管*（virtual, hosting）。在托管多个域名的网站时，这是一个常见的做法。如果你知道该做什么，这个过程很容易。

让我们回到你一直使用的那个文件——`/etc/network/interfaces`。你可以手动添加所需信息，如下例所示：

```
### /etc/network/interfaces
# -- ifup(8), ifdown(8) 的配置文件

### 回环接口
iface lo inet loopback

# 第一块网卡
# -- 此条目是在 Debian 安装期间创建的
# (网络、广播和网关是可选的)
iface eth0 inet static
    address 192.168.0.26
    netmask 255.255.255.224
    network 192.168.0.0
    broadcast 192.168.0.31
    gateway 192.168.0.1

iface eth0:0 inet static
    address 192.168.0.23
    netmask 255.255.255.224
    network 192.168.0.0
    broadcast 192.168.0.31
    gateway 192.168.0.1
```

这与你更改网卡 IP 的方式类似。区别在于，这里你通过为真实的以太网卡（`eth0:0`）设置新的 IP 地址来添加新接口。要更改网卡的地址，只需对现有文件内容进行修改。其他信息（子网掩码、网络、广播和网关）被设置为与原始真实网卡匹配。如果你有更多地址要添加，请增加别名数字（例如 `eth0:1`、`eth0:2` 等）。

# 网络故障排除

系统管理中最令人沮丧的部分之一是追踪问题。解决这些问题的关键在于了解手头有哪些工具。网络问题从物理连接不良到软件配置错误不一。诀窍在于学习定位问题的最佳方法。

通常，故障排除需要按照顺序执行一系列逻辑步骤或问题。在执行过程中，你会排除各种可能性，就像飞行员的故障排除检查清单一样。通常，你从物理（硬件）区域开始，然后移动到软件区域。网卡安装了吗？电缆插好了吗？电缆是完好的吗？最终你会找到问题并采取适当措施来解决它。在故障排除时，务必检查这些常见的网络区域：

- 电缆故障：由于某种原因电缆无法工作（内部线芯断裂、自制电缆接线错误等）
- 网卡使用了错误的设备驱动程序
- 与内核版本缺失或过旧的模块
- 接口配置错误（IP 地址、网络或网关）

这些只是常见问题。有几个工具——`ifconfig`、`ping`、`traceroute` 和 `route`——可以帮助诊断此类问题。后续部分将介绍其中几个。

## 使用 dmesg 进行故障排除

第一道防线——找出哪些模块已正确加载。

```
$ dmesg | more
```

Adding Swap: 18476k swap-space (priority -1)

rtl8193.cvl1.07 5/6/99 Donald Becker http://cesdis.gsfc.nasa.gov/linux/drivers/

rtl8193.html

eth0: RealTek RTL8193 Fast Ethernet at 0x6900, IRQ 9, 00:c0:f4:00c:f2.

Serial driver version 4.27 with no serial options enabled

tty500 at 0x03fb (irq = 4) is 16550

ty501 at 0x02fb (irq = 3) is 16550

显示的信息比这里显示的要多。大部分信息可能你不感兴趣；其他信息可以为问题提供深刻的洞察。例如，在这种情况下，网卡使用了 RealTek RTL8193 驱动模块。如果由于某些原因驱动无法与卡通信，这里会显示错误消息。其他驱动/硬件问题也是如此。

## 使用 ifconfig 进行故障排除

此实用它可以实时更改网络设置，但任何更改在系统重启后必须撤销。该工具在显示当前网络设置方面很有用。请注意我当前网络接口的配置：

```
# ifconfig encap:Ethernet HWaddr:00:CD:F0:46:0C:F2

inet addr:192.168.0.26 broadcast:192.168.0.31 Mask:255.255.255.224
UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
RX packets:1788 errors:0 dropped:0 overflows:0 frame:0
TX packets:2535 errors:0 dropped:0 overflows:0 carrier:0 collisions:0 txqueue:100

inet encap:Loopback
inet addr:127.0.0.1
```

此工具可以实时更改网络设置，但任何更改在系统重启后必须撤销。该工具在显示当前网络设置方面很有用。

## 使用 traceroute 排除故障

与 `ping` 同样重要的是 `traceroute`。该程序可以追踪 IP 包的路径以到达目的地。数据包在途中可能会经过许多网络设备（通常是网关）。对于互联网来说尤其如此，因为它是由一个接网关组成的。你可以把数据包想象成一辆跨越国家的汽车。当汽车从纽约开芝加哥时，它经过几个城市（把这些城市想象成网关）。以下是一个在网站 www.debian.org 使用 `traceroute` 的示例：
