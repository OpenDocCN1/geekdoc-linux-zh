
在大多数情况下，/etc/sysconfig/network 至少包含两个指令：

```
NETWORKING=yes
HOSTNAME=yourhostname
```

表 5-7 中显示的其他指令没有强制要求，包括 NIS 域、用于 IPv6 网络配置的指令以及网关地址。其中一些指令（包括 HOSTNAME）可能由 DHCP 服务器设置。

## /etc/sysconfig/network-scripts 文件

/etc/sysconfig/network-scripts 目录是 Red Hat Enterprise Linux 存储和获取网络信息的地方。虽然使用可用的 Red Hat 配置工具时无需手动修改这些文件，但了解它们的存在是有好处的。表 5-8 展示了一些具有代表性的文件。

![](img/9139201cfcaf4292284a0eed074928e5_302_0.png)

* /etc/sysconfig/network-scripts 中的某些命令可能通过硬链接指向 /etc/sysconfig/networking/devices 和 /etc/sysconfig/networking/profiles/default 目录中的文件。*

TABLE 5-8
/etc/sysconfig/network-scripts 文件

| /etc/sysconfig/network-scripts 中的文件 | 描述 |
|---|---|
| ifcfg-lo | 配置回环设备，这是一个虚拟设备，用于确认 TCP/IP 的正确安装。 |
| ifcfg-* | 每个已安装的网络适配器（例如 eth0）都会获得自己的 ifcfg-* 脚本。例如，eth0 对应文件 ifcfg-eth0。如果使用 NetworkManager，可能是 ifcfg-System_eth0。该文件包含识别此网络适配器在网络上所需的 IP 地址信息。 |
| network-functions | 此脚本包含其他网络脚本用于启动和停止网络接口的函数。 |
| ifup-* 和 ifdown-* | 这些脚本激活和停用其分配的协议。例如，ifup-ppp 启动 PPP 设备，通常是电话调制解调器。 |

现在让我们看一下 ifcfg-eth0 文件。基于第 2 章中定义的静态网络配置，相关的指令如下：

```
DEVICE="eth0"
BOOTPROTO="static"
BROADCAST="192.168.122.255"
DNS1="192.168.122.1"
GATEWAY="192.168.122.1"
HWADDR="52:54:00:55:00:A2"
IPADDR="192.168.122.50"
NETMASK="255.255.255.0"
NM_CONTROLLED="yes"
ONBOOT="yes"
```

这些指令中的大多数都很直观，因为它们将设备定义为第一个以太网网卡（eth0），使用静态网络配置，并使用定义的 IP 地址进行广播，指定 DNS 服务器、网络网关、网卡和网络掩码。请注意，此处显示的网卡硬件地址与图 5-11 中定义的硬件地址相匹配。是的，该 eth0 网卡在 Linux 启动过程中会被启用。

其中一个指令显得特别晦涩：NM_CONTROLLED。该指令指定是否可以使用 Red Hat 网络管理器来配置和控制该网卡。对于拥有多个网络连接的用户来说，这是一个极佳便利功能，但对于拥有单一稳定物理网络连接（如服务器）来说，其重要性较低。

## Red Hat 配置工具

与其他许多 Red Hat 配置工具一样，这里也有控制台工具和图形界面工具可用。控制台工具自然地可以从文本控制台运行。要打开它，请运行 system-config-network-tui 命令。这与从控制台的 setup 命令访问的工具相同；在这两种情况下，都会启动如图 5-13 所示的易于配置的网络配置工具。在 RHEL 6 中，NetworkManager 服务取代了网络管理工具。这不仅意味着 GUI 配置工具发生了变化，还意味着默认情况下未安装 GUI 工具。若要使用 GUI NetworkManager 配置工具，可能需要先使用以下命令安装相关包：

```
# yum install NetworkManager-gnome
```

### 图 5-13

控制台网络配置工具

![](img/9139201cfcaf4292284a0eed074928e5_304_0.png)

然后，您可以使用以下命令启动如图 5-14 所示的 GUI 网络连接工具：

```
# nm-connection-editor
```

### 图 5-14

网络连接工具。

![](img/9139201cfcaf4292284a0eed074928e5_304_1.png)

## 练习 5-3

### 使用网络连接工具修改网络接口

本练习依赖于 NetworkManager 服务的活跃使用以及随附的 GUI 配置工具。您将看到由该工具添加到关键配置文件中的内容。

