

## 注意

dhcpd.conf 文件要求在每个命令语句后使用分号（;）。如果你的配置文件有错误或运行不正常，请检查这一点。

dhcpd.conf 的下一部分处理你的 DHCP 服务器服务的不同子网；这一节相当直接。每个子网都是单独定义的，可以如下所示：

```
subnet 10.5.5.0 netmask 255.255.255.224 {
  range 10.5.5.26 10.5.5.30;
  option domain-name-servers ns1.internal.example.org;
  option domain-name "internal.example.org";
  option routers 10.5.5.1;
  option broadcast-address 10.5.5.31;
  default-lease-time 600;
  max-lease-time 7200;
}
```

这定义了 10.5.5.0 子网的 IP 地址分配。它将 10.5.5.26 到 10.5.5.30 的 IP 地址范围定义为动态分配给位于该子网上的主机。此示例显示，任何 TCP/IP 选项都可以从配置文件的子网部分进行设置。它显示了子网将连接到的 DNS 服务器，这对于 DNS 服务器负载均衡很有用，或者可用于限制可通过 DNS 到达的主机。它定义了域名，因此你可以在网络上拥有多个域名。它还可以更改默认和最大租约时间。

如果你希望服务器忽略特定子网，可以使用以下条目来实现：

```
subnet 10.152.187.0 netmask 255.255.255.0 {
}
```

这为 10.152.187.0 子网未定义任何选项；因此，DHCP 服务器会忽略它。

dhcp.conf 的最后一部分用于定义主机。如果希望网络上的计算机具有特定的 IP 地址或其他特定于该主机的信息，这会很有用。完成主机部分的 key 是要知道主机的硬件地址。正如你在本章前面“网络硬件设备”中所学到的，硬件地址用于区分主机以进行配置。你的硬件地址可以通过使用前面描述的 ifconfig 命令获得。硬件地址位于标记为“Hwaddr”的 eth0 行上。

```
host fantasia {
  hardware ethernet 08:00:07:26:c0:a5;
  fixed-address fantasia.fugue.com;
}
```

此示例将硬件地址为 08:00:07:26:c0:a5 的主机进行 DNS 查找，以将 fantasia.fugue.com 的 IP 地址分配给该主机。

DHCP 还可以像这样定义和配置无盘客户端的启动：

```
host passacaglia {
  hardware ethernet 0:0:c0:5d:bd:95;
  filename "vmunix.passacaglia";
  server-name "toccata.fugue.com";
}
```

无盘主机 passacaglia 将从服务器 toccata.fugue.com 获取其启动信息并使用 vmunix.passacaglia 内核。所有其他 TCP/IP 配置也可以包含在内。

## 警告

请记住，本地网络上只能存在一个 DHCP 服务器以避免问题。你的 DHCP 在 LAN 上运行过时遗留操作系统的主机时可能无法正常工作。通常 Windows NT 服务器默认安装了 Windows DHCP 服务器。由于 NT 没有需要梳理的配置文件，因此如果两台机器都在同一 LAN 上，该 DHCP 服务器会在 Linux 服务器之前配置你的主机。检查你的 NT 服务器是否存在这种情况并禁用 NT 服务器上的 DHCP；之后，你的其他 DHCP 启用主机应该能够正确配置。另外，请检查确保如果你在 LAN 上使用电缆或 DSL 调制解调器、无线接入点（WAP）或其他能够提供 DHCP 的智能路由器，则不会发生冲突。

## DHCP 的其他用途

可以在 dhcpd.conf 中使用大量选项：整本书都专门用于 DHCP。最全面的书籍是《DHCP 手册》，可在 http://www.dhcp-handbook.com/ 获取。你可以定义 NIS 域、配置 NETBIOS、设置子网掩码并定义时间服务器，或许多其他类型的服务器——仅举几个你可以使用 DHCP 选项的例子。前面的示例将使你的 DHCP 服务器和客户端运行起来。

DHCP 服务器发行版包含可作为网络模板使用的 dhcpd.conf 文件示例。该文件显示了可帮助你入门的基本配置，并对所使用的选项进行了说明。

## 无线网络

如前所述，自 1990 年代初开发出第一个标准以来，Linux 就一直支持无线网络。随着计算机越来越小，无线网络的用途不断增加；与此同时，传输速度也在不断提高。有几种不同的方法可以创建无线网络。以下

