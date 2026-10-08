
```
[root@vtun-client /root]# netstat -nr
Kernel IP routing table
Destination Gateway Genmask Flags MSS Window Use Iface
10.3.0 0.0.0.0 255.255.255.255 UH 40 0 0 tun1
10.3.0 10.3.0.1 255.255.255.255 UG 40 0 0 tun1
192.168.2.0 0.0.0.0 255.255.255.0 U 40 0 0 eth1
192.168.1.0 10.3.0.1 255.255.255.0 UG 40 0 0 tun1
127.0.0.0 0.0.0.0 255.0.0.0 U 40 0 0 lo
0.0.0.0 0.0.0.0 65.254.255.0 U 40 0 0 eth0
```

作为最后的测试，你应该尝试 `ping` 隧道远侧的 IP 地址。

```
[root@vtun-serv ~]# ping -c 3 192.168.254.254
PING 192.168.254.254(192.168.254.254) from 192.168.254.253 : 56(84) bytes of data.
64 bytes from 192.168.254.254: icmp_seq=0 ttl=255 time=729.680 msec
64 bytes from 192.168.254.254: icmp_seq=1 ttl=255 time=338.135 msec
64 bytes from 192.168.254.254: icmp_seq=2 ttl=255 time=366.832 msec
```

最后，为了完成端到端连通，你应该 `ping` 远程网络。

```
[root@vtun-serv ~]# ping -c 3 192.168.1.10
PING 192.168.1.10(192.168.1.10) from 192.168.254.253 : 56(84) bytes of data.
```

## 以太网隧道

对于我们的下一个 VPN，将在两个站点之间配置一个以太网隧道。以太网隧道允许我们转发 IP 流量，以及运行在以太网上的任何三层流量。设置以太网隧道需要一些额外的命令，比 IP 隧道复杂一点。除了 VTun 配置外，你还需要安装并运行 `bridge-utils` 包中的 `brctl` 命令。图 8.4 显示了桥接接口、`tap` 接口和以太网隧道之间的关系。

### 以太网隧道服务器

以太网隧道的大部分配置与之前提到的 IP 隧道相同。需要做的更改之一是设备设置。因为以太网隧道使用 TAP 驱动因此有一个 `tap` 接口，这需要在配置中体现。第二个更改是针对跨隧道转发的所有协议的 `up` 部分。在此示例中，`up` 部分将创建一个桥接接口，绑定内部以太接口和 `tap` 接口。接口绑定后，它们的 IP 地址将被清零，并将以太接口的 IP 地址重新分配给桥接接口。这将允许使用以太接口作为网关的设备进行 IP 访问，同时将以太网看到的所有以太网流量桥接到 `tap` 接口。

注意，对于这个示例，`192.168.1.0/24` 和 `192.168.2.0/24` 之间的 IP 连接并不是目标。这纯粹是为了封装以太网流量。

示例配置文件如下所示：

```
Ether-tunnel {
    pass password1;
    type ether;
    proto tcp;
    comp zlib:9;
    encr yes;
    keepalive yes;

  up {
    ifconfig %192.168.254.253 netmask 255.255.255.252;
    brctl addbr bridge0
    brctl addif bridge0 eth1
    brctl addif bridge0 %;
    ifconfig eth1 0.0.0.0;
    ifconfig % 0.0.0.0;
    ifconfig bridge0 192.168.1.254 netmask 255.255.255.0;
  }
  down {
    brctl delbr bridge0
    ifconfig eth1 192.168.1.254 netmask 255.255.255.0;
  }
};
```

如果你想在以太网上添加另一种协议的支持，可以在 `up` 部分添加相应的协议路由信息。

### 广播

请注意，在此项配置中，所有广播流量都将跨隧道转发。尽管这可能会显著降低你的 VPN 性能。

