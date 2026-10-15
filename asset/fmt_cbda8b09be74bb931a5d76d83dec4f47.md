
实际上为这些域或主机打开了开放中继。
其他可能性充满了问题：

- `FEATURE('promiscuous_relay')` – 允许中继；不要使用
- `FEATURE('relay_based_on_MX')` – 为指向你的 MX 记录中继
- `FEATURE('loose_relay_check')` – 允许“percent hack”地址格式
- `FEATURE('relay_local_from')` – 基于 From 地址进行中继

`promiscuous_relay` 功能允许从任何站点中继到任何其他地方。这是一张通往黑洞列表的单程票。不要在可以通过公共互联网访问的机器上使用此功能。

`relay_based_on_MX` 功能是糟糕的，因为你无法控制哪些站点被允许允许其 MX 记录。通常，指向你邮件服务器的 MX 记录的主机是你自己的，但没有什么阻止其他站点更改其 MX 记录以指向你。垃圾邮件发送者通常无法更改 MX 记录，但阴暗的站点可以。

`loose_relay_check` 功能允许垃圾邮件发送者喜爱的 `% hack` 形式的地址（见第 535 页）。

`relay_local_from` 功能信任邮件信封上的发送者地址，并中继看起来来自本地地址的消息。当然，邮件消息的信封和头信息都是很容易伪造的。

## 第 18 章 – 电子邮件

（注：由于 OCR 文本在不同页面之间存在大量重复和错位，此处已合并。）

## 18.10 sendmail 中的垃圾邮件相关

上述数据库文件将允许来自 `okguy@cyberspam.com` 的邮件，但将拒绝所有来自 `cyberspace.com` 的其他邮件，并带有指定的错误信息。来自 `sendmail.org` 或 `128.32.0/16`（加州大学伯克利分校的网络）的邮件将被转发。来自 `badguy@aol.com` 或任何域 `hotlivesex` 或 `friend` 的邮件也将被拒绝。

使用冒号分隔形式的 IPv6 地址也可以用于左侧，但它们必须以 `"IPv6:"` 为前缀。用户名 `hotlivesex` 和 `friend` 后的 `@` 符号是必不可少的；它用以区分用户名和域名。

`550` 是一个 RFC821 错误代码。RFC1893 错误代码（称为“投递状态消息”）更为详细。第一位数字 `4` 表示临时错误；`5` 表示永久错误。我们在表 18.13 中列出了其中几个。

### 表 18.13 RFC1893 状态码

| 临时 | 永久 | 含义 |
| --- | --- | --- |
| 4.2.1 | 5.2.1 | 邮箱已停用 |
| 4.2.2 | 5.2.2 | 邮箱已满 |
| 4.2.3 | 5.2.3 | 消息过长 |
| 4.2.4 | 5.2.4 | 列表扩展问题 |
| 4.3.1 | 5.3.1 | 邮件系统已满 |
| 4.4.4 | 5.4.4 | 无法路由 |
| 4.4.5 | 5.4.5 | 邮件拥塞 |
| 4.7.* | 5.7.* | 违反站点策略 |

为了更精细的控制，键字段（左侧）可以包含标签 `Connect`、`To`、`From`，以及在 8.12 及更高版本中的 `Spam`，以控制过滤器的应用方式。`Connect` 指连接信息，如客户端 IP 地址或客户端主机。`To` 和 `From` 指的是信封地址，而不是报头。`Spam` 标签允许通过“spam friend”和“spam hater”测试器对全局规则设置例外。它通过 `delay_checks` 功能启用：

```
FEATURE(delay_checks, 'friend')
```

```
FEATURE(delay_checks, 'hater')
```

第一条如果在 `access_db` 中存在映射的右侧为 `FRIEND` 的条目，则会跳过可能拒绝该消息的其他规则集。第二条如果 `access_db` 的值为 `HATER`，则应用其他规则集。这四项配置可以让你对邮件的转发和拒绝进行更精细的控制；它们也会覆盖相应的限制。对于对你全站垃圾邮件策略有异议的个人用户，可以使用 `spam FRIEND` 或 `HATER` 标签来解决。

使用了这些标签之一，查询将首先尝试使用标签信息，然后在不使用标签的情况下进行，以保持与旧访问数据库的后兼容性。

## 第 18 章 – 电子邮件

以下是一些示例：

```
From:spammer@some.domain REJECT
```

```
To:good.domain RELAY
```

```
Connect:good.domain OK
```

```
Spam:abuse@ FRIEND
```

