
`$IPT -N OUT_ICMP`

```
for dip $PING; do
$IPT -A OUT_ICMP -p icmp --icmp-type echo-request -s $dip -d $ip -j ACCEPT
$IPT -A OUT_ICMP -p icmp --icmp-type echo-reply -s $dip -j ACCEPT
done
```

`$IPT -A OUT_ICMP -p icmp --icmp-type destination-unreachable -j ACCEPT`
`$IPT -A OUT_ICMP -p icmp --icmp-type source-quench -j ACCEPT`
`$IPT -A OUT_ICMP -p icmp --icmp-type fragmentation-needed -j ACCEPT`
`$IPT -A OUT_ICMP -p icmp --icmp-type parameter-problem -j ACCEPT`

# 第二部分：防火墙设计与实现

> IANA 已经开始分配之前预留的地址。如果你选择拦截保留网络，请监控你的防火墙日志，并准备解封已分配的保留网络。

图 9-7 显示了 `BADIP` 链，它检查源地址和目的地址并拦截未测试的数据包。该链被 `INPUT` 和 `OUTPUT` 链调用。`BADIP` 链

1. 检查错误的源地址，并通过将其发送到 `LBADIP` 链来丢弃并记录任何具有错误源地址的数据包。
2. 检查错误的目的地址，丢弃并记录任何具有错误目的地址的数据包。
3. 将任何剩余的数据包返回调用链以便进一步处理。

![](img/0f69b2a8749a24b957044e9f26f2d5b4_309_0.png)

列表 9-7 显示了与 `BADIP` 链相关的代码。链使用 shell 变量 `$BADIP` 来指定被认为坏的网络地址。包含以下网络地址：

- 广播地址
- `0.0.0.0/8`
- `255.255.255.255`

# 第 9 章：IPTables 防火墙实现

- 回环地址
- `127.0.0.0/8`
- 多播地址
- `224.0.0.0/4`
- `240.0.0.0/5`
- 预留地址
- `169.254.0.0/16`
- `192.0.0.0/24`
- `192.0.34.0/24`
- RFC 1918 地址
- `10.0.0.0/8`
- `172.16.0.0/12`
- `192.168.0.0/16`

你可以根据自己的喜好定制此列表。特别是，如果受保护的主机位于使用 RFC 1918 地址的网络上，你需要从坏 IP 地址列表中删除该地址。

## 9-7：BADIP 链

```
BADIP="0.0.0.0/8 10.0.0.0/8 169.254.0.0/16 \
172.16.0.0/12 192.0.0.0/24 192.168.0.0/16 192.0.34.0/24 \
224.0.0.0/4 240.0.0.0/5 255.255.255.255"
```

```
$IPT -N BADIP
for ip in $BADIP; do
$IPT -A BADIP -s $ip -j BADIP
$IPT -A BADIP -d $ip -j BADIP
done
```

## TCP 标志

某些 TCP 标志组合不会出现在正常的 TCP 数据报中。扫描器和其他敌意程序使用这些标志组合来确定目标运行的操作系统，探测目标的防火墙，并执行不需要的侦察。如图 9-8 所示，`FLAGS` 链丢弃具有无效 TCP 标志组合的数据报。该链测试特定的标志组合，并将任何匹配的数据报发送到 `FLAGS` 链，由对其进行记录并丢弃。

# 第二部分：防火墙设计与实现

![](img/0f69b2a8749a24b957044e9f26f2d5b4_311_0.png)

图 9-8：`FLAGS` 链

列表 9-8 显示了与 `FLAGS` 链相关的防火墙代码。注意只测试 TCP 数据报。通常你可以在不修改的情况下使用此链。但是，如果需要，可以对其修改以实现不同的策略。

### 列表 9-8：FLAGS 链

