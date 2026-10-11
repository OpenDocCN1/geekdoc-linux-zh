
# CS 反向记录 (128.138.X.X)

```cs
zone "250.138.128.addr.arpa"
type master;
file "reverse/250.138.128";
```

```cs
zone "1.168.192.in-addr.arpa" # 私有地址空间网络
type master;
file "reverse/1.168.192"
allow-query (cnets; rfc1918);
```

# 省略了许多反向区域

```cs
# 从用服务器
zone "colorado.edu" { # colorado.edu 顶级域名
type slave;
file "secondary/colorado.edu";
allow-transfer { none };
masters { 128.138.240.1 };
}
```

```cs
zone "openbsd.org" { # openbackend 项目
type slave;
file "secondary/openbsd.org";
masters { 199.45.131.58 };
}
```

```cs
zone "233-in-addr.arpa" { # 实验性组播地址
type slave;
file "secondary/233.in-addr.arpa";
masters { 128.223.32.35 };
}
```

# 省略了更多区域

- 最后，我们拥有了 `cs.colorado.edu` 域名主名称服务器外部视图的配置文件。内部数据文件包含私有地址空间记录，以及指向每个主机首先、并指向中央邮件中枢机器作为备份的 `MX` 记录。内部邮件通常直接流动，不涉及邮件中枢。外部视图数据文件包含一个针对所有主机的 `MX` 记录，指向邮件中枢机器。

我们不再重复下面的许多配置语句，仅列出那些不同的部分。

# Linux 管理手册

# 来自 cs.colorado.edu 主服务器配置外部版本的片段
`directory "/"`; # 外部服务器也被锁定到 `/var/named`
`pid-file "named-external.pid"`
`named-xfer "named-xfer"`
`listen-on {128.138.243.151 }`; # 外部 IP 地址
`transfer-source 128.138.243.151`;
`query-source address 128.138.243.151 port 53`;

`zone "cs.colorado.edu" in {`
`type master;`
`file "forward-external/cs.colorado.edu";` # 区域的外部版本
`}`
`zone "245.138.128.in-addr.arpa" in {`
`type master;`
`file "reverse/245.138.128";` # 与内部版本相同
`}`

配置到此！现在让我们来看实际的数据文件。

## 16.11 DNS 数据库

域名的 DNS 数据库是由系统管理员在域名名称服务器上维护的一组文本文件。这些文本文件通常被称为区域文件（`zone files`）。它们包含两种条目：解析器命令（如 `$ORIGIN` 和 `$TTL`）以及“资源记录”（`resource records`，有时也称为 `RRs`）。只有资源记录真正上是数据库的一部分；而解析器命令提供了一些输入记录的简便方法。

我们从描述 DNS 资源记录开始，这些记录定义在 RFCs 882, 1035, 1183, 2065, 2181 和 2535 中。我们将解析器命令的讨论推迟到第 427 页。

### 资源记录

DNS 层次结构中的每个区域都有一组相关的资源记录（可能是空的）。记录的基本格式是：

`[name] [tttl] [class] type data`

字段之间由空白符（制表符或空格）分隔，并可以包含表 16.9 所示的特殊字符。

`name` 标识了记录所描述的实体（通常是主机或域名）。如果多个连续的记录引用同一个实体，则可以在第一条记录后留空名称。如果存在名称字段，它必须从一列开始。名称可以是相对的也可以是绝对的。绝对名称以点结尾并是完整的。在内部，软件只处理绝对名称；对于任何不以点结尾的名称，它会附加当前域名和一个点。此功能允许名称更短，但容易引发误解。

# 第 16 章 域名系统 409

**表 16.9** 在 RRs 中使用的特殊字符

| 字符 | 含义 |
| :--- | :--- |
| ; | 引入注释 |
| @ | 当前域名 |
| | | 允许数据跨行 |
| * | 通配符（仅限名称） |

请见第 417 页的警告说明。例如，在 `cs.colorado.edu` 域中，名称 "`anchor`" 将解释为 "`anchor.colorado.edu.`"。如果名称命名为 "`anchor.colorado.edu`" ，由于缺少结尾的点仍然意味着这是一个相对名称，并将附加默认域名，导致名称变为 "`anchor.colorado.edu.`"。这是一个常见的错误。`*TTL*`（生存时间）是指记录在缓存中的时间。

# 第 16 章 域名系统 411

## SOA 记录

`SOA` 记录标记了一个区域（`zone`）的开始，区域是位于 DNS 命名空间中相同位置的一组资源记录。DNS 树的此节点也称为授权点或区域切分（`zone cut`）。正如我们在第 414 页详细讨论的那样，DNS 数据通常包含两个区域：一个用于将主机名转换为 IP 地址，另一个以反方向进行映射。DNS 树有一个按名称组织的正向分支和一个按 IP 地址组织的反向分支。

每个区域恰好有一个 `SOA` 记录。该区域一直持续，直到遇到另一个 `SOA` 记录。`SOA` 记录包含了区域名称、技术联系人以及各种超时值。例如：

```text
+ ; Start of authority record for cs.colorado.edu
IN ns.cs.colorado.edu. hostmaster.cs.colorado.edu. (
@ IN 2001113300 Serial number
7200 Refresh (2 hours)
1800 Retry (30 minutes)
604800 Expire (1 week)
7200 Minimum (2 hours)
```
