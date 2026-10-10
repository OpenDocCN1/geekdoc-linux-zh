
# `chkconfig --list spamassassin`

`spamassassin 0:off 1:off 2:on 3:on 4:on 5:on 6:off`

# `chkconfig spamassassin on`

3. 使用任何文本编辑器创建一个 `/etc/procmailrc` 文件，或者 `procmailrc` 文件可以将 `procmail` 接收的所有邮件消息通过 `spamc`（它是上一步启动的垃圾邮件守护程序的客户端）进行处理：

```
:0fw

| /usr/bin/spamc
```

如果你愿意，可以在 `procmailrc` 文件中进行更多操作以实现基于系统范围的处理。例如，你可以创建一个 `procmailrc` 文件夹，接收垃圾邮件消息并将它们分类到系统级文件夹中，或将其完全删除。同样，你可以创建一个个人的 `$HOME/.procmailrc` 文件来创建个人的 `procmail` 配方。（输入 `man procmailex` 可查看 `procmailrc` 文件中规则的示例）。

4. 检查 `/etc/mail/spamassassin/local.cf` 文件。该文件包含 SpamAssassin 的系统级规则，除非这些规则被用户个人的 `$HOME/.spamassassin/user_prefs.cf` 文件覆盖。以下是 `local.cf` 文件的内容：

```
required_hits 5

report_safe 0

rewrite_header Subject [SPAM]
```

SpamAssassin 是一个评分系统，用于猜测特定消息是否为垃圾邮件。`required_hits` 行显示需要 5 分才能将消息标记为垃圾邮件。对于公共邮件服务器，你应该应该设置更高的分值（例如 8 或 10）。设置 `rewrite_header [SPAM]` 会让 SpamAssassin 在其发现的垃圾邮件的主题行中添加该文本。（输入 `man Mail::SpamAssassin::Conf` 查看你在 `local.cf` 中使用的其他设置）。

由于有时会发生误报，如果你需要进行系统级过滤，可能会阻止用户看到某些电子邮件。为了避免这种情况，这里显示的方法让用户自行决定如何处理标记为垃圾邮件的电子邮件。用户甚至可以调整他们认为消息被认为是垃圾邮件的阈值。

接下来，你应该让该邮件服务器的用户在他们的主目录中设置自己的偏好。偏好设置在每个用户的 `$HOME/.spamassassin/user_prefs.cf` 文件中，有助于告诉 SpamAssassin 针对该用户的电子邮件如何表现。以下是用户可能希望在该文件中包含的行示例：

```
required_score 3

whitelist_from jsmith@example.com bjones@example.net

blacklist_from *.example.org
```

`required_score` 行（默认设置为 5，但此处设置为 3）设置了将消息标记为垃圾邮件所需的评分。

设置 `rewrite_header [SPAM]` 会让 SpamAssassin 在其发现的垃圾邮件的主题行中添加该文本。（输入 `man Mail::SpamAssassin::Conf` 查看你在 `local.cf` 中使用的其他设置）。

由于有时会发生误报，如果你需要进行系统级过滤，可能会阻止用户看到某些电子邮件。为了避免这种情况，这里显示的方法让用户自行决定如何处理标记为垃圾邮件的电子邮件。用户甚至可以调整他们认为消息被认为是垃圾邮件的阈值。

接下来，你应该让该邮件服务器的用户在他们的主目录中设置自己的偏好。偏好设置在每个用户的 `$HOME/.spamassassin/user_prefs.cf` 文件中，有助于告诉 SpamAssassin 针对该用户的电子邮件如何表现。

```
required_score 3
whitelist_from jsmith@example.com bjones@example.net
blacklist_from *.example.org
```

`required_score` 行（默认设置为 5，但此处设置为 3）设置了将消息标记为垃圾邮件所需的评分。

## 第 19 章：设置邮件服务器 821

如果你更倾向于在自己的台式电脑上舒适地收发电子邮件，你可以设置邮局协议（POP3）或互联网消息访问协议（IMAPv4）。

POP3 和 IMAPv4 服务器会在网络上监听对用户电子邮件的请求，并将信箱的全部内容下载到用户的邮件阅读器中（使用 POP3），或者让用户在消息保留在服务器上管理消息（使用 IMAPv4）。

通常，你的邮件服务器将配置为使用 POP3 或 IMAPv4 为你的用户提供邮件消息（尽管在同一台机器上运行这两者也是可能的）。

下一节将解释如何设置 IMAPv4 或 POP3 服务以允许访问电子邮件账户。

**提示：** 有时，你可能想在不是常用电脑的电脑上检查电子邮件，但之后可以保存消息。在这种情况下，邮件阅读器允许你选择一种设置，即可以复制电子邮件消息而不从你的 POP3 服务器中删除它们。这样，当你回到自己的常用电脑时，就可以再次复制这些消息。IMAPv4 则避免了这种情况，因为它始终将邮件消息保留在服务器上，并允许用户在服务器上创建和处理额外的文件夹。

## 使用 dovecot 配置 IMAPv4 和 POP3

当用户被添加到 Fedora 时，在 `/var/spool/mail/` 目录下会以用户名命名配置一个信箱（例如 `/var/spool/mail/chris`）。默认情况下，它是传统的 mbox 格式，所有消息和附件都存储在一个文件中。通过在你的邮件服务器上配置 POP3 服务，用户将能够从其他机器上的邮件客户端下载他们的电子邮件消息。通过配置 IMAPv4，用户可以直接在服务器上处理消息和文件夹。

以下步骤描述了如何使用 `dovecot` 在 Fedora 中配置 IMAPv4 或 POP3 服务。

- 1. 检查 `/etc/dovecot.conf` 文件中的值。例如，你可以尝试在不更改此文件任何内容的情况下运行 `dovecot`。在本例中，已启用 POP3 协议，从标准的 `/etc/passwd` 文件中启用了明文密码，并使用 PAM 进行身份验证。阅读文件中的注释以查看是否有你想要更改的设置。

- 2. 输入以下内容（作为 root 用户）开启 `dovecot` 服务：
```bash
# chkconfig dovecot
```
（如果未安装 `dovecot`，请输入 `yum install dovecot` 安装它。）

- 3. 通过立即启动 `dovecot` 服务来启动 POP3 服务：
```bash
# /etc/init.d/dovecot start
```
