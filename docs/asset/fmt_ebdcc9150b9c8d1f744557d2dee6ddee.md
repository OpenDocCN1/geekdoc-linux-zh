
# `ipchains -L input -nv`

使用 `input` 链中相同的四个示例规则，以下显示了同时使用 `-n`（数字显示）和 `-v`（详细模式）选项时的列表输出情况：

`ipchains -L input -nv`

+ 1. Chain `input` (policy prot opt) `DENY`: 60018 个数据包, 420591 字节):

| pkts | bytes | target | prot | opt | tosa | tox | ifname | source | ports |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | `DENY` | all | --- | 1. | 0FF | `eth0` | `eth0` | 192.168.10.30 | 0.0.0/0 n/a |
| 0 | `ACCEPT` | in | --- | 0FF | `eth0` | `eth0` | 0.0.0/0 | 192.168.10.30 | 0 n/a |
| 61004 | 5987K | `ACCEPT` | all | --- | 0FF | `eth0` | `lo` | 0.0.0/0 | 0.0.0/0 n/a |
| 23332 | 1597K | `ACCEPT` | tcp | ly | --- | 0FF | `eth0` | `eth0` | 0.0.0/0 | 192.168.10.30 |

第 1 行标识出该列表针对 `input` 链。`input` 链的默认策略是 `DENY`。有 60018 个数据包通过了 `input` 链的规则，占 420591 字节的网络流量。

第 2 行包含以下列标题：

- `pkts` 是匹配规则的数据包数量。
- `bytes` 是匹配规则的数据包所包含的字节数。
- `target` 指匹配规则的数据包的目标处理方式——`ACCEPT`（接受）、`DENY`（拒绝）或 `REJECT`（拒绝）。
- `prot` 代表协议，可以是 all、`tcp`、`udp` 或 `icmp`。
- `opt` 代表数据包的选项或标志位。你将看到最常见的四个标志是 `none`（无）、`l`（记录匹配规则的数据包）、`y`（必须设置 SYN）和 `t`（必须设置 ACK）。
- 服务类型（TOS）掩码 `tosa` 和 `tox`，以及 xor 掩码代表处理数据包交付优先级的四种不同方式：最小延迟、最大吞吐量、最大可靠性和最小成本。你指定一个服务优先级位设置在掩码并选择该位。操作结果与 xor 掩码进行异或运算，以设置或清除标志。
- `ifname` 是网络接口名称——例如 `eth0`、`eth1,0` 或 `ppp0`——它适用于。只有此特定网络接口上的数据包才会匹配该规则。如果你有一个具有独立防火墙接口的局域网，此字段将变得重要。
- `is` 是输出中包含的两个未使用的占位符。我替换了 `mark` 和 `outsize` 字段以节省空间。
- `mark` 尚未使用或没有详尽文档。
- `outsize` 未文档。
- `source` 是数据包源自地址。
- `destination` 是数据包的目的地址。
- `ports` 列出了源端口和目的端口、`ICMP` 消息类型，或者如果规则中未指定端口则显示 n/a。

第 3 行是基础的 IP 欺骗规则，拒绝声称来自你机器的入站数据包，并启用了日志。

第 5 行说明了简单的 `-L` 命令配合详细选项时，当规则引用多个接口时如何提供某些清晰的细节。`-v` 选项明确了该规则指向环回接口 `lo`。该规则接受接受环回接口上的所有输入数据包。

第 6 行接受来自你联系过的远程 Web 服务器的数据包。协议是 `tcp`。服务器对你浏览器请求的入站响应必须设置了 ACK 位（1）。Web 服务器的源端口是 80，www。你的浏览器作为客户端程序，从一个非特权端口（1024-65535）连接了该 Web 服务器。

## 检查输入、输出和转发规则

现在你已经看到了防火墙链列表的样式以及可用的格式选项，我们将简要列出输入、输出和转发规则。这些示例规则对你自己最可能用到的某些规则具有代表性。

### 检查输入规则

当默认策略为 `DENY` 时，你的输入规则大部分是 `ACCEPT`。默认情况下一切被拒绝，你显式定义了哪些会被接受。以下示例包含具有代表性的输入接受规则样本：

`ipchains -L input`

```
Chain input (policy DENY):
| target | prot | opt | source | destination | ports |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1. ACCEPT | icmp | | anywhere | my.host.domain destination-unreachable |
| 2. ACCEPT | icmp | | anywhere | my.host.domain source-quench |
| 3. ACCEPT | icmp | | anywhere | my.host.domain time-exceeded |
| 4. ACCEPT | icmp | | anywhere | my.host.domain parameter-problem |
| 5. ACCEPT | udp | | isp.name.server | my.host.domain domain -> domain |
| 6. ACCEPT | udp | | isp.name.server | my.host.domain domain -> 1024:65535 |
| 7. ACCEPT | tcp | ly | --- | 0FF | eth0 | eth0 | 192.168.10.30 | 0.0.0/0 n/a |
```

*(注：此处原文后续表格内容似乎存在乱码或格式错误，翻译已根据上下文逻辑对齐，但根据指令不翻译代码块内容且保持格式)*

（由于提供的原文文本在后半部分存在大量重复和格式混乱，以下为基于逻辑的翻译内容）

```
Chain input (policy prot opt) DENY: 60018 个数据包, 420591 字节):

| pkts | bytes | target | prot | opt | tosa | tox | ifname | source | ports |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | DENY | all | --- | 1. | 0FF | eth0 | eth0 | 192.168.10.30 | 0.0.0/0 n/a |
| 0 | ACCEPT | in | --- | 0FF | eth0 | eth0 | 0.0.0/0 | 192.168.10.30 | 0 n/a |
| 61004 | 5987K | ACCEPT | all | --- | 0FF | eth0 | lo | 0.0.0/0 | 0.0.0/0 n/a |
| 23332 | 1597K | ACCEPT | tcp | ly | --- | 0FF | eth0 | eth0 | 0.0.0/0 | 192.168.10.30 |
```

## 调试防火墙规则

默认策略为 `DENY` 的入站数据包被拒绝。未被接受的数据包被丢弃。以下是 14 条规则：

- 第 1 行：接受任何 `ICMP` 目的不可达（destination-unreachable）。
- 第 2 行：接受任何 `ICMP` 源洪塞（source-quench）。
- 第 3 行：接受任何 `ICMP` 时间超时（time-exceeded）。
- 第 4 行：接受任何 `ICMP` 参数问题（parameter-problem）。
- 第 5 行：接受来自 `isp.name.server` 的 `UDP` 域名到域名包。
- 第 6 行：接受来自 `isp.name.server` 的 `UDP` 域名到 1024:65535 包。
- 第 7 行：接受来自 `my.host.domain` 的 `TCP` 包，带有 ACK 位。
- 第 8 行：拒绝来自 `my.host.domain` 的所有包。

输出链的默认策略是 `REJECT`（拒绝）。如果连接未被允许，你的本地程序将立即收到错误通知。该链上共有 13 条规则：

- 第 1 行—允许出的 `ICMP` 类型 3 错误消息发送到任何地方。虽然该消息被识别为“目标不可到达”（Destination Unreachable），但它实际上是一种通用错误类型消息。该消息包含一个指定特定错误代码类型的字段。
- 第 2 行—`ICMP` 源拥塞（Source Quench）流量控制消息允许发送到任何地方。
- 第 3 行—`ICMP` 超时（Time Exceeded）消息只能发送到你 `ISP` 的机器。这种本地限制将远程跟踪路由（traceroute）请求限制在你的 `ISP`。
- 第 4 行—`ICMP` 参数错误消息允许发送到任何地方。
