
`hide_ids` 设置为 `YES` 会在目录列表中将所有用户和组显示为 ftp。`NO` 则列出真实所有者。

默认值：`NO`

# `setprotitle_enable`

`NO` 会使 `ps` 命令将运行 vsftpd 的进程显示为 vsftpd。`YES` 会使 `ps` 命令显示 vsftpd 当前正在执行的操作（上传等）。将此参数设置为 `NO` 以获得更安全的系统。

默认值：`NO`

# `text_userdb_names`

`NO` 通过在目录列表中显示数字型的 UIDs 和 GIDs 来提高性能。`YES` 显示名称。

默认值：`NO`

# `use_localtime`

`NO` 会使 `ls`、`mls` 和 `modtime` FTP 命令显示 UTC 时间（第 1067 页）。`YES` 会使这些命令显示本地时间。

默认值：`NO`

# `ls_recurse_enable`

`YES` 允许执行 `ls -R` 命令。将此参数设置为 `YES` 可能会带来安全风险，因为在大型目录层次结构的顶部执行 `ls -R` 命令可能会消耗大量的系统资源。

默认值：`NO`

# 日志（Logs）

默认情况下日志是关闭的。然而，Ubuntu Linux 分带的 `vsftpd.conf` 文件开启了它。本节描述了控制日志细节和位置的参数。

# `log_ftp_protocol`

`YES` 记录 FTP 请求和响应，前提是 `xferlog_std_format` 被设置为 `NO`。

默认值：`NO`

# `xferlog_enable`

`YES` 在 `/var/log/vsftpd.log`（或由 `xferlog.file` 指定的其他文件）中维护传输日志。`NO` 不创建日志。

默认值：`NO`

Ubuntu: `YES`

# `xferlog_std_format`

只要显式设置了 `xferlog_file`，`YES` 会导致传输日志（不包括连接）以标准 xferlog 格式（如 wu-ftpd 使用的格式）写入。如果 `xferlog_std_format` 设置为 `YES` 但未显式设置 `xferlog_file`，则关闭日志。默认的 vsftpd 日志格式比 xferlog 格式更易读，但无法由生成 xferlog 文件摘要的程序处理。可以在网上搜索 xferlog 获取有关此命令的更多信息。

默认值：`NO`

# `xferlog_file`

参见 `xferlog_enable` 和 `xferlog_std_format`。

默认值：`/var/log/xferlog`

# 连接参数（CONNECTION PARAMETERS）

你可以允许客户端建立被动和/主动连接（第 730 页）。设置超时和最大传输速率可以提高服务器的安全性能。本节描述了控制客户端建立的连接类型、vsftpd 在建立连接时等待的时间以及不同类型用户连接速度的参数。

# 被动模式（PASV）连接

`pasv_enable` 防止使用 PASV 连接。

默认值：`YES`

`pasv_promiscuous` 导致 PASV 执行安全检查，确保数据连接和控制连接源自同一个 IP 地址。`YES` 禁用此检查；对于安全系统不建议这样做。

默认值：`NO`

`pasv_max_port` vsftpd 为 PASV 数据连接分配的最高端口号；用于设置防火墙有用。

默认值：`0`（使用任何端口）

`pasv_min_port` vsftpd 为 PASV 数据连接分配的最低端口号；用于设置防火墙有用。

默认值：`0`（使用任何端口）

`pasv_address` 指定除客户端联系服务器外使用的 IP 地址。

默认值：`none`；地址为客户端使用的地址

# 主动模式（PORT）连接

`port_enable` 防止使用 PORT 连接。

默认值：`YES`

`port_promiscuous` 导致 PORT 执行安全检查，确保输出数据仅连接到客户端。`YES` 禁用此检查；对于安全系统不建议这样做。

默认值：`NO`

`connect_from_port_20` 根据某些客户端的要求，在服务器上为 PORT 连接指定端口 20（ftp-data，一个特权端口）。`NO` 允许 vsftpd 以更少的端口运行。

默认值：`NO`

Ubuntu: `YES`

`ftp_data_port` 根据某些客户端的要求，在服务器上为 PORT 连接指定端口 20（ftp-data，一个特权端口）。`NO` 允许 vsftpd 以更少的端口运行。

# 超时（TIMEOUTS）

`accept_timeout` 服务器等待的秒数。

默认值：`60`