来自 `spammer@some.domain` 的邮件会被拦截，但即使该地址被列入黑名单，你仍然可以向该地址发送邮件。邮件将转发到 `good.domain`，但不会从那里转发（假设在其他地方禁用了转发）。来自 `good.domain` 的连接将是允许，即使它是基于 DNS 的拒绝列表之一。发往 `abuse@localdomain` 的邮件将通过，即使来自 `spammer@some.domain`（后者的邮件会被第一条访问数据库行拒绝）。

许多站点使用访问数据库来控制垃圾邮件或策略。科罗拉多大学计算机科学系的入站邮件服务器使用 `access_db` 功能拒绝来自由地址、域名或 IP 网络识别的 500 多个已知垃圾邮件者的邮件。

## 用户或站点黑名单

如果你有想要阻止邮件的本地用户或主机，请使用

```
FEATURE('blacklist_recipients');
```

它支持在你的访问文件中包含以下类型的条目：

```
To:nobody@ 550 Mailbox disabled for this user
```

```
To:printer.mydomain.edu 550 This host does not accept mail
```

```
To:user@host.mydomain.edu 550 Mailbox disabled for this user
```

这些行处理入站邮件，以通知任何主机、主机打印机以及某个主机上的特定用户地址。使用 `To:` 标签允许这些用户发送消息而不是接收消息；某些打印机具有此功能。遗憾的是，现在几乎不可能通过 DNS 手动维护黑名单。坦率地说，可以通过 DNS 访问几个社区维护的黑洞列表，其中一些是免费提供的。

要包含 DNS 类型的黑洞列表，使用 `dnsbl`：

```
FEATURE('dnsbl', 'sbl.spamhaus.org');
```

这些黑名单通过对 DNS 系统的巧妙调整进行发布；因此名为 `dnsbl`。运行开放中继和已知拨号地址拦截列表的其他站点可能是垃圾邮件者的天堂。例如，一种形式的特殊 DNS 资源记录

`sbl.spamhaus.org IN A 127.0.0.2.`

## 报头检查

垃圾邮件者经常试图隐藏他们的身份。从 `sendmail 8.9` 开始，如果信封地址不是 `user@valid.domain` 格式，就会被拒绝。你可以忽略这种行为，除非你是一个防火墙且只有本地 DNS 可用。详细的报头检查是一种强大的反垃圾机制，它利用了底层的 `sendmail` 配置（此处未介绍）。通过报头检查，`sendmail` 可以查找报头中的指定模式（例如 `"To:friend@public.com"`）并在投递到邮箱之前拒绝消息。

报头检查还可以通过特定的报头行来识别病毒。例如，1999 年 Melissa 病毒包含了主题 `"Important Message ..."`。当 Melissa 病毒发布并被识别后，`sendmail` 发布了本地规则将其丢弃。在查看各种示例时，我们看到了以下报头检查规则：

- 发往 `public.com` 域
- 发往 `friend` 或 `you`
- 带有 `X-spam` 报头，指示 Happy99 蠕虫
- 主题为 `Important Message ...` 的 Melissa 病毒
- 主题为 `all.net` 和 `Fred ...` 的 Papa 病毒
- 主题为 `ILOVEYOU` 的 iloveyou 病毒及其变体
- 大量的垃圾邮件
- 带有损坏 Outlook Express 报头的 SirCamm

所有的报头检查规则都位于 `.mc` 配置末尾的 `LOCAL_CONFIG` 和 `LOCAL_RULESETS` 语句下。通过 `m4 divert` 命令，`sendmail` 知道将它们放在哪里。在某种程度上，你实现的任何 `spam` 语句都会拦截垃圾邮件者并提高剩余者的门槛。使用带有“user unknown”错误消息而不是丢弃邮件的错误邮件器有助于垃圾邮件者清理他们的列表。干净的列表更有价值，因此如果你拦截、过滤垃圾邮件并响应错误消息，他们可能会从列表中被移除。

## 速率和连接限制

`sendmail 8.13` 增加了 `ratecontrol` 功能，对接受入站连接的速率设置每个主机或每个网络的限制。这种限制对于放缓来自无法阻塞的垃圾邮件特别有用，因为大型 ISP 有很大比例的拨号用户。要启用速率控制，在 `.mc` 文件中放置如下的一行：

```
FEATURE('ratecontrol','nodelay', 'terminate')
```

此外，你必须在 `/etc/mail/access` 文件中列出控制的主机或网络及其限制阈值。例如，以下行
