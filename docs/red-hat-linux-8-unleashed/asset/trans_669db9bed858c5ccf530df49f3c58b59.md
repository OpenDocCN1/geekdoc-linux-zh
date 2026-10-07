

## 第 15 章 网络连接

将为你的计算机提供静态或动态 IP（互联网协议）地址。动态 IP 地址在每次拨号时都会更改，而静态 IP 地址则保持不变。IP 还可能自动为你的计算机提供域名服务（DNS）服务器的名称。你需要知道计算机建立连接时拨打的电话号码；你的 ISP（服务提供商）也会提供该号码。你还需要一个调制解调器并知道调制解调器的设备名称（通常为 `/dev/modem`）。

> 注意
大多数 IP 由 ISP 动态分配的；它们拥有一个地址池，你会获得任何可用的地址。从它们的角度来看，少量的地址就可以服务大量用户，因为并不是所有人都会同时在线。对于大多数互联网服务，动态 IP 是可行的，因为向你提供信息是 ISP 的工作，而你处于你与所使用的服务之间的中间。但动态 IP 会发生变化，如果有人需要在同一个地址找到你（例如，你运行一个网站或进行文件传输），那么每次登录都会更改的 IP 将无法良好工作。为此，你需要静态 IP。由于你的 ISP 无法将该地址复用给其他客户，普通消费者并不需要静态 IP 的优势，他们乐意为动态分配的 IP 付费。此外，DNS 信息可以通过动态主机配置协议 DHCP 由 ISP 自动提供。这部分将在第 13 章“网络连接”中讨论。

如果你正在使用 DSL 访问或电缆调制解调器，你可能通过 DHCP 获得动态 IP，或者被分配静态 IP。如果你使用 DHCP，将自动为你提供 DNS 服务器，或者你需要手动设置 DNS（在这种情况下，你需要知道 DNS 服务器的 IP 地址）。

在所有情况下，你都需要知道你的用户名、密码，以及其他服务的配置，如邮件服务器名称和新闻服务器名称。这些信息可以向 ISP 专门请求获取。

> 注意
书中的信息将帮助你理解并避免许多连接问题，但你可能会遇到连接问题。请准备好 ISP 技术支持的电话，以防无法建立连接。请注意，很少 ISP 提供 Linux 支持，如果你的特殊情况无法通过从书中获得的知识来解决，你可能需要向熟悉 Linux 的朋友或 Linux 用户组寻求帮助。

## 建立基础：localhost 接口

在连接互联网或网络之前，你必须创建一个虚拟或本地接口。该接口被称为 `lo`（环回接口），用于 TCP/IP 协议为你的机器分配 IP 地址，并且建立 PPP 接口所必需。`lo` 接口也被许多感知网络的应用程序使用，并且于设置。

### 检查环回接口的可用性

Red Hat 通常在安装过程中处理此接口设置。你可以使用 `ifconfig` 命令查看它是否已可用。如果 `lo` 可用，命令及其响应将类似于下所示：

```
# /sbin/ifconfig
lo Link encap:Local Loopback
  inet addr:127.0.0.1 Mask:255.0.0.0
  UP LOOPBACK MTU:16384 Metric:1
  RX packets:1 errors:0 overflows:0 carrier:0
  TX packets:0 errors:0 overflows:0 txuel:0
  RX bytes:760 (760 bytes) TX bytes:760 (760 bytes)
```

示例输出显示环回接口处于激活并运行状态，它被分配了环回 IP 地址 127.0.0.1，使用了 255.0.0.0 的广播掩码，且接口没有产生流量（RX = 接收，TX = 发送）。如果没有看到类似的内容，在阅读本节剩余部分后，你可能需要手动配置 localhost 接口。否则跳到下一节。

### 手动配置环回接口

`localhost` 接口的互联网协议（IP）地址在 Linux 用于存储地址的文本文件中定义。文件名为 `/etc/hosts`，即使它是空的也应该存在。该文件为 Linux 内核和其他网络相关工具提供 IP 地址和关联主机。在配置网络接口之前，你可能会发现 `/etc/hosts` 文件只包含一行：

```
127.0.0.1 localhost
```

