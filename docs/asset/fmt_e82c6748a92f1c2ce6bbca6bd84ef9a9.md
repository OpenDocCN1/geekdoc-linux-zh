
```
SMTP_GATEWAY="my.isp.server" # 外部邮件服务器或中继服务器

if [ "$CONNECTION_TRACKING" = "1" ]; then
  $IPT -A OUTPUT -o $INTERNET -p tcp \
    -s $IPADDR --sport $UNPRIVPORTS \
    -d $SMTP_GATEWAY --dport 25 -m state --state NEW -j ACCEPT
fi

$IPT -A OUTPUT -o $INTERNET -p tcp \
  -s $IPADDR --sport $UNPRIVPORTS \
  -d $SMTP_GATEWAY --dport 25 -j ACCEPT

$IPT -A INPUT -i $INTERNET -p tcp --syn \
  -s $SMTP_GATEWAY --dport 25 \
  -d $IPADDR --dport 25 -j ACCEPT

if [ "$CONNECTION_TRACKING" = "1" ]; then
  $IPT -A INPUT -i $INTERNET -p tcp \
    --sport $UNPRIVPORTS \
    -d $IPADDR --dport 25 \
    -m state --state NEW -j ACCEPT
fi

$IPT -A INPUT -i $INTERNET -p tcp \
  --sport $UNPRIVPORTS \
  -d $IPADDR --dport 25 -j ACCEPT
```

# 启用通用 TCP 服务

```bash
$IPT -A INPUT -i $INTERNET -p tcp \
  --sport $UNPRIVPORTS \
  -d $IPADDR --dport 25 -j ACCEPT
```

```bash
$IPT -A OUTPUT -o $INTERNET -p tcp ! --syn \
  -s $IPADDR --sport 25 \
  --dport $UNPRIVPORTS -j ACCEPT
```

# 作为 SMTP 服务器发送邮件和作为 SMTP 服务器接收邮件

如果你既作为 SMTP 服务器发送邮件，又作为 SMTP 服务器接收邮件，那么你就提供了所有的邮件服务。你本地的 sendmail 守护进程被配置为将出站邮件中继到目标主机，同时也负责收集并投递邮件：

```bash
if [ "$CONNECTION_TRACKING" = "1" ]; then
  $IPT -A OUTPUT -o $INTERNET -p tcp \
    -s $IPADDR --sport $UNPRIVPORTS \
    --dport 25 -m state --state NEW -j ACCEPT
fi

$IPT -A OUTPUT -o $INTERNET -p tcp \
  -s $IPADDR --sport $UNPRIVPORTS \
  --dport 25 -j ACCEPT

$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
  --sport 25 \
  -d $IPADDR --dport $UNPRIVPORTS -j ACCEPT

if [ "$CONNECTION_TRACKING" = "1" ]; then
  $IPT -A INPUT -i $INTERNET -p tcp \
    --sport $UNPRIVPORTS \
    -d $IPADDR --dport 25 \
    -m state --state NEW -j ACCEPT
fi

$IPT -A INPUT -i $INTERNET -p tcp \
  --sport $UNPRIVPORTS \
  -d $IPADDR --dport 25 -j ACCEPT

$IPT -A OUTPUT -o $INTERNET -p tcp ! --syn \
  -s $IPADDR --sport 25 \
  --dport $UNPRIVPORTS -j ACCEPT
```

# 为远程客户端托管邮件服务器

对于小型系统而言，托管公共 POP 或 IMAP 服务是不寻常的。如果你为少数朋友提供远程邮件服务，或者他们的 ISP 邮件服务暂时不可用，你可能会这样做。无论如何，重要的是限制系统接受连接的对象，无论是在数据包过滤级别还是在服务器配置级别。

## 为远程客户端托管 POP 服务器

