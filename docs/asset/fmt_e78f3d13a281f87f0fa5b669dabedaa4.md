
可选的 `ttl` 字段指定生存时间（Time To Live）——数据可以缓存并被认为有效的持续。你可以使用以下格式之一指定持续时间：

- `N`，其中 `N` 是秒
- `NW`，其中 `N` 是周
- `ND`，其中 `N` 是天
- `NH`，其中 `N` 是小时
- `NM`，其中 `N` 是分钟
- `NS`，其中 `N` 是秒

字母 `W`, `D`, `H`, `M`, 和 `S` 可以写成小写。因此，你可以写成 `86400` 或 `1D`（或 `1d`）来表示一天的持续时间。你还可以组合字母来指定更精确的持续时间，例如用 `5w6d16h` 表示 5 周、6 天和 16 小时。

`class` 字段指定网络类型。最常用的值是 `IN`，代表 Internet。

资源记录中的下一个是 `type` 字段，它表示记录的类型（如 `SOA`, `NS`, `A` 或 `PTR`）。表 6-1 列出了 DNS 资源记录类型。接下来是 `data` 字段，其内容取决于 `type` 字段。

### 表 6-1 DNS 资源记录类型

| 类型 | 名称 | 说明 |
|---|---|---|
| A | IPv4 到 IPv6 转换地址 | 使用适用于从 IPv4 到 IPv6 转换的格式指定与名称对应的 IPv6 地址 |
| AAAA | IPv6 地址 | 指定与名称对应的 IPv6 主机地址 |
| AS | 地址 | 指定与主机名对应的 IP 地址 |

# 配置 DNS

| 类型 | 名称 | 说明 |
| --- | --- | --- |
| CERT | 数字证书 | 持有数字证书 |
| CNAME | 规范名称 | 为主机名定义别名或昵号 |
| DNAME | 委托名称 | 将指定的域名替换为另一个要查找的名称 |
| HINFO | 主机信息 | 识别主机的硬件和操作系统 |
| KEY | 公钥 | 存储与 DNS 名称关联的密钥 |
| MX | 邮件交换器 | 识别接收该域邮件的主机（用于路由电子邮件） |
| NS | 服务器 | 识别区域的权威域名服务器 |
| PTR | 指针 | 指定与地址对应的名称（用于反向映射——将地址转换为主机名） |
| RP | 负责人 | 提供提供该域的技术联系人名称 |
| SIG | 签名 | 包含在安全 DNS 中经过认证的数据（详见 RFC 2535） |
| SOA | 权威起始 | 表明后续所有记录对于该区域都是权威的 |
| SRV | 服务 | 列出该域提供的已知网络服务 |
| TXT | 文本 | 在 DNS 中包含注释和其他信息 |

读取区域文件中的资源记录，至少包括 `SOA`、`A`、`PTR` 和 `MX`，这些是最常用的几种记录。（你可以在 Debian 的 `/etc/bind` 目录、Fedora 的 `/var/named` 目录以及 SUSE 的 `/var/lib/named` 目录下找到它们。）接下来通过一个示例对这些记录进行简要描述。一个典型的 `SOA` 记录如下：

```
@ IN SOA root {
4 ; serial
```

# 配置 DNS

```
3H; refresh -- 3 小时
15M; retry -- 15 分钟
1W; expiry -- 1 周
1D; minimum -- 1 天
```

第一个字段指定域 `@`，意味着当前域（默认是区域名称，显示在 `/etc/named.conf` 文件中）。下一个字段指定记录的 TTL。`class` 字段设置为 `IN`，代表 Internet。`type` 字段指定记录类型为 `SOA`。其余字段构成了 `SOA` 记录。数据包括主域名服务器的名称（在此例中为 `@`，或当前域）、技术联系人的电子邮件地址以及括号内的时间。

`NS` 记录指定区域的权威域名服务器。一个典型的 `NS` 记录如下：

`-3600 IN NS A.ROOT-SERVERS.`

