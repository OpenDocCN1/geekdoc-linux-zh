
# 第 22 章 使用 NFS 和 NIS

这会告诉 NIS 每当请求密码信息时，都附加从 NIS 服务器检索的密码映射（文件）的内容。

注意，任何个人账户（包括你的账户）的条目已从简化的密码文件中删除。这使得你能够进行一个相当简单的测试来确定 NIS 是否正常工作。如果你可以登录一个在客户端系统密码文件中不存在但在 NIS 服务器密码文件中存在的账户，那么你就可以确定 NIS 正在工作了。

要设置 NIS 客户端，请以 `root` 身份或使用 `su` 命令切换到 `root` 身份，位于你正用作 NIS 客户端的系统，并执行以下操作：

1. 确保你的 Linux 系统上安装了 NIS 客户端软件。你至少需要 `/bin/domainname` 和 `/sbin/ypbind` 程序。
2. 确保目录 `/var/yp` 存在，如果不存在则创建它。
3. 设置你的新客户端将所属的 NIS 域名。这应该与本章稍些时候的域名相同。要设置 NIS 域名（在本例中设置为域 `foo.com`），请发布如下命令：
   ```
   /bin/domainname foo.com
   ```
4. 使用如下命令启动 NIS 客户端进程：
   ```
   /sbin/ypbind
   ```

要验证 NIS 是否工作正常，请从 NIS 客户端系统使用 `telnet` 或 `ssh` 命令尝试以你的身份登录。记住，你的密码文件条目存在 NIS 服务器的密码文件中，但不在 NIS 客户端的密码文件中。

你应该能够成功登录。恭喜你——你正在运行 NIS 了！你现在应该修改系统的启动序列，以添加 `/etc/init.d/ypserv` 启动脚本。

## 总结

NFS 和 NIS 提供了一个强大但易于配置的分布式文件系统和分布式认证服务的组合。SUSE 的管理工具简化了 NFS 和 NIS 的配置，使得创建 NFS/NIS 客户端和服务器变得简单。

## 在 SUSE 上运行 FTP 服务器

FTP 是文件传输协议（File Transfer Protocol），广为人知的允许从公共服务器进行匿名下载的方法。

传统上，Unix 系统默认运行 FTP 守护进程，用户期望能够从其他处的 FTP 客户端从他们的家目录移动文件。这是一种在不登录的情况下访问系统的方便方法，并且可以从任何类型的客户端访问。这种类型的 FTP 必须被视为既不安全又没有。

- 它被认为是不安全的，因为通常用户名/密码对是以明文形式跨网络发送的，容易受到网络嗅探的密码窃取。`telnet` 和 `ssh` 被认为是不安全的，在公共网络上使用 FTP 应该谨慎对待。
- 这种类型的 FTP 使用由于 `telnet` 和 `ssh` 同样的原因也是没有必要的：因为有了 `ssh`、`scp`、`sftp` 程序。这些程序提供了实现相同目的的完全安全的方法。（由于提供了如 KDE 的“fish” ios 等良好的客户端实现，意味着你可以在传输文件的同时从客户端图形化地查看服务器上的目录。）

FTP 糟糕的安全性声誉因某些 FTP 实现遭受了各种漏洞而变得更加糟糕，包括允许通过使用缓冲区溢出等手段获取客户端 root 权限的利用漏洞。

另一个点是，如果你的 FTP 服务器旨在允许上传，你将需要仔细考虑安全性。任何允许开放中继的邮件服务器在几小时内就会被用于该目的。与此类似，如果你在互联网上运行一个允许

## 本章内容

- FTP 的安全问题
- 使用 `vsftpd` 设置匿名 FTP 服务器
- 允许用户访问
- 允许上传
- 允许匿名上传
- 使用 `pure-ftpd`

匿名上传，如果你不小心，它将在短时间内被利用。与此类似，如果你在互联网上运行一个允许

# 第四部分 在 SUSE Linux 中实现网络服务

