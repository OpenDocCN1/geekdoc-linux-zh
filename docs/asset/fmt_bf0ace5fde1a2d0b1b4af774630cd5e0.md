
`file "example.org.db";`

}

注意，`named.conf` 文件中指定的 `directory` 会自动为 `example.org` 文件名加上前缀。如果你指定 `directory/var/named`，服务器软件将自动在 `/var/named/example.org.db` 查找 `example.org` 的信息。

在这里创建的区域定义是一个正向引用——即其他节点通过该机制查询名称并获取你的名称服务器管理的 `example.org` 域名下系统的 IP 地址。提供 IP 到主机名的映射也是符合 Internet 规范的（如果你想向某些网站发送电子邮件，这也是必要的）。要做到这一点，你需要在 `in-addr.arpa` 域名中提供一个条目。

`in-addr.arpa` 条目的格式是你的 IP 地址的前三个字节，后跟 `in-addr.arpa`。假设 `example.org` 的网络地址为 `192.168.1.1`，则 `in-addr.arpa` 域名将是 `1.1.168.192.in-addr.arpa`。因此，`named.conf` 文件中对应的语句如下：

```
zone "1.168.192.in.arpa" {

    type master;

    file "example.org.rev";

}
```

注意，在这里区域部分使用的文件名（`example.org.db` 和 `example.org.rev`）是完全任意的。你可以自由选择命名规范，只要它对你有意义即可。

示例 `example.org` 区域部分在整个 `named.conf` 文件中的具体位置将在稍后的“DNS 服务器设置详解”部分中显示。

## 附加选项

主域名还可以使用 `options` 语句中的以下配置选择：

- `check-names`
- `allow-update`
- `allow-query`
- `allow-transfer`
- `notify`
- `also-notify`

在区域配置中使用这些任何选项都只会影响该区域。

## 在 named.conf 文件中定义从区域

从服务器的区域条目格式与主服务器相似。对于正向解析，其格式如下：

```
zone domain-name {

    type slave;

    masters IP-address-list;

    file path-name;

}
```

在这里，`domain-name` 与主名称服务器上指定的区域完全相同，`IP-address-list` 是该区域主名称服务器所在的 IP 地址列表，而 `path-name` 是服务器保存主区域文件副本的完整路径位置。

## 附加选项

从区域配置也可以使用 `options` 语句中的某些配置选择：

- `check-names`
- `allow-update`
- `allow-query`
- `allow-transfer`
- `notify`
- `also-notify`

## 在 named.conf 中定义缓存区域

缓存区域配置是所有配置中最简单的。它被用于缓存 DNS 记录以加速未来的请求。格式如下：

```
zone domain-name {

    type cache;

    file path-name;

}
```

`path-name` 指向存储缓存的文件。该文件通常由 DNS 软件本身管理。

第 4 行是重试次数，单位为秒。当从服务器尝试检查记录是否已更新时，如果从服务器无法连接主 DNS 服务器以检查更新，则从服务器将在指定的秒数后重试。

第 5 行指定了过期 `expire` 指令。它用于已缓存数据的从服务器。它告诉这些服务器，如果它们无法联系主服务器进行更新，它们应该在指定的秒数后丢弃该值。对于此项，设置一到两周是一个合适的值。

最终值（第 6 行，最小值）告诉缓存服务器，在无法联系主 DNS 服务器时，它们在过期条目之前应该等待多久。对于此条目，五到七天是一个很好的指南。

> 提示：不要忘记在最后一个条目之后（第 7 行）放置右括号。

## NS: 域名服务器 Name Server

`NS` 记录用于指定哪些名称服务器维护该区域的记录。如果存在你想要传输区域的从名称服务器，则需要在这里指定它们。该记录的格式如下：

```
IN NS ns1.domain.name.

IN NS ns2.domain.name.
```

你可以为域名配置尽可能多的备份服务器——至少两个是一个好主意。如果大多数 ISP 为你提供连接，它们将作为从 DNS 服务器运行。

## A 和 AAAA: 地址记录 Address Records

这可能是在现实中找到的最常见的记录类型。`A` 记录用于提供从主机名到 IP 地址的映射。`A` 地址的格式非常简单：

```
Host_name IN A IP-Address
```

例如，为主机 `serverB.example.org`（其 IP 地址为 `192.168.1.2`）创建的 `A` 记录看起来如下所示：

```
serverB IN 192.168.1.2
```

在 IPv6 世界中，IPv4 资源记录的对应品被称为 `AAAA`（四 A A）资源记录。例如，主机 `serverB`（其 IPv6 地址为 `2001:DB8::2`）的 `AAAA` 记录如下所示：

```
serverB IN AAAA 2001:DB8::2
```

