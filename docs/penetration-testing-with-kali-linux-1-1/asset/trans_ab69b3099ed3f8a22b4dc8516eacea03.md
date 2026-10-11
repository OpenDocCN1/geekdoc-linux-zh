

![](img/ec25e59d75726b7041242a56d3376832_508_0.png)

我们可以使用名为 **hostname**[^444][^445] 的命令来发现主机名，该命令在 Windows 和 Linux 上均已安装。

让我们在 Windows 上运行它：

```
C:\Users\student>hostname
client251
```

*列表 518 – 在 Windows 上获取主机名信息*

然后在 Linux 上运行：

```
student@debian:~$ hostname
debian
```

*列表 519 – 在 Linux 上获取主机名信息*

Windows 机器相当通用的名称暗示了网络中可能存在一种命名约定，这有助于我们查找其他工作站，而 Linux 客户端的主机名则提供了关于所用操作系统（Debian）的信息。

识别机器的角色可以帮助我们集中信息收集工作。

### 18.1.1.3 枚举操作系统版本和架构

在权限提升过程的某个阶段，我们可能需要依赖专门针对目标操作系统核心漏洞的 *内核*[^446] 利用程序。这类利用程序是为非常具体的目标类型构建的，由特定的操作系统和版本组合作为标识。由于使用不匹配的内核利用程序攻击目标可能导致系统不稳定（导致访问权限丢失并很可能引起系统管理员警觉），因此我们必须收集关于目标的精确信息。

在 Windows 操作系统上，我们可以使用 **systeminfo**[^447] 实用工具来收集具体的操作系统和架构信息。

我们还可以使用 **findstr**[^448] 以及一些有用的标志来过滤输出。具体而言，我们可以使用 **/B** 匹配行首的模式，并使用 **/C:** 指定特定的搜索字符串。

在下面的示例中，我们将使用这些标志来提取操作系统名称（Name）及其版本（Version）和架构（System）。

```
C:\Users\student>systeminfo  |  findstr /B /C:"OS Name" /C:"OS Version" /C:"System Type"
    Microsoft Windows 10 Pro
    10.0.16299 N/A Build 16299
    X86-based PC
```

*列表 520 – 获取运行中操作系统的版本和架构*

![](img/ec25e59d75726b7041242a56d3376832_509_0.png)

输出表明，目标系统运行的是 x86 架构上的 Windows 10 Pro 版本 10.0.16299。

在 Linux 上，/etc/issue 和 /etc/*-release 文件包含类似的信息。我们也可以执行 `uname -a`[^449] 命令：

```
student@debian:~$ cat /etc/issue
Debian GNU/Linux \n \n
student@debian:~$ cat /etc/*-release
PRETTY_NAME="Debian GNU/Linux 9 (stretch)"
NAME="Debian GNU/Linux"
VERSION_ID="9"
VERSION="9 (stretch)"
ID=debian
...
student@debian:~$ uname -a
Linux debian 4.9.0-6-686 #1 SMP Debian 4.9.82-1+deb9u3 (2018-03-02) i686 GNU/Linux
```

> 列表 521 - 获取运行中操作系统的版本和架构

位于 /etc 目录中的文件包含操作系统版本（Debian 9），并且 `uname -a` 输出内核版本（4.9.0-6）和架构（i686 / x86）。

### 18.1.1.4 枚举正在运行的进程和服务

接下来，让我们看看可能允许我们提升权限的正在运行的进程和服务。为了实现这一点，进程必须以特权账户上下文运行，并且要么具有不安全的权限，要么允许我们以非预期的方式与其交互。

我们可以使用 `tasklist`[^450] 命令列出 Windows 上正在运行的进程。/SVC 标志将返回映射到特定 Windows 服务的进程。

```
C:\Users\student>tasklist /SVC
```

| 映像名称 | PID | 服务 |
|---|---|---|
| lassa.exe | 564 | KeyIso, Netlogon, SamSs, VaultSvc |
| svchost.exe | 676 | BrokerInfrastructure, DcomLaunch, LSM, PlugPlay, Power, SystemEventsBroker |
| fontdrvhost.exe | 684 | N/A |
| fontdrvhost.exe | 692 | N/A |
| svchost.exe | 776 | RpcEptMapper, RpcSs |
| dwm.exe | 856 | N/A |
| svchost.exe | 944 | Appinfo, BITS, DsmSvc, gpsvc, IKEEXT, iphlpsvc, LanmanServer, lmsvc, ProfSvc, Schedule, SENS, SessionEnv, ShellHwDetection, Themes, TokenBroker, UserManager, winmgmt, WpnService |
| svchost.exe | 952 | TermService |
| svchost.exe | 960 | BFE, CoreMessagingRegistrar, DPS, MpsSvc |
| svchost.exe | 988 | Dhcp, EventLog, Imahosts, TimeBrokerSvc, WindowsAutoProxySvc, wscsvc |
| ... | | |
| mysqld.exe | 1816 | mysql |
| ... | | |

> 列表 522 - 获取操作系统上正在运行的进程列表及匹配的服务

输出显示该机器上正在运行 **MySQL** 服务，在特定条件下这可能引起我们的兴趣。

请记住，此输出并未列出由特权用户运行的进程。在基于 Windows 的系统上，我们需要较高的权限才能收集此信息，这使得过程更加困难。

在 Linux 上，我们可以使用 **ps**[^451] 命令列出系统进程（包括由特权用户运行的进程）。我们将使用 **a** 和 **x** 标志列出所有具有或不具有 tty[^452] 的进程，并使用 **u** 标志以用户可读的格式列出进程。

```bash
student@debian:~$ ps axu
USER      PID %CPU %MEM    VSZ   RSS STAT         START TIME COMMAND
root       1  0.0  0.6  28032  6256 Ss   Nov07    0:03 /sbin/init
root       2  0.0  0.0     0     0 S    Nov07    0:00 [kthreadd]
root     254  0.0  0.9  54536  9924 Ss   Nov07    1:45 /usr/bin/vmtoolsd
root     255  0.0  0.0     0     0 S    Nov07    0:00 [kworker/0:1]
root     259  0.0  0.4  25956  5108 S    Nov07    0:01 /lib/systemd/systemd-journald
root     294  0.0  0.4  17096  4996 Ss   Nov07    0:00 /lib/systemd/systemd-udeved
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

输出列出了几个以 root 身份运行且值得研究以查找潜在漏洞的进程。请注意，我们的 **ps** 命令也列在输出中。

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
默认网关 . . . . . . . . . . :
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

