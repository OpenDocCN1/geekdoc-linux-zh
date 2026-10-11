
| V50 | 1 | - | 7 | Active 0007.b400.0101 local | |

| V50 | 1 | - | 7 | Listen 0007.b400.0102 | 192.168.1.11 |

| V50 | 1 | - | 7 | Listen 0007.b400.0103 | 192.168.1.12 |

# Switch-B show glbp brief

| Interface | Grp | Pwd | Pri | Active router | Standby router |
| :--- | :--- | :--- | :--- | :--- | :--- |
| V50 | 1 | - | 150 | Standby 192.168.1.11 | 192.168.1.10 local |
| V50 | 1 | - | 7 | Listen 0007.b400.0101 | 192.168.1.10 |
| V50 | 1 | - | 7 | Listen 0007.b400.0102 | 192.168.1.11 |
| V50 | 1 | - | 7 | Listen 0007.b400.0103 | 192.168.1.12 |

# Switch-C show glbp brief

| Interface | Grp | Pwd | Pri | Active router | Standby router |
| :--- | :--- | :--- | :--- | :--- | :--- |
| V50 | 1 | - | 100 | Listen 192.168.1.10 | |
| V50 | 1 | - | 7 | Listen 0007.b400.0101 | 192.168.1.11 |
| V50 | 1 | - | 7 | Listen 0007.b400.0102 | 192.168.1.11 |
| V50 | 1 | - | 7 | Listen 0007.b400.0103 | 192.168.1.12 |

*(注：由于原文中 Switch-C 表格内容存在错位或占位符，此处根据逻辑 进行了对齐翻译处理)*

# AVG

AVF vMAC `0007.b400.0101`

# 激活 AVG

AVF vMAC `0007.b400.0102`

AVF vMAC `0007.b400.0101`

# AVF vMAC 0007.b400.0103

GLBP Group 1 Priority 100

VLAN 50

GLBP Group 1 Priority 200

VLAN 50

192.168.1.10

0000.aaaa.aaaa

GLBP Group 1 Priority 150

VLAN 50

192.168.1.11

0000.bbbb.bbbb

VLAN 50

192.168.1.12

0000.cccc.cccc

![](img/4541d1f2c9832b9303a6df6c929f86f6_180_0.png)

交换机 A

交换机 B

交换机 C

AVG:

所有 ARP 回复：针对 192.168.1.1

发往网关的流量

冗余是 GLBP 组固有的：交换机 A 是 AVG，但如果 AVG 故障，优先级最高的路由器可以接管。

所有路由器都已为组内唯一的虚拟 MAC 地址分配了 AVF 角色。

如果一个 AVF 发生故障，某些客户端会记住分配出的最后一个已知虚拟 MAC 地址。因此，组中的另一台路由器也会接管故障路由器的工作，从而使虚拟 MAC 地址始终保持存状态。

上图说明了当当前激活 AVG 故障时，这些冗余功能是如何响应。在故障之前，交换机 A 因为其高 GLBP 优先级而成为 AVG。

故障后，交换机 B 成为 AVG，使用适用于网关 192.168.1.1 的相应虚拟 MAC 地址响应 ARP 请求。

交换机 A 同时也作为 AVF 运行，参与了网关负载均衡。

交换机 B 也承担了这一职责，使用了与 Switch A 一直使用的虚拟 MAC 地址 `0007.b400.0101` 相同的 `0007.b400.0102`。

因此，任何通过其虚拟 MAC 地址识别网关的主机仍然可以访问活跃的网关或 AVF。

![](img/4541d1f2c9832b9303a6df6c929f86f6_181_0.png)

图 13-2 HSRP 配置示例网络拓扑

# Cisco 设备上的 DHCP 设置 (IPv4)

```
Switch(config)#service dhcp -- 启用 - "no service dhcp" 关闭它
Switch(config)#ip dhcp pool Sales_Wireless -- 创建地址池
Switch(config-dhcp)#network 192.168.10.0 255.255.255.0 -- 地址池的网络号和子掩码
Switch(config-dhcp)#default-router 192.168.10.1 -- 默认网关
Switch(config-dhcp)#dns-server 4.4.4.4
Switch(config-dhcp)#lease 3 15 -- 天、小时、分钟 - 默认24 小小时
Switch(config)#exit
Switch(config-dhcp)#dhcp excluded-address 192.168.10.1 192.168.10.10
```

# DHCP 中继

如果你需要为与 DHCP 服务器不在同一局域网的主机提供地址，可以配置路由器接口来中继 DHCP 客户端请求。

```
Router(config)#interface fa0/0
Router(config-if)#ip helper-address 10.10.10.254
```

路由器和 `fa0/0` 位于 `192.168.10.1`，`10.10.10.254` 显然位于不同的子网，但 DHCP 服务器 IP 转发的不只是 DHCP 客户端请求。

# 验证 DHCP

```
show ip dhcp binding -- 列出当前租用每个 IP 地址的状态信息
show ip dhcp pool [poolname] -- 列出地址范围以及已租用地址的状态
show ip dhcp conflict statistics -- 列出 DHCP 服务器统计信息
show ip dhcp conflict -- 显示冲突地址
```

# 更多地址池示例

```
Corp#config
Corp(config)#ip dhcp excluded-address 192.168.10.1
Corp(config)#ip dhcp excluded-address 192.168.10.250
Corp(config)#ip dhcp pool SF_LAN
Corp(config-dhcp)#network 192.168.10.0 255.255.255.250
Corp(config-dhcp)#default-router 192.168.10.1
Corp(config-dhcp)#dns-server 4.4.4.4
Corp(config-dhcp)#exit
Corp(config)#ip dhcp pool LA_LAN
Corp(config-dhcp)#network 192.168.20.0 255.255.255.250
Corp(config-dhcp)#default-router 192.168.20.1
Corp(config-dhcp)#dns-server 4.4.4.4
```

将这些配置添加到两台路由器中，以便它们转发 DHCP：

```
LA(config)#int f0/0
LA(config-if)#ip helper-address 172.16.10.5
```

```
SF(config)#int f0/0
SF(config-if)#ip helper-address 172.16.10.1
```

# 网络地址翻译：静态 NAT、动态 NAT 和 PAT

![](img/4541d1f2c9832b9303a6df6c929f86f6_183_0.png)

# IP 静态 NAT
