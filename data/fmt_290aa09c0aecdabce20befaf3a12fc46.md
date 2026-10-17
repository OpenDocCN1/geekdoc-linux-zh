
```
#myorigin = /etc/mailname
smtpd_banner = $hostname SMTP $mail_name (Ubuntu)
biff = - no
append_dot_mydomain = no
#delay_warning_time = 4h
smtpd_tls_cert_file=/etc/ssl/certs/ssl-cert-snakeoil.pem
smtpd_tls_key_file=/etc/ssl/private/ssl-cert-snakeoil.key
smtpd_use_tls=yes
smtpd_tls_session_cache_database = \
  btree:${queue_directory}/smtpd_scache
smtpd_tls_session_cache_database = \
  btree:${queue_directory}/smtp_scache
```

```
myhostname = ubuntu.vonhagen.org
alias_maps = hash:/etc/aliases
ialias_database = hash:/etc/aliases
myorigin = /etc/mailname
mydestination = mail.vonhagen.org, ubuntu.vonhagen.org,
localhost.vonhagen.org, localhost
relayhost = \
mynetworks = 127.0.0.0/8 ::ffff:127:0:0.1/104
mailbox_size_limit = 0
recipient_delimiter = +
inet_interfaces = all
html_directory = /usr/share/doc/postfix/html
```

按照顺序，这些变量执行以下操作：

- `myorigin`：Debian 及其衍生发行版（如 Ubuntu）的一个选项，允许你使用 `/etc/mailname` 文件的第一行作为邮件传输器的名称。这实际上位于默认文件的后部分。
- `smtpd_banner`：设置建立 SMTP 连接时显示的横幅（banner）的值。在这种情况下，该横幅是由配置文件中设置的变量的值构造的。
- `biff`：决定当 Postfix 处理入邮件队列时，是否应对每个有新邮件的用户使用本地邮件通知服务（biff）。在这种情况下，它是禁用的，因为 biff 通知可能会导致性能损耗，并且仅在存放邮件文件的机器上相关。使用本地邮件文件的用户可以自己开启此功能。
- `append_dot_mydomain`：决定 Postfix 是否应向发送到 user@host 的邮件附加域名名。现在，这通常由 MUA 处理，因此它是禁用的。
- `delay_warning_time`：取消此参数的注释将指定如果发送的邮件尚未投递，一段时间后通知用户。毕竟，远程站点可能在使用 Microsoft Exchange，并且可能处于离机状态。
- `smtpd_tls_cert_file`：识别此系统上文件的完整路径，该文件持有机器在使用 TLS（传输层安全）发送消息时使用的证书。
- `smtpd_tls_key_file`：识别此系统上文件的完整路径，该文件持有在使用 TLS（传输层安全）发送消息时为 Postfix SMTP 客户端提供的 RSA 私钥。
- `smtpd_use_tls`：决定当远程 SMTP 服务器宣布 STARTTLS 支持时，此 Postfix 服务器是否应使用 TLS。如果远程服务器未宣布 STARTTLS 支持，消息将以明文发送。

## 修改出站邮件中的地址

尽管本地网络上的所有主机现在都可以通过邮件服务器发送邮件，但许多 MUA 使用发送邮件主机的完全限定域名发送邮件。这意味着来自 vwh（位于 64bit.vonhagen.org 主机上）的邮件以电子邮件地址 vwh@64bit.vonhagen.org 发出。虽然我并不不在意这一点，但我可能在那里没有邮箱箱，因此人们无法回复我。

为了解决这个问题，你可以使用 Postfix 配置参数 `masquerade_domains` 来识别 Postfix 应该重写哪些出站邮件地址的域名，使其看起来仅仅是 user@domain.com。在这种情况下，来自 vwh@64bit.vonhagen.org 的邮件将简单地以 vwh@vonhagen.org 发出，这是我的真实电子邮件地址。在这种情况下，我会在 `main.cf` 中添加 `masquerade_domains` 设置。

```
masquerade_domains = vonhagen.org
```

然后我重启 Postfix 服务器（使用 `sudo /etc/init.d/postfix restart`）或使用 `sudo postfix reload` 命令来激活活跃的 Postfix 守护进程，以获取我对配置文件的更改。

## 接收整个域的邮件

如前所述，`mydestination` 参数标识邮件主机将哪些邮件递交给本地。默认的 Postfix 配置文件接收 `localhost.localdomain`、`localhost`、机器的实际主机名，以及你在图 30-2 显示的配置屏幕指定的机器名称（如果它与机器的实际主机名不同）。为了让你的新 Postfix 邮件服务器成为你所有域的有效最终终点，你必须将你的域名添加到 `machine.cf` 文件的目标列表中。由于我将 `ubuntu.vonhagen.org` 指定为我的邮件名称，我的 `mydestination` 参数目前如下：

```
mydestination = ubuntu.vonhagen.org, ubuntu,
               localhost.vonhagen.org, localhost
```

我可以将我的域名添加到此列表中，或者添加我的域名并利用该参数的值来提供此信息。我会添加 `mydomain` 参数设置并更新 `mydestination` 参数的值，它们合并起来看起来如下：

```
mydomain = vonhagen.org,
mydestination = ubuntu.vonhagen.org, ubuntu,
               localhost.vonhagen.org, localhost, $mydomain
```

与其他配置文件的更改一样，我随后将使用 `sudo /etc/init.d/postfix restart` 重启 Postfix 服务器，或使用 `sudo postfix reload` 命令使活跃的 Postfix 守护进程获取我对配置文件的更改。

## 提示

当你进行本节建议的更改时，你可能还想在安装期间更改 `myorigin` 参数的值。`myorigin` 被设置为你所指定的机器名称，这很有用，因为该值也被用在了你的 `mydestination` 参数值中，这可以正确处理有人向 `root@ubuntu.vonhagen.org` 发送邮件的情况。然而，在安装之后，让 `myorigin` 与 `mydomain` 的值相同更有用。

## 激活 Qpopper 以支持 POP/POP3

Qpopper（[www.eudora.com/products/unsupported/index.html) 是由高通公司提供的一种流行的免费 POP/POP3 服务器，他们同时也销售和赠送 PC 和 Macintosh 的 MUA（邮件客户端）Eudora。我喜欢 Qpopper 是因为它支持 Postfix 在 Ubuntu 上默认使用的原生 Linux/Unix 邮件箱格式。（当使用 mbox 邮件箱格式时，所有消息都存储在一个文件中，每条消息都以字符串“From user@domain,”开头，紧接着是消息的时间戳。）我在安装 Postfix 的第 30 章：设置邮件服务器的节中建议过你安装 Qpopper——如果你还没有安装并想在你的新邮件服务器上激活 POP3 支持，请现在安装它，然后继续本节。

## 注意

如前所述，POP/POP3 和 IMAP 是访问你电子邮件的替代协议，只要你在邮件服务器上为该协议安装了适当的服务器，就可以与 Postfix 使用。Qpopper 速度快、轻量且支持良好。如果你想同时支持 POP/POP3 和 IMAP，Cyrus IMAP（[http://asr.web.cmu.edu/cypress/) 和 Courier IMAP（[http://www.courier-mta.org/imap/) 是流行的选择，且 Ubuntu 仓库中都可用。然而，配置 Cyrus IMAP 服务器可能很复杂，而 Courier IMAP 只支持 Linux/Unix 邮件箱格式（即每条消息都存储在一个文件中），这并不是 Ubuntu 上 Postfix 的默认行为。一旦使用了速度快、简单且“开箱即用”的 Qpopper。■
