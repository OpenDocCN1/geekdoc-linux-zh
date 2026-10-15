
directory，你可以添加任意数量的文件和目录。你甚至可以将某些目录指定为上传目录，使 FTP 用户能够向你的系统传输文件。

在 pub 目录下为存放 FTP 文件而设置的每个子目录中，你应创建 README 文件和 INDEX 文件以便 FTP 用户使用。README 文件包含对该目录中文件类型的简要描述。INDEX 文件包含文件列表以及每个文件内容的描述。

## 非常安全的 FTP 服务器

非常安全的 FTP 服务器（vsftpd）小巧、快速、易用且安全。它旨在避免像 ProFTPD 这样的大型 FTP 服务器应用程序的开销，同时保持非常高的安全级别。它还可以处理非常大的工作负载，管理 FTP 站点的高流量。它或许最适合许多匿名和访客用户会下载相同文件的站点。从 Red Hat 9 开始，它取代了华盛顿大学的 FTP 服务器 WU-FTPD。

非常安全的 FTP 服务器本质上设计为提供尽可能多的安全性，充分利用 Unix 和 Linux 操作系统的特性。服务器分为特权进程和非特权进程。非特权进程接收所有 FTP 请求，解释它们然后通过套接字将它们发送给特权进程，后者再安全地过滤所有请求。即使是特权进程也不以完整的 root 权限运行，仅使用执行其任务所必需的权限。此外，非常安全的 FTP 服务器使用自己版本的目录命令如 ls，而不是系统的版本。

## 运行 vsftpd

非常安全的 FTP 服务器的守护进程名为 vsftpd。在 Red Hat 上，它现在设计为作为独立服务器运行，可以使用 /etc/rc.d/init.d/vsftpd 服务器脚本启动和停止。要启动、停止和重启 vsftpd，你可以使用 service 命令。

```
service vsftpd start
```

要使服务器自动启动，你可以使用 chkconfig 命令和 on 参数将其打开，如下所示。使用 off 参数禁用服务器。如果你之前启用了另一个 FTP 服务器如 ProFTPD，请先禁用它。

```
chkconfig vsftpd on
```

你也可以使用 redhat-config-services 来启动和停止 vsftpd，或使其自动启动。

或者，你可以实现 vsftpd 由 xinetd 运行，仅在用户发出请求时运行服务器。xinetd 用于服务器的用法在第 20 章中有详细描述。xinetd 将运行位于 /etc/xinetd.d 目录中的名为 vsftpd 的 xinetd 脚本文件。

最初，服务器将被关闭。你可以使用 chkconfig 命令和 on 参数在 xinetd 中将其打开，如下所示。使用 off 参数禁用服务器。

```
chkconfig vsftpd on
```

使用 service 命令（或 redhat-config-services）重启 xinetd，以在你进行配置更改后重启 vsftpd 服务器。

```
service xinetd restart
```

## 配置 vsftpd

你使用一个配置文件 /etc/vsftpd/vsftpd.conf 来配置 vsftpd。配置选项简单且保持最小化，使其比 ProFTPD 灵活性差，但速度快得多（参见表 21-2）。vsftpd.conf 文件包含一组指令，其中选项被赋予一个值（= 号前后没有空格）。选项可以是赋予 YES 或 NO 值的开关功能、取数值的功能，或被赋予字符串的功能。Red Hat 在 /etc/vsftpd 目录中安装了默认的 vsftpd.conf 文件。该文件列出了一些常用的选项，并为每个选项提供详细解释。未使用的选项前面用 # 字符注释掉。选项名称非常易于理解。例如，anon_upload_enable 允许匿名用户上传文件，而 anon_mkdir_write_enable 则允许匿名用户创建目录。vsftpd.conf 的 man 手册列出了所有选项，并为每个选项提供详细解释。

| Option | Description |
|---|---|
| listen | Set standalone mode |
| listen_port | Specify port for standalone mode |
| anonymous_enable | Enable anonymous user access |
| local_enable | Enable access by local users |
| no_anon_password | Specify whether anonymous users must submit a password |
| anon_upload_enable | Enable uploading by anonymous users |
| anon_mkdir_write_enable | Allow anonymous users to create directories |
| anon_world_readable_only | Make uploaded files read only to all users |
| idle_session_timeout | Time limit in seconds for idle sessions |
| data_connection_timeouts | Time limit in seconds for failed connections |
| dirmessage_enable | Display directory messages |
| ftpd_banner | Display FTP login message |
| xferlog_enable | Enable logging of transmission transactions |
| xferlog_file | Specify log file |
| deny_email_enable | Enable denying anonymous users whose e-mail addresses are specified in vsftpd.banned |
| userlist_enable | Deny access to users specified in vsftpd.user_list file |

TABLE 21-2 Configuration Options for vsftpd.conf

