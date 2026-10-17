
如果下一个已知，但其邻居的物理地址尚未确定，则 `output` 将指向 `neigh_resolve_output`。该函数检查邻居缓存项的状态以确保它是可达的（reachable）。NUD 状态位于邻居缓存的 `nud_state` 中。这些状态用于判断是否有需要解析目的地址。NUD 状态被邻居发现协议 (NDP) [RFC 2641] 使用，并列于表 6.4 中。

一旦地址解析完成，邻居缓存中的 `hh` 字段将更新为指向硬件报头缓存项，该项包含实际的链路层报头。邻居缓存中的 `output` 字段将指向 `hh_output`。

*（注：原文此处似乎存在部分逻辑重复或乱码片段，译文已根据上下文进行了平滑处理，确保技术术语的准确性。）*

| 表 6.5: IPv4 配置项 |
| 名称 | 数值 | 目的 |
|---|---|---|
| `NET_IPV4_CONF_ARPFILTER` | 13 | 配置 ARP 过滤。ARP 过滤可防止多个接口响应 ARP 请求。 |
| `NET_IPV4_CONF_MEDIUM_ID` | 14 | 此配置项未在核心 TCP/IP 协议栈中使用。 |
| `NET_IPV4_CONF_NOFRM` | 15 | 在 Linux 转换器 (XFRM) 中跳过路由策略检查。 |
| `NET_IPV4_CONF_NOPOLY` | 16 | 此配置项作为默认值开启目标缓存中的 DST_NPOLICY 标志。它会跳过 XFRM 策略检查。 |

[表 6.5](#) 显示了在 `linux/include/linux/sysctl.h` 文件中定义的配置项。这些变量之前与 `ipv4_deconstruct` 结构相关。每个变量可以通过 `sysctl` 和 `ioctl` 设置。在 `linux/include/linux/sysctl.h` 文件中还定义了一组名称相似的 2.0 版本兼容变量。

与 `in_device` 结构相关的若干实用函数在 IP 协议及其他地方广泛使用。这些函数中最重要的是从分配给设备的地址列表中选择目标地址。该函数是 `inet_select_address`。

```c
u32 inet_select_addr(const struct net_device *dev, u32 dst, int scope);
```

`Dev` 指向网络接口设备，`dst` 是与缺少源地址的数据包相关的目标地址。我们希望找到源地址，并将其放入通过参数 `dst` 向目标地址发送的数据包中。参数 `dst` 设置为 `RT_SCOPE_LINK` 或 `RT_SCOPE_UNIVERSE`。`scope` 的完整值集见[第 9 章](#)。

# 6.10 安全、可堆叠性目标与 XFRM

多年来，IPsec 一直是首选的安全机制。TCP/IP 的安全特性首次规范于 20 世纪 90 年代中期。IP 安全架构（统称为 IPSec）在 20 世纪 90 年代后期进行了修订 [RFC 2401]。修订内容包含了身份验证头 (AH) [RFC 2402]、封装安全载荷 (ESP) [RFC 2406] 以及用于密钥管理的 Internet 密钥交换协议 (IKE) [RFC 2409]。本书将不会深入探讨网络安全理论，但我们将探索用于支持 IPSec 的一些内部结构。它还支持安全关联 (SAs) 概念。SA 可以被看作是连接。SA 的管理涉及一个三元组，由安全参数索引 (SPI)、目标地址和安全协议（可以是 ESP 或 SH）组成。对于某些类型的 SA，IP 流量通过 IP 隧道，其中外层 IP 头指定了 IPSec 信息，内层头则是“真实”的 IP 头。Linux 支持第 2 own `PF_KEY` 密钥管理 API [RFC 2367]。`PF_KEY` 类型族定义在 `include/linux/pfkey2.h` 文件中。

为了支持这些安全特性，Linux 提供了安全策略数据库 (SPD)，其中包含实现安全策略的规则。它还提供了安全关联数据库 (SAD) 来管理安全连接。本章前面提到的目标缓存用于为数据包分配目标，目标可以是外部机器或内部数据包处理程序。从 Linux 2.6 开始，有一种名为转换器 (XFRM) 的机制，它根据安全策略转换目标缓存条目。xfrm 实现的核心由由结构化 `xfrm_policy` 实现的策略规则组成。此外，它通过 `include/net/xfrm.h` 文件中的 `xfrm_state` 结构定义了转换器。SPD 转换按优先级排序的 `xfrm_policy` 实例列表实现的规则。转换器允许 `dst_entry` 结构累积在包（bundle）中。此外，`dst_entry` 结构有一个新字段 `xfrm_state`，它指向一个 `xfrm_state` 实例。

当协议通过调用在 `include/net/dst.h` 中定义的 `xfrm_lookup` 在 SPD 中查找时，访问 SPD。

```c
int xfrm_lookup(struct dst_entry **dst_ptr, struct flock *fl, struct sock *sk, int flags);
```
