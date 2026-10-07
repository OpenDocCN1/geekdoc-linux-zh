

## ping

ping（Packet Internet Groper，互联网分组探测器）程序用于查询另一台系统并确认连接处于活动状态。ping 程序通过向目标机器发送请求以获取回复来工作。如果目标机器的 IP 软件接收到该请求，它会立即发出回复。

发送机器持续发送请求，直到通过中断序列终止 ping 程序。终止后，ping 会显示一组统计信息。一个典型的 ping 会话示例如下：

```
prudie> ping merlin
PING merlin: 64 data bytes
64 bytes from 142.12.130.12: icmp_seq=0. time=20. ms
64 bytes from 142.12.130.12: icmp_seq=1. time=10. ms
64 bytes from 142.12.130.12: icmp_seq=2. time=10. ms
64 bytes from 142.12.130.12: icmp_seq=3. time=20. ms
64 bytes from 142.12.130.12: icmp_seq=4. time=10. ms
64 bytes from 142.12.130.12: icmp_seq=5. time=10. ms
64 bytes from 142.12.130.12: icmp_seq=6. time=10. ms
--- merlin PING Statistics ---
7 packets transmitted, 7 packets received, 0% packet loss
round-trip - min/avg/max = 10/12/20
```

如果 ping 无法连接到远程机器，它会显示错误消息。你也可以 ping 本地主机（localhost），这可以检查回环驱动程序配置文件中是否存在错误。

ping 程序非常有用，因为它提供了四个重要信息：TCP/IP 软件是否正常工作，本地网络设备是否可以寻址（验证其地址），远程机器是否可以访问（再次验证地址并测试路由），以及验证远程机器上的软件。

## 摘要

在本章中，你了解了如何安装、配置和测试 Linux 机器的以太网连接。下一章将介绍许多 Linux 机器用于连接 ISP（互联网服务提供商）的 SLIP 和 PPP 协议。在 Linux 机器上通常还能找到的另一种网络进程是使用 UUCP（UNIX-to-UNIX Copy，UNIX 到 UNIX 复制），这在第 44 章“NIS 和 YP”中进行了描述。

如果你想安装一个网络来连接你的多台机器（假设你拥有一台以上），你会发现这相当简单且实用。如果你有两台机器，只要另一台机器运行 TCP/IP，将 Linux 机器与 DOS 或 Windows 机器连接起来是非常快速且高效的。Windows 有 TCP/IP 的共享软件版本，DOS 和 Windows 也有许多商业实现版本。

从这里，你可以阅读下一章以了解 SLIP 和 PPP，或者跳读以下内容：

- 如何在第 42 章“网络安全”中配置网络以获得适当的安全性。
- 如何分别在第 43 章“NFS”和第 44 章“NIS 和 YP”中配置 NFS、NIS 和 YP。
- 如何在第 47 章“设置互联网站点”中利用你已联网的 Linux 系统设置互联网站点。

![](img/e8e6b47ac20475e23d48b4c476f5d891_700_0.png)

## SLIP 和 PPP

作者：Tim Parker

### 本章导读

- 设置虚拟接口 666
- 设置 SLIP 667
- 设置 PPP 671
- 使用 DNS 配合 SLIP 和 PPP 678

大多数希望通过 ISP 或网关连接到互联网的 UNIX 或 Linux 系统，均使用串行线路互联网协议（SLIP）或点对点协议（PPP）。SLIP 和 PPP 均通过拨号调制解调器（无论是异步、同步还是 ISDN）与远程系统建立链接。Linux 同时提供了 SLIP 和 PPP，以及 SLIP 的增强版本 CSLIP（压缩 SLIP）。

你可以配置 Linux TCP/IP 时执行 SLIP 和 PPP 的配置，也可以等到需要设置互联网访问时再进行。大多数互联网服务提供商倾向于让小系统使用 SLIP 或 PPP 访问，因为它们提供快速、高效的传输。因此，如果你计划使用 ISP，最终你很可能需要自己配置这些协议。

在 Linux 系统上设置 SLIP 或 PPP 的步骤并不太复杂。按照本章所示的过程，你可以在几分钟内完成 SLIP 或 PPP 的设置。

### 设置虚拟接口

虚拟接口（也称为回环接口或设备）用于在机器仅使用 SLIP 和 PPP 接口时，为其提供一个可用的 IP 地址。虚拟接口解决了独立机器没有网卡连接到其他机器的问题。大多数 TCP/IP 服务和应用程序需要一个 IP 地址，而在独立配置中通常缺乏这一点。因此，回环驱动程序被配置有一个标准的 IP 地址（127.0.0.1）。

创建虚拟接口很简单。如果你的机器在 /etc/hosts 文件中已经分配了 IP 地址，你只需设置接口并创建一个路由即可。对于 Linux，所需的两个命令如下：

```
ifconfig dummy machine_name
route add machine_name
```

machine_name 是你的本地机器名称。这会创建一个指向你自己 IP 地址的链接。如果你机器的 /etc/hosts 文件中没有 IP 地址，你应该在创建虚拟接口之前手动编辑 /etc/hosts 文件并添加一行，如下所示：

