
以下 CLI 命令创建 AAA 配置文件，然后将服务器组、认证配置文件和默认角色链接到该配置文件：

```
(config) #aaa profile employee-aaa-profile

(AAA Profile "employee-aaa-profile") #dot1x-server-group radius-group01

(AAA Profile "employee-aaa-profile") #authentication-dot1x 1x-auth-profile

(AAA Profile "employee-aaa-profile") #dot1x-default-role authenticated
```

选择 **Configuration（配置）** ⇒ **SECURITY（安全）** ⇒ **Authentication（认证）** ⇒ **AAA Profiles（AAA 配置文件）** 将带你进入可以使用 WebUI 创建 AAA 配置文件的菜单。

以下 CLI 命令显示指定的 AAA 配置文件的配置，在此例中 `employee-aaa-profile`。认证配置文件、默认角色和服务器组被高亮显示。

```
#show aaa profile employee-aaa-profile

AAA Profile "employee-aaa-profile" ----------------------------------
```

| 参数 | 值 |
| :--- | :--- |
| 初始角色 | `logon` |
| MAC 认证配置文件 | N/A |
| MAC 认证默认角色 | `guest` |
| MAC 认证服务器组 | `default` |
| 802.1X 认证配置文件 | `1x-auth-profile` |
| 802.1X 认证默认角色 | `authenticated` |
| 802.1X 认证服务器组 | `radius-group01` |
| 从 CPPM 下载角色 | 禁用 |
| L2 认证失败通过 | 禁用 |
| 多服务器审计 | 禁用 |
| 用户空闲超时 | N/A |
| 无线用户最大 IPv4 数量 | 2 |
| RADIUS 审计服务器组 | N/A |
| RADIUS 中期性审计 | 禁用 |
| XML API 服务器 | N/A |
| RFC 3576 服务器 | N/A |
| 用户派生规则 | N/A |
| 有线到无线漫游 | 启用 |
| SIP 认证角色 | N/A |
| 设备类型分类 | 启用 |
| 强制 DHCP | 禁用 |
| PAN 防火墙集成 | 禁用 |
| Open SSID radius accounting | 禁用 |

## SSID 配置文件

配置 SSID 是一项相当简单的任务。SSID 配置文件定义了将广播的 SSID、将使用的认证方法以及将实现的加密，如图 5-10 所示。请注意，SSID 配置文件指定了认证和加密的类型。

![](img/f0a787182fde585d5ed5e23c147a0298_144_0.png)

**图 5-10:** SSID 配置文件

以下 CLI 命令创建 SSID 配置文件，然后将服务器组、认证配置文件和默认角色链接到配置文件：

```
(config) #ssid profile employee-profile

(SSID Profile "employee-profile") #role authenticated 

(SSID Profile "employee-profile") #authentication-dot1x 1x-auth-profile

(SSID Profile "employee-profile") #encryption wpa2
```

SSID 配置文件通常在 RADIUS 菜单中创建，如图 5-11 所示。SSID 配置文件指定了认证和加密的类型，任何配置文件都可以在 RADIUS 菜单中修改。

以下 CLI 命令显示指定的 SSID 配置文件的配置，在此例中为 `employee-profile`。

```
#show wlan ssid employee-profile

SSID Profile "employee-profile" ----------------------------------
```

| 参数 | 值 |
| :--- | :--- |
| 启用 | 启用 |
| 加密 | `wpa2` |
| 管理帧保护 | 禁用 |
| DTIM 间隔 | 1 |
| 短前导 | 启用 |
| 最大连接数 | 64 |
| 无线多媒体 (WMM) | 禁用 |
| 无线多媒体-APSD 节能 | 启用 |
| WMM TSPEC 最小活动 | 0 |
| 覆盖 DSCP 映射 | 禁用 |
| WMM 语音 AC 映射 (0-63) | N/A |
| WMM 视频 AC 映射 (0-63) | N/A |
| WMM 尽力为 AC 映射 (0-63) | N/A |
| WMM 背景 AC 映射 (0-63) | N/A |
| 站点老化时间 | 1000 |
| 最大传输失败次数 | 0 |
| 传输尝试次数 | 8 |
| 电池增强 | 禁用 |
| WEP 密钥 1 | N/A |
| WEP 密钥 2 | N/A |
| WEP 密钥 3 | N/A |
| WEP 密钥 4 | N/A |
| WEP 传输密钥索引 | 1 |
| WPA 十进制密钥 | N/A |
| WPA 密码 | N/A |
| EDCA 参数站点 | N/A |
| EDCA 参数 AP | N/A |
| BC/MC 速率优化 | 禁用 |
| 交付 EAP 帧的速率优化 | 启用 |
| 严格 Spectralink 协议 (SVP) | 禁用 |
| 高吞吐量 SSID 配置文件 | `default` |
| 802.11g Beacon 速率 | `default` |
| 802.11a Beacon 速率 | `default` |
| 视频多播速率优化 | `default` |
| 宣告 QBSS 负载 IE | 禁用 |
| 宣告位置信息 | 禁用 |
| 宣告 AP 名称 | 禁用 |
| 802.11r 配置文件 | N/A |
| 强制开放站点用户 VLAN | 禁用 |
| 启用 OKC | 启用 |

## VLAN

关于 VLAN 没什么好说的。当你创建一个虚拟设备时，你会为它分配一个 VLAN。因此，需要在控制器上创建 VLAN。VAP 用户流量将放置在此 VLAN 中。以下 CLI 命令创建 VLAN 51 并分配 IP 地址 `10.1.51.2`：

```
(config) #vlan 51

(config) #interface vlan 51

(config-subif) #ip address 10.1.51.2 255.255.255.0
```

选择 **Configuration** ⇒ **NETWORK** ⇒ **IP** ⇒ **IP Interfaces** 进入菜单，在此您可以使用 WebUI 为 VLAN 分配 IP 地址。

以下 CLI 命令显示了控制器上配置的 VLAN 以及分配给它们的 IP 地址。

```
#show ip interface brief
```

| Interface | IP Address / IP Netmask | Admin | Protocol |
| :--- | :--- | :--- | :--- |
| `vlan 50` | `10.1.50.100 / 255.255.255.0` | up | up |
| `vlan 51` | `10.1.51.2 / 255.255.255.0` | up | down |
| `vlan 53` | `192.168.5.1 / 255.255.255.0` | up | down |
| `loopback` | `unassigned / unassigned` | up | up |

### 虚拟 AP 配置文件 (Virtual AP Profile)

此时，构建 VAP 配置文件所需的所有组件都已创建完毕：AAA 配置文件、SSID 配置文件和 VLAN。现在，我们只需要将这些组件组合起来创建 VAP 配置文件，如图 5-12 所示。

![](img/f0a787182fde585d5ed5e23c147a0298_148_0.png)

**图 5-12:** VAP 配置文件

除了为 VAP 配置文件分配 AAA 配置文件、SSID 配置文件和 VLAN 外，您可能还需要指定 AP 与控制器之间用户数据的转发模式。在第 2 章“理解 ArubaOS 环境”中，我解释了四种转发模式：隧道 (`tunnel`)、桥接 (`bridge`)、解隧道 (`decrypt-tunnel`) 和拆隧道 (`split-tunnel`)。默认且最常用的转发模式是隧道。以下 CLI 命令创建 VAP 配置文件并将 VLAN、AAA 配置文件、SSID 配置文件和转发模式分配给 VAP：
