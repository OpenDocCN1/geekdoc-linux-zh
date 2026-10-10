
$IPT -A OUTPUT -o $INTERNET -p tcp ! --syn \
    -s $IPADDR --sport 25 \
    --dport $UNPRIVPORTS -j ACCEPT

## 为远程客户端托管邮件服务器

对于小型系统而言，托管公共 POP 或 IMAP 服务并不常见。你可能会这样做，例如，如果你为少数朋友提供远程邮件服务，或者他们的 ISP 邮件系统暂时不可用。无论如何，重要的是要在数据包过滤级别和服务器配置级别上限制你的系统将接受连接的客户机。

## 为远程客户端托管 POP 服务器

POP 服务器是最常见且最成功的黑客攻击切入点之一。在许多情况下，防火墙规则可以提供一定程度的保护。当然，你也会在服务器配置级别限制访问。一如既往，尤其是对于邮件服务器软件，保持软件的安全更新最新至关重要。

如果你使用本地系统作为中央邮件服务器，并运行本地 POP3 服务器以提供局域网内本地机器的邮件访问，则不需要本示例中的服务器规则。来自 Internet 的传入连接应该被丢弃。如果你确实需要为有限数量的远程个人托管 POP 服务，下面的两条规则允许传入连接至你的 POP 服务器。连接被限制为你特定客户机的 IP 地址：

```
if [ "$CONNECTION_TRACKING" = "1" ]; then
    $IPT -A INPUT -i $INTERNET -p tcp \
    -s <my_pop_clients> --sport $UNPRIVPORTS \
    -d $IPADDR --port 110 \
    -m state --state NEW -j ACCEPT
fi
```

```
$IPT -A INPUT -i $INTERNET -p tcp \
    -s <my_pop_clients> --sport $UNPRIVPORTS \
    -d $IPADDR --port 110 -j ACCEPT
```

```
$IPT -A OUTPUT -o $INTERNET -p tcp ! --syn \
    -s $IPADDR --sport 110 \
    -d <my_pop_clients> --dport $UNPRIVPORTS -j ACCEPT
```

如果你的站点是一个 ISP，你可以使用网络地址掩码来限制你接受 POP 连接请求的来源地址：

```
POP_CLIENTS="192.168.24.0/24"
```

如果你的站点是一个拥有少数远程 POP 客户的住宅站点，则需要明确列出客户地址，并为每个客户地址设置单独的规则对。

## 为远程客户端托管 IMAP 服务器

IMAP 服务器是最常见且最成功的黑客攻击切入点之一。在许多情况下，防火墙规则可以提供一定程度的保护。当然，你也会在服务器配置级别限制访问。一如既往，尤其是对于邮件服务器软件，保持软件的安全更新最新至关重要。

如果你使用本地系统作为中央邮件服务器，并运行本地 `imapd` 脚本以提供局域网内本地机器的邮件访问，则不需要服务器规则。来自 Internet 的传入连接应该被丢弃。如果你确实需要为有限数量的远程个人托管 IMAP 服务，下面的规则允许传入连接至你的 IMAP 服务器。连接被限制为你特定客户机的 IP 地址：

```
if [ "$CONNECTION_TRACKING" != "1" ]; then
$IPT -A INPUT -i $INTERNET -p tcp \
-s <my.imap.clients> --sport $UNPRIVPORTS \
-d $IPADDR --dport 143 \
-m state --state NEW -j ACCEPT
fi

$IPT -A INPUT -i $INTERNET -p tcp \
-s <my.imap.clients> --sport $UNPRIVPORTS \
-d $IPADDR --dport 143 -j ACCEPT

$IPT -A OUTPUT -o $INTERNET -p tcp ! --syn \
-s $IPADDR --sport 143 \
-d <my.imap.clients> --dport $UNPRIVPORTS -j ACCEPT
```

如果你的站点是一个 ISP，你可以使用网络地址掩码来限制你接受 IMAP 连接请求的来源地址：

```
IMAP_CLIENTS="192.168.24.0/24"
```

如果你的站点是一个拥有少数远程 IMAP 客户的住宅站点，则需要明确列出客户地址，并为每个客户地址设置单独的规则对。

## 访问 Usenet 新闻服务（TCP NNTP 端口 119）

Usenet 新闻通过运行在 TCP 之上的 NNTP 访问，使用服务端口 119。阅读新闻和发布文章由你的本地新闻客户机处理。很少有系统需要服务器规则。表 4.4 列出了 NNTP Usenet 新闻服务的完整客户机/服务器连接协议。

**表 4.4**
**NNTP 协议**

| 描述 | 协议 | 远程地址 | 远程端口 | 本地进/出 | 本地地址 | 本地端口 | TCP 标志 |
|---|---|---|---|---|---|---|---|
| 本地客户机查询 | TCP | 新闻服务器 | 119 | 出 | IPADDR | 1024:65535 | 任意 |
| 远程服务器响应 | TCP | 新闻服务器 | 119 | 进 | IPADDR | 1024:65535 | ACK |
| 远程客户机查询 | TCP | NNTP 客户机 | 1024:65535 | 进 | IPADDR | 119 | 任意 |
| 本地服务器响应 | TCP | NNTP 客户机 | 1024:65535 | 出 | IPADDR | 119 | ACK |
| 本地服务器查询 | TCP | 新闻源 | 119 | 出 | IPADDR | 1024:65535 | 任意 |
| 远程服务器响应 | TCP | 新闻源 | 119 | 进 | IPADDR | 1024:65535 | ACK |

