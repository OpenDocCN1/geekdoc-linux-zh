
## sendmail 执行的日志记录

sendmail 执行的日志记录量可在 sendmail.cf 文件中进行配置，但默认级别已能很好地覆盖信息通知和错误消息。默认情况下，syslog 设施（/etc/syslog.conf 文件）将 sendmail 的日志信息存储在 /var/log/maillog 文件中。本节展示了该文件中的一些示例。

每次守护进程启动时（这也会导致哈希别名数据库被重新生成），都会在 /var/log/maillog 文件中写入类似以下的信息消息：

```
Feb 16 12:52:40 toys sendmail[1758]: alias database /etc/aliases
rebuild by root
Feb 16 12:52:40 toys sendmail[1758]: /etc/aliases: 63 aliases, longest
10 bytes, 625 bytes total
Feb 16 12:52:40 toys sendmail[1787]: starting daemon (8.12.8):
SMTP+queuing@01:00:00
```

每次发送或接收消息时，都会创建一条日志文件条目：

```
Feb 16 12:54:34 toys sendmail[1120]: 0AA01120: from=root, size=161,
class=0, pri=30161, nrcpts=1,
msgids<199907191254.0AA01120@toys.linuxtoys.net>, relay=root@localhost
Feb 16 12:54:35 toys sendmail[1127]: 0AA01120: to=jxpatt, ctagddr=root
(0/0), delay=00:00:01, xdelay=00:00:00, mailer=local, stat=Sent
```

日志甚至会显示人们尝试他们可能不应该尝试的事情。wiz 和 debug 命令在 sendmail 的早期版本中实现，被发现是巨大的安全问题。恶意人员可能会检查日志条目，例如下面代码示例中所示的内容，以确保你没有运行易受攻击的 sendmail 守护进程。此外，expn 和 vrfy 命令（可通过配置选项禁用）可能会泄露超出你希望分发的更多信息。

```
Feb 16 13:03:27 toys sendmail[699]: NOQUEUE: "wiz" command from
localhost
[127.0.0.1] (127.0.0.1)
Feb 16 13:03:29 toys sendmail[699]: NOQUEUE: "debug" command from
localhost [127.0.0.1] (127.0.0.1)
Feb 16 13:03:37 toys sendmail[701]: NOQUEUE: localhost [127.0.0.1]:
expn oracle
Feb 16 13:03:43 toys sendmail[702]: NOQUEUE: localhost [127.0.0.1]:
vrfy oracle
```

## 配置 sendmail

文件 /etc/mail/sendmail.cf 包含用于控制 sendmail 守护进程行为的配置信息和可选值。整个文件长度超过 1,700 行，使其处理起来相当困难。sendmail.mc 文件的创建是为了简化 sendmail.cf 文件的生成。因此，我建议配置 sendmail 的步骤如下：

- 编辑 /etc/sendmail.mc 文件。配置 sendmail 所需的大部分工作都可以通过编辑此文件完成。
- 使用 m4 处理器从编辑后的 sendmail.mc 文件生成 sendmail.cf 文件。
- 检查你的 sendmail.cf 配置。如果要进行更改，请修改 sendmail.mc 文件并重新生成 sendmail.cf。

> 注意：你在 sendmail.mc 文件中使用的 m4 宏与 sendmail.cf 文件中的最终设置不同。要了解在 sendmail.cf 文件中找到的设置应使用哪些宏，请参阅 /usr/share/doc/sendmail/README.cf 文件。

- 重新启动 sendmail 服务器。

> 警告：由于 sendmail 在 Red Hat Linux 中的配置方式，不应直接修改 sendmail.cf 文件。如果 sendmail.mc 发生变化，sendmail 重启时 sendmail.cf 文件会自动重新生成。因此，直接对 sendmail.cf 所做的任何修改都会丢失。

以下各节提供了此过程的详细信息。

## 配置 sendmail.mc 文件

以下代码示例取自随 Red Hat 版本 sendmail 提供的 /etc/mail/sendmail.mc 文件。

> 注意：在 sendmail.mc 文件中，以 dnl（delete to new line，删除到新行）开头，后跟注释字符（###）的行是注释行。在大多数情况下，我在所示示例中已将其省略。

```
divert(-1)dnl
include(\`/usr/share/sendmail-cf/m4/cf.m4\`\'dnl
VERSIONID(\`setup for Red Hat Linux\`\'dnl
OSTYPE(\`linux\`\'dnl
```

sendmail.mc 文件的前几行执行一些清理工作。divert 行在生成配置文件时删除多余的输出。include 行导致 sendmail 所需的规则集被包含。VERSIONID 行将配置文件标识为 Red Hat 用（尽管此设置不会被检查，因此可以是任何你喜欢的内容）。然而，OSTYPE 必须设置为 linux 才能获得 sendmail 所需文件的正确位置。

```
dnl define(\`SMART_HOST\',\`smtp.your.provider\`)
```

默认情况下，sendmail 守护进程会尝试将你的外发电子邮件直接发送到其所指向的邮件服务器。如果你希望所有电子邮件都通过特定的邮件服务器中继，则可以删除上面 SMART_HOST 行中的注释（dnl，表示“delete to new line”，删除到新行）。然后，将 smtp.your.provider 更改为你想要使用的邮件服务器的完全限定域名。

