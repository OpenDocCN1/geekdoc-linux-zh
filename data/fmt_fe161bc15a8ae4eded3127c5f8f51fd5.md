
下一步是验证 FastEthernet 0/2 是否已分配到销售 VLAN (VLAN 2)。可以使用 `show vlan` 命令进行验证。该命令显示分配给每个 VLAN 的接口。

```
Switch# show vlan
```

| VLAN Name | Status | Ports |
| --- | --- | --- |
| 1 | active | Fa0/1, Fa0/3, Fa0/4, Fa0/5, Fa0/6, Fa0/7, Fa0/8, Fa0/9, Fa0/10 |
| 2 | Sales | active Fa0/2 |

后续步骤是将端口 3 和 4 分配到销售 VLAN (VLAN 2)，并将端口 6、7、8 分配到工程 (VLAN 3)。完成后，可以使用 `show vlan` 命令验证端口分配，如所示。

```
Switch#show vlan
```

| VLAN Name | Status | Ports |
| --- | --- | --- |
| 1 | active | Fa0/1, Fa0/5, Fa0/9, Fa0/10 |
| 2 | Sales | active Fa0/2, Fa0/3, Fa0/4 |
| 3 | Engineering | active Fa0/6, Fa0/7, Fa0/8 |

你可以专门查看 VLAN 分配。可以使用 `show run` 查看交换机的运行配置。

```
Switch# show vlan
```

| VLAN Name | Status | Ports |
| --- | --- | --- |
| 1 | active | Fa0/1, Fa0/2, Fa0/3, Fa0/4, Fa0/5, Fa0/6, Fa0/7, Fa0/8, Fa0/9, Fa0/10 |
| 2 | Sales | active |
| 3 | Engineering | active |

（注：此处省略了重复的表格内容，翻译逻辑与原文保持一致）

## 测试你的知识

- 1. 下列哪项用于专门查看 Administrator VLAN 的分配情况？

a. Switch(config)#sh vlan name Administrator

b. Switch(vlan)#sh vlan name Administrator

c. Switch#sh vlan name Administrator

d. Switch#sh vlan name Administrator

- 2. 使用下列哪个命令可以在 Cisco 交换机上设置默认网关？默认网关的 IP 地址为 172.16.35.1

a. Switch(config-if)# ip default-gateway 172.16.35.1

b. SwitchA# ip default-gateway 172.16.35.1

c. Switch(config-gate)# ip default-gateway 172.16.35.1

d. Switch(config)# ip default-gateway 172.16.35.1

# 8-4 生成树协议

生成树协议（Spanning-Tree Protocol）：一种链路管理协议，用于防止环路并控制冗余数据路径上的流量。

本节介绍了生成树协议（STP）。STP 是一种链路管理协议，用于防止环路并控制冗余数据路径上的数据流。环路对以太网是有害的，因为数据包可以通过冗余路径发送。生成树协议用于确保只选择一条数据路径。生成树协议还通过将冗余数据路径置于阻塞状态，强制其中一条冗余路径处于备用状态。

桥接协议数据单元（Bridge Protocol Data Unit, BPDU）：交换机用于与参与生成树协议的交换机共享信息。

参与生成树协议的交换机通过桥接协议数据单元（BPDU）帧与其他交换机交换信息。交换机使用 BPDU 用于以下set：

- 为生成树网络拓扑选举根交换机。
- 移除冗余路径。
- 选择到交换机的最短距离路径作为通往根交换机的最佳路径。
- 选择每个交换机的一个端口作为根端口。
- 选择属于生成树协议的端口。

配置 BPDU（Configuration BPDU）：交换机用于选举“根”交换机。

交换机假设通过交换 BPDU 选举根交换机，并选择 MAC 地址最低的交换机作为根交换机。图中显示了 BPDU 包的一部分。在这种情况下，MAC 地址为 003014A6940 的交换机在开始查看哪个交换机将被选为“根”时发送了该包。

拓扑变化通知（Topology Change Notification, TCN）：用于指示交换机发生了变化。

BPDU Config BID=003014A6940 PID=0x801B

“Config”表示这是一个配置包，用于交换机选举“根”交换机。从交换机可能发出的另外两种类型的包是拓扑变化通知（TCN），用于指示交换网络拓扑发生了变化；以及拓扑变化通知确认（Topology Change Notification Acknowledgement, TCA），来自另一台交换机确认 TCN 的确认。

拓扑变化通知确认（TCA）：来自另一台交换机确认 TCN 的确认。

图 8-2 展示了 BPDU 内容的示例。显示根 ID——MAC 地址为 003019A6940。BPDU 定隔交换一次，用于让交换机感知网络拓扑的任何变化。默认通知间隔为 2 秒，称为“Hello 时间（Hello Time）”，如图 8-2 所示。

