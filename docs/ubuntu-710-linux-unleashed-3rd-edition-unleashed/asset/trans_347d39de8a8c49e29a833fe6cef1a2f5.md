

如果你希望服务器忽略某个特定的子网，可以使用以下条目来实现：

```
subnet 10.152.187.0 netmask 255.255.255.0 {
}
```

这为 10.152.187.0 子网定义了没有任何选项；因此，DHCP 服务器会忽略它。

你 dhcp.conf 的最后一部分是用于定义主机。这在你希望网络上的某台计算机具有特定的 IP 地址或其他特定于该主机的信息时很有用。完成主机部分的关键是知道主机的硬件地址。正如你在本章前面“硬件设备用于网络”中所学到的，硬件地址用于区分主机以进行配置。你的硬件地址可以通过使用前面描述的 ifconfig 命令获得。硬件地址位于标记为 “Hwaddr” 的 eth0 行。

```
host prowl {
    hardware ethernet 08:00:07:26:c0:a5;
    fixed-address prowl.hudson.com;
}
```

此示例将硬件地址为 08:00:07:26:c0:a5 的主机进行 DNS 查找，为该主机分配 prowl.hudson.com 的 IP 地址。

DHCP 还可以像这样定义和配置无盘客户端的启动：

```
host bumblebee {
    hardware ethernet 0:0:c0:5d:bd:95;
    filename "vmunix.bumblebee";
    server-name "optimus.hudson.com";
}
```

无盘主机 bumblebee 将从服务器 optimus.hudson.com 获取其启动信息并使用 vmunix.bumblebee 内核。所有其他 TCP/IP 配置也可以包含在内。

## CAUTION

请记住，本地网络上只能存在一个 DHCP 服务器以避免问题。你的 DHCP 在 LAN 上运行过时的旧版操作系统的主机时可能无法正常工作。通常 Windows NT 服务器默认安装了 Windows DHCP 服务器。因为 NT 没有需要整理的配置文件，所以如果两台机器在同一 LAN 上，该 DHCP 服务器会在 Linux 服务器之前配置你的主机。检查你的 NT 服务器是否存在这种情况并禁用 NT 服务器上的 DHCP；之后，你的其他 DHCP 启用主机应该能够正确配置。另外，请确保如果你在 LAN 上使用电缆或 DSL 调制解调器、无线接入点（WAP）或其他智能路由器提供 DHCP，则不会发生冲突。

## Other Uses for DHCP

`dhcpd.conf` 中可以使用大量选项：整本书都专门用于 DHCP。最全面的书籍是 *The DHCP Handbook*，可在 http://www.dhcp-handbook.com/ 获取。你可以定义 NIS 域、配置 NETBIOS、设置子网掩码并定义时间服务器，或许多其他类型的服务器——仅举几个你可以使用 DHCP 选项的例子。前面示例将使你的 DHCP 服务器和客户端运行起来。

DHCP 服务器发行版包含一个 `dhcpd.conf` 文件示例，你可以用它作为网络的模板。该文件显示了一个基本配置，可以让你入门并对所使用的选项进行解释。

## Wireless Networking

如前所述，Linux 自 1990 年代初首次制定标准以来就支持无线网络。随着计算机越来越小，无线网络的使用也越来越多；与此同时，传输速度也在不断提高。有几种不同的方法可以创建无线网络。以下各节将介绍你可以在 Ubuntu 系统上用于初始化、配置和管理无线网络的几个 Linux 命令。

## Support for Wireless Networking in Ubuntu

随 Ubuntu 发行的 Linux 内核为无线网络提供了广泛的支持。用于配置、管理和显示无线连接信息的相关无线工具包括

- `iwconfig`—设置无线网络接口的网络名称、加密、传输速率和其他功能
- `iwlist`—显示无线接口的信息，例如速率、功率电平或使用的频率
- `iwpriv`—使用它来设置无线网络接口的可选功能，例如漫游
- `iwspy`—显示多个节点的无线统计信息

无线设备的支持各不相同，但大多数现代（即 2005 年后）的无线设备应该能与 Ubuntu 配合使用。一般来说，Linux 无线设备软件（通常以内核模块的形式存在）支持创建可由传统接口工具（如 `ifconfig`）管理的以太网设备——设备的无线功能由各种无线软件工具管理。

