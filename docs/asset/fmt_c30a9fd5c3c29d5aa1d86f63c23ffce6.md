
默认情况下，`vsftpd` 几乎不允许任何操作。通过 `/etc/vsftpd/vsftpd.conf` 中的选项，你可以放宽限制以便使用户可以使用 FTP。如何设置这些选项取决于你。请注意，大多数选项被设置为 `YES`。这是因为大多数的默认设置都是 `NO`。若要反转某个选项的意图，只需在行首添加一个 `#` 注释掉该选项即可。

以下是你可以在 `/etc/vsftpd/vsftpd.conf` 中设置的选项：

- `anon_mkdir_write_enable=YES` 允许匿名用户创建新目录。这是另一个高风险选项，即使你允许匿名用户上传文件，可能也想将其设置为 `NO`。
- `anon_upload_enable=YES` 意味着匿名 FTP 用户可以上传文件。只有当 `write_enable` 已设置为 `YES` 且目录对所有人都有权限时，此选项才生效。因为允许匿名用户在你的系统上写入是非常危险的，有人可能会填磁盘或将你的磁盘用于个人存储。
- `anonymous_enable=YES` 启用匿名 FTP（这样用户可以使用 `anonymous` 作为用户名登录并提供其电子邮件地址作为密码）。如果你不需要匿名 FTP，请注释掉此行。
- `ascii_download_enable=YES` 启用 ASCII 模式下的文件。遗憾的是，恶意的远程用户可以针对大文件发出 `SIZE` 命令，导致 FTP 服务器浪费大量资源打开该文件并确定其大小。这可以被恶意用户用于拒绝服务攻击。
- `ascii_upload_enable=YES` 启用 ASCII 模式下的文件（针对文本文件）。
- `async_abor_enable=YES` 使 `vsftpd` 能够识别随时给出的 `ABOR`（中止）请求。你可能需要启用它以允许旧的 FTP 客户端与 `vsftpd` 配合。
- `banned_email=/etc/vsftpd.banned_email` 指定包含禁用地址列表的文件（仅当 `deny_email` 设置为 `YES` 时使用）。
- `chown_uploads=YES` 使上传的匿名文件由 `chown_username` 选项指定的不同用户所有。除非绝对必要，不要启用此项，且不要将 `chown_username` 设置为 `root`。
- `chown_username=name` 指定匿名 FTP 用户所拥有文件的用户名。
- `chroot_list=YES` 使 `vsftpd` 在用户登录 FTP 服务时，将 `chroot_list_file` 指定列表中的用户之外的所有用户限制在自己的主目录下。这防止了这些用户访问除指定内容以外的任何文件。
- `chroot_list_file=/etc/vsftpd.chroot_list` 是被限制在主目录内的用户列表。
- `connect_from_port_20=YES` 使 `vsftpd` 确保数据传输通过 20 端口进行。
- `data_connection_timeout=120` 是无活动连接超时的时间（秒）。
- `deny_email_enable=YES` 使 `vsftpd` 检查地址列表并拒绝任何尝试使用电子邮件登录的用户。
- `dirmessage_enable=YES` 使 `vsftpd` 在用户进入某些目录时显示消息。
- `ftp_banner=Welcome to my FTP service` 设置 `vsftpd` 显示的横幅。你可以更改为任何内容。
- `idle_session_timeout=600` 是空闲会话（连接后未进行操作）超时的时间（秒），`vsftpd` 会记录用户。
- `listen=YES` 使 `vsftpd` 监听请求并因此以独立模式运行。
- `local_enable=YES` 使 `vsftpd` 允许本地用户访问 FTP。
- `local_umask=022` 意味着 FTP 写入的文件权限为 644（所有人读，所有写）。你可以将其设置为任何掩码。例如，如果你希望没有任何权限，请将其改为 077。
- `ls_recurse=YES` 允许 FTP 使用 `-R` 递归遍历目录。
- `nopriv_user=vsftpd` 是 FTP 服务器可以使用的特权用户。
- `pam_service_name=vsftpd` 是 `vsftpd` 需要验证用户时使用的可插件认证模块（PAM）配置名称。默认情况下 PAM 配置位于 `/etc/pam.d`。这意味着 `vsftpd` 的 PAM 配置文件是 `/etc/pam.d/vsftpd`。
- `userlist_deny=YES` 使 `vsftpd` 拒绝 `/vsftpd.user_list` 文件中的用户。这些用户不会提示密码。
- `write_enable=YES` 使 `vsftpd` 允许向主机上传文件。
- `xferlog_enable=YES` 开启文件下载和上传的日志（好主意，但会占用磁盘空间）。
- `xferlog_file=/var/log/vsftpd.log` 指定 `vsftpd` 日志文件的完整路径。默认 `/var/log/vsftpd.log`。
- `xferlog_std_format=YES` 使 `vsftpd` 生成供守护进程使用的标准格式日志文件。

