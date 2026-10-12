

## 642 配置 FTP 服务器

- `ascii_download_enable=YES` 启用 ASCII 模式下的文件下载。不幸的是，恶意的远程用户可以发出带有巨大文件名的 `SIZE` 命令，实际上会导致 FTP 服务器浪费大量资源来打开该文件并确定其大小。这种技术被用于拒绝服务攻击（本节稍后将会提到）。
- `ascii_upload_enable=YES` 启用 ASCII 模式下的文件上传（针对文本文件）。
- `async_abor_enable=YES` 使 `vsftpd` 能够识别在任何时间到达的 `ABOR`（中止）请求。你可能需要启用它，以允许旧的 FTP 客户端与 `vsftpd` 配合工作。
- `banned_email_file=/etc/vsftpd.banned_emails` 指定包含被禁止电子邮件地址列表的文件（仅在 `deny_email_enable` 设置为 `YES` 时使用）。
- `chown_uploads=YES` 使上传的匿名文件的所有者变为由 `chown_username` 选项指定的其他用户。除非绝对必要，否则不要启用此选项——并且不要将 `root` 指定为 `chown_username`（那将是灾难发生的前兆）。
- `chown_username=name` 指定拥有由匿名 FTP 用户上传的文件的用户名。
- `chroot_list_enable=YES` 使 `vsftpd` 在 FTP 服务登录时，将除 `chroot_list_file` 指定列表中的用户以外的所有用户限制在其主目录中。此选项可防止这些用户访问主目录之外的任何其他文件。
- `chroot_list_file=/etc/vsftpd.chroot_list` 是用户列表，根据 `chroot_local_user` 的设置，这些用户要么被限制在其主目录中，要么不受限制。
- `connect_from_port_20=YES` 使 `vsftpd` 确保数据传输通过端口 20（FTP 数据端口）进行。
- `data_connection_timeout=120` 是数据连接超时的秒数，在此之后非活动数据连接将超时。
- `deny_email_enable=YES` 使 `vsftpd` 检查被禁止的电子邮件地址列表，并拒绝任何试图使用被禁止的电子邮件地址作为密码进行匿名登录的人的访问。
- `dirmessage_enable=YES` 使 `vsftpd` 在 FTP 用户切换到某些目录时显示消息。
- `ftpd_banner=Welcome to my FTP service` 设置当用户登录时 `vsftpd` 显示的横幅。你可以将消息更改为你想要的任何内容。
- `idle_session_timeout=600` 是空闲会话（指某人连接后未执行任何操作的情况）超时的秒数，之后 `vsftpd` 会将该用户注销。
- `listen=YES` 使 `vsftpd` 监听连接请求，从而以独立模式运行。如果你想通过 `xinetd` 运行 `vsftpd`，请将此选项设置为 `NO`。
- `local_enable=YES` 使 `vsftpd` 授予本地用户访问 FTP 的权限。
- `local_umask=022` 意味着 FTP 写入的任何文件的权限均为 644（所有人可读，但仅所有者可写）。你可以将其设置为任何你想要的文件权限掩码。例如，如果你希望除了所有者以外任何人没有权限，请将此选项更改为 077。
- `ls_recurse_enable=YES` 允许 FTP 用户通过使用 `ls -R` 命令递归遍历目录。
- `nopriv_user=ftp` 标识一个非特权用户账户，FTP 服务器可以使用该账户。
- `pam_service_name=vsftpd` 是当 `vsftpd` 必须验证用户时使用的可插拔认证模块（PAM）配置文件的名称。默认情况下，PAM 配置文件位于 `/etc/pam.d` 目录中。这意味着 `vsftpd` 的 PAM 配置文件是 `/etc/pam.d/vsftpd`。
- `tcp_wrappers=YES` 启用通过 TCP wrapper 进行访问控制的支持，该控制会参考文件 `/etc/hosts.allow` 和 `/etc/hosts.deny`（有关 TCP wrapper 的更多信息，请参阅第七卷，第 3 章）。
- `userlist_deny=YES` 使 `vsftpd` 拒绝 `/etc/vsftpd.user_list` 文件中列出的用户访问。甚至不会提示这些用户输入密码。
- `write_enable=YES` 使 `vsftpd` 允许向主机上传文件。
- `xferlog_enable=YES` 开启文件下载和上传的记录（这是一个好主意，但会占用磁盘空间）。
- `xferlog_file=/var/log/vsftpd.log` 指定 `vsftpd` 日志文件的完整路径名。默认值是 `/var/log/vsftpd.log`。
- `xferlog_std_format=YES` 使 `vsftpd` 生成其他 FTP 守护程序使用的标准格式的日志文件。

