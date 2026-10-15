
`MASQUERADE_AS(foobirds.org)`

`FEATURE(masquerade_envelope)`

```
此文件包含了第 5 章中描述的所有特性，加上 `relay_entire_domain` 特性。此额外特性允许你使用 M 类来识别邮件服务器应该转发的邮件来源。

### 警告

务必不要过度削弱配置，以至于让自己变成垃圾邮件源！上述列出的所有特性都会削弱邮件中继的屏障，但某些特性比其他更糟糕。不应使用泛用中继（promiscucuous relay），因为它会将系统变成潜在的垃圾邮件中继站。避免使用 `relay_local_from` 特性，因为它是危险的。

列表 11.4 结束。其格式为 `550 from $(client_addr) refused by blackhole site dnsbl-domain`，其中 `$(client_addr)` 是被拒绝的 IP 地址，而 `dnsbl-domain` 是提供给 `dnsbl` 功能的第一个参数的值。尽管我认为更改标准错误消息没有优势，但你可以通过以下命令将其更改为“Mail rejected. $(client_addr) is a suspected spam relay.”：

```
FEATURE '$dnsbl', 'dnsbl.foobirds.org', 'Mail rejected.

$$(client_addr) is a suspected spam relay.'$dnl
```

一如既往，使用 `MAPS` `RBL` 还是构建自己的黑洞服务器是在简单性与灵活性之间的权衡。如果你的站点较小，与你进行邮件交换的其他站点可能有限，且你认为其中任何站点出现在 `RBL` 中的概率微乎其微。此外，你可能没有足够的人员来构建和维护自己的黑洞站点。出于这些原因，小型站点可能会选择简单性。如果你为大型站点运行邮件服务器，你可能想要定义邮件访问列表，以确保能够持续连接到你直接控制的所有想要访问的站点。创建自己的黑洞服务器是 `sendmail` 提供的一项技术，即在访问数据库中定义访问控制。

### 理解访问数据库 (Access Database)

`sendmail` 访问数据库定义了电子邮件地址、域名和 IP 网络号，以及 `sendmail` 在接收来自指定源的邮件时应该采取的操作。例如：

```
spammer@bigisp.com    REJECT

wespamu.com             REJECT

172.18                 REJECT
```

此数据库告诉 `sendmail` 拒绝任何来自电子邮件地址 `spammer@bigisp.com` 的邮件、来自 `wespamu.com` 域名下任何主机的邮件，以及任何 IP 地址以网络号 `172.18` 开头的计算机的邮件。数据库中的每个条目都以邮件源开始，随后跟着一个告诉 `sendmail` 执行何种操作的关键字。表 11.3 列出了有效的关键字及其引起的操作。

### 表 11.3：访问数据库操作

| 关键字 | 操作 (Action) |
|---|---|
| `DISCARD` | 丢弃从指定源接收到的任何消息。 |
| `OK` | 绝对接受来自指定源接收的消息。 |
| `REJECT` | 发布错误消息，并丢弃发往或来自指定地址的邮件。 |
| `RELAY` | 继发来自或发送到指定地址的邮件。 |
| `Error message` | 向源地址返回指定的错误消息。 |

之前的数据库扩展部分已经说明了这些操作是如何使用的。列表 11.5 包含了这个更完整的访问数据库。

### 列表 11.5：sendmail 示例访问数据库

```
spammer@bigisp.com    REJECT

wespamu.com             REJECT

172.18

example.org

129.6

weselljunk.com

DISCARD

OK

RELAY

550 Junk mail is not accepted
```

`REJECT` 命令导致 `sendmail` 向源返回错误消息，然后丢弃邮件。`DISCARD` 命令在不向源发回任何消息的情况下丢弃邮件。大多数反垃圾邮件机构都不建议静默丢弃邮件，因为他们认为这不能威慑垃圾邮件发送者。在垃圾邮件发送者看来，你收到了邮件，所以他只会继续发送更多垃圾。

`OK` 命令导致 `sendmail` 接受来自 `example.org` 的邮件，无论其他条件如何。如果邮件来自包含 `example.org` 域名的主机名且无法通过 `DNS` 解析，`sendmail` 也会接受该邮件，即使没有启用 `accept_unresolvable_domains` 功能。当然，做到这一点需要完全信任 `example.org`。

`RELAY` 命令导致 `sendmail` 继发来自网络 `129.6` 的邮件，即使系统启用了基础继发。与 `OK` 命令一样，使用 `RELAY` 命令意味着你完全信任 `129.6` 上的每一个主机。如果你在数据库中没有其他内容，你可能想为自己的网络设置一个这样的 `RELAY` 条目。如之前讨论的，`sendmail` 会阻塞所有继发——甚至是来自你客户端的邮件。像 `172.16.5 RELAY` 这样的访问数据库条目允许访问指定网络的每个主机进行继发。

### 在 sendmail 中使用数据库

构建数据库后，你还需要让 `sendmail` 知道你有一个访问数据库并且你想使用它。使用 `access_db` 功能来实现。

假设你使用的是第 5 章中创建的配置。我们创建了自定义文件：专门针对 `foobirds.org` 的 `DOMAIN` 文件，以及一个将自定义 `DOMAIN` 文件包含在 `sendmail` 配置中的 `linux.mc` 文件。由于访问数据库是针对我们服务器的，让我们在 `foobirds.m4` `DOMAIN` 文件中添加必要的功能，列表 11.6 所示。

### 列表 11.6：向配置添加访问数据库

```
divert(0)

VERSIONID('foobirds.m4 03/16/2002')

define(FORWARD_PATH, '${/forward.${$w}:$z/.forward+h:$z}')

@.forward${$s}/forward.dnl

define(MAX_LENGTH, '32768')dnl

FEATURE('access_db', 'hash -o /etc/mail/access')

FEATURE('redirect'dnl)

FEATURE('use_cw_file')dnl

EXPOSED_USER('root')

MASQUADE_AS(foobirds.org)

FEATURE('masquerade_envelope')

FEATURE('generictable')
```

### 列表 11.8：创建本地规则集的示例

```
LOCAL_RULESETS

Message-Id: $>@check_MID_header
```

```
Scheck_MID_header

R$++ @@#OK

R$* $$error: 550 Invalid Header
```
