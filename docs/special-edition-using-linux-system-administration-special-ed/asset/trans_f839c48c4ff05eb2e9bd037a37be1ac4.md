
OSPF 是一种动态且自适应的协议。它能适应网络中出现的问题，并提供极短的收敛时间来稳定路由表。它旨在防止网状网络中或使用多个网桥连接不同局域网时出现流量环路。

OSPF 是 RIP 的替代方案。它克服了 RIP 的所有局限性。RIP 是距离矢量协议，而 OSPF 是链路状态协议。在链路状态协议中，每台路由器都会主动测试自己到每个邻居的链路状态，并将该链路状态信息发送给相邻路由器。每台路由器都使用这些链路状态信息来构建自己的路由表。这种方法能比距离矢量协议更快地完成路由收敛，并且非常适合拓扑频繁变化的大型网络。OSPF 还有其他几个特性使其优于 RIP，包括以下方面：

- **服务类型：** OSPF 可以为每种服务类型（TOS）计算一组单独的路由。
- **负载均衡：** 当存在多条到同一目的地的等成本路由时，OSPF 可以在这些路由之间均匀地分配数据。
- **VLSM：** OSPF 支持变长子网掩码（VLSM）。

> **注意**
>
> 与 RIP 不同，RIP 版本 2 也支持子网。

- 每个接口都会根据往返时间、流量、可靠性和安全性分配一个开销度量值。此外，还可以针对服务类型分配单独的开销。
- OSPF 使用组播进行路由通告，以减轻未参与 OSPF 的系统的负载。

OSPF 是管理由多厂商系统组成的复杂网络的解决方案。常见的路由协议（如 RIP）是为只有少量路由器且冗余度极低的简单网络而设计的。在大型网络中，路由消息会占用大量网络带宽，这些协议的效率不高。OSPF 通过使用组播与参与的路由器交换路由信息来解决这个问题。

对 OSPF 协议的完整阐述超出了本书的范围。要了解 OSPF 的详细信息，可以参考以下资源：

- RFC-1131，“OSPF 规范”
- RFC-1245，“OSPF 协议分析”
- RFC-1246，“OSPF 协议使用经验”
- RFC-1364，“BGP 与 OSPF 的交互”
- RFC-1850，“OSPF 版本 2 管理信息库”
- RFC-2154，“带数字签名的 OSPF”
- RFC-2328，“OSPF 版本 2”
- RFC-2329，“OSPF 标准化报告”
- RFC-2370，“OSPF 不透明 LSA 选项”
- RFC-2676，“QoS 路由机制与 OSPF 扩展”
- RFC-2740，“面向 IPv6 的 OSPF”
- *TCP/IP 网络互连（第 I 卷）*，Douglas Comer 著
- *TCP/IP 详解，卷 I：协议*，W. Richard Stevens 著

## gated

gated 是一个一体化路由守护进程，支持 RIP、RIP II、Hello、BGP、EGP 和 OSPF。由于 gated 能理解所有这些协议，因此它更适合在同一网络中使用多种路由协议的复杂网络。gated 会综合从所有这些协议学到的路由信息，并选择最佳路由。然而，gated 的配置文件比 routed 的更为复杂；如果你的网络很简单，你可以选择运行 routed 来代替。仅启用 RIP 或 RIP II 来运行 gated 非常简单，而且比运行 routed 更可取。

### gated 配置示例

为主机系统配置 gated 非常简单，只需几条配置语句。gated 启动时，会从文件 `/etc/gated.conf` 读取配置。

以下显示的配置模拟了 routed。使用的协议是 RIP。当多个网络接口处于活动状态且内核启用了 IP 转发时，就会发送更新：

```
#
rip yes ;
#
```

要启用内核中的 IP 转发，请使用以下命令：

```sh
# echo "1" > /proc/sys/net/ipv4/ip_forward
```

> **提示**
>
> 必须在内核中启用 UDP 校验和。通常，Linux 默认已启用此功能。此外，还必须在内核中启用 IP 组播支持。RIP 版本 2 使用 IP 组播。这在内核编译期间配置 Linux 内核时完成。关于重新编译内核的讨论，请参阅第 11 章。

以下配置以安静模式运行 RIP；它只侦听数据包，无论配置了多少接口：

