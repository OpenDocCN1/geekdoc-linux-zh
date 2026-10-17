
要将调试定向到 PPP 的单独日志文件，请在 `/etc/syslog.conf` 文件中添加以下行：

```
daemon.* /var/log/pppmsg
local1.* /var/log/pppmsg
```

之后，按如下方式重启 `syslog` 守护进程：

```
kill -SIGHUP syslogd
```

最好从桌面进行此调试过程，因为同时打开多个终端窗口会有所帮助。我建议至少打开三个终端窗口。从第一个窗口开始，运行一个命令，在调试消息到来时列出我们刚刚定义的日志文件（`pppmsg`）的内容：

```
tail -f /var/log/pppmsg
```

在下一个窗口中，启动 PPP 接口。假设为 `ppp0`，以 `root` 用户使用以下命令：

```
ppp-on
```

以下是输出的部分列表：

```
Jun 20:43:51 maple pppd[2079]: pppd 2.3.8 started by root, uid 0
Jun 20:43:51 maple pppd[2079]: timeout set to 3 seconds
Jun 20:43:52 maple pppd[2079]: abort (inBUSY\r)
Jun 20:43:52 maple pppd[2079]: abort (inWNO ANSWER\r)
Jun 20:43:52 maple pppd[2079]: abort (inRINGING\r\nrRINGING\r)
Jun 20:43:52 maple pppd[2079]: send (RAT*M)
Jun 20:43:53 maple pppd[2079]: expect (OK)
Jun 20:43:53 maple pppd[2079]: RAT*M
Jun 20:43:53 maple pppd[2079]: OK
Jun 20:43:53 maple pppd[2079]: -- got it
Jun 20:43:53 maple pppd[2079]: send (ATDT5551212*M)
Jun 20:43:53 maple pppd[2079]: expect (CONNECT)
Jun 20:43:53 maple pppd[2079]: *M
Jun 20:44:10 maple pppd[2079]: ATDT5551212*M
Jun 20:44:10 maple pppd[2079]: CONNECT
Jun 20:44:10 maple pppd[2079]: -- got it
Jun 20:44:10 maple pppd[2079]: send (\d)
Jun 20:44:14 maple pppd[2079]: Serial connection established.
Jun 20:44:14 maple pppd[2079]: Using Interface ppp0
Jun 20:44:14 maple pppd[2079]: Connect: ppp0 --> /dev/modem
Jun 20:44:17 maple pppd[2079]: local IP address 222.62.137.121
Jun 20:44:17 maple pppd[2079]: remote IP address 222.62.1.105
```

此输出显示了 `/dev/modem` 上的 PPP 连接。在验证调制解调器工作正常后，`chat` 脚本发送电话号码。连接建立，PPP 接口启动。在进行一些参数协商后，服务器为通信双方分配 IP 地址，连接就绪。

> 如果收到 `chat` 脚本失败的消息，请查看 `/etc/ppp/connect-errors` 目录。当 `chat` 脚本使用 `-v` 选项运行时（如前所示），错误消息就放在那里。根据错误消息，对 `/etc/ppp/ppp-dialer` 文件进行修正。

如果已连接但没有任何应用程序（Web 浏览器、FTP 等）似乎工作，请检查你的 PPP 接口是否被记为默认路由（`/sbin/route -n`）。如果是，请检查你在 `/etc/resolv.conf` 文件中是否正确指定了 DNS 服务器。使用 `ping` 命令 ping 这些 DNS 服务器 IP 地址，以确保可以访问。

## 将局域网连接到 Internet

你的局域网上的用户很高兴你让他们可以相互共享文件和打印机。然而，如果他们想访问 Internet，可能需要使用自己的调制解调器、电话线路和 Internet 账号。已有用户连接至局域网时，你可以设置一个大家共享的 Internet 连接。这样做的好处如下：

