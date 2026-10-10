

发送邮件。`TRUST_AUTH_MECH` 行将使 sendmail 允许使用除纯密码之外的认证机制（如果删除 `dnl` 注释符）。`confAUTH_MECHANISMS` 行可以配置允许使用的认证机制类型（如果删除 `dnl` 注释符）。上述接下来的几行将 sendmail 的证书目录位置设置为 `/etc/pki/tls/certs`，然后识别该目录中存储认证所需证书和密钥的不同文件。如果密钥文件需要能被 sendmail 以外的应用程序读取，则应该取消 `confDONT_BLAME_SENDMAIL` 行的注释。（通常，你不希望该文件被所有人读取。）

接下来的几行反映了 sendmail 使用的几个默认值：

```
dnl define('confTO_QUEUEWARN', '4h')
dnl define('confTO_QUEUERETURN', '5d')
dnl define('confQUEUE_LA', '12')
dnl define('confREFUSE_LA', '18')
dnl define('confTO_IDENT', '0')
```

上述被注释的行实际上显示了为某些超时条件设置的默认值。你可以删除注释并根据喜好更改这些值。`confTO_QUEUEWARN` 选项设置消息投递被延迟后，多久发送警告消息给发件人。默认值为 4 小时（4h）。`confTO_QUEUERETURN` 选项设置不可投递的消息在多久后返回。`confQUEUE_LA` 和 `confREFUSE_LA` 选项分别设置接收邮件被排队或拒绝时的系统平均负载级别。`confTO_IDENT` 选项设置等待 IDENT 查询响应时的超时时间（默认为 0，表示没有超时）。

下面是几行 `FEATURE` 行：

```
dnl FEATURE('no_default_msa')
dnl FEATURE('smrsh', '/usr/sbin/smrsh')
dnl FEATURE('mailer', 'hash -o /etc/mail/mailertable.db')
dnl FEATURE('virthertable', 'hash -o /etc/mail/virthertable.db')
dnl FEATURE('redirect')
dnl FEATURE('always_add_domain')
dnl FEATURE(use_cw_file)
dnl FEATURE(use_ct_file)
dnl FEATURE('local_procmail', ',/procmail -t -Y -a $h -d $u')
dnl FEATURE('access_db', 'hash -TCMP; -o /etc/mail/access.db')
dnl FEATURE('blacklist_recipients')
```

`FEATURE` 宏用于设置一些特殊的 sendmail 功能。`no_default_msa` 功能告诉 sendmail 不要生成默认的 MSA 守护进程（通常设置为监听 587 端口）。`smrsh` 功能定义 `/usr/sbin/smrsh` 作为 sendmail 用于接收命令的简单 shell。`mailertable` 和 `virthertable` 选项设置了 mailertable 和 virthertable 数据库的位置。`redirect` 选项允许你拒绝已移动用户邮件并提供新地址。`always_add_domain` 选项使本地域名被添加到所有投递邮件的主机名中。`use_cw_file` 和 `use_ct_file` 选项分别告诉 sendmail 使用文件 `/etc/mail/local-host-names` 作为此邮件服务器的替代主机名，以及使用 `/etc/mail/trusted-users` 作为受信任的用户名。（受信任的用户可以作为其他用户发送邮件，而不会导致警告消息。）

`local_procmail` 选项设置了用于投递本地邮件的命令（procmail），以及该命令的选项（包括 `$h` 主机名和 `$u` 用户名）。`access_db` 选项设置了 access 数据库的位置，该数据库标识了哪些主机和用户允许通过服务器中继邮件。`blacklist_recipients` 选项开启了服务器阻止选定用户、主机或地址的传入邮件的功能。（`access_db` 和 `blacklist_recipients` 功能对于阻止垃圾邮件很有用。）

这里是影响 root 用户名的暴露方式以及 sendmail 守护进程监听哪些接口的两行：

