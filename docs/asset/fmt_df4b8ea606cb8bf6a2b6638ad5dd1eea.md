
| LAN A 计算机 | LAN B 计算机 | LAN C 计算机 | LAN D 计算机 |
|---|---|---|---|
| 电脑 A1 | 10.10.200.1 | 电脑 B1 | 10.10.101.1 | 电脑 C1 | 10.10.1.1 | 电脑 D1 | 10.10.5.1 |
| 电脑 A2 | 10.10.200.2 | 电脑 B2 | 10.10.101.2 | 电脑 C2 | 10.10.1.2 | 电脑 D2 | 10.10.5.2 |
| 子网掩码 | 255.255.255.0 | 子网掩码 | 255.255.255.0 | 子网掩码 | 255.255.255.0 | 子网掩码 | 255.255.255.0 |

图 9-3 三台路由器的校园网络。

可以使用一个简化的网络来演示在多路由器网络中开发静态路由所需的条件。对于此示例，校园网络中的两个路由器 `RouterA` 和 `RouterB` 如图 9-4 所示连接到 LAN A 和 B。这个简化的网络将用于描述数据包如何从 LAN A > `RouterA` > `RouterB` > LAN B 传输，以及定义静态路由所需的条件。

![](img/ec00be08b0c45b337e7cb610696f1b45_388_0.png)

数据包从 LAN A 传输到 LAN B 时会通过三个子网（用 *NET* 表示）。每个网络的 IP 子网如下：

- 10.10.200.0 LAN A
- 10.10.200.0 `RouterA` 到 `RouterB` 的连接
- 10.10.10.0 LAN B

在网络网络中，只有两个路由器，`RouterA` 直接连接到 `RouterB`。这意味着路由器之间的唯一路由是经过 10.10.200.0 NET，即该连接。静态路由是在路由器的配置终端 `(config)#` 中使用 `ip route` 命令输入的。*ip route* 的命令结构为：

```
Router(config)#ip route <destination> <subnet mask> <next hop>
```

其中 `destination` 是网络的 IP 地址 (NET)，`subnet mask` 是为子网定义的，`next hop` 是链路中路由器的 IP 地址。将数据路由到 10.10.10.0 子网的命令如下：

```
Router(config)#ip route 10.10.10.0 255.255.255.0 10.10.200.252
```

在 `RouterA` 中输入了以下配置信息：

| 目标 IP 地址 | 子网掩码 | 下一跳 IP 地址 |
| --- | --- | --- |
| 10.10.10.0 | 255.255.255.0 | 10.10.200.2 |

下一跳 IP 地址是 `RouterB` 上 Ethernet2 端口的地址。现在路由器知道如何将 10.10.20.0 NET (LAN A) 主机的数据包传递到目的地。注意：每个静态路由可以使用不同的子网掩码。这被称为*变长子网掩码*。例如，一个静态路由的子网掩码可以是 255.255.255.0，另一个子网掩码可以是 255.255.255.252。用于为变长子网掩码手动设置下一跳 IP 地址并向路由表中添加条目的 `ip route` 命令，可以通过路由器的 `(config)#` 下输入 `show ip route` 命令来验证。示例所示：

```
RouterA# ip route
Codes: C connected, S static, I EGRP, R RIP, M BGP
D external, OSPF interface area
NI OSPF NSSA external type 1, N2 OSPF NSSA external type 2
EI OSPF external type 1, E2 OSPF external type 2, E BGP
IS-IS, L1 level-1, L2 level-2, * candidate default
U per-user static route, engineered route
Gateway of last resort is not set
10.0.0.0/24 is subnetted, 2 subnets
S 10.10.20.0 [1/0] via 10.10.20.1
C 10.10.20.0 is directly connected, FastEthernet/2
```

![](img/ec00be08b0c45b337e7cb610696f1b45_389_0.png)

## sh ip route 命令首先列出代码表，然后是路由列表。

