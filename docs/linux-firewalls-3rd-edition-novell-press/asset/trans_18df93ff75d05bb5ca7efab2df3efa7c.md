
## 表 3.12

**multiport 匹配扩展**

| | 选项 | 描述 |
|---|---|---|
| | --match **multiport** | |
| | --source-port <端口> [,<端口>] | 指定源端口。 |
| | --destination-port <端口> [,<端口>] | 指定目的端口。 |
| | --port <端口> [,<端口>] | 源端口和目的端口相等，且它们匹配列表中的某个端口。 |

**multiport** 语法可能有些棘手。这里包含了一些示例和注意事项。以下规则阻止经由接口 **eth0** 到达的、目标为与 NetBIOS 和 **SMB** 相关的 UDP 端口的传入数据包。这些是 Microsoft Windows 计算机上常见的端口，也是蠕虫病毒的攻击目标：

```bash
iptables -A INPUT -i eth0 -p udp\
-m multiport --destination-port 135,136,137,138,139 -j DROP
```

下一条规则阻止通过 **eth0** 接口发送到与 TCP 服务 NFS、**socks** 和 **squid** 相关的高端口的出站连接请求：

```bash
iptables -A OUTPUT -o eth0 -p tcp\
-m multiport --destination-port 2049,1080,3128 --syn -j REJECT
```

在这个示例中，需要注意的是 **multiport** 命令必须紧跟在协议规范之后。如果在 -p tcp 和 -m multiport 之间放置了 --**syn**，就会造成语法错误。

为了展示 --syn 放置位置的类似示例，以下写法是正确的：

```bash
iptables -A INPUT -i <interface> -p tcp \
-m multiport --source-port 80,443 ! --syn -j ACCEPT
```

然而，这种写法会导致语法错误：

```bash
iptables -A INPUT -i <interface> -p tcp ! --syn \
-m multiport --source-port 80,443 -j ACCEPT
```

此外，源参数和目的参数的位置并不直观。以下两种变体是正确的：

```bash
iptables -A INPUT -i <interface> -p tcp -m multiport \
--source-port 80,443 \
! --syn -d $IPADDR --dport 1024:65535 -j ACCEPT
```

以及

```bash
iptables -A INPUT -i <interface> -p tcp -m multiport \
--source-port 80,443 \
-d $IPADDR ! --syn --dport 1024:65535 -j ACCEPT
```

然而，这种写法会导致语法错误：

```bash
iptables -A INPUT -i <interface> -p tcp -m multiport \
--source-port 80,443 \
-d $IPADDR --dport 1024:65535 ! --syn -j ACCEPT
```

该模块有一些出人意料的语法副作用。如果移除对上述两条正确规则中 **SYN** 标志的引用，它们都会产生语法错误：

```bash
iptables -A INPUT -i <interface> -p tcp -m multiport \
--source-port 80,443 \
-d $IPADDR --dport 1024:65535 -j ACCEPT
```

然而，以下规则对就不会：

```bash
iptables -A OUTPUT -o <interface> \
-p tcp -m multiport --destination-port 80,443 \
! --syn -s $IPADDR --sport 1024:65535 -j ACCEPT

iptables -A OUTPUT -o <interface> \
-p tcp -m multiport --destination-port 80,443 \
! --syn -s $IPADDR --sport 1024:65535 -j ACCEPT
```

请注意，**multiport** 模块中的 **--destination-port** 参数与执行 **-p tcp** 参数匹配的模块中的 **--destination-port** 或 **--dport** 参数不同。

## limit 过滤器表匹配扩展

速率限制匹配对于抑制在大量记录数据包期间生成的日志消息数量非常有用。

表 3.13 列出了 **limit** 匹配扩展可用的选项。

### 表 3.13

*limit 匹配扩展*

| 选项 | 描述 |
| :--- | :--- |
| --limit <速率> | 在给定时间范围内要匹配的最大数据包数 |
| --limit-burst <数量> | 在应用限制之前要匹配的最大初始数据包数 |