在 `up` 部分，添加了 `brctl` 命令来创建一个名为 `bridge0` 的桥。一旦桥创建，我们就添加 `eth1` 和新创建的 `tap` 接口（由 `%` 引用）。将这两个接口添加到桥中将镜像原始以太网帧，从而实现 `192.168.1.254` 的 IP 连通性。一旦桥创建，使用 `brctl show` 查看状态。

除了协议路由信息外，需要做的另一个更改是 `type` 字段。

### 以太网隧道客户端

以太网隧道客户端的配置方式与 IP 客户端非常相似。部分配置选项不同。

```
Default {
  Port 5000;
}

Ether-Tunnel {
  pass password1;
  type ether;
  proto top;
  keepalive yes;

  up {
    ifconfig %192.168.254.253 netmask 255.255.255.252;
    brctl addbr bridge0
    brctl addif bridge0 eth1
    brctl addif bridge0 %;
    ifconfig eth1 0.0.0.0;
    ifconfig % 0.0.0.0;
    ifconfig bridge0 192.168.1.254 netmask 255.255.255.0;
  }
  down {
    brctl delbr bridge0
    ifconfig eth1 192.168.1.254 netmask 255.255.255.0;
  }
}
```

`bridge0 8000.002078102dc4 yes eth1 tap0 VTun Configuration 257`

从此命令的输出可以看出，`eth1` 和 `tap0` 均属于 `bridge0`。

## 串口隧道 (Serial Tunnel)

在无法使用 `tun` 或 `tap` 接口的场景下，你可以建立串口隧道。如前所述，串口隧道会创建一个虚拟串口链路并充当隧道使用。在本例中，我们将创建一个 PPP 隧道。`PPP` 是为点对点链路设计的，这也是隧道接口的配置方式。

图 8.5 是将用 PPP 隧道构建的 VPN 高级结构图。

![](img/ac8d70f99c3fa1e7029fbd036fc254da_274_0.png)

图 8.5 串口隧道。

### 串口隧道服务器

串口隧道服务器将使用服务器模式下的 PPP 向客户端传 own IP 信息。

```
PPP-tunnel {
  pass password1;
  comp yes;
  encr yes;
  up {
    ppp "192.168.254.254:192.168.254.253 proxyarp";
    route "add -net 192.168.2.0/24 gw 192.168.254.253";
  }
}
```

`up` 部分中的 `ppp` 语句指定了本地和远程 IP 地址。本地接口的 IP 为 `192.168.254.254`，远程 PPP 接口的 IP 为 `192.168.254.253`。`proxyarp` 告诉 PPP 向系统 ARP 表中添加条目，包含远程 PPP 接口的 IP 地址和本地接口的硬件地址。这创建了一种远程 PPP 接口连接到本地网络的幻象，因为本地服务器将用自己的地址响应 ARP 请求。

### 串口隧道客户端

与其他隧道类型一样，隧道选项从服务器传递给客户端。`PPP` 也会从 PPP 服务器获取地址，因此 `up` 部分的语句较少。

```
PPP-tunnel {
  pass default;
  up {
    ppp "noipdefault";
    route -add 192.168.1.0/24 gw 192.168.254.254";
  }
}
```

在该部分，正如我们之前的那样，为远程 VPN 网络添加了路由。或者，由于 PPP 接口的 IP 地址未在本地配置，可以使用设备名称代替 IP 地址来添加路由。通过设备添加路由的命令如下：

```
route -add 192.168.1.0/24 dev ppp0
```

此外，注意串口隧道建立连接比其他隧道类型耗长时间。这是由于 PPP 守护进程协商 PPP 协议需要额外的时间。由于连接较慢，这可能会导致输出部分中的语句失败。在建立连接后，你应该双检串口隧道，以确保所有路由已就绪。

在 VTun 客户端上启动 PPP 隧道，输入以下命令：

`vtund tunnel 270.8.8.8`

如“PPP”部分所述，本地接口的 IP 地址将从服务器接收。`noipdefault` 设置告诉 PPP 客户端不要将 PPP 接口配置为默认路由。一旦链路建立，路由表中应包含包含以下行的条目：