从 10.10.10.0 NET (LAN B) 到 10.10.20.0 NET (LAN A) 的流量是怎样的？同样，数据包从 LAN B 传输到 LAN A 时会通过三个网络（用 NET 表示）。对于此示例，校园网络中的两个路由器 `RouterA` 和 `RouterB` 如图 9-4 所示连接到 LAN A 和 B。这个简化的网络被用于描述数据包如何从 LAN A > `RouterA` > `RouterB` > LAN B 传输，以及定义静态路由所需的条件。

在这个网络中，只有两个路由器，`RouterA` 直接连接到 `RouterB`。这意味着路由器之间的唯一路由是经过 10.10.200.0 NET，即该连接。静态路由是在路由器的配置终端 `(config)#` 中输入的。*ip route* 的命令结构为：

```
Router(config)#ip route <destination> <subnet mask> <next hop>
```

其中 `destination` 是网络的 IP 地址 (NET)，`subnet mask` 是为子网定义的，`next hop` 是链路中路由器的 IP 地址。将数据路由到 10.10.10.0 子网的命令如下：

```
Router(config)#ip route 10.10.10.0 255.255.255.0 10.10.200.252
```

在 `RouterA` 中输入了以下配置信息：

| 目标 IP 地址 | 子网掩码 | 下一跳 IP 地址 |
| --- | --- | --- |
| 10.10.10.0 | 255.255.255.0 | 10.10.2 |

下一跳 IP 地址是 `RouterB` 上 Ethernet2 端口的地址。现在路由器知道如何将 10.10.20.0 NET (LAN A) 主机的数据包传递到目的地。注意：每个静态路由可以使用不同的子网掩码。这被称为*变长子网掩码*。例如，一个静态路由的子网掩码可以是 255.255.255.0，另一个子网掩码可以是 255.255.255.252。用于为变长子网掩码手动设置下一跳 IP 地址并向路由表中添加条目的 `ip route` 命令，可以通过路由器的 `(config)#` 下输入 `show ip route` 命令来验证。示例所示：

```
RouterA# ip route
Codes: C connected, S static, I EGRP, R RIP, M BGP
D external, OSPF interface area
NI OSPF NSSA external type 1, N2 OSPF NSSA external type 2
EI OSPF external type 1, E2 OSPF external type 2, E BGP
IS-IS, L1 level-1, L2 level-2, * candidate default
U per-user static route, engineered route
Gateway of last resort is not set
10.0.0.0/24 is subnetted, 2 subnets
S 10.10.20.0 [1/0] via 10.10.20.1
C 10.10.20.0 is directly connected, FastEthernet/2
```

路由更改发生在持续动态路由协议中，这些协议在路由器之间通信信息，以确定用于数据包的最优路由。动态路由协议的概念在 9-3 中介绍。

## 最后备网关 (Gateway of Last Resort)

静态路由最重要的应用之一是在路由器上配置最后备网关。最后备网关是网络中路由器的 IP 地址，当具有未知路由的数据包时，应转发到该路由器。其目的是为路由表中未配置目的路由的数据包配置路由。在此情况下，可以配置一条默认路由，指示路由器将具有未知路由的数据包转发。执行此操作的命令为：

最后备网关

网络中具有未知路由的数据包应被往的路由器 IP 地址

```
ip route 0.0.0.0 0.0.0.0 <next hop address>
```

如果没有配置静态路由，当输入 `show ip route` 命令时，路由器将显示以下消息：

Gateway of last resort is not set（未设置最后备网关）

这意味着路由器不知道如何路由目的 IP 地址与路由表中存储的路由不同的数据包。这将导致发往目的 IP 地址的数据包被丢弃。如果没有最后备网关，路由器将丢弃任何目的网络不在其路由表中的数据包。

## 配置静态路由

以下描述介绍了如何在 Cisco 路由器上配置静态路由。所使用的拓扑是 9-3 所示的三路由器园区网络。本演示用于为 `RouterA` 配置静态路由。

第一步是通过控制台或虚拟终端连接到路由器。接下来，进入所示的特权 EXEC 模式：

```
Router# is now available Press RETURN to get started!
RouterA#
```

