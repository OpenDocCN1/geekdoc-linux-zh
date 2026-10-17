
| home | 拒绝入站流量，除非与出站流量相关或匹配 ssh、mdns、pp-client、samba-client 或 dhcpv6-client 预定义服务。 |

| internal | 拒绝入站流量，除非与出站流量相关或匹配 ssh、mdns、pp-client、samba-client 或 dhcpv6-client 预定义服务（初始与 home 区域相同）。 |

| work | 拒绝入站流量，除非与出站流量相关或匹配 ssh、pp-client 或 dhcpv6-client 预定义服务。 |

| public | 拒绝入站流量，除非与出站流量相关或匹配 ssh 或 dhcpv6-client 预定义服务。新添加网络接口的默认区域。 |

| 区域名称 | 默认配置 |

|---|---|

| external | 拒绝入站流量，除非与出站流量相关或匹配 ssh 定义的服务。通过此区域转发出的站 IPv4 流量将被伪装，看起来像是源自网络接口的 IPv4 地址。 |

| dmz | 拒绝入站流量，除非与出站流量相关或匹配 ssh 定义的服务。 |

| block | 拒绝所有入站流量，除非与出站流量相关。 |

| drop | 丢弃所有与出站流量相关的入站流量（甚至不响应 ICMP 错误）。 |

有关可用预定义区域列表及其索引用法，请参阅 `firewall.zones(5)` 手页。

# 预定义服务

防火墙服务包含了一些常用服务的预定义配置，以简化过滤规则。例如，与其研究 NFS 服务器的相关部分，不如使用预定义的 `nfs`。下表列出了防火墙服务在默认配置中使用的预定义服务。

| 服务名称 | 配置 |

|---|---|

| ssh | 本地 SSH 服务器。指向 22/tcp 的流量。 |

| dhcpv6-client | 本地 DHCPv6 客户端。指向 546/udp 的 fe80::64 网络流量。 |

| ipp-client | 本地 IP 打印。指向 631/udp 的流量。 |

| samba-client | 本地 Windows 文件共享客户端。指向 137/udp 和 138/udp 的流量。 |

| mdns | 多播 DNS (mDNS) 本地名称解析。指向 5353/udp 224.0.0.251 (IPv4) 或 ff02::fb (IPv6) 多播地址。 |

你可以使用 `firewall-cmd --get-services` 列出服务。

```
[root@host]# firewall-cmd --get-services
RH-Satellite-6 RH-Satellite-6-capsule amenda-client amanda-k5-client amqp amqs
apcusd bacula bacula-client bb bitcoin-rpc bitcoin-testnet
bitcoin-testnet-rpc bitorrent-lsd ceph ceph-mon cfengine collect
...output ...
```

如果预定义的服务配置不适用于你的场景，则需要手动指定所需的端口和协议。你可以使用控制台界面查看预定义服务并手动定义额外的端口和协议。

# 配置防火墙守护

除此之外，系统管理员与防火墙服务的交互常用方式有两种：

- 控制台图形界面

- `firewall-cmd` 命令行工具

# 使用控制台配置防火墙服务

要使用控制台管理防火墙服务，你需要登录并提升权限。你可以通过点击“Limited access”（限制访问）或“Turn on administrative access”（开启管理访问）按钮来提升权限。在在提示时输入密码。管理模式根据你的用户 sudo 配置提升权限。作为安全提醒，在执行完需要管理权限的任务后，记得切换回限制访问模式。

点击左侧导航菜单中的“Networking”选项进入防火墙网络页面。点击“Rules and zones”按钮导航到防火墙页面。

![](img/2eff90170b8c94cce3a908ab927e38c2_278_0.png)

图 9.1：控制台网络页面

![](img/2eff90170b8c94cce3a908ab927e38c2_278_1.png)

图 9.2：控制台防火墙页面

## 第 9 章 | 管理网络安全