注意，除非主机名以点结尾，否则任何主机名都会自动加上与其关联的 `SOA` 记录中列出的域名。在以下示例中，如果其对应的 `SOA` 记录优先级是 `serverB.example.org`，那么 `server` 被理解为 `serverB.example.org`。如果你将其更改为 `serverB.example.org`（不带尾部点），名称服务器将将其理解为 `serverB.example.org.example.org`——这可能不是你想要的结果！

## PTR: 指针记录 Pointer Record

`PTR` 记录用于执行反向主机名解析，从而允许人们指定 IP 地址并确定相应的主机名。该记录的格式与 `A` 记录相似，只是字段顺序反过了：

```
IP-Address IN PTR Host_name
```

**`IP-Address`** 可以采取两种形式之一：IP 地址的最后一个字节（留出名称以 `in-addr.arpa` 域中的信息作为后缀）或完整的 IP 地址（其后加一个点）。*`Host_name`* 必须具有完整的完全限定域名（FQDN）。例如，`serverB` 的 `PTR` 记录如下：

```
192.168.1.2 IN PTR serverB.example.org.
```

`ipv6.arpa` 域中 IPv6 地址的 `PTR` 记录的表示方式与 IPv4 地址类似，但顺序相反。与普通的 IPv6 方式不同，地址不能被压缩或缩写；因此，它以所谓的“反半字节格式”（四位聚合）表示。因此，对于 IPv6 地址为 `2001:db8::2` 的主机的 `PTR` 记录，地址将扩展为其等效的 `2001:0db8:0000:0000:0000:0000:0000:0002`。

例如，这里是 IPv6 地址为 `2001:DB8::2` 的 `serverB` 的 `PTR` 记录的 IPv6 等效表示（单行）：

```
2.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.8.b.d.0.1.0.0.2 IN PTR serverB.example.org.
```

## MX: 邮件交换器

`MX` 记录负责告诉其他站点你区域的邮件服务器。如果你网络上的某个主机生成了带有其主机名的传出消息，回复消息的人不会直接发送到该主机。相反，回复的邮件服务器将查找该站点的 `MX` 记录并将消息发送到那里。

例如，当名为 `pc.domain` 的用户桌面电脑使用其基于的邮件客户端/读取器发送消息时，该读取器无法接受简单邮件传输协议（SMTP）邮件；回复方有一个可靠的方法来知道 `pc.domain` 邮件服务器的身份，这一点至关重要。

`MX` 记录的格式如下：

```
domainname. IN MX weight Host_name
```

在这里，**`domainname`** 是站点的域名（末尾带有一个点）；**`weight`** 是邮件服务器的重要性（如果存在多个邮件服务器，数字越小的服务器优先级高于数字较大的服务器）；而 *`Host_name`* 是主机名。

为 `serverA.example.org` 定义联系信息。

好的，邦德先生，你已经接到指令了。去吧，完成任务。祝你好运！

# DNS 服务器设置详解

为了完成为 `example.org` 设置 DNS 服务器的目标，我们需要执行一系列步骤。让我们逐一完成这些步骤。

![](img/10063bc94c89912e4f6ac282fcb67141_446_0.png)

> **提示** 如果你不想手动输入所有内容，我们已经将跟进所需的所有文件打包，并为你保存在了以下 URL 中。你只需要下载、解压并将文件复制到步骤指定的正确目录即可，如下所示：

```
# pwd

# wget http://linuxserverexperts.com/7e/chapter-16.tar.xz

# tar xvf chapter-16.tar.xz

# cd chapter-16 && ls
```

- 1. 确保你已经按照本节早前的描述安装了 BIND DNS 服务器软件。使用 `rpm` 命令确认此操作：

```
[root@serverA ~]# rpm -q bind

bind-9.*
```

![](img/10063bc94c89912e4f6ac282fcb67141_446_1.png)

> **注意** 如果你仅从源码编译并安装了 BIND，之前的 `rpm` 命令将不会任何为空，因为 RPM 数据库不知道关于它的任何信息。但你应该清楚自己安装了什么以及安装在哪里。

- 2. 使用你熟悉的任何文本编辑器创建主 DNS 服务器配置文件——`/etc/named.conf`。在文件中输入以下文本：

```
listen-on port 53 { any };

listen-on-v6 port 53 { any };

directory "/var/named"

dump-file "/var/named/data/cache_dump.db";

statistics-file "/var/named/data/named_stats.txt";

notify yes;
```

# 以下区域定义不需要任何修改。第一个
# 是根域名服务器的定义，并将我们的服务器设置为
# 缓存型 DNS 服务器。
# 第二个定义了 localhost。
# 第三个定义了 localhost 的反向查找。

```
zone "." in {

	type hint;

	file "root.hints";

}
```

