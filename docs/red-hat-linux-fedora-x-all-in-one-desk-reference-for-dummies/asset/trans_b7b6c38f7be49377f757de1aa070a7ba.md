

## 642 配置 FTP 服务器

- `ascii_download_enable=YES` 启用 ASCII 模式下的文件下载。遗憾的是，恶意的远程用户可以使用一个大文件的名称发出 `SIZE` 命令，从根本上导致 FTP 服务器浪费大量资源来打开该文件并确定其大小。这种技术被用于拒绝服务攻击（在本节稍后的部分提到）。

- `ascii_upload_enable=YES` 启用 ASCII 模式下的文件上传（用于文本文件）。

- `async_abor_enable=YES` 让 vsftpd 识别任何时候到达的 ABORT（中止）请求。你可能需要允许旧版本的 FTP 客户端与 vsftpd 工作。

- `banned_email_file=/etc/vsftpd.banned_emails` 指定包含禁电子邮件列表的文件（仅在 `deny_email` 设置为 YES 时使用）。

- `chown_uploads=YES` 允许匿名文件由 `chown_username` 选项指定的用户所有。除非绝对必要，否则不要启用此选项 —— 不要将 `chown_username` 设置为 root（那将是一个不可避免的灾难）。

- `chown_username=NAME` 指定拥有匿名 FTP 用户上传文件的所有者用户名。

- `chroot_list_enable=YES` 让 vsftpd 将 `chroot_list_file` 列表中列出的用户以外的所有用户限制在他们登录 FTP 服务时的家目录中。此选项防止这些用户访问其家目录之外的任何文件。

- `chroot_list_file=/etc/vsftpd.chroot_list` 是一个用户列表，根据 `chroot_local_user` 的设置，这些用户将被限制在家目录内或不受限制。

- `connect_port_20=YES` 让 vsftpd 确保数据通过 20 端口（FTP 数据端口）传输。

- `data_connection_timeout=120` 是空闲连接在多少秒后超时超时（单位为秒）。

- `deny_email_enable=YES` 让 vsftpd 检查禁电子邮件列表，并拒绝任何尝试用禁电子邮件作为密码进行匿名登录的用户。

- `dismissage_enable=YES` 当 FTP 用户切换到特定目录时，让 vsftpd 显示消息。

- `ftpd_banner=Welcome to my FTP service` 设置用户登录时 vsftpd 显示 banner。你可以将消息更改为任何内容。

- `idle_session_timeout=600` 是空闲会话（指有人连接但未进行任何操作的情况）超时后的时间（单位为秒），此时 vsftpd 将用户注销。

- `listen=YES` 让 vsftpd 在独立模式下按顺序监听连接请求。如果你想在 xinetd 模式下运行 vsftpd，请将此选项设置为 NO。

- `local_enable=YES` 让 vsftpd 授予本地用户访问 FTP 的权限。

- `local_umask=022` 意味着 FTP 写入权限为 644（所有人可读，但仅所有者可写）。你可以通过设置文件权限掩码来设置它。例如，如果你希望除所有者之外的任何人都没有权限，请将此选项改为 077。

- `Is_recursive_enable=YES` 让 vsftpd 使用 `ls -R` 命令递归遍历目录。

- `nopriv_user=vsftpd` 让 vsftpd 识别一个 FTP 服务器可以使用非特权账户。

- `pam_service_name=vsftpd` 是当 vsftpd 必须验证用户时使用的可插身份模块（PAM）配置文件名。默认情况下，PAM 配置文件位于 /etc/pam.d 目录。这意味着 vsftpd 的 PAM 配置文件为 /etc/pam/vsftpd。

- `tcp_wrappers=YES` 通过 TCP wrapper 启用访问控制，该 wrapper 使用 `/etc/hosts.allow` 和 `/etc/hosts.deny` 文件（关于 TCP wrapper 的更多信息，请参阅第七卷第三章）。

