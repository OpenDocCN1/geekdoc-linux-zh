
在本节的描述中，`IP-list` 是一个用分号分隔的 IP 地址列表，每个 IP 地址后面可选地跟一个斜杠和子网掩码长度（第 529 页）。在 `IP-list` 前加感叹号（`!`）可以对其取反。你可以使用内置名称。在 `named.conf` 中，用井号（`#`）或双斜杠（`//`）指定注释。

## 包含的文件

在本节的描述中，`IP-list` 是一个用分号分隔的 IP 地址列表，每个 IP 地址后面可选地跟一个斜杠和子网掩码长度（第 529 页）。在 `IP-list` 前加感叹号（`!`）可以对其取反。你可以使用内置名称。

## OPTIONS 子句

`Options` 语句可以出现在两个地方：`Options` 子句和区域中。`Options` 子句以关键字 `options` 开头并以括号结尾。

# 25 DNS/BIND：跟踪域名

区域的主体由一对括号括着一个或多个区域子句。以下是一些选项的列表：

- `allow-query [IP-list]`：允许该系统进行查询。如果没有此选项，服务器将响应所有查询。
- `allow-recursion [IP-list]`：指定服务器将为哪些系统执行递归查询。如果没有此选项，服务器将执行迭代查询。
- `allow-transfer [IP-list]`：指定允许执行传输的系统。
- `directory path`：指定包含区域的目录的绝对路径。
- `forwarders [IP [port]]`：指定查询转发到的 IP 地址和可选的端口号。
- `notify YES`：当信息更改时，向该区域的从服务器发送消息。
- `recursion YES`：`YES`（默认）如果客户端请求，则提供递归查询（第 849 页）。`NO`——仅执行迭代查询（第 849 页）。

## ZONE 子句

区域子句定义了一个区域，并可以包含 `Options` 子句列出的任何语句。区域子句由关键字 `zone`、双引号内的区域名称以及类（始终为 `IN`）引入。

- `allow-update [IP-list]`：指定允许动态更新此区域的系统。当你为一个非本地管理员拥有的域名托管主 DNS 服务器时，此语句可能非常有用，它允许远程用户更新 DNS 条目而无需授予用户访问服务器的权限。
- `filename`：指定区域——即指定区域的文件。`filename` 相对于 `Options` 子句中 `directory` 语句指定的目录。对于主区域和提示区域，文件语句是强制性的。对于从区域包含它是一个好主意（见 `type`）。
- `masters (IP-list)`：指定从区域可以使用哪些更新区域。
- `type ztype`：指定由此子句定义的区域类型。从以下列表中选择 `ztype`：
    - `forward`：指定转发区域，它转发指向该区域的查询。参见 `Options` 子句中的 `forward` 和或 `forwarders` 语句。
    - `hint`：指定提示区域。提示区域列出了服务器启动且在缓存中找不到答案时查询的根服务器。
    - `master`：指定本地系统作为该区域的主服务器（第 850 页）。
    - `slave`：指定本地系统作为该区域的从服务器（第 850 页）。

# 区域文件 (ZONE FILES)

区域文件定义了区域特性。区域通常在 `named.conf` 中指定。与 `named.conf` 不同，区域文件在域名的末尾使用句号。示例区域文件请参见第 866 页。

# 时间格式

BIND 文件中的所有时间均以秒为单位，除非后面紧跟着这些字母之一（大写或小写）：`S`（秒）、`M`（分钟）、`H`（小时）、`D`（天）或 `W`（周）。你可以组合这些格式。例如，时间 `2h25m30 seconds` 意味着 2 小时 25 分钟 30 秒，等同于 8,730 秒。

# 域名限定

区域文件中的未限定域名被认为位于当前区域（即由该区域文件定义并引用该区域文件的 `named.conf` 文件命名的区域）。例如，`myzone.com` 区域文件中的名称 `zach` 将扩展为完全限定域名 (FQDN) `zach.myzone.com.`。使用 FQDN（包括句号）来指定不在当前区域的域名。任何不以句号结尾的名称都将被视为当前区域的子域名。

# 区域名称 (ZONE NAME)

在区域文件中，符号 `@` 会被替换为引用该区域文件的 `named.conf` 文件所指定的区域名称。区域名称也称为源 (`ORIGIN`)。请参见下一节中的“ORIGIN”。

