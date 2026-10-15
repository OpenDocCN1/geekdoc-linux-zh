
```
iptables -A FORWARD -m icmp -p icmp --sport echo-request -j LOG
```

此规则将统计所有的 `icmp` `echo-request` 数据包（`icmp 0`）。以下命令将发现所有已转发的 `icmp-reply` 数据包：

```
iptables -A FORWARD -m icmp -p icmp --sport echo-reply -j LOG
```

你不局限于 `ICMP` 数据包。例如，如果你想收集正在转发的 `HTTP` 数据包的信息，你需要输入：

```
iptables -A FORWARD -p tcp --sport 80,443 -j LOG
```

要确定两个网络之间通过的 `HTTP` 流量数量，你需要执行以下命令：

```
iptables -A FORWARD -s 192.168.1.0/24 -d 10.100.100.0/24 -p tcp --sport 80,443 -j LOG
```

![](img/a7a9caa80ec85507179284d91e216f9f_483_0.png)

## 列出和重置计数器

要列出计数器信息，你可以从终端执行以下任意命令：

```
ipchains -L -v
iptables -L -v
```

你可以使用 `ipchains-save` 和 `iptables-save` 命令保存这些信息。以下命令将重置计数器：

```
ipchains -L -Z
iptables -L -Z
```

## 在 Linux 路由器中设置服务类型

许多路由器（包括使用 `Ipchains` 或 `Iptables` 的 Linux 路由器）能够在流量通过时对其进行整形。所有数据包的 IP 头部都有一个特殊字段称为服务类型（`ToS`）字段，它允许你在流量通过路由器时对其进行优先级排序。使用 `ToS` 字段，你可以让某些类型的流量（例如 `SMTP` 和 `POP3`）优先于其他流量（例如 `SSH` 和 `Telnet`）。被标记的数据包在路由器处会被区别对待。`ToS` 字段位于网络层（OSI/RM 的第 3 层）。你可以通过咨询 `RFC 1349` 学习更多关于 `ToS` 工作原理的知识。

通常，配置防火墙时为数据包分配优先级是一个次要考虑的问题。但在某些情况下，你会发现防火墙可以“兼任”提供两种服务。在网络流量中设置 `ToS` 字段的主要原因是减少网络拥塞，特别是在流量巨大的网络中。

> 注意
>
> 不要将服务类型（`ToS`）与服务质量（`QoS`）混淆。`QoS` 指物理设备（如交换机、路由器）根据 IP 包中的 `ToS` 值传输数据包的能力。`QoS` 涉及数据包是否通过 Relay、异步传输模式（`ATM`）、以太网、同步光网络（`SONET`）等交付。由于 `ToS` 是指标记某些数据包使其比其他包具有更高的优先级，这些标记决定了它们是否可以用于 `QoS` 路由。

## 服务值

普通服务值为 0（在实际数据包中为 `0x00`）。表 9.7 列出了在标记数据包时可用的四种不同选项。

### 表 9.7 ToS 字段选项

| 服务值 | 描述 |
| --- | --- |
| 最小延迟 | 最小延迟字段减少了数据报从路由器传输到主机所需的时间。最小延迟选项对于在建立初始连接或传输控制数据时需要速度的协议是理想的。`ftp` 协议端口 (`20`)、`Telnet` 和 `SSH` 等流量将受益于此设置。标记此类流量将减少路由器的延迟（即请求与响应之间的时间间隔）。`ToS` 字段为 `10`（实际数据包中为 `0x10`）。 |
| 最大吞吐量 | 此值适用于 `ftp-data` 端口 (`20`) 以及通过文件传输进行的文件传输。此值适用于需要大量数据的协议。`ToS` 字段为 `08`（实际数据包中为 `0x08`）。 |
| 最大可靠性 | 此值确保数据包被可靠地交付。它对于数据包丢失关键的协议有用，例如 `TCP`。`ToS` 字段为 `02`（实际数据包中为 `0x02`）。 |
| 最小成本 | 此值用于沿最便宜路径路由流量。它对于成本是主要因素的协议有用。`ToS` 字段为 `04`（实际数据包中为 `0x04`）。 |

## iptables 中额外的 ToS 选项

