
## MX

```text
speedy    IN      MX      10 mail
                     MX      20 mail.sam.net.
```

## NS

### 名称服务器

指定为域名提供服务（DNS 记录）的系统名称。名称（`Name`）字段存储域名；数据（`Data`）字段存储 DNS 服务器的名称。每个域名必须至少有一个 `NS` 记录。DNS 服务器不需要位于该域名内，实际上，如果至少有一个服务器不位于该域名内会更好。系统名称 `ns` 通常用于指定名称服务器，但这不是必须的，除了帮助人类识别名称服务器外，该名称没有特殊含义。以下资源记录指定 `ns.max.net.` 作为区域中 `peach` 的名称服务器：

```text
peach     IN      NS      ns.max.net.
```

## PTR

### 指针

将 IP 地址映射到域名，用于反向名称解析。名称（`Name`）字段存储 IP 地址；数据（`Data`）字段存储域名。不要将 `PTR` 资源记录与别名一起使用。以下资源记录将反向区域中的 `3`（例如，在 `0.168.192.in-addr.arpa` 区域中，`3` 代表 `192.168.0.3`）映射到区域中的 `peach`：

```text
3         IN      PTR     peach
```

有关更多信息，请参阅第 831 页的“反向名称解析”。

## SOA

### 授权开始

指定区域的开始部分。每个区域必须恰好有一个 `SOA` 记录。权威服务器维护其负责区域的 `SOA` 记录。

所有区域文件必须有一个 `SOA` 资源记录，并且它必须是文件中的第一个资源记录。名称（`Name`）字段存储区域开始处的域名。数据（`Data`）字段存储创建数据的主机名称、负责该区域的人员的电子邮件地址，以及以下信息，如果记录无法放在一行上，这些信息必须用括号括起来。如果这些信息用括号括起来（通常如此），则开括号必须出现在 `SOA` 记录的第一个物理行上：

- `serial`：范围为 1 到 2,147,483,647 的值。此数字的变化表明区域数据已更改。按照惯例，此字段设置为字符串 `yyyy-mm-dd`（年、月、日、变更编号）。除了日期外，最后两位数字——即变更编号——在每次更改 `SOA` 记录时都应该递增。

- `refresh`：主服务器通知从（辅助）服务器刷新记录经过的时间；两次更新之间的时间间隔。

- `retry`：刷新失败后在再次尝试刷新前等待的时间。

- `expire`：经过此时间后，区域不再具有权威性，必须查询根服务器。过期时间仅适用于从服务器。

- `minimum`：`负缓存`（第 1161 页）的 `TTL`，即不存在域名错误（`NXDOMAIN`）可以在从服务器缓存中保留的时间。`负缓存` `TTL` 与普通 `TTL` 相同，只是它适用于不存在的域名，而不是存在的域名。

`$TTL` 指令（第 839 页）指定默认区域 `TTL`（数据保留在从服务器缓存中的最长时间）。默认区域 `TTL` 和 `负缓存` `TTL` 共同涵盖了服务器可以生成的所有类型的响应。如果你将经常添加子域或修改现有域，请将 `负缓存` `TTL` 设置为较低的值。较短的 `TTL` 会增加请求不存在域名的客户端到 DNS 的流量，但允许新域名快速传播，尽管代价是流量增加。

以下两个 `SOA` 资源记录是等效的（第一个记录中的括号是可选的，因为该记录可以放在一个物理行上）：

```text
@ IN SOA ns.zach.net. mgs@sobel11.com. ( 2010111247 8H 2H 4W 1D )
@ IN SOA ns.zach.net. mgs@sobel11.com.
2010111247 ; serial
8H ; refresh
2H ; retry
4W ; expire
1D ) ; minimum
```

第二种格式更具可读性，因为其布局和注释。`SOA` 资源记录开头的 `at` 符号（`@`）代表在 `named.conf` 文件中指定的区域名称（也称为源）。由于 `named.conf` 文件指定区域名称为 `zach.net`，你可以将第一行重写为如下形式：

