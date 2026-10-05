

# DNS 简介

在反向区域中的 3（例如，0.168.192.in-addr.arpa 区域中的 3 是 192.168.0.3）对应于区域中的 peach：

3 IN PTR peach

更多信息请参阅第 831 页的“反向域名解析”。

SOA（起始起始记录）指定区域的开始。每个区域必须恰好有一个 SOA 记录。权威服务器维护其所权威区域的 SOA 记录。
所有文件必须有一个 SOA 资源记录，且该记录必须是文件中的第一个资源。Name（名称）字段包含区域起始处的域名。Data（数据）字段包含创建该主机的主机、负责区域的人员电子邮件地址以及以下信息，如果记录无法在一行内，这些信息必须包含在括号内。如果这些信息包含在括号内（通常如此），左括号必须出现在 SOA 记录的第一个物理行：

- serial（序列号）范围在 1 到 2,147,483,647 之间。此数字的变化表示区域发生了变化。按照惯例，此字段被设置为字符串 yyyymmddann（年、月、日、变更次数）。与日期一起，每次你更改 SOA 记录时，都应该增加最后两位——即变更天。

- refresh（刷新）：在主主服务器通知从服务器（备用服务器）刷新记录后经过的时间；以及它们之间更新的时间间隔。

- retry（重试）：在刷新失败后，尝试再次刷新之前等待的时间。

- expire（过期）：在区域不再具有权威性且必须查询根服务器后经过的时间。expire 仅适用于从服务器。

- minimum（最小 TTL）：负缓存（缓存 NXDOMAIN TTL）的 TTL，即不存在的域名错误（NXDOMAIN）在从服务器缓存中保留的时间。负缓存 TTL 与普通 TTL 相同，不同之处在于适用于不存在的域名，而不是存在的域名。

TTL 指令（第 839 页）定义了区域 TTL（从服务器缓存中保留记录的最长天数）。默认区域 TTL 和负 TTL 共同涵盖了服务器可以生成的所有类型记录。如果你将频繁地添加域名或修改现有域名，请将负 TTL 设置为较小的值。短 TTL 会增加请求不存在域名的客户端的 DNS 流量，但允许域名快速传播，尽管是以增加流量为代价。

两个 SOA 资源记录是等效的（第一条记录中的括号是可选的，因为记录适合单行物理行）：

```
@ IN SOA ns.zach.net. sobel.com. ( 2010111247 8H 2W 1D )
@ IN SOA ns.zach.net. sobel.com. (
 : serial 2010111247
8H : refresh
2H : retry
4W : expire
1D : minimum
)
```

# 830 第 24 章 DNS/BIND：跟踪域名和地址

由于布局和注释，第二种格式更具可读性。SOA 资源记录中的 @ 符号代表在 named.conf 文件中指定的区域名称（也称为源地址）。因为 named.conf 文件指定的区域名称为 zach.net，你可以将第一行重写为：

```
zach.net. IN SOA ns.zach.net. mgs@sobell.com. .
```

host 工具在指定的每个秒数上返回与第一种格式更接近的内容：
$ host -t so zach.net
zach.net. SOA ns.zach.net. mgs@sobell.com. 03111 28800 7200 2419200 86400

TXT 将字符字符串与域名关联。Name 字段持有域名。data 可以包含多达 256 个字符并必须包含引号内。TXT 记录可以包含任何任意文本值。作为通用信息，它们可用于公钥分发等事项。以下是一个指定公司名称的 TXT 资源记录：

```
zach.net IN TXT "Sobell Associates Inc."
```

# DNS 查询与响应

一个 DNS 查询有三个部分：

1. 域名、FQDN（完全限定域名）或用于反向域名解析的 IP 地址
2. Type（类型）——请求的记录类型（第 827 页）
3. Class（类）——互联网始终为 IN

大多数 DNS 服务器在缓存内存中存储其他 DNS 服务器的查询响应。当 DNS 服务器接收到查询时，它首先尝试从缓存解析查询。如果尝试失败，服务器可能会查询其他服务器以获取答案。由于 DNS 使用缓存，当你对 DNS 记录进行更改时，更改需要时间——有时需要几天——才能传播到整个 DNS 层次结构。

响应 查询发送的 DNS 消息可以包含以下记录：

- Header record（头部记录）——关于此消息的信息
- Query record（查询记录）——重复查询
- Answer records（回答记录）——回答查询的资源记录
- Authority records（权威记录）——对答案具有权威性的服务器记录
- Additional records（附加记录）——额外的资源记录，如 NS 记录

dig 工具不会咨询 /etc/switch.conf（第 475 页）来决定查询哪个服务器。以下示例使用 dig 查询 DNS 服务器。+all 选项导致 dig 查询所有记录。

# DNS 简介 831

```
$ dig +all ubuntu.com
;; <<>> DIG 9.0-P1 << +all ubuntu.com
;; global options: +cmd
;; Got answer:
;; --HEADER-- opcode: QUERY, status: NOERROR, id: 51842
;; flags: qr rd: 1, ANSWER: 1, AUTHORITY: 3, ADDITIONAL: 3

;; QUESTION SECTION:
ubuntu.com.                IN      A

;; ANSWER SECTION:
ubuntu.com.               600    IN      A       91.189.94.156

;; AUTHORITY SECTION:
ubuntu.com.               50715   IN      NS      ns2.canonical.com
ubuntu.com.               50715   IN      NS      ns3.canonical.com
ubuntu.com.               50715   IN      NS      ns1.canonical.com

;; ADDITIONAL SECTION:
sns1.canonical.com.       78819   IN      A       91.189.94.173
ns2.canonical.com.       78819   IN      A       91.189.94.219
sns3.canonical.com.       78819   IN      A       209.6.3.210
```

# 反向域名解析

除了普通的解析外，DNS 还提供了反向解析（也称为反向或反映射），以便你可以根据 IP 地址查找域名。由于正向 DNS 数据库中的资源记录是按域名分级索引的，DNS 无法在该域上通过 IP 进行高效搜索。

DNS 通过名为 in-addr.arpa (IPv4) 和 ip6.int (IPv6) 的特殊域名实现反向解析。这些域名中的资源记录持有 IP 地址字段；这些记录按 IP 地址分级索引。Data 字段持有这些 IP 地址对应的 FQDN。

反向解析可以验证某人是否如其所言或位于其所在的域名。通常，它允许服务器检索为其提供服务的客户端域名。例如，合法邮件包含发送者的域名和发送机的 IP 地址。邮件服务器可以通过检查与 IP 地址关联的域名来验证声明的域名。反向解析也可用于匿名 FTP 服务器验证用于密码的电子邮件域名是否合法。

例如，为了确定下页图 24-5 中 IP 地址 82.211.81.150 对应的域名，解析器将查询 DNS 关于 150.81.211.82.in-addr.arpa 域的信息。

# 832 第 24 章 DNS/BIND：跟踪域名和地址

img/45ff4cd21497435daa35084a84b95d07_882_0.png

**图 24-5** 反向解析与 in-addr.arpa 域

