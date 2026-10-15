
`use_localtime` `NO` 导致 `ls`、`mls` 和 `modtime` FTP 命令显示 UTC（第 1195 页）。

`YES` 导致 `ls`、`mls` 和 `modtime` FTP 命令显示本地时间。

`ls_enable` `YES` 允许 `ls` 命令列出子目录。`NO` 禁用它。

默认：`NO`

`ls_recursive` `YES` 允许 `ls` 命令递归地列出子目录。`NO` 禁用它。

默认：`NO`

# 日志

默认关闭日志记录。要启用日志，请设置 `log_enable=YES`。本节描述了控制日志细节的参数。

`log_enable` `YES` 启用日志。`NO` 禁用它。

默认：`NO`

`log_ftp_event` `YES` 启用 FTP 事件日志。`NO` 禁用它。

默认：`NO`

`log_verbosity_level` 设置日志的详细程度。`0` 是最小的，`1` 是中等的，`2` 是详细的，`3` 是冗长的。

默认：`1`

`log_filepath` 指定日志文件的存储路径。

默认：`/var/log/vsftpd.log`

# 设置 FTP 服务器 (vsftpd)

## 连接参数

本节描述了控制如何建立连接的参数。

`pasv_address` 指定一个与服务器用于被动模式的地址不同的 IP 地址。

默认：`none`

## 被动 (PASV) 连接

`pasv_enable` `NO` 防止使用被动模式。

默认：`YES`

`pasv_promisous` `NO` 导致被动模式执行安全检查，确保数据连接仅来自客户端。`YES` 禁用此检查。

默认：`NO`

`pasv_max_port` `vsftpd` 为被动模式分配的最高端口号。

默认：`50000`

`pasv_min_port` `vsftpd` 为被动模式分配的最低端口号。

默认：`40000`

## 主动 (PORT) 连接

`port_enable` `NO` 防止使用主动模式。

默认：`YES`

`port_promisous` `NO` 导致主动模式执行安全检查，确保数据连接仅来自客户端 IP。`YES` 禁用此检查。

默认：`NO`

`connect_from_port_20` 当 `connect_from_port_20` 设置为 `NO` 时，指定 `vsftpd` 用于 `PORT` 连接的端口。

默认：`20`

# 第 724 页 第 19 章 FTP：跨网络传输文件

`accept_timeout` 服务器等待客户端建立被动数据连接的秒数。

默认：`60`

`connect_timeout` 服务器等待客户端响应 `PORT` 数据连接的秒数。

默认：`60`

`data_connection_timeout` 服务器等待阻塞的数据传输恢复并断开的秒数。

默认：`300`

`idle_session_timeout` 服务器在断开连接前等待 FTP 命令的秒数。

默认：`300`

`local_max_rate` 对于用户，每秒字节的最大传输速率。零（`0`）表示无限制。

默认：`0`

`anon_max_rate` 对于匿名用户，每秒字节的最大传输速率。零（`0`）表示无限制。

默认：`0`

`one_process_model` 为每个连接建立一个进程，这提高了性能但降低了安全性。`NO` 允许每个连接多个进程。为了更安全的系统，请设置为 `NO`。

默认：`NO`

## 其他

本节描述了在其他地方未讨论的参数。

`pam_service_name` `vsftpd` 使用的 PAM 服务名称。

默认：`ftp`

Fedora/RHEL: `vsftpd`

`rsa_cert_file` 指定 SSL加密连接的 RSA 证书存放位置。

默认：`/usr/share/ssl/certs/vsftpd.pem` own

### rsa_private_file

指定保留 SSL 加密连接的 RSA 密钥。

默认：`none`

如果 `vsftpd` 编译时支持 `tcp_wrappers`，设置 `tcp_wrappers` `YES` 会导致传入连接使用 `tcp_wrappers`（第 484 页）。当 `tcp_wrappers` 设置环境变量 `VSFTPD_LOAD_CONF` 时，`vsftpd` 会加载由该变量指定的配置文件，允许按 IP 进行配置。

默认：`NO`

Fedora/RHEL: `YES`

