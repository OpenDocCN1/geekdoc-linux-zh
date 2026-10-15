

| Directive | Description |
|---|---|
| AllowFilter regular-expression | 允许配置一个正则表达式，所有发送到 ProFTPD 的命令都必须匹配该表达式。 |
| AllowUser user-expression | 允许访问的用户。 |
| <Anonymous root-directory> | 创建一个匿名 FTP 登录，由匹配的 </Anonymous> 指令终止。root directory 参数是 proftpd 首先移动到的目录，然后 chroot 到该目录，以隐藏其余文件系统。 |
| Bind address | 允许将额外的 IP 地址绑定到主或 VirtualHost 配置。可以使用多个 Bind 指令来绑定多个地址。 |
| DefaultRoot directory [group-expression] | 用户登录时分配的默认根目录。group-expression 参数将 DefaultRoot 指令限制为某个组或一组组。默认值：DefaultRoot / |
| Deny ["from"] "all"/"none"/host/network [,host/network[...]] | 在给定的 <Limit> 上下文块中明确拒绝访问的主机和网络列表。all 表示拒绝所有主机访问，none 表示没有主机被明确拒绝。 |
| DenyAll | 拒绝对目录、匿名 FTP 或 Limit 块的访问。 |
| DenyFilter regular-expression | 指定一个正则表达式，该表达式不得匹配任何命令。 |
| DenyUser user-expression | 在 Limit 块内被拒绝访问的用户。 |
| <Directory pathname> | 目录特定配置。用于创建适用于指定目录及其子目录的一组指令块。 |
| DisplayLogin filename | 指定在用户登录时向用户显示的文本文件。 |
| <Global> | 全局配置块 |
| <Limit command/command-group [command2...]> | 在给定上下文中对 FTP 命令的访问限制。command-group 指 ProFTPD 文档中定义的命令分组。 |
| LsDefaultOptions "options string" | 目录列表的默认选项（如 ls 命令）。 |
| MasqueradeAddress host | 指定 FTP 服务器的公共主机名。用于由 NAT 表（包过滤）伪装的 FTP 服务器。参见第 19 章。 |
| MaxClients number/none message | 允许的最大连接客户端数。指定的消息在客户端连接被拒绝时显示。 |
| MaxLoginAttempts number | 客户端在给定连接期间尝试登录服务器的最大次数。 |
| Order allow, deny / deny, allow | 配置 <Limit> 块内 Allow 和 Deny 指令的检查顺序。默认值：Order allow,deny 上下文：<Limit> |
| PersistentPasswd on | off | 当为 on 时，proftpd 在登录期间打开系统范围的 /etc/passwd、/etc/group 文件，即使在更改根目录的 chroot 操作期间也会访问它们。 |
| ServerAdmin "admin-email-address" | 服务器或虚拟主机的管理员电子邮件地址。 |
| ServerType type-identifier | 服务器守护进程的运行模式，为 inetd 或 standalone。 |
| TimeoutIdle seconds | proftpd 允许客户端在无活动状态下保持连接的最大秒数。默认值：TimeoutIdle 600 |
| Umask octal-mask | 在给定上下文中应用于新创建的文件和目录的权限。 |
| User userid | proftpd 守护进程以其运行的用户。 |
| UserAlias login-user userid | 将客户端使用的登录名映射到服务器上的用户 ID。以 login-user 登录的客户端实际上以 user ID 登录。通常在 <Anonymous> 块内使用，以允许指定的登录名执行匿名登录。 |
| <VirtualHost address> | 适用于特定主机名或 IP 地址的配置指令。通常与在同一物理机器上运行的虚拟服务器一起使用。该块以 </VirtualHost> 指令终止。 |

## 华盛顿大学 FTP 守护进程：WU-FTPD

华盛顿大学 FTP 服务器虽然使用广泛，但在 Red Hat 9 及更高版本中已不再包含。华盛顿大学 FTP 守护进程的名称为 wu-ftpd；必须运行它才能允许远程用户通过 FTP 访问。与其他服务器一样，您可以在启动时启动 FTP 服务器，通过 xinetd 在收到请求时启动，或直接从命令行启动。默认情况下，wu-ftpd 服务器安装为使用 xinetd 运行。服务器使用 xinetd 的情况在第 20 章中有详细描述。调用 FTP 服务器的命令名称为