# 理解 /etc/vsftpd.ftpusers

`vsftpd` 服务器使用可插件认证模块（PAM）在用户尝试登录时进行身份验证，就像普通登录过程使用 PAM 一样。`vsftpd` 的 PAM 配置文件为 `/etc/pam.d/vsftpd`。PAM 如下引用 `/etc/vsftpd.ftpusers`：

```
auth required pam_listfile.so item=sense-deny
file=/etc/vsftpd.ftpusers onerr=succeed
```

继续

## 第三部分：使用 Red Hat Linux 进行联网

这基本上意味着列在 `/etc/vsftpd.ftpusers` 中的任何用户都应该被拒绝登录。默认的 `/etc/vsftpd.ftpusers` 文件包含以下用户列表：

- `root`
- `bin`
- `daemon`
- `adm`
- `lp`
- `sync`
- `shutdown`
- `halt`
- `mail`
- `news`
- `uucp`
- `operator`
- `games`
- `nobody`

如果你想拒绝其他任何用户名的 FTP 访问，只需将这些名称添加到 `/etc/vsftpd.ftpusers` 文件中即可。

## 理解 /etc/vsftpd.user_list 文件

如果 `userlist_deny` 选项设置为 `YES`，`vsftpd` 不允许 `/etc/vsftpd.user_list` 文件中列出的用户访问任何 FTP 服务。它甚至不会提示他们输入密码。然而，如果 `userlist_deny` 被设置为 `NO`，含义就反过来了，这些用户是唯一被允许访问的用户（但 PAM 配置仍会拒绝 `/etc/vsftpd.ftpusers` 列表中的任何人）。

## 设置安全匿名 FTP

匿名 FTP 指使用用户名 `anonymous`，任何人都可以使用它通过 FTP 从系统传输文件。匿名 FTP 是互联网上共享文件的常用方式。

如果你已经使用匿名 FTP 从互联网站点下载过文件，你已经知道该服务的便利性了。匿名 FTP 让互联网上的任何人都能获取信息。如果你有一个想与世界共享的新 Linux 应用程序，请在你的 Linux 电脑上设置匿名 FTP，并将软件放置在适当的目录中。之后，你所做的就是向世界宣布（可能通过通过在 `comp.os.linux.announce` 新闻组中发帖）你已经有一个新程序可用了。现在，任何人都可以根据自己的方便从你的系统获取该软件。

# 第 17 章：FTP 服务器

即使你经营的是营利性业务，也可以使用匿名 FTP 来支持你的客户。如果你销售硬件或软件产品，你可能希望通过匿名 FTP 提供技术信息或软件“修复”。

遗憾的是，匿名 FTP 的便利性是有代价的。如果你不配置你的匿名 FTP 服务，入侵者和恶作剧者可能会访问你的系统。某些入侵者可能仅仅将你的系统磁盘作为各种文件的临时存放；另一些人可能会用垃圾文件填充你的磁盘，实际上导致你的系统无法运行（这种攻击被称为拒绝服务攻击——DoS 攻击）。在极端情况下，入侵者可能会获得你系统的用户级（或更糟的 root 级）访问权限并造成更大的破坏。

如果你已经从这本书的附带 CD-ROM 中安装了 Red Hat Linux，那么你的系统中已经有了匿名 FTP。默认设置已采用了必要的安全预防措施。

## 尝试匿名 FTP

要查看匿名 FTP 的运行情况，尝试使用 FTP 客户端访问你的系统。例如，在下面的示例会话中，我从局域网上的另一台 PC 访问了我的系统（我的输入以粗体显示）：
