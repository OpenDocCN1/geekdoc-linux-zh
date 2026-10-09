
| SOA | 起始，启动区域文件中的 DNS 条目，指定域名称服务器以及服务器联系方式和序列号等功能 |
| WKS | 已知服务描述 |
| PTR | 指针记录，用于执行反向域名查找，将 IP 地址映射到主机名 |
| RP | 包含主机信息的文本字符串 |
| HINFO | 主机信息 |
| MINFO | 邮箱箱或邮件列表信息 |
| MX | 邮件交换器，告知远程站点你区域的邮件服务器 |
| TXT | 文本字符串，通常是关于主机的信息 |
| KEY | 域私钥 |
| SIG | 资源记录签名 |
| NXT | 下一个资源记录 |

表 30-7：域名系统资源记录类型

# 生存时间指令与字段：`$TTL`

所有区域文件都以一个生存时间（Time To Live）指令开端，该指令指定了客户端在再次从 DNS 服务器刷新信息之前应保留所提供的 DNS 信息的时间。从实际情况来说，这至少应该是一天，但如果服务器的更改安排得更早，你可以临时缩短该时间，稍后再恢复。事实上，每条记录都有一个生存时间值，可以通过 `TTL` 字段显式指定。这是资源记录中的第二个字段。如果记录中没有指定 `TTL` 字段，则可以使用由 `$TTL` 指令定义的默认值。`$TTL` 指令位于每个区域文件的开头。默认情况下，它将以秒为单位列时间，通常为 86400，即 24 小时。

你也可以以天 (`d`)、小时 (`h`) 或分钟 (`m`) 指定时间，例如：

```
$TTL 2d3h
```

当作为字段使用时，`TTL` 将是指定为第二个字段的时间。在示例中，`turtle` 资源记录可以缓存三天。这将覆盖 `$TTL` 指令中的默认时间：

```
turtle 3d IN A 192.168.0.1
```

# 区域起始：SOA

区域或反向映射文件始终以一个特殊的资源记录开始，称为区域起始（Start of Authority）记录。该记录指定所有记录都是该域名的权威记录。它还包含了关于名称服务器域的信息，这些信息将提供给其他名称服务器。`SOA` 记录的格式与其他资源记录相同，但其数据段的排列方式不同。`SOA` 记录如下：

```
name (ttl) class SOA Origin Person-in-charge (
Serial number
Refresh
Retry
Expire
Minimum)
```

每个区域都有自己的 `SOA` 记录。`SOA` 以 `named.conf` 区域条目指定的区域名称开始。这通常是一个域名。`@` 符号通常用于名称，并像宏一样扩展为域名。类（class）用于互联网服务器，`IN`。`SOA` 是类型（type）。源（Origin）是记录来源的机器，通常是运行你名称服务器的机器。负责人（Person-in-charge）是管理区域服务器的人员的电子邮件地址（使用电子邮件地址，而不是 @，因为该符号用于域名）。多个配置项放置在一个用大括号分隔的块中。第一个是序列号（Serial number）。当你添加或更改记录时需要更改序列号，以便其他服务器进行更新。只要每次对区域进行更改时都增加，序列号可以是任何数字。常见的做法是使用“年-月-日-数字”作为序列号，其中数字是当天更改的次数。例如，199912403 表示 1999 年 12 月 4 日的第 3 次更改。进行更改时务必更新它。

刷新（Refresh）指定刷新 `SOA` 信息的时间间隔。重试（Retry）是尝试联系权威服务器的频率。过期（Expire）是二级名称服务器在不更新的情况下保留区域信息的时间。最小（Minimum）是区域内记录的生存时间。这些时间以秒为单位指定。

下面的示例显示了一个 `SOA` 记录。运行名称服务器的机器是 `turtle.mytrek.com.`，负责服务器的人员电子邮件地址是 `hostmaster.turtle.mytrek.com.`。注意这些名称末尾的点。对于没有点的名称，将附加域名。`turtle.mytrek.com.`。在输入完整主机名时，请务必加上点，以免附加域名。

```
IN SOA turtle.mytrek.com. hostmaster.turtle.mytrek.com. (
1990022700 ; Serial
28800 ; Refresh
14400 ; Retry
3600000 ; Expire
86400 ) Minimum
```

# 名称服务器：NS

