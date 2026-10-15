
## access_db 接受类
`{Accept}OK RELAY`
`{Re5Ok}OKR`
# 允许转发的邮件中继的主机（`$=R`）
`FR-o /etc/mail/relay-domains`

这里有一份来自 `sendmail.mc` 文件的引用，供对比：

```
dn1 define(`SMART_HOST',`smtp.your.provider.')
define(`confDEF_USER_ID',`"8:12"')dn1
undefined(` UUCP_RELAY')dn1
undefine(`BINTET_RELAY')dn1
dn1 define(`confAUTO_REBUILD')\dn1
define(`confTO_CONNECT', `1m')dn1
define(`confTRY_NULL_MX_LIST',true)dn1
```

你可以理解为什么该文件被描述为晦涩难懂。

复杂的邮件服务器设置超出了本书的范围；有关此主题的更多信息，我们建议参考 Costales 和 Allman 所著的《Sendmail，第三版》，这是一部关于 Sendmail 配置的 1200 页综合巨著。然而，以下五个部分将介绍一些常用的高级选项。

## 配置伪装（Masquerading）

有时，你可能希望 Sendmail 伪装成除了系统实际主机名之外的其他主机。这种情况可能发生在你通过拨号连接到互联网，且你的 ISP 为你处理所有邮件时。在这种情况下，你希望 Sendmail 伪装成你 ISP 的域名。例如：

```
MASQUERADE_AS(`samplel.net.org')dn1
```

## 使用智能主机（Smart Hosts）

如果你没有全天候的互联网连接，你可能希望 Sendmail 将你的消息发送到你 ISP 的邮件服务器，并让它为你处理投递。在没有全天候互联网连接的情况下，你可能会发现将消息投递到某些地点（例如世界上电子邮件服务不可靠且零星出现的欠发达地区）非常困难。在这些情况下，你可以配置 Sendmail 作为智能主机，通过将其传递给另一个发送者而不是直接尝试投递邮件来实现。你可以在 `sendmail.mc` 文件中使用类似下面的行来启用智能主机：

```
define(`SMART_HOST', `smtp.samplel.net.org')
```

这一行导致 Sendmail 将其接收到的任何邮件传递给服务器 `smtp.samplel.net.org`，而不是尝试直接投递。如果你的 ISP 像许多其他 ISP 一样阻止任何邮件中继，智能托管对你将不起作用。一些 ISP 阻止中继，因为它经常被用于传播垃圾邮件。

## 设置邮件投递间隔

如前所述，Sendmail 通常会在收到消息后立即尝试投递，并在之后的固定间隔再次尝试。如果你只有定期的互联网连接（例如拨号连接），你很可能更希望 Sendmail 将所有消息保留在队列中，并在特定的时间间隔或你的提示下尝试投递它们。你可以通过在 `sendmail.cf` 中添加以下行来配置 Sendmail 以实现此功能：

```
define(`confDELIVERY_MODE', `d')dnl
```

这一行导致 Sendmail 仅在定期调度的队列处理间隔（默认情况下，介于 20 到 30 分钟之间）尝试邮件投递。

然而，如果你离线时间更长，这个延迟时间可能不够。在这些情况下，你可以调用没有队列处理时间的 Sendmail。例如，默认情况下，Sendmail 可能会以以下命令启动：

```
# sendmail -bd -q30m
```

这告诉 Sendmail 它应该每 30 分钟处理一次邮件队列（并尝试投递消息）。你可以将 30 更改为任何其他数字来更改投递间隔。如果你希望 Sendmail 在特定提示前等待再处理队列，你可以像这样调用没有队列时间的 Sendmail：

```
# sendmail -bd -q
```

该命令告诉 Sendmail 在启动时处理一次队列，并且仅在手动指示时才再次处理。要手动告诉 Sendmail 处理队列，你可以使用以下命令：

```
# sendmail -q
```

> **提示**
>
> 如果你通过调制解调器进行网络传输，有一个用于 `pppd` 的配置文件叫做 `ppp.linkup`，它位于 `/etc/ppp` 中。该文件中的任何命令都会在 PPP 守护进程每次启动时自动运行。你可以将 `sendmail -q` 这一行添加到该文件，以便在每次拨通互联网连接时自动处理你的邮件队列。

## 构建 sendmail.cf 文件

市面上有书籍可以探索 Sendmail 配置的深度，但*《Sendmail 安装和运行指南》*是标准参考。也可以通过 Google 搜索找到配置指导；许多人在许多不同的配置中使用 Sendmail。幸运的是，Fedora 提供了一个默认 Sendmail 配置，只要你的网络配置正确且不需要类似 ISP 的 Sendmail 配置，该配置对于家庭用户即可开箱即用。

在对 `sendmail.mc` 进行所有更改后，你必须重新构建 `sendmail.cf` 文件。首先，备份你的旧文件：

```
# cp /etc/mail/sendmail.cf /etc/mail/sendmail.cf.old
```

你必须通过 `m4` 宏处理器运行 `sendmail.mc`，以生成可用的配置文件。使用如下命令来完成此操作：

```
# m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf
```

该命令从 `/usr/share/sendmail-cf/m4/cf.m4` 加载 `cf.m4` 宏文件，然后使用它处理 `sendmail.mc` 文件。输出通常发送到 STDOUT，然后重定向到文件 `sendmail.cf`，你的新配置文件即准备就绪。在更改生效之前，你必须重启 Sendmail。

> **提示**
> Fedora 还提供了使用 `awk` 重建 Sendmail 配置的替代方法。作为 root，执行：
> ```
> # make -C /etc/mail
> ```

### 邮件中继

默认情况下，Sendmail 不中继未从本地域起源的邮件。这意味着，如果在 `lion.org` 上运行的 Sendmail 安装收到了一封打算发给 `cheetah.org` 的邮件，且该邮件未从 `lion.org` 起源，该邮件将被拒绝且不会被中继。如果你想允许特定域通过你进行中继，请在文件 `/etc/mail/relay-domains` 中添加该域的条目。如果文件不存在，只需在你喜欢的文本编辑器中创建它，并添加包含你允许进行中继的域名的一行。此更改需要重启 Sendmail 才能生效。

> **注意**
> 你需要有非常充分的理由才能中继邮件；否则，不要这样做。允许所有域通过你进行中继会使你成为垃圾邮件发送者的磁铁，他们希望使用你的邮件服务器发送垃圾邮件。这可能导致你的站点被许多其他站点列入黑名单，这些站点随后将不接受来自你或你站点用户的任何邮件——即使邮件是合法的！

### 使用别名转发电子邮件

别名允许你在系统中拥有无限数量的有效收件人地址，而无需担心为每个地址创建帐户或其他支持文件。

例如，大多数系统都定义了 `postmaster` 作为一个有效收件人，却没有一个实际的名为 `postmaster` 的登录帐户。别名在文件 `/etc/aliases` 中配置。这是一个别名的条目示例：

```
postmaster: root
```

该条目将收到发往 `postmaster` 的任何邮件转发给 `root` 用户。默认情况下，`/etc/aliases` 文件中列出的几乎所有别名都转发给 `root`。

> **注意**
>
> 以 `root` 身份读取电子邮件是一种安全隐患；恶意电子邮件消息可以利用电子邮件客户端导致其以运行该客户端的用户身份执行任意代码。为了避免这种危险，你可以将 `root` 的所有邮件转发到另一个帐户，并在那里读取它。你可以选择两种方式来执行此操作。
>
> 你可以在 `/etc/mail/aliases` 文件中添加一个条目，将 `root` 的邮件发送到不同的帐户。例如，`root: foorbar` 将发往 `root` 的所有邮件转发到帐户 `foorbar`。
>
> 另一种方式是在 `root` 的主目录中创建一个名为 `.forward` 的文件，其中包含邮件应转发到的地址。

每当你对 `/etc/mail/aliases` 文件进行更改时，在该更改生效之前，你必须重建别名数据库。这通过以下方式完成：

```
# newaliases
```

## 拒绝来自特定站点的邮件

你之前在本章中读到，在邮件中继方面你必须小心，以避免成为垃圾邮件磁铁。但是，如果你正在与某个向你发送垃圾邮件的站点出现问题的话该怎么办？你可以使用 `/etc/mail/access` 文件自动拒绝来自某些站点的邮件。

你可以在 `access` 文件中使用多条规则。表 25.1 列出了这些规则。

表 25.1 访问规则的各种可能选项

| 选项 | 动作 |
| :--- | :--- |
| OK | 接受来自此站点的邮件，覆盖任何会拒绝来自此站点邮件的规则 |
| RELAY | 允许此域通过服务器进行中继 |
| REJECT | 拒绝来自此站点的邮件并发送预先设定的错误消息 |
| DISCARD | 简单地丢弃从该站点收到的任何消息 |
| ERROR: "n message" | 其中 n 是符合 RFC821 的错误代码编号，message 是你希望发回给起源服务器的任何消息 |

以下是一个使用三条规则来控制对 Sendmail 账户访问权限的示例。第一条规则拒绝来自 `spam.com` 的邮件。第二条规则拒绝来自 `1amer.com` 的邮件，并向该站点显示错误消息。第三条规则允许来自特定主机 `user5.1amer.com` 的邮件，尽管存在一条拒绝来自 `1amer.com` 站点的邮件的规则。（为了更直观地说明为什么要这样做，我发现我收到大量来自 Hotmail 域名的垃圾邮件，所以我宁愿全部拒绝。但是，我妻子使用 Hotmail 账户收发邮件。如果我不允许她的邮件通过，对我来说将是个问题。）
