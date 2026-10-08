

## 配置文件被划分为模块，每个模块都有各自的选项

模块是导出树（一个目录及其子目录）的符号表示。模块名称用方括号括起来，例如，**[ftp]** 代表一个 FTP 模块。然后，你可以为该模块输入选项，例如，使用 `path` 选项指定 FTP 站点目录和文件的位置。可以使用 `uid` 和 `gid` 选项指定用户和组 ID。默认值是 `nobody`。下面展示了一个用于匿名访问的 FTP 模块示例：

```text
[ftp]
    path = /var/ftp/pub
    comment = ftp site
```

对于更受限的访问，你可以添加一个 `auth users` 选项来指定授权用户；默认情况下，rsync 允许所有用户进行匿名访问。使用 `hosts allow` 或 `hosts deny` 来控制来自特定主机的访问。可以使用机密文件进一步控制 rsync 对 FTP 站点区域访问，例如 `/etc/rsyncd.secrets`。这是一个以冒号分隔的用户名和密码列表。

```text
aleina:mypass3
larisa:yourp5
```

与受控区域相对应的模块将如下所示：

```text
[specialftp]
    path = /var/projects/special
    command = restricted access
    auth users = aleina,larisa
    secrets file = /etc/rsyncd.secrets
```

如果你在你的 FTP 服务器上并且想要查看将提供哪些模块，你可以运行 **rsync**，使用 `localhost` 选项，并且双冒号后面不跟任何内容。

```bash
$ rsync localhost::
ftp
specialftp
```

远程用户可以通过输入你的主机名和双冒号来了解你拥有哪些模块。

```bash
$ rsync ftp.mytrek.com::
```

# rsync 镜像

某些站点允许你使用 rsync 执行镜像操作。使用 rsync，你无需复制整个站点，只需复制那些已更改的文件。以下示例将 mytrek FTP 站点镜像到本地系统的 /var/ftp/mirror/mytrek 目录：

```bash
$ rsync -a --delete ftp.mytrek.com::ftp /var/ftp/mirror/mytrek
```

使用的选项如下：`-a` 选项是归档模式，其中包括其他几个选项，例如 `-r`（递归）以包含所有子目录，`-t` 以保留文件时间和日期，`-l` 以重新创建符号链接，以及 `-p` 以保留所有权限。此外，添加了 `--delete` 选项，用于删除发送方不存在的文件，从而移除过期的文件。

# 非常安全的 FTP 服务器

非常安全的 FTP 服务器（vsftpd）小巧、快速、简单且安全。它旨在避免像 ProFTPd 这样的大型 FTP 服务器应用的开销，同时保持极高的安全级别。它还可以处理非常大的工作负载，管理 FTP 站点上的高流量水平。也许它最适合许多匿名和访客用户下载相同文件的站点。从 Red Hat 9 开始，它取代了华盛顿大学 FTP 服务器，WU-FTPd。

非常安全的 FTP 服务器在设计上固有地提供了尽可能多的安全性，充分利用了 Unix 和 Linux 操作系统的特性。服务器被分为特权和非特权进程。非特权进程接收所有 FTP 请求，解释这些请求，然后通过套接字将它们发送到特权进程，特权进程随后安全地过滤所有请求。即使特权进程也不具有完整的 root 权限运行，只使用执行其任务所需的权限。此外，非常安全的 FTP 服务器使用其自己版本的目录命令（如 `ls`），而不是系统版本。

# 运行 vsftpd

非常安全的 FTP 服务器的守护进程名为 **vsftpd**。它被设计为作为独立服务器运行，可以使用 `/etc/rc.d/init.d/vsftpd` 服务器脚本启动和停止。要启动、停止和重启 **vsftpd**，你可以使用 **service** 命令。

```bash
$ service vsftpd start
```

要使服务器自动启动，你可以使用 **chkconfig** 命令和 **on** 参数将其打开，如下所示。使用 **off** 参数来禁用服务器。如果你之前启用了另一个 FTP 服务器，如 ProFTPd，请务必先禁用它。

```bash
$ chkconfig vsftpd on
```

你还可以使用 `system-config-services` 来启动和停止 **vsftpd**，或者让其自动启动。

或者，你可以实现 **vsftpd** 由 **xinetd** 运行，仅在用户发出请求时运行服务器。第 21 章详细描述了 **xinetd** 用于服务器的用途。**xinetd** 守护程序将运行位于 `/etc/xinetd.d` 目录中的名为 **vsftpd** 的 **xinetd** 脚本文件。

最初，服务器将被关闭。你可以在 **xinetd** 中使用 **chkconfig** 命令和 **on** 参数将其打开，如下所示。使用 **off** 参数来禁用服务器。

```bash
$ chkconfig vsftpd on
```

如果你进行了配置更改，请使用 **service** 命令（或 `system-config-services`）重启 **xinetd** 以重启 **vsftpd** 服务器。

```bash
# service xinetd restart
```

# 配置 vsftpd

