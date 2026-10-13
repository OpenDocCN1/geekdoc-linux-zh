
``` 
define('CONFCACERT', '/usr/share/ssl/certs/bundle.crt') dnl

define('CONFSERVER_CERT', '/usr/share/ssl/certs/sendmail.pem') dnl

define('CONFSERVER_KEY', '/usr/share/ssl/certs/sendmail.pem') dnl

define('CONFDONT_BLAME_SENDMAIL', 'groupreadablekeyfile') dnl
```

这里显示的带有 `dnl` 的某些行（如果它们被注释掉了）可以通过取消注释（删除前面的 `dnl`）来提供某些功能。另一些则是显式的。`CONFAUTH_OPTIONS` 行可用于设置带有 SMTP 认证的选项。此示例（带有 `A` 和 `p` 选项）允许使用明文登录的认证用户发送邮件。`TRUST_AUTH_MECH` 行将使 sendmail 允许除明文密码以外的认证机制（如果删除了 `dnl`）。`AUTH_MECHANISMS` 行可以配置可使用的认证机制类型（如果删除了 `dnl`）。上面的新几行设置了 sendmail 证书的位置为 `/usr/share/ssl/certs`，然后识别该目录中持有认证所需的证书和密钥的不同文件。如果密钥文件需要被 sendmail 以外的应用程序读取，则应取消注释 `CONF_BLAME_SENDMAIL` 行。（通常情况下，你并不希望文件能被所有人读取。）

``` 
define('CONFTO_QUEUERETURN', '4h') dnl

define('CONFTO_QUEUERETURN', '5d') dnl

define('CONFQUEUE_LA', '12h') dnl

define('CONFREFUSE_LA', '18h') dnl

define('CONFTO_IDENT', '0h') dnl
```

上述被注释的行实际上显示了某些超时条件下设置的默认值。如果你喜欢，可以删除注释并更改这些值。`CONF_QUEUEWARN` 选项设置了邮件投递延迟到向发送者发送警告消息的时间。四小时（4h）是默认值。`CONFTO_QUEUERETURN` 选项设置了无法投递的邮件返回之前的时间。`CONFQUEUE_LA` 和 `CONFREFUSE_LA` 选项分别设置了收到的邮件进入队列或被拒绝的系统负载水平。`CONFTO_IDENT` 选项设置了等待接收 IDENT 查询响应的超时时间（如果设为 0，则意味着没有超时）。

``` 
FEATURE("no default msa") dnl

FEATURE("smsh", /usr/sbin/smsh) dnl

FEATURE("mailertable", hash -o /etc/mail/mailertable.db) dnl

FEATURE("virtertable", hash -o /etc/mail/virtertable.db) dnl

FEATURE("redirect") dnl

FEATURE("always add domain") dnl

FEATURE("use cw_file") dnl

FEATURE("use ct_file") dnl

FEATURE("local procmail", procmail -t -Y -a $h -d $u) dnl

FEATURE("access_db", hash -TMWPE -o /etc/mail/access.db) dnl

FEATURE("blacklist_recipients") dnl
```

`FEATURE` 用于设置某些特殊的守护进程功能。该特性告诉 send 不要生成默认的 MSA 守护进程（通常设置在端口 S87）。`smsh` 特性将 `/usr/sbin/smsh` 定义为 sendmail 用于接收命令的简单 shell。`mailertable` 和 `virtertable` 选项设置了 mailertable 和 virtertable 数据库的位置。`redirect` 选项允许你拒绝已移动用户的邮件，并提供新地址。`always_add domain` 选项会导致在所有投递的邮件中将本地名添加到主机名中。`use_cw_file` 和 `use_ct_file` 选项分别告诉 sendmail 使用 `/etc/mail/local-names` 文件作为此邮件服务器的备用主机名，使用 `/etc/mail/trusted-users` 作为可信任用户名。（可信任用户可以）

`local procmail` 选项设置了入站邮件的命令（`procmail`）。`access_db` 选项设置了访问数据库的位置，`blacklist_recipients` 选项开启了拦截用户。`FEATURE` 用于设置某些特殊的守护进程功能。该特性告诉 send 不要生成默认的 MSA 守护进程（通常设置在端口 S87）。`smsh` 特性将 `/usr/sbin/smsh` 定义为 sendmail 用于接收命令的简单 shell。`mailertable` 和 `virtertable` 选项设置了 mailertable 和 virtertable 数据库的位置。`redirect` 选项允许你拒绝已移动用户的邮件，并提供新地址。`always_add domain` 选项会导致在所有投递的邮件中将本地名添加到主机名中。`use_cw_file` 和 `use_ct_file` 选项告诉 sendmail 使用 `/etc/mail/local-names` 文件作为此邮件服务器的备用主机名，使用 `/etc/mail/trusted-users` 作为可信任用户名。（可信任用户可以）

`local procmail` 选项设置了入站邮件的命令（`procmail`）。`access_db` 选项设置了访问数据库的位置，`blacklist_recipients` 选项开启了拦截用户。`FEATURE` 用于设置某些特殊的守护进程功能。该特性告诉 send 不要生成默认的 MSA 守护进程（通常设置在端口 S87）。`smsh` 特性将 `/usr/sbin/smsh` 定义为 sendmail 用于接收命令的简单 shell。`mailertable` 和 `virtertable` 选项设置了 mailertable 和 virtertable 数据库的位置。`redirect` 选项允许你拒绝已移动用户的邮件，并提供新地址。`always_add domain` 选项会导致在所有投递的邮件中将本地名添加到主机名中。`use_cw_file` 和 `use_ct_file` 选项告诉 sendmail 使用 `/etc/mail/local-names` 文件作为此邮件服务器的备用主机名，使用 `/etc/mail/trusted-users` 作为可信任用户名。（可信任用户可以）

## 第 19 章：设置邮件服务器 765

`accept_unvable_domains` 选项开启，会导致你接受来自无法解析域名的邮件。如果你有客户（如拨号计算机）需要使用你的邮件服务器，关闭此选项。然而，关闭它可以帮助消除垃圾邮件。

``` 
LOCAL_DOMAIN=`localhost.localdomain` dnl

MAILER(smtp) dnl

MAILER(procmail) dnl
```
