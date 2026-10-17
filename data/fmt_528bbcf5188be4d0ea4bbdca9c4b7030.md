
对于每个估计器（无论是绝对模式还是相对模式），计算估计器确定的流速率与静态值之间的差。如果流速率高于指定的 PPS，则使用 0 代替负值。`“max(0, rateest_bps)”`。

> [!]—`rateest-lt`

如果速率小于指定的速率/估计器，则匹配。

> [!]—`rateest-gt`

如果速率大于指定的速率/估计器，则匹配。

> [!]—`rateest-eq`

如果速率等于指定的速率/估计器，则匹配。在所谓的“绝对模式”中，使用一个估计器并对比静态值；而在“相对模式”中，比较两个估计器。

- —`rateest` 名称

绝对模式的估计器名称。

- —`rateest1`

—`rateest2`

相对模式的两个估计器名称。

`rateest-bps` [值]

`rateest-pps` [值]

`rateest-bps1` [值]

`rateest-bps2` [值]

`rateest-ps1` [值]

`rateest-ps2` [值]

通过字节或每秒比较估计器(s)，并与选择的值比较。查看上方列表在什么情况下使用选项。后缀可以是：`[gt]bit, [gt]bit, [gt]ps`。

示例：这是根据连接开始时的可用带宽路由来自服务器的连接：

## Estimate outgoing rates 估计输出速率

```
iptables -t mangle -A POSTROUTING -o eth0 -j RATE --rateest-name eth0 --rateest-interval 250ms --rateest-ewma 0.5s
iptables -t mangle -A POSTROUTING -o ppp0 -j RATE --rateest-name ppp0 --rateest-interval 250ms --rateest-ewma 0.5s
```

## Mark based on available bandwidth 基于可用带宽标记

```
iptables -t mangle -A balance -m conrack -ctstate NEW -m helper -m rateest --rateest-delta eth0 --rateest-bps1 2bit --rateest-gt ppp0 --rateest-bps2 2bit -j CONNMARK --set-mark 1
iptables -t mangle -A balance -m conrack -ctstate NEW -m helper -m rateest --rateest-delta ppp0 --rateest-bps1 2bit --rateest-gt eth0 --rateest-bps2 2bit -j CONNMARK --set-mark 2
iptables -t mangle -A balance -j CONNMARK --restore
```

## realm 区域（IPv4 特定）

匹配路由区域。路由区域用于涉及 BGP 等动态协议的复杂路由设置。

> [!]—`realm` 数字（可选掩码）。如果不是数字，值可以是 `/etc/route2/rt_realms` 中的命名区域（情况下不能使用掩码）。匹配 `/etc/route2/rt_realms` 中的给定区域（情况下不能使用掩码）。

## recent 最近

允许你动态创建 IP 地址列表，然后以几种方式匹配该列表。例如，你可以为尝试连接到防火墙 139 端口的人创建一个“坏人”列表，并在不考虑它们的情况下丢弃所有后续数据包。

—`set`、—`check`、update 和 —`remove` 是互斥的。

- —`name` 名称

指定命令使用的列表。如果没有给出名称，将使用 DEFAULT。

- [!]—`set`

将数据包的源地址添加到列表中。如果源地址已经在列表中，则更新更新现有条目。这将始终返回成功（或传递失败 !）。

- —`source`

匹配/保存最近列表表中每个数据包的源地址。这是默认值。

- —`rdest`

匹配/保存最近列表表中每个数据包地址。

- —`mask` 掩码

应用于此最近列表的网络掩码。

- [!]—`rcheck`

检查数据包的源地址当前在列表中。

- [!]—`update`

类似于—`rcheck`，如果匹配，将更新“最后看到”时间戳。

- [!]—`remove`

检查数据包的源地址当前在列表中，如果是，则将该地址从列表中移除且规则返回 true。如果未找到地址，则返回 false。

- —`seconds` 秒数

