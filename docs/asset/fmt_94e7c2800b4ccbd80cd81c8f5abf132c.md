
其中：

- `type` 是规则类型：`pass`（通过）、`log`（记录）或 `alert`（警报）。
- `protocol` 是协议：`ip`、`tcp`、`udp` 或 `icmp`。
- `sip` 是源 IP 地址。
- `sport` 是源端口号。
- `dip` 是目的 IP 地址。
- `dport` 是目的端口号。

如果数据包匹配了某个 Snort 规则，规则的类型将决定所采取的操作。Snort 不会尝试将数据包匹配到后续规则。可以指定的动作列表所示：

- `pass` 导致 Snort 忽略该数据包。
- `log` 导致 Snort 记录该数据包。
- `alert` 导致 Snort 生成警报。

值 `any` 可用于指定数据包中出现的源端口或目的端口。IP 地址可以单独指定，也可以作为列表形式指定，使用与配置文件中相同的语法。此外，可以使用配置文件中定义的 Snort 变量来指定 IP 地址。例如：

```
alert tcp $EXTERNAL_NET any -> $HOME_NET 80
```

这匹配源 IP 地址位于监控网络之外、且进入被监控网络 80 端口的流量。符号 `->` 表示其左侧的 IP 地址和端口属于源，而右侧的 IP 地址和端口属于目的。使用备用符号 `<>` 的规则如下：

```
alert tcp $EXTERNAL_NET any <> $HOME_NET 80
```

该规则匹配的是与以下规则组合匹配的相同数据包：

```
alert tcp $EXTERNAL_NET any -> $HOME_NET 80

alert tcp $HOME_NET 80 -> $EXTERNAL_NET any
```

> 如果你难以判断 Snort 是否正在生成警报，可以临时添加一条标记常见流量的警报规则。例如：
> `alert tcp $EXTERNAL_NET any -> $HOME_NET 80`
> 一旦你确认一切无误，就可以删除该规则。

![](img/0f69b2a8749a24b957044e9f26f2d5b4_442_0.png)

# 第 13 章：管理防火墙

## 高级 SNORT 规则

Snort 支持更高级的规则，这些规则可以测试额外的头部和负载字段，并自定义生成的警报。在编写高级规则时，有三十多个指定符可可用。表 13-5 总结了最常用的指定符。请参阅《Snort 用户手册》了解其他指定符，并学习所总结指定符的操作细节。大多数 Snort 规则仅使用表中总结的指定符定义。因此，你应该能够通过参考该表阅读并理解大多数规则。

指定符编写在括号内，位于关联规则的末尾。例如，这条规则针对 TCP 端口 69 的出站活动（关联 TFTP 服务）生成警报：

```
alert tcp $HOME_NET any -> $EXTERNAL_NET 69 (msg:"Outbound TFTP attempt";:priority:2)
```
