
# vsftpd 配置选项

- `anon_upload_enable=YES` 表示匿名 FTP 用户可以上传文件。此选项仅在 `write_enable` 已设置为 `YES` 且目录对所有人具有写权限时才生效。请记住：允许匿名用户在你的系统上写入可能非常危险，因为用户可能会填满磁盘或将你的磁盘用作他们的个人存储。

- `anonymous_enable=YES` 启用匿名 FTP。（用户可以使用用户名 `anonymous` 登录，并将他们的电子邮件地址作为密码提供。）如果你不想要匿名 FTP，请注释掉这一行。

- `ascii_download_enable=YES` 启用 ASCII 模式下的文件下载。不幸的是，恶意远程用户可以发出带有巨大文件名称的 `SIZE` 命令，实际上导致 FTP 服务器浪费大量资源打开该文件并确定其大小。这种技术用于拒绝服务攻击。（有关拒绝服务 `DoS` 攻击的更多信息，请参阅第六卷第一章。）

- `ascii_upload_enable=YES` 启用 ASCII 模式下的文件上传（适用于文本文件）。

- `async_abor_enable=YES` 使 `vsftpd` 能够识别在任何时间到达的 `ABOR`（`abort`）请求。你可能需要启用它，以允许较旧的 FTP 客户端与 `vsftpd` 配合工作。

- `banned_email_file=/etc/vsftpd.banned_emails` 指定包含被禁止电子邮件地址列表的文件（仅当 `deny_email_enable` 设置为 `YES` 时使用）。

- `chown_uploads=YES` 使上传的匿名文件归属于由 `chown_username` 选项指定的另一个用户。除非绝对必要，否则不要启用此选项——并且不要将 `root` 指定为 `chown_username`。（那将是一场灾难。）如果由特定用户名运行的进程使用上传的文件，则你可能需要启用此选项，这意味着无论谁上传文件，所有者都必须更改为该进程预期的用户名。

- `chown_username=name` 指定拥有由匿名 FTP 用户上传文件的所有者用户名。

- `chroot_list_enable=YES` 使 `vsftpd` 在 FTP 服务登录时，将除 `chroot_list_file` 指定的列表中的用户以外的所有用户限制在其主目录中。此选项防止这些用户访问主目录之外的任何文件。默认情况下，`vsftpd` 在 `/etc/vsftpd.chroot_list` 文件中查找 chroot 用户列表，但你可以通过 `chroot_list_file` 选项指定文件名来覆盖此设置。

- `chroot_list_file=/etc/vsftpd.chroot_list` 是用户列表，根据 `chroot_local_user` 的设置，这些用户要么被限制在其主目录中，要么不被限制。

- `connect_from_port_20=YES` 使 `vsftpd` 确保数据传输通过 20 端口（FTP 数据端口）进行。

- `data_connection_timeout=120` 是非活动数据连接超时前的秒数。

- `deny_email_enable=YES` 使 `vsftpd` 检查被禁止的电子邮件地址列表，并拒绝任何试图使用被禁止的电子邮件地址作为密码匿名登录的人访问。默认情况下，`vsftpd` 期望被禁止的电子邮件地址位于 `/etc/vsftpd.banned_emails` 文件中，但你可以通过 `banned_email_file` 选项指定其他文件名。

- `dirmessage_enable=YES` 使 `vsftpd` 在 FTP 用户切换到特定目录时显示消息。

- `ftpd_banner=Welcome to my FTP service` 设置 `vsftpd` 在用户登录时显示的横幅。你可以将消息更改为任何你想要的内容。

- `idle_session_timeout=600` 是非活动会话（指某人连接但什么也不做的情况）超时并导致 `vsftpd` 注销用户的秒数。

- `listen=YES` 使 `vsftpd` 监听连接请求，并因此以独立模式运行。如果你希望 `vsftpd` 在 `xinetd` 下运行，请将此选项设置为 `NO`。

- `local_enable=YES` 使 `vsftpd` 允许本地用户访问 FTP。

- `local_umask=022` 意味着 FTP 写入的任何文件权限均为 644（对所有人有读取权限，但仅对所有者有写入权限）。你可以将其设置为任何你想要的文件权限掩码设置。例如，如果你希望除了所有者外任何人都没有权限，请将此选项更改为 `077`。（要了解有关文件权限掩码的更多信息，请查阅第六卷第二章。）

