
字段由制表符或空格分隔，并可能包含一些特殊字符，例如用于域名的 `@` 符号和表示注释开始的分号 (`;`)。

第一个字段，必须从行的第一个字符开始，标识域名。您可以使用 `@` 符号为此记录使用当前的 `$ORIGIN` 作为域名。如果您有针对相同域名名的多个记录，请留第一个字段为空。

可选的 `ttl` 字段指定生存时间（Time To Live）——数据可以被缓存并视为有效的时间长度。您可以使用以下任一格式指定持续时间：

- `$N$`，其中 `$N$` 是表示 `$N$` 秒的数字
- `$Mw$`，其中 `$M$` 是表示 `$M$` 周的数字
- `$Md$`，其中 `$M$` 是表示 `$M$` 天的数字
- `$Mh$`，其中 `$M$` 是表示 `$M$` 小时的数字
- `$Mm$`，其中 `$M$` 是表示 `$M$` 分钟的数字
- `$Ms$`，其中 `$M$` 是表示 `$M$` 秒的数字

字母 `$W, D, H, M$` 和 `$S$` 也可以是小写的。因此，您可以写 `86400` 或 `1D`（或 `1d`）来表示一天的持续时间。您还可以将这些组合起来指定更精确的持续时间，例如 `5w6d1h16m` 表示 5 周、6 天、1 小时和 16 分钟。

`class` 字段指定网络类型。该字段最常用的值是 `$IN$`，代表 Internet。

资源记录中的下一个是 `*type*` 字段，它表示记录的类型（例如 `$SOA$`、`$NS$`、`$A$` 或 `$PTR$`）。表 5-1 列出了 DNS 资源记录类型。接下来是数据字段，它取决于 `*type*` 字段。

### 表 5-1 DNS 资源记录类型

| Type | Name | Description |
| :--- | :--- | :--- |
| A | IPv4 Address | 指定与主机名对应的 IPv4 地址 |
| AAAA | IPv6 Address | 指定与名称对应的 IPv6 主机地址 |
| AS | Address | 指定与主机名对应的 IP 地址 |
| CERT | Digital Certificate | 保存数字证书 |
| CNAME | Canonical Name | 定义主机名的昵称或别名 |
| DNAME | Delegation Name | 用另一个要查找的名称替换指定的域名 |
| HINFO | Host Info | 标识主机的硬件和操作系统 |
| KEY | Public Key | 保存与 DNS 名称关联的公钥 |

### 表 5-1（续）

| 类型 | 名称 | 描述 |
| :--- | :--- | :--- |
| MX | 邮件交换器 | 识别接受发往特定域名的邮件的主机（用于路由电子邮件） |
| NS | 名称服务器 | 标识区域的权威名称服务器 |
| PTR | 指针 | 指定地址对应的名称（用于反向映射——将 IP 地址转换为主机名） |
| RP | 负责人 | 提供域名的技术联系人姓名 |
| SIG | 签名 | 包含在安全 DNS 中经过认证的数据（详细信息参见 RFC 2535） |
| SOA | 权威开始 | 表示后续所有记录对该区域均为权威 |
| SRV | 服务 | 列出域名提供的知名网络服务 |
| TXT | 文本 | 用于在 DNS 数据库中包含注释和其他信息 |

请阅读区域文件中的资源记录，至少包括类型 `SOA`、`NS`、`A`、`PTR` 和 `MX` 的记录，这些是最常用的几种类型。（您可以在 Debian 和 Xandros 的 `/etc/bind` 目录、Fedora Core 的 `/var/named` 目录以及 SUSE 的 `/var/lib/named` 目录中找到区域文件。）接下来，我将简要描述这些记录，并通过示例说明每种记录类型。

典型的 `SOA` 记录具有以下格式：

```
@   1D IN SOA     @ root (
                    42      ; serial
                    3h      ; refresh -- 3 hours
                    15m     ; retry -- 15 minutes
                    1w      ; expiry -- 1 week
                    1D )    ; minimum -- 1 day
```

