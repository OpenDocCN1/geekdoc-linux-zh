
```bash
iptables -N IPOPOTS
iptables -A INPUT -m ipv4options --ssrr -m recent \
--set -j IPOPOTS
iptables -A INPUT -m ipv4options --lsrr -m recent \
--set -j IPOPOTS
iptables -A INPUT -m ipv4options --rr -m recent \
--set -j IPOPOTS
iptables -A IPOPOTS -j LOG --log-prefix \
"BAD IPOPOTS --SHUN " \
--log-tcp-sequence \
--log-tcp-options --log-ip-options -m limit \
--limit 1/second
iptables -A IPOPOTS -j DROP
```

## 小数据包及处理它们的规则

此规则集检查 UDP、TCP 和 ICMP 数据包的长度。小于指定长度的数据包将会被丢弃。在这里这样做是安全的，并且不会导致分片产生任何问题，因为真实的 IP 分片在在我们进入这些规则之前就已经处理过了。

## 第 7 章 使用 IPTABLES

这些规则用于丢弃刻意破坏的数据包，这些包被用于许多恶意目的（DoS 攻击等）。

```bash
iptables -N SMALL
iptables -A INPUT -p udp -m length --length 0:27 \
-m recent --set -j SMALL
iptables -A INPUT -p tcp -m length --length 0:39 \
-m recent --set -j SMALL
iptables -A INPUT -p icmp -m length --length 0:27 \
-m recent --set -j SMALL
iptables -A INPUT -p 30 -m length --length 0:31 \
-m recent --set -j SMALL
iptables -A INPUT -p 47 -m length --length 0:39 \
-m recent --set -j SMALL
iptables -A INPUT -p 50 -m length --length 0:49 \
-m recent --set -j SMALL
iptables -A INPUT -p 51 -m length --length 0:35 \
-m recent --set -j SMALL
iptables -A INPUT -m length --length 0:19 -m recent \
--set -j SMALL
iptables -A SMALL -m limit --limit 1/sec -j LOG \
--log-level info --log-prefix "SMALL - SHUN " \
--log-tcp-sequence --log-tcp-options \
--log-ip-options
iptables -A SMALL -j DROP
```

## 使用字符串模块检测数据包中的数据的规则

接下来的规则需要 patch-o-matic 提供的字符串匹配模块。它专门用于匹配包含已知滥用模式的系统字符串。例如，第一条规则查找 22 端口上包含“Version_Mapper”字符串的连接，这是一个用于枚举服务的工具。第二条规则应用于 OUTPUT 链。这防止防火墙自身发送匹配这些规则的数据包。注意，这些规则也适用于 FORWARD 链，即处理通过防火墙的流量。字符串匹配在处理非常特定的滥用模式（例如网络蠕虫和病毒）时特别有用。

```bash
iptables -N STRINGS
iptables -A INPUT -p tcp --dport 22 -m string \
--string "Version_Mapper" -j STRINGS
iptables -A FORWARD -p tcp --dport 22 -m string \
--string "Version_Mapper" -j STRINGS
iptables -A INPUT -p tcp --dport 22 -m string \
--string "/bin/sh" -j STRINGS
iptables -A INPUT -p tcp --dport 443 -m string \
--string "TERMextern" -j STRINGS
iptables -A INPUT -p tcp --dport 53 -m string \
--string "i.a" -j --log-prefix SID303
iptables -A FORWARD -p tcp --dport 53 -m string \
--string "i.a" -j --log-prefix SID303
```

将用户定义的字符串转换为该协议的实际数据结构和格式。

## 无效数据包及丢弃它们的规则

与数据包的内容一样，我们可能会因为其头部而丢弃数据包，因为它不匹配已知的连接状态、其校验和不匹配，或者存在其他错误问题。`iptables` 为我们提供了帮助解决这些问题的工具：`INVALID` 状态和 `unclean` 模块。前面的章节描述了 `INVALID` 状态定义不符合 `NEW`、`RELATED` 或 `ESTABLISHED` 状态的数据包。`unclean` 模块被认为是实验性的，已从早期 2.6 内核中移除，用于检测具有错误头部选项和其他问题（如错误的端口）的数据包。我们目前不建议你使用该模块。

```bash
iptables -N BOGUS
iptables -t filter -A INPUT -m conntrack \
--ctstate INVALID -j BOGUS
iptables -t filter -A OUTPUT -m conntrack \
--ctstate INVALID -j BOGUS
iptables -t filter -A FORWARD -m conntrack \
--ctstate INVALID -j BOGUS
iptables -A BOGUS -m limit --limit 1/second -j LOG \
--log-level info --log-prefix "INVALID PACKET \" \
-- DROP " --log-tcp-sequence --log-tcp-options \
--log-ip-options
```

```bash
iptables -A BOGUS -j DROP
```

如果你想尝试 `unclean` 模块，这里有一种将其添加到规则集中的简单方法。记住，`iptables` 是线性的，所以如果你想让 `unclean` 模块检查你所有的数据包，你需要将此链放在你可能拥有的任何 `ACCEPT` 规则之前。

```bash
iptables -N DIRTY
iptables -A INPUT -m unclean -j DIRTY
iptables -A OUTPUT -m unclean -j DIRTY
iptables -A FORWARD -m unclean -j DIRTY
iptables -A DIRTY -m limit --limit 1/second -j LOG \
--log-level info --log-prefix "CLEAN PACKET \" \
-- DROP " --log-tcp-sequence --log-tcp-options \
--log-ip-options
iptables -A DIRTY -j DROP
```

## 关于分片的简述

在 2.4 和 2.6 内核中，只要你使用连接跟踪引擎或进行 NAT，分片重组就是自动完成的。因此，通常不需要担心通过你防火墙的分片。然而，我们都会犯错，防火墙在启动时可能没有正确地编译连接跟踪引擎，甚至没有加载。因此，我们喜欢包含一个分片完整性检查规则集，以丢弃任何尝试通过防火墙的分片。如所述，如果你正在使用连接跟踪，此规则不应被触发，因为状态引擎将自动处理分片重组。

如下列出的规则除非发生极其严重的错误，否则永远不会被触发，这就是为什么如果你忘记加载 `conntrack` 模块或破坏了你的 NAT 规则，将它们保留在规则中可能是用的。底线是，如果你在进行 NAT 或两者兼顾，添加这些规则对你没有坏；在最坏的情况下，它只会有帮助。记住，在安全方面，我们并不感兴趣安全技术是如何工作的；我们感兴趣的是它是如何失效的。我们想要捕捉并阻止系统中的故障，而不是假设它们不会发生。
