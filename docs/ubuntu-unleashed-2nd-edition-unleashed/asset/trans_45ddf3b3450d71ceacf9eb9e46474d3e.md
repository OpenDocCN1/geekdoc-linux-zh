
a cable connection, then they usually come with an ethernet cable, in which case you just need a router. Check with your ISP before buying to ensure that whatever router you do end up with can be supported by them.

## 手动配置 PPPoE 连接

你只有在使用 ISP 提供的调制解调器而不是路由器时才需要使用这些步骤。使用 Ubuntu 手动设置 DSL 连接的基本步骤包括连接适当的硬件，然后如果使用 Roaring Penguin 的 pppoe，则运行一个简单的配置脚本。

首先，将你的 DSL 调制解调器连接到电话线，然后将调制解调器的以太网电缆插入到你计算机的网络接口卡。如果计划与 LAN 的其他部分共享你的 DSL 连接，你至少需要两块网卡——分别指定为 eth0（用于 LAN）和 eth1（用于 DSL 连接）。

以下示例假设你有多台计算机并且将在 LAN 上共享你的 DSL 连接。

首先，以 root 身份登录，并确保你的第一个 eth0 设备已启用并处于活动状态（可能使用 ifconfig 命令）。接下来，启动另一个接口，但分配一个空 IP 地址，如下所示：

```
$ sudo /sbin/ifconfig eth1 0.0.0.0 up
```

现在使用 adsl-setup 命令设置你的系统。像这样输入命令：

```
$ sudo /sbin/adsl-setup
```

你将看到一个文本脚本，并被要求输入你的用户名和用于连接的以太网接口（例如 eth1）。然后你将被要求使用“按需”服务或让连接一直保持活动状态（直到由 root 操作员关闭）。如果需要，你还可以设置超时时间（以秒为单位）。然后你将被要求输入 ISP 的 DNS 服务器的 IP 地址，如果你尚未配置系统的 /etc/resolv.conf 文件。

之后，你将被提示输入密码两次，并必须选择要使用的防火墙类型和 IP 伪装。（你在本章前面“在 Ubuntu 中使用 IP 伪装”部分学习了 IP 伪装。）实际配置是自动完成的。如今使用防火墙是必不可少的，因此除非你打算自行制定防火墙规则集——这超出了本书的范围，否则你应该选择此选项。在你选择防火墙和 IP 伪装设置后，你将被要求确认、保存并实施你的设置。你还将被提供一个选项，允许用户管理连接，这对家庭用户来说很方便。

系统将对 /etc/sysconfig/network-scripts/ifcfg-ppp0、/etc/resolv.conf、/etc/ppp/pap-secrets 和 /etc/ppp/chap-secrets 文件进行更改。

配置完成后，使用 adsl-start 命令启动连接和 DSL 会话，如下所示：

```
$ sudo /sbin/adsl-start
```

DSL 连接应该几乎是即时的，但如果出现问题，请检查你的 DSL 调制解调器是否正在与电话公司的中央办公室通信，方法是检查调制解调器上的状态 LED。由于这因调制解调器而异，请参阅你的调制解调器用户手册。

检查所有电缆是否已正确连接，你的接口是否已正确配置，以及你是否已向设置脚本输入了正确的信息。

如果启用了 IP 伪装，则 LAN 上同一子网地址（例如 192.168.1.XXX）的其他计算机可以使用 Internet，但必须具有相同的 /etc/resolv.conf 名称服务器条目以及以 DSL 连接计算机作为网关的路由条目。例如，如果具有 DSL 连接的主机计算机的 IP 地址为 192.168.1.1，并且 LAN 上的其他计算机使用 192.168.1.XXX 范围内的地址，请在每台计算机上使用 route 命令，如下所示：

```
# /sbin/route add default gw 192.168.1.1
```

请注意，如果每台计算机都有包含 LAN 主机名和 IP 地址条目的 /etc/hosts 文件，你也可以使用主机名。要停止连接，请使用 adsl-stop 命令，如下所示：

```
# /sbin/adsl-stop
```

## 配置拨号上网

大多数 ISP 提供支持 PPP 的拨号连接，因为它是一种快速高效的协议，可用于在串行线路上使用 TCP/IP。PPP 旨在进行双向联网；TCP/IP 为数据提供传输协议。新 Ubuntu 用户面临的一个障碍是如何设置 PPP 并连接到 Internet。无需了解 PPP 协议的细节即可使用它，并且设置 PPP 连接很容易。你可以使用命令行手动配置 PPP 连接，也可以在 X 会话期间使用 Ubuntu 的 Internet 配置向导以图形方式进行配置。每种方法都会产生相同的结果。

PPP 在你的系统上使用多个组件。第一个是名为 pppd 的守护进程，它控制 PPP 的使用。第二个是名为高级数据链路控制（HDLC）的驱动程序，它控制两台机器之间信息流。PPP 的第三个组件是名为 chat 的例程，当你希望它拨号时，它会为你拨号另一端。虽然 PPP 有许多“可调”参数，但默认设置对大多数人来说效果很好。

