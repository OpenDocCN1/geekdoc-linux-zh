
**指针（Pointer）** 将 IP 地址映射到域名，用于反向解析。`Name` 字段持有 IP 地址；`Data` 字段持有域名。不要对别名使用 `PTR` 资源记录。以下资源记录映射

# DNS 简介

在反向区域中的 3（例如，`0.168.192.in-addr.arpa` 区域中的 3 是 `192.168.0.3`）对应于区域中的 `peach`：

```
3 IN PTR peach
```

更多信息请参阅第 831 页的“反向域名解析”。

`SOA`（起始起始记录）指定区域的开始。每个区域必须恰好有一个 `SOA` 记录。权威服务器维护其所权威区域的 `SOA` 记录。
所有文件必须有一个 `SOA` 资源记录，且该记录必须是文件中的第一个资源。`Name`（名称）字段包含区域起始处的域名。`Data`（数据）字段包含创建该主机的主机、负责区域的人员电子邮件地址以及以下信息，如果记录无法在一行内，这些信息必须包含在括号内。如果这些信息包含在括号内（通常如此），左括号必须出现在 `SOA` 记录的第一个物理行：

- `serial`（序列号）范围在 1 到 2,147,483,647 之间。此数字的变化表示区域发生了变化。按照惯例，此字段被设置为字符串 `yyyymmddann`（年、月、日、变更次数）。与日期一起，每次你更改 `SOA` 记录时，都应该增加最后两位——即变更天。

- `refresh`（刷新）：在主主服务器通知从服务器（备用服务器）刷新记录后经过的时间；以及它们之间更新的时间间隔。

- `retry`（重试）：在刷新失败后，尝试再次刷新之前等待的时间。

- `expire`（过期）：在区域不再具有权威性且必须查询根服务器后经过的时间。`expire` 仅适用于从服务器。

- `minimum`（最小 TTL）：负缓存（缓存 `NXDOMAIN TTL`）的 TTL，即不存在的域名错误（`NXDOMAIN`）在从服务器缓存中保留的时间。负缓存 TTL 与普通 TTL 相同，不同之处在于适用于不存在的域名，而不是存在的域名。

`TTL` 指令（第 839 页）定义了区域 TTL（从服务器缓存中保留记录的最长天数）。默认区域 TTL 和负 TTL 共同涵盖了服务器可以生成的所有类型记录。如果你将频繁地添加域名或修改现有域名，请将负 TTL 设置为较小的值。短 TTL 会增加请求不存在域名的客户端的 DNS 流量，但允许域名快速传播，尽管是以增加流量为代价。

两个 `SOA` 资源记录是等效的（第一条记录中的括号是可选的，因为记录适合单行物理行）：

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

由于布局和注释，第二种格式更具可读性。`SOA` 资源记录中的 `@` 符号代表在 `named.conf` 文件中指定的区域名称（也称为源地址）。因为 `named.conf` 文件指定的区域名称为 `zach.net`，你可以将第一行重写为：

```
zach.net. IN SOA ns.zach.net. mgs@sobell.com. .
```

`host` 工具在指定的每个秒数上返回与第一种格式更接近的内容：

```
$ host -t so zach.net
zach.net. SOA ns.zach.net. mgs@sobell.com. 03111 28800 7200 2419200 86400
```

`TXT` 将字符字符串与域名关联。`Name` 字段持有域名。`data` 可以包含多达 256 个字符并必须包含引号内。`TXT` 记录可以包含任何任意文本值。作为通用信息，它们可用于公钥分发等事项。以下是一个指定公司名称的 `TXT` 资源记录：

```
zach.net IN TXT "Sobell Associates Inc."
```

# DNS 查询与响应

一个 DNS 查询有三个部分：

1. 域名、`FQDN`（完全限定域名）或用于反向域名解析的 IP 地址
2. `Type`（类型）——请求的记录类型（第 827 页）
3. `Class`（类）——互联网始终为 `IN`

大多数 DNS 服务器在缓存内存中存储其他 DNS 服务器的查询响应。当 DNS 服务器接收到查询时，它首先尝试从缓存解析查询。如果尝试失败，服务器可能会查询其他服务器以获取答案。由于 DNS 使用缓存，当你对 DNS 记录进行更改时，更改需要时间——有时需要几天——才能传播到整个 DNS 层次结构。

响应查询发送的 DNS 消息可以包含以下记录：

- `Header record`（头部记录）——关于此消息的信息
- `Query record`（查询记录）——重复查询
- `Answer records`（回答记录）——回答查询的资源记录
- `Authority records`（权威记录）——对答案具有权威性的服务器记录
- `Additional records`（附加记录）——额外的资源记录，如 `NS` 记录

