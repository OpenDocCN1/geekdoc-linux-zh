
Solaris 有两个版本的 `ifconfig` 命令，一个在 `/bin` 中，另一个在 `/usr/bin` 中。`/bin` 版本使用固定的“主机名到 IP”的查找顺序：它首先查询 `/etc/hosts`，然后是 DNS。`/usr/bin` 版本使用 `/etc/hosts` 来确定查找顺序；这是更符合常规的行为。在启动时使用 `ifconfig` 是预期 `etc/hosts` 文件中没有条目，以便无需求助于 DNS 查找即可获取接口。

对于两个版本的 `ifconfig`，`ifconfig -a` 以 root 用户身份运行的输出与以普通用户身份运行时不同。以 root 身份运行时，除了显示 IP 地址和参数外，还会显示链路层以太网地址。

Solaris 允许你通过 `ifconfig` 命令和 `ether` 地址族更改接口的链路层（MAC）地址。我们认为这是一个 bug，而不是一个特性。

# 13.13 HP-UX 网络配置

HP-UX 使用金星标志进行网络配置。所有的配置参数都设置在 `/etc/rc.conf.d/netconf` 文件中。该文件（以及 `rc.conf.d` 目录下的所有其他文件）中的值在启动时环境中可用，并在机器启动时由 `/sbin/rc` 脚本使用。`netconf` 文件中充斥着注释，告诉哪些变量必须设置以及它们的含义是什么。

## HP-UX 基础网络配置

要为机器分配主机名并配置其第一个网络接口，需要编辑 `netconf` 文件并为以下变量赋值：

```
HOSTNAME
INTERFACE_NAME[0]
IP_ADDRESS[0]
SUBNET_MASK[0]
```

## UNIX 系统管理手册

例如：

```
HOSTNAME=disaster
INTERFACE_NAME[0]=lan0
IP_ADDRESS[0]=192.108.215.99
SUBNET_MASK[0]=255.255.255.0
```

第二个网络接口将具有下标 1，其存在性将通过变量 `NET_CARDS` 设置为 2 来指示。

`netconf` 文件还包含用于配置静态路由和启动路由守护进程的变量。要建立默认路由，请参阅以下变量：

```
ROUTE_DESTINATION[0]=default
ROUTE_MASK[0]=*
ROUTE_GATEWAY[0]=192.108.21.254
ROUTE_COUNT[0]=1
```

HP-UX 系统是门控的（gated）但不是路由的（routed）；使用将变量 `GATED` 设置为 1，并将 `GATED_ARGS` 设置为你想要门控启动的参数。有关门控配置的更多细节，请参见第 14 章“路由与配置”。HP-UX 关于路由的页面（`man routing`）包含了很多很好的背景信息。

`netconf` 文件中的许多字段可以包含主机名或 IP 地址。如果使用主机名，则必须在 `/etc/hosts` 中定义。在启动时，HP-UX 只查找 `/etc/hosts`，不使用任何其他查找机制。`/etc/hosts` 中的项应先列出它们的完全限定域名，然后是它们的短名和任何别名。

HP 使用 `lanscan` 命令显示机器上网络接口的信息。如果 `ifconfig` 不起作用，但 `ifconfig interface` 是可以的。网络接口以 "lan" 或 "snap" 开始：`lan` 用于以太网链路层封装，`snap` 用于 IEEE 802.3 封装。第一个接口是 `lan0`，第二个是 `lan1`，以此此类推。

HP-UX 拥有与 Solaris 类似的“接水（plumbing）”机制，但当接口被 `ifconfig` 分配 IP 地址时，它们会自动完成“接水”配置。

`SAM` 是 HP 的系统管理工具，据称它让 UNIX 管理变得轻而易举。它是一个基于菜单的系统，可以配置网络接口，还可以执行许多其他系统管理命令。

## HP-UX 配置示例

要手动启动 HP-UX 网络接口并添加默认路由，你可以使用如下命令：

```
# ifconfig lan0 192.108.21.99 netmask 0xffffff00
# route add 192.108.21.254 12*
```

HP 的 `lanscan` 命令列出系统中的网络接口以及控制它们的设备驱动程序的特性。`lanscan -v` 显示稍多的信息。下面的示例已合并以适应页面宽度。值为 ETHER 的 MAC 条目意味着网络设备名称应为 `lan0`, `snap0`；`ifconfig` 显示这确实如此。

% lanscan

| Hardware Station Crd Hdw Net-Int State Name Type |
| :--- | :--- | :--- | :--- | :--- |
| 0 | HP | 0x108309e6 | UP | YES | ethernet |
| 10/100 | | | | |

% ifconfig lan0

flags=BROADCAST,RUNNING,inet 192.108.21.99  netmask 255.255.255.0

% ifconfig snap0

ifconfig: no such interface

% netstat -i

| Name Mtu Opts |
| :--- | :--- | :--- |
| lan0 | 1500 | 6047 |
| lo0 | 1500 | 0 |

% netstat -nr

| Dest/Mask Gateway Refs Pmt |
| :--- | :--- | :--- | :--- |
| default | * | 192.108.21.254 | UG | 1 |

% lansadmin

LOCAL AREA NETWORK ADMINISTRATION, Version 1.0

Copyright 1994 Hewlett-Packard Company.

All rights reserved.

`lanadmin` 命令显示接口的流量摘要。它还可以操作接口。除了上面显示的 `lan` 和 `display` 命令外，我们还尝试了 `clear` 和 `reset`，它们会清除计数器并重置接口。但由于我们没有以 root 身份运行 `lanadmin`，操作被拒绝了。

Test Selection.

- lan = LAN Interface

- menu = Display this menu

- quit = Terminate the Administration

- terse = Do not display

- verbose = Display command

- ppa = PPA Number of the LAN Interface

- quit = Terminate the Admin, return to shell

- reset = Reset LAN Interface, execute selftest

- specific = Go to Driver menu

Enter command: lan

LAN Interface test mode. LAN Interface PPA = 0

- clear = Clear statistics

- display = Display LAN status/statistics

- end = End Interface Admin., go up1

- menu = Display this menu

Enter command: display

LAN INTERFACE STATUS DISPLAY

Thu, Mar 2,2000 00:41:24

| PPA Number | Description | MTU Size | Speed | Station Address | Administration Status | Operation Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | lan0 HP 10/100 TX Half-Duplex | 1500 | 10 | 0x108309e6 | up(1) | up(1) |

- Inbound Unicast Packets = 4204

- Inbound Nonicast Packets = 5594

- Inbound Unknown Protocols = 501

- Outbound Octets = 454903

- Outbound Unicast Packets = 3603

- Deferred Transmissions = 2

- Late Collisions = 0

- Excessive Collisions = 2

在 HP-UX 11 上，`count` 字段不是必须的；如果没有指定，默认值为 0。

## HP-UX 配置

与其他网络配置参数一样，你通过设置 `/etc/rc.config/netconf` 文件中的变量在启动时开启 DHCP 使用。在这种情况下，

变量名以 `DHCP_ENABLE` 开头；索引 `[0]` 指第一个接口，`[1]` 指第二个接口，依此类推。例如：