- 节省调制解调器 — 不必让每台计算机都配备一台高速调制解调器（如 DSL 或至少 56K 调制解调器）来路由所有到 Internet 的消息。
- 节省电话线路 — 不必为每个想上网的人使用一条电话线路，你可以使用一条线路连接到你的 ISP。（在 DSL 的情况下，电话公司可能允许你使用同一条电话线路同时进行模拟语音和高速度数据传输）。
- 集中维护 — 如果与你的 Internet 连接相关的信息发生变化（如拨号号码或名称服务器地址），你可以在一个位置管理这些更改，而不必在每台计算机上都更改。
- 集中化服务 — 你可以更好地控制进出网络的 Internet 流量。

本节中的程序假定你已经按照第 16 章所述设置了局域网。它还假定你的 OpenLinux 系统已建立到 Internet 的外发 PPP 连接（或其他类型的连接），以便局域网计算机与 Internet 之间的所有流量都可以通过（如本章前面所述）。本节描述了两种设置 OpenLinux 计算机的方法，以便局域网上的客户端可以访问 Internet：

1. 作为路由器 — 通过将 OpenLinux 配置为路由器，它可以通过拨号连接将局域网客户端的 IP 数据包路由到 Internet。
2. 作为代理服务器 — 你可以将 OpenLinux 配置为代理服务器。这样，局域网上的客户端计算机就可以像连接来自 Linux 计算机一样访问 Internet。

接下来的两个章节涵盖了将局域网连接到 Internet 的这两种方法。第一个章节介绍如何设置 OpenLinux 作为路由器。随后章节介绍如何设置 OpenLinux 作为代理服务器。

## 设置 OpenLinux 作为路由器

从局域网到 Internet 的路由设置有几种不同的方法。你可以有一个专用路由器（如 Cisco 675 ADSL 路由器），也可以让已连接到局域网的计算机充当路由器。一台计算机可能有多个网络接口，例如回环、以太网局域网、到另一台计算机的直连线路或拨号接口。对于客户端计算机使用路由器访问 Internet，它可能为大多数接口分配静态 IP 地址，而到路由计算机的连接则是默认路由（处理对所有地址的请求）。

本节介绍如何使用你的 OpenLinux 计算机充当路由器。以下是当 OpenLinux 计算机用作局域网与 Internet 之间的路由器时发生情况的一个相当简单的示例：

- OpenLinux 系统至少有两个接口：一个连接到办公局域网，一个连接到 Internet。
- 局域网上未发往局域网上已知计算机的数据包会被转发到路由器（即充当路由器的 OpenLinux 系统）。
- 路由器随后将其数据包转发到其另一个接口（可能是到 Internet 的 PPP 连接）。

你可以将 Linux 计算机设置成专用路由器。Linux Router Project (`http://www.psychosis.com/linux-router`) 是一个可放入 3.5 英寸软盘的迷你 Linux 发行版。有了它，你可以用完整的 Linux 系统更简单地维护路由器和终端服务器。这是一种利用储藏室里那台 486 的好方法。

以下章节将介绍如何设置 OpenLinux 路由器，以及将使用此路由器的局域网客户端计算机（OpenLinux 和 Windows 客户端）。之后，将介绍设置 IP 链和伪装的程序，供使用私有局域网地址并关心安全性的用户使用。

## 第 17 章 连接到 Internet

### 配置 OpenLinux 路由器

要将你的 OpenLinux 计算机配置为路由器，你需要具备一些条件。设置路由之前需要做以下工作：

- 连接到你的局域网。添加一块网卡并在（`/etc/hosts` 或 DHCP 服务器）中设置局域网计算机的地址。
- 连接到 Internet。从你的 OpenLinux 计算机设置到 ISP 的拨号或其他类型的连接。这在本章关于设置外发 PPP 连接的章节中已有描述。
- 将你的 OpenLinux 计算机配置为路由器。此过程在本节的其余部分中描述。

