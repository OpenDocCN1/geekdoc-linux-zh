
`local_transport = lmtp:unix`

`local_transport = local`

## alias_maps

`alias_maps` 参数告诉 Postfix 使用哪些表进行别名。别名提供了一种将传入邮件重定向到不同账户的方法。默认情况下，Postfix 将搜索本地别名数据库，然后是 NIS 数据库（如果机器使用 NIS）。

```
alias_maps = hash:/etc/aliases
```

## alias_database

`alias_database` 参数与 `alias_maps` 参数类似，不同之处是 `alias_database` 限于由 `newaliases` 构建的表。

```
alias_database = dbm:/etc/aliases
```

## home_mailbox

`home_mailbox` 参数允许你更改接收邮件的目录。该值是相对于用户的目录指定。因此，`Maildir/` 的值会将邮件放在用户的家目录中，就像 Qmail 这样做一样。默认情况下，传入邮件通常被重定向到 `/var/spool/mail`。

```
home_mailbox = Maildir/
```

## mail_spool_directory

`mail_spool_directory` 参数指向包含传统 Unix 风格邮箱文件的目录。在大多数 Linux 系统上，默认值为 `/var/spool/mail`。

```
mail_spool_directory = /var/spool/mail
```

## mailbox_command

`mailbox_command` 参数允许你指定一个执行以代替正常邮件投递的程序。该程序以接收者的用户的身份和权限运行。这允许使用 `procmail` 命令，这是一种在 Sendmail 安装中经常使用的本地投递程序。

此参数有些独特之处，它不替换以美元符号（`$`）开头的 Postfix 变量。这允许你指定以美元符号开头的环境变量。特别是，此命令为以下内容设置环境值：

- `SHELL`
- `HOME`
- `USER`
- `EXTENSION`
- `LOGNAME`
- `LOCAL`
- `DOMAIN`

```
mailbox_command = /usr/bin/procmail -a $DOMAIN -d $LOGNAME
```

## mailbox_transport

如果你在 `master.cf` 中指定了可选的邮件传输机制，此参数将导致在处理转发文件和别名之后调用。此参数优于其他相关参数（如 `mailbox_command`）。

```
mailbox_transport = newtransport
```

## fallback_transport

`fallback_transport` 参数与 `mailbox_transport` 参数类似，不同之处是它仅对密码文件中未列出的用户调用。

```
fallback_transport =
```

## luser_relay

`luser_relay` 参数对于向在机器没有账户的用户投递邮件非常。如果传入的消息发送给当前机器上的未知用户，通常会向发送者返回退信邮件。设置了 `luser_relay` 后，向未知用户的邮件将发送到另一个机器上的另一个用户。某些特殊变量可在此参数中使用：

- `$recipient` 是完整地址名。
- `$shell` 是接收者的 shell。
- `$user` 是收件者的用户名。
- `$local` 是收件者的本地信息。
- `$domain` 是收件者的域名信息。

此外，可以使用布尔语法来条件地替换值。指定 `${variable?value}` 会导致在变量存在时使用该变量的值，如果 `$variable` 不存在，则使用指定的 `value` 值。

```
user_relay = $user@other.host
```

## smtpd_recipient_limit

`smtpd_recipient_limit` 设置了单条邮件中可以包含的收件者最大数量。

```
smtpd_recipient_limit = 1000
```

## smtpd_timeout

`smtpd_timeout` 参数设置了在声明超时之前，SMTP 响应之间允许的时间间隔。该数字后面跟着 `s`（秒）、`m`（分钟）或 `h`（小时）。

```
smtpd_timeout = 300s
```

## mynworks_style

`mynetworks_style` 用于建立哪些机器应该被本机器所信任。信任设置可以应用于整个网络类（A、B 或 C）、特定的子网，或仅限本地主机。一旦确定了机器是受信任或不受信任的，Postfix 就可以用它来确定活动和限制。

```
mynetworks_style = class
mynetworks_style = subnet
mynetworks_style = host
```

## mynetworks

如果你没有使用 `mynetworks_style` 参数来声明受信任的网络，可以使用 `mynetworks` 参数显式地声明受 Postfix 信任的网络和节点。

```
mynetworks = 166.100.19.0/28, 127.0.0.0/8
```

## allow_untrusted_routing

`allow_untrusted_routing` 参数可以防止发送者指定的邮件从不受信任的客户端路由到 `relay_domains` 参数中列出的域名。垃圾邮件发送者有时会备份备用 MX 主机来将邮件转发给主 MX 主机。主 MX 主机在收到来自信任的备用 MX 主机的邮件后，会被欺骗向世界中转发这些垃圾邮件。此参数可以防止这种情况的发生。

```
allow_untrusted_routing = no
```

## maps_rbl_domains

`maps_rbl_domains` 参数允许你指定托管已知垃圾邮件发送者黑名单的域名。这允许 Postfix 拒绝来自常见垃圾邮件域名的邮件。默认情况下，不进行此类检查。

```
maps_rbl_domains = blackholes.mail-abuse.org
```

## smtpd_client_restrictions

`smtpd_client_restrictions` 参数允许你根据多种原因拒绝客户端。例如，你可以检查入站邮件的标头信息，并对照正则表达式表进行查询，如果它满足调用拒绝的规则，则拒绝该邮件。`reject_unauth_pipelining` 值用于拒绝通过流水线命令（提前发送命令）来加速交付的大群邮件程序发送邮件。`reject_unknown_client` 值拒绝声称发送自无效域名的邮件。`maps_rbl_domains` 参数拒绝来自 `$maps_rbl_domains` 变量中列出的任何域名的邮件，该变量包含已知垃圾邮件域名的列表。`permit_mynetwork` 允许访问受信任的主机。

```
smtpd_client_restrictions =
    check_client_access:/etc/postfix/client_access,
reject_unknown_client,
reject_unauth_pipelining,
reject_maps_rbl
```

## smtpd_sender_restrictions

`check_sender_access` 值允许根据正则表达式检查发送者的域名。`reject_unknown_sender_domain` 值导致在 DNS 服务器不知道该主机名时拒绝连接。`reject_non_fqdn_sender` 在发送者名称不是完全限定域名（FQDN）时会导致拒绝。

### 第 10 章：创建一个 SMTP 邮件服务器

```
smtpd_sender_restrictions =
    check_sender_access hash:/etc/postfix/sender_access,
reject_unknown_sender_domain,
reject_non_fqdn_sender
```

## smtpd_recipient_restrictions

`smtpd_recipient_restrictions` 参数引导 Postfix 在收件者名称不符合标准时拒绝邮件。`check_recipient_access` 值允许通过正则表达式对收件者名称进行过滤。`reject_unknown_recipient_domain` 值导致如果收件者主机 DNS 服务器未知，则拒绝连接。`reject_non_fqdn_recipient` 在收件者名称不包含完全限定域名时会导致拒绝。`check_relay_domains` 值允许如果客户端或收件者主机被 `$relay_domains` 变量中的条目覆盖，则允许邮件通过。
