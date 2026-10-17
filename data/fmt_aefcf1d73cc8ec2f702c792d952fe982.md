
```
[root@server1]# ping -c 5 3.0.0.2
PING 3.0.0.2 (3.0.0.2) 56 (84) bytes of data.
64 bytes from 3.0.0.2: icmp_seq=0 ttl=128 time=0.448
64 bytes from 3.0.0.2: icmp_seq=1 ttl=128 time=0.401
64 bytes from 3.0.0.2: icmp_seq=2 ttl=128 time=0.403
64 bytes from 3.0.0.2: icmp_seq=3 ttl=128 time=0.419
64 bytes from 3.0.0.2: icmp_seq=4 ttl=128 time=0.439
---
3.0.0.2 statistics
5 packets transmitted, 5 received, 0% packet loss, time=4001ms
rtt min/avg/max/mdev = 0.401/0.422/0.448/0.018 ms, pipe 2

[root@server1 root]# _
```

> 如果 `ping` 命令未能从网络上的其他计算机接收任何响应，说明网络介质有问题。

也可以在桌面环境中配置 NIC 接口，如图 14-2 所示。只需导航到红帽菜单、系统设置、网络。

![](img/8fe037bf1ed016dccb79dbd1a27184f2_635_0.png)

图 14-2 配置网络接口

如果你突出网络接口并点击图 14-2 所示的 `Edit` 按钮，将提示提供相应的 IP 配置并点击 `OK`，如图 14-3 所示。

在编辑完 IP 配置后，务必点击文件菜单中的 `Save`，将你的更改保存到 `/etc/sysconfig/network-scripts` 目录下的相应文件中。接下来，为了在不重启的情况下激活更改，你需要点击 `Activate` 按钮。

![](img/8fe037bf1ed016dccb79dbd1a27184f2_636_0.png)

图 14-3 为网络接口配置 TCP/IP 信息

# 第 14 章 网络配置

## 配置 PPP 接口

与其在 NIC 上配置 TCP/IP 以获取网络访问，你也可以使用 WAN 协议（如 SLIP 或 PPP）在串口上运行 TCP/IP。PPP 是比 SLIP 更更新的技术，并整合了 SLIP 的所有功能；PPP 是今天通过串口连接远程网络的标准协议。

三种常用技术使用 PPP 将计算机连接到如互联网的网络：

- 调制解调器
- ISDN
- DSL

调制调器（调制解调器）设备使用 PPP 通过普通电话线发送 TCP/IP 信息；它们是过去十年家庭用户获取互联网的最常用方法。与大多数其他技术相比，调制调器连接今天被认为是慢的；大多数调制调器只能以 56KB/s 的速度传输数据。调制调器通常在安装期间或随后的设置提示中检测并配置。由于调制调器在串口上传输信息，系统通常会创建一个名为 `/dev/modem` 的符号链接，指向正确的串口设备，例如指向 COM1 的 `/dev/ttyS0`。

集成业务数字网络（ISDN）最初旨在取代普通电话线，并允许以 128KB/s 的速度传输数据。ISDN 使用 ISDN 设备连接到与普通电话线不同的介质。尽管 ISDN 在欧洲很流行，但在北美并没有广泛应用。与现代拨号器一样，ISDN 拨号器通常由内核或在安装期间进行检测和配置。

北美最流行的连接技术之一是 DSL。DSL 有许多变体，例如异步 DSL（ADSL），它是北美各家庭最常用的 DSL；以及高比特 DSL（HDSL），它常见于业务环境；为了简单起见，所有 DSL 变体统称为 xDSL。你使用以太网网卡（NIC）通过 TCP/IP 和 PPP 连接到 DSL 拨号器；DSL 拨号器通过普通电话线传输信息，速度可以超过 8MB/s。由于 DSL 拨号器通过某种介质连接到网卡，它们通常不会在安装期间或由内核自动配置；相反，它们通常需要手动配置。