```
EXPOSED_USER(`root')
DAEMON_OPTIONS(`Port=smtp,Addr=127.0.0.1, Name=MTA')
```

`EXPOSED_USER` 行允许显示 root 用户名，而不是伪装名称。目前，`DAEMON_OPTIONS` 行仅允许接受由本地主机创建的传入邮件。如果你希望允许来自互联网或其他网络接口（例如本地 LAN）的传入邮件，请务必注释掉此行。

```
FEATURE(`accept_unresolvable_domains')
```

`accept_unresolvable_domains` 选项已开启，导致你接受来自没有可解析域名的主机的邮件。对于大多数公共邮件服务器，你应该注释掉此行，以便不接受来自不可解析域名的邮件（这是减少垃圾邮件的好方法）。

```
LOCAL_DOMAIN(`localhost.localdomain')
MAILER(smtp)
MAILER(procmail)
```

此处的 `LOCAL_DOMAIN` 选项使得 `localhost.localdomain` 被接受为本地计算机的名称。你的 sendmail.mc 文件中的最后几行定义了要在服务器上使用哪些邮件器。`/usr/share/sendmail-cf/mailer` 目录包含 smtp、procmail 和其他邮件器的定义。在你对 sendmail.mc 文件进行所需更改后，你可以按照“启动 sendmail 并生成数据库文件”一节中描述的方法重新生成 sendmail.cf 文件。

## 定义传出邮件访问

每当你的 sendmail 服务器接收到一条旨在作为传出邮件的电子邮件消息时，服务器需要决定是接受还是拒绝该消息的中继。过于严格的政策可能会阻止合法邮件发出。过于宽松的政策则可能使你的服务器对垃圾邮件发送者开放大门。

鉴于当今电子邮件滥用的状况，你不应该运行开放中继（即你的服务器将所有接收到的消息中继到请求的邮件服务器）。垃圾邮件发送者可以使用被称为*爬虫*（*spiders*）的软件来寻找开放中继。如果你让你的邮件服务器保持开放，他们会迅速找到你并利用你的机器来中继他们的垃圾邮件。如果发生这种情况，你可能会遇到以下一种或所有情况：

-   **你可能会被列上黑名单。** 一些电子邮件黑名单维护者会主动查找开放中继并在滥用被报告之前将其屏蔽。使用这些黑名单的服务器将屏蔽来自你的所有邮件，即使是合法邮件。
-   **人们会讨厌你。** 你的邮件服务器会被识别为发送垃圾邮件的源头。因此，人们可能会对你的服务器进行报复，或者至少非常希望你停止向他们发送有关帮助他们摆脱债务或自我提升的广告。
-   **你面临罚款和入狱的可能。** 越来越多的法律正在制定，以试图阻止垃圾邮件的扩散。即使你没有主动发起垃圾邮件，你也可能因疏忽而获罪，或者你的机器被关停或没收。

本节描述如何设置 sendmail access 文件（`/etc/mail/access`），使其包含一组合理的规则，定义你的服务器将为谁中继邮件。使用 *access* 文件，sendmail 可以根据发件人的主机/域名、IP 地址或电子邮件地址来决定是否中继消息。你可以通过检查与消息关联的 Connect、From 或 To 数据中的这些地址来进一步细化匹配。

然后，你可以让服务器在匹配时采取四种基本操作：

-   **RELAY**（中继）— 你的邮件服务器可以将消息发送到邮件消息中请求的邮件服务器。
-   **REJECT**（拒绝）— 消息被拒绝（不中继），并告知发件人已拒绝。
-   **DISCARD**（丢弃）— 消息被静默丢弃，且不告知发件人。
-   **ERROR:** *你选择的文本* — 你可以在此添加一些说明性文本，以向发件人说明未发生中继的原因。

`/etc/mail/access` 文件默认仅中继来自直接登录到邮件服务器（*localhost*）的用户的消息。如果没有明确允许，来自其他所有机器的用户都不允许中继消息。以下是 access 文件的默认设置方式：

```
Connect:localhost.localdomain RELAY
Connect:localhost RELAY
Connect:127.0.0.1 RELAY
```

设置这些默认值后，仅中继从本地机器发送的邮件。因此，如果你发送的唯一传出邮件是在直接登录到服务器时完成的，你不需要

