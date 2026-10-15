
<wday>*</wday>

<who>root</who>

<command>/usr/bin/nice -n20 adjkerntz -a</command>

</item>

```

将 `bridgecheck.sh` 作为 cron 条目。添加以下内容将每分钟运行一次脚本：

```xml
<item>
<minute>*</minute>
<hour>*</hour>
<mdday>*</mdday>
<month>*</month>
<wday>*</wday>
<who>root</who>
<command>/usr/bin/bridgecheck.sh</command>
</item>
```

## 9.5.2.3.3. 启动时禁用桥接

你需要在配置中添加一条命令，在启动时关闭桥接：

```xml
<shellcmd>/sbin/ifconfig bridge0 down</shellcmd>
```

## 9.5.2.3.4. devd 钩子

此方案在 pfSense 2.3 或更高版本中可行，它涉及使用 `devd` 捕捉发生的 CARP 状态转换。在备用和主设备上编辑 `/etc/devd.conf`，并添加这些行：

```
notify 100 {
	match "system" "IFNET";
	match "type" "LINK_UP";
	action "/usr/local/bin/carpup";
};

notify 100 {
	match "system" "IFNET";
	match "type" "LINK_DOWN";
	action "/usr/local/bin/carpdown";
};
```

然后创建两个文件：`/usr/local/bin/carpup`

```bash
#!/bin/sh
/sbin/ifconfig bridge0 up
```

以及：`/usr/local/bin/carpdown`

```bash
#!/bin/sh
/sbin/ifconfig bridge0 down
```

## 9.5.3. 多 WAN 口

桥接在本质上在许多场景下与多 WAN 口配置是不兼容的。当使用桥接时，通常是 pfSense 以外的设备作为桥接接口上主机的默认网关，而该路由器是唯一能够引导这些主机流量的设备。这并不会阻止你在同一防火墙上对其他未桥接的接口使用多 WAN 口，并让 pfSense 作为它们的默认网关。如果你将多个内部接口桥接在一起，并且 pfSense 是你桥接接口上主机的默认网关，那么你就可以像使用非桥接接口一样使用多 WAN 口。

# 第 10 章 虚拟局域网 (VLANs)

VLAN 提供了一种将单个交换机划分成多个广播域的方法，允许单台交换机充当多个交换机使用。这通常用于网络分段，其使用方式与使用多个交换机相同，即根据交换机上的配置将主机放置在特定的网段上。在交换机之间采用汇干时，同一交换机上的设备并不实际上位于同一个交换机上。本章将涵盖 VLAN 的概念、术语和配置。

## 10.1. 要求

部署 VLAN 需要满足以下两个均都必要的条件：

1.  **支持 802.1Q VLAN 的交换机** —— 2000 年左右以后制造的每个合格交换机都支持 802.1Q VLAN 汇干。你无法在无管理交换机上使用 VLAN。
2.  **支持 VLAN 标记的网络适配器** —— 你需要一个支持硬件 VLAN 标记或长帧的网卡。由于每个帧的头部都添加了 4 字节的 802.1Q 标记，帧的大小可达 1522 字节。之所以需要支持硬件 VLAN 标记或长帧的网卡，是因为其他适配器无法处理大于正常 1500 MTU 以太网上限 1518 字节的帧。这会导致大帧被丢弃，从而引发性能问题和连接稳定性问题。

> 仅仅适配器列出支持长帧，并不保证你网卡的特定芯片组实现能够良好支持长帧。Realtek 的 `rl(4)` 网卡是最大的“重灾区”。许多网卡可以工作但不能良好支持长帧，而有些完全不接受 802.1Q 标记帧。如果你在使用长帧支持列表中的某个网卡时遇到问题，建议尝试具有 VLAN 硬件标记支持的接口。我们尚未发现 VLAN 硬件支持列表中的网卡出现过类似问题。

支持 VLAN 硬件标记的以太接口：

```
bce(4), bge(4), cxgb(4), em(4), ixgb(4), msk(4), nge(4), re(4), stge(4), ti(4), txp(4), vge(4).
```

支持长帧的以太接口：

```
bfe(4), dc(4), fxp(4), gem(4), hme(4), le(4), nfe(4), nve(4), rl(4), sis(4), sk(4), ste(4), tl(4), tx(4), vr(4), xl(4)
```

## 10.2. 术语

本节涵盖了成功部署 VLAN 所需要理解的术语。

### 10.2.1. 汇干 (Trunking)

汇干是指在同一交换机端口上携带多个 VLAN 的方法。离开汇干端口的帧被标记有 802.1Q 标记，使连接的设备能够区分多个 VLAN。汇干端口用于连接多个交换机，并用于连接任何支持 802.1Q 标记且需要访问多个 VLAN 的设备。这通常仅限于提供 VLAN 之间连通性的路由器（在本例中为 pfSense），以及连接到包含多个 VLAN 的其他交换机的连接。

### 10.2.2. VLAN ID

每个 VLAN 都有一个关联的 ID（标识符），用于识别带标记流量。这是一个介于 1 到 4094 之间的数字。交换机上的默认 VLAN 是 VLAN 1，在部署 VLAN 汇干时不应使用该 VLAN。这将在第 10.3 节“VLAN 与安全”中进一步讨论。除了避免使用 VLAN 1 之外，你可以自行选择要使用的 VLAN 数字。从 VLAN 2 开始逐一加 1，直到达到所需的 VLAN 数量。另一种常见做法是使用 VLAN IP 子网的第三个字节作为 VLAN ID。例如，如果你使用 `10.0.10.0/24`、`10.0.20.0/24` 和 `10.0.30.0/24`，那么逻辑上分别使用 VLAN 10、20 和 30。选择一个符合你逻辑的 VLAN 分配方案。

### 10.2.3. 父接口 (Parent interface)

父接口指的是 VLAN 所在的物理接口，例如 `em0` 或 `bge0`。当在 pfSense 或 FreeBSD 上配置 VLAN 时，每个 VLAN 被分配一个虚拟接口，从 `vlan0` 开始，每配置一个额外的 VLAN 增加 1。在 pfSense 1.2.x 中，VLAN 接口的数量与 VLAN ID 之间没有关联。你不应该将父接口分配给 pfSense 上的任何接口 —— 它的唯一功能是作为定义 VLAN 的父接口。在某些情况下这样做可行，但会导致交换机配置出现困难，导致使用强制门户时出现问题，并迫使你使用汇干端口的默认 VLAN，正如第 10.3 节进一步讨论的那样，应该避免这样做。

### 10.2.4. 接入端口 (Access Port)

接入端口指的是为单个 VLAN 提供服务的交换机端口，其帧不带 802.1Q 标记。你将位于单个 VLAN 上的设备连接到接入端口。你的大多数交换机端口将配置为接入端口。接入端口上的设备无法感知网络中的任何 VLAN。它们会像往常一样看到每个 VLAN。

### 10.2.5. 双重标记 (Double tagging / QinQ)

也可以进行双重标记，但 pfSense 不支持。在许多环境中，DMZ 区域也是通过第三台交换机单独处理的。

### 10.2.6. 私有 VLAN (Private VLAN / PVLAN)

PVLAN 指的是单个 VLAN，其中你使用这些。通常最好是将内部流量与你的数据流量隔离。这并不直接与 VLAN 有关。

## 10.3. VLAN 与安全

VLAN 本身并不安全，但配置错误可能会导致你的。过去也出现过安全问题。

### 10.3.1. 隔离信任区域

由于存在配置错误的可能性，你应该隔离不同的级别。至少，你应该使用两台交换机，一台用于防火墙，一台用于内部。

### 10.3.2. 使用默认 VLAN

VLAN1 是默认（或“原生”） VLAN，它可能会以意想不到的方式被。这类似于在防火墙规则中使用默认允许策略而不是默认拒绝。始终最好使用不同的 VLAN，并确保只在交换机上选择你需要的端口。

### 10.3.3. 使用汇干端口的默认 VLAN

当 VLAN 标记流量通过原生 VLAN 在汇干端口上发送时，匹配原生 VLAN 的数据包标记可能会被移除以保持与旧网络的兼容性。更糟糕，双重标记为原生 VLAN 和另一个 VLAN 的数据包在这样汇干传输时只会移除原生 VLAN 标记，并在稍后处理，该流量可能会进入不同的 VLAN。这被称为“VLAN 跳跃”。

如前节所述，干道端口上的未标记流量将被假设为原生 VLAN，这可能与已分配的 VLAN 接口重叠。取决于交换机处理此类流量的方式以及 pfSense 如何看到它，直接使用接口可能会在同一个 VLAN 上产生两个接口。

### 10.3.4. 限制干道端口的访问

由于干道端口可以与干道交换机组中的任何 VLAN 通信（取决于您的交换机配置，某些 VLAN 可能不存在于当前交换机上），因此在物理上保护干道端口至关重要。同时，确保没有被配置为干道的端口处于未插拔状态，防止有人无意或蓄意地接入。根据您的交换机类型，它可能支持干道的动态协商。您应该确保此功能已禁用或受到适当限制。

### 10.3.5. 交换机的其他问题

有报告显示，基于 VLAN 的交换机在负载过高时，或者当一个 VLAN 的 PC MAC 地址在另一个 VLAN 上出现时，会发生 VLAN 流量泄露。这些问题通常出现在固件过时的旧款交换机或质量极差的交换机上。这类问题在许多年前安全问题频发时已得到很大程度上解决。无论您使用什么品牌的交换机，请研究一下它是否通过了某种形式的安全测试，并确保您正在使用最新的固件。虽然这些问题是交换机而非 pfSense 的，但它们也是您整体安全的一部分。

这里的许多内容针对特定品牌和型号的交换机。您使用的交换机可能有不同的特定安全考量。请参阅其文档获取有关 VLAN 安全的建议。

## 10.4. pfSense 配置

本节介绍 pfSense 侧的 VLAN 配置。

## 10.4.1. 控制台 VLAN 配置

您可以在控制台通过使用“分配接口”功能配置 VLAN。以下示例显示了如何配置 ID 为 10 和 20 的两个 VLAN，并将 `le2` 作为父接口。VLAN 接口分配为 OPT1 和 OPT2。

```
pfSense console setup
***************************
0) 退出 (仅限 SSH)
1) 分配接口
2) 设置 LAN IP 地址
3) 重置 webConfigurator 密码
4) 恢复出厂默认设置
5) 重启系统
6) 停止系统
7) Ping 宿主机
8) Shell
9) PFtop
10) 过滤日志
11) pfSense 开发者 Shell
12) 从控制台升级
13) 禁用 Secure Shell (sshd)
98) 将配置文件移动到移动设备

