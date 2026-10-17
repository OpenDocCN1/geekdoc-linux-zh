
此时，SpamAssassin 应该已经在运行，并根据您以及使用您邮件服务器的人的输入来识别垃圾邮件。接下来，每个用户需要决定如何处理被标记为垃圾邮件的邮件，如本节所述。

提示：您可以在 SpamAssassin 服务中使用的技术包括实时黑洞列表 (RBL) 和 SpamCop。通过 RBL (`www.mail-abuse.com/services/mds_rbl.html`)，您可以在垃圾邮件到达您的服务器之前就拦截它们。SpamCop (`www.spamcop.net`) 提供了一种服务，允许您将收到的垃圾邮件输入数据库，帮助他人拦截这些垃圾邮件。

# 设置邮件读取器过滤器

设置邮件读取器过滤标记为垃圾邮件的邮件。为了避免这个问题，这里采用的方法让您决定如何处理标记为垃圾邮件的邮件。用户甚至可以在邮件被认为是垃圾邮件时调整他们的阈值。

接下来，您应该让该邮件服务器的用户在他们的主目录中设置自己的偏好设置。在每个用户的 `$HOME/.spamassassin/user_prefs` 文件中设置的偏好有助于告诉 SpamAssassin 如何处理该用户的邮件行为。以下是用户可能希望在该文件中包含的行示例：

| required_hits 3 |
| :--- |
| whitelist_from smith@example.com bjones@example.net |
| blacklist_from *.example.org |

`required_hits` 行（默认情况下）设置了将邮件视为垃圾邮件所需的命中次数。命中次数基于 SpamAssassin.org 测试中匹配或不匹配准则的评分（参见 `http://spamassassin.org/assists.html`）。

`whitelist_from` 和 `blacklist_from` 行定义了不应被视为垃圾邮件（白名单）或应始终被视为垃圾邮件（黑名单）的人、单个主机或域名。要修改 SpamAssassin 行为的其他方法，请使用以下命令：

```bash
man Mail::SpamAssassin::Conf
```

# 在 Linux 中访问邮箱

当邮件在您的 `sendmail` 或 `postfix` 服务器上接收时，它们会被分类到文件中，每个文件代表一个用户的邮箱。信箱的默认位置是 `/var/mail/`。登录账户 `jsmith` 将拥有一个邮箱：`/var/mail/jsmith`

在登录邮件服务器时，`jsmith` 可以直接从终端输入 `mail` 来读取邮件。然而，由于大多数人更喜欢在舒适的电脑上获取邮件，您可以设置邮局协议 (POP3) 或互联网邮件传输协议 (IMAP)。

POP3 和 IMAP 服务器在网络上监听用户邮件的请求，然后将整个邮箱内容下载到用户的邮件读取器中（如 POP3），或者让用户在邮件留在服务器上进行管理（如 IMAP）。

通常，您的邮件服务器将配置为使用 POP3 或 IMAP 为用户提供邮件。下一节将介绍如何设置 IMAP 或 POP3 服务以允许访问电子邮件账户。

## 使用 dovecot 配置 IMAP 和 POP3

当用户被添加到 Fedora 时，系统会在 `/var/spool/mail/` 目录下根据用户用户名配置一个邮箱（例如 `/var/spool/mail/chris`）。该文件采用传统的 `mbox` 格式，所有邮件和附件都存储在一个文件中。通过在您的邮件服务器上配置 POP3 服务，用户将能够从其他机器上的电子邮件客户端下载其电子邮件消息。通过配置 IMAP，用户可以直接在服务器上对消息和文件夹进行操作。

以下步骤描述了如何在 Fedora 中使用 `dovecot` 配置 IMAP 或 POP3 服务。

1. 检查 `/etc/dovecot.conf` 文件中设置的值。在本示例中，我假设使用默认值，包括：

   - `mbox` — 所有邮件都存储在一个文件中。对于 IMAP 服务器，使用 Maildir 样式。Maildir 将每条消息存储在单独的文件中。
   - `protocols` — 这设置了要监听哪些协议。默认情况下 `imap` 和 `imaps` 是开启的。你可以添加 `pop3` 和 `pop3s`，使该行显示为：`protocols = imap imaps pop3 pop3s`
   - `auth_userdb` `passwd` — 虽然可以使用不同的身份验证方法，默认是简单地从 `/etc/passwd` 文件中验证用户名和密码。使用的身份验证方法是 `pam`，密码以明文格式使用。可以使用 `/usr/share/doc/dovecot*/auth.txt` 获取身份验证类型的信息。

2. 输入以下命令（作为 root 用户）开启 `dovecot` 服务：
   ```
   # chkconfig dovecot on
   ```

3. 通过如下方式启动 `dovecot` 服务来启动 POP3 服务：
   ```
   # /etc/init.d/dovecot start
   ```

您的邮件服务器上拥有用户账户的所有用户默认都已配置为接收邮件（accept-mail）。例如，如果有一封给 `jsmith` 的邮件发送到 `mail.handsonhistory.com`，该消息将被复制到服务器上的 `/var/spool/mail/jsmith` 文件。继续该示例，在 `jsmith` 的电脑上，他可以将其邮件读取器设为：

- **邮件服务器**: `mail.handsonhistory.com`
- **用户名**: `jsmith`
- **协议**: `POP3`

## 第 19 章：设置邮件服务器

邮件读取器配置完成后，当 `jsmith` 点击其邮件读取器上的“发送并接收”（Send & Receive）时，`/var/spool/mail/jsmith` 中的所有电子邮件消息将下载到他的本地邮件读取器中。随后消息将从服务器上删除。

> 注意：如果您的用户都无法从邮件服务器下载消息，请检查防火墙 (`iptables`) 是否配置为允许访问 POP 服务。默认情况下，`pop3` 监听 110 端口，支持 SSL 的 `pop3` 监听 995 端口。

## 使用 SquirrelMail 从浏览器获取邮件

一旦您的邮件服务器启动并运行，您就可以配置 SquirrelMail，允许邮件服务器用户通过 Web 浏览器获取邮件。要使用 SquirrelMail，您必须从 Fedora Core 4 安装 DVD 或随附的第二张 CD 中安装 `squirrelmail` 包。此外，为了使用 SquirrelMail，您需要配置好邮件服务器、IMAP 服务器和 Web 服务器，以及通过 SquirrelMail 读取邮件的用户账户。

SquirrelMail 拥有一个非常直观的基于菜单的管理界面。该界面包含了多种可以添加到 SquirrelMail 的插件，用于使用诸如拼写检查、日历、更改密码和从 POP 服务器获取邮件等功能。您也可以从 `squirrelmail.org` 获取更多插件。

要配置 SquirrelMail，请在终端窗口中作为 root 用户输入以下命令：

```
# /usr/share/squirrelmail/config/conf.pl
```

在配置时，您可能想要考虑调优的功能：组织偏好（例如放入 SquirrelMail 界面的组织名称和标志）、主题（有二十多个主题可用）以及插件（只需检查是否有任何感兴趣的插件可以安装即可）。

此外，默认情况下，邮件只能通过本地主机的上的浏览器访问，因此您可能想要更改“服务器设置”（Server Settings）。例如，将域名更改为允许用户访问邮件的域名。

要让用户使用 squirrelmail 获取邮件，他仅需在其 Web 浏览器的位置框中输入以下地址（如果您在 localhost 之外运行，请将 server 替换为 localhost 或计算机名称）：

```
http://server/webmail
```