接下来，使用 `configure terminal (conf)#` 命令在路由器上进入配置终端模式 [`RouterA(config)#`]。在配置静态路由之前，确保接口已配置好。`FastEthernet/1` 接口配置了分配的 IP 地址 10.10.200.1 和子网掩码 255.255.255.0，`FastEthernet/2` 接口分配了地址 10.10.100.1 和子网掩码以启用 FastEthernet 端口。

```
Router#Enter configuration commands, one per line. End with CNTL.
RouterA(config)#interface FastEthernet/1
RouterA(config-if)#ip address 10.10.200.1 255.255.255.0
RouterA(config-if)#no shut
00:19:07:LINK-3-UPDOWN: Interface FastEthernet/1, changed state to up
Routerinterface FastEthernet/2
RouterA(config-if)#ip address 10.10.100.1 255.255.255.0
RouterA(config-if)#no shut
00:21:05:LINK-3-UPDOWN: Interface FastEthernet/2, changed state to up
```

注意在执行 `no shut` 命令后，`FastEthernet0/1` 和 `FastEthernet0/2` 接口的状态发生了变化。使用所示的 `show ip interface (sh ip int)` 命令验证接口状态是良好的。

```
Router# sh ip int
00:22:18: %SYS-5-CONFIG: Configured from console
Interface      IP-Address Method Protocol
FastEthernet0/1 10.100.2 YES up down
FastEthernet0/2 10.100.1 YES up down
```

两个 `FastEthernet` 端口的状态均显示为 `up`（开启）；然而，链路层协议（line protocol）告诉我们路由器之间没有建立物理连接。这个“protocol down”（协议关闭）的问题通过重启路由器之间的物理连接来解决。

在接口配置完成后，静态路由使用 `ip route` 命令。你不需要一次性输入所有路由，但为了简化示例，已列出通往 10.10.10.0/24 网络的所有必须正确录入路由。

```
Router(config)#ip route 10.10.10.0 255.255.255.0 10.10.200.2
Router(config)#ip route 10.10.10.0 255.255.255.0 10.10.100.2
```

有两个地方可以验证静态路由是否配置正确。首先，通过 `show ip` 或 `show ip interface (sh ip route static)` 验证路由是否在使用路由表。添加 `show ip route` 单词会将显示的路由限制为静态路由。重要笔记是，只有当链路层协议为正常时，才会使用 `show ip route` 命令显示路由。

> show ip route static

(sh ip route static)

将显示的路由限制为静态

```
Router# ip route
Codes: C connected, S static, I IGRP, R RIP, M mobile, B BGP
D EIGRP, E OSPF, IA OSPF interface area.
NT NSFA external type 1, O NSFA external type 2
EI OSPF external type 1, E OSPF external type 2, E EGP
IS IS-IS, L1 IS-IS level-1, L2 IS-IS level-2, candidate default
u U static, traffic engineered router
Gateway of last resort is not set
10.0.0.0/8 is subnetted, S 10.10.10.0 [1] via 10.10.200.2
S 10.10.100.0 [1] via 10.10.100.2
C 200.0.0 is directly connected, FastEthernet0/1
C 100.0.0 is directly connected, FastEthernet0/2
```

> show running-config

(sh run)

显示路由器的运行配置

另一个检查路由配置的地方是命令 `show running-config (sh run)`。该命令显示路由器当前的配置，但不显示保存在非易失性存储器（NVRAM）中的配置。`show startup-config (sh start)` 显示保存在 NVRAM 中的配置。

```
Router# sh run
Using 519 out 3276 bytes

version 12.0
service timestamps
service password-encryption
hostname router

ip-zero

interface FastEthernet/1

ip address 10.10.200.1 255.255.255.0

no ip directed-broadcast

keepalive

interface FastEthernet/2

ip address 10.10.100.1 255.255.255.0

no ip directed-broadcast

keepalive

ip route 10.10.10.0 255.255.255.0 10.10.200.2

ip route 10.10.10.0 255.255.255.0 10.10.100.2

line con0

transport input none

line vty 0 4

end
```

在操作过程中将配置更改保存到路由器是非常重要的。使用 `running-configuration (copy run start)` 或 `write memory (wr)` 命令将更改保存到路由器：

```
Router#copy run start

Router#wr
```