- `ls_recurse_enable=YES` 允许 FTP 用户通过使用 `ls -R` 命令递归遍历目录。

- `nopriv_user=ftp` 标识 FTP 服务器可以使用的非特权用户账户。

- `pam_service_name=vsftpd` 是当 `vsftpd` 必须对用户进行身份验证时使用的可插拔身份验证模块（PAM）配置文件的名称。默认情况下，PAM 配置文件位于 `/etc/pam.d` 目录中。这意味着 `vsftpd` 的 PAM 配置文件是 `/etc/pam.d/vsftpd`。

- `tcp_wrappers=YES` 启用通过 TCP 包装器的访问控制支持，该包装器查阅 `/etc/hosts.allow` 和 `/etc/hosts.deny` 文件。（有关 TCP 包装器的更多信息，请参阅第六卷第三章。）

- `userlist_deny=YES` 在 `userlist_enable` 设置为 `YES` 的情况下，使 `vsftpd` 拒绝访问列在 `/etc/vsftpd_user_list` 文件中的用户。这些用户甚至不会被提示输入密码。另一方面，如果你将 `userlist_deny=NO` 设置为，除非用户列在 `/etc/vsftpd_user_list` 文件中，否则他们将无法访问。

- `userlist_enable=YES` 使 `vsftpd` 从 `/etc/vsftpd_user_list` 文件读取用户列表，并拒绝这些用户访问 FTP 服务器，甚至不会提示输入密码。默认的用户列表是 `/etc/vsftpd_user_list`，但你可以通过 `userlist_file` 选项覆盖此设置。

- `write_enable=YES` 使 `vsftpd` 允许向主机上传文件。

- `xferlog_enable=YES` 开启文件下载和上传的日志记录（这始终是个好主意，但会占用磁盘空间）。

- `xfer_log_file=/var/log/vsftpd.log` 指定 `vsftpd` 日志文件的完整路径名。默认值为 `/var/log/vsftpd.log`。

- `xferlog_std_format=YES` 使 `vsftpd` 以其他 FTP 守护进程使用的标准格式生成日志文件。

## `/etc/vsftpd.ftpusers` 文件

当 `vsftpd` 服务器尝试让用户登录时，它使用 PAM 来验证用户（正如正常登录过程使用 PAM 来完成工作一样）。`vsftpd` 的 PAM 配置文件是 `/etc/pam.d/vsftpd`。该 PAM 配置文件以如下方式引用 `/etc/vsftpd.ftpusers`：

```text
auth    required      /lib/security/pam_listfile.so item=user sense=deny
          file=/etc/vsftpd.ftpusers sense=success
```

此命令基本上表示，任何列在 `/etc/vsftpd.ftpusers` 文件中的人都将被拒绝登录。

根据发行版的不同，`/etc/pam.d/vsftpd` 文件可能引用除 `/etc/vsftpd.ftpusers` 之外的其他文件名。例如，在 Fedora Core 中，`/etc/pam.d/vsftpd` 文件指定 `/etc/vsftpd/ftpusers` 作为包含被拒绝登录的用户名的文件，而 SUSE Linux 使用 `/etc/ftpusers` 文件列出不允许访问 `vsftpd` 的用户名。通常，该列表设置为拒绝与服务器相关而非真实用户的用户名（如 `root`、`news`、`uucp` 等）的 FTP 访问。

## `/etc/vsftpd.user_list` 文件

如果 `userlist_enable` 选项设置为 `YES` 且 `userlist_deny` 设置为 `YES`，`vsftpd` 不允许列在 `/etc/vsftpd.user_list` 文件中的用户访问任何 FTP 服务。它甚至不会提示他们输入密码。然而，如果 `userlist_deny` 设置为 `NO`，含义则相反，这些用户是允许访问的唯一用户。（但是，PAM 配置仍然拒绝任何在 `/etc/vsftpd.ftpusers` 列表中的人。）如果 `userlist_enable` 设置为 `NO`，则不使用 `/etc/vsftpd.user_list` 文件。
