
IP-Address 可以采取两种形式之一：仅为 IP 地址的最后一个字节（让名称服务器自动加上 `in-addr.arpa` 域中的信息作为后缀），或完整的 IP 地址（末尾带有点号）。`Host_name` 必须形成完整的 FQDN。例如，主机 `serverB` 的 PTR 记录如下：

```
192.168.1.2 IN PTR serverB.example.org.
```

`ip6.arpa` 域中 IPv6 地址的 PTR 记录表示方式与 IPv4 地址类似，但是反序的。与普通的 IPv6 方式不同，地址不能压缩或缩写；它以所谓的“反向半字节格式”（四位聚合）表示。因此，对于 IPv6 地址为“2001:DB8::2”的主机的 PTR 记录，地址必须扩展为其等效的“2001:0db8:0000:0000:0000:0000:0000:0002”。

例如，对于 IPv6 地址为 2001:DB8::2 的主机 `server` 的 IPv6 等 PTR 记录（单行）：

```
2.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.8.b.d.0.1.0.2  PTR \
serverB.example.org.
```

## MX：邮件交换器 (Mail Exchanger)

MX 记录负责告诉其他站点你所在区域的邮件服务器。如果你网络上的某个主机生成了带有其主机名的传出邮件，回复消息的人将不会直接发回给该主机。相反，邮件服务器将查找该站点的 MX 记录并发送消息。例如，当用户的桌面名称 `pc.domain` 使用其基于 PC 的邮件客户端/读取器发送消息时，该读取器无法接受简单传输协议（SMTP）；因此让回复方有一种可靠的方法来获知 `pc.domain` 邮件服务器的身份是至关重要的。

MX 记录的格式如下：

```
domainname. IN MX weight Host_name
```

其中，`domainname` 是站点的域名（当然末尾带有一个点）；`weight` 是邮件服务器优先级（如果存在多个邮件服务器，数字越小的排在数字大的之前）；而 `Host_name` 显然是邮件服务器的名称。`Host_name` 也必须拥有 A 记录，这一点非常重要。

这里有一个示例：

```
example.org. IN MX 10 smtp1
IN MX 20 smtp2
```

通常情况下，MX 记录出现在 DNS 配置文件的顶部附近。如果未指定域名，默认名称将从 SOA 记录中提取。

## CNAME：规范名称 (Canonical Name)

CNAME 记录允许你为主机名创建别名。CNAME 记录可以被视为别名。当你想要用一个易记的名称提供高可用服务，但仍给主机一个真实名称时，这非常有用。

CNAME 的另一个流行用途是在无需实际投入新服务器的情况下，“创建一个”一个具有易记名称的新服务器。示例：假设一个站点有一个主机名名为 `zabsuj-content.example.org` 的 Web 服务器。可以认为 `zabsuj-content.example.org` 既不于记也不用户友好。因此，由于该系统是 Web 服务器，可以为该主机创建一个名为“www”的 CNAME 记录（即别名）。这将简单地将不友好的名称 `zabsuj-content.example.org` 映射到更友好的名称 `www.example.org`。这将允许所有指向 `www.example.org` 的请求匿名地传递到托管网页内容的实际系统，即 `zabsuj-content.example.org`。

以下是 CNAME 记录的格式：

```
New_host_name   IN CNAME    old_host_name
```

例如，对于我们之前描述的场景，CNAME 条目将是：

```
zabsuj-content   IN A        192.168.1.111
www             IN CNAME   zabsuj-content
```

## RP 和 TXT：文档条目

有时，将联系信息作为数据库的一部分是很有用的——不仅仅是注释，而是作为其他其他人可以查询的实际记录。这可以通过 RP（负责人）记录和 TXT 记录来实现。TXT 记录是自由格式的文本，你可以在其中放置你认为需要的的信息。例如：

```
serverA.example.org   IN TXT    "Contact"
                       IN TXT    "Admin"
```

RP 记录说明了负责人是谁。拥有这些信息是一项常见的礼貌：

```
serverB.example.org   IN RP     admin.example.org
```

## 设置 BIND 数据库文件

现在你已经了解了所有的记录类型并可以开始了。是时候创建实际数据库了。数据库的格式并不严格，但随着时间的推移形成了一些约定。

每个数据库文件都应该以 `$TTL` 条目开始。该条目告诉每个单独记录的生存时间，除非未另行指定。（SOA 记录中的生存时间或 TTL 仅对 SOA 记录有效。）在 `$TTL` 条目之后是 SOA 记录和至少一个 NS 记录。其他内容都是可选的。（当然，“其他所有内容”使得文件变得有用！）你可能会发现以下通用格式很有帮助：

```
$TTL
SOA record
NS records
MX records
A and CNAME records
```

让我们从头到尾梳理构建一个完整的 DNS 服务器的过程，以更好地展示到为止的信息是如何整合在一起的。对于此示例，我们将为 `example.org` 构建 DNS 服务器，以实现以下目标：

- 建立两个名称服务器：`ns1.example.org` 和 `ns2.example.org`。
- 名称服务器能够对它们已知的 IPv6 记录查询做出响应。
- 作为 `sales.example.org` 区域的从服务器，其中 `serverB.example.org` 将作为主服务器。
- 为 `serverA`、`serverB`、`smtp` 和 `ns2` 定义 A 记录。
- 为 `serverA-v6` 和 `serverB-v6` 定义 AAAA 记录（IPv6）。
- 将 `smtp.example.org` 定义为 `example.org` 域的邮件交换器（MX）。
- 将 `www.example.org` 定义为 `serverA.example.org` 的备用名称（CNAME），并将 `ftp.example.org` 定义为 `serverB.example.org` 的备用名称。
- 最后，我们将为 `serverA.example.org` 定义联系信息。

### 拆解具体步骤

为了完成为 `example.org` 设置 DNS 服务器的目标，我们将会执行一系列步骤。让我们逐一进行。

- 1. 确保你已经按照本章较早部分的描述安装了 BIND DNS 服务器软件。使用 `rpm -q` 来确认此类型。

```
[root@serverA ~]# rpm -q bind
bind-9.* ]
```

> 如果你是从源码编译并安装 BIND 的，那么前面的 `rpm` 命令将不会显示任何内容，因为 RPM 数据库对它一无所知。但你应该清楚自己安装了什么以及安装在何处。

- 2. 使用你熟悉的文本编辑器创建主 DNS 服务器配置文件，即 `/etc/named.conf` 文件。在文件中输入以下文本：

```
options (
    listen-on port 53 { any };
    listen-on-v6 port 53 { any };
    directory "/var/named";
    dump-file "/var/named/data/cache_dump.db";
    statistics-file "/var/named/data/named_stats.txt";
    notify yes;
);

# 以下的区域定义不需要任何修改。第一个
# 是根域名服务器的定义，并将我们的服务器设置为一个
# 具有缓存能力的 DNS 服务器。
# 第二个定义了 localhost。
# 第三个区域定义定义了 localhost 的反向查询。

zone "." in {
    type hint;
    file "root.hints";
}

zone "localhost" in {
    type master;
    file "localhost.db";
}

zone "0.0.127.in-addr.arpa" in {
    type master;
    file "127.0.0.rev";
}

# 下方的区域定义用于我们的名称服务器具有权威性的域名
# 即 example.org 域名。
```

```
zone "example.org" {
  type master;
  file "example.org.db";
}

# 下面是 example.org 站点的 in-addr.arpa 区域。

zone "1.168.192.in-addr.arpa" {
```
