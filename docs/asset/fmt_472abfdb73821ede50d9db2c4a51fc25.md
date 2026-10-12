
`[root]# cat /etc/lilo.conf`

```
boot=/dev/hda

map=/boot/map

install=/boot/boot.bin

prompt

timeout=50

# Normal Linux boot

image=/boot/vmlinuz-2.2.9

label=linux

root=/dev/hdb1

read-only

# Emergency Linux boot

image=/boot/vmlinuz-2.2.5

label=safe

root=/dev/hdb1

read-only

# DOS boot

other=/dev/hda1

label=dos

table=/dev/hda
```

```bash
[root]# #sbin/lilo

Added linux *

Added safe

Added dos
```

新内核现在已准备好运行。重启系统让新内核投入运行。如果在启动过程中出现任何问题，请退回到启动安全内核。当你对新内核熟悉后（例如一个月后），可以删除旧的源码树、模块库和内核，如果需要磁盘空间。

## 网络服务器故障排除

尽管你对修复已知漏洞很慷慨，对安装不需要的软件很保守，问题将会发生。许多问题在你发现异常之前就会被用户发现。追踪这些报告的问题既是艺术也是科学。

故障排除的艺术在于你对服务器和网络状态的直觉，以及对用户问题报告准确性的洞察。我说这些并不是贬低报告问题的用户的智力，因为作为报告问题的人，我也犯过不准确的错误。在压力下，我曾完全误解了清晰的指令并报告了问题，而真正的问题只是我没有时间仔细阅读指令。因此，你不能从问题报告中假设太多，你需要有系统地应用自己的知识来解决问题。这里是一些建议：

为该区域选择合适的测试工具。以下是一些帮助你做出决策的指南：

- 如果问题发生在出站连接上，它可能与你服务器上运行的任何守护进程（`daemon`）无关。使用 `ifconfig` 检查网络接口的配置，使用 `ping` 测试基本连通性，并使用 `traceroute` 测试到远程服务器的路由。与远程服务器的管理员联系，确保他们正在运行用户请求的服务，并且该服务配置正确。

- 如果问题发生在入站连接上，确保你的系统已通过 `inetd.conf` 或启动脚本运行了所需的守护进程。从本地主机连接到守护进程以确保它正在运行。如果守护进程正在运行，请确保其配置正确。检查 `Wrapper` 和 `ipfw` 以确保允许远程系统访问该服务。

- 如果问题只发生在一个客户端上，请集中精力测试该客户端。如果问题发生在多个客户端上，请将精力集中在网络和服务器上。

## 诊断工具

排查故障可能需要同时使用硬件工具和软件工具。你可能并不认为自己是硬件专家，但手头有一个小型的硬件工具包是有用的。在大多数销售局域网设备的地方，都可以买到简单的线测试器和一个包含你可能需要的所有工具的 `LAN` 维护工具箱。在这些工具的基础上加上双启动系统，你就拥有了所需的所有故障排除硬件。

笔记本电脑是我最喜欢的测试设备。我将笔记本电脑配置为双启动 `Microsoft Windows` 和 `Linux`。当用户报告一个我在桌前无法解决的问题时，我会带着笔记本电脑到用户的办公室，直接插上她的以太线，并从那里运行测试。这可以快速告诉我问题是存在于用户的计算机还是网络中。

> 提示：我使用双启动系统，这样我既可以使用 `Linux` 系统上提供的优秀工具，又可以向用户演示 `Microsoft Windows` 的连接情况。我发现，很多 `Windows` 用户除非我能用 `Windows` 显示其正在运行，否则他们就不相信网络正在正常。

`Linux` 包含了大量简单的软件工具，可以通过测试帮助隔离问题。我相信这些软件工具足以解决任何企业级网络问题。除了之前提到的 `sendmail -bt` 和 `ismod` 等工具外，我使用并推荐的工具包括：

`ifconfig` 用此工具显示网络接口的配置、特性和统计数据。

`arp` 和 `arpwatch` 使用这些工具来监控 `IP` 地址到以太网地址的映射。

`ping` 用此工具测试基本的网络连通性。
`traceroute` 用此跟踪端到端的网络路径。
`netstat` 用此工具显示端口状态和活动连接。
`nslookup`、`dig` 和 `host` 使用这些工具测试域名解析服务（`DNS`）。`nslookup` 是随 `BIND` 软件提供的强大交互式工具。`dig` 和 `host` 是可以在 `shell` 脚本内部使用的类似工具。

`tcpdump` 用此分析网络包。

在接下来的章节中，将检查所有由 `Linux` 提供的软件工具。

## 检查网络接口

配置错误（包括导致安全漏洞的错误）经常是成熟系统中问题的所在。你无法通过正确配置系统来消除这些问题。当你接入网络时，网络终端管理员的配置错误可能会影响用户。此外，你可能会被邀请帮助用户纠正他们在设置桌面系统时犯的配置错误。

> 警告：我特别提到了“成熟系统”，因为对新事物的渴望（即使它尚未完全成熟）可能会导致更大的问题。除非绝对必要，否则应避免在生产服务器上使用 `Beta` 版软件。

检查网络服务器的配置可能意味着读取配置文件，也可以积极运行测试。`Red Hat` 和 `Calder` 系统将基础网络接口配置存储在 `/etc/sysconfig` 文件中。检查 `Red Hat` 系统上以太网接口 `eth0` 的配置，你可以列出 `/etc/sysconfig/network` 文件和 `/etc/sysconfig/network-scripts/ifcfg-eth0` 文件，如下：

```
$ /etc/sysconfig/network

NETWORKING=yes

FORWARD_IPV4=false

HOSTNAME=parrot.foobirds.org

DOMAINNAME=foobirds.org
```

GATEWAY=172.16.0.1
DEV=eth0
cat /etc/sysconfig/network-scripts/ifcfg-eth0
DEVICE=eth0
IPADDR=172.16.0.2
NETMASK=255.255.255.0
NETWORK=172.16.0.0
ONBOOT=yes