POP 服务器是黑客利用攻击最常用且最成功的入口点之一。在许多情况下，防火墙规则可以提供一定程度的保护。当然，你也会在服务器配置级别限制访问。一如既往，对于邮件服务器软件而言尤其如此，保持软件安全更新的最新状态至关重要。

如果你使用本地系统作为中央邮件服务器，并运行本地 POP3 服务器为局域网上的本地机器提供访问，那么你不需要此示例中的服务器规则。来自 Internet 的传入连接应被丢弃。如果你需要为有限数量的远程个人提供 POP 服务，接下来的两条规则允许传入连接到你的 POP 服务器。连接限制于你特定客户端的 IP 地址：

```bash
if [ $CONNECTION_TRACKING = "1" ]; then
  $IPT -A INPUT -i $INTERNET -p tcp \
    -s <my.pop.clients> --sport $UNPRIVPORTS \
    -d $IPADDR --port 110 \
    -m state --state NEW -j ACCEPT
fi

$IPT -A INPUT -i $INTERNET -p tcp \
  -s <my.pop.clients> --sport $UNPRIVPORTS \
  -d $IPADDR --port 110 -j ACCEPT

$IPT -A OUTPUT -o $INTERNET -p tcp ! --syn \
  -s $IPADDR --port 110 \
  -d <my.pop.clients> --dport $UNPRIVPORTS -j ACCEPT
```

如果你的站点是一个 ISP，你可以使用网络地址掩码来限制哪些源地址会接受 POP 连接请求：

```bash
POP_CLIENTS="192.168.24.0/24"
```

如果你的是一个住宅站点，只有少数几个远程 POP 客户端，那么客户端地址需要明确列出，并为每个客户端地址设置单独的规则对。

## 为远程客户端托管 IMAP 服务器

IMAP 服务器是黑客利用攻击最常用且最成功的入口点之一。在许多情况下，防火墙规则可以提供一定程度的保护。当然，你也会在服务器配置级别限制访问。一如既往，对于邮件服务器软件而言尤其如此，保持软件安全更新的最新状态至关重要。

如果你使用本地系统作为中央邮件服务器，并运行本地 imap 服务器为局域网上的本地机器提供访问，那么你不需要服务器规则。来自 Internet 的传入连接应被丢弃。如果你确实需要为有限数量的远程个人提供主机 IMAP 服务，接下来的两条规则允许传入连接到你的 IMAP 服务器。连接限制于你特定客户端的 IP 地址：

```bash
if [ "$CONNECTION_TRACKING" = "1" ]; then
  $IPT -A INPUT -i $INTERNET -p tcp \
    -s <my.imap.clients> --sport $UNPRIVPORTS \
    -d $IPADDR --dport 143 \
    -m state --state NEW -j ACCEPT
fi

$IPT -A INPUT -i $INTERNET -p tcp \
  -s <my.imap.clients> --sport $UNPRIVPORTS \
  -d $IPADDR --dport 143 -j ACCEPT

$IPT -A OUTPUT -o $INTERNET -p tcp ! --syn \
  -s $IPADDR --dport 143 \
  -d <my.imap.clients> --dport $UNPRIVPORTS -j ACCEPT
```

如果你的站点是一个 ISP，你可以使用网络地址掩码来限制接受哪些地址的 IMAP 连接请求：

```bash
IMAP_CLIENTS="192.168.24.0/24"
```

如果你的是一个住宅站点，只有少数几个远程 IMAP 客户端，那么客户端地址需要明确列出，并为每个客户端地址设置单独的规则对。

## 7.5.2 访问 Usenet 新闻服务

（TCP NNTP 端口 119）

Usenet 通过运行在 TCP 之上的 NNTP 协议，经由服务端口 119 进行访问。阅读新闻和发布文章由你本地的新闻客户端处理。很少有系统需要服务器规则。表 7.4 列出了 NNTP Usenet 新闻服务的完整客户端/服务器连接协议。

### 表 7.4 NNTP 协议