输入选项: 1

有效的接口为：
| le0 | 00:0c:29:d6:e7:dc | (up) |
| le1 | 00:0c:29:d6:e7:e6 | (up) |
| le2 | 00:0c:29:d6:e7:f0 | (up) |
| plip0 | 0 | |

您想先设置 VLAN 吗？
如果您不打算使用 VLAN，或者仅将其用于可选接口，应在此处输入 no，并在以后需要时使用 webConfigurator 配置 VLAN

您现在要设置 VLAN 吗 [y|n]? y

支持 VLAN 的接口：
| le0 | 00:0c:29:d6:e7:dc | (up) |
| le1 | 00:0c:29:d6:e7:e6 | (up) |
| le2 | 00:0c:29:d6:e7:f0 | (up) |

输入新 VLAN 的父接口名称（完成后可留空）：
输入 VLAN 标签 (1-4094): 10

支持 VLAN 的接口：
le0 00:0c:29:d6:e7:dc (up)
le1 00:0c:29:d6:e7:e6 (up)
le2 00:0c:29:d6:e7:f0 (up)

输入新 VLAN 的父接口名称（完成后可留空）：
输入 VLAN 标签 (1-4094): 20

支持 VLAN 的接口：
le0 00:0c:29:d6:e7:dc (up)
le1 00:0c:29:d6:e7:e6 (up)
le2 00:0c:29:d6:e7:f0 (up)

