
# 配置 DNS

## 配置缓存名称服务器

此行表示 IP 地址 127.0.0.1 被分配给了主机名 `lnbp200`、`localhost.localdomain` 和 `localhost`。

在最新的 Linux 内核版本——即使用 GNU C 库版本 2（glibc 2）或更高版本的内核——中，名称服务切换（NSS）文件 `/etc/nsswitch.conf` 控制了解析器库、NIS、NIS+ 以及 `/etc/hosts` 和 `/etc/shadow` 等本地文件等服务的交互方式。例如，`/etc/nsswitch.conf` 文件中的以下 `hosts` 条目指定了解析器库先尝试 `/etc/hosts` 文件，然后尝试 NIS+，最后尝试 DNS：

```
hosts:          files nisplus dns
```

若要了解关于 `/etc/nsswitch.conf` 文件及其功能的更多信息，请在终端窗口中输入 `man nsswitch.conf`。

一个简单但实用的名称服务器，它会通过（使用其他名称服务器）查找主机名查询的答案，然后记住该答案（将其保存在缓存中）以便下次需要时使用。这种缓存名称服务器可以缩短访问最近访问过的主机所需的时间；因为答案已经在缓存中了。

当你安装 BIND 时，缓存名称服务器的配置文件也会随之安装。这意味着你无需太多操作即可开始运行缓存名称服务器。本节介绍配置文件以及启动缓存名称服务器需要执行的操作。

### /etc/named.conf 文件

你需要第一个配置文件是 `/etc/named.conf`。（实际上，这是 Fedora Core 和 SUSE 中的文件名；在 Debian、MEPIS、Ubuntu 和 Xandros 中，BIND 配置文件被称为 `/etc/bind/named.conf`。）named 服务器在启动时读取此配置文件。如果你安装了 BIND，你应该已经有这个文件。以下是一个来自 Fedora Core 的 `/etc/named.conf` 文件：

```
options {
    directory "/var/named";
    dump-file "/var/named/data/cache_dump.db";
    statistics-file "/var/named/data/named_stats.txt";
    /*
     * If there is a firewall between you and nameservers you want
     * to talk to, you might need to uncomment the query-source
     * directive below.  Previous versions of BIND always asked
     * questions using port 53, but BIND 8.1 uses an unprivileged
     * port by default.
     */
    // query-source address * port 53;
};

//
// a caching only nameserver config
//
controls {
    inet 127.0.0.1 allow { localhost; } keys { rndckey; };
};
zone "." IN {
    type hint;
    file "named.ca";
};

zone "localdomain" IN {
    type master;
    file "localdomain.zone";
    allow-update { none; };
};

zone "localhost" IN {
    type master;
    file "localhost.zone";
    allow-update { none; };
};

zone "0.0.127.in-addr.arpa" IN {
    type master;
    file "named.local";
    allow-update { none; };
};

zone "0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.ip6.arpa" IN {
    type master;
    file "named.ip6.local";
    allow-update { none; };
};

zone "255.in-addr.arpa" IN {
    type master;
    file "named.broadcast";
    allow-update { none; };
};

zone "0.in-addr.arpa" IN {
    type master;
    file "named.zero";
    allow-update { none; };
};

include "/etc/rndc.key";
```

注释可以是 C 风格（`/* . . . */`）或 C++ 风格（以 `//` 开头）。该文件包含由花括号（`{ . . . }`）包围并以分号（`;`）终止的块语句。块语句反过来又包含其他语句，每个语句都以分号结尾。

此 `/etc/named.conf` 文件以一个 options 块语句开头，其中包含多个 option 语句。directory option 语句告诉 named 在配置文件的 file 行中查找所有其他文件的位置。在这种情况下，named 会在 /var/named 目录中查找文件。

![](img/11709a8f88c8cd03868a929dc94c0e2b_674_0.png)

在 SUSE 中，/etc/named.conf 中的 directory option 指向 /var/lib/named 目录，这意味着所有其他 BIND 配置文件都在 /var/lib/named 中。在 Debian 和 Xandros 中，配置文件被明确指定位于 /etc/bind 目录中。

![](img/11709a8f88c8cd03868a929dc94c0e2b_674_1.png)

/etc/named.conf 中的 controls 语句包含安全信息，以便 rndc 命令可以连接到 named 服务的 953 端口并与 named 交互。在这种情况下，controls 语句包含以下行：

```
inet 127.0.0.1 allow { localhost; } keys { rndckey; };
```

此命令表示 rndc 可以使用名为 rndc 的密钥从 localhost 连接。（/etc/rndc.key 文件定义了密钥和使用的加密算法。）

![](img/11709a8f88c8cd03868a929dc94c0e2b_674_2.png)