# 区域文件指令 (ZONE FILE DIRECTIVES)

区域文件中可以出现以下指令。每个指令都由开头的美元符号 `$` 标识。`$TTL` 指令是强制性的，且必须是区域文件的第一个条目。

- `$TTL` 定义区域内所有资源记录的默认生存时间。此指令必须在它所适用的任何资源记录之前出现在区域文件中。资源记录可以包含一个 TTL 值来覆盖此值，但根区域 (`.`) 中的资源记录除外。
- `$ORIGIN` 将区域名称更改为在 `named.conf` 文件中指定的名称。此名称（或如果区域文件中未出现此指令，则为区域名称）将替换资源记录 `Name` 字段中的 `@` 符号。
- `$INCLUDE` 包含文件，就像它是区域文件的一部分一样。在包含文件中 `$ORIGIN` 指令的作用范围是该包含文件。也就是说，包含文件中的 `$ORIGIN` 指令不会影响持有 `$INCLUDE` 指令的文件。

# DNS 缓存

当你安装 `bind9` 软件包时，会安装一个 DNS 缓存（也称为解析缓存名称服务器）。“JumpStart: Setting Up a DNS Cache (第 858 页)”章节解释了如何运行此服务器。本节描述了 Ubuntu Linux 实现此服务器提供的文件。

# named.conf: named 配置文件

默认的 `named.conf` 文件显示如下：

```
$ cat /etc/bind/named.conf
// 这是用于 BIND DNS 服务器命名的主配置文件。
// 请阅读 /usr/share/doc/bind9/README.Debian.gz 以获取关于
// Debian 中 BIND 配置文件的结构信息，在自定义
// 此配置文件之前进行阅读。
// 如果你只是想添加区域，请在 /etc/bind/named.conf 中进行操作。
include "/etc/bind/named.conf.options"

// 使用根服务器的知识预热服务器
zone "" {
    type hint;
    file "/etc/bind/db.root";
}

//  localhost 的正向和反向区域具有权威性，并根据
// RFC 1912 广播区域
zone "localhost" {
    type master;
    file "/etc/bind/db.local";
}

zone "127.in-addr.arpa" {
    type master;
    file "/etc/bind/db.127";
}

zone "0.in-addr.arpa" {
    type master;
    file "/etc/bind/db.0";
}

zone "255.in-addr.arpa" {
    type master;
    file "/etc/bind/db.255";
}

// zone "com" { type delegation-only; }
// zone "net" { type delegation-only; }
// 根据发布说明：
// 由于我们的许多用户对根域或顶级域提供的未委托
// 回答感到不习惯（除了少数长期以来一直信任并
// 预料这种行为行为的用户外），我们现在引入了
// "root-delegations-only" 功能，该功能将仅限委托
// 逻辑应用于所有顶级域名以及根域名。应该指定一个
// 列表，包括 "MUSEUM" 和 "DE"，并且任何其他
// 来自意外响应的顶级域名都是预期且受信任的。
// root-delegation-only exclude "DE"; "MUSEUM";
```

`include "/etc/bind/named.conf";`

**Options 子句 (Options clause)**：`Options` 子句位于 `named.conf` 中：`named.conf` 通过 `include` 语句包含。

**区域子句 (Zone clauses)**：`named.conf` 文件包含五个区域，每个区域都使用绝对路径来定位其区域文件。此文件中出现的相对文件名将相对于 `named.conf` 中指向的 `/var/cache/bind`。

- （区域名称为一个句号。）提示区域 (`hint zone`)。指定当服务器启动或不知道应查询哪个服务器时，它应该查找 `/etc/bind/db.root` 文件以根域权威服务器的地址。
- `allow-recursion`：在本地系统上设置本地服务器。
- `127.in-addr.arpa`：设置 IPv4 反向解析。
- `0.in-addr.addr`：指定本地服务器处理以 0 开头的 IP 地址的反向查找，防止本地服务器向上游查找信息。
- `255.in-addr.addr`：指定本地服务器处理以 255 开头的 IP 地址的反向查找，防止本地服务器向上游查找信息。

# named.conf: OPTIONS 文件

`named.conf.options` 文件由 `named.conf` 通过 `include` 语句包含，其中主要包含以下未注释的语句：