输入新 VLAN 的父接口名称（完成后可留空）：

VLAN 接口：
vlan0 VLAN tag 10, interface le2
vlan1 VLAN tag 20, interface le2

如果您不知道接口的名称，可以选择自动检测。在这种情况下，请在按下 'a' 启动自动检测之前断开所有接口。

输入 LAN 接口名称或输入 'a' 进行自动检测：le1
输入 WAN 接口名称或输入 'a' 进行自动检测：le0
输入可选接口 1 的名称或输入 'a' 进行自动检测（完成后可留空）：vlan0
输入可选接口 2 的名称或输入 'a' 进行自动检测（完成后可留空）：vlan1
输入可选接口 3 的名称或输入 'a' 进行自动检测（完成后可留空）：<enter>

接口将分配如下：
LAN -> le1
WAN -> le0
OPT1 -> vlan0
OPT2 -> vlan1
```

## 10.5. 交换机配置

本节介绍交换机侧的 VLAN 配置。

### 10.5.1. 通用交换机配置步骤

1.  **创建 VLAN** — 在交换机上创建所需的 VLAN。
2.  **配置干道端口** — 将 pfSense 连接的端口配置为干道端口，在该接口上对所有 VLAN 进行打标。
3.  **配置访问端口** — 将内部主机将使用的端口配置为所需 VLAN 的访问端口，即不打标签 VLAN。
4.  **配置端口 VLAN ID (PVID)** — 某些交换机需要为端口配置 PVID。这指定了进入该交换机端口的流量使用哪个 VLAN。对于某些交换机，这是一个一步完成的过程，通过将该端口配置为特定 VLAN 的访问端口，它会自动为进入该端口的流量打上标签。其他交换机则要求你在两个地方进行配置。如果本章中没有详细说明，请查阅您的交换机文档。

### 10.5.2. 基于 Cisco IOS 的交换机

在带有 IOS 的 Cisco 交换机上配置和使用 VLAN 是相当简单的过程，只需几条命令即可创建和使用 VLAN、干道端口以及将端口分配给 VLAN。其他厂商的许多交换机行为与 IOS 类似，使用的配置语法几乎相同，甚至完全一致。

#### 10.5.2.1. 创建 VLAN

VLAN 可以独立方式创建，也可以使用 VLAN 干道协议 (VTP) 创建。使用 VTP 可能会更方便，因为它会自动将 VLAN 配置传播到 VTP 域上的所有交换机，尽管它也可能产生安全问题，并可能导致无意中擦除您的 VLAN 配置。使用 VTP，如果您决定需要另一个 VLAN，只需在单个交换机上添加，然后组中的所有其他交换机都可以将端口分配给该 VLAN。如果独立配置 VLAN，您必须手动将它们添加到每个交换机中。请参考 Cisco 关于 VTP 的文档，以确保您的配置是安全的，不易被意外破坏。在只有少数几个交换机且 VLAN 不频繁更改的网络中，通常最好不要使用 VTP 以避免其潜在的缺陷。

##### 10.5.2.1.1. 独立 VLAN

创建独立 VLAN：

```
sw# vlan database
sw(vlan)# vlan 10 name "DMZ Servers"
sw(vlan)# vlan 20 name "Phones"
sw(vlan)# exit
```

##### 10.5.2.1.2. VTP VLAN

要为交换机设置 VTP 和 VLAN，请在主交换机创建一个 VTP 数据库，然后创建两个 VLAN：

```
sw# vlan database
sw(vlan)# vtp server
sw(vlan)# vtp domain example.com
sw(vlan)# vtp password SuperSecret
sw(vlan)# vlan 10 name "DMZ Servers"
sw(vlan)# vlan 20 name "Phones"
sw(vlan)# exit
```

#### 10.5.2.2. 配置干道端口

对于 pfSense，交换机端口不需要处于干道模式，但必须使用 802.1q 打标。可以这样操作：

```
sw# configure terminal
sw(config)# interface Ethernet 0/24
sw(config-if)# switchport mode trunk
sw(config-if)# switchport trunk encapsulation dot1q
```

> **注意**
>
> 在某些较新的 Cisco IOS 交换机上，Cisco 私有的 ISL VLAN 封装方法已弃用且不再支持。如果您的交换机不允许配置 `encapsulation dot1q`，则它仅支持 802.1Q，您无需指定封装方式。

#### 10.5.2.3. 将端口添加到 VLAN

要将端口添加到这些 VLAN，您需要进行如下进行分配：

```
sw# configure terminal
sw(config)# interface Ethernet 0/12
sw(config-if)# switchport mode access
sw(config-if)# switchport access vlan 10
```