`connect_timeout` 服务器等待连接的秒数。

默认值：`60`

`data_connection_timeout` 服务器等待数据连接的秒数。

默认值：`300`

`idle_timeout` 服务器等待空闲的秒数。

默认值：`300`

`local_max_rate` 对于本地用户的每秒传输速率。`0` 表示不限制。

默认值：`0`

`anon_max_rate` 对于匿名用户的每秒传输速率。`0` 表示不限制。

默认值：`0`

`one_process_model` `YES` 每个连接建立一个进程，提高性能。`NO` 允许多个。

默认值：`NO`

# 杂项（MISCELLANEOUS）

本节描述其他地方未讨论的参数。

`pam_service_name` vsftpd 使用的 PAM 服务名称。

默认值：`vsftpd`

`rsa_cert_file` 指定加密连接证书存放。

默认值：`/usr/share/ssl/certs`

`rsa_private_key_file` 指定加密连接的 RSA 私钥。

默认值：`none`

`tcp_wrappers` 如果 vsftpd 编译时支持，`YES` 允许使用 tcp_wrappers。

默认值：`NO`

`user_config_dir` 指定包含用户名的目录。这些文件每个模仿 `vsftpd.conf`，包含按用户覆盖默认参数和 `vsftpd.conf` 参数的设置。例如，`user_config_dir` 设置为 `/etc/vsftpd/user_conf`。假设默认配置文件 `/etc/vsftpd.conf` 设置了 `idle_timeout=300`，而单独配置文件 `/etc/vsftpd/user_conf/sam` 设置了 `idle_timeout=1200`。那么除了 Sam 外的所有将在 300 秒后超时。

# 文件（FILES）

除了 `/etc/vsftpd.conf` 之外，以下文件控制 vsftpd 的功能。`user_config_dir` 指向的目录未包含列表中。

`/etc/ftusers` 每行列出一个不允许登录 FTP 服务器的用户，无论 `user_enable`（第 743 页）如何设置，也无论 `user_list` 文件中的用户。默认列出 root、bin、daemon 等。

`/etc/vsftpd.user_list` 列出允许登录服务器的用户，或列出不允许登录服务器的用户。必须将 `user_enable`（第 743 页）选项设置为 `YES`，vsftpd 才会检查文件中的用户列表。将 `userlist_enable` 设置为 `YES` 并 `userlist_deny`（第 744 页）设置为 `YES`（或不设置）防止用户登录服务器。将 `userlist_enable` 设置为 `YES` 并 `userlist_deny` 设置为 `NO` 则允许列出的用户登录服务器。

`/etc/vsftpd.chroot_list` 根据 `chroot_list_enable`（第 745 页）和 `chroot_local_user`（第 745 页）的设置，列出强制进入其家目录 chroot 狱的用户，或列出不放入 chroot 狱的用户。

`/var/log/vsftpd.log` 日志文件。更多信息请参见第 749 页的“日志（Logs）”。

# 练习题 753

## 章节摘要

文件传输协议（FTP）是一种通过网络从另一个系统下载文件或向其上传文件的协议。FTP 既是指客户端/服务器协议（FTP）名称，也是指调用该协议的客户端工具（`ftp`）名称。由于 FTP 不是一种安全协议，它应该仅用于下载公共信息。你可以在 chroot 监狱（chroot jail）的限制环境中运行 vsftp FTP 服务器，从而显著降低恶意用户破坏系统的可能性。

许多服务器和客户端都实现了 FTP 协议。`ftp` 工具是原始的客户端实现；`sftp` 和 `lftp` 是使用 OpenSSH 功能加密连接的安全实现。尽管它们并不直接理解 FTP 协议，但它们将 `ftp` 命令映射到 OpenSSH 命令。vsftp 进程是一个安全的 FTP 服务器；它比其他 FTP 服务器更好地保护服务器免受恶意用户的攻击。

公共服务器允许以匿名或 ftp 用户身份登录。按照惯例当你作为匿名用户登录时，提供你的电子邮件地址作为密码。公共服务器的 `pub` 目录下经常会有有趣的文件。

FTP 提供两种传输模式：二进制和 ASCII。使用二进制模式传输所有类型的文件（包括 ASCII 文件）是安全的。如果你使用 ASCII 模式传输二进制文件，传输将失败。

## 练习题