```
directory "/var/cache/bind"
auth-zone conform to RFC1035
listen-on-v6 { any };
allow-recursion { localnets };
```

`directory` 语句指定了 `named.conf` 中所有路径以及 `named.conf` 中包含的所有其他文件所相对于该目录。如果运行在 chroot 禁闭（chroot jail）中，它位于 `/var/lib/named` 下。`auth` 语句不允许服务器回答 NXDOMAIN；请使用负缓存。`listen-on-v6 { any }` 语句允许服务器在任何地址上监听 IPv6 查询。`allow-recursion { localnets }` 语句允许本地网络执行递归查询。

# 区域文件 (ZONE FILES)

有五个区域文件位于 `/etc/bind/`，每个文件都对应 `named.conf` 中的区域子句。`db.root` 文件与 `named.conf` 中的区域子句类似：`db.root` 描述了根域的权威服务器。根域的权威服务器经常变化，`db.root` 文件初始化根域。如果没有根区域文件，它将不知道去哪里查找根域。

```
$ cat /etc/bind/db.root

DIG 9.2 @a.root-servers.net

 global options:

print: opcode: QUERY, status: NOERROR, id: 18944

flags: qr; QUERY: 1, AUTHORITY: 0

QUESTION SECTION:

IN NS

ANSWER SECTION:

518400 NS A.ROOT.NET.

518400 NS B.ROOT.NET.

518400 NS C.ROOT.NET.

518400 NS D.ROOT.NET.

518400 NS E.ROOT.NET.

518400 NS F.ROOT.NET.

518400 NS G.ROOT.NET.

518400 NS H.ROOT.NET.

518400 NS I.ROOT.NET.

518400 NS J.ROOT.NET.

518400 NS K.ROOT.NET.

518400 NS L.ROOT.NET.

518400 NS M.ROOT.NET.

ADDITIONAL SECTION:

A.ROOT.NET. 360000 A 198.4.0

B.ROOT.NET. 360000 A 192.228.79.201

C.ROOT.NET. 360000 A 192.33.41.12

D.ROOT.NET. 360000 A 128.8.10.90

E.ROOT.NET. 360000 A 192.203.230.10

F.ROOT.NET. 360000 A 192.5.5.241

G.ROOT.NET. 360000 A 192.112.36.4

H.ROOT.NET. 360000 A 128.63.253.3

I.ROOT.NET. 360000 A 192.36.145.17

J.ROOT.NET. 360000 A 192.58.128.30

K.ROOT.NET. 360000 A 193.0.14.129

L.ROOT.NET. 360000 A 198.32.64.12

M.ROOT.NET. 360000 A 202.12.27.33

; Query time: 81 msec

;; SERVER: 198.41.0.4#53(a.root-servers.net)

;; WHEN: Sun Feb 1 11:27:14 2004

;; MSG Size rcvd: 436
```

**db.local.** The `.local` 区域文件定义了 `localhost` 区域，本地系统上的普通服务器。它从 TTL 记录开始，并包含三个资源记录：`SOA`、`NS` 和 `A`。后续文件中定义的 TTL 记录指定了文件中指定的资源记录的默认生存时间为 604,800 秒（一周）：

```bash
$ cat /etc/bind/db.local

; BIND data file for local loopback interface

$TTL    604800    localhost.root.localhost. (
        IN      SOA             1 : Serial
               604800    : Refresh
               86400     : Retry
               2419200    : Expire
               604800 ) : Negative Cache TTL

@       IN      NS        localhost.
@       IN      A       127.0.0.1
```

如前所述，`@` 代表源（区域名称），即在 `named.conf` 中指定的 `localhost`。最后两行是 `NS` 资源记录，它将该区域的名称服务器指定为 `localhost`，而 `A` 记录指定了主机在 `127.0.0.1` 的 IPv4 地址。

**db.127.** The `db.127` 区域文件提供了关于 `127-in-addr.arp` 反向查找区域的信息。它遵循与 `localhost` 区域文件相同的模式，但有一个例外：该文件包含不是 `A` 资源记录，而是 `PTR` 记录，提供与 IP 地址关联的名称。`PTR` 记录指定了名称 `1.0.0`，它将区域 (`127.in-addr.arpa`) 中地址为 `1.0.0` 的系统等同于名称 `localhost`，后者的 IP 地址为 `127.0.0.1`：