正如你所料的，`iptables` 增加了一些选项并使用了一些不同的术语。首先，你可以设置路由器匹配具有 `ToS` 选项的数据包，或者让路由器设置实际的 `ToS` 选项。这两者是完全不同的。一种允许路由器处理具有 `ToS` 值的数据包

# 使用 Ipchains 和 Iptables 实现防火墙 • 第 9 章 487

前者已经设置，而后者实际上是设置值。要创建一个匹配 `ToS`（服务类型）字段的规则，您可以使用 `-m` 选项并配合其参数：

```
-m tos --tos tos_value -j TARGET
```

在前面的语法中，`tos_value` 是表 9.7 中找到的任何 `ToS` 位（例如，用于表示最大吞吐量的 `08`）。至于目标值，您可以指定任何所需的目标（`ACCEPT`、用户定义的链等）。例如，以下规则允许来自源端口 `80` 且 `ToS` 值设为 `08` 的入站流量：

```
iptables -A INPUT -p tcp -m tos 0x08 -j ACCEPT
```

关于设置 `ToS` 值的事宜，您只能在 `FORWARD` 和 `OUTPUT` 链中设置它们。语法如下：

```
-j TOS --set-tos tos_value
```

例如，要将所有传出的 Web 流量的 `ToS` 值设为最大吞吐量：

```
iptables -A OUTPUT -p tcp -m tcp --dport 80 -j TOS --set-tos 0x08
```

以下是使用 `Iptables` 为各种流量设置 `ToS` 字段的其他额外示例：

```
iptables -A OUTPUT -p tcp -m tcp --dport 21 -j TOS --set-tos 0x04
iptables -A OUTPUT -p tcp -m tcp --dport 20 -j TOS --set-tos 0x08
iptables -A OUTPUT -p tcp -m tcp --dport 22 -j TOS --set-tos 0x10
iptables -A OUTPUT -p tcp -m tcp --dport 25 -j TOS --set-tos 0x04
iptables -A OUTPUT -p tcp -m tcp --dport 53 -j TOS --set-tos 0x04
iptables -A OUTPUT -p tcp -m tcp --dport 80 -j TOS --set-tos 0x08
iptables -A OUTPUT -p tcp -m tcp --dport 110 -j TOS --set-tos 0x08
iptables -A OUTPUT -p tcp -m tcp --dport 143 -j TOS --set-tos 0x04
iptables -A OUTPUT -p tcp -m tcp --dport 443 -j TOS --set-tos 0x04
```

![](img/a7a9caa80ec85507179284d91e216f9f_487_0.png)

# 使用和获取自动化防火墙脚本及图形化防火墙实用程序

人们已经尝试将 Linux 中创建防火墙的过程自动化。同样，开发者们也在创建 GUI 应用来让这项工作变得更简单。这些工具中许多非常有用，尽管它们主要在启动防火墙配置方面有效；您可能需要对这些应用程序生成的规则进行自定义。

更有效的防火墙脚本和 GUI 工具包括以下这些：

- **Firestarter**：一个相当复杂的图形化工具，同时支持 `Ipchains` 和 `Iptables`。它可以创建个人防火墙，也支持多网卡系统。与许多自动化防火墙一样，它创建多条规则来过滤已知和预期的攻击。您可能需要调整其中的一些自动设置。尽管 `Firestarter` 支持多个接口，但与大多数开源 GUI 应用一样，它最适合作为多网卡系统防火墙的起点。您可以在 http://sourceforge.net/projects/firestarter 获取 `Firestarter`。

- **Mason**：这是一个独特的产品，`Mason` 设计的目的是首先对通过防火墙的流量进行第一线处理，然后生成 `Ipchains` 或 `ipfwadn`（`ipchains` 和 `Iptables` 的前身）规则。在本书期间，`Mason` 不支持 `Iptables`。尽管如此，`Mason` 的规则创建方法既独特又合理，因为它尝试根据你通过防火墙的网络流量流量来创建规则。您可以在 http://users.dhp.com/~whisper/mason 下载此二进制文件。请勿将此产品与为 Apache 服务器动态生成 HTML 的 HTML Mason 实用程序混淆。

- **Knetfiler**：一个为 KDE 桌面环境设计的 GUI 防火墙。尽管它声称稳定，但在与当前 KDE 版本配合时似乎存在问题。您可以在 http://expansa.sns.it:8080/knetfiler 了解更多关于 `Knetfiler` 的信息。
