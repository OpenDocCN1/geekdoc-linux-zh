
作为一种协议，`SMTP`定义了电子邮件的传输和存储方式。它是`TCP/IP`协议栈应用层的一部分，提供了一套所有基于电子邮件的程序同意遵循的规则。简单来说：没有`SMTP`，就没有电子邮件。

为了理解`SMTP`，了解电子邮件的一些主要组件会有帮助：邮件用户代理 (`MUA`)、邮件提交代理 (`MSA`)、邮件传输代理 (`MTA`) 和邮件投递代理 (`MDA`)。

- `MUA`——邮件用户代理（`Mail User Agent`）是用户用于创建电子邮件消息的客户端程序。Linux 上有多种 `MUA` 可用，包括命令行工具（如 `mutt`）、基于 GUI 的程序（如 `Thunderbird`）和基于 Web 的界面（如 `SquirrelMail`）。`MUA` 通常还负责连接邮件池。配置 `MUA` 不是 `LPIC-2` 考试目标；但是，`MUA` 是电子邮件过程的一部分，你应该在你的组织中制定有关正确使用公司 `MUA` 的策略。
- `MSA`——邮件提交代理（`Mail Submission Agent`）接受来自 `MUA` 的电子邮件消息并与 `MTA` 通信，开始将消息传输给预定接收者的过程。在大多数情况下，担任 `MSA` 角色的软件程序同时也担任 `MTA` 角色。
- `MTA`——邮件传输代理（`Mail Transfer Agent`）负责从 `MUA` 接收电子邮件消息并将其发送到正确的接收邮件服务器（另一个 `MTA`）。通信可能不是直接的，因为消息在到达最终目的地之前可能需要通过多个 `MTA`。Linux 中的 `MTA` 服务器示例包括 `Postfix`、`sendmail` 和 `exim`。
- `MDA`——邮件投递代理（`Mail Delivery Agent`）从 `MTA` 获取消息并将其发送到本地邮件队列。通常，`MTA` 服务器也可以充当 `MDA`；但是，也有专门设计用作 `MDA` 的程序，例如 `procmail` 和 `maildrop`。`MDA` 的优势在于它可以配置为在发送消息到队列之前对其进行操作。例如，可以将 `MDA` 用作过滤器，可能用来拦截垃圾邮件。`procmail` 将在第 33 章“管理本地电子邮件投递”中介绍。
- 邮局协议 (`POP`) 和互联网邮件访问协议 (`IMAP`)——这些协议被 `MUA` 用于检索电子邮件。第 34 章“管理远程电子邮件投递”涵盖了这些协议以及 `Dovecot` `POP/IMAP` 服务器。

32-1 展示了传输电子邮件消息过程的视觉示例。在图中，`user1` 想向 `user2` 发送一封邮件。`user1` 在 `MUA` 上操作，编写并发送了消息。消息被发送到公司的 `MTA`（尽管这些可能是同一个系统）。灰色框表示在 `user1` 的 `MTA` 和 `user2` 的 `MTA` 之间多个可能的 `MTA`。

最终，消息到达 `user2` 所在域的 `MTA`。从那里，它可以直接发送到邮件队列（通常是邮件服务器上 `/var/spool` 中的一个文件），但可能先发送到 `MDA` 进行过滤（为了 `user1` 考虑，希望它能通过垃圾过滤器！）。当 `user2` 想读取新邮件时，`MUA` 连接到 `POP` 或 `IMAP` 服务器以下载消息。

# 第 32 章：使用电子邮件 (Using E-mail)

**图 32-1** 电子邮件消息的传输

> **注意：** 请记住发送邮件的过程还有另一个部分。发送 `MTA` 必须能够接收消息。这是由 `DNS` 记录处理的。

# 配置 Postfix (Configuring Postfix)

