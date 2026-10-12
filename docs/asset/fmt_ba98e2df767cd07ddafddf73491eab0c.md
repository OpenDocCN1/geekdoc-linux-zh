
```
######## Log all kernel messages to the console.
######## Logging much else clutters up the screen.
#kern.* /dev/console

######## Log anything (except mail) of level info or higher.
######## Don't log private authentication messages!
*.info;mail.none;authpriv.none;cron.none /var/log/messages

######## The authpriv file has restricted access.
authpriv.* /var/log/secure

######## Log all the mail messages in one place.
mail.* /var/log/maillog

######## Log cron stuff
cron.* /var/log/cron

######## Everybody gets emergency messages
*.emerg *

######## Save news errors of level crit and higher in a special file.
uucp,news.crit /var/log/spooler

######## Save boot messages also to boot.log
local7.* /var/log/boot.log
```

> 注意：对于 SUSE，我们需要配置 `syslog-ng.conf` 以定制我们在 `/var/log/messages` 中希望查看的信息类型。文件 `syslog-ng.conf` 位于 `/etc/syslog-ng` 目录中。

通过分析 `syslog.conf` 的示例，我们注意到 `mail.* /var/log/maillog` 这一行负责将所有与邮件相关的信息写入文件 `/var/log/maillog`。请参阅示例 9-3 以了解具体打印了哪些内容以及是如何打印的。

### 示例 9-3 /var/log/maillog 的部分内容

```
Sep 13 15:40:34 linux postfix[3343]: warning: hostname lnxmr2 is not a fully qualified name - set myhostname or mydomain in /etc/postfix/main.cf
Sep 13 15:40:35 linux postfix/postfix-script: fatal: the Postfix mail system is not running
Sep 13 15:41:38 linux postfix/postfix-script: fatal: the Postfix mail system is not running
Sep 13 15:45:31 lnxmr2 postfix/postfix-script: starting the Postfix mail system
Sep 13 15:45:31 lnxmr2 postfix/master[5627]: daemon started -- version 2.2.9, configuration /etc/postfix
Sep 13 15:47:43 lnxmr2 postfix/postfix-script: refreshing the Postfix mail system
Sep 13 15:47:43 lnxmr2 postfix/master[5627]: reload configuration /etc/postfix
Sep 13 15:47:43 lnxmr2 postfix/master[5627]: daemon started -- version 2.2.9, configuration /etc/postfix
Sep 13 17:55:02 lnxmr2 postfix/postfix-script: fatal: the Postfix mail system is not running
```

`*.info;mail.none;authpriv,none;cron.none /var/log/messages` 这一行负责禁止在文件 `/var/log/messages` 中记录私有认证消息。

请参阅示例 9-4 以了解在文件 `/etc/syslog.conf` 中配置的信息是如何记录在 `/var/log/messages` 中的。

### 示例 9-4 /var/log/messages 的示例
