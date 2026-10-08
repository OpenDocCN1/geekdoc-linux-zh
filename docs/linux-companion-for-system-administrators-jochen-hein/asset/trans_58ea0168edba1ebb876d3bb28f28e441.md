

[content]

# 490 名称服务器的配置与操作

PTR 记录是 `ghostbyaddr(3)` 函数所需的，该函数负责将 IP 地址转换为名称。PTR 记录中的每个名称都以点结尾，以防止 BIND 绑定到 `IN-ADDR.ARPA` 域。你应该包含所有在名称服务器中拥有 IP 地址的网络用户，以避免因为没有可用的反查条目而等待名称服务器超时。

```
name        (ttl)   addr-class  PTR      real name
155.31      IN          PTR      pea.example.org.
151.31      IN          PTR.
```
**Listing 20.11** 域名指针。

请注意，所有名称都必须以点结尾。否则，将追加域名 `(...in-addr.arpa)`。

## 20.7.8 邮件交换 (MX)

如果在发送邮件时无法访问某计算机（或计算机未连接到互联网，而是通过 UUCP 连接），可以输入另一台可用的计算机来接收邮件。如果原始计算机恢复可连接，邮件将被转发。较低的优先级值对应“成本”。

此功能通常用于允许网络中仅有一或两台计算机接受邮件。这可以将配置工作和可用性问题集中在几台计算机上。在将 MX 记录指向另一台计算机之前，你应该咨询该计算机的管理员。否则，这台计算机将受到意外邮件的轰炸，这些邮件可能会丢失。

大多数邮件服务器被配置为仅接受本地邮件，并且仅向本地用户转发邮件。这被认为是一种良好的实践，防止成员滥用系统。然而，你不能简单地将该机器作为你的 MX，因为会被拒绝中继，且邮件将退回给发送者。

```
name                (ttl) addr-class preference exchange
pea.example.org.      MX 0
```
**Listing 20.12** 邮件交换。

## 20.7.9 文本 (TXT)

对于每台计算机，可以将任意文本作为附加信息存储。除了这些文本必须包含在双引号（""）之外，没有其他限制。

| name | {ttl} | addr-class | TXT | string |
|---|---|---|---|---|

| pea.example.org. | IN | TXT | "A text" |

**Listing 20.13** 文本。

## 20.7.10 负责人 (RP)

除了名称服务器的负责人外，还可以为每个条目存储一个该计算机的联系人。在这里，邮件地址中的“@”字符（@）被替换为点。然而，如果你通过 SNMP（简单网络管理协议）辅助管理你的计算机，你应该将此信息输入管理基准（MIB）。

| owner | {ttl} | addr-class | RP domain-name |
|---|---|---|---|
| jochen.example.org. | IN | RP | |
| sysadmins.example.org. | IN | TXT | "Tel:..."

**Listing 20.14** 负责人。

## 20.7.8 文件名为 named.local

位于 `/var/named` 目录下的 `named.local` 文件（见 Listing 20.15）包含关于你自己的计算机的数据，它仅由几条条目组成，如果用户也想在他们的 hosts 文件中使用该条目，那么这些条目是非常重要的。

```
@ SOA example.org. hostmaster.example.org. (19860201 3600 300 3600 14400)
IN NS example.org.
0 IN PTR loopback
0 IN PTR localhost
```
**Listing 20.15** 文件名为 named.local。

## 20.9 文件名为 named.rev

`named.rev` 文件存储了属于给定 IP 地址的名称。这使得查找 IP 地址对应的名称变得相对快速简单；此功能也称为反查。该文件以 Master 格式存储。有些人通过 perl 或 awk 脚本从外部数据库生成两者。无论什么情况下，你可能都想使用像 `nslookup` 这样的程序来详细检查你的区域。

```
@ SOA example.org. hostmaster.example.org. (198602501 10800 3600 3600 86400)
IN NS example.org.
0 IN PTR example.org.
IN PTR A example.org.255.255.255.0
151.31 IN PTR corn.example.org.
155.31 IN PTR pea.example.org.
```
**Listing 20.16** 文件名为 named.rev。

请注意，你必须以点为每个主机名结尾。否则，将追加域 `in-addr.arpa`。此外，你应该确保 `named.data` 和 `named.rev` 文件之间的一致性。

## 20.10 从名称服务器

出于防止故障的安全考虑，每个区域至少应运行两台名称服务器。在一台计算机故障的情况下第二台名称服务器可以回答所有请求。为了随时保持数据一致，每个区域必须存在一个（已授权的）主服务器。此外，可以配置一个或多个从服务器。从服务器从主服务器获取数据。如果主服务器不可用，则使用存储在备份副本（.bak）中的数据。如果数据生存过期，将尝试从主服务器重新获取这些数据。Listing 20.17 显示了从服务器的 `/etc/named.conf` 示例。

```
zone "example.org" {
  type slave;
  masters { 192.168.3.150 };
  file "named.bak"
}
zone "192.in-addr.arpa" {
  type slave;
  masters { 192.168.3.150 };
  file "named.bak"
}
```
**Listing 20.17** 从服务器的/named.conf。

根据 SOA 记录中的序列号，从服务器可以判断它是否拥有区域最新数据。如果不是，将触发新的传输。因此，你应该关注所有名称服务器的系统日志。否则，从服务器是完全免维护的。

## 20.11 从名称服务器

从服务器不管理区域数据，仅作为缓存，并将无法回答的请求转发到特定的名称服务器（转发器）。这允许这台计算机建立良好的缓存，所有用户从中受益。

## 494 名称服务器的配置与操作

原则上，每个名称服务器都可以配置用于转发。如果名称服务器没有直接连接到互联网，将路由器或防火墙作为转发器是明智的。另一个优势是形成缓存减少了需要其他名称服务器回答的请求。

转发器向已知的根服务器提问。在从服务器中，仅询问转发器。如果这些服务器无法提供答案，则主机名无法解析。由于这些计算机可能需要自行获取数据，你应该在 `/etc/named.conf` 中多次输入这些地址。示例见 Listing 20.18。

```
# 仅转发名称服务器的配置文件 {
    directory "/etc/named";
    forward only;
    forwarders {
        194.45.71.65;
        192.168.3.150;
        194.45.71.65;
    }
};
zone "." {
    type hint;
    file "named.root";
};
```
**Listing 20.18** 仅转发名称服务器的示例。

首先，你应该输入最快且最稳定的名称服务器。由于这台计算机可能（甚至可能）最初必须获取数据，你应该在其他转发器之间放置该计算机的条目。

# 514 关于 DNS 的更多信息

## 20.12 关于 DNS 的更多信息

最重要的信息由 BIND 名称服务器操作指南提供，该指南包含在 bind 的源码中。一本强烈推荐的书是 Albitz 和 Liu (1992)。

| 附加信息和来源 |
|------|
| ftp 服务器: ftp.vix.com |
| ftp 服务器: /pub/bind/release |
| 文件名: bind.tar.gz |
| 新闻组: comp.protocols.tcp-ip.domains |
| 邮件列表: bind-users@vix.com，通过邮件向 users-request@vix.com 订阅 |
| 手页: named(8), ndc(8), resolver(5) |
| 其他文档: bind 源码发行中的各种文本 |

