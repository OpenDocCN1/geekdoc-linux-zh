
上述注释行显示了某些超时条件的默认值。您可以根据需要移除 `*CONTO_` 行并更改这些值。`CONTO_QUEUEWARN` 选项设置了推迟发送以向发送者发送警告消息的时间。默认值为四小时（4h）。`CONTO_QUEUETURN` 选项设置了返回未定义消息之前的等待时间。`CONQUEUE_LA` 和 `CONREFUSE_LA` 选项分别设置了邮件队列或拒绝的系统层级。`CONTO_IDENT` 选项设置了等待 IDENT 查询响应的时间（默认值为 0，意味着没有超时）。

```
FEATURE(`no_default_msa` `*d`)*dnl

FEATURE(`smsh` `* /usr/bin/smsh -o`)*dnl

FEATURE(`mailertable` `*hash -o /etc/mail/mailertable.db`)*dnl

FEATURE(`virtuertable` `*hash -o /etc/mail/virtuertable.db`)*dnl

FEATURE(`always_add_domain` `)*dnl

FEATURE(`use_ct_file` `)*dnl

FEATURE(`local_procmail` `*procmail -t -Y -a $h -d $u`)*dnl

FEATURE(`access_db` `*hash -TMPF -o /etc/mail/access.db`)*dnl

FEATURE(`redirect` `)*dnl

FEATURE(`blacklist_recipients` `)*dnl
```

`FEATURE` 宏用于设置某些特殊功能。`no_default_msa` 功能告诉 sendmail 不要生成默认 msa 守护进程（通常监听 587 端口）。`smsh` 宏将 `/usr/bin/smsh` 定义为 sendmail 接收命令的简单 shell。`mailertable` 和 `virtuertable` 选项设置了 mailertable 和 virtuertable 数据库的位置。`redirect` 选项允许您为移动的用户重定向邮件并提供新地址。`always_add_domain` 选项设置在所有投递邮件的主机上添加本地域名。`use_ct_file` 选项告诉 sendmail 分别使用 `/etc/mail/local-host-name` 作为此邮件服务器的备用主机名，使用 `/etc/mail/trusted-users` 作为信任用户名（用户可以另一个用户的身份发送邮件而不会产生警告消息）。

`local_procmail` 选项设置了投递邮件的命令（procmail）以及命令选项（使用 `$h` 和 `$u` 名字）。`access_db` 选项设置了访问数据库的位置，该数据库标识哪些主机和用户允许通过服务器中继邮件。`blacklist_recipients` 选项开启服务器阻止针对选用户、主机或地址的入邮件的能力（`access_db` 和 `blacklist_recipients` 功能有助于拦截垃圾邮件）。

## 第 19 章：设置邮件服务器 807

```
EXPOSED_USER(`root`)=dnl

DAEMON_OPTIONS(`Port=smtp,Addr=127.0.0.1,Name=MTA`)=dnl
```

`EXPOSED_USER` 行允许 root 用户作为伪装名显示。目前，`DAEMON_OPTIONS` 行仅允许接受本地主机创建的入站邮件。如果您想允许来自互联网或其他网络接口（如局域网 LAN）的入站邮件，请务必注释此行。

```
FEATURE(`unresolvable_domains`)=dnl
```

`unresolvable_domains` 选项的作用导致您接受来自具有解析域名的计算机的邮件。如果您有客户端计算机（如拨号计算机）需要使用您的邮件服务器，请保持开启状态。然而，将其关闭有助于消除垃圾邮件。

```
LOCAL_DOMAIN(`localhost.localdomain`)=dnl

MAILER(`smtp`)=dnl

MAILER(`procmail`)=dnl
```
