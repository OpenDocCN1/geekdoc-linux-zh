

- `http://www.isc.org/products/BIND/bind4.html` — 旧版 BIND 4 的文档。
- `http://www.dns.net/dnsrd/` — DNS 资源目录。
- `http://www.isc.org/bind.html` — Internet Software Consortium 的 BIND 页面，包含 BIND 下载链接以及其他宝贵信息的链接。此页面还包含指向 BIND 操作指南的链接，该指南提供 HTML、Postscript 和行式打印机版本（针对 BIND 4）。

## 使用 DHCP 自动配置客户端

DHCP 代表动态主机配置协议（Dynamic Host Configuration Protocol）。它是一种用于动态配置主机（计算机）的协议，这意味着未配置的客户端计算机可以接入提供 DHCP 服务的局域网，并自动获得 IP 地址、DNS 服务器地址、WINS 服务器地址以及许多其他配置项，否则这些配置需要由网络管理员手动设置。管理员唯一的网络配置任务是确保每个客户端拥有唯一的 hostname。

显然，在一个中等规模局域网的生命周期内，这可以节省数周的配置时间。当局域网的网络地址或网络掩码变更时，它也让重新编号变得轻而易举。DHCP 可用于自动重新配置局域网客户端，以适应 DNS 和 WINS 服务器地址的变化。

## 配置 DHCP 服务器

第一步是检查 DHCP 是否已在服务中。使用以下命令：

```
# ps ax | grep dhcpd
```

如果你看到一个正在运行的 `dhcpd` 实例，说明它已经配置好并在运行。否则，你需要配置 `dhcpd`。这是一个简单的任务。

第一步是尝试在前台运行 `dhcpd`，并观察错误消息（如果有的话）：

```
# dhcpd -f
Internet Software Consortium DHCP Server 2.0
Copyright 1995, 1996, 1997, 1998, 1999 The Internet Software Consortium.
All rights reserved.

Please contribute if you find this software useful.
For info, please visit http://www.isc.org/dhcp-contrib.html

Can't open /etc/dhcpd.conf: No such file or directory
exiting.
#
```

在上面的示例中，注意错误消息指出它找不到 `/etc/dhcpd.conf`。如果收到此错误，下一步是创建该文件。以下是一个位于 `192.168.100.1` 的服务器简单的 `dhcpd.conf` 示例：

```
subnet 192.168.100.0 netmask 255.255.255.0 {
  range 192.168.100.200 192.168.100.240;
  option subnet-mask 255.255.255.0;
  option broadcast-address 192.168.100.255;
  option routers 192.168.100.1;
  option domain-name-servers 192.168.100.1;
  option domain-name "domain.cxm";
  option ip-forwarding on;
  option netbios-node-type 8;
}
```

上述配置指定，`192.168.100.0/24` 子网中的任何客户端都将获得 `192.168.100.200-240` 范围内的 IP 地址，广播地址为 `192.168.100.255`，默认路由为 `192.168.100.1`，DNS（相当于 `resolv.conf`）位于 `192.168.100.1`，域名为 `domain.cxm`，IP 转发开启。netbios-node-type 8 指的是客户端的 netbios 节点类型 H，它指示客户端首先尝试通过单播进行 netbios 解析，失败后再通过广播进行解析。这是广泛推荐的方法。

注意，上述是一个极其简单的 `dhcpd.conf`。它可以变得更加复杂。可以提供多个子网的服务，它们可以在独立的物理网络上，也可以共享一个网络。子网组可以共享属性。单个主机可以集中配置，仅使用其 MAC 地址作为标识，并且如果需要，还可以集中分配主机名。甚至可以将 DHCP 配置为拒绝来自未在 `dhcpd.conf` 中列出的主机的请求，尽管这会消除一些“即插即用”功能。

DHCP 功能强大且灵活。要了解更多信息，请参考以下 man 页面：

- dhcpd
- dhcpd.conf
- dhcp-options
- dhcpd.leases
- dhclient
- dhcrelay

创建 /etc/dhcpd.conf 后，再次尝试在前台运行守护进程：

```
$ dhcpd -f
Internet Software Consortium DHCP Server 2.0
Copyright 1995, 1996, 1997, 1998, 1999 The Internet Software Consortium.
All rights reserved.

Please contribute if you find this software useful.
For info, please visit http://www.isc.org/dhcp-contrib.html

Can't open lease database /var/lib/dhcp/dhcpd.leases: No such file or directory
You: Check for failed database rewrite attempt!
Please read the dhcpd.leases manual page if you
don't know what to do about this.
Exiting.
#
```

在上面的示例中，注意错误消息指出它无法打开租约数据库 /var/lib/dhcp/dhcpd.leases。你必须创建该目录，并确保沿目录树一直到该文件模式均为 755。然后，使用以下命令创建一个空的 dhcpd.leases 文件：

```
$ touch /var/lib/dhcp/dhcpd.leases
```

现在，dhcpd 应该可以运行了，如下例所示：

```
$ dhcpd -f
Internet Software Consortium DHCP Server 2.0
Copyright 1995, 1996, 1997, 1998, 1999 The Internet Software Consortium.
All rights reserved.

Please contribute if you find this software useful.
For info, please visit http://www.isc.org/dhcp-contrib.html

Listening on LPF/eth0/00:a0:c9:e8:20:3c/192.168.100.0
Listening on LPF/eth0/00:a0:c9:e8:20:3c/192.168.100.0
Sending on Socket/fallback/fallback-net
#
```

