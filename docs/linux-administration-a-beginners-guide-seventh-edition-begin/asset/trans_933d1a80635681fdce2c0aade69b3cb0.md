

## NS: 名称服务器 (Name Server)

NS 记录用于指定哪些名称服务器维护该区域的记录。如果你有任何打算传输区域的辅助名称服务器，则需要在这里指定它们。该记录的格式如下：

```
IN NS ns1.domain.name.
IN NS ns2.domain.name.
```

你可以为一个域名设置任意数量的备份名称服务器——至少设置两个是一个好主意。如果 ISP 为你提供连接性，大多数 ISP 都愿意担任辅助 DNS 服务器。

## A 和 AAAA: 地址记录 (Address Records)

这可能是现实世界中最常见的记录类型。A 记录用于提供从主机名到 IP 地址的映射。A 地址的格式非常简单：

```
Host_name      IN      IP-Address
```

例如，主机 serverB 的记录记录（其 IP 地址为 192.168.1.2）如下：

```
serverB      IN      A      192.168.1.2
```

在 IPv6 世界中，等同于 A 资源记录的是 AAAA（四 A）资源记录。例如，对于主机 serverB（其 IPv6 地址为 2001:DB8::2）的四 A 记录如下：

```
serverB      IN      AAAA     2001:DB8::2
```

请注意，任何主机名都会带有 SOA 记录中列出的名称的后缀，除非该主机名以点结尾。在上述 serverB 的示例中，其之前的 SOA 记录是针对 example.org 的，因此 serverB 被理解为 serverB.example.org。如果你将其更改为 serverB.example.org（不带末尾点），名称服务器将将其理解为 serverB.example.org.org——这可能不是你想要的结果的！所以，如果你想使用 FQDN（完全限定域名），请务必在它后面加上一个点。

## PTR: 指针记录 (Pointer Record)

PTR 记录用于执行反向域名解析，从而允许指定指定 IP 地址并确定对应的主机名。该记录的格式与 A 记录相似，但值不同：

```
IP-Address      IN      Host_name
```

## 第 16 章 域名系统 (DNS)

IP 地址可以采取两种形式之一：离开名称服务器的 IP 地址的最后一个字节（自动带有其从 in-addr.arpa 域获得的信息作为后缀），或者完整的 IP 地址（其带有一个点作为后缀）。Host_name 必须具有完整的 FQDN。例如，主机 serverB 的 PTR 记录如下：

```
192.168.1.2.    IN    PTR       serverB.example.org.
```

ipv6.arpa 域中 IPv6 地址的 PTR 记录表示方式与 IPv4 地址类似，但顺序是反的。与普通的 IPv6 方式不同，所谓的“反向半字节格式”（四位聚合）在地址中的表达式无法被压缩或缩写；因此，对于 IPv6 地址为 2001:0db8::2 的主机的 PTR 记录，地址将扩展为其等效的 2001:0db8:0000:0000:0000:0000:0002。
例如，这里是主机 serverB（IPv6 地址为 2001:DB8::2（单写））PTR 记录的 IPv6 等效表示：

```
2.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.8.b.d.0.1.0.2.    IN    PTR \
serverB.example.org.
```

## MX: 邮件交换 (Mail Exchange)

MX 记录负责告诉其他站点你区域的邮件服务器。如果你网络上的主机生成了一封带有其主机名的发送邮件，回复消息的人将不会将其发回该主机。相反，回复邮件的服务器将查找该站点的 MX 记录并发送消息。
例如，当用户的桌面名称 pc.domain 使用其基于 PC 的电子邮件客户端/读取器发送消息时，会使用 MX 记录，该客户端无法接受简单邮件传输协议（SMTP）邮件；回复方拥有一种可靠的方法来了解 pc.domain 邮件服务器的身份是非常重要的。
MX 记录的格式如下：

```
domainname.      IN    MX    weight       Host_name
```

在这里，domainname 是站点的名称（当然末带有一个点）；weight 是邮件服务器的重要性（如果存在多个邮件服务器，数字越小的优先级高于数字越大的）；而 Host_name 当然是邮件服务器的名称。Host_name 具有如下所示的 A 记录是非常重要的。
这里有一个示例：

```
example.org.      IN    MX    10    smtp1
                   IN    MX    20    smtp2
```

