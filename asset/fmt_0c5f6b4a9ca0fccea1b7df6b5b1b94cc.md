
`append="ether=12,0x300,eth0 ether=15,0x340,eth1"`

## 5.3 配置网络地址

这是真正有趣的部分。现在你必须做一些决定。由于我们不希望互联网访问私有网络的任何部分，有一组互联网地址被预留给私有网络。因为每个人都需要地址，而且这些地址无法连接互联网，它们是很好的选择。

在这些地址中，`192.168.2.xxx` 被预留了，我们将在示例中使用它。

你的代理将是两个网络的成员，以便它可以在私有网络内部和外部之间传输数据。

## 5. 准备 Linux 系统

如果你打算使用过滤型防火墙，你仍然可以使用这些数字。你需要使用 IP 伪装（IP masquerading）来实现。通过这个过程，防火墙将转发数据包并将其翻译为“真实”IP 地址以便在互联网上传输。

你必须将真实 IP 地址分配给互联网外侧（out）的网卡。同时，为内侧以太网卡分配 `192.168.2.1`。这将是你的代理/网关 IP 地址。你可以为受保护网络中的所有其他机器分配 `192.168.2.3xx` 范围内的任意数字（`192.168.2.2` 到 `254`）。

由于我使用 RedHat Linux（嘿，伙计们，能给我个副本吗？;)）来在启动时配置网络，我在 `/etc/sysconfig/network-scripts` 目录下有一个 `ifcfg-eth1` 文件。该文件在启动过程中被读取，以设置你的网络和路由表。

以下是我的 `ifcfg-eth1` 的样子：

```
#!/bin/sh

# Device type: ethernet

# Variable declarations:

DEVICE=eth1

IPADDR=192.168.2.1

NETMASK=255.255.255.0

NETWORK=192.168.2.0

BROADCAST=192.168.2.255

GATEWAY=192.1.2.10

ONBOOT=yes

# End variable declarations
```

你也可以使用这些脚本通过你的运营商自动连接调制解调器。查看 `ipup-ppp` 脚本。

如果你使用调制解调器连接互联网，外部 IP 地址将在连接时由你的运营商为你分配给你。

## 5.4 测试你的网络

首先检查 `ifconfig` 和 `route`。如果你有两个网卡，你的 `ifconfig` 应该像这样：

```
#ifconfig

Link encap:Local Loopback

addr:127.0.0.0 Bcast:127.255.255.255 Mask:255.0.0.0

UP BROADCAST LOOPBACK RUNNING MTU:3584 Metric:1

RX packets:1620 errors:0 dropped:0 overflows:0

TX packets:1620 errors:0 dropped:0 overflows:0
```

```
eth0

Link encap:0Mbps Ethernet Hwaddr 00:00:09:85:AC:55

addr:192.168.2.1 Bcast:192.1.2.255 Mask:255.255.255.0

UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1

RX packets:0 errors:0 dropped:0 overflows:0

TX packets:0 errors:0 dropped:0 overflows:0

Interrupt:12 Address:0x310
```

```
eth1

Link encap:0Mbps Ethernet Hwaddr 00:00:09:80:1E:D7

addr:192.168.2.1 Bcast:192.168.2.255 Mask:255.255.255.0

UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1

RX packets:errors:0 dropped:0 overflows:0

TX packets:errors:0 dropped:0 overflows:0

Interrupt:15 Base address:0x3550
```

并且你的路由表应该像这样：

```
route -n

Kernel routing table

Destination     Gateway         Genmask         Flags Metric Ref Interface

192.1.2.0         *               255.255.255   U    1500      0 15 eth0

192.168.2.0       *               255.255.255   U    1500      0 0 eth1

127.0.0.0         *               255.0.0.0     U    3584      0 2 lo

default           192.1.2.10     *               UG    1500      0 72 eth0
```

注意：`192.1.2.0` 是该防火墙访问的互联网，`192.168.2.0` 是私有网络。

现在从防火墙 ping 互联网。使用 `google.com` 作为我的测试点。这是一个很好的测试，但事实比我预想的要可靠得多。如果起初不起作用，尝试 ping 其他几个未连接到你局域网（LAN）的地方。如果还是不行，说明你的 PPP 设置不当。重读 Net-2 HOWTO，并祈祷吧。

接下来，尝试从防火墙 ping 受保护网络内的一个主机。所有计算机都应该能够互相 ping。如果不能，请回过 NET-2 HOWTO 并进一步研究网络。

然后，尝试从受保护网络内部 ping 防火墙的外部地址。（注意：这并不是 `192.168.x` 的任何一个 IP 数字）。如果可以通的，说明你没有关闭 IP 转发（IP Forwarding）。确保这是你想要的。如果你留着它，你将还需要阅读本文的 IP 过滤章节。

现在尝试从你的防火墙 ping 互联网。使用之前有效的那个地址。再次，如果你关闭了 IP 转发，这不应该起作用；但如果你开启了并将受保护网络分配到 `192.168.2.*`，那么任何数据包都可以路由过去。如果你跳过了这一步并已经开启了 IP 伪装，这应该是可以的。现在，你有了基础设置。

## 5.5 加固防火墙

防火墙如果处于开放状态是不安全的。“坏人”可以访问防火墙并根据自己的需要对其修改。从关闭任何未使用的服务开始。查看 `/etc/rc.d` 文件，它控制着许多守护进程的启动。要关闭某个服务，在行首加上 `#`。

在我的系统中，我创建了几个脚本来拒绝所有访问并刷新上次运行时的 iptables 规则。这个脚本会起作用。

```
# setup IP Accounting

# Forwarding

# By default DENY all services

ipfwadm -F -p deny

# Flush commands

ipfwadm -f

ipfwadm -I -f

ipfwadm -O -f
```

现在我们有了终极防火墙。没有任何通过。你可能有些需要转发的服务，这里有一些对你有用的示例：

```
# Forward email to your server

ipfwadm -F -a accept -p tcp -S 0.0.0.0/0 1024:65535 -D 192.1.2.10 25

# Forward connections to outside email servers

ipfwadm -F -a accept -p tcp -S 192.1.2.10 25 -D 0.0.0.0/0 1024:65535

# Forward Web connections to your Web Server

/sbin/ipfwadm -F -a accept -p tcp -S 0.0.0.0/0 1024:65535 -D 192.1.2.11 80

# Web connections to outside Web Server

/sbin/ipfwadm -F -a accept -p tcp -S 192.1.2.* 80 -D 0.0.0.0/0 1024:65535

# Forward DNS traffic

/sbin/ipfwadm -F -a accept -p udp -S 0.0.0.0/53 -D 192.1.2.0/24
```

你可能对对通过防火墙的流量进行计数（accounting）。这个脚本会统计每一个数据包。你可以添加一行来统计去单个系统的数据包。

```
# Flush the current accounting rules

ipfwadm -A -f

# Accounting

/sbin/ipfwadm -A -f
```

```
# Accounting and Forwarding
```