1. 当你从 Linux 服务器以 ASCII 模式将 ASCII 文件下载到 Windows 机器时，FTP 对文件做了哪些更改？下载到 Mac 时又会有哪些更改？

2. 如果以 ASCII 模式传输可执行程序文件，会发生什么？

3. 在什么情况下 `ftp` 是比 `sftp` 更好的选择？

4. 你如何防止本地用户使用他们的系统用户名和密码登录 vsftppd 服务器？

5. `sftp` 相比 `ftp` 有什么优势？

6. `ftp` 中的 `cd` 和 `cdw` 命令有什么区别？

## 高级练习题

7. 为什么在连接到端口模式（PORT mode）的 FTP 服务器时可能会遇到问题？

8. 为什么在 chroot 监狱中运行 vsftpd 是有利的？

9. 下载文件后，你发现它与提供的 MD5 校验和不匹配。再次下载文件得到的是相同的错误校验和。你哪里做错了？应该如何修复？

10. 你如何配置 vsftpd 通过 xinetd 运行？这种方法的主要优势是什么？

## exim4: 设置邮件服务器、客户端及更多

## 本章内容

- exim4 简介 ........ 756
- 快速上手 1：配置 exim4 使用智能主机（Smarthost） ....... 758
- 快速上手 2：配置 exim4 发送和接收邮件 .... 760
- 配置 exim4 .............. 765
- SpamAssassin ................ 768
- 网页邮箱 ................... 772
- 邮件邮件列表 ................ 775
- 设置 IMAP 或 POP3 服务器 .............. 776
- 身份验证中继 ........ 777

发送和接收邮件需要三部分软件。在每一端都有一个客户端，称为 MUA（邮件用户代理），它是用户与邮件系统之间的桥梁。常见的 MUA 有 mut、Evolution、KMail、Thunderbird 和 Outlook。当你发送邮件时，MUA 将其交给 MTA（邮件传输代理，例如 `exim` 或 `sendmail`），由 MTA 将其传输到 ISP 的 SMTP（简单邮件传输协议）。在目的端，MDA（邮件投递代理，例如 `procmail`）将其放入收件人的邮箱文件中。在 Linux 系统上，接收系统上的 MUA 要么读取邮箱文件，要么从远程 MUA 或 MTA 获取邮件，例如 ISP 的 POP（邮局协议）或 IMAP（互联网消息访问协议）。

大多数 MUA 期望像 `exim` 这样的本地 MTA 来传递发出的邮件。在某些系统上（包括拨号连接互联网的系统），MTA 将邮件发送到 ISP 的邮件服务器。由于大多数 MTA 使用 SMTP 传递邮件，因此它们通常被称为 SMTP 服务器。默认情况下，当你在 Ubuntu 服务器上安装 `exim` 时，`exim4` 使用其内置的 MDA 将邮件投递收件人的邮箱文件中。

## 你不需要设置 exim4 即可发送和接收邮件

大多数 MUA 使用 POP 或 IMAP 从 ISP 服务器接收邮件。这些协议不需要像 `exim4` 这样的 MTA。因此，你不需要安装或配置 `exim4`（或其他 MTA）来接收邮件。虽然你仍然需要 SMTP 来发送邮件，但 SMTP 服务器可以位于远程位置（例如你的 ISP）。因此，你可能也不需要关心它。

## exim4 简介

当后来演变为互联网的网络首次建立时，它连接了少数台计算机，为大量用户服务并运行了几项服务。每台计算机都能够发送和接收邮件，并有一个唯一的主机名，作为邮件的目的地址。

今天，互联网有大量的临时客户端。由于这些客户端没有固定的 IP 地址或主机名，它们无法直接接收邮件。系统上的用户通常在雇主或 ISP 的邮件服务器上维护账户，并使用 POP 或 IMAP 从该账户收集邮件。除非使用你想接收邮件的域名，否则你不需要设置 `exim4` 来接收来自非本地系统的邮件。

智能主机（智能主机）：你可以在客户端系统上设置 `exim4`，使其将发往非本地系统的邮件发送到 SMTP 服务器，由该服务器将邮件中继到目的地。这种服务器被称为智能主机。

你可以在客户端系统上设置 `exim4`，使其将发往非本地系统的邮件发送到 SMTP 服务器，由该服务器将邮件中继到目的地。这种服务器被称为智能主机。

