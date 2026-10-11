
接下来的两条规则适用于查找响应无法装入 DNS UDP 数据报的罕见情况。它们不会在正常的日常操作中使用。您可以没有这些 TCP 规则而毫无问题地运行系统数月。不幸的是，如果没有这些规则，您的 DNS 查找偶尔会挂起。更典型的是，这些规则由辅助名称服务器向主名称服务器请求区域传输时使用：

```bash
if [ $CONNECTION_TRACKING = "1" ]; then
$IPT -A OUTPUT -o INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVPORTS \
-d $NAMESERVER --dport 53 \
-m state --state NEW -j ACCEPT
fi

$IPT -A OUTPUT -o INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVPORTS \
-d $NAMESERVER --dport 53 -j ACCEPT

$IPT -A INPUT -i INTERNET -p tcp ! --syn \
-s $NAMESERVER --dport 53 \
-s $IPADDR --dport $UNPRIVPORTS -j ACCEPT
```

### 允许作为转发服务器进行 DNS 查找

配置本地转发名称服务器可以带来巨大的性能提升。如图 7.5 所示，当 BIND 被配置为缓存和转发名称服务器时，它既作为本地服务器，也作为远程 DNS 服务器的客户端。直接客户端到服务器交换与转发的服务器到服务器交换之间的区别在于所使用的源端口和目标端口。BIND 不再从非特权端口发起交换，而是从其自身的 DNS 端口 53 发起交换。（查询源端口现在是可配置的。在新版本的 BIND 中，本地服务器默认从非特权端口发出请求。）

历史上，DNS 服务器在与其它服务器通信时使用 UDP 端口 53 作为其源端口。这将客户端流量与由服务器发起的流量区分开来，因为客户端始终使用高的非特权端口作为其源。后来版本的 BIND 允许服务器到服务器的源端口可配置，并默认使用非特权端口。本书中的所有示例都假设 BIND 被配置为使用 UDP 端口 53，而不是非特权端口，用于服务器到服务器的查询。

![](img/7d04225c75a86d3cf4bd6077596f35b2_316_0.png)

图 7.5 DNS 转发服务器查找。

第二个区别是，这种类型的转发服务器查找始终通过 UDP 进行。（如果响应太大而无法装入 UDP DNS 数据包，本地服务器必须退回到标准的客户端/服务器行为以发起 TCP 请求。）

本地客户端请求被发送到本地 DNS 服务器。第一次时，BIND 将没有查找信息，因此它将请求转发到远程服务器。返回的信息传递给客户端。下一次请求相同信息时，BIND 会在其本地缓存中找到它（根据记录的生命周期 [TTL]），而不再进行远程请求：

```bash
$IPT -A OUTPUT -o $INTERNET -p udp \
  -s $IPADDR --sport 53 \
  -d $NAMESERVER --dport 53 -j ACCEPT
```

```bash
$IPT -A INPUT -i $INTERNET -p udp \
-s $NAMESERVER --sport 53 \
-d $IPADDR --dport 53 -j ACCEPT
```

如果因 UDP 数据包大小导致查找失败，服务器将回退到 TCP 模式循环。如果因远程服务器没有相关信息导致查找失败，本地服务器将查询根缓存服务器。由于这些服务器的存在，客户端需要允许向任何服务器发送 DNS 流量，而不仅仅是本地配置中列出的特定服务器。

替代的 BIND 配置是将其不仅配置为转发服务器，还配置为 BIND 配置文件 `named.conf` 中指定的远程服务器的从属服务器。作为从属服务器时，不需要一般的客户端 UDP 规则。

## 7.4.2 过滤 AUTH 用户身份识别服务（TCP 端口 113）

AUTH，即 ident，用户身份识别服务有时用于发送邮件或发布 aenet 文章。一些 FTP 站点也配置为要求可解析的 AUTH 查找。出于日志记录目的，服务器会向您的机器发起 AUTH 请求，以获取发起邮件或新闻连接的用户的账户名称。表 7.2 列出了 AUTH 服务的完整客户端/服务器连接协议。尽管要求此服务的情况正在减少，因此我不建议在你的服务器上运行它。

### 表 7.2 ident 协议

| 描述 | 协议 | 远程地址 | 远程端口 | 入/出 | 本地地址 | 本地端口 | TCP 标志 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 本地客户端查询 | TCP | ANYWHERE | 113 | Out | IPADDR | 1024:65535 | Any |
| 远程服务器响应 | TCP | ANYWHERE | 113 | In | IPADDR | 1024:65535 | ACK |
| 远程客户端查询 | TCP | ANYWHERE | 1024:65535 | In | IPADDR | 113 | Any |
| 本地服务器响应 | TCP | ANYWHERE | 1024:65535 | Out | IPADDR | 113 | ACK |

### 作为客户端允许你的出站 AUTH 请求

如果你运行邮件或 FTP 服务器，你的机器将作为 AUTH 客户端运行。以下是规则，允许你的服务器作为 AUTH 客户端运行（如果你选择这样做）：

```bash
if [ "$CONNECTION_TRACKING" = "1" ]; then $IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVPORTS \
--dport 113 -m state --state NEW -j ACCEPT
fi
$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVPORTS \
--dport 113 -j ACCEPT
```

```bash
$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
--sport 113 \
-d $IPADDR --dport $UNPRIVPORTS -j ACCEPT
```

### 过滤传入你服务器的请求

无论你决定是否提供该服务，当你发送邮件时，你很可能会收到针对该服务的传入请求。

如果你运行 identd 服务器，以下规则启用传入的 identd 连接请求：

```bash
if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A INPUT -i $INTERNET -p tcp \
--sport $UNPRIVPORTS \
-d $IPADDR --dport 113 \
-m state --state NEW -j ACCEPT
fi
$IPT -A INPUT -i $INTERNET -p tcp \
--sport $UNPRIVPORTS \
-d $IPADDR --dport 113 -j ACCEPT
```

```bash
$IPT -A OUTPUT -o $INTERNET -p tcp ! --syn \
-s $IPADDR --sport 113 \
--dport $UNPRIVPORTS -j ACCEPT
```

如果你决定不提供该服务，拒绝连接请求是一个好习惯，以避免等待 TCP 连接超时。这种情况仅发生在传入数据包被拒绝而不是被丢弃时，在这些示例中：

```bash
$IPT -A INPUT -i $INTERNET -p tcp \
--sport $UNPRIVPORTS \
-d $IPADDR --dport 113 -j REJECT --reject-with tcp-reset
```

或者，你可以使用接受规则，但不运行 identd 服务器。结果将是相同的：TCP 层将向发送方返回一个 TCP RST 消息。

## 7.5 启用常见 TCP 服务

很可能没有人希望启用本节列出的所有服务，但大多数人希望启用其中的一部分。这些是当今互联网上最常用的服务。因此，本节更多是一个参考章节。本节提供了以下规则：

- 电子邮件
- Usenet
- Telnet
- SSH
- FTP
- Web 服务
- Whois
- RealAudio、RealVideo 和 QuickTime

### 7.5.1 电子邮件（TCP SMTP 端口 25，POP 端口 110，IMAP 端口 143）

还有许多其他服务未在此处涵盖。其中一些用于专用服务器，一些由大型企业或组织使用，还有一些设计用于本地私有网络。