在这种情况下，`NS` 记录列出了根的权威域名服务器（注意，Time To Live 字段指定该记录有效为 3600 秒）。`class` 是 `IN`，代表 Internet。`type` 字段指定记录类型为 `NS`。`final` 字段列出了 `A.ROOT-SERVERS.` 的地址。`A` 记录指定与名称对应的 `198.41.0`。

```
A.ROOT-SERVERS.NET 3600 198.41.0
```

在这种情况下，没有指定 `class`，因为默认是 `IN`。`PTR` 记录用于反向映射——将地址转换为名称。考虑以下示例：

`-1 PTR localhost.`

这条记录来自名为 `0.127.in-arpa` 的文件。因此，该记录表示地址 `127.0.0` 对应 `localhost`。

`MX` 记录指定接收该域邮件的主机名称。例如，这里有一个典型的 `MX` 记录：

```
server7 IN 10 mailhub.com
```

# 配置 DNS

此记录表示指向 `server7` 的邮件发送到 `mailhub.com`（这是一个邮件交换器）。`10` 是优先值。对于具有不同优先值的 `MX` 记录，会优先尝试优先值较低的。

有了资源记录的信息，你可以通过区域文件查看缓存域名服务器。

## 根区域文件

Internet 有 13 个根服务器；大多数根服务器位于美国。关于 13 个根服务器的信息位于 `/etc/named.conf` 中 `name` 语句引用的区域文件（Fedora 为 `/var/named/`，Debian 为 `/etc/bind/`，SUSE 为 `/lib/named/`）。以下列表显示了根区域：

- 该文件包含初始化 Internet 缓存服务器所需的根服务器信息（例如在 BIND 配置文件 "file" 中引用此文件）。
- 该文件通过匿名 FTP 在服务器 `INTERNIC.NET` 的 `domain/named.cache` 提供。
- `RS.INTERNIC.NET`
- 最后更新：2004年1月29日
- 根区域版本：2004012900
- 原 `NS.INTERNIC.NET`:
  `360000 IN NS A.ROOT-SERVERS.NET.`
  `A.ROOT-SERVERS.NET. 360000 A 198.41.0.4`
- 原 `NS1.ISI.EDU`:
  `360000 IN B.ROOT-SERVERS.NET.`
  `B.ROOT-SERVERS.NET. 360000 A 192.228.79.201`
- 原 `C.PSI.NET`:
  `360000 IN C.ROOT-SERVERS.NET.`
  `C.ROOT-SERVERS.NET. 360000 A 192.33.4.112`
- 原 `TERP.UMD.EDU`:
  `360000 IN D.ROOT-SERVERS.NET.`
  `D.ROOT-SERVERS.NET. 360000 A 128.8.10.90`
- 原 `NS.NASA.GOV`:
  `360000 IN E.ROOT-SERVERS.NET.`
  `E.ROOT-SERVERS.NET. 360000 A 192.203.230.110`

# 配置 DNS

```
; formerly NS.ISC.ORG
;
 360000 NS F.ROOT-SERVERS.NET
F.ROOT-SERVERS.NET 360000 A 192.5.5.241
;
 formerly NS.NIC.DDN.MIL
;
 360000 NS G.ROOT-SERVERS.NET
G.ROOT-SERVERS.NET 360000 A 192.112.36.4
;
 formerly AOS.ARMY.MIL
;
 360000 NS H.ROOT-SERVERS.NET
H.ROOT-SERVERS.NET 360000 A 128.63.2.53
;
 formerly NS.NORDU.NET
;
 360000 NS I.ROOT-SERVERS.NET
I.ROOT-SERVERS.NET 360000 A 192.36.148.33;
; operated by Verisign, Inc.
; 360000 NS J.ROOT-SERVERS.NET
J.ROOT-SERVERS.NET 360000 A 192.58.128.30;
; operated by RIPE NCC
; 360000 NS K.ROOT-SERVERS.NET
K.ROOT-SERVERS.NET 360000 A 193.0.142.29;
; operated by ICANN
; 360000 NS L.ROOT-SERVERS.NET
L.ROOT-SERVERS.NET 360000 A 198.32.64.12;
; operated by WIDE
; 360000 NS M.ROOT-SERVERS.NET
M.ROOT-SERVERS.NET 360000 A 202.127.33;
 End of File
```