此外，MX 记录出现在 DNS 配置文件的顶部附近。如果未指定域名，则默认值将从 SOA 记录中提取。

## CNAME: 规范名称 (Canonical Name)

CNAME 记录允许你为 A 创建别名。CNAME 记录可以被视为一种别名。当你想要用易记的名称提供高可用服务，但仍给主机一个真实名称时，这非常有用。
CNAME 的另一个流行用途是“创建一个”一个具有易记名称的新服务器，而无需实际投资新服务器。这里有一个示例：假设一个主机名为 zabsuj-content.example 的 Web 服务器既不便于记忆也不便于用户。由于该系统是 Web 服务器，可以为该主机创建一个“www”的 CNAME 记录（或别名）。这将简单地将用户不友主机名 zabsuj-content.example.org 映射到 www.example.org。这将允许所有发往 www.example.org 的请求透明地传递到托管内容的实际系统——即 zabsuj-content.example.org。
以下是 CNAME 记录的格式：

```
New_host_name IN CNAME old_host_name
```
对于我们的场景，CNAME 条目将是

| | | |
|---|---|---|
| zabsuj-content | A | 192.168.1.111 |
| www | CNAME | zabsuj-content |

## RP 和 TXT: 文档条目 (Documentation Entries)

有时，将联系信息作为数据库的一部分是很有用的——不仅仅是注释，而是作为他人查询的实际记录。这可以通过 RP（责任人）和 TXT 记录来实现。
TXT 记录是一个自由格式的文本输入，你可以在其中放置你认为的任何信息。大多数情况下，你会在这些记录中放入联系信息。每个 TXT 记录都必须与特定的主机名绑定。这里有一个示例：

|---|---|---|
| serverA.example.org. | TXT | "Contact: Admin Guy" |
| IN | TXT | "SysAdmin/Android" |
| IN | TXT | "Voice: 999-999-9999" |

RP 记录被创建作为主机联系信息的显式容器。该记录指明特定主机的责任人是谁；这里有一个示例：

```
serverB.example.org. IN RP admin-address.example.org example.org.
```

尽管这些记录可能有用，但它们现在已很罕见，因为人们认为它们泄了了关于站点的信息，可能导致基于社会工程学的攻击。你可以在内部 DNS 服务器中发现此类记录很有用，但你应该将它们排除在任何可以从互联网查询的内容之外。

## 设置 BIND 数据库文件 (Setting Up BIND Database Files)

现在你已经了解了所有的 DNS 记录类型并可以开始了。现在是时候为服务器创建实际数据库了。数据库文件的格式并不严格，但一些约定随着时间的推移形成了。遵循这些约定会让你的生活变得更容易，并为接手你工作的管理员铺平道路。

> 注意：在 bind 配置文件中要字面地添加注释。注释行以井号 (#) 开头。尽管 DNS 数据库文件中发生的事情并不神秘，但更改历史对于了解完成了什么以及如何完成的非常有参考价值。

数据库文件是你最重要的配置文件。创建正向查找数据库很容易；但通常会漏掉反向查找。某些程序（如 Sendmail 和 TCP Wrappers）会对 IP 地址进行反向查找以查看人们的来源，因此提供这些信息是种常见的礼貌。

每个数据库文件都应该以 $TTL 条目开始。该条目告诉 BIND 在没有显式指定的情况下，每个单独记录的生存时间是多少。（SOA 记录中的生存时间，即 TTL，仅适用于 SOA 记录本身。）在 $TTL 条目之后是 SOA 记录和至少一个 NS 记录。其他内容都是可选的。（当然，“其他内容”才是使文件有用的关键！）可能会发现以下通用格式很有帮助：

```
$TTL
SOA 记录
NS 记录
MX 记录
A 和 CNAME 记录
```

让我们从头到尾构建一个完整的配置的过程，以演示目前为止的信息是如何结合的。例如，我们将为实现以下目标的示例构建 DNS 服务器：

- 建立两个名称服务器：ns1.example.org 和 ns2.example.org。
- 名称服务器将能够对它们所知的 IPv6 记录的查询做出响应。
- 作为 sales.example.com 区域的从服务器，其中 serverB.example.org 是主服务器。
- 为 serverA、serverB、smtp、ns1 和 ns2 定义 A 记录。
- 为 serverA-v6 和 serverB-v6 定义 AAAA 记录（IPv6）。