`dig` 工具不会咨询 `/etc/switch.conf`（第 475 页）来决定查询哪个服务器。以下示例使用 `dig` 查询 DNS 服务器。`+all` 选项导致 `dig` 查询所有记录。

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

DNS 通过名为 `in-addr.arpa` (IPv4) 和 `ip6.int` (IPv6) 的特殊域名实现反向解析。这些域名中的资源记录持有 IP 地址字段；这些记录按 IP 地址分级索引。`Data` 字段持有这些 IP 地址对应的 `FQDN`。

反向解析可以验证某人是否如其所言或位于其所在的域名。通常，它允许服务器检索为其提供服务的客户端域名。例如，合法邮件包含发送者的域名和发送机的 IP 地址。邮件服务器可以通过检查与 IP 地址关联的域名来验证声明的域名。反向解析也可用于匿名 `FTP` 服务器验证用于密码的电子邮件域名是否合法。

例如，为了确定下页图 24-5 中 IP 地址 `82.211.81.150` 对应的域名，解析器将查询 DNS 关于 `150.81.211.82.in-addr.arpa` 域的信息。

# 832 第 24 章 DNS/BIND：跟踪域名和地址

![图 24-5 反向解析与 in-addr.arpa 域](img/45ff4cd21497435daa35084a84b95d07_882_0.png)

**图 24-5** 反向解析与 `in-addr.arpa` 域

# DNS 简介 833

```
;; QUESTION SECTION:

;;22.18.157.209-in-addr.arpa.   IN PTR
```

```
;; ANSWER SECTION:

;;22.18.157.209-in-addr.arpa. 2204 IN PTR   www.sobell.com.

...
```

或者，你也可以直接运行：

```
$ host 209.157.128.22
22.128.157.209-in-addr.arpa domain name pointer www.sobell.com.
```

# DNS 工作原理

应用程序并不直接发布 DNS 查询，而是使用 `gethostbyname()` 系统调用。系统会得出相应的 IP 地址，且对调用程序是透明的。`gethostbyname()` 会调用 `/etc/hosts.conf`（第 475 页）中的 `hosts` 行来确定它应该检查哪些文件以及/或查询哪些服务，以及以什么种顺序获取与域名对应的 IP 地址。当需要查询 DNS 时，本地系统（即 DNS 客户端）会通过调用本地系统上的解析库来查询 DNS 数据库。这会将所需信息返回给应用程序。

### 更多信息

《Rocket Scientists 的 DNS》是一个非常出色的网站，它很好地利用链接以非常易懂的形式呈现了 DNS 信息。同样的信息在《Pro DNS and BIND》一书中也可以找到。

- 本地 `Bind` 员参考手册：`/usr/share/doc/bind9-doc/arm/Bv9ARM.html`。

- 为火箭科学家提供的 Web DNS：`www.zytract.com/books/dns`
  `BIND`: DNS 安全：`www.sans.org/reading_room/whitepapers/dns/1069.php`（可下载的 PDF 文件）

- 《HOWTO Book DNS & BIND》，第五版，Albitz & Liu 著，O'Reilly & Associates 出（2006年5月）
  《Pro DNS and BIND》，第一版，Ron Aitchison 著，Apress 出（2005年8月）

# 注意事项

- 术语：DNS 服务器的名为 `named`。本章将“DNS”和“`named`” DNS 以及 `named` 互换使用。

- 防火墙：服务器通常接受 `TCP` 和 `UDP` 端口 53 的查询。如果系统正在运行防火墙，你需要开放这些端口。使用 `gufw`（第 876 页），通过设置允许 DNS 服务的策略来开放此端口。

- `chroot` 监狱：`bind-chroot.sh` 脚本在 `chroot` 监狱中设置 `named`。在你运行此脚本后，所有控制 `BIND` 的文件都位于监狱内部。在这种情况下，本章中使用的文件是指向 `chroot` 监狱中文件的符号链接。更多信息请见第 847 页。

# 834 第 24 章 DNS/BIND：跟踪域名和地址

`/etc/default/bind9` 文件随 `resolveconf` 软件包安装。如果安装了该软件包（会自动安装 `bind9` 初始化脚本），在启动或重启 `named` 服务器时（但在重新加载配置文件时不会），该脚本会读取 `/etc/default/bind9` 文件中的选项。如果 `RESOLVCONF` 变量设置为 `yes`（默认即如此），脚本将运行 `resolveconf`，从而重新构建 `/etc/resolv.conf`。你可以通过将 `RESOLVCONF` 设置为 `no` 来导致脚本不运行 `resolveconf`。`-u bind` 选项导致以用户 `bind` 的身份运行。