```
IEEE 802.1D - Bridge Management Protocol (IEEE 802.1)
Bridge Protocol Data Unit (BPDU)
Version    0x0000 (Bridge PDDU)
Type        0x00 (Configuration)
Flags      ... Not Topology Change Acknowledgment
>           ... Not Topology Change
>           ... Not Root Bridge
>           ... Not Designated Bridge
>           ... Not Priority Election
>           ... Not Claim Election
>           ... Not Message Age
Root ID     0030.19a6.9400
Root Bridge Priority 0x8010
Bridge ID     0030.14a6.9400
Bridge Priority 32768
Root Port 0
Designated Port 0
Message Age 0




```

# 8-5 网络管理

SNMP（简单网络管理协议）：一种用于收集和组织网络信息的协议。

管理信息库（Management Information Base, MIB）：定义受管理实体的数据库。

SNMP 使用管理-代理模型。SNMP 管理是监控网络的软件，而代理是运行在网络设备上的软件。

SNMP 协议使用几种消息与代理通信：

- GetRequest：从代理检索信息。
- GetNextRequest：检索 MIB 中的下一个项。
- SetRequest：设置代理上的值。
- Trap：由代理通知管理器事件。
- Response：由代理用于响应 Get 或 GetNext 请求。

MIB 组织成树形结构。MIB 中的每个对象都通过对象标识符（OID）识别。OID 是由点分隔的数字序列，例如 1.3.6.1.2.1.1.1.0。

## SNMP 操作

| 消息 | 说明 |
| :--- | :--- |
| GetRequest | 管理器发送请求特定对象的值。 |
| GetNextRequest | 管理器发送请求 MIB 树中的下一个对象。 |
| SetRequest | 管理器发送设置特定对象的值。 |
| Trap | 代理发送通知管理器事件。 |
| Response | 代理用于响应 Get 或 GetNext 请求。 |

## 配置 SNMP

要在 Cisco 交换机上配置 SNMP，使用以下命令：

1. 进入全局配置模式：

```
Switch#conf t
```

2. 配置只读访问的社区字符串：

```
Switch(config)#snmp-server community public ro
```

3. 配置读写访问的社区字符串：

```
Switch(config)#snmp-server community private rw
```

4. 配置 Trap 目标，指定管理器的 IP 地址和社区字符串：

```
Switch(config)#snmp-server host 172.16.35.1 version 2c public
```

## SNMP 管理软件

在下一个示例中，社区字符串密码设置为 `makessecret`，权限设置为读写 (rw)。再次进入路由器的 `(config)#` 模式并输入命令 `sniff community makessecret rw`：

```
RouterB(config)# show run
```

```
snmp-server community makessecret RW
```

可以使用路由器特权模式提示符下的 `show run` 命令来验证 SNMP 配置。这里显示了配置文件中列出路由器 SNMP 配置的部分内容：

图 8-4 显示了已配置路由器与运行 SNMP 管理软件的计算机之间的连接设置。SNMP 管理软件通过端口 161 向路由器下发 MIB 实例，由路由器返回响应。图 8-5 显示了另一个使用 SNMP 获取路由器接口信息的示例。SNMP 管理器配置了主机 IP 地址 `10.10.10.1`、set值（端口号）`161` 以及 10 字符社区字符串 `makessecret`（显示为 **************）。MIB (ifDespd) 被设置为路由器，对于每个接口，提供的数据均显示了路由器接口的速率设置。

![](img/ec00be08b0c45b337e7cb610696f1b45_367_0.png)

图 8-4 将 SNMP 管理工具连接到路由器的设置。

![](img/ec00be08b0c45b337e7cb610696f1b45_367_1.png)

图 8-5 使用 SNMP 软件管理工具获取接口速率设置。

SNMP 的另一个重要应用是获取流量数据统计。图 8-6 显示了此类示例。SNMP 管理程序 MIB (ifOutOctets) 返回离开路由器的字节数。路由器有一个计数器来跟踪它。第一个结果显示 `ifOutOctets 7002270`。下一个结果显示 `ifOutOctets` 返回值为 `7002361`。

![](img/ec00be08b0c45b337e7cb610696f1b45_368_0.png)

图 8-6 使用 SNMP 收集流量统计数据的示例。

收集统计数据的 SNMP 管理程序会跟踪测量之间的时间和通过的字节数。根据所需信息，这些信息可以按小时、天、周或月计算平均流量。收集流量统计数据的示例见第 10 章第 6 节。关于计数器的最后一点是，除非路由器重启，否则计数器不会重置。

网络管理开发了两个版本的 SNMP。版本分别是 SNMPv2 和 SNMPv3。SNMPv2 开发于 1993 年；然而，它从未与 SNMPv1 完全兼容。SNMPv2 试图解决安全问题，但这导致了许多变体的产生，且 SNMPv2 从未被网络行业完全接受。一种名为 SNMPv2c（基于社区的 SNMP 版本 2）的变体比其他变体应用广泛。SNMPv3 开发于 1998 年，实现了与 SNMPv1 兼容并为 SNMP 添加安全性的重要目标。SNMPv3 的安全功能包括机密性、完整性和身份验证。机密性意味着包经过加密以防止嗅探；完整性确保正在传输的数据未被篡改；身份验证则意味着数据来自已知源。

