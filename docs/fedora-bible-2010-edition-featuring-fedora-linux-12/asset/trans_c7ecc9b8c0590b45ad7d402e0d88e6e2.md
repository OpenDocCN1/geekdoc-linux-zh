
互联网向 DNS 服务器（`ns1.yourdomain.com`）请求地址，它们将获取地址 `123.45.67.89`。然而，当查询 `ns1.yourdomain.com` 的请求来自局域网内部时，返回的地址是 `10.0.0.1`。此外，任何来自互联网的对私有计算机地址（如 `red.yourdomain.com`、`blue.yourdomain.com` 等）的查询都会被拒绝。

## 编辑 named.conf

首先，你需要配置代表你的示例域名 `yourdomain.com` 的主 DNS 服务器上的 `/var/named/chroot/etc/named.conf` 文件。此示例从 Fedora 中随 caching-nameserver 包提供的 `/etc/named.conf` 文件开始。（请确保在继续之前安装 caching-nameserver 和 BIND 软件包，并为你编辑的任何配置文件创建备份副本。）以下是关于 `named.conf` 文件的一些提示：

- 如果语句包含子语句，请确保在最后一个子语句末尾加上分号。
- 注释可以采用流行编程语言使用的格式。这些语言包括 C（以 `/*` 开始并以 `*/` 结束）、C++（以 `//` 开始并持续到物理行的末尾）以及 shell 或 Perl 风格（从 `#` 开始并持续到物理行的末尾）。
- 开头的感叹号 (!) 用于取反某个元素。在语句中放入 `!123.45.67.89` 会导致 IP 地址 `123.45.67.89` 不匹配该元素。（只需确保取反发生在正向匹配之前，否则正向匹配将优先。）

`/var/named/chroot/etc/named.conf` 文件的编辑版本如下：

```
options {
	directory "/var/named";
	dump-file "/var/named/data/cache_dump.db";
	statistics-file "/var/named/data/named_stats.txt";
};

acl "mylan" {
	127/8; 10.0.0.0/24;
};

controls {
	inet 127.0.0.1 allow { localhost; } keys { rndckey; };
};

view "inside" {
	match-clients { "mylan"; };
	recursion yes;

	zone "." IN {
		type hint;
		file "named.ca";
	};

	zone "0.0.10.in-addr.arpa" IN {
		type master;
		file "yourlan.db";
	};

	zone "yourdomain.com" {
		type master;
		file "db.yourdomain.com.inside";
		allow-transfer { 10.0.0.2; };
	};
};

view "outside" {
	match-clients { any; };
	recursion no;

	zone "." IN {
		type hint;
		file "named.ca";
	};

	zone "yourdomain.com" {
		type master;
		file "db.yourdomain.com.outside";
		allow-transfer { 123.45.67.2; };
	};
};

include "/etc/rndc.key";
```

`options` 定义位于 named.conf 文件的开头，并指定 `/var/named` 目录为区域文件所在的存放位置。`acl` 行定义了 `mylan` 访问控制列表，它由 10.0.0.0 本地私有网络上的主机计算机和 localhost (127/8) 组成。（有关 IP 地址格式、CIDR 和子网掩码的信息，请参阅第 14 章。）你在 `0.0.10.in-addr.arpa` 区域中使用此定义，以仅允许局域网上的用户执行对局域网内计算机名称的反向查找。

`controls` 部分表明，rndc 命令（用于启动、停止以及更改 named 服务）只能从 localhost 运行。文件末尾的 `include` 语句指明了 rndc 密钥的位置。named 启动脚本 (`service` named start) 会调用 rndc 命令，因此你很少需要直接使用 rndc 命令。