多年来 `sendmail` 服务器一直是 Unix 和 Linux 的标准。许多人认为现在的标准是 `Postfix`，而 `sendmail` 与旧系统有关。无论哪种服务器类型主宰 `SMTP` 世界，在准备 `LPIC-2` 时，你应该意识到考试重点是 `Postfix`，你只需要对 `sendmail` 和 `exim` 有了解即可。

注意：你对 `Postfix` 的更改将在 `/etc` 目录下的文件中进行，你应该意识到 `Postfix` 将信息（如入站邮件）存储在 `/var/spool` 目录。电子邮件消息在被处理程序（如 `qmgr` 工具）处理之前最初存储在用户的邮件队列中 (`/var/spool/mail/username`)。

# Postfix配置文件 (Postfix Configuration File)

`Postfix` 的主配置文件是 `/etc/postfix/main.cf`。格式类似于环境变量：

```
setting = value
```

你可以手动修改此文件，也可以使用 `postconf` 命令进行更改。`postconf` 命令的优势在于提供一些语法检查，降低了出错的概率。它还可以用于显示 `Postfix` 的当前配置。通常默认会显示所有设置：

```
[root@localhost] postconf -wc -1
816
[root@localhost] postconf | head -5
bounce_notice_recipient = postmaster
access_map_defer_code = 450
access_map_reject_code = 554
address_verify_cache_cleanup_interval = 12h
address_verify_default_transport = $default_transport
```

如所示，`postconf` 命令默认显示所有配置设置。这包含了所有的默认值，而不仅仅是配置文件中指定的那些。如果你只想查看配置文件中自定义设置，请对 `postconf` 命令使用 `-n` 选项，如示例 32-1 所示。

# 示例 32-1 postconf -n 命令

```
[root@localhost] postconf -n
alias_database = hash;/etc/aliases
alias_maps = hash;/etc/aliases
command_directory = /usr/sbin
config_directory = /etc/postfix
daemon_directory = /usr/libexec/postfix
data_directory = /var/lib/postfix
debug_peer_level = 2
```

```bash
debugger_command = PATH=/bin:/usr:/usr/local/bin:/usr/X11R6/bin dd $daemon
directory=$process_name $process_id & sleep 5
html_directory = no
inet_interfaces = localhost
inet_protocols = all
mail_owner = postfix
mailq_path = /usr/bin/mailq.postfix
manpage_directory = /usr/share/man
mydestination = $hostname, localhost.$mydomain
newaliases_path = /usr/bin/newaliases.postfix
queue_directory = /var/spool/postfix
readme_directory = /usr/share/doc/postfix-2.10.1/README_FILES
sample_directory = /usr/share/doc/postfix-2.10.1/samples
sendmail_path = /usr/bin/sendmail.postfix
setgid_group = postdrop
unknown_local_recipient_reject_code = 550
```

你可以通过提供设置名称作为参数来定义一个特定的设置：

```bash
[root@localhost ~]# postconf inet_interfaces
inet_interfaces = localhost
```

要进行更改，请使用 `-e` 选项并采用以下语法：

```bash
[root@localhost ~]# postconf -e inet_interfaces
[root@localhost ~]# postconf inet_interfaces
inet_interfaces = all
```

尽管并非总是如此，但 `postconf` 命令会进行一些错误检查。例如，它知道 `main.cf` 文件中允许哪些合法设置：

```bash
[root@localhost ~]# postconf ine_interfaces
postconf: warning: ine_interfaces: unknown parameter
```

## 重要 Postfix 设置

如你通过运行 `postconf` 命令所示，`Postfix` 服务器有数百个可能的设置：

```bash
[root@localhost ~]# postconf wc -l
```

如果你将管理公司范围内的 `Postfix` 服务器，你肯定想探索这些设置中的许多。但对于基础 `Postfix` 配置，表 32-2 中描述的设置足够了。

## 表 32-2 Essential Postfix 设置

| 设置 | 描述 |
| :--- | :--- |