## 作为 Usenet 客户机阅读和发布新闻

客户机规则允许连接至你 ISP 的新闻服务器。阅读新闻和发布文章都由这些规则处理：

```
NEWS_SERVER="my.news.server"        # 外部新闻服务器（如果有）

if [ "$CONNECTION_TRACKING" = "1" ]; then
   $IPT -A OUTPUT -o $INTERNET -p tcp \
       -s $IPADDR --sport $UNPRIVPORTS \
       -d $NEWS_SERVER --dport 119 -m state --state NEW -j ACCEPT
fi

$IPT -A OUTPUT -o $INTERNET -p tcp \
    -s $IPADDR --sport $UNPRIVPORTS \
    -d $NEWS_SERVER --dport 119 -j ACCEPT

$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
    -s $NEWS_SERVER --sport 119 \
    -d $IPADDR --dport $UNPRIVPORTS -j ACCEPT
```

## 为远程客户端托管 Usenet 新闻服务器

小型站点不太可能为外部世界托管新闻服务器。即使是托管本地新闻服务器也不太可能。对于罕见的例外情况，应配置服务器规则以仅允许来自选定客户机组的传入连接：

```
if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A INPUT -i $INTERNET -p tcp \
-s <my.news.clients> --sport $UNPRIVPORTS \
-d $IPADDR --dport 119 \
-m state --state NEW -j ACCEPT
fi

$IPT -A INPUT -i $INTERNET -p tcp \
-s <my.news.clients> --sport $UNPRIVPORTS \
-d $IPADDR --dport 119 -j ACCEPT

$IPT -A OUTPUT -o $INTERNET -p tcp ! --syn \
-s $IPADDR --sport 119 \
-d <my.news.clients> --dport $UNPRIVPORTS -j ACCEPT
```

## 允许本地 Usenet 服务器接受对等新闻源

小型、家庭式站点不太可能与 ISP 建立点对点新闻源服务器关系。虽然以前新闻服务器对一般 Internet 用户来说相当容易访问，但由于垃圾邮件和服务器负载问题，如今可用的开放新闻服务器很少。

如果你的站点足够大或足够富裕，可以托管通用的 Usenet 服务器，你必须从某处获取新闻源。接下来的两条规则允许你的本地新闻服务器从远程服务器接收其新闻源。本地服务器作为客户机联系远程服务器。点对点新闻源规则与常规客户机规则之间的唯一区别是远程主机的名称或地址：

```
if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVPORTS \
-d <my.news.feed> --dport 119 -m state --state NEW -j ACCEPT
fi

$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVPORTS \
-d <my.news.feed> --dport 119 -j ACCEPT

$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
-s <my.news.feed> --sport 119 \
-d $IPADDR --dport $UNPRIVPORTS -j ACCEPT
```

## Telnet（TCP 端口 23）

Telnet 多年来一直是 Internet 上远程登录的事实标准方式。随着 Internet 社区性质的变化，telnet 被视为一种不安全的服务，因为它以 ASCII 明文通信。如果你有选择，应该始终使用加密服务（如 SSH），而不是 telnet。然而，Microsoft Windows 不提供 SSH 服务，只提供 telnet——这就是对安全承诺的讽刺！

此处的客户机和服务器规则允许来自任何地方的访问。如果你使用 telnet，你可以在数据包过滤级别将外部地址限制为非常特定的子集。表 4.5 列出了 telnet 服务的完整客户机/服务器连接协议。

**表 4.5**
**Telnet 协议**

| 描述 | 协议 | 远程地址 | 远程端口 | 本地进/出 | 本地地址 | 本地端口 | TCP 标志 |
|---|---|---|---|---|---|---|---|
| 本地客户机请求 | TCP | 任意 | 23 | 出 | IPADDR | 1024:65535 | 任意 |
| 远程服务器响应 | TCP | 任意 | 23 | 进 | IPADDR | 1024:65535 | ACK |
| 远程客户机 TCP 请求 | TCP | Telnet 客户机 | 1024:65535 | 进 | IPADDR | 23 | 任意 |
| 本地服务器响应 | TCP | Telnet 客户机 | 1024:65535 | 出 | IPADDR | 23 | ACK |

## 允许出站客户机访问远程站点

如果你需要使用 telnet 访问远程系统（如今 SSH 服务器非常普遍），接下来的两条规则允许出站连接至远程站点。如果你的站点有多个用户，如果可能，应将出站连接限制为用户拥有帐户的具体站点，而不是允许出站连接至任何地方：

```
if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVPORTS \
--dport 23 -m state --state NEW -j ACCEPT
fi

$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVPORTS \
--dport 23 -j ACCEPT

$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
-s $IPADDR --sport 23 \
-d $IPADDR --dport $UNPRIVPORTS -j ACCEPT
```