```
zone "localhost" in {

	type master;

	file "localhost.db";

}
```

```
zone "0.0.127.in-addr.arpa" in {

	type master;

	file "127.0.0.rev";

}
```

# 下方的区域定义是用于我们的名称服务器
# 权威的域名，即 example.org 域名。
zone "example.org" {

  type master;
  file "example.org.db";

};

# 下方是用于 example.org 站点的 in-addr.arpa 区域。
zone "1.168.192.in-addr.arpa" {

  type master;
  file "example.org.rev";

};

# 下方是该服务器作为从服务器的子域名条目
# sales.example.org 主服务器 IP 地址为 192.168.1.2
zone "sales.example.org" {

  type slave;
  file "sales.example.org.bk";
  masters {192.168.1.2};

};

# 下方是用于 example.org 站点的 ip6.arpa 区域。
# 该区域将将其数据存储在与
# 1.168.192.in-addr.arpa 域相同的文件中
zone "0.0.0.0.0.0.0.0.b.d.0.1.0.2.ip6.arpa" {

  type master;
  file "example.org.rev";

};
```

- 3. 将上述文件保存为 `/etc/named.conf` 并退出文本编辑器。

- 4. 接下来，我们需要创建 `/etc/named.conf` 文件中 `file` 部分引用的实际数据库文件。特别是，我们要创建的文件是 `root.hints`、`localhost.db`、`127.0.0.1`、`example.org.db` 和 `example.org.rev`。所有文件将存储在 BIND 的工作目录 `/var/named/` 中。我们将按照从 `named.conf` 文件顶部到底部的顺序创建它们。

- 5. 幸运的是，我们不需要手动创建 root hints 文件。从互联网下载根 hints 的最新副本。使用 `wget -O /var/named/root.hints http://www.internic.net/zones/named.root`。

- 6. 使用你熟悉的任何文本编辑器为 localhost 创建区域文件。这就是 `localhost.db` 文件。在文件中输入以下文本：

```
$TTL 1W

@ IN SOA localhost root (

                2006123100 ; serial

                3H ; refresh (3 hours)

                30M ; retry (30 minutes)

                2W ; expiry (2 weeks)

                1W ; minimum (1 week)

            IN NS

            IN A 127.0.0.1
```

- 7. 将上述文件保存为 `/var/named/localhost.db` 并退出文本编辑器。
- 8. 使用任何文本编辑器为 localhost 创建反向查找区域文件。这就是 `127.0.0.rev` 文件。在文件中输入以下文本：

```
$TTL 1W

@ IN SOA localhost. (

                2006123100 ; serial

                3H ; refresh

                30M ; retry

                2W ; expiry

                1W ; minimum

            IN NS

            PTR localhost.
```
**提示** BIND 中可以使用缩写值。例如，`3H` 表示 3 小时，`2W` 表示 2 周，`30M` 意味着 30 分钟，依此类推。

- 9. 将上述文件保存为 `/var/named/127.0.0.rev` 并退出文本编辑器。
- 10. 接下来，为主区域 `example.org` 创建数据库文件。使用文本编辑器创建 `example.org` 文件，并在文件中输入以下文本：

```
# TTL 1W

@ IN SOA ns1.example.org. root (

    2009123100 ; serial

    3H ; refresh (3 hours)

    30M ; retry (30 minutes)

    2W ; expiry (2 weeks)

    1W ; minimum (1 week)

    IN NS ns1.example.org.

    IN NS ns2.example.org.

    IN MX 10 smtp.example.org.

    ns1 IN 192.168.1.1 ; primary name server

    ns2 IN 192.168.1.2 ; secondary name server

    serverA IN 192.168.1.1

    serverB IN 192.168.1.2

    smtp IN 192.168.1.25 ; mail server

    www IN CNAME serverA ; web server

    ftp IN CNAME serverB ; ftp server

    serverA IN TXT "Fax: 999-999"
```

; serverA (serverA-v6) 和 serverB (serverB-v6) 的 IPv6 目如下：

```
serverA-v6 IN AAAA 2001:DB8::1

serverB-v6 IN AAAA 2001:DB8::2
```

- 11. 将预设文件保存为 `/var/named/example.org.db` 并退出文本编辑器。
- 12. 为 `example.org` 创建反向查找文件。使用文本编辑器创建 `/var/named/example.org.rev`，并在文件中输入以下文本：

```
TTL 1W

@ IN SOA ns1.example.org. root (

    2009123100 ; serial

    3H ; refresh (3 hours)

    30M ; retry (30 minutes)

    2W ; expiry (2 weeks)

    1W ; minimum (1 week)

    IN NS ns1.example.org.

    IN NS ns2.example.org.

    1 IN PTR serverA.example.org. ; Reverse info for serverA
```
