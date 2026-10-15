
创建目的别名后，就可以创建分隧道防火墙策略。该策略应首先允许 DHCP。接下来，务必包含任何所需的“拒绝访问”规则，以限制和控制远程用户不应访问的任何资源的访问。然后策略将检查流量是否应转发到企业网络。最后，任何其他流量都将使用`route src-nat`命令放在本地网络。该命令将使用远程 AP 的 IP 地址作为流量的源。以下 CLI 命令将定义策略和规则：

```cli
(config)#ip access-list session split-tunnel-policy
(config-sess-split-tunnel-policy)#any any svc-dhcp permit
(config-sess-split-tunnel-policy)#alias corpnet alias corpnet any permit
(config-sess-split-tunnel-policy)#alias user any any route src-nat
```

以下分隧道策略的 CLI 示例更具限制性。你不需要使用这些示例；你可以定义任何想要的防火墙规则。

```cli
(config) #ip access-list session split-tunnel-policy
(config-sess-split-tunnel-policy)#any any svc-dhcp permit
(config-sess-split-tunnel-policy)#user alias corpnet any permit
(config-sess-split-tunnel-policy)#alias user any any route src-nat
```

由于客户端分配的是用户角色而非策略，因此需要创建一个用户角色，并将策略分配给该角色，如下文的 CLI 命令所示：

```cli
(config) #user-role corp-split-role
(config-role) #session-acl split-tunnel-policy
```

接下来，你需要指定如何为通过验证的客户端分配用户角色。客户端可以通过 VSA、服务器派生的角色或默认角色接收角色。该过程在第 7 章中已进行解释。

最后，在 VAP 配置文件中，需要将转发模式设置为分隧道。在分隧道模式下运行时，无法通过 VSA、服务器派生规则或用户派生规则更改 VLAN。分配给 VAP 的 VLAN 将是用户接收的 VLAN。

## 解密隧道 (Decrypt-Tunnel)

当 VAP 配置为解密隧道模式时，所有 WLAN 流量都被封装并转发到控制器，类似于隧道模式（Tunnel mode）。区别在于，当客户端将数据发送到远程 AP 时，远程 AP 在转发到控制器之前会先对数据解密。虽然在运行于远程 AP 的 VAP 上启用解密隧道技术上是有效的配置，但通常不是明智的决定。由于远程 AP VPN 隧道默认不对客户端流量提供任何加密，解密客户端流量然后通过互联网将其隧道到 Aruba 控制器并不是明智的安全选择。因此，将不再进一步解释此配置。

## VAP 远程 AP 操作模式

上一节“VAP 数据转发模式”描述了四种可能的转发模式。在将 WLAN 分配给远程 AP 时，除了选择将使用的转发模式外，必须指定远程 AP 操作模式。VAP 配置文件可以配置为四种操作模式之一。远程 AP 操作模式定义了 VAP 如何广播以及当远程 AP 与 VPN 服务器之间出现连接性问题时其可用性。

四种远程 AP 操作模式为标准模式（Standard）、始终模式（Always）、备份模式（Backup）和持久模式（Persistent）。根据 VAP 的需求，可以为每个 VAP 分配自己的操作模式。将在后续将在将在介绍。

### 标准模式 (Standard)

当远程 AP 启动并与控制器建立 VPN 连接时，此时远程 AP 将下载任何配置为标准操作模式的 VAP 配置。任何配置为标准操作模式的 VAP 将处于运行状态。简单来说，如果 VPN 隧道接通，WLAN 就可用。标准模式可用于任何转发方法（隧道、桥、分隧道和解密隧道）。

标准模式通常与隧道模式和分隧道模式配合使用，因为如果隧道关闭，这些模式将毫无用。

### 始终模式 (Always)

当将 VAP 配置为始终模式时，只要远程 AP 有电且有链路，VAP 即可运行。始终模式通常与本文介绍的桥模式配合使用，如图 11-7 所示。无线用户将收到门户登录页面并允许登录。如果用户验证成功，由于用户流量通过远程 AP 进行 NAT，因此允许访问互联网的是远程 AP 的 MAC 地址。

![img/f0a787182fde585d5ed23c147a0298_382_0.png]

**图 11-7:** 酒店模式

### 备份模式 (Backup)