注意，FTP 服务器假设默认用户名与客户端上的用户名相同。此时，如果你接受默认值并按回车，或者输入系统已知的另一个用户名，你将看到此内容：

```
530 This FTP server is anonymous only.
ftp: Login failed.
ftp>
```

但如果你使用 `ftp` 或 `anonymous` 中的任一用户名登录，你可以提供任何密码（传统情况下这应该是一个有效的电子邮件地址，但服务器将接受任何内容，包括空密码），你就登录成功。

```
username:/home/user > ftp bible
Connected to bible.
220 (vsFtpd 2.0.2)
Name (bible:user):ftp
331 Please specify the password.
Password:
230 Remote system type is UNIX.
Using binary mode to transfer files.
ftp>
```

如果你现在使用 `ls` 列出 FTP 服务器上的文件，你（并不不意外地）会发现那里并没有：

```
ftp> ls
229 Entering Extended Passive Mode (||37477|)
150 Here comes the directory listing.
226 Directory OK.
ftp>
```

作为匿名 FTP 根目录的服务器位置是 `/srv/ftp/`（就像 Apache Web 服务器的根目录是 `/srv/www/`）。无论你在那里放置什么文件和目录，在 FTP 中都是可见的。如果你将文件复制到 `/srv/ftp/`，你将通过 FTP `get` 命令下载它：

```
ftp> get afile
local: afile remote: afile
229 Entering Extended Passive Mode (||19160)
150 Opening BINARY mode data connection for afile (4096 bytes).
226 File sent OK.
ftp>
```

如果你查看服务器上的 `/var/log/messages`，你会发现 `vsftpd` 记录了该登录：

```
Jun 25 16:41:13 bible vsftpd: Sun Jun 25 16:41:13 2004 [pid 21339] CONNECT: Client
"192.168.2.3"
```

```
Jun 25 16:41:13 bible vsftpd: Sun Jun 25 16:41:13 2004 [pid 21338] [ftp] LOGIN: Client
"192.168.2.3", anon password "password"
```

# 第 23 章 在 SUSE 上运行 FTP 服务器

每次下载都会被记录。

注意，你可以通过对 `/etc/vsftpd.conf` 进行细微更改，强制 `vsftpd` 将其日志写入自己的日志文件。只需确保存在以下行即可：

```
log_ftp_protocol=YES
xfer_enable=YES
vsftpd_log_file=/var/log/vsftpd.log
```

然后注释掉或删除该行：

```
syslog_enable=YES
```

你可以通过在配置文件包含包含这样的行来创建一个自定义的 FTP 横幅：

```
ftpd_banner="Welcome to our very fine FTP service."
```

当用户使用文本模式 FTP 或专用 FTP 客户端登录时，他们将在登录提示符之前看到以下消息：

```
220 "Welcome to our very fine FTP service."
Name (localhost:user):
```

这可以用于提供服务消息，但对于通过浏览器连接的用户来说没有用。包含 `README` 和 `README.html` 文件可能有用，这些用户可以点击这些文件。

你还可以在 `/srv/ftp/` 或其任何子目录下放置名为 `.message` 的文件。当用户切换到一个包含文件的目录时，文件的内容将被显示。

```
ftp> cd pub
250-This directory contains useful files
250 Directory successfully changed.
ftp->
```

文件 `/srv/ftp/pub/.message` 仅包含这一行：

```
This directory contains useful files
```

`vsftpd` 允许被动 FTP 连接，除非你在配置文件中设置了

`pasv_enable=NO`。

你几乎想要允许被动连接，否则许多从防火墙后方连接的客户端将无法连接。

主动 FTP 同时在服务器的 20 端口（用于数据传输）和 21 端口（用于控制命令）上运行，并涉及从服务器到客户端的响应连接，这种连接可能会被客户端所在的防火墙阻挡。被动 FTP 仅涉及服务器 21 端口，不太可能引起允许建立连接的标准防火墙配置产生问题。有关更多防火墙配置，请参阅第 24 章。

注意配置文件中的所有选项都以以下形式指定：

```
option=value
```

并且在 `=` 符号前后不应有空格。