```
$IPT -N FLAGS
$IPT -A FLAGS -p tcp --tcp-flags ACK,FIN -j FIN
$IPT -A FLAGS -p tcp --tcp-flags ACK,RST -j PSH
$IPT -A FLAGS -p tcp --tcp-flags ACK,URG -j URG
$IPT -A FLAGS -p tcp --tcp-flags FIN,RST -j RST
$IPT -A FLAGS -p tcp --tcp-flags SYN,FIN -j FIN
$IPT -A FLAGS -p tcp --tcp-flags SYN,RST -j RST
$IPT -A FLAGS -p tcp --tcp-flags ALL -j ALL
$IPT -A FLAGS -p tcp --tcp-flags ALL -j NONE
$IPT -A FLAGS -p tcp --tcp-flags FIN,PSH,URG -j URG
$IPT -A FLAGS -p tcp --tcp-flags ALL SYN,FIN,URG -j FLAGS
$IPT -A FLAGS -p tcp --tcp-flags ALL SYN,RST,ACK,FIN,URG -j
```
剩余视为有效的标志组合。

## 敌意主机

有时，网络监控会发现与特定主机相关的敌意活动。在这种情况下，快速方便地拦截来自此类主机的流量是有用的。如图 9-9 所示的 `SHUN` 链提供了这种能力。该链的结构类似于 `BADIP` 链，其功能是在运行期间将主机添加到 `SHUN` 链并移除。在创建链时，主机也会添加到 `BADIP` 链，直到防火墙重新设计。

![](img/0f69b2a8749a24b957044e9f26f2d5b4_312_0.png)

### 9-9：SHUN 链

列表 9-9 显示了与 `SHUN` 链相关的代码。代码使用 shell 变量来保存屏蔽的主机 IP 地址。通常，此变量初始化为空值。要将主机添加到 `SHUN` 链，执行以下命令：

```
iptables -A SHUN -s address -j SHUN
```

`address` 是要屏蔽的主机或网络的 IP 地址。要从 `SHUN` 列表中移除主机，执行如下形式的命令：

```
iptables -D SHUN -s address -j SHUN
```

要进行大赦（移除所有主机），执行此命令：

```
iptables -F SHUN
```

### 列表 9-9：SHUN 链

```
$IPT -N SHUN
for ip in $SHUN; do
$IPT -A SHUN -s ip -j SHUN
$IPT -A SHUN -d ip -j SHUN
done
```

`shield.org` 维护一个活跃探测并攻击其他主机的列表。与其等待此类主机出现在你的网络监控中，你可能更倾向于使用 `SHUN` 链主动拦截它。

## FLOOD 链：防止洪攻击

如图 9-10 所示的 `FLOOD` 链保护主机不受 SYN 洪攻击。该链包含一条规则以限制速率触发（即匹配数据包）。如果数据包的速率超过指定的阈值，它们将被记录并丢弃。

![](img/0f69b2a8749a24b957044e9f26f2d5b4_313_0.png)

图 9-10：`FLOOD` 链

列表 9-10 显示了组成链的命令。阈值设置为允许接受十个 SYN 数据报。之后，直到规则充电，每秒接受不超过五个 SYN 数据报。多余的数据包传递给 `FLOOD` 链，对其记录并丢弃。

### 列表 9-10：FLOOD 链

```
SYNOPT="-m limit --limit 5/second --limit-burst 10"
$IPT -N FLOOD
# 后续规则以限制速率接受数据报
$IPT -A FLOOD $SYNOPT
```

主机接受 SYN 数据报的速率取决于主机的性能，模型中设置的突发限制和阈值速率可能适用于适用于主机。设置这些值的最佳方法是实验。然而，许多管理员不愿让主机暴露在 SYN 洪之下，即使是出于目的。在这种情况下，给定的值可能足够了。只需监控防火墙日志以确保数据报不被错误丢弃。如果你发现它们被错误丢弃，请增加突发限制、阈值速率或两者，直到不再被错误丢弃。

## 日志链

模型防火墙包含四个记录并丢弃发送到它们的特定类型包的链。此外，它还包括 `LDROP` 链，由于各种原因记录并丢弃包。列表 9-11 显示了这些链相关的代码。注意每个链包含一条规则，在初始十个包后将日志速率限制为每秒一个包。这些规则防止防火墙主机成为填充主机日志空间的拒绝服务攻击受害者。

### 列表 9-11：日志链

```
LOGOPT="--log-level 3 m limit --limit 1/second --limit-burst 10"
$IPT -N LDROP
$IPT -A LDROP -j LOG --log-prefix "IPT Drop: " $LOGOPT
```