- 1. 备份要更改的网络卡的配置。如果是第一个以太网卡，请从 /etc/sysconfig/network-scripts 目录备份 ifcfg-eth0 文件。确保该文件的副本存在于这两个目录中。
- 2. 启动网络连接工具。在 GUI 终端中，按 ALT+F2，并在出现的文本框中输入 nm-connection-editor。这将打开网络连接工具。
- 3. 如果“有线”选项卡未处于活动状态，请选择它。
- 4. 选择要修改的适配器，然后单击“编辑”。如果是以太网适配器，您将看到一个类似于下一图所示的“编辑系统”窗口。

![](img/9139201cfcaf4292284a0eed074928e5_305_0.png)

- 5. 选择“IPv4 设置”选项卡。高亮显示当前 IP 地址，然后单击“删除”以移除当前 IP 地址信息。单击“添加”。将 IP 地址设置为 192.168.1.11，将网络掩码（子网掩码）设置为 255.255.255.0。（如有需要，可替换为不同的 IP 地址以将此系统与本地网络隔离。）
- 6. 单击“应用”。如果提示，请输入 root 管理员密码。返回到网络连接工具窗口，单击“关闭”。
- 7. 在命令行提示符下，通过命令行界面运行 ifconfig 以检查目标网卡的 IP 地址设置。发生什么情况？
- 8. 查看修改后的网络配置文件的内容。如果是第一个以太网卡，该文件名在 /etc/sysconfig/network-scripts 目录中包含术语 ifcfg 和 eth0。更改是否反映在那里？如果文件名已更改，则可能您忘记在指定目录中保存 ifcfg-eth0 文件的副本。
- 9. 运行 ifdown eth0 和 ifup eth0 命令以应用来自 ifcfg-eth0 文件新版本的更改。
- 10. 重新运行 ifconfig 命令以确保其正常工作。
- 11. 比较配置文件的原始版本和新版本。您可以在匹配的终端中打开它们，或应用 diff 命令。
- 12. 差异是什么？除了不同的 IP 地址信息外，网络连接工具还添加了什么？附加的指令应该很直观。注意网络连接工具如何添加 UUID 以唯一标识配置。
- 13. 恢复关联网卡的配置文件的原始版本；如果是第一个以太网卡，则是 ifcfg-eth0。如果您忘记在指定目录中保存 ifcfg-eth0 文件，该文件现在可能命名为 ifcfg-System_eth0。

**考试提示**
如果您想在考试中使用网络连接工具，请确保您对该工具了如指掌。确保您知道如何安装它。试验可用的选项。进行一些更改，并检查对我所描述文件的影响。

## 配置名称解析

网络配置的最后一部分通常是名称解析。换句话说，本地系统是否有将域名（如 mcgraw-hill.com）转换为 IP 地址（如 198.45.24.143）所需的信息？

在 Unix 最初开发时，名称解析很简单。当互联网的前身首次投入使用时，全球计算机网络只有四个主机，每个大学有一台计算机。设置一个包含每个主机名称和对应地址列表的静态文件是很简单的。该文件已演变为 Linux 中所谓的 /etc/hosts。

但现在互联网更加复杂。虽然您可以尝试在 /etc/hosts 文件中设置互联网上每个域名和 IP 地址的数据库，但这几乎需要永远。这就是为什么大多数用户设置与 DNS（域名服务）服务器的连接。在 RHEL 6 中，这仍然记录在 /etc/resolv.conf 配置文件中。在第 2 章创建的基础系统中，该文件包含两行：

```
search example.com
nameserver 192.168.122.1
```

第一行将 example.com 域名附加到给定的主机名；例如，如果您在 server1 系统上运行 ping 命令，它实际上会搜索 server1.example.com 系统。第二行指定与本地 DNS 服务器关联的 IP 地址。作为 RHCE，您需要知道如何配置仅缓存的 DNS 服务器；该主题在第 17 章中涵盖。DNS 配置不是 RHCSA 的要求。

在较小的网络中，一些管理员设置 /etc/hosts 文件作为本地网络上每个系统名称和 IP 地址的数据库。如果需要，管理员甚至可以在互联网上设置一些域的 IP 地址。对于之前章节中描述的系统，适当的 /etc/hosts 文件可能包含以下指令：

```
192.168.122.50 server1.example.com
192.168.122.150 tester1.example.com
192.168.100.100 outsider1.example.org
```

但是，如果您配置了 DNS 服务器和 /etc/hosts 中的系统连接，首先搜索什么？搜索顺序由 /etc/nsswitch.conf 配置文件中的一行指定，该文件首先搜索本地文件（/etc/hosts）中的主机名，然后搜索任何可访问的 DNS 服务器。

```
hosts: files dns
```

