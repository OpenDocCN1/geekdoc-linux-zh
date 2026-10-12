
```
system+  309  0.0  0.3  16884  3940 Ssl  Nov07    0:07 /lib/systemd/systemd-timesyncd

root     359  0.0  0.0     0     0 S    Nov07    0:00 [ttm_swap]

root     514  0.0  1.5  53964 16720 Sl   Nov07    0:00 /usr/bin/VGAuthService

root     515  0.0  0.2   5256  2816 Ss   Nov07    0:00 /usr/sbin/cron -f

message+ 518  0.0  0.3   6368  3896 S    Nov07    0:37 /usr/bin/dbus-daemon --system

rtkit    523  0.0  0.3  24096  3156 SNsl Nov07    0:00 /usr/lib/rtkit/rtkit-daemon

...

student 8868  0.0  0.3   7664  3336 R+   Nov07   14:25 ps axu
```

> 列表 523 - 获取 Linux 上正在运行的进程列表

输出列出了几个以 root 身份运行且值得研究以查找潜在漏洞的进程。请注意，我们的 `ps` 命令也列在输出中。

### 18.1.1.5 枚举网络信息

分析目标主下一步是审查可用的网络接口、路由和开放端口。

这些信息有助于我们确定被入侵的目标是否连接到多个网络，因此可以被用作跳板（pivot）。此外，特定虚拟接口的存在可能表明虚拟化或防病毒软件的存在。

![](img/ec25e59d75726b7041242a56d3376832_511_0.png)

> 攻击者可能会使用被入侵的目标进行跳板（pivot），即在连接的网络之间移动。这将扩大网络可见性，并允许攻击者针对无法从原始攻击机器直接看到的宿主。

我们还可以调查端口绑定，以查看正在运行的服务是否仅在环回地址上可用，而不是在可路由的地址上。调查监听环回接口的特权程序或服务可以扩大我们的攻击面，并增加权限提升攻击的成功率。

我们可以从 Windows 操作系统上的 `ipconfig`[^453] 开始收集信息，使用 `/all` 标志显示所有适配器的完整 TCP/IP 配置。

```
C:\Users\student> ipconfig /all
```

**Windows  ip 配置**

主机名 . . . . . . . . . . . . : client251
主 Dns 后缀 . . . . . . . . . : corp.com
节点类型 . . . . . . . . . . . : Hybrid
启用 IP 路由. . . . . . . . . : No
启用 WINS 代理. . . . . . . . : No
DNS 后缀搜索列表. . . . . . : corp.com

**以太网 适配器 Ethernet0:**

连接专用 DNS 后缀 . :
描述 . . . . . . . . . . . . . : Intel(R) 82574L 千兆网络连接
物理地址. . . . . . . . . . . . : 00-0C-29-C1-ED-B0
启用 DHCP. . . . . . . . . . . : No
启用自动配置 . . . . . . . . : Yes
链路本地 IPv6 地址 . . . . . . : fe80::bc64:ab2f:a10f:edc9%15(Preferred)
IPv4 地址. . . . . . . . . . . : 10.11.0.22(Preferred)
子网掩码 . . . . . . . . . . . : 255.255.255.0
默认网关 . . . . . . . . . . . :
DHCPv6 IAID . . . . . . . . . . : 83889193
DHCPv6 客户 DUID. . . . . . . . : 00-01-00-01-25-55-82-FF-00-0C-29-C1-ED-B0
DNS 服务器 . . . . . . . . . . . : 10.11.0.2
NetBIOS over Tcpip. . . . . . . . : Enabled

**以太网 适配器 Ethernet1:**

连接专用 DNS 后缀 . :
描述 . . . . . . . . . . . . . : Intel(R) 82574L 千兆网络连接 #2
物理地址. . . . . . . . . . . . : 00-0C-29-C1-ED-BA
启用 DHCP. . . . . . . . . . . : No
启用自动配置 . . . . . . . . : Yes
链路本地 IPv6 地址 . . . . . . : fe80::9d3e:158a:241b:b6b7%4(Preferred)
IPv4 地址. . . . . . . . . . . : 192.168.1.111(Preferred)
子网掩码 . . . . . . . . . . . : 255.255.255.0

[^444]: (Microsoft, 2017). https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/hostname
[^445]: (Peter Tobias, 2003). https://linux.die.net/man/1/hostname
[^446]: (Wikipedia, 2019). https://en.wikipedia.org/wiki/Kernel_(operating_system)
[^447]: (Microsoft, 2017). https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/systeminfo
[^448]: (Microsoft, 2017). https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/findstr
[^449]: (David MacKenzie, 2003), https://linux.die.net/man/1/uname
[^450]: (Microsoft, 2017), https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/tasklist
[^451]: (Linux man-pages project, 2018, http://man7.org/linux/man-pages/man1/ps.1.html)
[^452]: (Linus Åkesson, 2018, https://www.linusakesson.net/programming/tty/)
[^453]: (Microsoft, 2017), https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/ipconfig

默认网关 . . . . . . . . . . . . . . . . . : 192.168.1.1
DHCPv6 IAID . . . . . . . . . . . . . . . : 167775273
DHCPv6 客户端 DUID. . . . . . . . . : 00-01-00-01-25-55-82-FF-00-0C-29-C1-ED-B0
DNS 服务器 . . . . . . . . . . . . . . . : fec0:0:0:ffff::1%1
                              fec0:0:0:ffff::2%1
                              fec0:0:0:ffff::3%1
通过 TCP 的 NetBIOS. . . . . . . . : 已启用

![](img/ec25e59d75726b7041242a56d3376832_512_0.png)

这台机器确实拥有多个网络接口。接下来，让我们仔细查看其路由表。

要显示网络路由表，我们将使用 `route` 命令并附加 `print` 参数。

```
C:\Users\Student>route print
=====================================================================

接口列表

 15...00 0c 29 c1 ed b0 ...Intel(R) 82574L Gigabit 网络连接
```
