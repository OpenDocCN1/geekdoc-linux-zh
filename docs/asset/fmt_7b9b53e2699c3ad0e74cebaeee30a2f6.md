
# 处理所有以 eng.starlight.com 结尾的内容

* 同样，本地处理任何地址为
* `username@hostname.eng.starlight.com` 的邮件，
`eng.starlight.com` `local`:
`eng.starlight.com` `relay`:
* # 将所有发往企业域的邮件转发到企业邮件
* 中枢
`starlight.com` `relaymailhost.starlight.com`
`starlight.com` `relaymailhost.starlight.com`
* # 将其他所有内容转发到 gw.starlight.com 进行处理
`relay@gw.starlight.com.`

```
最后一行开头的 `.` 相当于完全限定 DNS 节点（如 sun.com）中的最后一个点。在它前面没有任何内容时，这个点 (`.` 被解释为任何内容（如 com, gov, net, org 等）。由于由于中文件中任何之前的、更具体的规则都会覆盖此规则，我们可以设置规则，防止源自 eng.starlight.com 内部并发往 eng.starlight.com 内部的邮件到达网关并进入互联网，那里可能会被不法分子拦截。

同样注意，主机名结尾有一个点 (.)，以确保它是完全限定主机名。

使用 `makemap` 命令处理此文件，如下例所示。
```

```
# makemap hash /etc/mail/mailertable > /etc/mail/mailertable
```

## 邮件服务规划

- `/etc/mail/relay-domains`

在此文件中包含你的域名，以确保来自你域内部的电子邮件被此网关接受并投递到任何地方、任何位置。此外，转发发送或来自 `starlight.com` 域的任何内容。

```
# 在此文件中列出我们实际上转发邮件的域。
# 如果域名未在此处列出，则拒绝来自该域的邮件。
starlight.com
eng.starlight.com
```

由于 `sendmail` 将 `relay-domains` 视为纯文本文件，你不需要采取任何其他操作来处理它。

- `/etc/mail/sendmail.cw`

使用此文件列出此主机已知的全部名称，因为 `sendmail` 识别出发送到这些任何主机名的邮件确实是发给此系统的。此外，由于该系统是该域的邮件中枢，此处列出名称是因为大多数电子邮件发送到 `username@starlight.com`，而你希望 `sendmail` 识别出 `starlight.com` 是指代此主机的另一种方式。

```
# 邮件中枢已知的所有名称，以便
# sendmail 不会产生混淆，认为它不应该
# 将邮件投递到该系统正确的邮件队列中。注意
# 注意 DNS 域名本身位于列表末尾，因为
# 有多多邮件的地址是 username@eng.starlight.com
mailhost.eng.starlight.com
eng.starlight.com
```

由于 `sendmail` 将 `sendmail.cw` 视为纯文本文件，你不需要采取任何其他操作来处理它。一如既往，一旦你执行了这些更改，请重启 `sendmail`。

## 企业级配置

使用以下宏配置文件为 `starlight.com` 企业域中的每个客户端生成 `sendmail.cf` 文件。

```
dnl
dnl corp-client.mc:
dnl starlight.com 客户端宏配置文件
dnl
include('/usr/lib/mail/mc/cf.m4')
OSTYPE('solaris2')
FEATURE('nullclient','mailhost.starlight.com')
```

注意，仅激活了 `nullclient` 功能。此功能告诉所有客户端将本地生成的所有电子邮件发送到 `mailhost.starlight.com`，而不进行任何标头重写。

使用以下命令创建客户端 `sendmail` 配置文件。

```
# m4 /usr/lib/mail/corp-client.mc > /usr/lib/mail/corp-client.cf
```

将 `corp-client.cf` 配置文件复制到每个企业客户端工作站的 `/etc/sendmail.cf` 上。

## 工程部邮件中枢配置