你可以在客户端系统上设置 `exim4`，使其将发往非本地系统的邮件发送到 SMTP 服务器，由该服务器将邮件中继到目的地。这种服务器被称为智能主机。

你可以在客户端系统上设置 `exim4`，使其将发往非本地系统的邮件发送到 SMTP 服务器，由该服务器将邮件中继到目的地。这种服务器被称为智能主机。

本地系统是运行 `exim4` 的系统。本地系统是那些位于局域网内的系统……详见第 776 页。

## 前提条件

- `exim4`（虚拟包）
- `eximon`（可选）；监控 `exim4`
- `mailx`（可选）；安装 `mail`，用于从命令行测试 `exim4`
- `exim4-doc-html`（可选）；`exim4` HTML 文档
- `exim4-doc-info`（可选）；`exim4` info 文档

`exim4` 脚本：当你安装 `exim4` 包时，`dpkg postinst` 脚本会配置 `exim4` 并启动 `exim4`。当你配置 `exim4` 时，调用 `exim4` 脚本进行重启：

```
$ /etc/init.d/exim4 restart
```

在活动服务器上更改 `exim4` 配置后，使用 `reload` 重新加载 `exim4` 配置而不中断 `exim4` 进程。`exim4` 脚本接受几个非标准参数：

```
/etc/init.d/exim4
用法:/etc/init.d/exim4 {start|restart|reload}[status|what|force-stop]
```

`status` 和 `what` 参数显示关于 `exim4` 的信息。`force-stop` 参数立即杀死所有 `exim4` 进程。

## 注意事项

防火墙：SMTP 服务器通常使用 TCP 端口25。如果接收邮件的 SMTP 服务器运行防火墙，你需要开启此端口。使用 `ufw`（第 886 页）设置允许 SMTP 策略。

日志文件：你必须是 `adm` 组成员或拥有 `root` 权限才能查看 `/var/log/exim4` 中的日志文件。

`sendmail`：尽管工作方式与 `sendmail` 不同，Ubuntu 使用 `exim4` 作为 `sendmail` 的替代。`exim4-daemon-light` 包作为 `exim4` 虚拟包的一部分会安装 `/usr/sbin/sendmail`，它是指向 `exim4` 的链接。由于 `exim4` 接受许多 `sendmail` 选项，依赖 `sendmail` 的程序在安装 `exim4` 后可以正常工作。

本地和非本地系统：`exim4` 进程发送并接收邮件。`exim4` 接收的邮件可能源自本地系统或非本地系统。同样，`exim4` 发送的邮件可能目的地是本地系统或非本地系统。`exim4` 进程根据其来源和目的地处理每封邮件。

# 更多信息

- Web `exim4` www.exim.org (包含完整的 `exim4` 规范), www.exim-new-users.co.uk, wiki.debian.org/PkgExim4
- SpamAssassin spamassassin.apache.org, wiki.apache.org/spamass
- 垃圾邮件数据库 razor.sourceforge.net
- Mailman www.list.org
- `procmail` www.procmail.org
- SquirrelMail www.squirrelmail.org
- IMAP www.imap.org
- Dovecot www.dovecot.org
- Postfix www.postfix.org/docs.html (另一种 MTA；第 779 页)
- Qmail www.qmail.org/top.html
- 本地 `exim4` /usr/share/doc/exim4/*
- SpamAssassin /usr/share/doc/spam*
- Dovecot /usr/share/doc/dovecot*
- 手册页 `exim4` `exim4_files` `update-exim4.conf` `update-exim4defaults` `spamass` `spamc` `spamd`

### SpamAssassin

安装 `perl-doc` 软件包并执行以下命令：

```
$ perldoc Mail::SpamAssassin::Conf
```

## 快速上手 1：配置 exim4 使用智能主机 (SMARTHOST)

快速上手用于配置 `exim4` 服务器，该服务器将来自本地系统的邮件发送到本地和非本地目的地，并且不接受非本地系统的邮件。此服务器：

* 接收来自本地系统的电子邮件并投递到本地系统。
* 接收来自本地系统的电子邮件并投递到非本地系统，使用 SMTP 服务器（智能主机）——通常是 ISP——来中继邮件并发送到其目的地。
* 不投递来自非本地系统的电子邮件。通常情况下，您需要使用 POP 或 IMAP 来接收电子邮件。
* 不转发来自非本地系统的电子邮件到其他非本地系统（不中继邮件）。
