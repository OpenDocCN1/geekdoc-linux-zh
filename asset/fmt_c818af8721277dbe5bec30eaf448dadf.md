
连接到服务器后，我在登录提示处输入了 `anonymous`。服务器说 `anonymous` 可以，并输入我的电子邮件地址作为密码（密码不会显示；我用星号来表示密码）。服务器接受密码为有效。如果地址不符合标准，服务器将“警告”用户但仍然允许用户登录。如果是非有效的，服务器将允许用户登录。在 Red Linux 系统中，访客用户被限制在 `/var/ftp` 目录。在连接时，我通过输入 `bye` 结束了会话。

在连接服务器时，我以 `用户` 登录。`在` 情况下，用户可以访问 `/var/ftp` 目录。

`/var/ftp` 目录内包含了使 FTP 正常工作所需的目录和文件，而无需您访问文件系统中的其他文件。`/bin` 目录包含 FTP 可能需要的执行命令（如 `compress`、`ls` 和 `gzip`）。`/etc` 目录包含 `passwd` 和 `group` 条目。`/lib` 目录存放 FTP 需要的共享对象库。最后，`/pub` 目录可用于放置您希望匿名用户通用的文件。

在 Red Linux 7 之前，FTP 家主目录的位置是 `/home/ftp`。由于管理员经常在组计算机之间共享 `/home` 目录，以便从不同的计算机访问他们的文件，因此以这种方式共享 FTP 家主目录并没有用。现在的 FTP 家主目录是 `/var/ftp`。您的 Web 服务器主目录（`www` 目录）也移动到了 `/var`。

`message` — 这表示当用户登录 FTP 时，应显示 `/welcome.msg` 文件中包含的消息。类似的行表示，当用户进入包含此类文件的目录时，将显示该 `.message` 文件。默认情况下，这些文件都不存在。

`/welcome.msg` 文件相对于 FTP 用户登录时的根目录。访客用户作为匿名用户，默认其根目录为 `/var/ftp`。因此，`welcome.msg` 文件必须被存放在 `/var/ftp` 中。

`compress yes all` — 这允许对 FTP 站的所有用户启用文件压缩。`compress` 命令是 UNIX 系统中使用的标准压缩命令（尽管在 Linux 等自由操作系统中更频繁地使用 `gzip`）。用于执行压缩的 `compress` 命令行定义在 `/etc/ftpconversions` 中。（由 `compress` 存储的文件具有 `.z` 后缀）。

`tar yes all` — 这允许 FTP 站的所有用户启用 `tar` 压缩。`tar` 命令是创建多个文件的标准 UNIX 命令。用于压缩的 `tar` 命令定义在 `/etc/ftpconversions` 中。（由 `tar` 存储的文件具有 `.tar.gz` 或 `.tar.Z` 后缀）。

`chmod no guest, anonymous` — 这防止访客和匿名用户名更改任何文件或目录的权限。

`delete no guest, anonymous` — 这防止访客和匿名用户删除文件或目录。

`overwrite no guest, anonymous` — 这防止访客和匿名用户覆盖文件或目录。

`rename no guest, anonymous` — 这防止访客和匿名用户重命名任何文件或目录。

`log transfers anonymous, real inbound, outbound` — 这记录匿名用户以及真实用户（即在 Linux 系统上拥有自己用户账户的用户）的文件传输。上传（入站）和下载（出站）传输都会被记录。

`shutdown/etc/shutmsg` — 这检查 `/etc/shutmsg` 文件以查看服务器需要关闭。如果是，你的服务器将向 FTP 用户发送消息，警告他们服务器即将关闭。它还会在关机前的指定时间拒绝新的 FTP 连接并断开用户。（默认情况下，`/etc/shutmsg` 文件不存在）。请参阅本章中关于设置 FTP 关机的部分，获取有关如何设置计划的 FTP 关机的信息。

