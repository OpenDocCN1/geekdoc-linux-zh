
`ip tcp_metrics` 用于操作内核中保留 IPv4 和 IPv6 目的地 TCP 信息的条目。这些条目在 TCP 套接等待共享目的地信息时创建，并以目的地址为键存储在缓存中。保存的信息可能包括指标值（最初从路由获取）、用于 TIME-WAIT 回收的近期 TSVAL、用于快速打开（Fast Open）功能的状态。为了性能考虑，缓存增长不能超过配置的限制，旧条目会被新信息替换，有时会被回收并用于新的目的地。内核从不移除条目，只能通过此工具进行刷新。

## `ip tcp_metrics show` - 显示缓存条目

`address PREFIX` (默认值)

IPv4/IPv6 前缀或地址。如果没有提供前缀，则显示所有条目。

输出可能包含以下信息：

`age <S.MAM>sec` - 条目创建、重置或使用套接字指标更新以后的时间。如果指标在过去一小时内未更新，则在使用路由指标时会重置并刷新条目。并非所有缓存值在更新时都会重置 `age`。

`cwd <N>` - CWND 指标值。

`fo_cookie <HEX-STRING>` - SYN-ACK 中的 Cookie 值，用于快速打开的下一个 SYN。

`fo_mss <N>` - SYN-ACK 中的的 MSS 值，用于快速打开的下一个 SYN。

`fo_syn_drops <N>/<S.MAM>sec ago` - 通过接收 SYN 重传后的 SYN-ACK 检测到的初始带数据的快速打开 SYN 的丢弃次数。秒数为上次 SYN 丢弃后的时间，结合丢弃计数可禁用一段时间快速打开。

`reordering <N>` - 重排序指标值。

`ttt <N>us` - RTT 指标值。

`tttvar <N>us` - RTTVAR 指标值。

`ssthresh <SSTHRESH>` - SSTHRESH 指标值。

`tw_ts <TSVAL>/<SEC>sec ago` - 近期 TSVAL 以及保存到 TIME-WAIT 套接字后的秒数。

## `ip tcp_metrics delete` - 删除单个条目

`address ADDRESS` (默认值)

IPv4/IPv6 地址。地址是必需参数。

## `ip tcp_metrics flush` -

此命令刷新符合某些标准的条目。

此命令的参数与 `show` 相同。

## 示例

`ip tcp_metrics show address 192.168.0.0/24`

显示来自子网的目的地条目。

`ip tcp_metrics show 192.168.0.0/24`

`ip tcp_metrics delete 192.168.0.0/24`

`ip tcp_metrics show address 192.168.0.0/24`

（此处省略重复的示例...）

`ttl` 与此选项不兼容：具有固定 `ttl` 的隧道始终会 `pmtu` 发现。

## `key K`

`ikey K`

`okey K`

( 仅 GRE 隧道 ) 使用带有密钥 `K` 的加密 GRE 隧道。`K` 可以是一个数字或类似于 IP 地址的点分四位值。`key` 参数设置双方向均使用的密钥。`ikey` 和 `okey` 参数为输入和输出设置不同的密钥。

## `csum`, `icsum`, `ocsum`

( 仅 GRE 隧道 ) 为封装内的数据包生成/要求校验和。`ocsum` 标志为传出的数据包计算校验和。`icsum` 标志要求所有输入数据包必须具有正确的校验和。`csum` 标志等同于 `icsum` 和 `osum` 的组合。

## `seq`, `isseq`, `oseq`

( 仅 GRE 隧道 ) 对数据包进行序列化。`oseq` 标志启用传出数据包的排序。`isseq` 标志要求所有输入数据包序列化。`seq` 标志等同于 `isseq` 和 `oseq` 的组合。无效。请勿使用。

## `encaplim ELIM`

( 仅 IPv6 隧道 ) 设置固定的封装限制。默认值为 4。

## `flowlabel FLOWABEL`

( 仅 IPv6 隧道 ) 设置固定的流标签。

## `ip tunnel prl potential router list` (ISATAP 仅)

## `dev NAME`

强制性设备名称。

## `prl-default ADDR`

`prl-nodefault ADDR`

`pr-delete ADDR`

添加或删除 `ADDR` 作为潜在路由器或默认路由器。

## `ip tunnel show list tunnels` 此命令没有参数。

## 另阅

`ip(8)`

## 作者

原始 Man页由 Michail Litvak <mci@owl.openwall.com>

# IP-XFRM

### 名称

`ip-xfrm` - 转换配置

## 摘要

```
ip [ OPTIONS ] xfrm { COMMAND | help }
ip xfrm-OBJECT { COMMAND | help }
```

`XFRM-OBJECT := state | policy | monitor`