`user_config_dir` 指定一个包含本地用户文件的目录。这些文件每一个都模拟 `vsftpd.conf`，包含允许以每个用户为基础覆盖默认参数以及 `vsftpd.conf` 中指定参数的参数。例如，将 `user_config_dir` 设置为 `/etc/vsftpd/user_conf.dir`。进一步假设默认配置文件 `/etc/vsftpd/vsftpd.conf` 设置了 `idles_timeout=300`，而 Sam 的个人配置文件 `/etc/vsftpd/user_conf/sam` 设置了 `idles_timeout=1200`。那么，除 Sam 之外的所有用户会话将在闲置 300 秒后超时。Sam 的会话将在 1,200 秒后超时。

默认：`none`

### 其他配置文件

除了 `/etc/vsftpd/vsftpd.conf` 之外，以下文件控制 `vsftpd` 的运行。`user_config_dir` 指向的目录层次未包含在此列表中，因为它没有默认名称。

`/etc/vsftpd/ftpusers`

每行列出永远不允许在 FTP 服务器上登录的用户，无论 `userlist_enable` 如何设置，也与 `user_list` 中列出的用户无关。默认文件列出了 root、bin、daemon 等其他用户。

`/etc/vsftpd/user_list`

列出可以在服务器上登录的用户，或者列出唯一不允许在服务器上登录的用户。必须将 `userlist_enable`（第 716 页）参数设置为 `YES`，`vsftpd` 才会检查此文件中的用户列表。将 `userlist_enable` 设置为 `YES` 并将 `userlist_deny`（第 716 页）设置为 `YES`（或不设置它）将阻止用户登录服务器。将 `userlist_enable` 设置为 `YES` 并将 `userlist_deny` 设置为 `NO` 则只允许列表中的用户登录。

`/etc/vsftpd/chroot_list`

根据 `chroot_list_enable`（第 718 页）和 `chroot_local_user`（第 718 页）的设置，列出被强制在其主目录进入 chroot 监狱的用户，或列出未被放入 chroot 监狱的用户。

`/var/log/xferlog`

日志文件。更多信息请参见第 722 页的“日志”。

### 章节总结

文件传输协议（FTP）是一种通过网络向另一个系统下载文件和上传文件的协议。FTP 既是客户端/服务器协议（FTP）也是调用该协议的客户端程序（`ftp`）的名称。由于 FTP 不是一种安全协议，它应该只用于下载公共信息。你可以在 chroot 监狱的受限环境中运行 `vsftpd` FTP 服务器，这可以显著降低恶意用户破坏系统的可能性。

许多服务器和客户端实现了 FTP 协议。`ftp` 实用是原始的客户端实现；`sftp` 和 `ftp` 是使用 OpenSSH 功能加密连接的安全实现。尽管它们不理解 FTP 协议，但它们可以将命令映射到 OpenSSH 命令。`vsftpd` 守护进程是一个安全的 FTP 服务器；它比其他服务器更好地保护服务器免受恶意用户的攻击。

公共 FTP 服务器允许你以匿名或 `ftp` 身份登录。按照惯，当你以匿名用户登录时，提供你的电子邮件地址作为密码。公共服务器的 `pub` 目录下经常会有有趣的文件。

FTP 提供了两种文件传输模式：二进制（binary）和 ASCII。使用二进制模式传输所有类型的文件（包括 ASCII 文件）是安全的。如果你使用 ASCII 模式传输二进制文件，传输将失败。

### 练习题

- 1. 当你从 Linux 服务器以 ASCII 模式下载到 Windows 机器时，FTP 对 ASCII 文件做了哪些更改？下载到 Mac 时会有哪些更改？
- 2. 如果用 ASCII 传输传输可执行程序文件会发生什么？
- 3. `ftp` 会比 `sftp` 更好的选择吗？
- 4. 你如何防止本地用户使用其系统用户名和密码登录 `vsftpd` 服务器？
- 5. `sftp` 相比 `ftp` 有什么优势？
- 6. `ftp` 中 `cd` 和 `get` 有什么区别？

### 进阶练习题

- 7. 为什么在 `PORT` 模式下连接 FTP 服务器可能会遇到问题？
- 8. 为什么在 chroot 监狱中运行 `vsftpd` 有利？
- 9. 下载文件后，发现它与提供的 MD5 校验和不匹配。再次下载文件得到相同的错误校验和。你做错了什么，该如何修复？
- 10. 你将如何配置 `vsftpd` 通过 `xinetd` 运行，这种方法的主要优势是什么？

# 20

`sendmail`: 建立邮件服务器、客户端及更多

## 本章内容

- `sendmail` 简介 ............................................ 730
- 快速启动 I：在客户端上配置 `sendmail` ...................... . . . . . 733