`passwd-check rfc822 warn` — 这检查匿名登录的密码是否符合 rfc822 标准的地址。也就是说，FTP 服务器要求使用任何有效的 电子邮件地址作为匿名登录的密码。如果地址不符合标准（即不是 `user@host.domain` 格式），服务器将“警告”用户但仍然允许用户登录。

### FTP 根目录

对于以匿名用户登录的用户，`/var/ftp` 目录被分配为用户的根目录。也就是说，匿名用户不能 `cd` 到 `/var/ftp` 目录以上（甚至不知道 `/var/ftp` 目录结构之外存在哪些文件）。

`/var/ftp` 目录内包含了使 FTP 正常工作所需的目录和文件，而无需您访问文件系统中的其他文件。`/bin` 目录包含 FTP 可能需要的执行命令（如 `compress`、`ls` 和 `gzip`）。`/etc` 目录包含 `passwd` 和 `group` 条目。`/lib` 目录存放 FTP 需要的共享对象库。最后，`/pub` 目录可用于放置您希望匿名用户通用的文件。

在 Red Linux 7 之前，FTP 家主目录的位置是 `/home/ftp`。由于管理员经常在组计算机之间共享 `/home` 目录，以便从不同的计算机访问他们的文件，因此以这种方式共享 FTP 家主目录并没有用。现在的 FTP 家主目录是 `/var/ftp`。您的 Web 服务器主目录（`www` 目录）也移动到了 `/var`。

## 创建 FTP 用户

可以使用您服务器 FTP 服务的不同类型用户包括匿名用户、已添加到您的计算机（`/etc/passwd`）的任何用户以及您设置的任何特殊访客账户。以下章节描述了这些类型的用户以及如何设置它们。

## 匿名 FTP 用户

由于大多数从互联网访问您 FTP 站的人没有您计算机的个人登录账户，因此公共 FTP 站点使用匿名用户。通过匿名用户名，任何可以从网络访问 FTP 站的人都可以登录服务器并获得其使用的最小权限。通常情况下，最小权限意味着匿名用户只能向 FTP 服务器复制文件（而不能写入文件），并且只有选定的目录对匿名用户可见。

以下是一个匿名用户登录会话的示例：

```
$ ftp maple

Connected to maple.

220 maple.trees FTP server (Version wu-2.6.1(1) Mon Dec 25 09:21:53

EDI 2000 ready.

Name (pinksmile): anonymous

31 Guest login ok, send your complete e-mail address as password.

Password: *************

230 Guest login ok, access restrictions apply.

Remote system type is UNIX.

Using binary mode to transfer files.
```

```
ftp>
ft> bye

You have transferred 0 bytes in 0 files.

Total traffic for this session was 313 bytes in 0 transfers.

Thank you for using the FTP service on maple.trees.

Goodbye.
```

连接到服务器后，我在登录提示处输入了 `anonymous`。服务器说 `anonymous` 可以，并输入我的电子邮件地址作为密码（密码不会显示；我用星号来表示密码）。服务器接受密码为有效。如果地址不符合标准，服务器将“警告”用户但仍然允许用户登录。在 Red Linux 系统中，访客用户被限制在 `/var/ftp` 目录。在结束会话时，我通过输入 `bye` 结束了会话。

### 真实用户

拥有独立账户的用户可以登录访问 FTP 服务。他们拥有比匿名用户更多的权限。

### 访客用户

访客用户介于真实用户和匿名用户之间。这种方法允许特定用户在文件系统的特定区域添加文件，但不允许执行其他操作。

创建访客用户主目录所需的目录，以确保 FTP 正常工作所需的所有内容。为了这一点，我以 root 用户身份将 `/home/ftp` 目录结构中的所有内容复制到我的访客用户主目录（`/home/mike`）。之后，我将 `/home/mike/pub` 的组分配改为 mike：

```
cp -r /var/ftp/* /home/mike

chgrp mike /home/mike/pub
```
