
```
options {
  directory "/var/named";
  dump-file "/var/named/data/cache_dump.db";
  statistics-file "/var/named/data/named_stats.txt";
  /*
   * If there is a firewall between you and name servers you want
   * to talk to, you might need to uncomment the query-source
   * directive below. Previous versions of BIND always asked
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
zone "0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.ip6.arpa" IN {
```

```
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

注释采用 C 风格（`/* ... */`）或 C++ 风格（以 `//` 开头）。文件包含用大括号（`{ ... }`）括起并以分号（`;`）结束的块语句。块语句本身又包含其他语句，每个语句以分号结束。

这个 `/etc/named.conf` 文件以包含若干选项语句的 `options` 块语句开始。`directory` 选项语句告诉 `named` 在配置文件各行中出现的其他文件查找位置。在本例中，`named` 在 `/var/named` 目录中查找文件。

![](img/322157d1fa7d965f05bcd68ed0ffc36b_285_0.png)

在 SUSE 中，`/etc/named.conf` 中的 `directory` 选项指向 `/var/lib/named` 目录，这意味着所有其他 BIND 配置文件都位于 `/var/lib/named`。在 Debian 中，配置文件被明确指定在 `/etc/bind` 目录中。

![](img/322157d1fa7d965f05bcd68ed0ffc36b_285_1.png)

`/etc/named.conf` 中的 `controls` 语句包含安全信息，以便 `rndc` 命令能够连接到端口 953 上的 `named` 服务并与之交互。在本例中，`controls` 语句包含以下行：

```
inet 127.0.0.1 allow { localhost; } keys { rndckey; };
```

该命令表示 `rndc` 可以使用名为 `rndc` 的密钥从 `localhost` 连接。（文件 `/etc/rndc.key` 定义了要使用的密钥和加密算法。）

![](img/322157d1fa7d965f05bcd68ed0ffc36b_285_2.png)

`rndc`（remote name daemon control，远程名称守护进程控制）实用程序是旧的 `ndc`（name daemon controller，名称守护进程控制器）实用程序的继任者，后者通过专用控制通道向 `named` 服务器发送消息来控制 `named` 服务器，该通道是一个 `named` 监听消息的传输控制协议（TCP）端口。`rndc` 实用程序使用加密密钥向 `named` 服务器进行身份验证。`named` 服务器拥有相同的加密密钥，以便能够解码 `rndc` 发送的身份验证信息。

在 `options` 语句之后，`/etc/named.conf` 文件包含多个 `zone` 语句，每个语句都用大括号括起并以分号结束。每个 `zone` 语句定义一个区域。第一个区域名为 `.`（根区域）；它是一个提示区域，用于指定根名称服务器。（当 DNS 服务器启动时，它使用提示区域查找根名称服务器并获取最新的根名称服务器列表。）

`/etc/named.conf` 中的接下来两个 `zone` 语句是主区域。（主区域是域数据的 `master` 副本。）Internet 类区域（由 `IN` 关键字表示）的主区域语句的语法如下：

```
zone "zone-name" IN {
type master;
file "zone-file";
[ ... other optional statements ... ]
};
```

`zone-name` 是区域的名称，`zone-file` 是包含该区域资源记录（RR）——数据库条目——的区域文件。接下来两个章节描述区域文件格式和 RR 格式。

## 区域文件格式

区域文件通常以指令开始，每个指令都以美元符号（`$`）后跟关键字开头。两个常用的指令是 `$TTL` 和 `$ORIGIN`。

行

```
$TTL 86400
```

使用 `$TTL` 指令为后续未定义 TTL 的记录设置默认生存时间（TTL）。该值以秒为单位，有效 TTL 范围为 0 到 2147483647 秒。在本例中，该指令将默认 TTL 设置为 86400 秒（即一天）。

`$ORIGIN` 指令设置附加到任何未限定记录的域名。下面的 `$ORIGIN` 指令将域名设置为 `localhost`：

```
$ORIGIN localhost.
```

如果不存在 `$ORIGIN` 指令，则初始 `$ORIGIN` 与 `/etc/named.conf` 文件中 `zone` 关键字后的区域名称相同。

在指令之后，区域文件包含一个或多个 RR。这些记录遵循特定格式，将在下一节中概述。

## RR 格式

在能够理解并智能地操作区域文件之前，必须先理解 RR 的格式。每个 RR 具有以下格式（方括号中显示可选字段）：

```
[domain] [ttl] [class] type data [;comment]
```

字段由制表符或空格分隔，可能包含一些特殊字符，例如用于域的 `@` 和用于表示注释开始的分号（`;`）。

第一个字段必须从行的第一个字符开始，用于标识域名。可以使用 `@` 来使用当前 `$ORIGIN` 作为此记录的域名。如果同一域名有多个记录，请将第一个字段留空。

可选的 `ttl` 字段指定 TTL——数据可以被缓存并被视为有效的持续时间。您可以按以下格式之一指定持续时间：

- N，其中 N 为秒数

- NW，其中 N 为周数

- ND，其中 N 为天数

- NH，其中 N 为小时数

- NM，其中 N 为分钟数

- NS，其中 N 为秒数

字母 W、D、H、M 和 S 也可以小写。因此，您可以输入 86400 或 1D（或 1d）来表示一天的持续时间。您还可以组合这些字母以指定更精确的持续时间，例如 5w6d16h 表示 5 周、6 天和 16 小时。

`class` 字段指定网络类型。该字段最常用的值是 `IN`，表示 Internet。

RR 中接下来是 `type` 字段，表示记录的类型（如 `SOA`、`NS`、`A` 或 `PTR`）。表 5-1 列出了 DNS RR 类型。接下来是 `data` 字段，其内容取决于 `type` 字段。

阅读区域文件中的 RR——至少是 `SOA`、`NS`、`A`、`PTR` 和 `MX` 类型，它们是最常用的类型之一。（您可以在 Debian 的 `/etc/bind` 目录、Fedora 的 `/var/named` 目录以及 SUSE 的 `/var/lib/named` 目录中找到区域文件。）接下来是对这些记录的简要描述，通过示例说明每种记录类型。

## 表 5-1 DNS RR 类型

| 类型 | 名称 | 描述 |

|------|------|-------------|
