

FEATURE('no_default_msa', 'dn!')!dn!
FEATURE('smrsh', '/usr/bin/smrsh')dn!
FEATURE('mailertable', 'hash -o /etc/mail/mailertable.db')!dn!
FEATURE('virtusertable', 'hash -o /etc/mail/virtusertable.db')!dn!
FEATURE(redirect)dn!
FEATURE(always_add_domain)!dn!
FEATURE(use_cw_file)dn!
FEATURE(use_ct_file)!dn!
FEATURE(local_procmail, '`', 'procmail -t -Y -a $h -d $u')dn!
FEATURE('access_db', 'hash -<TMP#> -o /etc/mail/access.db')!dn!
FEATURE('blacklist_recipients')!dn!

`FEATURE` 宏用于设置某些特殊的 sendmail 特性。`no_default_msa` 特性告知 sendmail 不生成默认的 MSA 守护进程（该进程通常设置为监听 587 端口）。`smrsh` 特性将 `/usr/bin/smrsh` 定义为 sendmail 用于接收命令的简单 shell。`mailertable` 和 `virtusertable` 选项设置 mailertable 和 virtusertable 数据库的位置。`redirect` 选项允许您拒绝已移动用户的邮件并提供新地址。`always_add_domain` 选项会在所有投递的邮件中为主机名添加本地域名。`use_cw_file` 和 `use_ct_file` 选项分别告知 sendmail 使用 `/etc/mail/local-host-names` 文件作为此邮件服务器的备用主机名，以及使用 `/etc/mail/trusted-users` 文件作为可信用户名。（可信用户可以以另一个用户的名义发送邮件，而不会产生警告信息。）

`local_procmail` 选项设置了用于投递本地邮件（procmail）的命令，以及该命令的选项（包括 $h 主机名和 $u 用户名）。`access_db` 选项设置了访问数据库的位置，该数据库用于标识哪些主机和用户被允许通过服务器中转邮件。`blacklist_recipients` 选项开启了服务器阻止选定用户、主机或地址的传入邮件的功能。（`access_db` 和 `blacklist_recipients` 特性对于阻止垃圾邮件非常有用。）

EXPOSED_USER('root')dn!
DAEMON_OPTIONS('Port=smtp,Addr=127.0.0.1, Name=MTA')dn!

`EXPOSED_USER` 行允许显示 root 用户名而不是伪装名（masquerade name）。目前，`DAEMON_OPTIONS` 行仅允许接受由本地主机创建的传入邮件。如果您希望允许来自 Internet 或其他网络接口（如本地局域网）的传入邮件，请务必注释掉此行为。

FEATURE('accept_unresolvable_domains')!dn!

`accept_unresolvable_domains` 选项已开启，这会导致您接受来自域名不可解析的主机的邮件。如果您有需要使用您的邮件服务器的客户端计算机（例如拨号计算机），请保持此选项开启。但是，关闭此选项有助于消除垃圾邮件。

LOCAL_DOMAIN('localhost.localdomain')!dn!
MAILER(smtp)!dn!
MAILER(procmail)!dn!

这里的 `LOCAL_DOMAIN` 选项会导致 localhost.localdomain 被接受作为您的本地计算机的名称。您的 sendmail.mc 文件中的最后几行定义了要在您的服务器上使用的邮件器（mailer）。`/usr/share/sendmail-cf/mailers` 目录包含 smtp、procmail 和其他邮件器的定义。在对 sendmail.mc 文件进行所需的更改后，您可以按照“启动 sendmail 和生成数据库文件”一节中所述的方法重新生成 sendmail.cf 文件。

## 定义传出邮件访问

每当您的 sendmail 服务器收到一条旨在作为传出邮件的电子邮件消息时，服务器需要决定是接受还是拒绝该消息的中转。过于严格的策略可能会阻止合法邮件的发送。过于宽松的策略可能会使您的服务器对垃圾邮件发送者敞开大门。

