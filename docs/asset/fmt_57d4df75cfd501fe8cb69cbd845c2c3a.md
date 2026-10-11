
> 注意：在类 Debian 系统上，vsftpd 配置文件直接位于 `/etc` 目录下。例如，Fedora 中 `/etc/vsftpd/ftpusers` 的等效文件在 Ubuntu 中位于 `/etc/ftpusers`。

`/etc/vsftpd/vsftpd.conf` 文件中的选项（或指令）可以根据它们扮演的角色进行分类。其中一些内容在表 17-2 中讨论。

# 434 Linux 管理：入门指南

| 选项类型 | 守护进程 | 套接字 | 安全 | 说明 | 示例 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| | | | | 这些选项控制 `vsftpd` 守护进程的行为。这些是网络和端口相关的选项。 | | 当启用时，`vsftpd` 将以独立模式运行而不是作为守护进程运行，并且 `vsftpd` 将负责监听并处理入站连接。默认值为 NO。`listen_address` 指定 `vsftpd` 监听网络客户端的 IP 地址。此选项没有默认值。`anon_max_rate` 允许匿名客户端每秒允许的最大数据传输率。默认值为 0。`listen_port` `vsftpd` 监听入站连接的端口。默认值为 21。`pasv_enable` 启用或禁用通过 PASV 方法获取连接。默认值为 YES。`anonymous_enable` 控制是否允许匿名登录。如果启用，用户名 `ftp` 和 `anonymous` 被识别为匿名登录。默认值为 YES。`tcp_wrappers` 假设 `vsftpd` 支持，入站连接将通过 `tcp_wrappers` 进行访问控制。默认值为 NO。`local_enable` 控制是否允许本地登录。如果启用，可以使用 `/etc/passwd` 中的用户账户进行登录。默认值为 YES。`user_list` 当启用此选项时，将从 `user_list` 指令指定的文件中加载用户名列表。如果用户尝试登录某个在列表中的名称，即使在提示输入密码之前也会被拒绝访问。默认值为 NO。`user_deny` 检查 `user_list` 是否激活。当为文件时，除非通过 `user_list` 设置为 NO，否则用户将被拒绝登录。默认值为 YES。这有助于防止用户使用密码访问网络。 | | 表 17-2 vsftpd 配置选项 |

# 第 17 章：FTP 435

| 类型 | 选项 | 说明 |
| --- | --- | --- |
| 文件传输 | `userlist_file` | `userlist_file`: 此选项指定了当 `userlist_enable_option` 选项激活时要加载的文件名。默认值为 `vftpd.user`。 |
| | | `cnds_allow`: 指定了允许的 FTP 命令列表。然而，登录后的命令总是被允许的（例如，允许的 PAUSE, RETR, QUIT；诸如允许的 DELIST-RETR 则被拒绝）。默认值为空。 |
| | | `download_enable`: 如果设置为 NO，所有下载请求都将被拒绝。默认值为 YES。 |
| | | `write_enable`: 此选项控制允许哪些更改文件系统的 FTP 命令。这些命令是 STOR, DELE, ENTR, RNTO, MKD 和 SIZE。 |
| | | `ch_uploads`: 此选项的作用是将匿名上传文件的所有权更改为设置中 `username` 指定的用户的所有权。默认值为 NO。 |
| | | `username`: 指定了哪个用户将拥有上传的文件的所有权。默认值为 `root`。 |
| 目录 | `use_location` | 当启用时，`vsftpd` 将显示本地时间。默认值为 GMT。 |
| | | `hide_ids`: 启用或禁用执行目录列表的能力。如果为 NO，将给出权限拒绝的错误。默认值为 NO。 |
| | | `dir_enable`: 启用或禁用目录列表。默认值为 YES。 |
| 日志 | `vftpd.log` | 指定了主要的 `vsftpd` 日志文件。默认值为空。 |
| | | `syslog_enable`: 通知软件保留所有文件传输的日志。如果启用，任何本应发送到系统日志的输出都在该 facility 下进行。 |
| | | `xcontrol` | 这些选项控制 `vsftpd` 如何以及在何处记录信息。 |