突发速率定义了要接受的初始匹配次数。默认值为五次匹配。当达到限制时，进一步的匹配受到速率限制。默认限制为每小时三次匹配。可选的时间段指定符包括 /second、/minute、/hour 和 /day。

换句话说，默认情况下，如果在时间限制内达到五次匹配的初始突发速率，那么在接下来的一个小时内，最多再有三个数据包匹配，每 20 分钟一次，无论接收到多少数据包。如果在速率限制内没有发生匹配，突发计数将重新充一次电。

用示例演示速率限制匹配比用文字描述更容易。以下规则将在给定秒内接收到初始五个 echo-request 时，限制传入 ping 消息匹配的日志记录频率为每秒一次：

```bash
iptables -A INPUT -i eth0 \
-p icmp --icmp-type echo-request \
-m limit --limit 1/second -j LOG
```

也可以进行速率限制的接受。以下两条规则结合使用时，将在给定秒内接收到初始五个 echo-request 时，限制接受传入 ping 消息的频率为每秒一次：

```bash
iptables -A INPUT -i eth0 \
-p icmp --icmp-type echo-request \
-m limit --limit 1/second -j ACCEPT
iptables -A INPUT -i eth0 \
-p icmp --icmp-type echo-request -j DROP
```

下一条规则限制了针对被丢弃的 ICMP 重定向消息生成的日志消息数量。如果在 20 分钟的时间范围内已记录初始五条消息，那么在接下来的一个小时内，最多将再生成三条日志消息，每 20 分钟一条：

```bash
iptables -A INPUT -i eth0 \
-p icmp --icmp-type redirect \
-m limit -j LOG
```

最后一个示例的假设是，默认情况下以及任何未匹配的重定向数据包都会被 INPUT 链的默认 DROP 策略静默丢弃。

## dstlimit 过滤器表匹配扩展

dstlimit 匹配扩展支持基于目的地的速率限制，无论是按 IP 地址还是按端口。请注意 dstlimit 匹配扩展和 limit 匹配扩展之间的区别，后者针对特定类型的数据包只有一个限制。

表 3.14 列出了 dstlimit 匹配扩展的选项。

### 表 3.14

*dstlimit 匹配扩展*

| 选项 | 定义 |
| :--- | :--- |
| `--dstlimit <平均值>` | 每秒最大平均匹配速率。 |
| `--dstlimit-mode <模式>` | 定义限制是按 IP (*dstip*)、按 IP 和端口元组 (*dstip-dstport*)、按源 IP 和目的 IP 元组 (*srcip-dstip*)，还是按源 IP、目的 IP 和目的端口元组 (*srcipdstip-dstport*)。 |
| `--dstlimit-name <名称>` | 指定放置在 `/proc/net/ipt_dstlimit/` 中的文件的名称。 |
| `[--dstlimit-burst <burst>]` | 指定作为突发接收的数据包应匹配的数量。默认为 5。 |
| `[--dstlimit-htable-size <大小>]` | 定义哈希表中的桶数量。 |
| `[--dstlimit-htable-max <条目>]` | 定义哈希表中条目数量的限制。 |
| `[--dstlimit-htable-gcinterval <间隔>]` | 定义清理哈希表之间的时间长度。`<间隔>` 的值以毫秒为单位，默认为 1000 ms。 |
| `[--dstlimit-htable-expire <时间>]` | 定义空闲条目从哈希表中清除前的时间量。该值以毫秒为单位，默认为 10000 ms。 |

## state 过滤器表匹配扩展

静态过滤器仅从单个数据包的角度查看流量。每个数据包特定的源和目的地址及端口组合、传输协议以及当前的 TCP 状态标志组合，都是在没有参考任何正在进行上下文的情况下进行检查的。ICMP 消息被视为不相关的、带外的 IP 层 3 事件。

state 扩展提供了额外的监控和记录技术，以增强无状态的静态包过滤技术。当 TCP 连接或 UDP 交换开始时，会记录状态信息。后续的数据包不仅基于静态元组信息进行检查，还基于正在进行的交换上下文进行检查。换句话说，通常与上层 TCP 传输层或 UDP 应用层相关的某些上下文知识被带到了过滤器层。