企业邮件中枢的宏配置文件与网关的相同。因此，最终的 `sendmail` 配置文件也是相同的。此邮件中枢的行为由下面列出的 `sendmail` 外部数据库控制。

## 单一互联网连接的 DNS 域和子域

### 工程部邮件中枢的外部数据库

- `/etc/mail/mailertable`

由于该系统是该域的邮件中枢，请使用 `mailtertable` 文件确保所有入站邮件 `username@eng.starlight.com` 最终投递到此系统。该文件还处理极少数情况，即邮件地址为 `username@hostname.eng.starlight.com`。由于该系统不是该域的邮件网关，请确保所有从该域内部发送到互联网的电子邮件都转发到网关机器 (`gw.starlight.com`) 进行处理。

最后，如果邮件源自该域内部并发往企业域，请不要通过网关发送。相反，将其直接发送到企业邮件中枢。

```
# 处理所有以 eng.starlight.com 结尾的内容
* 同样，本地处理任何地址为
* username@hostname.eng.starlight.com 的邮件，
eng.starlight.com local:
eng.starlight.com relay:
* # 将所有发往企业域的邮件转发到企业邮件
* 中枢
starlight.com relaymailhost.starlight.com
starlight.com relaymailhost.starlight.com
* # 将其他所有内容转发到 gw.starlight.com 进行处理
relay@gw.starlight.com.
```

最后一行开头的 `.` 相当于完全限定 DNS 节点（如 `sun.com`）中的最后一个点。在它前面没有任何内容时，这个点 (`.` 被解释为任何内容（如 `com`, `gov`, `net`, `org` 等）。由于由于中文件中任何之前的、更具体的规则都会覆盖此规则，我们可以设置规则，防止源自 `eng.starlight.com` 内部并发往 `eng.starlight.com` 内部的邮件到达网关并进入互联网，那里可能会被不法分子拦截。

同样注意，主机名结尾有一个点 (.)，以确保它是完全限定主机名。

使用 `makemap` 命令处理此文件，如下例所示。

```
# makemap hash /etc/mail/mailertable > /etc/mail/mailertable
```

## 邮件服务规划

- `/etc/mail/relay-domains`

在此文件中包含你的域名，以确保来自你域内部的电子邮件被此网关接受并投递到任何地方、任何位置。此外，转发发送或来自 `starlight.com` 域的任何内容。

```
# 在此文件中列出我们实际上转发邮件的域。
# 如果域名未在此处列出，则拒绝来自该域的邮件。
starlight.com
eng.starlight.com
```

由于 `sendmail` 将 `relay-domains` 视为纯文本文件，你不需要采取任何其他操作来处理它。

- `/etc/mail/sendmail.cw`

使用此文件列出此主机已知的全部名称，因为 `sendmail` 识别出发送到这些任何主机名的邮件确实是发给此系统的。此外，由于该系统是该域的邮件中枢，此处列出名称是因为大多数电子邮件发送到 `username@starlight.com`，而你希望 `sendmail` 识别出 `starlight.com` 是指代此主机的另一种方式。

```
# 邮件中枢已知的所有名称，以便
# sendmail 不会产生混淆，认为它不应该
# 将邮件投递到该系统正确的邮件队列中。注意
# 注意 DNS 域名本身位于列表末尾，因为
# 有多多邮件的地址是 username@eng.starlight.com
mailhost.eng.starlight.com
eng.starlight.com
```

由于 `sendmail` 将 `sendmail.cw` 视为纯文本文件，你不需要采取任何其他操作来处理它。一如既往，一旦你执行了这些更改，请重启 `sendmail`。

## 企业级配置

使用以下宏配置文件为 `starlight.com` 企业域中的每个客户端生成 `sendmail.cf` 文件。

```
dnl
dnl corp-client.mc:
dnl starlight.com 客户端宏配置文件
dnl
include('/usr/lib/mail/mc/cf.m4')
OSTYPE('solaris2')
FEATURE('nullclient','mailhost.starlight.com')
```