**添加服务**页面显示了可用的预定义服务。

![](img/2eff90170b8c94cce3a908ab927e38c2_279_0.png)

要选择服务，请滚动列表或在**过滤服务**文本框中输入。在接下来的示例中，`http` 字符串会过滤出相关的服务。勾选服务左侧的复选框以允许其通过防火墙。点击**添加服务**按钮完成过程。

![](img/2eff90170b8c94cce3a908ab927e38c2_279_1.png)

界面返回到**防火墙**页面，您可以在此处查看更新后的允许服务列表。

262 RH134-RHEL9.0-en-2-20220609

## 第 9 章 | 管理网络安全

![](img/2eff90170b8c94cce3a908ab927e38c2_280_0.png)

## 从命令行配置防火墙

`firewall-cmd` 命令与 `firewall` 守护进程交互。它作为 `firewall` 包的一部分安装的，适用于倾向于使用命令行的管理员、没有图形用户界面的系统，或用于防火墙设置的脚本。

下表列出了频繁使用的 `firewall-cmd` 命令及其说明。请注意，除非另有指定，否则所有命令都作用于*运行时*配置上，除非指定了 --permanent 选项。如果指定了 --permanent 选项，您必须通过运行 `firewall-cmd load` 命令来激活设置，该命令会读取当前的永久配置并将其应用于新的运行时配置。列出的许多命令使用 --zone= 选项来确定它们影响哪个区域。在需要子网掩码的地方，请使用 CIDR 表示法，例如 192.168.1/24。

| firewall-cmd 命令 | 说明 |

| --- | --- |

| --get-default-zone | 查询当前区域。 |

| --set-default-zone=ZONE | 设置默认区域。这会同时更改运行时和永久配置。 |

| --get-zones | 列出所有可用区域。 |

| --get-active-zones | 列出所有当前使用的区域（已绑定接口或源的区域），以及它们的接口和源信息。 |

| --add-source=CIDR [--zone=ZONE] | 将所有来自 IP 地址或子网掩码的流量路由到指定的区域。如果没有提供 --zone 选项，则使用默认区域。 |

| --remove-source=CIDR [--zone=ZONE] | 移除路由来自 IP 地址或网络区域的所有流量的路由规则。如果没有提供 --zone 选项，则使用默认区域。 |

| --add-interface=INTERFACE [--zone=ZONE] | 将所有来自 INTERFACE 的流量路由到指定的区域。如果没有提供 --zone 选项，则使用默认区域。 |

### firewall-cmd 命令

### 说明

```
--change-interface=INTERFACE --zone=ZONE
```

将接口与 ZONE 关联，而不是其当前的区域。如果没有提供 --zone= 选项，则使用默认区域。

```
--list-all [--zone=ZONE]
```

列出 ZONE 配置的所有接口、源和端口。如果没有提供 --zone= 选项，则使用默认区域。

```
--list-all-zones
```

检索所有区域的所有信息（接口、源、服务）。

```
--add-service=SERVICE --zone=ZONE
```

允许流量通过 SERVICE。如果没有提供 --zone= 选项，则使用默认区域。

```
--add-port=PORT/PROTOCOL --zone=ZONE
```

允许流量通过 PORT/PROTOCOL(s)。如果没有提供 --zone= 选项，则使用默认区域。

```
--remove-service=SERVICE --zone=ZONE
```

从该区域的允许列表中移除 SERVICE。如果没有提供 --zone= 选项，则使用默认区域。

```
--remove-port=PORT/PROTOCOL --zone=ZONE
```

从该区域的允许列表中移除 PORT/PROTOCOL(s)。如果没有提供 --zone= 选项，则使用默认区域。

```
--reload
```

丢弃运行时配置并应用持久化配置。

以下示例将默认区域设置为 dmz，将所有来自 192.168.0.0/24 网络的所有流量分配给内部（internal）区域，并为内部区域上的 mysql 服务打开网络端口。