表 17-2 vsftpd 配置选项（续）

# 436 Linux 管理：启动和测试 FTP 服务器

由于 `vsftpd` 守护进程带有了一些使其开箱即用的默认设置，因此它基本上已经准备好开箱即可运行了。当然，我们需要启动该服务。一旦您学会了如何启动守护进程，本节的其余部分将引导您通过 FTP 客户端连接来测试 FTP 服务器。
让我们开始一个 FTP 会话。但首先我们要启动服务。

- 1. 启动 FTP 服务：

```
[root@server]# service vsftpd start

Starting vsftpd for vsftpd:[ OK ]
```

在运行 `systemd` 的 Linux 发行版上，可以使用 `systemctl` 命令替代启动 `vsftpd` 守护进程：

```
[root@fedora-server ~]# systemctl start vsftpd.
```

> 提示：如果发行版中没有 `service` 命令，您可以通过执行其运行脚本来控制服务。例如，您可以使用以下命令重启 `vsftpd`：
```bash
[root@server ~]#etc/init.d/vsftpd start
```

> 提示：在 Ubuntu 中通过 `apt-get` 安装软件后，ftp 守护进程会自动启动。因此，在尝试启动之前，请检查它是否已经在运行。
您可以检查 `ps -aux grep vsftpd` 的输出来确认。

- 2. 启动命令行 FTP 客户端，并作为匿名用户连接到本地 FTP 服务器：
```bash
[root@server -l]# ftp localhost

Connected to localhost (127.0.0.1).

220 (vsFTPD 2..*)

Name (localhost:root):
```

- 3. 提示时输入匿名 FTP 用户名——即输入 `ftp`：

```
Name (localhost:root): ftp

331 Please specify the password.
```

# 第 17 章：FTP

> **提示** 大多数 FTP 服务器允许匿名登录，并通常允许隐式使用用户名 "anonymous"。我们不需要使用 "ftp" 作为用户名来匿名连接到我们的示例 Fedora FTP 服务器时，而是可以使用常用的用户名 "anonymous"。

- 4. 在提示输入密码时，输入任意内容：

```
Password: <type-absolutely-anything-you-want-for-the-password>

230 Login successful.

Remote system type is UNIX.

Using binary mode to transfer files.
```

- 5. 使用 `ls` (or `dir`) FTP 命令列出 FTP 服务器上当前目录下的文件列表：

```
ftp> ls

227 Entering Passive Mode (127,0,0,1,63,225)

150 Here comes the directory listing.

drwxr-xr-x 2 0 4096 Sep 29 06:18 pub

226 Directory send OK.
```

- 6. 使用 `pwd` 命令显示我们在 FTP 服务器上的当前工作目录：

```
ftp> pwd

257 "/"
```

- 7. 使用 `cd` 命令切换到允许的匿名 FTP 目录之外的目录；尝试切换到本地系统的 `/boot` 目录：

```
ftp> cd /boot

550 Failed to change directory.
```

- 8. 使用 `bye` FTP 命令退出 FTP 服务器：

```
ftp> bye

221 Goodbye.
```

接下来我们将尝试使用本地系统账户连接到 FTP 服务器。具体而言，我们将使用在之前的章节中创建的用户名 "yyang"。现在，让我们开始一个示例的身份验证 FTP 会话吧。

> **提示** 为了执行后续步骤，你可能需要从你的 Fedora 服务器上临时禁用 SELinux。使用命令 `setenforce 0` 来禁用 SELinux。

- 1. 再次启动命令 -f `ftp` 客户端程序：
```bash
[root@fedora-server ~]# ftp localhost

Connected to localhost (127.0.0.1).

220 (vsftpd 2.0*)
```

- 2. 在提示时，输入 `yyang` 作为 FTP 用户：
```
Name (localhost:root): yyang
```