第一个字段指定域名为 `@`，这意味着当前域名（默认为区域名称，如在 `/etc/named.conf` 文件中所示）。下一个字段指定该记录的生存时间（TTL）为一 天。类字段设置为 `IN`，表示该记录用于互联网。类型字段指定记录类型为 `SOA`。其余字段构成了 `SOA` 记录的数据。数据包括主名称服务器的名称（在此情况下为 `@`，即当前域名）、技术联系人的电子邮件地址，以及括号内的五个不同时间值。

`NS` 记录指定区域的权威名称服务器。典型的 `*NS*` 记录如下所示：

```
. 3600000 IN NS A.ROOT-SERVERS.NET.
```

在这种情况下，`*NS*` 记录列出了根区域的权威名称服务器。（请注意，第一个字段的名称是一个点。）`*生存时间*` 字段指定该记录的有效性为 1000 小时（3600000 秒）。`*类*` 为 `*IN*`，代表互联网；`*记录类型*` 为 `*NS*`。最后一个字段列出了名称服务器的名称（`*A.ROOT-SERVERS.NET.*`），以点结尾。

`*A*` 记录指定名称对应的地址。例如，以下 `*A*` 记录显示 `*A.ROOT-SERVERS.NET.*` 的地址为 `*198.41.0.4*`：

```
A.ROOT-SERVERS.NET. 3600000 A 198.41.0.4
```

在这种情况下，未指定网络类，因为该字段是可选的，默认值为 `*IN*`。

`*PTR*` 记录用于反向映射——将地址转换为名称。考虑以下示例：

```
1 IN PTR localhost.
```

该记录来自一个名为 `*0.0.127.in-addr.arpa*` 的区域文件。因此，该记录表示与地址 `*127.0.0.1*` 关联的名称是 `*localhost*`。

`*MX*` 记录指定代表特定域接受邮件的主机名称。例如，这是一个典型的 `*MX*` 记录：

```
naba IN MX 10 mailhub.lnbsfott.com.
```

该记录表示发往当前域名中名为 `*naba*` 的主机的邮件将发送到 `*mailhub.lnbsfott.com*`。（该主机被称为 `*邮件交换器*`。）数字 10 是优先级值。对于具有不同优先级值的多个 `*MX*` 记录列表，会先尝试优先级值较低的那些。

掌握了一些关于资源记录的知识后，您可以浏览缓存名称服务器的区域文件。

## 根区域文件

关于十三个根名称服务器的信息位于 `*/etc/named.conf*` 文件中根区域区域语句引用的区域文件中。

（在 Fedora Core 中，根区域文件是 `/var/named/named.ca`；在 Debian、MEPIS、Ubuntu 和 Xandros 中是 `/etc/bind/db.root`；在 SUSE 中是 `/var/lib/named/root.hint`。）以下列表展示了根区域文件：

```
This file holds the information on root name servers needed to
initialize cache of Internet domain name servers
(e.g. reference this file in the "cache . <files>"
configuration file of BIND domain name servers).
This file is made available by InterNIC
under anonymous FTP as
file       /domain/named.cache
on server    FTP.INTERNIC.NET
-OR-         RS.INTERNIC.NET
last update:  Jan 29, 2004
related version of root zone:   2004012900
; formerly NS.INTERNIC.NET
       3600000      IN  NS  A.ROOT-SERVERS.NET.
A.ROOT-SERVERS.NET.   3600000      A 198.41.0.4
; formerly NS1.ISI.EDU
       3600000      NS  B.ROOT-SERVERS.NET.
B.ROOT-SERVERS.NET.   3600000      A 192.228.79.201
; formerly C.PSI.NET
       3600000      NS  C.ROOT-SERVERS.NET.
C.ROOT-SERVERS.NET.   3600000      A 192.33.4.12
; formerly TERP.UMD.EDU
```
