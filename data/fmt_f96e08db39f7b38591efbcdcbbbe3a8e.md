
![](img/1ea833f5a3e3c1547e3dd2891f52804a_400_0.png)

*图 15.10*  *使用 netconf 为您的以太网适配器分配 IP 地址并控制其活动状态。*

系统管理员也可以使用 `netconf` 命令来创建接口。启动 `netconf`，单击“基本主机信息”按钮，然后单击“适配器 1”选项卡，如图 15.4 所示。将出现一个对话框，如图 15.10 所示。

请注意，您可以选择一种引导配置类型，如 DHCP，或手动分配 IP 地址。您还可以使用“启用”复选框来启用或禁用接口。请注意，Linux 最多支持四个以太网设备（使用较新的内核可能支持更多）。完成后，单击“接受”按钮，然后遍历 `netconf` 对话框以激活您的更改。

### 基本网络实用工具

本节介绍一些基本的实用工具，作为 root 操作员，您可以使用它们来创建、操作或测试您的接口。例如，您可以使用 `ifconfig` 命令手动创建以太网接口。此命令通常接受如下形式的参数：

```
ifconfig interface hostname/IP_address status
```

例如，由于在您的系统上创建的第一个以太网接口默认为 `eth0`，您可以像这样快速创建它：

```
# ifconfig eth0 cubic.home.org up
```

如果您尚未为计算机分配主机名，也可以像这样替换为其 IP 地址：

```
# ifconfig eth0 192.168.2.66 up
```

创建系统的以太网接口后，您可以像这样使用 `ifconfig` 进行检查：

```
$ /sbin/ifconfig eth0

eth0       Link encap:Ethernet  HWaddr 00:30:65:AB:F6:D6
           inet addr:192.168.2.66  Bcast:192.168.2.255  Mask:255.255.255.0
           inet6 addr: fe80::30:65ab:fed6:f6d6/10  Scope:Link
           inet6 addr: fe80::230:65ff:feab:fd66/10  Scope:Link
           UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
           RX packets:2233795 errors:0 dropped:0 overruns:0 frame:0
           TX packets:2115741 errors:0 dropped:0 overruns:0 carrier:0
           collisions:0
```

您应该能看到分配的 IP 地址以及接口的 MAC 地址。检查接口的另一种方法是使用 `ping` 命令向另一台计算机回显小数据包，就像这样：

```
$ ping green.home.org
PING green.home.org (192.168.2.37): 56 data bytes
64 bytes from 192.168.2.37: icmp_seq=0 ttl=255 time=0.419 ms
64 bytes from 192.168.2.37: icmp_seq=1 ttl=255 time=0.328 ms
64 bytes from 192.168.2.37: icmp_seq=2 ttl=255 time=0.361 ms
64 bytes from 192.168.2.37: icmp_seq=3 ttl=255 time=0.360 ms
-- green.home.org ping statistics --
4 packets transmitted, 4 packets received, 0% packet loss
round-trip min/avg/max = 0.328/0.367/0.419 ms
```

`ping` 命令将一直运行，直到您按下 Ctrl+c（您也可以使用命令的 `-c` 选项后跟一个数字来设定预先确定的回显次数）。如果您遇到麻烦，首先确保您的网络服务已启用。接下来，确保您的本地环回设备也已启用：

```
$ ifconfig lo

lo       Link encap:Local Loopback
           inet addr:127.0.0.1  Mask:255.0.0.0
           inet6 addr: ::1/128  Scope:Host
           UP LOOPBACK RUNNING  MTU:1924  Metric:1
           RX packets:45171 errors:0 dropped:0 overruns:0 frame:0
           TX packets:45171 errors:0 dropped:0 overruns:0 carrier:0
           collisions:0
```

### 配置远程登录

如果你无法 `ping` 通远程主机，请确保 `DNS` 工作正常（检查 `/etc/resolv.conf` 文件中是否列出了地址），或者主机的 `名称` 已在系统的 `/etc/hosts` 文件中定义：

- 127.0.0.1 localhost localhost.localdomain
- 192.168.2.32 green.home.org green
- 192.168.2.33 stinkpad.home.org stinky
- 192.168.2.34 presario.home.org presario
- 192.168.2.35 thinkpad.home.org thinkpad
- ...

有许多其他工具可用于测试你的网络以及与其它网络的连接。请阅读 `traceroute` 和 `dig` 命令的手册页。

> 还有一个实用的命令，可用于测试两个远程主机（而不仅仅是你的机器）之间的连接性，即 `binger` 命令。与 `ping` 类似，`binger` 会报告数据包在两台计算机之间往返的最佳、平均和最慢时间。

![](img/1ea833f5a3e3c1547e3dd2891f52804a_402_0.png)

设置你的 Linux 系统以接受远程登录非常容易。Linux 用户可以访问几种不同类型的远程登录。你可以允许其他用户通过 `telnet`、`ssh` 或 `ftp` 命令进入你的计算机。你也可以允许人们通过外接或内置调制解调器拨入，登录，然后使用 shell。你还可以设置一个 `拨号点对点协议（dialup Point-to-Point Protocol）` 服务器，以分配动态或静态 IP 地址。

`Telnet` 和 `FTP` 访问通常由系统 `/etc/inetd.conf` 或 `/etc/xinetd.d` 目录中的设置决定。例如，`SuSE` 和 `LinuxPPC 2000` 目前都使用 `inetd`（Internet 超级守护进程）及其 `/etc/inetd.conf` 配置文件。在这个文本文件中，你会看到：

```
...
#
ftp stream tcp nowait root /usr/sbin/tcpd in.proftpd
telnet stream tcp nowait root /usr/sbin/tcpd in.telnetd
#
```

这些设置允许在你的系统中使用 FTP 和 telnet 服务。其他配置文件，如 `services` 或 `ttypesace`，可用于微调来自特定远程主机的用户控制和访问权限。

### 编辑 `/etc/inittab`

要允许拨入访问，请编辑 `/etc/inittab` 文件，然后使用行监控和登录工具，如 `agetty`、`ugetty` 或 `ngetty`，来确定用户的访问权限。例如，如果你使用的是 SuSE Linux，并且可能在 `/dev/ttyS0` 上有一个内置调制解调器，你可以这样使用 `agetty` 命令：

```
2:123:respawn:/sbin/agetty -w -I 'ATE0Q1&D2&C1S0=1,015' 115200 ttyS0 vt100
```

使用此条目替换 runlevel 2 的默认条目：

```
2:123:respawn:/sbin/mingetty tty2
```

`agetty` 命令将监控你的调制解调器，如果用户拨入，它将自动接电话并提供登录提示。用户必须在你的系统上拥有一个账户才能登录。

### 处理 Shell 账户

允许远程 shell 账户可能存在安全隐患，但也可以为某些用户提供更好的在线工具和实用程序访问权限。例如，如果你的服务器拥有互联网访问权限，这将允许远程用户利用你的服务。用户可以使用基于文本的互联网实用程序，如 `pine`、`elm`、`trn`、`slrn` 或 `lynx`，来发送电子邮件、阅读新闻或浏览网络。