| Destination | Gateway | Genmask | Flags | MSS Window | irtt Interface |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 192.168.254.253 | 0.0.0.0 | 255.255.255.255 | UH | 40 | 0 ppp0 |

此 PPP 隧道配置的工作与与章之前详细介绍的 IP 隧道相同。由于相似，我们能够使用相同的技术来测试并验证 PPP 隧道运行正常。

要测试 PPP 连接本身，我们可以测试远程端是否可达。如果我们在客户端上，可以使用 `ping` 来验证两个 PPP 接口正在通信。

```
PING 192.168.254.254 (192.168.254.254) from 192.168.254.253 : 56(84) bytes of
  -
64 bytes from 192.168.254.254: icmp_seq=0 ttl=255 time=196.615 msec
64 bytes from 192.168.254.254: icmp_seq=1 ttl=255 time=352.150 msec
64 bytes from 192.168.254.254: icmp_seq=2 ttl=255 time=274.243 msec
```

如果接口对 `ping` 有响应，我们可以继续测试，并使用 `ping` 测试远程网络的可达性。从客户端开始，我们应该能够 `ping` 网络上的 `192.168.1.0` 主机。

```
[root@vtun-cl]# ping -c 3 192.168.1.10
PING 192.168.1.10 (192.168.1.10) from 192.168.254.253 : 56(84) bytes of data
64 bytes from 192.168.1.10: icmp_seq=0 ttl=255 time=175.704 msec
64 bytes from 192.168.1.10: icmp_seq=1 ttl=255 time=150.991 msec
64 bytes from 192.168.1.10: icmp_seq=2 ttl=255 time=264.362 msec
```

### 真实测试

为了真正测试隧道路由是否正确完成，远程地址 `192.168.1.0` 应该是 VTun 服务器的 IP。如果隧道的任意端都能 `ping` 远程接口，也能 `ping` VTun 服务器背后的接口。

## 管道隧道示例 (Pipe Tunnel)

此示例的目标是将日志安全地传输到另一个归档服务器。出于安全考虑，我们将使用 VTun 加密流量防止无关人员查看日志文件。VTun 客户端将发送日志文件。管道隧道的第一步是决定使用哪个程序进行传输。如果在同一台机器上归档文件，可能会使用 `tar` 或 `cp` 命令创建备份。例如，如果想为 `/var/log/` 目录下的所有文件创建一个 `tar` 归档，输入：

```
tar -cvf log_backup.tar /var/log/*
```

这将创建一个名为 `log_backup.tar` 的 `tar` 归档。一旦确定了使用的命令，就需要将其分解到客户端和服务器部分。例如，服务器部分将存储输出。注意客户端和服务器的角色可以反转——服务器可以输出，客户端可以接收。要将 `tar` 的输出重定向到屏幕，使用 `-f` 选项。`-f` 选项赋予 `tar` 存储的文件名。`-` 选项将标准输出作为文件名。我们可以使用重定向 `>` 将 `tar` 命令的输出发送文件。

```
tar -cvf - /var/log/* > backup.tar
```

## 第 8 章 使用 VTun

在这里，`tar -cvf - /var/log/*` 部分是客户端部分，因为它将产生数据。`backup.tar` 部分是服务器部分，它将存储数据。图 8.6 显示来自 VTun 客户端的输出被重定向到 VTun 服务器。VTun 服务器使用 `cat` 命令接收输入并将其重定向到文件。

![](img/ac8d70f99c3fa1e7029fbd036fc254da_277_0.png)

图 8.6 管道隧道。

### 管道隧道服务器

管道隧道服务器将是归档文件的机器。对于管道隧道，这意味着它必须“接收”文件并将它们放入目录中。根据前述的示例命令，我们希望在此侧运行 `backup.tar` 命令来接收数据。