你使用一个配置文件 `/etc/vsftpd/vsftpd.conf` 来配置 **vsftpd**。配置选项简单且保持最少化，使其灵活性不如 ProFTPd，但速度要快得多（见表 22-2）。`vsftpd.conf` 文件包含一组指令，其中选项被赋予值。选项可以是分配了 YES 或 NO 值的开关标志，接受数值的特性，或分配了字符串的特性。在 /etc/vsftpd 目录中安装了一个默认的 `vsftpd.conf` 文件。此文件列出了某些常用选项，并提供了每个选项的详细解释。未使用的选项之前带有 # 字符进行注释。选项名称非常易于理解。例如，`anon_upload_enable` 允许匿名用户上传文件，而 `anon_mkdir_write_enable` 允许匿名用户创建目录。`vsftpd.conf` 的手册页列出了所有选项，并提供了每个选项的详细解释。

**表 22-2 vsftpd.conf 配置选项**

| 选项 | 描述 |
| :-- | :-- |
| listen | 设置独立模式。 |
| listen_port | 指定独立模式的端口。 |
| anonymous_enable | 启用匿名用户访问。 |
| local_enable | 启用本地用户访问。 |
| no_anon_password | 指定匿名用户是否必须提交密码。 |
| anon_upload_enable | 启用匿名用户上传。 |
| anon_mkdir_write_enable | 允许匿名用户创建目录。 |
| anon_world_readable_only | 使上传的文件对所有用户只读。 |
| idle_session_timeout | 空闲会话的时间限制（秒）。 |
| data_connection_timeout | 失败连接的时间限制（秒）。 |
| dirmessage_enable | 显示目录消息。 |
| ftpd_banner | 显示 FTP 登录消息。 |
| xferlog_enable | 启用传输事务日志记录。 |
| xferlog_file | 指定日志文件。 |
| deny_email_enable | 启用拒绝 vsftpd.banned 中指定的电子邮件地址的匿名用户。 |
| userlist_enable | 拒绝访问 vsftpd.user_list 文件中指定的用户。 |
| userlist_file | 根据 userlist_deny 的设置拒绝或允许用户访问。 |
| userlist_deny | 当设置为 YES 时，userlist_file 列出的用户被拒绝访问。当设置为 NO 时，userlist_file 列出的用户且仅限这些用户被允许访问。 |
| chroot_list_enable | 将用户限制在其主目录中。 |
| chroot_list_file | 允许用户访问主目录。除非 chroot_local_user 设置为 YES，否则此文件包含不允许访问其主目录的用户列表。 |
| chroot_local_user | 允许所有用户访问其主目录。 |
| pam_service_name | 指定 PAM 脚本。 |
| ls_recurse_enable | 启用递归列出。 |

![图片描述](img/ab68ea377332b50bf70ef1316c8175b6_518_0.png)

> **注意** *在* `vsftpd.conf` *文件中设置选项时，* `=` *符号周围没有空格。*

# 启用独立访问

要将 `vsftpd` 作为独立服务器运行，你将 `listen` 选项设置为 `YES`。这指示 `vsftpd` 持续在其分配的端口上监听请求。你可以使用 `listen_port` 选项指定它监听的端口。

```text
listen=YES
```

# 启用登录访问

在以下示例中，取自 `vsftpd.conf` 文件，通过将 `YES` 值分配给 `anonymous_enable` 选项来启用匿名 FTP。`local_enable` 选项允许你系统上的本地用户使用 FTP 服务器。

```text
# Allow anonymous FTP?
anonymous_enable=YES
#
# Uncomment this to allow local users to log in.
local_enable=YES
```

如果你希望允许匿名用户在不提供密码的情况下登录，你可以将 `no_anon_password` 设置为 `YES`。

# 本地用户权限

各种用户权限控制本地用户如何访问服务器上的文件。如果你希望允许本地用户在其账户中创建、重命名和删除文件和目录，你必须使用 `write_enable` 选项启用写访问。这样，他们上传的任何文件，他们也可以删除。字面上，`write_enable` 选项激活了一系列更改文件系统的命令，包括创建、重命名和删除文件和目录。

```text
write_enable=YES
```

你可以使用 `local_umask` 选项进一步指定上传文件的权限（`vsftpd.conf` 中的默认设置为 022，表示所有者具有读写权限，所有其他用户只有读权限，即 644）。

```text
local_umask=022
```

虽然 ASCII 上传默认是禁用的，但你可以启用此功能。ASCII 上传涉及某些安全风险，默认情况下是关闭的。但是，如果你正在上传大型文本文件，你可能会在特殊情况下想要启用它们。使用 `ascii_upload_enable` 来允许 ASCII 上传。

# 匿名用户权限

你还可以允许匿名用户上传和删除文件，以及创建或删除目录。使用 `anon_upload_enable` 选项启用匿名用户上传。要允许匿名用户重命名或删除他们的文件，你设置 `anon_other_write_enable` 选项。要让他们也能创建目录，你设置 `anon_mkdir_write_enable` 选项。