名称服务器（NS）记录指定该区域的名称服务器。通常是一个完整主机名。注意这些名称末尾的点。对于没有点的名称，将附加域名。`turtle.mytrek.com.`。在输入完整主机名时，请务必加上点，以免附加域名。

```
IN NS turtle.mytrek.com.
```

`@` 符号通常代表域名。`NS` 记录指定该区域的名称服务器。`mytrek.com`。

```
IN NS mytrek.com.
```

# 地址记录：A

`A` 记录将主机名与 IP 地址关联。通常是 IPv4 地址。`A` 记录指定主机名。`turtle.mytrek.com.`。在以下示例中，是 `turtle.mytrek.com`。

```
IN A 192.168.0.1
```

# IPv6 地址：AAAA

`AAAA` 记录将主机名与 IPv6 地址关联。通常是 128 位地址。`AAAA` 记录指定主机名。`turtle.mytrek.com.`。

```
IN AAAA 2001:db8:85a3::8a2e:370:7334
```

# 邮件交换器：MX

`MX` 记录提供该区域或特定主机的邮件服务器。邮件交换器是接收邮件的服务器。在以下示例中，邮件服务器指定为 `turtle.mytrek.com`。

```
MX turtle.mytrek.com
```

# 第 30 章：域名系统

`mytrek.com.` `IN` `MX` 10 `turtle.mytrek.com.`

`IN` `MX` 20 `rabbit.mytrek.com.`

你也可以为特定主机指定邮件服务器。在下面的示例中，`lizard.mytrek.com` 的邮件服务器指定为 `rabbit.mytrek.com`：

`lizard.mytrek.com.` `IN` `A` 192.168.0.3

`IN` `MX` 10 `rabbit.mytrek.com.`

## 别名：CNAME

`CNAME` 类型的资源记录用于指定区域内主机别名。别名通常用于运行多种类型的服务器，例如 Web 和 FTP 服务器。它们还用于在主机更改名称时定位该主机。旧名变成新名的别名。在下面的示例中，`ftp.mytrek.com` 是实际上名为 `turtle.mytrek.com` 的机器的别名：

`ftp.mytrek.com.` `CNAME` `turtle.mytrek.com.`

`CNAME` 一词代表 canonical（规范）。规范名称是主机的实际名称。在前面的示例中，规范名称是 `turtle.mytrek.com`。别名（也称为 `CNAME`）是 `ftp.mytrek.com`。在 `CNAME` 条目中，别名指向规范名称。别名不能用于 `NS`（名称服务器）或 `MX`（邮件服务器）条目。对于这些记录，你需要使用原始域名或 IP 地址。

实现别名的一种更稳定方法是简单地为主机或域名创建另一个记录。只要经过认证，你可以为同一个 IP 地址拥有任意数量的主机名。例如，要让 `mytrek.com` 成为 `turtle.mytrek.com` 的别名，你只需要为它添加另一个地址记录，赋予它与 `turtle.mytrek.com` 相同的 IP 地址。

`turtle.mytrek.com.` `IN` `A` 192.168.0.1

`www.mytrek.com.` `IN` `A` 192.168.0.1

## 指针记录：PTR

`PTR` 记录用于执行 IP 地址到主机的反向映射。主机条目持有反向 IP 地址，数据条目持有主机的名称。下面的示例将 IP 地址 192.168.0.1 映射到 `turtle.mytrek.com`：

`192.168.0.1` `PTR` `turtle.mytrek.com.`

在 `PTR` 记录中，你可以仅指定地址的最后一段（主机地址），并让 DNS 填充地址的域名部分。在下一个示例中，IP 自动添加域名地址 192.168.0.1，以生成 192.168.0.1：

`1.` `PTR` `turtle.mytrek.com.`

## 主机信息：HINFO, RP, MINFO 和 TXT

`HINFO`、`RP`、`MINFO` 和 `TXT` 记录用于提供有关主机的信息。`RP` 记录允许你指定负责特定主机的负责人。`HINFO` 记录提供基本的硬件和操作系统标识。`TXT` 记录用于输入你想要的任何文本。`MINFO` 提供主机邮件和邮箱信息中指定的地址域。这些记录的使用较少，因为它们可能会提供过多服务器的信息。

## 区域文件