### /etc/vsftpd.ftpusers 文件

当用户尝试登录时，`vsftpd` 服务器使用*可插拔认证模块（PAM）*来验证用户（就像正常的登录过程使用 PAM 来完成这项工作一样）。`vsftpd` 的 PAM 配置文件是 `/etc/pam.d/vsftpd`。该 PAM 配置文件像这样引用 `/etc/vsftpd.ftpusers`：

```
auth required /lib/security/pam_listfile.so item=user sense=deny file=/etc/vsftpd.ftpusers onerr=succeed
```

这条命令基本上表示，如果某人列在 /etc/vsftpd.ftpusers 中，则被拒绝登录。默认的 /etc/vsftpd.ftpusers 文件包含以下用户列表：

- root
- bin
- daemon
- adm
- lp
- sync
- shutdown
- halt
- mail
- news
- uucp
- operator
- games
- nobody

### /etc/vsftpd.user_list 文件

如果 user_list_deny 选项设置为 YES，vsftpd 不允许列在 /etc/vsftpd.user_list 文件中的用户访问任何 FTP 服务。甚至不会提示他们输入密码。然而，如果 user_list_deny 设置为 NO，含义则相反，这些用户是唯一被允许访问的用户（但 PAM 配置仍然拒绝 /etc/vsftpd.ftpusers 列表中的任何人）。

## 设置安全的匿名 FTP

匿名 FTP 指的是使用用户名 anonymous，任何人都可以使用该用户名通过 FTP 从系统传输文件。匿名 FTP 是在互联网上共享文件的常见方式。

如果你曾经使用匿名 FTP 从互联网站点下载文件，你就已经知道该服务的便利之处了。匿名 FTP 使互联网上的任何人都可以获取信息。如果你有一个新的 Fedora Core 应用程序想要与世界分享，请在你的 Fedora Core 计算机上设置匿名 FTP，并将软件放在适当的目录中。之后，你只需要向世界宣布（可能是通过在 comp.os.announce 新闻组中发布帖子）你有一个新的程序可用。现在，任何人都可以根据自己的方便从你的系统获取软件。

即使你经营一家盈利企业，你也可以使用匿名 FTP 来支持你的客户。如果你销售硬件或软件产品，你可能希望通过匿名 FTP 提供技术信息或软件“修复包”。

不幸的是，匿名 FTP 的便利性是有代价的。如果你没有正确配置匿名 FTP 服务，入侵者和恶作剧者可能会获得对你系统的访问权限。一些入侵者可能只是将你的系统磁盘用作各种文件的临时存储场所；另一些则可能用垃圾文件填满你的磁盘，实际上使你的系统无法运行（这种攻击被称为拒绝服务攻击）。在另一个极端，入侵者可能会获得用户级（或更糟糕的，root 级）访问权限，并造成更大的破坏。Fedora Core 中的默认匿名 FTP 设置采用了必要的安全预防措施。

### 尝试匿名 FTP

为了查看匿名 FTP 的实际运行情况，请尝试使用 FTP 客户端访问你的系统。例如，在以下示例会话中，我从同一系统上的终端窗口访问了 FTP 服务器（我的输入以**粗体**显示）：

```
ftp localhost
Connected to localhost (127.0.0.1).
220 (vsFTPD 1.2.1)
Name (localhost:naba): anonymous
331 Please specify the password.
Password: < - I can type anything as password
230 Login successful. Have fun.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls -l
227 Entering Passive Mode (127,0,0,1,169,190)
150 Here comes the directory listing.
drwxr-xr-x   2     0         0     4096 Jun 06 04:36 pub
226 Directory send OK.
ftp> bye
221 Goodbye.
```

当你成功登录匿名 FTP 时，你访问的是名为 ftp 的用户的主目录（默认目录是 /var/ftp）。将公开可访问的文件——即你希望允许他人从你的系统下载的文件——放在 /var/ftp/pub 目录中。

### 匿名 FTP 的关键特性

匿名 FTP 设置的关键特性如下：

- 一个名为 ftp 的用户，其主目录是 /var/ftp。该用户没有分配 shell。这是在 /etc/passwd 文件中搜索 ftp 时得到的结果：

```
grep ftp /etc/passwd
```