DNS 服务器被分为两个视图：内部（inside）和外部（outside）。内部视图定义了如何处理来自私有局域网和 localhost（如在 mylan 中定义）的请求的 IP 地址解析。通过开启递归（recursion yes），named 守护程序将允许局域网上的任何计算机向任何域名（甚至是本地 DNS 服务器不控制的域名）发起名称服务器查询。外部视图定义了如何处理来自其他所有地方（通常是互联网）的查询。通过关闭递归（recursion no），仅响应其他名称服务器对本地 DNS 服务器所控制域名的查询。关于其他域名的信息请求将以未找到的消息被拒绝。（关闭递归有助于消除一种常见的攻击，即攻击者诱导你的服务器去从攻击者控制的 DNS 服务器获取信息。）

named.conf 文件中的每个区域条目描述了该计算机对该区域服务器的类型（此处除了根区域外，所有情况都是主服务器），包含该区域记录的数据库文件（位于 named 目录中），以及与区域记录相关的其他选项。named.ca 文件默认为你设置好。它标识了互联网根服务器的位置。

我为这个示例制作了其他区域（yourlan.db, db.yourdomain.com.inside, db.yourdomain.com.outside, 和 0.0.10.in-addr.arpa）。对于“内部”视图，yourlan.db 文件让你的局域网中的计算机执行反向地址查找（即通过 IP 地址查询获取名称）。db.yourdomain.com.inside 文件包含你域名中所有计算机的名称和地址（包括本地局域网上的那些）。该域名内部视图的 DNS 从属服务器位于 10.0.0.2。（你局域网中的客户端将在 /etc/resolv.conf 中使用 10.0.0.1 和 10.0.0.2 作为 DNS 服务器。）

对于“外部”视图，db.yourdomain.com.outside 文件包含你希望公开的域中计算机的名称和 IP 地址（你私有局域网上的计算机被排除在外）。该域名外部视图的 DNS 从属服务器是 123.45.67.2。请注意，位于 123.45.67.2 的服务器担任 FTP 服务器和 DNS 从属服务器双重角色。

请注意，每个区域都指向 named 目录中的一个区域文件。表 24-1 显示了每个区域在 named 目录中指向的文件。

## 表 24-1: DNS 示例中的区域和相关区域文件

| 区域 | 区域文件（位于 /var/named/chroot/var/named 目录中） |
|---|---|
| . （代表互联网根服务器的单个点） | named.ca |
| 0.0.10.in-addr.arpa | yourlan.db |
| yourdomain.com（内部视图） | db.yourdomain.com.inside |
| yourdomain.com（外部视图） | db.yourdomain.com.outside |

编辑 named.conf 文件时要非常小心。忘记加一个分号太容易了，结果会导致整个文件无法加载。为了确保 named.conf 文件不包含任何语法错误，你可以运行以下命令（作为 root 用户）：

```
# named-checkconf
```

如果存在语法错误，消息将指出有问题的行，并告知你该处似乎有什么错误。如果语法正确，请继续在 /var/named 目录中创建区域文件。

## 设置区域文件（内部）

/var/named/chroot/var/named 目录包含 /var/named/chroot/etc/named.conf 文件所指向的区域文件。对于这个示例，你只需要从头创建三个区域文件。你可以（也应该）保持 named.ca 文件不变。

域名服务器的大部分实际工作都在区域文件中完成。在示例中，db.yourdomain.com.inside 文件包含 yourdomain.com 域的基本记录，包括所有私有名称和地址。以下是该文件的一个示例：

```
$TTL    86400
@       IN  SOA  yourdomain.com. hostmaster.yourdomain.com.
(
        2009042701    ; Serial
        28800         ; Refresh
        14400         ; Retry
        3600000       ; Expire
        86400 )       ; Minimum

; Name servers
        IN   NS      ns1.yourdomain.com.
        IN   NS      ns2.yourdomain.com.

; Mail server for domain
        IN   MX   10   mail.yourdomain.com.

; Public servers
ns1     IN   A      10.0.0.1
ns2     IN   A      10.0.0.2
mail    IN   A      123.45.67.2
www     IN   A      123.45.67.3
ftp     IN   A      123.45.67.4

; Private clients on the LAN
red     IN   A      10.0.0.2
blue    IN   A      10.0.0.3
green   IN   A      10.0.0.4
yellow  IN   A      10.0.0.5

; EOF
```