注意，在上面的示例中，这次 dhcpd 在套接字上进行监听和发送，并持续运行。当你需要故障排除时，可以使用 dhcpd -f 命令在前台运行 DHCP 服务器。然而，你通常会在后台运行它。按 Ctrl+C 终止 dhcpd，然后使用以下命令将其作为守护进程运行：

```
$ /etc/rc.d/init.d/dhcpd restart
Shutting down dhcpd: [FAILED]
Starting dhcpd: [OK ]
#
```

关机时的失败是因为它最初并没有在运行。最后一步是配置服务器以便在重启时运行 dhcpd。这可以通过 linuxconf、控制面板、控制服务活动、dhcpd 来实现。按 Enter 键获取 dhcpd 服务屏幕。在 Startup 行勾选 Automatic 复选框，勾选 Level 3 和 Level 5 的复选框，然后点击 Accept 按钮，并完全退出 linuxconf。下次重启时，dhcpd 将自动运行。

一旦 DHCP 服务器启动并运行，客户端必须被告知使用该服务器的信息。下一节描述如何设置客户端以使用服务器的信息。

## 配置基于 Linux 的 DHCP 客户端

将 Linux 客户端设置为 DHCP 客户端需要在某个文件的一行中添加或修改内容。该文件是 /etc/sysconfig/network-scripts/ifcfg-eth0。你需要修改的行如下所示：

```
BOOTPROTO=static
```

如果该行存在，它指定 eth0 接口的 IP 地址是一个静态地址，由文件中的其他行指定。要使客户端成为 DHCP 客户端，请按照以下方式修改该行，或者如果该行不存在，请添加以下内容：

```
BOOTPROTO=dhcp
```

然后使用以下命令重启客户端的网络接口：

```
# /etc/rc.d/init.d/network restart
```

如果在客户端上执行 ifconfig 命令，你会发现客户端的 IP 地址现在是服务器 dhcpd.conf 文件指定的范围内的一个地址。要切换回静态寻址，请将改回 BOOTPROTO=static 并重启网络。

你还可以使用 linuxconf 在静态和 DHCP 寻址之间切换。菜单顺序是 Networking, Basic Host Information, 查找 Config Mode 单选按钮，并启用显示为 Dhcp 的那个。不幸的是，linuxconf 会不必要地更改 ifcfg-eth0 和其他几个文件中的几行内容。在静态和 DHCP 引导协议之间切换的最少侵入方法是手动编辑 ifcfg-eth0。

### 注意

上述讨论假设客户端计算机通过其 eth0 网卡与网络交互。如果它通过 eth1 交互，则需要编辑的文件将是 ifcfg-eth1。

## 跟踪 DHCP 服务器变更

如前所述，DHCP 的一个主要好处是集中管理客户端网络属性。想象一下，你的组织决定将当前局域网的子网用在其他地方，因此你必须对局域网进行重新编号。如果使用静态配置的客户端，你需要走到每个客户端并更改几个参数。但如果它们通过 DHCP 接收网络参数，客户端会自动更改。几乎如此。

必须告知每个客户端释放并更新其当前的 DHCP 租约。更新将传输新信息。

释放和更新的一种方法是简单地重启客户端。在 Linux 世界中，重启被认为是不礼貌的，因此你只需重启网络以释放并更新你的 DHCP 租约。在客户端上运行以下命令，可重启客户端的网络接口：

```
# /etc/rc.d/init.d/network restart
```

## 配置基于 Windows 的 DHCP 客户端

配置基于 Windows 的 DHCP 客户端几乎与配置基于 Linux 的 DHCP 客户端一样简单。首先，右键点击任何“网上邻居”图标并选择“属性”以调出网络对话框。在“配置”选项卡中的列表框中，选择 TCP/IP->以太网适配器（具体措辞取决于适配器），然后点击“属性”按钮。然后你会进入 TCP/IP 属性对话框。

在 IP 地址选项卡上，选中 **自动获取 IP 地址** 单选按钮。然后，在 WINS 配置选项卡上，选中 **使用 WINS 进行 WINS 解析** 单选按钮。一路点击“确定”，当询问是否要重启时回答“是”。计算机重启后，其 IP 地址将由 DHCP 服务器分配。同样，DHCP 服务器上的 *dhcpd.conf* 中设置的所有参数都将覆盖 Windows 客户端上设置的参数。因此，诸如 DNS 配置等参数可以集中设置。

## 释放和更新你的 DHCP 租约

与 Linux 不同，Windows 在重启时不会释放和更新。这意味着即使 DHCP 服务器修改了 IP 地址范围，Windows 客户端仍会继续使用旧地址，直到 DHCP 租约到期。这显然是一个问题。

Windows 提供了一种通过名为 *winipcfg.exe* 的程序来释放和更新 DHCP 租约的方法，该程序位于 C:\windows\system 目录中。只需运行 *winipcfg.exe*，从下拉列表中选择以太网适配器，点击“释放”按钮，然后点击“更新”。

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_526_0.png)