```
$ cat /etc/default/bind9

# run resolveconf?

RESOLVCONF=yes

# 服务器选项设置
OPTIONS="-u bind"
```

# 设置 DNS 服务器

本节始于解释如何设置最简单的 DNS 服务器，即 DNS 缓存。

# 前提条件

安装以下软件包：

- `bind9utils`
- `bind9-doc`（可选；安装 `bind` 文档）
- `dnsutils`（默认安装；包含 `dig`, `nslookup` 和 `nsupdate`）

- `bind9` 初始化脚本：当你安装 `bind9` 软件包时，`dpkg postinst` 脚本启动 `named` 守护进程。在配置 `BIND` 后，调用 `bind9` 初始化脚本来重启 `named` 守护进程：

```
$ sudo service bind9 restart
```

在服务器上更改 `BIND` 配置后，使用 `reload` 代替 `restart` 来重新加载配置文件而不干扰客户端。默认情况下，启动或重启——而不是重新加载——`named resolvconf`，这将重新构建 `/etc/resolv.conf`。更多信息见上面的“`named` options”。

# 跳转：设置 DNS 缓存

如前所述，DNS 缓存是解析器和权威服务器之间的桥梁：它不是权威的，而仅仅是在内存中存储查询结果。大多数 `ISP` 为客户提供 DNS 缓存。设置本地缓存可以减少局域网（`LAN`）与外部世界的流量。虽然可以在局域网内的任何系统上设置 DNS 缓存，但在局域网上设置单个 DNS 缓存可以防止局域网内的多个系统向远程服务器查询相同的信息。

安装 `BIND` 后，你就拥有了一个可以运行的仅缓存服务器。参考第 839 页的“设置 DNS 缓存”以了解该服务器如何工作。

# 设置 DNS 服务器

`resolv.conf`：在启动 DNS 缓存之前，你需要修改 `/etc/resolv.conf` 文件（第 496 页）。如何修改此文件取决于 `resolv-conf` 软件包是否在本地系统中安装并设置。当你给出命令 `resolvconf` 时，使用信息表示已安装，而信息表示未安装。

如果没有安装 `resolv-conf` 或你按照“`named` options”所述关闭了它，请在 `/etc/resolv.conf` 中的其他 `nameserver` 行之前加入以下行：

```
nameserver 127.0.0.1
```

如果 `resolv-conf` 已安装并设置为在运行 `bind9` 初始化脚本（第 834 页）时重新构建 `resolv-conf`，请在 `/etc/resolv.conf` 的 `head` 部分（即任何其他 `nameserver` 行之前）加入注释。如果你忽略了不要编辑 `/resolv.conf` 的注释，该注释是写给尝试编辑它的人看的。你必须将其放在 `head` 文件中，以便 `resolv-conf` 将其放在任何其他 `nameserver` 行之前。`nameserver` 行告诉解析器使用本地系统（`localhost` 或 `127.0.0.1`）作为主 DNS。要实验使用本地系统作为唯一的 DNS，请在 `resolv.conf` 中的其他 `nameserver` 行前加上注释符号 (#)。

最后，运行 `bind9` 脚本启动 `named` 守护进程（第 834 页）。当你这样做时，如果 `resolv-conf` 已安装并设置为运行，`bind9` 初始化脚本将重新构建 `resolv-conf`。关于 `resolv.conf` 的更多信息请见 `resolver` 和 `resolv.conf` 手页。

参考第 849 页的“故障排除”以确认 DNS 缓存正在工作。一旦你重启了 `named`，就可以使用 `dig` 查找远程系统的 IP 地址来查看缓存的效果：

```
$ dig www.ubuntu.com

<<>> DIG 9.7.0-P1 <<>> www.ubuntu.com

;; global options: +cmd

;; Got answer:

;;;>>HEADER-- opcode: QUERY, status: NOERROR, id: 19622

;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:

www.ubuntu.com.	IN	A

;; ANSWER SECTION:

www.ubuntu.com.	2204	IN	A	93.184.216.34

;; Query time: 496 msec

;; SERVER: 127.0.0.1#53(127.0.0.1)

;; WHEN: Mon Apr 5 16:45:38 2010

;; MSG SIZE received: 512
```

上一页示例的倒数第四行显示此查询花费了 496 毫秒（约半秒）。当你再次运行相同的查询时，由于缓存将信息保存在本地内存中，运行速度会快得多：

```
$ dig www.ubuntu.com

:: Query time: 1 msec

;; SERVER: 127.0.0.1#53(127.0.0.1)

;; WHEN: Mon Apr 5 16:45:46 2010
```