```text
zach.net.   IN    SOA          ns.zach.net.  mgs@sobel11.com. (
```

`host` 工具返回的内容更接近第一种格式，其中每个时间都以秒为单位指定：

```text
$ host -t soa zach.net
zach.net.   SOA ns.zach.net. mgs@sobel11.com. 03111 28800 7200 2419200 86400
```

## TXT

### 文本

将字符串与域名关联。`Name` 字段存储域名。数据字段最多可以包含 256 个字符，并且必须用引号括起来。`TXT` 记录可以包含任意文本值。除了通用信息外，它们还可以用于公共密钥分发等用途。以下是一个指定公司名称的 `TXT` 资源记录：

```text
zach.net.   IN    TXT "Sobel1 Associates Inc."
```

## DNS 查询和响应

### 查询

DNS 查询由三部分组成：

1. `Name`——域名、`FQDN` 或用于反向名称解析的 IP 地址

2. `Type`——请求的记录类型（第 827 页）

3. `Class`——对于 Internet 类始终为 `IN`

`缓存`：大多数 DNS 服务器在缓存内存中存储来自其他 DNS 服务器的查询响应。当 DNS 服务器收到查询时，它首先尝试从缓存中解析查询。如果该尝试失败，服务器可能会查询其他服务器以获取答案。由于 DNS 使用缓存，当你对 DNS 记录进行更改时，该更改需要一段时间——有时长达几天——才能在 DNS 层级中传播。

### 响应

作为查询响应的 DNS 消息可以包含以下记录：

- `Header` 记录——关于此消息的信息

- `Query` 记录——重复查询内容

- `Answer` 记录——回答查询的资源记录

- `Authority` 记录——对答案具有权威的服务器资源记录

- `Additional` 记录——附加资源记录，例如 `NS` 记录

`dig` 工具不会咨询 `etc/nsswitch.conf`（第 475 页）来确定要查询哪个服务器。以下示例使用 `dig` 查询 DNS 服务器。`--all` 选项使 `dig` 查询所有记录。

# 反向名称解析

除了常规的正向名称解析，DNS 还提供`反向名称解析`（也称为`逆映射`或`反向映射`），允许你根据 IP 地址查找域名。由于正向 DNS 数据库中的资源记录是按域名层级索引的，DNS 无法在该数据库上基于 IP 地址进行高效搜索。

DNS 通过名为 `in-addr.arpa`（IPv4）和 `ip6.int`（IPv6）的特殊域来实现反向名称解析。这些域中的资源记录具有包含 IP 地址的名称字段；这些记录是按 IP 地址层级索引的。数据字段包含与这些 IP 地址对应的 `FQDN`（完全限定域名）。

反向名称解析可以验证某人是否为其声称的身份，或者至少是否属于其声称的域。通常，它允许服务器检索并记录为其提供服务的客户端的域名。例如，合法邮件包含发件人的域名和发送主机的 IP 地址。邮件服务器可以通过检查与 IP 地址关联的域来验证发件人声明的域。反向名称解析还可用于匿名 FTP 服务器，以验证在用作密码的电子邮件地址中指定的域是否合法。

例如，为了确定与下一页图 24-5 中 IP 地址 `82.211.81.150` 对应的域名，解析器会向 DNS 查询名为 `150.81.211.82.in-addr.arpa` 的域的信息。

![](img/2344fc4a798f29dca9e8b5ed7288171a_882_0.png)

以下示例使用 `dig` 查询 DNS 中与 `www.sobell.com` 对应的 IP 地址，即 `209.157.128.22`。第二行命令使用 `dig` 实用程序查询相同的 IP 地址，将其反转并附加 `.in-addr.arpa`（`22.128.157.209.in-addr.arpa`）以显示一个 `PTR` 资源记录（第 828 页）。结果资源记录的数据部分是原始查询中的域名：`www.sobell.com`。

