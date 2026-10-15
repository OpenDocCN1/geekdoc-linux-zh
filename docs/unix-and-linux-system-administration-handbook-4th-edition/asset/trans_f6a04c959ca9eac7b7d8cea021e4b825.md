

数据字段的内容取决于记录类型。对特定域名和记录类型的 DNS 查询会从区域文件中返回所有匹配的资源记录。表 17.6 列出了常见的记录类型。

**表 17.6 DNS 记录类型**

| 类别 | 类型 | 名称 | 功能 |
|---|---|---|---|
| Zone | SOA | Start of Authority | Defines a DNS zone |
| Zone | NS | Name Server | Identifies servers, delegates subdomains |
| Basic | A | IPv4 Address | Name-to-address translation |
| Basic | AAAA | IPv6 Address | Name-to-IPv6 address translation |
| Basic | PTR | Pointer | Address-to-name translation |
| Basic | MX | Mail Exchanger | Controls email routing |
| Security and DNSSEC | DS | Delegation Signer | Hash of signed child zone's key-signing key |
| Security and DNSSEC | DNSKEY | Public Key | Public key for a DNS name |
| Security and DNSSEC | NSEC | Next Secure | Used with DNSSEC for negative answers |
| Security and DNSSEC | NSEC3<sup>a</sup> | Next Secure v3 | Used with DNSSEC for negative answers |
| Security and DNSSEC | RRSIG | Signature | Signed, authenticated resource record set |
| Security and DNSSEC | DLV | Lookaside | Nonroot trust anchor for DNSSEC |
| Security and DNSSEC | SSHFP | SSH Fingerprint | SSH host key, allows verification via DNS |
| Security and DNSSEC | SPF | Sender Policy | Identifies mail servers, inhibits forging |
| Security and DNSSEC | DKIM | Domain Keys | Verify email sender and message integrity |
| Optional | CNAME | Canonical Name | Nicknames or aliases for a host |
| Optional | SRV | Services | Gives locations of well-known services |
| Optional | TXT | Text | Comments or untyped information<sup>b</sup> |

a. 原始的 NSEC 系统允许熟悉 dig 命令的黑客轻松列出区域的所有记录。NSEC3 已修复了这一弱点，但计算成本更高；两者目前都在使用。

b. TXT 记录越来越多地被用来尝试新想法，而无需获得 IETF 对新记录类型的正式认可。例如，SPF 和 DKIM 记录最初都是作为 TXT 记录实现的。

某些记录类型已过时、处于实验阶段或未被广泛使用。请参阅名称服务器的实现文档以获取完整列表。大多数记录都是手工维护的（通过编辑文本文件），但安全资源记录需要加密处理，因此必须使用软件工具进行管理。这些记录在第 648 页开始的 DNSSEC 部分中进行了描述。

区域文件中资源记录的顺序是任意的，但传统上 SOA 记录在最前面，其后是 NS 记录。每个主机的记录通常会放在一起。常见做法是按名称字段排序，尽管有些站点按 IP 地址排序，以便更容易识别未使用的地址。从属服务器上的区域文件不是由人工管理的，而是由名称服务器软件写入的；记录顺序是混乱的。

## The SOA record

正如我们在下一节中详细描述每种类型的资源记录时，我们会检查来自 atrust.com 域数据文件的一些示例记录。在此上下文中，默认域为“atrust.com”，因此指定的主机“bark”实际上是指“bark.atrust.com。”

每种类型的资源记录的格式和解释由 IETF 在 RFC 系列中指定。在即将到来的章节中，我们会在边注中列出与每个记录相关的特定 RFC（连同其起源年份）。

SOA（Start of Authority）记录标记了区域的开始，区域是一组位于 DNS 命名空间同一位置的资源记录。DNS 域的数据通常至少包括两个区域：一个用于将主机名转换为 IP 地址，称为正向区域，以及将 IP 地址映射回主机名的区域，称为反向区域。

每个区域恰好有一个 SOA 记录。SOA 记录包括区域的名称、区域的主名称服务器、技术联系人以及各种超时值。注释以分号引入。以下是一个示例：

```
; Start of authority record for atrust.com
atrust.com.   IN  SOA  ns1.atrust.com. hostmaster.atrust.com. (
    2009070200   ; Serial number
    10800        ; Refresh    (3 hours)
    1200         ; Retry      (20 minutes)
    3600000      ; Expire     (40+ days)
    3600 )       ; Minimum    (1 hour)
```

SOA 记录的名称字段（本例中为 atrust.com.）通常包含符号 @，它是当前区域名称的简写。@ 的值是 named.conf 的区域语句中指定的域名，或 nsd.conf 文件中区域名称条目中的域名。此值可通过区域文件中的 $ORIGIN 解析器指令进行更改（参见第 596 页）。

此示例没有 TTL 字段。类别为 IN 表示 Internet，类型为 SOA，其余项目构成数据字段。括号中的数值参数是超时值，通常写在一行上且不带注释。

“ns1.atrust.com.”是区域的主名称服务器。<sup>11</sup>

“hostmaster.atrust.com.”是以“user.host”而非标准 user@host 格式的技术联系人电子邮件地址。只需将第一个点替换为 @ 并去掉最后的点，即可向域管理员发送邮件。站点通常使用 admin 或 hostmaster 等别名代替实际的登录名。负责 hostmaster 职责的系统管理员可能会变更，更改 aliases 文件（参见第 756 页）中的一个条目比在需要更新联系人时更改所有区域文件要容易。

11. 实际上，除非使用动态 DNS，否则可以在 SOA 记录中列出区域的任何名称服务器。在这种情况下，SOA 记录必须命名主服务器。

有关 RFC 的更多信息，请参见第 449 页。

SOA 记录在 RFC1035（1987）中指定。

有关配置细节，请参见第 597 页的 named.conf 和第 625 页的 nsd.conf。