rndc（远程名称守护进程控制）实用程序是较旧的 ndc（用于名称守护进程控制器）实用程序的后继者，后者用于通过向 named 服务器发送消息来控制它，该消息通过一个特殊控制通道发送，即 named 监听消息的 TCP 端口。rndc 实用程序使用加密密钥向 named 服务器进行身份验证。named 服务器拥有相同的加密密钥，因此可以解码 rndc 发送的身份验证信息。

在 options 语句之后，/etc/named.conf 文件包含多个 zone 语句，每个语句都包含在花括号中并以分号结尾。每个 zone 语句定义一个区域。第一个区域名为 .（根区域）；它是一个提示区域（hint zone），指定了根名称服务器。（当 DNS 服务器启动时，它使用提示区域找到一个根名称服务器，并获取最新的根名称服务器列表。）

/etc/named.conf 中的接下来两个 zone 语句是主区域（master zones）。（主区域仅仅是某个域的数据的主副本。）互联网类区域（由 IN 关键字指示）的主区域语句的语法如下：

```
zone "zone-name" IN {
type master;
file "zone-file";
[...其他可选语句...]
};
```

*zone-name* 是区域的名称，*zone-file* 是包含该区域的资源记录（RR）——即数据库条目——的区域文件。我将在接下来的两节中介绍区域文件格式和资源记录格式。

### 区域文件格式

区域文件通常以多个指令开头，每个指令都以美元符号（$）开头，后跟一个关键字。两个常用指令是 $TTL 和 $ORIGIN。

例如，这一行

```
$TTL		86400
```

使用 $TTL 指令为后续未定义 TTL 的记录设置默认的生存时间（Time To Live，TTL）。值以秒为单位，有效的 TTL 范围是 0 到 2147483647 秒。在这种情况下，该指令将默认 TTL 设置为 86400 秒（或一天）。

$ORIGIN 指令设置要附加到任何未限定记录上的域名。例如，以下 $ORIGIN 指令将域名设置为 localhost：

```
$ORIGIN localhost.
```

如果没有 $ORIGIN 指令，初始 $ORIGIN 将与 */etc/named.conf* 文件中 zone 关键字后的区域名称相同。

在指令之后，区域文件包含一个或多个资源记录。这些记录遵循特定的格式，我将在下一节中概述。

### 资源记录（RR）格式

在理解区域文件并智能地操作之前，你必须理解资源记录的格式。每个资源记录具有以下格式。（可选字段用方括号表示。）

```
[domain]  [ttl]  [class] type data [;comment]
```

字段之间用制表符或空格分隔，并且可能包含一些特殊字符，例如用于域名的 @ 符号和用于指示注释开始的分号（;）。

第一个字段必须从行的第一个字符开始，它标识域名。你可以使用 @ 符号为当前记录使用当前的 $ORIGIN 作为域名。如果你为同一个域名有多个记录，请将第一个字段留空。

可选的 ttl 字段指定生存时间——数据可以缓存并被视为有效的时间段。你可以使用以下格式之一指定时间段：

- **N**，其中 *N* 是一个数字，表示 *N* 秒
- **Mw**，其中 *M* 是一个数字，表示 *M* 周
- **Md**，其中 *M* 是一个数字，表示 *M* 天
- **Mh**，其中 *M* 是一个数字，表示 *M* 小时
- **Mm**，其中 *M* 是一个数字，表示 *M* 分钟
- **Ms**，其中 *M* 是一个数字，表示 *M* 秒

字母 **w**、**d**、**h** 和 **s** 也可以是小写的。因此，你可以写 `86400` 或 `1d`（或 `1D`）来表示一天的时间段。你也可以组合这些来指定更精确的时间段，例如 `5w6d1h` 表示 5 周、6 天和 1 小时。

**class** 字段指定网络类型。此字段最常用的值是表示 Internet 的 **IN**。

资源记录中的下一个字段是 *type* 字段，它表示记录的类型（例如 **SOA**、**NS**、**A** 或 **PTR**）。表 5-1 列出了 DNS 资源记录类型。数据字段接下来出现，具体取决于类型字段。

| 类型 | 名称 | 描述 |
| :--- | :--- | :--- |
| **A** | 地址 | 指定与主机名对应的 IPv4 地址 |
| **AAAA** | IPv6 地址 | 指定与名称对应的 IPv6 主机地址 |
| **AS** | (非标准/常见) | *注意：原文列出的 "AS" 为 "Address"，但上下文暗示 "A"。然而，仔细查看标准 DNS 表格，"A" 是 Address。"AAAA" 是 IPv6。"NS" 是 Name Server。让我们仔细重新检查 OCR 文本。* |
| **CERT** | 数字证书 | 保存数字证书 |
| **CNAME** | 规范名称 | 定义主机名的昵称或别名 |
| **DNAME** | 委派名称 | 用另一个名称替换指定的域名以进行查找 |
| **HINFO** | 主机信息 | 标识主机的硬件和操作系统 |
| **KEY** | 公钥 | 保存与 DNS 名称关联的公钥 |

*（待续）*