此选项必须与 —`rcheck` 或 —`update` 之一一起使用。当使用时，这将匹配缩小为仅当地址在列表中并在最后指定的秒数内被看到时发生。

- —`reap`

此选项只能与 —`seconds` 配合使用。当使用时，这将清除早于最后指定的秒数的条目。

- —`hitcount` 次

此选项必须与 —`rcheck` 或 —`update` 之一一起使用。当使用时，这将匹配缩小为仅当地址在列表中且收到的数据包大于或等于该值时发生。此选项可以配合 —`seconds` 使用，创建一个在特定时间内需要特定次数的更窄的匹配。`hitcount` 参数的最大值由 `xt_recent` 内核模块的“`ip_pkt_list_to`”参数给出。超过此值的命令行将导致路由被拒绝。

- —`rtl`

此选项可能只能与 —`rcheck` 或 —`update` 之一一起使用。当使用时，这将匹配缩小为仅当地址在列表中且当前数据包的 TTL 与命中 —`set` 规则的数据包的 TTL 匹配时发生。

如果你在使用此模块通过发送伪造数据包到你的网站来阻止他人访问时，遇到了 DoS 伪造源地址的问题，那么这可能有所帮助。

示例：

```
iptables -A FORWARD -m recent --name badguy --rcheck --seconds 60 -j DROP
iptables -A FORWARD -p tcp --i eth0 --dport 139 -m recent --name badguy --set -j DROP
```

`/proc/net/xt_recent/*` 是当前地址列表以及每个列表中每个条目的信息。

可以读取 `/proc/net/xt_recent/` 下的每个文件来查看当前列表，或使用以下命令进行写入以修改列表：

```
echo +addr > /proc/net/xt_recent/DEFAULT
将 addr 添加到 DEFAULT 列表中
echo -addr > /proc/net/xt_recent/DEFAULT
从 DEFAULT 列表中移除 addr
echo / > /proc/net/xt_recent/DEFAULT
清空 DEFAULT 列表（移除所有条目）。
```

该模块本身接受参数，默认值如所示：

- `ip_list_tot=100`

每个表记录的地址数量。

- `ip_pkt_list_tot=20`

每个地址记录的数据包数量。

- `ip_list_hash_size=0`

哈希表大小。0 表示根据 `ip_list_tot` 计算，默认值：512。

- `ip_list_perms=0644`

`/proc/net/xt_recent/*` 文件的权限。

- `ip_list_uid=0`

`/proc/net/xt_recent/*` 文件的所有者数值 UID。

- `ip_list_gid=0`

`/proc/net/xt_recent/*` 文件的所有者数值 GID。

# rpfilter

对数据包执行反路径过滤测试。如果对数据包的回复通过数据包到达的接口发送，则该数据包将匹配。注意，与内核中的 `rp_filter` 不同，受 IPsec 的数据包不会被特殊处理。如果你需要，可以将此匹配与策略匹配结合。此外，通过环回接口到达的数据包始终是允许的。此匹配只能在 raw 或 mangle 表的 PREROUTING 链中使用。

- -`loose`

用于指定即使选定的输出设备不是预期的设备，反路径过滤测试也应匹配。

以及在执行反路径路由查找时数据包的 `nfmark` 值。

- -`accept-local`

这将允许来自网络且源地址分配给本地机器的数据包通过检查。

- -`invert`

这将反转匹配的含义。不再匹配通过反路径过滤测试的数据包，而是匹配测试失败的数据包。

记录并丢弃反路径过滤测试失败包的示例：

```
iptables -t raw -N RPFILTER
iptables -t raw -A RPFILTER -m rpfilter -j RETURN
iptables -t raw -A RPFILTER -m limit --limit 10/minute -j nflog --nlog-prefix "rpfilter drop"
iptables -t raw -A RPFILTER -j DROP
iptables -t raw -A PREROUTING -j RPFILTER
```

不记录日志直接丢弃失败包的示例：

