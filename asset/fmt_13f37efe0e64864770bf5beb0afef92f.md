
```
:: ANSWER SECTION:
30.232.187.66.in-addr.arpa. 539 IN PTR ftp.redhot.com.
```

在这种情况下，IP 地址 `66.187.232.30` 对应的主机名正好是 `ftp.redhot.com`。

你也可以使用 `host` 程序查询 DNS。`host` 程序以紧凑格式输出。例如，这里是 `host` 查找主机名 IP 地址的典型用法：

```
host www.google.com
```

这生成了以下单行：

```
www.google.com has address 142.250.1
```

默认情况下，`host` 打印 IP 地址和任何 MX 记录（这些记录列出了这些记录）。对于反向查找，使用 `-t` 选项并配合 IP 地址，如下：

`host` 打印 IP 地址和任何 MX 记录（这些记录列出了这些记录）。对于反向查找，使用 `-t` 参数并配合 IP 地址：

在这种情况下，`host` 打印对应 IP 地址的主机名。`google.com` 是 `host` 的响应如下：

```
google.com
google.com is an alias for google.com.
```

# 第八卷 第 5 章 设置 DNS

## 678 配置 DNS

* 下方的指令。之前的 BIND 版本总是使用 53 端口提问

* 请求，但 BIND 8.1 默认使用非权端口。

```
// query-source address * port 53;
);
//
// 缓存名称服务器配置
//
controls {
  inet 127.0.0.1 allow (localhost); keys (rndckey);
  zone "*" IN {
    type hint;
    file "named.ca";
  };
}
zone "localhost" IN {
  type master;
  file "localhost.zone";
  allow-update none;
}
zone "0.0.0.27.in-addr.arpa" IN {
  type master;
  file "named.local";
  allow-update none;
}
```

注释采用 C 风格 (`/* */`) 或 C++ 风格 (带有 `//`)。该文件包含用大括号(`{...}`) 包围的块语句，并以分号 (`;`) 结束。块语句又包含其他语句，每个语句都以分号结尾。

此 `/etc/named.conf` 文件以 `options` 块语句开始，包含多个 `option` 语句。`directory` 选项语句告知去哪里查找配置文件行中出现的所有其他文件。在这种情况下，named 在 `/var/named` 目录中查找文件。

`/etc/named.conf` 中的 `controls` 语句包含信息，使得 `rndc` 命令可以通过 953 端口连接到 `named` 服务并与其交互。在这种情况下，`controls` 语句包含以下行：

`inet 127.0.0.1 allow (localhost); keys (rndckey);`

这表示 `rndc` 可以名为 `rndc` 的密钥从 `localhost` 连接（文件 `/etc/rndc.key` 定义了密钥和使用的加密算法）。

## 679 配置 DNS

`rndc`（远程守护进程控制）工具是旧版 `ndc`（名称守护进程控制器）工具的继承者，后者通过特殊的控制通道（named 监听消息的 TCP 端口）发送消息来控制 `named` 服务器。`rndc` 工具使用加密密钥来向 `named` 服务器进行身份验证。`named` 服务器拥有相同的加密密钥，它可以解码由 `rndc` 发送的认证信息。

在 `options` 语句之后：

`/etc/named.conf` 中的两个 `zone` 语句是主区域（master zones）。互联网类区域（由 `IN` 关键字指示）的主区域语句语法如下：

```
zone "zone-name" IN {
    type <type>;
    file "zone-file";
    [其他可选语句...]
}
```

`zone-name` 是区域名称，`zone-file` 是包含该区域资源记录 (RR) —— 即数据库条目的区域文件。我将在接下来的两个章节中描述区域格式和资源记录格式。

### 区域文件格式

区域文件通常以若干指令开始，每个指令都以美元符号 (`$`) 开头，后跟一个关键字。两个常用的指令是 `$TTL` 和 `$ORIGIN`。

例如，该行

`$TTL 86400`

