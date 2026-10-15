
# 第6 章 日志

`<管道的完整路径>`

## Red Hat: 默认 syslog.conf

以下显示 Red Hat 的默认 `syslog.conf`。

- `*.alert;mail.none /var/adm/alerts`
- `*.crit`
- `*=crit`
- `!alert`
- `*!debug`
- `/var/log/critical`
- `@loghost.my.site.com`
- `/dev/console`
- `root,operator,valjean`
- `*`
- `kern.* /dev/console`
- `*info /var/log/messages`
- `*authpriv /var/log/secure`
- `*cron /var/log/cron`
- `*emerg /var/log/news`
- `local1.* /var/log/spooler`
- `*boot /var/log/boot`
- `*notice`

### 基础操作

注意此 `syslog.conf` 防止了任何消息输出到控制台。如果系统控制台未被监控，则没有理由发送到那里。相反，如果你有人监控屏幕，那么取消此文件第三行的注释可能是明智的。

我们特别建议在此文件中添加一个条目，将所有消息发送到远程服务器。当然，这只有当你确实有一个集中日志服务器时才有意义。假设该机器存在且名为 `loghost.my.site.com`，在文件的最后一行输入：

```
*notice@loghost.my.site.com
```

更好的方法是在 `/etc/hosts` 文件中添加条目，指定 `loghost.my.site.com` 也称为 `loghost`。`syslog.conf` 的条目如下：

```
*notice@loghost
```

通过这种方式，如果日志主机发生 IP，你只需要更新一个文件。

## Solaris: 默认 syslog.conf

以下列表显示 Solaris 8 的默认 `syslog.conf`：

```
#ident "@($).syslog.conf    1.5    98/12/14 SMI"    / *SunOS 5.0 */
# Copyright 1991-1998 by Sun Microsystems, Inc.
# All rights reserved.
#n syslog configuration file.
#n 此文件由 m4 处理，因此对于引号（'\'')与 m4 保留字匹配的名称要小心。此外，在 ifdef 内部，包含逗号的参数必须引用。
#n*err:kern.notice;auth.notice               /dev/sysmsg
*err:kern.debug;daemon.notice;mail.crit      /var/adm/messages
*alert;kern.err;daemon.err                  operator
*alert                               root
*emerg                               *
# 如果非日志主机选择将身份消息
# 发送到日志主机，请取消注释以下行：
#auth.notice                               ifdef('LOGHOST', /var/log/authlog, @loghost)
mail.debug          ifdef('LOGHOST', /var/log/syslog, @loghost)
# 非 loghost 机器将使用以下行将“user”
# 日志消息记录在本地。
ifdef('LOGHOST', ,
user.err               /dev/sysmsg
user.err               /var/adm/messages
user.alert             'root, operator'
user.emerg
*
```