```
#
rip yes {
        no broadcast ;
};
#
```

下一个示例适用于运行 RIP 且只有一个网络接口的主机系统。它还演示了如何指定默认路由：

```text
# Define the only network interface as passive to prevent timing out
# the only network interface.
interfaces {
        interface eth0 passive ;
} ;

# enable RIP version 2 with multicast.
rip yes {
        broadcast ;
        defaultmetric 5 ;
        interface eth0 version 2 multicast ;
} ;

# Define a default static route
static {
        0.0.0.0 mask 0.0.0.0 gateway 10.2.0.254 retain ;
}
```

关键字 passive 用于 interface 命令中。在这种情况下，通过使用关键字 passive，你可以确保经过主机唯一网络接口的永久路由不会被 gated 从路由表中删除。通常，当 gated 认为某个网络接口已关闭时，会将其从路由表中删除。在本例中，主机只有一个网络接口，即使 gated 认为该接口已关闭，你也不希望 gated 将其从路由表中删除。将该接口声明为 passive 即可实现此目的。

static 语句用于定义静态路由。在前面的示例中，定义了一条使用默认网关的静态路由，该网关的 IP 地址为 10.2.0.254。

以下示例说明了 RIP II 和 OSPF 两种路由协议的使用：

```text
interfaces {
        interface eth0 passive ;
} ;

rip yes {
        broadcast ;
        defaultmetric 5 ;
        interface eth0 version 2 multicast ;
} ;

ospf yes {
        backbone {
                authtype simple;
                networks {
                10.2.0.0 mask 255.255.0.0;
                10.3.0.0 mask 255.255.0.0;
                };
                interface eth {
                enabled;
authkey "secret";
};
};
};
static {
    0.0.0.0 mask 0.0.0.0 gateway 10.2.0.254;
};
```

`rip yes` 语句可启用 RIP 协议。如果未指定任何 rip 语句，则默认启用该协议。如果系统是只有一个接口的主机，默认选项为 `nobroadcast`。在前面的配置示例中，你指定的是 RIP `broadcast`。指定 `broadcast` 后，无论存在多少接口，RIP 数据包都会被广播。当你想把静态路由或通过其他协议学到的路由传播到 RIP 中时，这非常有用。`defaultmetric` 指令定义了在通过 RIP 通告从其他协议学到的路由时使用的度量值。`interface` 命令控制通过指定接口发送 RIP 的属性。在这里，你已指定在接口 `eth0` 上通过 IP 组播使用 RIP 版本 2。

`ospf yes` 语句启用 OSPF 协议。`backbone` 指令将 OSPF 区域指定为骨干网络。如果配置了多个区域，则至少有一个区域必须是骨干区域。骨干区域也称为区域 `0`。两个术语都可用来指定骨干区域。`authtype` 指令的值可以是 `none` 或 `simple`。如果指定为 `none`，则无需认证；而 `simple` 使用简单的密码认证方法。OSPF 在每个区域使用一种认证方案。每个区域必须使用相同的认证方案。`networks` 指令描述区域的范围。条目以网络地址和网络掩码对的形式指定。`interface` 指令后跟 `eth` 用于指定所有以太网接口。`enable` 指令使所有以太网接口能够参与 OSPF 路由。`authkey` 指令后跟 OSPF 用来验证 OSPF 报文头中认证字段的密码字符串。

> **提示**
>
> 有关所有 gated 选项的完整详细信息以及如何编写 `gated.conf` 文件，请运行 `man gated` 参阅在线手册页。另请参阅《Gated 配置指南》和《Gated 操作指南》，它们位于常规 gated 安装的 `/usr/doc/gated-3.5/doc` 目录中。

## 启动和停止 gated

gated 发行版附带一个名为 `gdc` 的程序，用于启动和停止 gated，并检查 `gated.conf` 文件是否正确。有关 `gdc` 的完整详细信息，请运行 `man gdc` 查看在线手册页。以下是 `gdc` 的一些示例用法。

要使用 gdc 启动 gated，请使用以下命令：

```sh
# /usr/sbin/gdc start
```

要使用 gdc 停止 gated，请使用以下命令：

```sh
# /usr/sbin/gdc stop
```