- SNMPv2: 简单管理协议版本 2
- SNMPv3: 简单管理协议版本 3

## 8-5 节回顾

本节涵盖了以下 Network+ 考试目标。

4.4 给定场景，使用适当 Network+ 监控资源分析流量

本节介绍了简单网络管理协议（SNMP）。一个重要概念是 SNMP 使用网络端口 161 传输数据。此外，确保你理解 MIB。

## 测试知识

+ 1. 下列哪项是基础网络管理工具的最佳示例？

a. SNMP

b. ping

c. trace route

d. Documentation

+ 2. 下列哪项最能描述 MIB？（选择所有适用项）

a. 管理信息库（Management Internet Base）是标准对象的集合，用于获取网络设备上的某些配置参数和性能数据。

b. 管理信息库（Management Information Base）是标准对象的集合，用于获取网络设备的数据。

c. 管理信息库（Management Information Base）是标准组播地址的集合，用于获取某些配置参数。

d. 管理信息库（Management Information Base）是标准对象的集合，用于获取某些配置参数。

# 8-6 以太网供电 (PoE)

随着校园规模扩大，网络管理员面临的挑战之一是确保为网络设备（例如交换机、无线接入点和 IP 电话）提供电源。为每个需要的网络设备布电并不总是现实或负担得起的。这一挑战通过以太网供电（PoE）得到了解决。以太网供电标准（IEEE 802.3af）于 2003 年通过，适用于运行 100BASE-T、100BASE-T 和 1000BASE-T 技术的网络。这提供了一种标准化技术，可以通过现有的 CAT5 或更好的网络线缆（CAT5 或更高）为网络设备供电。

PoE 的优点包括：

- 无需为所有网络设备布外部电源。
- 可以在一根电缆上传输电源和数据。
- 可以通过 SNMP 进行管理。
- 网络设备可以灵活移动。

以太网供电（PoE）：通过网络线缆（CAT5 或更高）供电的技术。

由 IEEE 802.3af 定义的以太网供电如下：

- 每个端口 15.4 瓦
- 48 伏系统

PoE 定义了两个网络硬件设备：受电设备（PD）和供电设备设备（PSE）。PSE 的三个主要功能如下：

| 受电设备 (PD) | 供电设备设备 (PSE) |
| :--- | :--- |
| 检测 PD 的能力 |
| 为 PD 供电 |
| 电源监控 |

两种供电设备设备（PSE）是终端设备和中间设备。检查交换机状态的实用命令是：

```
show power inline
```

| 接口 |可用 (Watts) | 已用 (Watts) | 剩余 (Watts) |
| :--- | :--- | :--- | :--- |
| 0/0 | 30.0 | 0.0 | 30.0 |
| 0/1 | 30.0 | 0.0 | 30.0 |
| 0/2 | 30.0 | 0.0 | 30.0 |
| 0/3 | 30.0 | 0.0 | 30.0 |
| 0/4 | 30.0 | 0.0 | 30.0 |
| 0/5 | 30.0 | 0.0 | 30.0 |
| 0/6 | 30.0 | 0.0 | 30.0 |
| 0/7 | 30.0 | 0.0 | 30.0 |
| 0/8 | 30.0 | 0.0 | 30.0 |
| 0/9 | 30.0 | 0.0 | 30.0 |
| 0/10 | 30.0 | 0.0 | 30.0 |
| 0/11 | 30.0 | 0.0 | 30.0 |
| 0/12 | 30.0 | 0.0 | 30.0 |
| 0/13 | 30.0 | 0.0 | 30.0 |
| 0/14 | 30.0 | 0.0 | 30.0 |
| 0/15 | 30.0 | 0.0 | 30.0 |

由 IEEE 802.3af 定义的 PoE 供电如下

## 测试你的知识

- 1. 下列哪是运行以太网供电（Power over Ethernet）的优点？（选择所有适用项）

a. 不需要为所有网络设备接入外部电源。

b. PoE 允许提高数据吞吐量。

c. 无论制造商是哪个，PoE 适用于所有网络设备。

d. 你可以在一根电缆上传输电源和数据。

- 2. PD 设备是如何被发现的，由哪个设备发现它们？

a. 电阻功率发现/ESE

b. PoE 发现/PSE

c. 电阻功率发现/PSE

d. PoE 发现/ESE

## 总结

本章介绍了 VLAN 的基础知识和交换机配置。你还被介绍了生成树协议（Spanning-Tree Protocol）以及选择根桥接的过程。此外，你还学习了 SNMP 网络管理工具以及相关的 MIB。最后，介绍了以太网供电（Power over Ethernet）的操作。请确保你理解本章中提出的以下概念：

- 理解并能够描述三种类型的 VLAN。
- 理解交换机配置和静态 VLAN 配置的基础。
- 能够解释生成树协议。
- 解释如何使用 SNMP 管理工具监控校园网内部的数据流量和性能。
- 讨论以太网供电的操作。

## 问题与练习

## 8-2 节
