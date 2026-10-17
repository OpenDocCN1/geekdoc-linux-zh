
进入 `/etc/mail/relay-domains` 目录，找到 `xxx.json`。

- `/etc/mail/relay-domains`: 在此文件中列入您的域名，以确保源自您域名名的电子邮件可以被此网关接受并投递到任何地方。

- `*` 在文件中列出我们实际上中继邮件的域名。
# 如果此处未列出域名，则拒绝该域名的邮件中继。
`starlight.com`
`eng.starlight.com`

由于 `sendmail` 将 `relay-domains` 视为纯文本文件，您不需要执行其他操作来处理它。

- `/etc/mail/sendmail.cw`: 列出主机已知的所有名称，以便 `sendmail` 识别发送到任何这些主机名的电子邮件确实是发送给该系统的。由于该系统是该域的邮件中枢，也在此处列出域名；大多数电子邮件发送到 `username@starlight.com`，您希望 `sendmail` 识别出 `starlight.com` 是引用此主机的另一种方式。

# 规划邮件服务

一如既往，在做完这些更改后，您需要重启 `sendmail`。

# DNS 配置

为了确保从任何互联网站点发送的所有电子邮件都能正确到达 `starlight.com` 域名，请在 `starlight.com` DNS 服务器表中输入类似示例的条目。

| `starlight.com` IN MX 10 gw |
| `gw` IN A 205.172.3.46 |

此示例假设网关的 IP 地址为 `205.172.3.46`。任何尝试向 `username@starlight.com` 发送电子邮件的互联网站点都会执行 DNS 查询，并发现所有发往 `starlight.com` 的邮件交换器（MX）记录都应该直接发送到 `gw.starlight.com`，优先级为 10。

如您所见，所有入邮件都通过网关到达邮件中枢。此操作不会影响出邮件，因为它们由邮件中枢和网关上的 `sendmail` 直接处理，不涉及 DNS。记住，该域名中的邮件客户端将所有内容发送到邮件中枢进行处理，因此它们也不查看 DNS。

# DNS 域名和带有一个互联网连接的子域名

本节描述了一个更复杂的示例，其中 DNS 域名——`starlight.com` 用于 Starlight 公司的总部，子 DNS 域名——`eng.starlight.com` 用于公司的工程部门。考虑此配置的以下问题。

- 每个域名都需要独立于其他域名发送内部和外部电子邮件。
- 两个域名必须能够相互发送电子邮件。
- 只有其中一个域名（`starlight.com`）具有连接的连接，但两者都需要与互联网站点发送和接收电子邮件。两个域名的网络是互连的。

起初，这个示例看起来相当复杂，但您可以使用五个配置文件来处理它。

## DNS 域名和带有一个互联网连接的子域名 89

1. 一个用于名为 `gw.starlight.com` 的网关。
2. 一个用于名为 `mailhost.starlight.com` 的公司邮件中枢。
3. 一个用于名为 `mailhost.eng.starlight.com` 的工程邮件中枢。
4. 用于 `starlight.com` 域名的每个客户端。
5. 用于 `eng.starlight.com` 域名的每个客户端。

# 网关配置

此网关使用与第 84 页上“网关配置”部分相同的宏配置文件。再次，您通过外部数据库文件指定差异。

## 网关的外部数据库

- `*` `/etc/mail/mailertable`: 使用此文件使网关能够正确处理所有来自互联网并发往以下常见格式的入邮件：`username@starlight.com`, `username@eng.starlight.com`，或者更罕见的 `username@hostname.starlight.com` 和 `username@hostname.eng.starlight.com`。当发往公司域时，邮件通过 SMTP 传输到 `mailhost.starlight.com` 进行最终处理。当发往工程域时，邮件通过 SMTP 传输到 `mailhost.eng.starlight.com` 进行最终处理。

> 此系统作为下面列出的所有 DNS 域的 `sendmail` 网关
* 注意围绕邮件中枢名称的 `'*'` 确保
* 此网关不会查找 MX 记录，从而防止
* 出现恶性的 MX 循环

```
starlight.com smtp:[mailhost.starlight.com]

starlight.com:[mailhost.starlight.com]

eng.starlight.com:[mailhost.eng.starlight.com]

eng.starlight.com smtp:[mailhost.eng.starlight.com]
```

记得在该文件上运行 `makemap` 命令。

- `*` `/etc/mail/relay-domains`: 使用此文件确保 `sendmail` 将所有发往 `starlight.com` 或 `eng.starlight.com` 源或目的地址的邮件中继到此网关。

# 规划邮件服务

```
# 在文件中列出我们实际上中继邮件的域名。

# 如果此处未列出域名，则拒绝该域名的邮件中继。

starlight.com

eng.starlight.com
```

- `/etc/mail/sendmail.cw`: 列出主机已知的所有名称，以便 `sendmail` 识别发送到任何这些主机名的电子邮件确实是发送给该系统的。由于该系统是该域的邮件中枢，也在此处列出域名；大多数电子邮件发送到 `username@starlight.com`，您希望 `sendmail` 识别出 `starlight.com` 是引用此主机的另一种方式。

# 公司邮件中枢

- `*` `/etc/mail/mailertable`: 使用此文件使网关能够正确处理所有来自互联网并发往以下常见格式的入邮件：`username@starlight.com`, `username@eng.starlight.com`，或者更罕见的 `username@hostname.starlight.com` 和 `username@hostname.eng.starlight.com`。当发往公司域时，邮件通过 SMTP 传输到 `mailhost.starlight.com` 进行最终处理。当发往工程域时，邮件通过 SMTP 传输到 `mailhost.eng.starlight.com` 进行最终处理。

`domain`，在此处列出 `starlight.com` 域名。大多数电子邮件发送到 `username@starlight.com`，你希望让 `sendmail` 识别出 `starlight.com` 是指代此主机的另一种方式。

```
# 列出邮件中枢已知的所有名称，以便 sendmail

# 不会产生混淆，认为它不应该

# 将邮件投递到该系统正确的邮件队列中。注意

# DNS 域名本身位于列表末尾，因为

# 有多多邮件的地址是 username@starlight.com

mailhost.starlight.com
```

由于 `sendmail` 将 `sendmail.cw` 视为纯文本文件，你不需要进行任何其他操作来处理它。

一如既往，一旦你执行了这些更改，请重启 `sendmail`。

## 企业级客户端配置

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
