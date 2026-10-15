

在旧版本的 Solaris 中，网络启动脚本是位于 /etc/init.d 的文件（主要是 rootusr、inetinit、sysid.net 和 inetsvc）。Solaris 10 从根本上重构了启动文件和系统服务的管理方式。脚本已被重构，现在位于 /lib/svc/method。请参阅第 97 页，了解 Solaris 服务管理设施的概述。

如果 /etc/defaultrouter 存在，则假定其中包含默认网关的标识（同样可以是主机名或数字地址），并且不再进行进一步的路由配置。像往常一样，数字地址更可取；使用名称需要 /etc/hosts 条目或本地网络上的 DNS 服务器。

Solaris 以前在未指定默认网关时会运行 routed（它实际上称为 in.routed），但在 Solaris 10 及更高版本中，您必须使用 svcadm enable routing/route 显式启用 routed。使用命令 svcs route 来确定服务的当前状态。

注意：routed 如果机器有多个网络接口或文件 /etc/gateways 存在，则会自动进入服务器（多话）模式。这通常不是您想要的。您可以通过打开“静默模式”标志来防止 routed 喋喋不休：

```
solaris# svccfg -s routing/route:default setprop routing/quiet_mode = true
```

## Solaris 配置示例

以下是启动 Solaris 接口并向默认网关添加路由所需的命令示例：

```
solaris$ sudo ifconfig e1000g0 plumb
solaris$ sudo ifconfig e1000g0 192.108.21.48 netmask 255.255.255.0 up
solaris$ sudo route add default 192.108.21.254
```

以下示例展示了如何查看网络接口和路由表的状态。以 sudo 为前缀的命令必须以 root 身份运行。最后一个示例展示了 Solaris route 命令的一个特性，在我们的其他架构上并不存在：get 参数显示到特定目的地的下一跳。我们做了一些取舍以使示例适合页面。

```
solaris$ netstat -nr
Routing Table: IPv4
Destination        Gateway           Flags Ref Use Interface
----------         -------           ----- --- --- ---------
default            192.108.21.254    UG    1   9959
192.108.21.0       192.108.21.48     U     1   4985 e1000g0
127.0.0.1           127.0.0.1         UH    1   107  lo0
```

```
solaris$ sudo route get google.com
route to: gw-in-f100.google.com
destination: default
mask: default
gateway: 192.108.21.254
interface: e1000g0
flags: <UP,GATEWAY,DONE,STATIC>
recvpipe sendpipe ssthresh rtt,ms rttvar,ms hopcount mtu expire
0       0       0       0       0       0       1500    0
```

## Solaris DHCP 配置

Solaris 包含一个 DHCP 客户端，并且赢得了最简单、最合理的 DHCP 客户端配置奖：

```
solaris$ sudo ifconfig interface dhcp
```

它就是这么好用！ifconfig 调用 dhcpagent 程序从 DHCP 获取接口的参数并用它们配置接口。您可以在 ifconfig 命令行上包含多个选项，以指定接口为主接口、设置超时、增加租约时间或显示接口状态。要手动取消 DHCP 配置，只需运行

```
solaris$ sudo ifconfig interface drop
```

这都很不错，但您可能希望在启动时自动咨询 DHCP。您可以通过完全不为接口提供配置文件（从而依赖自动配置，类似于 Linux 的 Network Manager）或通过为相应的 /etc/hostname.interface 文件创建 /etc/dhcp.interface 文件来设置此项。如果您愿意，dhcp.interface 文件可以包含要传递给 ifconfig 命令的附加命令行参数。

hostname.interface 文件仍然必须存在才能使接口被连接；但是可以将其留空。如果 hostname.interface 文件不为空，启动脚本将首先使用其内容静态配置接口，然后稍后使用 DHCP 重新配置接口。