您在 LAN 上使用的 IP 地址类型会影响本程序中的几个步骤。以下是区别：

- **私有 IP 地址**—如果您的 LAN 上的计算机使用私有 IP 地址（见第 16 章所述），您需要设置 IP 伪装。因为这些号码是私有的，当 OpenLinux 路由器转发它们的请求时，必须将其隐藏在互联网之外。经过伪装转发的包在外部世界看来似乎来自转发包的 OpenLinux 计算机。
  `ipfwadm` 包已不再推荐用于执行 IP 转发。相反，应使用 `ipchains`，如本章所述。
- **有效 IP 地址**—如果您的 LAN 使用由 ISP 或注册机构正式分配的地址，则无需进行任何特殊的 IP 伪装。

在 OpenLinux 计算机的 LAN 和 Internet 接口就绪后，请按照以下步骤将 OpenLinux 设置为路由器（以 `root` 身份从终端窗口操作）：

1. 打开 `/etc/sysconfig/network` 文件。
2. 在文件中添加行 `IPFORWARDING=yes`。完成后，该文件的内容应类似于以下内容：

```
NETWORKING=yes
IF_LIST='to eth tr sl ppp'
IPFORWARDING=yes
FORWARD_IPWARDING_IPV4=yes
HOSTNAME=maple.handsonhistory.com
DOMAINNAME=handsonhistory.com
GATEWAYDEV=ppp0
```

3. `ip_forward` proc 文件的值应为 `1`。要验证这一点，请输入以下命令：

```
# cat /proc/sys/net/ipv4/ip_forward
```

如果不是这样（如果未设置为 `1`），请输入以下命令：

```
# echo 1 > /proc/sys/net/ipv4/ip_forward
```

4. 如果您的 LAN 上的计算机具有有效 IP 地址，请跳到配置 OpenLinux 路由客户端部分。如果您的计算机具有私有 IP 地址，请继续执行本程序。

下一步中的 `ipchains` 示例安全性不是很高，尽管在许多情况下它可以运行。我建议您阅读本章后面的 IP 伪装部分，以及第 15 章，以了解防火墙和其他安全问题的信息。

5. 要在 OpenLinux 路由器上启用 IP 伪装，您需要定义将进行伪装和转发的地址。以下是一个示例，其中 LAN 上网络号为 `10.0.0.0` 的所有计算机都被接受用于转发和伪装：

```
ipchains -P forward DENY
ipchains -A forward -s 10.0.0.0/255.0.0.0 -j MASQ
```

此示例显示，默认情况下转发被拒绝（`DENY`）。您的外部接口（即用于将数据包转发到 Internet 的接口）是 `ppp0`（您的第一个拨出 PPP 接口）。转发已完成；然而，对于网络 `10.0.0.0`（网络掩码为 `255.0.0.0`）上的计算机，如果数据包来自本地 OpenLinux 系统，则数据包将被转发到默认路由并进行伪装（`MASQ`）。

您可以为输入网络使用更短的名称。对于 A 类、B 类或 C 类网络，其值分别为 `8`、`16` 或 `24`。您可以不允许整个网络，而只允许单个主机。例如，您可以为 `10.0.0.11`、`10.0.0.12` 等分别设置单独的行。

要永久设置转发规则，您需要将它们添加到每次系统重新启动（或网络重新启动）时都会运行的启动脚本中。我将 `ipchains` 行添加到 `/etc/rc/init.d/network` 文件中，以便在网络启动时运行。我将它们放在 `case` 和 `start` 行之后，因此它们如下所示：

```
case "$1" in
(start)
ipchains -P forward DENY
ipchains -A forward -s 10.0.0.0/8 -i ppp0 -j MASQ
```

6. 此时，您可能希望重新启动 OpenLinux 系统。

7. 要检查您的 `ipchains` 命令是否生效，请按如下方式打印 `ip_fwchains` 文件内容：