```
127.0.0.1    loopback
```

一些 Linux 系统不使用 ifconfig 和 route 实用程序，而是依赖菜单驱动的用户界面来设置相同的参数。在大多数 Linux 情况下，安装 Linux 时会自动为你添加回环驱动程序。请检查 /etc/hosts 文件中是否有 IP 地址为 127.0.0.1 的行。如果不存在，请使用你的 Linux 版本用于设置新链路的例程，或者简单地使用编辑器将其添加到文件中，然后重新启动机器以使更改生效。

### 设置 SLIP

SLIP 可用于许多拨号 ISP，也可用于与其他配备 SLIP 的机器进行网络连接。当你要与另一台机器建立 SLIP 连接时，调制解调器照常建立连接，然后 SLIP 接管并为你维护该会话。SLIP 驱动程序通常作为操作系统内核的一部分进行配置，因此如果尚不存在，需要添加它。大多数 Linux SLIP 驱动程序也可以处理 CSLIP，这是一种提供更高吞吐量的压缩版 SLIP。（并非所有 ISP 都支持 CSLIP，因此你在为其连接进行配置之前应先与他们确认。）

对于使用 SLIP 进行连接的许多 Linux 操作系统，必须为此专门指定一个串行端口。这意味着串行端口必须专门配置为使用 SLIP，而不能用于任何其他目的。内核使用一个通常称为 SLIPDISC（SLIP 规约）的特殊程序来控制串行端口，并阻止非 SLIP 应用程序使用该端口，即使该端口未被 SLIP 使用也是如此。

### 配置 SLIP

在 SLIP 连接中，涉及两个 Linux 程序：dip 和 slattach。这两个程序都可以用于启动 SLIP 连接。由于 SLIP 使用特殊的系统调用，因此你无法使用标准的通信程序拨号连接到 SLIP 线路。

dip 和 slattach 具有不同的用途。slattach 程序仅连接到串行设备，在存在到 SLIP 服务器的永久连接时使用（无需调制解调器或设置握手）。dip 程序处理连接的发起、登录以及连接握手。如果你使用调制解调器连接到 SLIP 服务器，应使用 dip。dip 程序还可以用于将你的系统配置为 SLIP 服务器，允许其他人拨入连接。

SLIP 是一种相当简单的网络协议，因为只涉及两个设备：你的设备和服务器设备。连接建立后，SLIP 会发送一个用于该连接的 IP 地址。一些系统使用相同的 IP 地址（静态），而另一些系统在每次建立连接时使用不同的 IP 地址（动态）。每种类型的配置略有不同。

![](img/e8e6b47ac20475e23d48b4c476f5d891_704_0.png)

将串行端口专门用于 SLIP 的最简单方法是 slattach 程序。大多数 Linux 版本都支持此命令。slattach 命令将串行端口的设备名称作为参数。例如，要将第二个串行端口（取决于操作系统，为 /dev/cua1 或 /dev/ttyS1）专门用于 SLIP，请发出以下命令或类似命令，用正确的设备名称代替 /dev/cua1（这是 Linux 对调制解调器串行端口的约定）：

```
slattach /dev/cua1 &
```

slattach 命令通过 ampersand（&）发送到后台模式。如果未发送到后台，意味着发出该命令的终端或控制台在进程终止之前将不可用。如果你愿意，可以将 slattach 命令嵌入启动文件中，例如 rc 文件或会话 shell 启动文件。

一旦 slattach 命令成功执行，串行端口将设置为第一个 SLIP 设备（通常为 /dev/sl0）。如果你使用多个串行端口用于 SLIP 线路，需要为每个线路发出命令。默认情况下，大多数 Linux 系统将 SLIP 端口设置为使用 CSLIP（压缩 SLIP）。如果你想覆盖此操作，请使用 -p 选项和此设备名称：

```
slattach -p slip /dev/cua1 &
```

确保连接的双方使用相同形式的 SLIP 至关重要。存在 slip6（SLIP 的 6 位版本）和自适应 SLIP（调整以适应连接另一端的内容）。例如，你不能将你的设备设置为 CSLIP 并与另一台运行 6 位 SLIP 的机器通信。

串行端口设置为 SLIP 使用后，使用与普通网络连接相同的程序配置网络接口。对于 Linux，使用的命令是 ifconfig 和 route。例如，如果你的机器名为 merlin，并且你要呼叫远程机器 arthur，请发出以下命令：

```
ifconfig sl0 merlin-slip pointopoint arthur
route add arthur
```

上面的 ifconfig 命令将接口 merlin-slip（SLIP 接口的本地地址）配置为与 arthur 的点对点连接。route 命令将名为 arthur 的远程机器添加到路由表中。

如果你要使用 SLIP 端口访问互联网，它必须拥有 IP 地址并且在 /etc/hosts 文件中有条目。这使 SLIP 系统在互联网上拥有有效的条目。

在 ifconfig 和 route 命令执行后，你可以测试和使用你的 SLIP 网络。如果你决定在未来移除 SLIP 接口，你必须首先移除