此行定义了 `localhost` 接口并分配了 IP 地址 `127.0.0.1`。你可能会听到或读到如 `localhost`、`loopback` 和 `dummy interface` 等术语；这些术语都指向 IP 地址 `127.0.0.1` 的使用。`loopback interface` 表示 Linux 正在与一个由一台机器组成的网络通信；内核向自身发送和接收流量。`dummy interface` 表示从外部世界来看，该接口并不存在；它只存在于本地机器。你可以在第 13 章阅读更多关于网络的知识。

局域网（LAN）上的每台联网机器都会使用相同的 IP 地址 `localhost`。如果由于某种原因 Red Linux 没有此接口，请编辑 `/etc/hosts` 文件添加条目，然后以 root 身份使用 `ifconfig` 命令创建接口：

```
# ifconfig lo 127.0.0.1
# route add lo
```

这些命令将在内存中创建 `localhost` 接口（使用 Linux 时 `eth0` 或 `ppp0` 等接口也在内存中创建），并将 IP 地址 `127.0.0.1` 添加到内存表中，以便 Linux 内核代码跟踪不同地址的路由。

使用之前显示的 `ifconfig` 命令测试接口。你现在应该能够使用 `ping` 命令检查接口响应正常，如下（使用 `localhost` 或其 IP 地址）：

```
# /bin/ping -c 3 localhost
PING localhost.localdomain (127.0.0.1): 56(84) bytes of data.
64 bytes from localhost.localdomain (127.0.0.1): icmp_seq=0 ttl=255 time=0 ms
64 bytes from localhost.localdomain (127.0.0.1): icmp_seq=1 ttl=255 time=0 ms
64 bytes from localhost.localdomain (127.0.0.1): icmp_seq=2 ttl=255 time=0 ms

--- localhost.localdomain ping statistics ---
3 packets transmitted, 3 packets received, 0% packet loss
round-trip min/avg/max/stddev = 0.050/0.114/0.070 ms
```

`-c` 用于设置 ping 的次数，并返回向指定主机发送测试包的往返速度。

## 配置拨号上网

大多数 ISP 使用 PPP 提供拨号连接，因为它是串行线路 TCP/IP 的一种快速且高效的协议。PPP 设计用于双向网络；TCP/IP 为数据提供传输协议。新 Red Linux 用户面临的一个障碍是如何设置 PPP 并连接网络。使用 PPP 并不需要理解其协议的细节，设置 PPP 连接非常简单。你可以使用命令行手动配置 PPP 连接，也可以在 X 会话期间使用 Red Hat 的网络向导进行图形化配置。每种方法产生相同的结果。

PPP 使用系统上的几个组件。第一个是名为 `pppd` 的守护进程，控制 PPP 的使用。第二个是名为高级数据链路控制（HDLC）的驱动程序，控制两台机器之间的信息流。第三个组件是名为 `slack` 的程序，当你需要时它为你拨号连接的另一端。尽管 PPP 有许多“可调”参数，但默认设置适用于大多数人。

> 注意
你可以通过从 root 命令行带有 `--help` 参数运行 `pppd` 命令来检查系统是否安装了 PPP，如下：

```
# pppd --help
```

如果安装了 PPP，此列表将列出当前版本并并描述选项。如果系统中没有安装 PPP，请使用 Red Hat 的 `rpm` 命令从第二个 Red Linux CD-ROM 安装 PPP 包，或使用系统设置菜单中的“软件包”项。第 8 章“管理软件和系统资源”涵盖了使用 rpm 和图形包管理器的细节。

### 手动配置拨号连接

手动配置 PPP 的第一步是以 root 身份登录并复制编辑必要的文件。登录后，你将使用 `chat` 命令、`pppd` 守护进程和几个文件来配置 PPP：

- `/etc/ppp/ppp-on`:用于启动 PPP 连接。该文件包含 ISP 的电话号码、你的用户名和密码，以及各种选项，如 IP 地址选项、调制解调器设备及其设置（如波特率）。
- `/etc/ppp/ppp-off`:终止 PPP 连接。
- `/etc/ppp/ppp-dialer`:配合 `chat` 命令执行拨号和协商；chat 脚本创建远程系统与 chat 脚本之间的错误处理和协商响应。

> 注意
许多软件调制解调器无法在 Linux 上工作，因为制造商不发布它们的编程信息或提供 Linux 驱动。外部串口调制解调器或 ISA 调制解调器几乎可以使用；USB 和 PCI 调制解调器仍然有问题。建议你使用型号名称和数字进行彻底 Google 搜索，查看他人如何解决特定调制解调器的问题。本章末尾有调制解调器网站的链接。