```bash
$ dig www.sobell.com

; QUESTION SECTION:
;www.sobell.com.      IN     A

; ANSWER SECTION:
www.sobell.com.      2274   IN     A     209.157.128.22

$ dig 22.128.157.209.in-addr.arpa PTR

; QUESTION SECTION:
;22.128.157.209.in-addr.arpa. IN PTR

; ANSWER SECTION:
22.128.157.209.in-addr.arpa. 2244 IN PTR www.sobell.com.
```

除了像前面的例子那样重新格式化 IP 地址外，你还可以使用 `dig` 的 `-x` 选项执行反向查询：

```bash
$ dig -x 209.157.128.22

; QUESTION SECTION:
;22.128.157.209.in-addr.arpa. IN PTR

; ANSWER SECTION:
22.128.157.209.in-addr.arpa. 2204 IN PTR www.sobell.com.
```

或者，你可以直接使用 `host`：

```bash
$ host 209.157.128.22
22.128.157.209.in-addr.arpa domain name pointer www.sobell.com.
```

# DNS 的工作原理

应用程序程序不直接发出 DNS 查询，而是使用 `gethostbyname()` 系统调用。系统如何得出对应的 IP 地址对于调用程序来说是透明的。`gethostbyname()` 调用会检查 `/etc/nsswitch.conf`（第 475 页）中的 `hosts` 行，以确定它应该检查哪些文件以及/或者应该查询哪些服务，以及按什么顺序获取与域名对应的 IP 地址。当它需要查询 DNS 时，本地系统（即 DNS 客户端）通过调用本地系统上的解析器库来查询 DNS 数据库。此调用将所需信息返回给应用程序。

##### 更多信息