```
define(`confDEF_USER_ID',`8:12')dnl
            define(`confTRUSTED_USER', `smmsp')dnl
```

与作为 root 用户运行不同，守护进程基于之前设置的 confDEF_USER_ID 行，以 mail 用户（UID 8）和 mail 组（GID 12）运行。这是良好的策略，因为它可防止可能入侵你的邮件服务器的人获得对机器的 root 访问权限。confTRUSTED_USER 行将 smmsp 添加到 sendmail 信任的用户列表中。其他受信任用户包括 root、uucp 和 daemon。（smmsp 用户拥有某些 sendmail spool 目录和邮件数据库文件的所有权。）

```
dnl define(`confAUTO_REBUILD')dnl
            define(`confTO_CONNECT', `1m')dnl
```

如果删除 dnl，confAUTO_REBUILD 行将指示 sendmail 在必要时自动重建别名数据库。confTO_CONNECT 行将 sendmail 等待初始连接完成的时间设置为一分钟（1m）。

```
define(`confTRY_NULL_MX_LIST',true)dnl
            define(`confDONT_PROBE_INTERFACES', true)dnl
```

当 confTRY_NULL_MX_LIST 为 true 时，如果接收服务器是主机最佳邮件交换（MX），则尝试直接连接到该主机。如果 confDONT_PROBE_INTERFACES 为 true，sendmail 守护进程将不会将本地网络接口插入已知等效地址列表中。

```
define(`PROCMAIL_MAILER_PATH', `/usr/bin/procmail')dnl
            define(`ALIAS_FILE', `/etc/aliases')dnl
            dnl define(`STATUS_FILE', `/etc/mail/statistics')dnl
```

接下来的三行（PROCMAIL_MAILER_PATH、ALIAS_FILE 和 STATUS_FILE）分别设置分发传入邮件的程序（默认为 procmail）、邮件别名数据库和邮件统计文件的位置。

```
define(`UUCP_MAILER_MAX', `2000000')dnl
            define(`confUSERDB_SPEC', `/etc/mail/userdb.db')dnl
            define(`confPRIVACY_FLAGS', `authwarnings,novrfy,noexpn,restrictqrun')dnl
            define(`confAUTH_OPTIONS', `A')dnl
```

UUCP_MAILER_MAX 行设置 UUCP 邮件传输代理接收的消息的最大大小（以字节为单位）。confUSERDB_SPEC 行设置用户数据库的位置（你可以在此处为特定用户覆盖默认邮件服务器）。confPRIVACY_FLAGS 行导致 sendmail 坚持使用某些邮件协议。例如，authwarnings 导致使用 X-Authentication-Warning 头并在日志文件中记录。novrfy 和 noexpn 设置可防止请求这些服务。restrictqrun 选项可防止 sendmail 的 -q 选项。

```
dnl define(`confAUTH_OPTIONS', `A p')dnl dnl TRUST_AUTH_MECH (`EXTERNAL DIGEST-MD5 CRAM-MD5 LOGIN PLAIN')dnl dnl define(`confAUTH_MECHANISMS', `EXTERNAL GSSAPI DIGEST-MD5 CRAM-MD5 LOGIN PLAIN')dnl dnl define(`confCACERT_PATH', `/usr/share/ssl/certs') dnl define(`confCACERT', `/usr/share/ssl/certs/ca-bundle.crt') dnl define(`confSERVER_CERT', `/usr/share/ssl/certs/sendmail.pem') dnl define(`confSERVER_KEY', `/usr/share/ssl/certs/sendmail.pem') dnl define(`confDONT_BLAME_SENDMAIL', `groupreadablekeyfile')dnl
```

刚才显示的一组行（全部以 dnl 开头，因此被注释掉了）可以取消注释（删除初始的 dnl）以提供某些功能。confAUTH_OPTIONS 行设置与 SMTP 认证一起使用的选项。此示例（带 A 和 p 选项）允许使用明文登录的已认证用户中继邮件。TRUST_AUTH_MECH 行将导致 sendmail 允许除明文密码之外的认证机制。上面的接下来的四行应取消注释以启用证书（如果密钥文件需要被 sendmail 以外的应用程序读取，则设置上面的最后一行）。

```
dnl define(`confTO_QUEUEWARN', `4h')dnl dnl define(`confTO_QUEUERETURN', `5d')dnl dnl define(`confQUEUE_LA', `12')dnl dnl define(`confREFUSE_LA', `18')dnl define(`confTO_IDENT', `0')dnl
```

上面的注释行实际上显示了为某些超时条件设置的默认值。你可以删除注释并更改这些值。confTO_QUEUEWARN 设置在消息投递被延迟后多久向发件人发送警告消息。四小时（4h）为默认值。confTO_QUEUERETURN 选项设置在不可投递消息被退回之前的时间。confQUEUE_LA 和 confREFUSE_LA 分别设置接收邮件被排队或拒绝的系统负载平均值。confTO_IDENT 选项设置等待 IDENT 查询响应时的超时时间（默认为 0，表示无超时）。

```
FEATURE(`smrsh', `/usr/sbin/smrsh')dnl FEATURE(`mailertable',`hash -o /etc/mail/mailertable.db')dnl FEATURE(`virtusertable', `hash -o /etc/mail/virtusertable.db')dnl FEATURE(`redird') dnl FEATURE(`always_add_domain')dnl FEATURE(`use_cw_file')dnl FEATURE(`use_ct_file')dnl FEATURE(`local_procmail',`procmail -t -Y -a $h -d $u')dnl FEATURE(`access_db', `hash -T<TMPF> -o /etc/mail/access.db')dnl FEATURE(`blacklist_recipients')dnl
```