- `userlist_deny=YES` 让 vsftpd 拒绝访问 `/etc/vsftpd.user_list` 中列出的用户。这些用户不会被提示密码。

- `write_enable=YES` 让 vsftpd 允许向主机上传文件。

- `xferlog_enable=YES` 开启文件下载和上传的日志记录（始终是个好主意，但会占用磁盘空间）。

- `xferlog_file=/var/log/vsftpd.log` 指定 vsftpd 日志文件的完整路径。默认值是 /var/log/vsftpd.log。

- `xferlog_std_format=YES` 让 vsftpd 生成其他 FTP 守护进程使用的格式的日志文件。

## etc/vsftpd.ftusers 文件

vsftpd 服务器使用可插身份模块（PAM）在用户尝试登录时对其进行身份验证（就像普通登录过程使用 PAM 来完成工作一样）。vsftpd 的 PAM 配置文件为 /etc/pam.d/vsftpd。该 PAM 配置文件如下引用 /etc/vsftpd.ftusers 文件：

```
auth required /lib/security/pam_listfile.so item=user-deny
file=/etc/vsftpd.ftusers sense=succeed
```

![](img/d9230b719dc0efd80851f363d8c6f571_669_0.png)

## 644 设置安全的匿名 FTP

此命令基本上表示拒绝在 /etc/vsftpd.ftpusers 中列出的任何用户登录。默认的 /etc/vsftpd.ftpusers 文件包含以下用户列表：

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
- nbody

## etc/vsftpd.userlist 文件

如果 `userlist_deny` 设置为 YES，vsftpd 将拒绝访问 `/etc/vsftpd.user_list` 中列出的用户。这些用户不会被提示密码。如果 `userlist_deny` 设置为 NO，情况则反过来，只有在列表中的用户才被允许访问。

## 设置安全的匿名 FTP

此命令基本上表示拒绝在 /etc/vsftpd.ftpusers 中列出的任何用户登录。默认的 /etc/vsftpd.ftpusers 文件包含以下用户列表：

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
- nbody

## 645 尝试匿名 FTP

遗憾的是，匿名 FTP 的便利是有代价的。如果你不正确配置匿名 FTP 服务，入侵者和恶作剧可能会访问你的系统。某些入侵者可能只是将你的磁盘作为各种文件的临时存放；另一些可能会用垃圾文件填满你的磁盘，导致你的系统无法运行（这种攻击被称为拒绝服务攻击）。在极端情况下，入侵者可能会获得系统的用户级（更糟的是 root 级）访问并造成巨大破坏。Fedora Core 的匿名 FTP 设置采用了必要的措施。

### 尝试匿名 FTP

要查看匿名 FTP 的效果，尝试使用 FTP 客户端访问你的系统。在下面的示例会话中，我访问了 FTP 服务器（我的输入加粗显示）：

```
ftp localhost
Connected to localhost (127.0.0.1).
220 (vsFTPd 1.2.1)
Name (localhost): anonymous
331 请指定密码。
Password: 我可以输入任何密码
230 登录成功。
远端系统类型为 UNIX。
使用二进制模式传输文件。
227 进入被动模式 (127,0,0,169,190)
150 正在发送目录列表。
drwx-xr-x 2 0 4096 Jun 06 04:36 pub
226 目录发送完成。
ftp bye
221 再见。
```

当你以匿名 FTP 登录时，你访问名为 ftp 的用户的家目录（默认目录为 /var/ftp）。将公开访问的文件 —— 即你希望其他人从你的系统下载的文件 —— 放在 /var/ftp/pub 目录下。

### 匿名 FTP 的特征

匿名 FTP 设置的主要特征如下：

- 用户 ftp，其家目录为 /var/ftp。该用户没有分配 shell。当你在 /etc/passwd 文件中搜索 ftp 时，会得到如下：

```bash
grep ftp /etc/passwd
```

