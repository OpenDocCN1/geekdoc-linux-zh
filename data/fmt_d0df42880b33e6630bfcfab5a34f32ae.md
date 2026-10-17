
```
local-IPAddress=remote-IPAddress
```

服务器上的 PPP 用户 shell 设置为 `/usr/bin/pppd` 以守护程序自动启动。所有的认证密钥都必须提前用 `ssh-agent` 设置好，这样就不会提示密码。在客户端，配置在 `/etc/ppp/peers` 目录中完成，并为服务器指定文件名——我们将该配置命名为 "my-work"。客户端的 `/etc/ppp/peers/my-work` 文件包含：

```
- noauth
- debug
- logfile pppd.log
- passive
- silent
- pty "ssh -t user@remotehost"
```

从家里通过安全 PPP 连接登录，用户只需输入 `pppd call my-work`。

最后，我们包含一个使用 `wvdial` 命令及其看似必要的简单配置脚本的示例：`/etc/wvdial.conf`：

```
[Dialer Defaults]
Phone = phonumber
Username = login-name
Password = password
Modem = /dev/tty1
```

```
[Dialer creditcard]
Phone = long-distance-access-code,phone-number,cc-number
```

![](img/4baff4a9c0bcfa44e5d38fbdc1a0e2_336_0.png)

# Linux 管理

`wvdial` 被调用时带有参数，Red Hat 和 Debian 系统上使用守护程序，而在 SuSE 上使用 `local2`。遗憾的是，`ifdown` 会杀死 `pppd` 以解决问题。这里是连接建立后 `ppp` 接口的配置示例：

```
% ifconfig pp0
pp0 Link encap:Point-Point
addr 10.0.0.56 P-T:10.0.0.56 Mask:255.255.255.255
UP RUNNING OVER MULTAST MTU:1500 Metric:1
RX packets:125 errors:0 overruns:0 frame:0
TX packets:214 errors:0 overruns:0 carrier:0
collisions:0 txqueelen:3
RX bytes:11446 (11.1 KB) TX bytes:105586 (103.1 KB)
```

```
% netstat -nr
```

| 内核 IP 路由表 | | | | |

| --- --- --- --- --- |

| Destination Genmask Flags MSS Window Iface |

| 10.0.0.55 255.255.255.255 UH 40 0 pp0 |

| 0.0.0.0 10.0.0.55 0.0.0.0 UG 40 0 pp0 |

你可以通过 `pppstats` 获取 PPP 连接及其传输数据包的统计信息：

```
% pppstats
| IN PACK VICOMP VIUNC VIJUNC | OUT PACK VICOMP VIUNC NON-VI |
| 11862 133 8 96 0 | 11446 226 27 89 110 |
```

`VIJCOMP` 列计算 Van TCP Header，`VIUNC` 列计算不包含它的包。详情请参阅 RFC1144。

调试 PPP 连接可能非常痛苦，因为涉及到许多人。`pppd` 在 Red Hat 和 Debian 系统上将日志记录到守护设施，在 SuSE 上记录到 `local2`。你可以通过在 `pppd` 命令行中使用 `debug` 标志或在选项文件中请求日志来增加日志级别。`peter` 提供了详细的退出码，如果你尝试运行 `pppd` 时它崩溃了，恢复退出码并在 `pppd` 手册中查找该值。

# 第 13 章 TCP/IP 网络

SUSE Linux 倾向于为每个子系统包含示例配置文件，这些文件大多带有注释，但解释了格式以及可用选项的含义。SuSE 的 `/etc/ppp` 目录下的文件也不例外；它们有完善的文档，并为许多参数包含了合理的建议值。

![](img/4baff4a9c0bcfa45d38f4bdc1a0e2_338_0.png)

Debian 拥有文档完善的 PPP 示例配置文件。它有一个专门用于 chat 脚本的子目录 `/etc/chatscripts`。要使用 PPP 启动接口，你可以在 `/etc/network/interfaces` 文件中包含该接口，并使用 `ppp` 方法和 `provider` 选项将你的提供者名称（在本例中为 `my-isp`）绑定到 `/etc/peers` 目录下的一个文件名（`/etc/peers/my-isp`）。例如：

```
iface eth0 inet ppp
    provider my-isp
```

在这种情况下，将使用 Debian 特有的命令 `pon` 和 `poff` 来管理连接。

## 13.14 LINUX 网络怪异

与大多数内核不同，Linux 会关注 IP 数据包中的服务类型（TOS），并对标记为交互式（低延迟）的数据包提供更快速的服务。太棒了！遗憾的是，微软方面的脑残行为导致你必须关闭这种完全合理的行为。

源自 Windows 95、98、NT 和 200 的所有数据包无论用途如何，都被标记为非活动。相反，UNIX 系统通常不会将任何数据包标记为交互式。如果你的 Linux 网关为 UNIX 和 Windows 系统的混合网络提供服务，Windows 数据包将始终获得优先对待。UNIX 的性能受影响可能会非常明显。

你可以在编译 Linux 内核时关闭基于 TOS 的数据包排序。只需拒绝“IP: use TOS value as routing”选项即可。

当启用掩码（NAT）时，它告诉内核在转发分片之前将分片重组为完整的数据包，即使内核必须立即对包进行重新分片以发送。这种重组可能会消耗几个 CPU 周期，但现在的 CPU 速度足够快，在现代机器上这不应该是问题。

Linux 允许你更改某些类型网络接口的 MAC 地址：

```
sudo ifconfig eth1
eth1 link enc Ethernet Haddr 00:02:B3:19:C8:87
    BROCAST MULTICAST MTU:1500 Metric:1
    RX packets:0 errors:0 overflows:0
    TX packets:0 errors:0 overflows:0
    collisions:0 txqueuel:100
    Interrupt:7 Base address:0xe80
```

```
sudo ifconfig eth1 ether 00:02:B3:19:C8:28
```

# Linux 管理手册

```
sudo ifconfig eth1
Link encap:Ethernet HWaddr 00:02:B3:19:C8:21
BROCAST MULTICAST MTU:1500 Metric:1
RX packets:0 errors:0 overflows:0
TX packets:0 errors:0 overflows:0
collisions:0 txqueuel:100
Interrupt:7 Base address:0xe80
```

这是一个容易导致故障的危险功能。它可能很有用，但应该仅作为最后的手段使用。

## 推荐阅读

STEVENS, W. RICHARD. TCP/IP Illustrated, Volume One: The Protocols. Reading, MA: Addison-Wesley, 1994. 有些过时，但内容扎实。

WRIGHT, GARY R., AND W STEVENS. TCP/IP Illustrated, Volume Two: The Implementation. Reading, MA: Addison-Wesley, 1995. 关于 TCP/IP 协议栈的优秀且详尽的指南。

STEVENS, W. RICHARD. UNIX Programming. Upper Saddle River, NJ: Prentice Hall, 1990. 学生的圣经。

STEVENS, W. RICHARD. UNIX Programming, Volume 1: Networking APIs—Sockets and XTI. Upper Saddle River, NJ: Prentice Hall, 1997. 原版很好。

STEVENS, W. RICHARD. UNIX Programming, Volume 2: Interprocess Communications. Upper Saddle River, NJ: Prentice Hall, 1998. 第二版包含了 IPv6。