使用 `$TTL` 指令为后续未定义 TTL 的记录设置默认生存时间 (TTL)。该值单位为秒，有效的 TTL 范围在 0 到 2147483647 秒之间。在这种情况下，该指令将默认 TTL 设置为 86400 秒（或一天）。

`$ORIGIN` 指令设置附加到任何未限定记录末后的域名。例如，以下 `$ORIGIN` 指令将域名设置为 `localhost`：

```
$ORIGIN localhost:
```

# 配置 DNS

如果没有 `$ORIGIN` 指令，则初始的 `$ORIGIN` 与 `/etc/named.conf` 文件中 `zone` 关键字后面的区域名称相同。

在指令之后，区域文件包含一个或多个资源记录。这些记录遵循特定的格式，该格式将在下一节中概述。

# 资源记录 (RR) 格式

在理解并智能地处理区域文件之前，你必须理解资源记录的格式。每个资源记录都具有以下格式（可选字段显示在方括号中）：

```
[domain] [ttl] [class] type data [:comment]
```

字段由制表符或空格分隔，并可能包含某些特殊字符，例如用于域名的 `@` 符号和表示注释开始的分号 (`;`)。

第一个字段必须从行的第一个字符开始，标识域名。你可以使用 `@` 符号使用 `$ORIGIN` 作为此记录的域名。如果你对同一个域名有多个记录，请将第一个字段留空。可选的 `ttl` 指定了生存时间（Time To Live）——数据可以被缓存并视为有效的时长。你可以使用以下格式之一指定时长：

- N，其中 N 是数字，表示 N 秒

- NW，其中 N 是数字，表示 N 周

- ND，其中 N 是数字，表示 N 天

- NH，其中 N 是数字，表示 N 小时

- NM，其中 N 是数字，表示 N 分

- NS，其中 N 是数字，表示 N 秒

字母 W, D, H, M, 和 S 也可以小写。因此，你可以写 `86400` 或 `ID` (或 `id`) 来表示一天的时长。

## 配置 DNS 683

`/named/named.ca` 文件

关于根域名服务器的信息位于 `/var/named/named.ca` 文件，如 `/etc/named.conf` 文件中根区域（root zone）语句中所指定的。以下列表显示了来自 Red Hat Linux 系统的 `/var/named/named.ca`：

- 此字段包含了初始化互联网域名服务器缓存所需的根域名服务器信息。

- （例如，在 BIND 域名服务器的 "cache" 配置文件中引用此文件）。

- 该文件由 InterNIC 通过匿名 FTP 提供。

file /domain/named.cache

server /FTP.INTERNIC.NET

- 最后更新日期：2002年11月5日

根区域相关版本：2002110501

- 曾名为 NS.INTERNIC.NET

| A.ROOT-SERVERS.NET | 3600000 NS | A.ROOT-SERVERS.NET. |

| | 3600000 A | 198.41.0.4 |

- 曾名为 NS1.ISI.EDU

| B.ROOT-SERVERS.NET | 3600000 NS | B.ROOT-SERVERS.NET. |

| | 3600000 A | 128.90.0.107 |

- 曾名为 C.PSI.NET

| C.ROOT-SERVERS.NET | 3600000 NS | C.ROOT-SERVERS.NET. |

| | 3600000 A | 192.33.4.12 |

- 曾名为 TERP.MD.EDU

| D.ROOT-SERVERS.NET | 3600000 NS | D.ROOT-SERVERS.NET. |

| | 3600000 A | 128.8.10.90 |

- 曾名为 NS.NASA.GOV

| E.ROOT-SERVERS.NET | 3600000 NS | E.ROOT-SERVERS.NET. |

| | 3600000 A | 192.203.230.10 |

- 曾名为 NS1.ISC.ORG

| F.ROOT-SERVERS.NET | 3600000 NS | F.ROOT-SERVERS.NET. |

| | 3600000 A | 192.5.5.241 |

- 曾名为 NS.NIC.DDN.MIL