配置 PPP 连接需要内核中编译了 PPP 或作为模块可用 PPP、PPP 守护进程（`pppd`）以及一系列辅助工具，例如用于与拨号器通信的 `chat` 程序。以前的 PPP 配置非常繁琐；你必须创建一个包含建立 PPP 连接所需的全部信息（用户名、密码等）的脚本，一个连接脚本，以及一个包含 PPP 守护进程所用设备参数的程序（如用于启动网络通信的 `minicom`）。由于 TCP/IP 配置通常由你连接的互联网服务提供商（ISP）分配，因此在过程中很少需要配置。

今天，各种图形化程序可以配置必要的文件并启动必要的实用程序以允许 PPP 网络通信。在 Red Hat Linux 中，你只需导航到 Red Hat 按钮、系统设置、网络（如前面的图 14-2 所示），然后点击“新建”（New）按钮并指定要添加的设备类型，如图 14-4 所示。

如果你选择从图 14-4 中配置调制解号器连接或 ISDN 连接，系统会先后提示输入图 14-5 和图 14-6 所示的设备信息。

无论你为现代连接还是 ISDN 连接配置硬件，系统都会提示输入 ISP 和 TCP/IP 信息，如图 14-7 和图 14-8 所示。

或者，如果你选择从图 14-4 设置 xDSL 连接，系统会提示你选择连接到 DSL 拨号器的以太网接口以及 ISP 信息，如本章稍后的图 14-9 所示。

![](img/8fe037bf1ed016dccb79dbd1a27184f2_638_0.png)

图 14-4 添加网络接口

![](img/8fe037bf1ed016dccb79dbd1a27184f2_638_1.png)

图 14-5 选择调制解调器硬件

与配置网卡一样，每个 PPP 设备的信息存储在 `/etc/sysconfig/network-scripts/` 目录下名为 `ifcfg-InternetServiceProviderName` 的文件中。例如，之前为 xDSL 连接配置的信息存储在 `/etc/sysconfig/network-scripts/ifcfg-isp` 文件中，如下输出所示：

```
[root@server1 root]# cat /etc/sysconfig/network-scripts/ifcfg-isp

# Please read /usr/share/doc/iniciitsd-*/sysconfig.txt

# for the documentation of these parameters.

IPV6INIT=no

BOOTON=no

USERCTL=yes

PEERDNS=yes

TYPE=xDSL

DEVICE=ppp0

BOOTPROTO=dialup

PIDFILE=/var/run/pppoe-adsl.pid

FIREWALL=NONE

PING=

PPPOE_TIMEOUT=80

LCP_FAILURE=3

LCP_INTERVAL=20

CLAMPMSS=1412

CONNECT_POLL=6

CONNECT_TIMEOUT=60

PERSIST=no

SYNCHRONOUS=no

DEFROUTE=yes

USER=1

ETH=eth0

PROVIDER=isp

DEMAND=no
```

PPP 守护进程使用的其他配置存储在 `/etc/ppp` 和 `/etc/isdn` 目录。双检查连接 ISP 使用的密码很好，因为错误的密码是 PPP 连接中最常见的问题。这些密码存储在两个文件中：`/etc/ppp/pap-secrets`（密码认证协议密钥）和 `/etc/ppp/chap-secrets`（挑战握手认证协议密钥）。如果 ISP 在网络上接受明文形式的密码，则 `/etc/ppp/pap-secrets` 将填充正确的密码；然而，如果 ISP 需要更安全的方法来验证用户身份，则 `/etc/ppp/chap-secrets` 中的密码会自动添加到两个文件中，如下所示：

```
[root@server1 root]# cat /etc/ppp/pap-secrets

# Secrets for authentication using PAP

# client server secret IP addresses

###### redhat-config-network will overwrite this part!!! (begin) ####

"user1"          "isp"           "secret"

###### redhat-config-network

###### redhat-config-network will overwrite this part!!! (end)
```

```
[root@server1 root]# cat /etc/ppp/chap-secrets

# Secrets for authentication using CHAP

# client server secret IP addresses
```
