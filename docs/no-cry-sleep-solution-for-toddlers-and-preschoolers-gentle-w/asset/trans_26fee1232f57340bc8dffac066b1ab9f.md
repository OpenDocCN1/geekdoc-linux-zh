

```
allow-transfer { internals; }
};
```

在外部 DNS 服务器的配置中，internals 和 externals 的 ACL 设置相同。在 options 语句中，递归现在对 externals 和 internals 都允许。在 mygolf.com 区域中，查询允许来自任何地方，递归对 externals 和 internals 允许。传输完全不允许。

### External DNS server

```
acl internals { 192.168.0.1; 192.168.0.2; 192.168.0.3; };
acl externals {10.0.0.1};
options {
    allow-transfer { none; }; // allow-transfer to no one
    allow-query { internals; externals; };// restrict query access
    allow-recursion { internals; externals }; // restrict recursion
};
zone "greatgolf.com" {
    type master;
    file "greatgolf";
    allow-query { any; };
    allow-transfer { internals; externals; };
};
```

## CHAPTER DHCP Server

现在许多网络都提供 DHCP 服务，可自动为所有连接的主机提供网络配置。它们使用一种名为 DHCP（动态主机配置协议）的协议。通过 DHCP 协议，管理员可以使用一个 IP 地址池，根据需要为主机分配 IP 地址。该协议还可以用于提供所有必要的网络连接信息，例如网络的网关地址或子网掩码。无需分别配置每台主机，网络配置可以通过中央 DHCP 服务器处理。地址可以使用的时间长度可以通过租约来控制，从而有效利用可用地址。如果你的网络使用 DHCP 配置系统，你就无需手动配置。所有必要的信息将自动输入到你的网络配置文件中。

DHCP 为连接到 TCP/IP 网络的系统提供配置信息，无论是 Internet 还是内联网。网络上的机器作为 DHCP 客户端运行，从其网络上的 DHCP 服务器获取网络配置信息。网络上的一台机器运行 DHCP 客户端守护进程，可自动从其网络的 DHCP 服务器下载网络配置信息。这些信息包括其 IP 地址，以及网络的名称服务器、网关和代理地址，包括子网掩码。本地系统无需手动配置。这还有助于将网络配置的控制集中在网络上的不同系统上。网络管理员可以从 DHCP 服务器管理网络上所有系统的网络配置。

> NOTE DHCP 基于为无盘工作站开发的 BOOTP 协议。查阅 DHCP 文档以了解专为与 BOOTP 配合使用而设计的机器的特定选项。

DHCP 服务器还支持几种 IP 地址分配方法：自动、动态和手动。自动分配为一台主机分配永久 IP 地址。手动分配由网络管理员指定的 IP 地址分配给主机。使用动态分配时，DHCP 服务器只能在主机实际需要使用时才为网络上的主机分配 IP 地址。动态分配从主机在需要时可以使用并在完成后释放的 IP 地址池中获取地址。

当前版本的 DHCP 现在支持 DHCP 故障转移协议，其中两个 DHCP 服务器支持相同的地址池。如果其中一个出现故障，另一个可以继续为网络提供 DHCP 服务。此方案中的主服务器和次服务器分别用 primary 和 secondary 语句指定。

有多种 DHCP 服务器和客户端可用于不同的操作系统。对于 Linux，你可以从 Internet 软件联盟（ISC）获取 DHCP 软件，网址为 www.isc.org。软件包包括 DHCP 服务器、客户端和中继代理。Linux 包含 DHCP 服务器和客户端。DHCP 客户端称为 dhcpc，服务器称为 dhcpd。DHCP 客户端下载的网络信息保存在其自己的 /etc/dhcpcd 目录中的网络配置文件中。例如，你可以在这里找到网络名称服务器的 resolv.conf 文件。

### Configuring DHCP Client Hosts

将主机配置为使用 DHCP 服务器，只需为其网络接口设备（如以太网卡）设置选项即可。对于 Linux 主机，你可以使用发行版的网络工具将主机设置为自动访问 DHCP 服务器以获取网络信息。在网络工具的 Internet 连接配置面板上，通常会找到用于选择 DHCP 的复选框。单击此框即可启用 DHCP。对于 Red Hat，你可以使用 redhat-config-network 工具并在 Devices 面板上选择网络设备并编辑它。在 General 面板上，单击标记为 Automatically Obtain IP Address Settings With 的条目，并确保从弹出菜单中选择 DHCP。如果要连接到 Internet 服务提供商（ISP），在 DHCP Setting 下，单击 Automatically Obtain DNS Information From Provider。在 Red Hat 中，BOOTPROTO 条目将被设置为 DHCP，该条目位于 /etc/sysconfig/network-scripts 目录中该接口的网络脚本中，例如 ifcfg-eth0 代表第一块以太网卡。你也可以手动添加此条目：

```
BOOTPROTO=dhcp
```

确保使用网络脚本重新启动网络设备以使更改生效。DHCP 服务器提供给客户端的信息列在客户端的 /etc/dhcpcd 目录中。在这里你会找到客户端特定网络设备的信息文件。例如，为第一块以太网设备提供的信息将列在 /etc/dhcpcd/dhcpcd-eth0.info 文件中。你会找到诸如 IP 地址、子网掩码、广播地址、主机名、域名和 DNS 服务器等信息——所有这些都由 DHCP 服务器分配给客户端。

在 Windows 客户端上，找到网络接口卡的 TCP/IP 条目，然后打开其属性窗口。单击标记为 Obtain IP Address Automatically 的框。然后找到 Wins 面板（通常通过单击 Advanced 按钮）并选择 DHCP 作为你想要使用的协议。

### Configuring the DHCP Server

在 Red Hat 系统上，你可以使用 /etc/rc.d/init.d 目录中的 dhcpd 命令停止和启动 DHCP 服务器。使用 redhat-config-services 工具或 service 命令配合 start、restart 和 stop 选项。以下示例启动 DHCP 服务器。使用 stop 选项关闭它，restart 将重新启动它。

```
service dhcpd start
```