```
iptables -t raw -A RPFILTER -m rpfilter --invert -j DROP
```

# rt (IPv6 专用)

匹配 IPv6 路由头部

- [!] --`rt-type` type

匹配类型（数值）。

- [!] --`rt-segleft` num[:num]

匹配“剩余段”字段（范围）。

- [!] --`rt-len` length

匹配该头部的长度。

- --`rt-0-res`

也匹配预留字段（type=0）

- --`rt-0-adds` addr[,addr...]

匹配 type=0 的地址（列表）。

- --`rt-0-strict`

type=0 的地址列表为严格匹配。

# sctp

- [!] --`source-port,--sport[::port]`

源端口

- [!] --`destination-port,--dport[::port]`

目的端口

- [!] --`chunk-types` {all|any|only} chunktype[:flags]

大写标记表示在已设置时匹配，小写表示在未设置时匹配。

块类型：DATA INIT INIT_ACK SACK HEARTBEAT HEARTBEAT_ACK ABORT SHDOWN SHDOWN_ERROR COOKIE ECHOCHO COOKIE_ACK ECN SHDOWN_COMPLETE ASCONF ASCONF_ACK CWR FORWARD_TS SHDOWN_COMPLETE

（小写表示“关闭”，大写表示“开启”）

示例：

```
iptables -A INPUT -p sctp --dport 80 -j DROP
iptables -A INPUT -p sctp --chunk-types any -j DROP
iptables -A INPUT -p sctp --chunk-types any -j ACCEPT
```

此模块匹配由 `ipset()` 定义的 IP 集

- [!] --`match-set` setname[,flag]...

其中 flags 是逗号分隔的 src 或 dst 指定，最多可以六个。因此，命令 `iptables -A FORWARD -m set --match-set src,dst` 会匹配在指定的集中可以找到（例如 ipmap））源地址和目的端口对的数据包。

- --`nomatch`

如果指定了 --`nomatch` 且集支持 nomatch 标记，则匹配反转：标记为 nomatch true 的元素，匹配返回 false。

- --`update-counters`

如果 --`update-counters` 标记被反转，则集中匹配元素的数据包计数和字节计数不会更新。默认更新数据包计数。

- --`update-subcounters`

如果 --`update-subcounters` 标记被反转，则集中匹配元素的数据包计数和字节计数不会更新。默认更新数据包计数。

- [!] --`packets-eq` value

如果数据包匹配集中的元素，仅当数据包计数等于给定值时匹配。

- --`packets-lt` value

如果数据包匹配集中的元素，仅当数据包计数小于给定值时匹配。

- --`packets-gt` value

如果数据包匹配集中的元素，仅当数据包计数大于给定值时匹配。

- --`bytes-eq` value

如果数据包匹配集中的元素，仅当字节计数等于给定值时匹配。

- --`bytes-lt` value

如果数据包匹配集中的元素，仅当字节计数小于给定值时匹配。

- --`bytes-gt` value

如果数据包匹配集中的元素，仅当字节计数大于给定值时匹配。

当定义集时不带计数器时，数据包和字节计数相关的选项将被忽略。使用 -m set 需要 iptset 支持，标准内核从 Linux 2.6.9 起提供。

# socket

如果通过对数据包进行 socket 查找可以找到的 TCP/UDP socket，则匹配。如果存在已建立的监听 socket（带有本地地址）。查找使用嵌入 ICMP 错误中的 TCP/UDP 头部元组执行。

- --`transparent`

忽略非透明 socket。

- --`wildcard`

不忽略绑定到“any”地址的 socket。socket 匹配默认接受零绑定监听，因为本地服务可能会拦截流量。此选项用于匹配转发到本地的流量。在使用 socket 匹配实现对非本地地址完全透明时，建议使用 --`transparent`。

示例（假设标记 1 的数据包被递送）：

```
iptables -t mangle -A PREROUTING -m socket --transparent -j MARK --set-1
```

