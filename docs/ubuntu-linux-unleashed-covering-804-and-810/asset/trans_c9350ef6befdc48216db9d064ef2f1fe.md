

## 图 18.1 以太客户端可以过滤并嗅探 FTP 会话以捕获用户名和密码。

## wu-ftpd 的 inetd 配置

inetd（读作“eye-net-d”）是扩展的 Internet 服务守护进程，用于处理网络服务的传入连接。

该守护进程根据 /etc/inetd.conf 中的设置控制系统上的多个服务。

使用编辑器，将 disable = yes 行改为 disable = no。保存文件并退出编辑器。然后必须重启 inetd，因为配置文件仅在启动时解析。要以 root 启动 inetd，请执行命令 /etc/init.d/inetutils-inetd start。这会调用在任何运行级别启动或停止 inetd 守护进程时调用的同一 shell 脚本（从而启动或关闭系统）。inetd 应报告其状态为

```
# /etc/init.d/inetutils-inetd restart
Stopping internet superserver inetd:           [ OK ]
Starting internet superserver inetd:           [ OK ]
```

重启后，FTP 服务器可供所有传入请求访问。

## 启动非常安全的 FTP 服务器（vsftpd）包

你可以使用 /etc/init.d 目录下的名为 vsftp 的 shell 脚本启动、停止、重启和查询 vsftpd 服务器。你必须拥有 root 权限才能使用 vsftpd 脚本来控制服务器，但任何用户都可以使用 status 关键字查询服务器（查看其是否正在运行以及其进程 ID 号），例如：

```
$ /etc/init.d/vsftpd status
```

切勿在系统上同时运行两个 FTP 服务器！

## 配置非常安全的 FTP 服务器

该服务器提供简单性、安全性和速度。它已被多个站点使用，例如 ftp.debian.org、ftp.gnu.org、rpmfind.net 和 ftp.gimp.org。请注意，尽管其名称如此，非常安全的 FTP 服务器并不启用加密用户名或密码的使用。

其主要配置文件是 vsftpd.conf，位于 /etc 目录下。服务器具有许多功能和默认策略，但这些可以通过更改已安装的配置文件来覆盖。

默认情况下，匿名登录已启用，但用户不允许上传文件、创建新目录或删除或重命名文件。Ubuntu 安装的配置文件允许本地用户（即具有登录和 shell 账户的用户）登录然后访问其主目录。此配置存在潜在的安全风险，因为用户名和密码在网络上传输时未加密。最佳策略是禁止用户从其用户账户访问服务器。标准的 vsftpd 配置已禁用此功能。

## 控制匿名访问

通过编辑 vsftpd.conf 文件并将相关条目更改为 YES 或 NO 来切换 FTP 服务器的匿名访问功能。控制服务器对匿名登录的工作方式的设置包括：

- anonymous_enable—默认启用。使用 NO 设置，然后重启服务器以关闭匿名访问。
- anon_mkdir_write_enable—允许或禁止创建新目录。
- anon_other_write_enable—允许或禁止删除或重命名文件和目录。
- anon_upload_enable—控制匿名用户是否可以上传文件（还取决于全局 write_enable 设置）。这是一个潜在的安全和责任隐患，应很少使用；如果启用，请始终监控指定的上传目录。
- anon_world_readable_only—仅允许匿名用户下载具有世界可读（444）权限的文件。

对服务器配置文件进行任何更改后，请务必重启服务器；这会强制 vsftpd 重新读取其设置。

## 其他 vsftpd 服务器配置文件

你可以编辑 vsftpd.conf 以启用、禁用和配置 vsftpd 服务器的许多功能和设置，例如用户访问、伪密码过滤和访问日志记录。

某些功能可能需要创建和配置其他文件，例如：

- /etc/vsftpd.user_list—由 userlist_enable 和/或 userlist_deny 选项使用；该文件包含要拒绝访问服务器的用户名列表。
- /etc/vsftpd.chroot_list—由 chroot_list_enable 和/或 chroot_local_user 选项使用，该文件包含被允许或被拒绝访问主目录的用户列表。可通过使用 chroot_list_file 选项指定替代文件。
- /etc/vsftpd.banned_emails—匿名密码条目列表，如果启用了 deny_email_enable 设置则用于拒绝访问。可通过使用 banned_email_file 选项指定替代文件。
- /var/log/vsftpd.log—如果使用 xferlog_enable 设置启用了日志记录，则数据传输信息将被捕获到此文件。

### TIP

在编辑 FTP 服务器文件时，请先制作备份文件。此外，最好通过在行首使用井号注释掉所更改的内容，而不是删除或覆盖条目。随后附上简要说明，解释更改的原因。这会留下关于所做更改、由谁、何时以及为何进行更改的良好审计轨迹。如果配置出现任何问题，这些注释和详细信息可以帮助你进行故障排除，并在必要时返回有效条目。你可以使用 dpkg 命令或其他 Linux 工具（如 mc）从软件的包存档中提取配置文件的全新副本。但请注意，提取的版本将替换当前版本并覆盖你的配置更改。

## vsftpd 默认行为

如果当前目录中存在名为 .message 的文件，则其内容会在用户进入该目录时显示。此功能在已安装的配置文件中已启用，但由守护进程禁用。FTP 用户也不允许执行递归目录列表，这有助于减少带宽使用。

已启用 PASV 数据连接方法，以便外部用户了解 FTP 服务器的 IP 地址。当在防火墙/网关后面使用 FTP 并使用 IP 伪装或当传入数据连接被禁用时，这是一个常见问题，因为没有