备份模式的示例通常被称为“酒店模式”。如果远程 AP 插入酒店以太网网络或任何带有门户的以太网网络，门户将阻止远程 AP 向控制器建立 VPN 隧道。如果远程 AP 无法建立 VPN 隧道，将广播备份模式（酒店模式）VAP。此 WLAN 将允许无线用户连接到 SSID，远程 AP 将用户流量 NAT 到门户服务器。在远程 AP 被允许访问互联网并成功建立到控制器的 VPN 隧道后，备份模式 VAP 将关闭。

备份模式 VAP 的另一个良好用途是为通常使用 802.1X/EAP 分隧道连接的员工提供备份互联网访问。如果 VPN 隧道断开，启用分隧道的 VAP 也断开。这将导致客户端无法访问企业网络或互联网。在这种情况下，启用备份模式 VAP 为员工提供临时互联网访问可能是很有用的，直到 VPN 隧道和 802.1X/EAP 分隧道 VAP 恢复工作。

### 持久模式 (Persistent)

在使用持久模式时，必须在启用 VAP 之前先建立 VPN 隧道。一旦 VPN 隧道接通，如果它断开，VAP 将继续运行。

持久模式（Persistent mode）是为基于 802.1X/EAP 的 VAP 设计的。遗憾的是，持久模式适用于使用桥接模式（Bridge forwarding mode）的 VAP，而大多数基于 802.1X/EAP 的 VAP 都配置为分拆隧道模式（Split-Tunnel forwarding mode）。因此，你几乎没有理由使用持久操作模式。持久模式的一种场景是：你正在使用桥接模式，并希望初始认证发送到控制器。一旦认证通过，用户流量将通过本地桥接到互联网。如果 VPN 隧道断开，已认证的用户将继续工作，而新用户将无法通过认证。

## 带操作模式的转发模式

前面的几节描述了四种转发模式和四种操作模式。表 11-1 提供了转发模式与操作模式使用的交叉引用表。图中未包含解密隧道模式（Decrypt-Tunnel mode），因为不建议在远程 AP（RAP）中使用。

在本章中，提供了使用不同转发模式的示例。这些用途列在图中的括号内。

**表 11-1：** 带操作模式的转发模式

| 转发模式 | 隧道 (Tunnel) | 桥接 (Bridge) | 分拆隧道 (Split-Tunnel) |
| :--- | :--- | :--- | :--- |
| **标准 (Standard)** | VPN 隧道建立时时启用 VAP（语音 VAP） | VPN 隧道建立时时启用 VAP | VPN 隧道建立时时启用 VAP（员工 802.1X/EAP VAP）（访客强制性门户 VAP） |
| **始终开启 (Always)** | 不支持 | VAP 始终启用。开启或启用 PSK 的 SSID VAP 配置文件存储在远程 AP 上（家庭访客 VAP） | 不支持 |
| **备份 (Backup)** | 不支持 | VPN 隧道断开时启用 VAP。开启或启用 PSK 的 SSID VAP 配置文件存储在远程 AP 上（酒店临时 VAP） | 不支持 |
| **持久 (Persistent)** | 不支持 | VPN 隧道建立时启用 VAP | VPN 隧道断开时 VAP 保持启用 |

### 空口监控 (AIR MONITOR)

空口监控（AM）功能可以在任何 IAP、UAP、园区 AP 或 RAP 的任何射频上配置。AM 是一种不支持任何 VAP 的射频模式，专门扫描 802.11 信道以获取二层信息。虽然 AP 也会扫描工作信道以外通道，但 AM 的扫描速度更快，能为控制器提供更多信息并更快速地访问。AP 或 AM 采样射频（RF）环境的时间越长，无线入侵防御（WIP）的计算就越准确、及时。

控制器还可以使用 AM 来提供无线和/或有线非法 AP 封禁。这意味着如果你在网络中部署了 AM，AP 将不会被调用来执行此任务，从而使其能够投入更多精力来支持无线用户。

AM 执行的额外扫描将为控制器或外部监控服务器（如果你在使用的话，例如 AirWave 服务器）提供更多统计信息。在某些情况下，AP 无法执行扫描，例如 AP 正在托管来自语音或视频客户端的高优先级流量。在这些期间，AP 贡献的数据量将大幅减少。在设计运行大量高优先级流量的无线网络时，应始终考虑实施 AM。