鉴于当前电子邮件滥用的现状，您不能运行开放中继（即您的服务器只是将其收到的所有消息中继到请求的邮件服务器）。垃圾邮件发送者可以使用被称为“蜘蛛”的软件来寻找开放中继。如果您让您的邮件服务器保持开放，他们会很快找到您并您的机器来中继他们的垃圾邮件。垃圾邮件发送者使用您的机器可能会导致以下后果：

-   您可能会被列入黑名单。一些电子邮件黑名单维护者会自行寻找开放中继并在滥用被报告之前就将其屏蔽。使用这些黑名单的服务器将屏蔽来自您所有的邮件，即使是合法邮件也是如此。
-   人们会讨厌您。您的邮件服务器将被标识为发送垃圾邮件的服务器。因此，人们可能会对您的服务器进行报复，或者至少非常希望您停止向他们发送广告，以帮助他们摆脱债务或在某些方面提升自己。

本节描述了如何设置 sendmail 访问文件（`/etc/mail/access`）以包含一组合理的规则，定义您的服务器将为谁中转邮件。使用访问文件，sendmail 可以根据发件人的主机/域名、IP 地址或电子邮件地址做出是否中继消息的决定。您可以进一步通过检查与消息关联的 Connect、From 或 To 数据中的这些地址来细化匹配。

然后，您可以让服务器在匹配时执行以下四种基本操作：

-   **RELAY** — 您的邮件服务器只需将消息发送到邮件消息中请求的邮件服务器。
-   **REJECT** — 消息被拒绝（不予中继），并告知发件人该消息已被拒绝。
-   **DISCARD** — 消息被静默丢弃，且不会告知发件人。
-   **ERROR: text you choose** — 您可以在此处添加一些信息性文本，以给出未发生中转的一些原因。

默认情况下，`/etc/mail/access` 文件仅中转由直接登录到邮件服务器（localhost）的用户发送的消息。如果未明确允许，来自所有其他机器的用户都不被允许中转消息。默认情况下访问文件的设置如下：

```text
localhost.localhost			RELAY
localhost				RELAY
127.0.0.1			RELAY
```

设置这些默认值后，只有从本地机器发送的邮件才会被中继。因此，如果您发送的所有传出邮件都是在直接登录到服务器的情况下完成的，则无需修改此文件。以下示例说明了如何有选择地决定中继或拒绝由您的 sendmail 服务器收到的邮件：

```text
Connect:192.168				RELAY
Connect:linuxtoys.net			RELAY
Connect:spammer-domain.com		REJECT

From:chris@linuxtoys.net			RELAY
To:spidermaker.com			RELAY
To:former-user@linuxtoys.net		ERROR: User no longer works here
```

在 `Connect:192.168` 行中，网络地址（可能是您的局域网中使用的 IP 地址的第一部分）被允许中继邮件。这是允许从本地局域网上的任何机器发送邮件的所有用户的邮件被中继的一种好方法。在下一行（`Connect:linuxtoys.net`）中，基本上来自指定域名内任何机器的邮件都被允许中继。第三行代表一个您已知为垃圾邮件中继的域名，因此您拒绝源自该域名的消息。

接下来三行说明了如何根据与消息关联的 From 和 To 名称来处理收到的中转邮件。如您所见，第一个示例允许中继来自 `chris@linuxtoys.net` 的任何消息。在最后一个示例中，转发给特定人员（`former-user@linuxtoys.net`）的邮件被拒绝，并向发件人发送自定义错误消息（在此情况下为“User no longer works here”）。

> **注意：** 在基于用户电子邮件地址创建中继规则时要小心。由于这些值是由用户自己报告的，因此容易受到欺骗。

调整此文件以满足您的需求后，您必须重建访问数据库（`access.db` 文件）才能使更改生效。有关此主题的更多信息，请参阅“启动 sendmail 和生成数据库文件”。

## 配置虚拟服务器

如果您已经为一个域名设置了 sendmail 邮件服务器，那么将来您很可能希望从同一台计算机提供多个域名的服务。要在同一台计算机上创建虚拟服务器，您必须将正在服务的每个域名的名称添加到 `/etc/mail/local-host-names` 文件中。

