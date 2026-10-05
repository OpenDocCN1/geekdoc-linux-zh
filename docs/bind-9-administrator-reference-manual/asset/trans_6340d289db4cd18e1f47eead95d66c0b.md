

# allow-update-forwarding

指定哪些主机允许向从区提交动态 DNS 更新，并将这些更新重定向到主区。默认值为 `{ none };`，这意味着不会执行任何更新转发。要启用更新转发，请指定 `allow-update-forwarding { any };`。指定除 `{ none; }` 或 `{ any; }` 以外的值通常是适得其反的，因为访问控制的责任应该由主服务器承担，而不是从服务器。

请注意，在从服务器上启用更新转发功能可能会导致依赖于不安全的 IP 地址访问控制的主服务器受到攻击；更多信息请参阅第 7.3 节。

# also-notify

仅当此区域的 `notify` 激活时才有意义。接收 DNS NOTICE 的机器set由所有列出的名称服务器（主服务器除外）加上任何通过 `also-notify` 指定的 IP 地址组成。每个 `also-notify` 地址后面都可以指定一个端口，以便将通知消息发送到默认端口 53 以外的端口。`also-notify` 对于存根区（stub zones）没有意义。默认是空列表。

# check-names

此选项在 BIND 8 中用于限制主文件中域名的字符集和或从网络接收的 DNS 响应的字符集。BIND 9 不限制域名的字符集，并且没有实现 `check-names` 选项。

# database

指定用于存储区域数据使用的数据库类型。`database` 关键字后面的字符串被解释为由空白符分隔的单词列表。第一个单词标识数据库类型，任何后续单词将作为参数传递给数据库，并以特定于数据库类型的方式进行解释。

默认值为 `"rbt"`，即 BIND 9 原生的内存红黑树数据库。该数据库不接受参数。

如果向服务器中链接了额外的数据库驱动程序，则可以使用其他值。发行版中包含了一些示例驱动程序，但默认没有链接。

# dialup

请参阅第 6.2.14 节中关于 `dialup` 的描述。

# forward

仅当区域具有转发器列表时才有意义。**only**（唯一）值会导致查找在尝试转发器且未得到答复后失败，而 **first** 则允许允许尝试正常查找。

# forwarders

用于覆盖全局转发器列表。如果在类型为 **forward** 的区域中未指定，则对该区域不进行转发；不使用全局选项。

# ixfr-base

在 BIND 8 中用于指定动态更新和 IXFR 的事务日志（journal）文件名称。这是一个未文档的选项，通过附加 `.jn1` 来构建日志文件的名称。

# ixfr-tmp-file

曾是 BIND 8 中的一个未文档的选项。BIND 9 忽略了它。

# max-transfer-time-in

请参阅第 6.2.14.6 节中 **max-transfer-time-in** 的描述。

# max-transfer-idle-in

请参阅第 6.2.14.6 节中 **max-transfer-idle-in** 的描述。

# max-transfer-time-out

请参阅第 6.2.14.6 节中 **max-transfer-time-out** 的描述。

# max-transfer-idle-out

请参阅第 6.2.14.6 节中 **max-transfer-idle-out** 的描述。

# notify

请参阅第 6.2.14.1 节中 **notify** 的描述。

# pubkey

在 BIND 8 中，此选项用于指定公区域密钥，以便在从磁盘加载 DNSSEC 签名区域时验证签名。BIND 9 在加载时不验证签名并忽略该选项。

# zone-statistics

如果为 **yes**，服务器将保留此区域的统计信息，这些信息可以转储到服务器选项中定义的 **statistics-file**。

# sig-validity-interval

请参阅第 6.2.14.14 节中 **sig-validity-interval** 的描述。

# transfer-source

请参阅第 6.2.14.6 节中 **transfer-source** 的描述。

# transfer-source-v6

请参阅第 6.2.14.6 节中 **transfer-source-v6** 的描述。

# notify-source

请参阅第 6.2.14.6 节中 **notify-source** 的描述。

# notify-source-v6

请参阅第 6.2.14.6 节中 **notify-source-v6** 的描述。

# min-refresh-time

# max-retry-time

# min-retry-time

# max-retry-time

请参阅第 6.2.14.14 节中的描述。

# 6.2.22.4. 动态更新策略

BIND 9 支持两种授予客户端对区域执行动态更新权限的方法，分别通过 **allow-update** 和 **update-policy** 选项配置。

**allow-update** 类的工作方式与 BIND 之前的版本相同。它授予给定客户端更新区域内任何名称的任何记录的权限。

**update-policy** 子句是 BIND 9 中的新功能，允许对允许的更新进行更细粒度的控制。它指定了一组规则，每条规则授予或拒绝一个或多个身份更新一个或多个名称的权限。如果动态更新请求消息已签名（即它包含了 TSIG 或 SIG(0) 记录），则可以确定签名者的身份。

规则指定在 **update-policy** 中。规则格式如下：
```
allow|deny { identity } name [ [ ]
```
```
allow|deny { identity } name [ type ]
```
```
allow|deny { identity } name [ type ] [ time ]
```
```
allow|deny { identity } name [ type ] [ time ] [ interval ]
```
```
allow|deny { identity } name [ type ] [ time ] [ interval ] [ predicate ]
```
如果使用 `deny`，则忽略时间参数。如果使用 `allow`，则允许更新。

# 6.3 区域文件

# 6.3.1. 资源记录类型及其使用场景

本节很大程度上借自 RFC 1034，描述了资源记录 (RR) 的概念以及何时使用。

# 6.3.1.1. 资源记录 (RR)

域名标识一个节点。每个节点有一组资源信息，可以是空的。

# 6. BIND 9 配置参考

一组与特定名称相关的资源信息由多个 RR 组成。RR 的顺序不需要名称服务器、解析器或 DNS 的其他部分保留。为了优化，例如指定某个服务器首先尝试。

资源记录的组成部分：

| 所有者域名 | RR 所在的域名。 |
| 类型 | 一个 16 位编码值，指定资源记录中的类型。类型指向抽象资源。 |
| TTL | RR 的生存时间。该字段是以秒为单位的 32 位整数，解析器在缓存 RR 时主要使用。TTL 描述了 RR 在丢弃前可以缓存多久。 |
| 类 | 一个 16 位编码值，标识协议族或协议实例。 |
| RDATA | 描述资源的类型和有时取决于类的数据。 |

以下是有效的 RR 类型（列出的某些类型虽然未过期，但是实验性的 (x) 或历史性的 (h)，不再广泛使用）：

| A | 主机地址。 |
| A6 | IPv6 地址。 |
| AAAA | 过时的 IPv6 地址格式 |
| AFSDB | (x) AFS 数据库服务器的位置。实验性。 |
| CERT | 持数字证书。 |
| CNAME | 指定别名的规范名称。 |
| DNS | 反向地址的委托。替换为另一个名称进行查找。在 RFC 2672 中。 |
| GPOS | 指定全局位置。被 LOC 代替。 |
| HINFO | 标识主机使用的 CPU 和操作系统。 |
| ISDN | (x) ISDN 地址的表示。实验性。 |
| KEY | 存储与域名关联的公钥。 |
| KX | 标识此域名的密钥交换者。 |

