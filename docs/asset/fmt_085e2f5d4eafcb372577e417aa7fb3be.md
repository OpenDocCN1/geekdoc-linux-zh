
# HP-UX 网络接口配置示例

```
hp-ux$ sudo ifconfig lan0 192.108.21.99 netmask 0xffffffff
hp-ux$ sudo route add default 192.108.21.254 1
```

HP 的 `lanscan` 命令列出系统中的网络接口以及控制它们的设备驱动程序的特性。`lanscan -v` 显示稍多信息。下面示例已被修改以适应页面。MAC 条目值为 `ETHER` 意味着网络设备名称应为 `lan0`，而不是 `snap0`；`ifconfig` 显示这是正确的。

```
$ lanscan
Hardware      Station     Crd  Hdw  Net-Int   NM   MAC      HP-DLPI  DLPI
Path          Address     In#  State NamePPA  ID   Type     Support  Mjr#
8/0/20/0      0x001...    0    UP    lan0 snap0 1    ETHER    Yes      130
```

```
$ ifconfig lan0
lan0: flags=843<UP,BROADCAST,RUNNING,MULTICAST> inet 192.108.21.99
netmask ffffff00 broadcast 192.108.21.255
```

```
$ ifconfig snap0
ifconfig: no such interface
```

`netstat -i` 显示网络接口名称，`netstat -nr` 显示路由表：

```
$ netstat -i
Name  Mtu  Network        Address          Ipks  Opkts
lan0  1500 192.108.21.0   disaster.atrust.com 6047 3648
lo0   4136 127.0.0.0      localhost.atrust.com 231 231
```

```
$ netstat -nr
Routing tables
Dest/Netmask     Gateway          Flags Refs Use Int Pmtu
127.0.0.1        127.0.0.1         UH    0    231 lo0 4136
192.108.21.99    192.108.21.99     UH    8    lan0 4136
192.108.21.0     192.108.21.99     U     2    0   lan0 1500
127.0.0.0        127.0.0.1         U     0    0   lo0 4136
default          192.108.21.254    UG    0    0   lan0 1500
```

`lanadmin` 命令显示每个接口所见网络流量的摘要。它还可以操作和监控接口。它是一个基于菜单的程序，具有有用的帮助列表，可引导你找到所需的信息。以下是显示 `lan0` 接口统计信息的示例：

```
% lanadmin
LOCAL AREA NETWORK ONLINE ADMINISTRATION, Version 1.0
Copyright 1994 Hewlett Packard Company.
All rights are reserved.

Test Selection mode.

lan     = LAN Interface Administration
menu    = Display this menu
quit    = Terminate the Administration
terse   = Do not display command menu
verbose = Display command menu

Enter command: lan

LAN Interface test mode. LAN Interface PPA Number = 0
clear   = Clear statistics registers
display = Display LAN Interface status/statistics
end     = End LAN Interface Admin., go up 1 level
menu    = Display this menu
ppa     = PPA Number of the LAN Interface
```

`quit` = 终止 Admin，返回 shell

`reset` = 重置 LAN 接口，执行自检

`specific` = 进入驱动程序专用菜单

Enter command: `display`

```
LAN INTERFACE STATUS DISPLAY
Tue, Jun 2, 2009 00:41:24

PPA Number                 = 0
Description                = lan0 Intel PCI Pro 10/100Tx Server Adapter
Type (value)               = ethernet-csmacd(6)
MTU Size                   = 1500
Speed                      = 100000000
Station Address            = 0x00306eea9237
Administration Status (value) = up(1)
Operation Status (value)   = up(1)
...
Inbound Unicast Packets    = 45691
Inbound Non-Unicast Packets = 2630
...
Deferred Transmissions     = 0
Late Collisions            = 0
Excessive Collisions       = 0
...
```

## HP-UX DHCP 配置

与其它网络配置参数一样，你可以通过在 `/etc/rc.config.d/netconf` 文件中设置变量来在启动时启用 DHCP。在这种情况下，变量名以 `DHCP_ENABLE` 开头。索引 `[0]` 指第一个接口，`[1]` 指第二个接口，以此类推。例如，

```
DHCP_ENABLE[0]=1
```

将第一个网络接口设置为 DHCP 模式。它将从本地网络上的 DHCP 服务器获取其 IP 地址、子网掩码和其他网络参数。将变量设置为 0 将禁用 DHCP；你必须在 `netconf` 文件中分配静态地址。如果没有 `DHCP_ENABLE` 子句，变量默认为 1。

`/sbin/auto_parms` 脚本负责实际联系 DHCP 服务器的工作。程序 `dhcpdb2conf` 将由 `auto_parms` 获取的 DHCP 参数写入 `netconf` 文件，启动时的配置信息即由此获取。

## HP-UX 动态重配置和调优

与 Solaris 类似，你可以使用 `ndd` 来调优许多不同的网络参数。交互使用时，`ndd` 会即时调整值。要永久更改值，请将它们输入 `/etc/rc.config.d/nddconf`，该文件在启动时读取。

描述变量的作用并显示其最小值、最大值和默认值。例如：

```
$text
$ ndd -h | grep source
ip_forward_src_routed - Controls forwarding of source routed packets
```

```
$text
$ ndd -h ip_forward_src_routed
ip_forward_src_routed:
  Set to 1 to forward source-routed packets; set to 0 to
  disable forwarding. If disabled, an ICMP Destination
  Unreachable message is sent to the sender of source-
  routed packets needing to be forwarded. [0,1] Default: 1
```

`ndd` 的输出声称此版本的 HP-UX 默认允许转发源路由数据包。这可能是内核的偏好，但实际上我们实验室系统上的默认 `/etc/rc.config.d/nddconf` 文件禁用了此行为：

```
$text
TRANSPORT_NAME[2]=ip
NDD_NAME[2]=ip_forward_src_routed
NDD_VALUE[2]=0
```
