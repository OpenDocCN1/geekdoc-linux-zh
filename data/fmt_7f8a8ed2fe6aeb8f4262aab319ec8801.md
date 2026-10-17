
# ps -aux | grep inetd

root  1640 0.0 0.6 1048 780 ?? Ss Thu08PM 0:00.15 inetd -Ww

如果您没有看到 `inetd` 进程正在运行，您可能已经在 `/etc/rc.conf` 中将其关闭；请在那里查找 `inetd_enable="NO"` 行，如果存在则删除或禁用它。其次，打开 `/etc/inetd.conf` 并确保 `ftpd` 服务已启用：

```
ftp stream tcp nowait root /usr/libexec/ftpd ftpd -l
```

如果此行被注释掉了，请取消注释，并重启 `inetd`（使用 `killall -HUP inetd` 命令）。通过尝试连接服务器（`ftp localhost`）来检查您的配置。如果您看到登录提示，说明一切正常。如果没有，请重新检查上述步骤；如有必要，完全终止 `inetd` 并重新启动它。

## 控制 FTP 访问

FTP 访问不是可以随意启用的；虽然用户访问 FTP 以向服务器上传文件（如网页）至关重要，但它也是潜在的安全问题来源——它是一种明文机制，这意味着所有数据（包括密码）都未经加密传输，任何使用数据包嗅探软件窃听的人都可以获取。正如您将在第 29 章“网络安全”中学到的，大多数主要的明文服务都可以被安全等价物所取代：用 SSH 取代 Telnet，用 Secure HTTP 取代 HTTP，以及用 POP3 和 IMAP 自带的加密层取代它们。然而，FTP 本质上是不安全的，尽管提出了几种安全解决方案（如 Brian Wellington 的 `sftp` 和相应的 `sftpd`），未加密的 FTP 仍作为最后一种广泛使用的不安全数据传输协议，难以被取代，并且是一个功能完善的服务器的事实上的需求。您将在第 29 章中学习如何使 FTP 更安全；在此期间，请记住，在启用用户 FTP 访问时必须格外小心，以确保系统的安全。

鉴于此，您需要一种方式将某些用户锁定，使他们无法通过 FTP 连接到系统。这可以通过多种方式实现。最方便的两种涉及 `/etc/ftpusers` 和 `/etc/shells` 文件。第三种，`/var/run/nologin`，控制服务器是否完全接受连接。

### /etc/ftpusers 文件

禁止某个特定用户（或一组用户）连接到 FTP 服务器的最简单方法是将该用户的登录名添加到 `/etc/ftpusers` 文件中，该文件在默认的 FreeBSD 安装中存在，并包含各种系统伪用户（如 `operator`、`bin`、`tty` 等）的名称。这些用户具有空密码，`ftpd` 不允许任何具有空密码的人连接；在 `/etc/ftpusers` 中保留用户名提供了额外的安全层。

您可以向文件中添加任何用户名，并且由于 `ftpd` 每次新连接都会读取所有相关配置文件，因此无需重启任何进程。尝试作为被拒绝的用户连接到 FTP 服务器，您应该会得到类似于以下的响应：

```
# ftp localhost

Connected to localhost.somewhere.com.

220 stripes.somewhere.com FTP server (Version 6.00LS) ready.

Name (localhost:frank):

530 User frank access denied.

ftp: Login failed.

ftp>
```

### 注意

> 请注意，访问被拒绝的消息会在服务器接收到用户名后立即出现——它不会提示输入密码。这可以防止密码通过网络传输，从而在你因为担心窃听者嗅探密码而禁用某个用户时，提供额外的安全预防措施。

你还可以将任何组名添加到 `/etc/ftpusers` 中；只需在名称前加上“at”（@）符号（例如，@users）。属于文件中列出的任何组的用户都将被禁止访问。

### `/etc/shells` 文件

在查看用户是否列在 `/etc/ftpusers` 中之后，`ftpd` 会检查与该用户关联的 shell，并查看它是否列在 `/etc/shells` 中。如果没有，用户将获得与 `/etc/ftpusers` 相同类型的访问被拒绝消息。你可以通过将用户的 shell 更改为 `/sbin/nologin` 来利用此功能，以防止用户通过终端程序或 FTP 登录（这在第 11 章中见过——它只是打印一条账户不可用的消息并退出，且未列在 `/etc/shells` 中）或类似构建的内容。

### `/var/run/nologin` 文件

如果要完全关闭 FTP 登录，而不修改 `/etc/inetd.conf` 或任何其他此类配置文件，你只需在 `/var/run` 中放置一个名为 `nologin` 的文件即可。如果 `ftpd` 发现此文件，它将按以下方式响应所有连接：

```
$ ftp localhost

Connected to localhost.somewhere.com.

530 System not available.

ftp>
```