- [`DNS` for Rocket Scientists](https://www.zytrac.com/books/dns) 是一个出色的网站，它很好地利用了链接，以非常易于消化的形式呈现有关 DNS 的信息。相同的也可在 `Pro DNS and BIND` 书籍中找到。

- 本地：`Bind 管理员参考手册`：`/usr/share/doc/bind9-doc/arm/Bv9ARM.html`。

- Web：`DNS for Rocket Scientists`：`www.zytrac.com/books/dns`

- `BIND`：`www.isc.org/products/BIND`

- DNS 安全：`www.sans.org/reading_room/whitepapers/dns/1069.php`（可下载的 PDF 文件）

- `HOWTO`：`DNS HOWTO`

- 书籍：`DNS & BIND`，第五版，作者 `Albitz` 与 `Liu`，`O'Reilly & Associates`（2006 年 5 月）

- `Pro DNS and BIND`，第一版，作者 `Ron Aitchison`，`Apress`（2005 年 8 月）

###### 笔记

- `DNS` 和 `named` 术语：DNS 服务器的名称是 `named`。本章中“DNS”和“`named`”互换使用。

- `防火墙`：`named` 服务器通常接受 TCP 和 UDP 端口 53 上的查询。如果服务器系统正在运行防火墙，你需要打开这些端口。使用 `gufw`（第 876 页），通过允许 DNS 服务的策略来打开此端口。

- `chroot` 监狱：`bind-chroot.sh` 脚本设置 `named` 在 `chroot` 监狱中运行。运行此脚本后，所有控制 `BIND` 的文件都位于此监狱内。在这种情况下，本章中使用的文件名是 `chroot` 监狱中文件的符号链接。更多信息参见第 847 页。

`named` 选项 `/etc/default/bind9` 文件随 `resolvconf` 包安装。如果安装了此包，当 `bind9` 初始化脚本启动或重新启动 `named` 服务器时（但不仅仅是重新加载配置文件时），它会读取 `/etc/default/bind9` 文件中的选项。如果 `RESOLVCONF` 变量设置为 `yes`（默认值），脚本将运行 `resolvconf`，从而重建 `/etc/resolv.conf`。你可以通过将 `RESOLVCONF` 设置为 `no` 来使脚本不运行 `resolvconf`。`-u bind` 选项使 `named` 作为用户 `bind` 运行。

```bash
$ cat /etc/default/bind9
# run resolvconf?
RESOLVCONF=yes

# startup options for the server
OPTIONS="-u bind"
```

# 设置 DNS 服务器

本节从解释如何设置最简单类型的 DNS 服务器——DNS 缓存开始。

## 先决条件

- `安装` 安装以下软件包：

  - `bind9`（自动安装 `bind9utils`）

  - `bind9-doc`（可选；安装 `bind` 文档）

  - `dnsutils`（默认安装；包括 `dig`、`nslookup` 和 `nsupdate`）

`bind9` 初始化脚本 安装 `BIND9` 软件包时，`dpkg` `postinst` 脚本会启动 `named` 守护进程。配置 `BIND` 后，调用 `bind9` 初始化脚本以启动 `named` 守护进程：

```bash
$ sudo service bind9 restart
```

在活动服务器上更改 `BIND` 配置后，使用 `reload` 代替 `restart` 来重新加载 `named` 配置文件，而不会干扰连接到服务器的客户端。默认情况下，启动或重新启动（但不是重新加载）`named` 会运行 `resolvconf`，从而重建 `/etc/resolv.conf` 文件。有关更多信息，请参见上面的“`named` 选项”。

## 快速入门：设置 DNS 缓存

如前所述，DNS 缓存是解析器和权威 DNS 服务器之间的桥梁：它不是权威的，只是将其查询结果存储在内存中。大多数 ISP 为其客户提供 DNS 缓存。在本地设置缓存可以减少局域网和外部世界之间的流量，从而改善响应时间。虽然可以在局域网上的每个系统上设置 DNS 缓存，但在局域网设置单个 DNS 缓存可以防止局域网上的多个系统不得不向远程服务器查询相同的信息。

安装 `BIND` 后，你已准备好运行大部分仅缓存的名称服务器。有关此名称服务器使用哪些文件以及其工作原理的解释，请参见第 839 页的“设置 DNS 缓存”。

在启动 DNS 缓存之前，你需要修改 `/etc/resolv.conf` 文件（第 496 页）。如何修改此文件取决于 `resolvconf` 包是否已安装并设置为在本地系统上运行。当你输入命令 `resolvconf` 时，如果显示用法消息，说明该包已安装；如果显示 `not installed` 消息，则说明它未安装。

如果 `resolvconf` 未安装，或者你已按照“`named` 选项”中的说明将其关闭，请在 `/etc/resolv.conf` 中，在其他 `nameserver` 行之前添加以下行：

```
nameserver 127.0.0.1
```

如果 `resolvconf` 已安装并设置为在运行 `bind9` `init` 脚本（第 834 页）时重建 `resolv.conf`，请将上述行放入 `/etc/resolvconf/resolv.conf.d/head` 文件中，放在注释之后、其他 `nameserver` 行之前。你可以忽略提示不要编辑该文件的注释：此注释是针对尝试编辑 `/etc/resolv.conf` 的人的。你必须将此行放入 `head` 文件中，以便 `resolvconf` 在任何其他 `nameserver` 行之前将其放入 `resolv.conf`；否则，本地 DNS 缓存将永远不会被使用。如有需要，将其他 `nameserver` 行放入同一目录下的 `base` 文件中。

`nameserver` 行告诉解析器将本地系统（`localhost` 或 `127.0.0.1`）用作主要名称服务器。若要尝试使用本地系统作为唯一的名称服务器，请在 `resolv.conf` 或 `base` 中注释掉其他 `nameserver` 行，方法是每行前面加上井号（`#`）。

最后，运行 `bind9` `init` 脚本以重启 `named` 守护进程（第 834 页）。这样做时，如果 `resolvconf` 已安装并设置为运行，`bind9` `init` 脚本将重建 `resolv.conf`。有关 `resolv.conf` 的更多信息，请参阅 `resolver` 和 `resolv.conf` 的手册页。

参考第 849 页的“`Troubleshooting`”（故障排除）部分，了解如何确认 DNS 缓存是否正常工作。一旦重启了 `named`，你可以通过使用 `dig` 查询远程系统的 IP 地址来查看缓存的效果：

```
$ dig www.ubuntu.com
```