# state

“state”扩展是“conntrack”模块的子集。“state”允许访问此数据包的连接状态。

- --`state` state

逗号分隔的要匹配连接状态列表。仅识别“conntrack”理解的部分状态：INVALID、ESTABLISHED、NEW、RELATED 或 UNTRACKED。有关它们的描述，请参见此手册中的“conntrack”章节。

# statistic

此模块根据某些统计条件匹配数据包。它支持通过 --`mode` 选项设置两种不同模式。

支持的选项：

- --`mode` mode

设置匹配规则的匹配模式，支持的模式为 random（随机）和 nth（第n）。

- [!] --`probability` p

设置数据包随机匹配的概率。它仅在 random 模式下有效。p 必须在 0.0 到 1.0 之间。支持的粒度为 1/2147483648 增量。

- [!] --`every` n

每 n 个数据包匹配一个。它仅对 nth 模式有效（见 --`packet` 选项）。

- --`packet` p

为 nth 模式设置初始计数（0 <= p <= n-1,默认为 0）。

# string

此模块通过某些匹配策略匹配字符串。它要求 linux 内核 >= 2.6.14。

- --`algo` {bmkmp}

选择匹配策略。（bm = Boyer-Moore, kmp = Knuth-Pratt-Morris）

- --`from` offset

设置查找任何匹配的偏移量。如果没有传递，默认为 0。

- --`to` offset

设置扫描到哪个偏移量。即 offset-1（从 0 开始计数）是最后一个扫描的。如果没有传递，默认为数据包大小。

- [!] --`string` pattern

匹配给定的模式。

- [!] --`hex-string` pattern

匹配十六进制表示的给定模式。

示例：

# 字符串模式可用于简单的文本字符。`iptables -A INPUT -p tcp --dport 80 -m string --algo --string ‘GET/index.html’ -j LOG`

# 十六进制模式可用于不可打印字符，如 |0D 0A| 或 |0D0A|, `iptables -p udp --dport 53 -m string --algo --from 40 --to 57 --hex-string ‘[03]www[09]netfilter[03]org[00]’`

当指定了 `protocol tcp` 时，可以使用这些扩展。它提供了以下选项：

- --`source-port,--port[:port]` 源端口范围指定。这可以是服务名，也可以是端口号。可以指定包含范围，默认为 "0"；如果省略了最后一个，则认为 "65535"。如果省略了第一个端口，且第一个端口大于第二个端口，则将交换它们。`--port` 参数是该选项的方便别名。

- --`destination-port,--dport port[:port]` 目的端口范围指定。`--dport` 参数是该选项的方便别名。

- --`tcp-flags mask` 当 TCP 标志符合指定时进行匹配。第一个参数 `mask` 是我们需要检查的标志，而 `argument` 是必须设置的标志的逗号分隔列表。标志有：ACK FIN RST URGSH ALL NONE -A FORWARD。例如 -p tcp-flags SYN, ACK, FIN, RST 将仅匹配设置了 SYN 标志且未设置 ACK, RST 标志的数据包。

- --`syn` 仅匹配带有 SYN 位且清除了 ACK、RST 和 FIN 位的 TCP 数据包。此类数据包用于请求建立 TCP 连接；例如，阻塞进入接口的此类包将阻止入站 TCP 连接，而不会影响传出的 TCP 连接。它等同于 `tcp-flags SYN,RST,ACK,FIN SYN`。如果 "!" 标志位于 `--syn` 之前，该选项会被取反。

- --`tcp-option number` 如果设置了选项则进行匹配。

## tcpmss

此匹配 TCP 头部中的 MSS（最大段大小）字段。你仅可以在 TCP SYN 或 SYN/ACK 包上使用此项，因为 MSS 仅在连接启动时的 TCP 握手期间协商 [:value]。

- --`mss value[:value]` 匹配给定的 TCP MSS 值或范围。

## time