DNS 服务器使用多个覆盖 DNS 不同组件的区域文件。每个区域使用两个区域文件：主区域文件和反向映射文件。区域文件包含服务器中主机的记录。反向映射文件包含提供你的域名反向映射的记录，允许你从 IP 地址映射到域名。用于区域文件的名称可以是任何名称。文件名在 `named.conf` 文件的 `zone` 语句条目中指定。如果你的服务器支持多个区域，你可能想使用域名作为区域文件名。例如，`mytrek.com` 将有一个具有相同名称且扩展名为 `db` 的区域文件，如 `mytrek.db`。在后续使用的区域文件称为 `mytrek.db`。反向映射文件也可以是任何名称，尽管它通常是对应区域文件中的反向 IP 地址。例如，在 `mytrek.com` db 区域中，反向映射文件可能命名为 `192.168.0.db`，这是 `mytrek.com` db 区域中定义的 `mytrek.com` 域名的 IP 地址。此文件将包含域内所有主机地址记录，允许将其主机名地址映射到相应的 IP 地址。此外，BIND 为 localhost 设置了缓存文件和一个区域。缓存文件持有从根名称服务器到你的名称服务器的记录。缓存文件可以是任何名称，尽管它被称为 `named.ca` 或 `localhost`。`localhost` 区域文件持有环回接口 `localhost` 的反向 IP 资源记录。`localhost` 区域由 `named.rfc1912.zones` 配置文件中的语句配置，该文件包含在 `named.conf` 文件中。尽管地址是根据 RFC 1912 互联网协议标准配置的。

一旦创建了区域文件，你就应该用 `named-check` 工具检查它们的语法。该工具要求你同时指定区域和文件。在下面的示例中，检查了 `/var/named` 目录下、文件 `mytrek.com.db` 中的 `mytrek.com` 区域：

```
named-check mytrek.com mytrek.com.db
```

## 互联网区域的区域文件

区域文件持有遵循特定格式的记录。文件以通用指令开始，定义默认域名或包含其他资源文件。随后是 `SOA` 记录、名称服务器和域记录，然后是不同主机的记录。注释以分号开头，可以贯穿整个文件。`@` 符号像一个宏，代表区域名称。`@` 符号用于 `SOA` 记录的第一个字段表示域。如果名称留空，则自动使用资源记录的前一个条目。通过这种方式，你可以列出适用于同一主机的多个条目而无需重复主机名。任何不以点结尾的主机或域名都会在其后附加该域。例如，如果区域是 `mytrek.com` 且资源记录没有尾随点，则会自动附加 `mytrek.com`。

## 指令

你还可以使用几个指令来设置全局属性。`$ORIGIN` 为不以点结尾的地址设置默认名称，`$INCLUDE` 包含一个域或 IP 地址不同的文件。`$ORIGIN` 指令通常用于指定记录中的域。下面的示例将域设置为 `mytrek.com.`，并会自动附加到后续的主机：

```
$ORIGIN mytrek.com.
lizard IN A 192.168.0.2
```

## SOA 记录

区域文件以指定名称服务器的 `SOA` 记录开始。`@` 符号用于 `SOA` 记录的域。在 `SOA` 之后列出了域自身的资源记录（`NS`）。随后是主机记录（`A`）、别名（`CNAME`）和邮件交换记录（`MX`）。接下来的示例显示了一个区域文件，它以 `SOA` 记录开始，随后是域 `NS` 记录以及主机记录：

```
; Authoritative data for mytrek.com
$TTL 86400
@ SOA mytrek.com. (
71200 ; Serial number
10800 ; Refresh 3 hours
3600 ; Retry 1 hour
360000 ; Expire 1000 hours
86400 ; Minimum 24 hours
```

|  | 类型 | 值 |
| :--- | :--- | :--- |
| IN | NS | mytrek.com. |
| IN | A | 192.168.0.1 |
| IN | MX | 10 | turtle.mytrek.com. |
| IN | MX | 15 | rabbit.mytrek.com. |
| turtle | A | 192.168.0.1 |
| gopher | HINFO | LINUX |
| gopher | CNAME | turtle.mytrek.com. |
| ftp | CNAME | turtle.mytrek.com. |
| www | A | 192.168.0.1 |
| rabbit | A | 192.168.0.2 |
| lizard | HINFO | MA |

## 第 6 部分：网络支持

前两行以分号开头。文件中资源记录的类为 `IN`，表示这些是互联网记录。`SOA` 记录以 `@` 符号开头，代表域。在本示例中，它是 `mytrek.com`。整个文件中使用的任何不以点结尾的主机或域名都会附加该域。例如，接下来的资源记录 `turtle` 没有点，因此它扩展为 `turtle.mytrek.com`。`rabbit` 和 `lizard` 也是如此。它们读取为 `rabbit.mytrek.com` 和 `lizard.mytrek.com`。此外，在 `SOA` 中，注意 `hostmaster` 的邮箱使用的是点而不是符号；`@` 是区域文件中的特殊符号，不能用于其他用途。