```
options {
  port 5000;
  default {
    compress no;
    speed 0;
  }
  Pipe-tunnel {
    type pipe;
    password1;
    encrypt yes;
    up {
      prog /bin/bash -c 'cat /var/backup/backup.tar*';
    }
}
```

从我们的配置示例来看，`type pipe` 配置 VTun 创建管道隧道。`encrypt yes` 行开启了 Blowfish 加密。最后，`prog` 和 `args` 是用于接收客户端输出的程序和参数。由于此示例是简单的重定向，我们可以使用 `/bin/bash` 接收输出并重定向到 `/var/backup/backup.tar`。`-c` 选项告诉 `bash` 执行 `-c` 之后的程序并退出。

```
[root@vtun-server log]# grep TUN /var/log/dmesg
Universal TUN/TAP device driver 1.3 1999-2000 Maxim Krasnyansky
```

### 不支持 ZLIB 压缩

此消息表示 VTun 编译时没有包含 Zlib 支持。要修复此问题，请下载并编译 Zlib。其他选项是使用 LZO 压缩（如果已安装）或完全禁用压缩。

### 不支持 LZO 压缩

当 VTun 尝试在未添加 LZO 支持的隧道上初始化 LZO 压缩时，会产生此错误。请禁用压缩或使用 Zlib。

### 会话网络超时

已建立的隧道丢失与远程端的连接。请确保远程端可达，且 VTun 在其上运行。

### 不支持加密

VTun 编译时没有包含 OpenSSL 支持。要修复此问题，你需要下载并安装 OpenSSL 库。

### 不支持流量整形

VTun 编译时没有包含流量整形支持。通过运行带有 `disable-shaper` 选项的配置脚本可以禁用流量整形。要解决此问题，请重新运行配置脚本并重新编译 VTun。

### 未定义主机

配置文件中没有定义隧道。请定义隧道（使用本章之前列出的示例作为指南）并重启 `vtund`。

### 连接超时

客户端在尝试连接服务器时超时。请通过 `ping` 确保服务器是可的。如果你正尝试通过名称连接，请确保 DNS 解析到正确的 IP 地址。此外，确保客户端和服务器的端口设置相同。

### 拒绝来自 *host* 的连接

服务器拒绝了客户端的连接。请确保两台机器上的密码相同。

在这些平台上安装 VTun 的步骤与在 Linux 上安装相似。在可能的情况下，本文列出的命令被设计为可以在其他平台上复用。

## 总结

在本章中，你学习了作为 VPN 解决方案的 VTun。VTun 提供了一种灵活的方法，用于在跨不可信的网络上创建安全隧道。由于 VTun 支持多种类型的隧道，它比许多竞争产品提供的 VPN 解决方案要强大得多。

有关 VTun 的更多信息，请访问 VTun 网站：http://vtun.sourceforge.net。

![](img/ac8d70f99c3fa1e7029fbd036fc254da_282_0.png)

# 9 cIPe

当你想要构建一个 VPN 时，特别是如果你频繁使用 UNIX，你往往倾向于使用更简单、更轻量级的包作为底层工具来在此基础上构建。之后，你可能想要添加脚本、`cron` 任务和其他漂亮的功能，因此，你选择的包具有高度的可定制性和简单性至关重要。

许多为了填补这一空白而设计的轻量级包最终往往为了简单性而牺牲了重要功能。然而，许多包或多提供了构建安全私有网络所需的最小功能。在本章中，我们将描述一种名为 `cIPe` 的包。

## cIPe 概述

Crypto IP Encapsulation (`cIPe`) 是一个简单、轻量级的包，提供在 UDP 上隧道化加密的 IP 数据包的功能。该包根据 GNU 的 GPL 协议发布，可以免费下载。本章中的示例基于该包的 `1.5.1` 版本，该版本支持 Linux 内核 v2.{2, 3, 4} 并主要关注 i386 平台。虽然 `cIPe` 有 Windows NT 端口，但考虑到本书的重点，我们将专注于 Linux 的实现。

## cIPe 组件及其功能
