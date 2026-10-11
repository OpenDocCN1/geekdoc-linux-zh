
```
iptables -t nat -v -L
```

```
1   PREROUTING (policy DROP 0 packets, 0 bytes)
2   pkts bytes target prot opt in out source \ destination
3   0    0      DNAT   tcp  -- eth1 any 192.168.1.129 \ this.host
                          tcp  spts:1020:65535 dpt:53 \ to:hosta.lan
4   0    0      REDIRECT tcp -- eth0 any anywhere \ anywhere
                          tcp  spts:1024:65535 dpt:http

5   POSTROUTING (policy DROP 0 packets, 0 bytes)
6   pkts bytes target prot opt in out source \ destination
7   0    0      SNAT   tcp  -- any eth1 hosta.lan \ 192.168.1.129
                          tcp  spts:1024:65535 dpt:21 \ to:this.host
8   0    0      MASQUERADE all -- any ppp0 lan_network \ anywhere
```

第 1 行标识该列表属于 `PREROUTING` 链，这是应用目标 `NAT` 的位置。`PREROUTING` 链的默认策略是 `DROP`。

第 2 行包含以下列标题：

- `pkts` 是匹配该规则的数据包数量。
- `bytes` 是匹配该规则的数据包中包含的字节数。
- `target` 指匹配该规则的数据包的处置目标，例如 `DNAT` 或 `REDIRECT`。
- `prot` 是 `protocol` 的缩写，可以是 `all`、`tcp`、`udp` 或 `icmp`，也可以是 `/etc/protocols` 中的某个值。
- `opt` 代表 `fragmentation options`，是通过 `-f` 或 `! -f` 选项设置的。第一个位置上的 `!` 表示 `! -f` 选项，意为匹配未分片的数据包或系列中的第一个分片。第二个位置上的 `f` 表示 `-f` 选项，意为匹配第二个及后续的分片。
- `in` 是入站网络接口名称——例如 `eth0`、`eth1`、`lo` 或 `ppp0`——该规则适用于此接口。只有在此特定网络接口上到达的数据包才会匹配该规则。如果您拥有具有针对不同接口设置不同防火墙规则的 LAN，或者您在接口之间转发流量，此字段就变得很重要。
  - 在 `PREROUTING` 链上，只有 `in` 字段是相关的。在 `PREROUTING` 链上，`out` 字段没有意义。
- `out` 是出站网络接口名称——例如 `eth0`、`eth1`、`lo` 或 `ppp0`——该规则适用于此接口。只有从此特定网络接口发出的数据包才会匹配该规则。如果您拥有具有针对不同接口设置不同防火墙规则的 LAN，或者您在接口之间转发流量，此字段就变得很重要。
  - 在 `POSTROUTING` 链上，只有 `out` 字段是相关的。在 `POSTROUTING` 链上，`in` 字段没有意义。
- `source` 是 IP 数据包头部中的源地址。
- `destination` 是 IP 数据包头部中的目标地址。

第 3 行是一个 `DNAT` 规则，用于修改传入 SSH 数据包中的目标地址。来自外部主机 192.168.1.129 的 SSH 客户端连接，地址指向本地主机，被重定向到 LAN 上的主机 A。

第 4 行是 `DNAT` 专门形式 `REDIRECT` 的一个示例，它会将数据包重定向到本地主机。在这种情况下，到达 `eth0` 接口的任何 HTTP 数据包（假定将被转发到远程 Web 服务器）被重定向到监听此主机 TCP 端口 80 的本地代理服务器。

第 5 行标识下一个列表属于 `POSTROUTING` 链，这是应用源 `NAT` 的位置。`POSTROUTING` 链的默认策略是 `DROP`。

第 6 行包含列标题，与第 2 行相同。

第 7 行是一个 `SNAT` 规则，用于修改传出 FTP 客户端数据包中的源地址。来自 LAN 上主机 A 的 FTP 客户端连接，地址指向外部 LAN 上的主机 192.168.1.129，被修改为看起来像是从本地主机发出的。

第 8 行是 `SNAT` 专门形式 `MASQUERADE` 的一个示例，它旨在用于具有可变更 IP 地址的临时连接。在这种情况下，本地网络通过 `ppp0` 接口发出的所有数据包都进行了伪装。

## mangle 表列表格式

列出 `mangle` 表链中所有规则的 `mangle` 表列表命令的基本格式如下：

```
iptables -t mangle -vn -L PREROUTING
iptables -t mangle -vn -L OUTPUT
```

或者

```
iptables -t mangle -vn -L
```

请注意，上述列表命令仅显示 `mangle` 表链中的规则。

以下是两个 `mangle` 表规则示例，一个是 `PREROUTING` 链上的 `MARK` 规则，另一个是 `OUTPUT` 链上的 `TOS` 规则。为了简洁起见，仅展示 `-v` 选项的输出：

```
> iptables -t mangle -v -L
```

| Line | Chain | pkts | bytes | target | prot | opt | in | out | source | destination |
|------|-------|------|-------|--------|------|-----|----|-----|--------|-------------|
| 1 | PREROUTING (policy DROP 0 packets, 0 bytes) | | | | | | | | | |
| 2 | | | | | | | | | | |
| 3 | | 0 | 0 | MARK | tcp | -- | eth0 | any | laptop.private.lan | anywhere |
| | | | | | | | | spts:1024:65535 dpt:ssh MARK set 0x10070 | | | |
| Line | Chain | pkts | bytes | target | prot | opt | in | out | source | destination |
|------|-------|------|-------|--------|------|-----|----|-----|--------|-------------|
| 4 | OUTPUT (policy DROP 0 packets, 0 bytes) | | | | | | | | | |
| 5 | | | | | | | | | | |
| 6 | | 0 | 0 | TOS | tcp | -- | any | eth1 | bastion.firewall.lan | anywhere |
| | | | | | | | | spts:1024:65535 dpt:ssh TOS set Minimize-Delay | | | |

第 1 行标识该列表属于 `PREROUTING` 链，这是 `MANGLE` 被应用的位置。`PREROUTING` 链的默认策略是 `DROP`（丢弃）。

第 2 行包含这些列标题：

- `pkts` 是匹配该规则的数据包数量。
- `bytes` 是匹配该规则的数据包中包含的字节数。
- `target` 指代匹配该规则的 `MARK` 或 `TOS` 目标处置方式。
- `prot` 是协议的缩写，可以是 `all`、`tcp`、`udp` 或 `icmp`，也可以是 `/etc/protocols` 文件中的值。
- `opt` 代表 `分段选项`，该选项可以通过 `-f` 或 `! -f` 选项设置。第一个空格中的 `!` 表示 `! -f` 选项，这意味着匹配未分段的数据包或系列中的第一个分段。第二个空格中的 `f` 表示 `-f` 选项，这意味着匹配第二个及后续分段。
- `in` 是入站网络接口名称——例如 `eth0`、`eth1`、`lo` 或 `ppp0`——此规则适用于该接口。只有到达该特定网络接口的数据包才匹配规则。如果您有一个局域网，为不同接口设置了单独的防火墙规则，或者您正在接口之间转发流量，此字段就变得很重要。