## 名称服务器记录

下一个记录指定该区域的名称服务器。在这里，是 `mytrek.com`。注意该资源记录的名称是空的。如果名称为空，资源记录将继承上一个记录的名称。在这种情况下，`NS` 记录继承了 `SOA` 记录中的 `@` 值。这是域，`NS` 记录指定 `mytrek.com` 为该区域的名称服务器。

```
IN NS turtle.mytrek.com.
```

在这里，继承了域名。该条目的读取方式如下。注意域名末尾的点：

```
mytrek.com. IN NS turtle.mytrek.com.
```

## 地址记录

接下来的地址记录为域本身设置地址。这通常与名称服务器相同。在这种情况下，是 192.168.0.1（`turtle.mytrek.com` 的 IP 地址）。这允许用户引用域本身，而不是其中的特定主机。随后是邮件交换记录，将域邮件路由到名称服务器。用户可以向 `mytrek.com` 域发送邮件，邮件将路由到 `turtle.mytrek.com`。

```
IN A 192.168.0.1
```

在这里，继承了域名。该条目的读取方式如下：

```
mytrek.com. IN A 192.168.0.1
```

## 邮件交换记录

后续记录是邮件交换（`MX`）记录，列出 `turtle.mytrek.com` 和 `fast.mytrek.com` 为该区域的邮件服务器。你可以为一个主机设置多个邮件交换记录。可能存在多个可以路由的主机。这些可以列在邮件交换记录中，你可以设置优先级排名（数字越小优先级越高）。例如，如果无法访问 `turtle.mytrek.com`，其邮件将通过 `rabbit.mytrek.com` 路由，该服务器已设置为处理 `mytrek.com` 域的邮件。

```
IN MX 100 turtle.mytrek.com.
IN MX 200 rabbit.mytrek.com.
```

再次继承了域名。这些条目的读取方式如下：

## 第 30 章：域名命名系统

`mytrek.com.` `IN` `MX` 100 `turtle.mytrek.com.`

`mytrek.com.` `IN` `MX` 150 `rabbit.mytrek.com.`

## 带有主机名的地址记录

接下来的资源记录是一个地址记录（`A`记录），它将 IP 地址与完全限定域名名 `mytrek.com` 关联。该资源记录名称仅包含 `turtle` 且末尾没有点号，因此它会被自动扩展为 `turtle.mytrek.com`。此记录提供了 `turtle.mytrek.com` 可以映射映射的 IP 地址。

```
turtle IN A 192.168.0.1
```

## 继承名称

紧随其后的是几个名称为空的资源记录。它们从前一个记录中继承名称——在本例中，即为 `turtle.mytrek.com`。实际上，这些记录也适用于该主机。使用空名称是列出同一台主机额外资源记录的简单方法（注意这里有一个明显的缩进）。第一条记录是信息记录，提供了该机器的硬件和操作系统。

```
IN HINFO PC-686 LINUX
```

## 别名记录

如果你在同一台机器上运行多个不同的服务器，例如 Web、FTP 和 Gopher 服务器，你可能希望为这些服务器设置别名，以便用户更容易访问。用户可能会发现，使用实际域名（如 `turtle.mytrek.com`）来访问运行其上的 Web 服务器，不如使用以下名称更方便：对于 Web 服务器，使用 `www.mytrek.com`；对于 Gopher 服务器，使用 `gopher.mytrek.com`；对于 FTP 服务器，使用 `ftp.mytrek.com`。在 DNS 中，你可以使用别名记录（`CNAME`）来实现这些功能。在示例文件中，为 `turtle.mytrek.com` 主机存在两个 `CNAME` 别名：FTP 和 Gopher。下一条记录使用针对同一台机器的另一个地址记录为 `www` 实现了别名。由于这些名称都没有以点号结尾，因此它们将附加域名 `mytrek.com`。`www.mytrek.com`、`ftp.mytrek.com` 和 `gopher.mytrek.com` 都是 `turtle.mytrek.com` 的别名。输入这些 URL 的用户将自动访问 `turtle.mytrek.com` 机器上的相应服务器。
