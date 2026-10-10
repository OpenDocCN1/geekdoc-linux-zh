
## 配置 Very Secure FTP 服务器

尽管 vsftpd 服务器不如 wu-ftpd 流行，但 Red Hat, Inc. 仍将其用于其 FTP 服务器操作。（vsftpd 服务器的首页位于 http://vsftpd.beasts.org/。）该服务器提供诸如简单性、安全性和速度等功能。它已被多个站点使用，例如 ftp.debian.org、ftp.gnu.org、rpmfind.net 和 ftp.gimp.org。请注意，尽管名为“非常安全”的 FTP 服务器，它并不支持使用加密的用户名或密码。

其主要配置文件是 vsftpd.conf，位于 /etc/vsftpd 目录下。服务器具有多种功能和默认策略，但你可以通过修改已安装的配置文件来覆盖它们。

默认情况下，匿名登录是启用的，但不允许用户上传文件、创建新目录或删除或重命名文件。Fedora 安装的配置文件允许本地用户（即拥有登录和 shell 账户的用户）登录并访问其主目录。这种配置存在潜在的安全风险，因为用户名和密码在没有加密的情况下通过网络传输。最佳策略是拒绝用户通过其用户账户访问服务器。标准的 vsftpd 配置会禁用此功能。

## 控制匿名访问

你可以通过编辑 vsftpd.conf 文件并将文件中的相关条目更改为 YES 或 NO 来切换 FTP 服务器的匿名访问功能。控制服务器如何处理匿名登录的设置包括：

- anonymous_enable——默认启用。使用 NO 设置，然后重启服务器以关闭匿名访问。
- anon_mkdir_write_enable——允许或禁止创建新目录。
- anon_other_write_enable——允许或禁止删除或重命名文件和目录。
- anon_upload_enable——控制匿名用户是否上传文件（这也取决于全局 write_enable 设置）。这是一个潜在的安全和责任隐患，应极少使用；如果启用，请始终监控指定的上传目录。
- anon_world_readable_only——允许匿名用户仅下载具有全局可读（444）权限的文件。

在对服务器配置文件进行任何更改后，请确保重启服务器；这样做会强制 vsftpd 重新读取其设置。

## 其他 vsftpd 服务器配置文件

你可以编辑 vsftpd.conf 来启用、禁用和配置 vsftpd 服务器的许多功能和设置，例如用户访问、过滤虚假密码以及访问日志记录。某些功能可能需要创建和配置其他文件，例如：

- /etc/vsftpd.user_list——由 userlist_enable 和/或 userlist_deny 选项使用；该文件包含一个用户名列表，用于拒绝访问服务器。
- /etc/vsftpd.chroot_list——由 chroot_list_enable 和/或 chroot_local_user 选项使用，该文件包含一个用户列表，这些用户被允许或拒绝访问主目录。你可以使用 chroot_list_file 选项指定替代文件。
- /etc/vsftpd.banned_emails——这是一个匿名密码条目列表，如果启用了 deny_email_enable 设置，则用于拒绝访问。你可以使用 banned_email 选项指定替代文件。
- /var/log/vsftpd.log——如果你使用 xferlog_enable 设置启用日志记录，数据传输信息会被记录到此文件中。

> **注意**：在编辑 FTP 服务器文件之前，请先制作备份文件。此外，始终建议注释掉（在行首使用井号）被更改的内容，而不是删除或覆盖条目。在这些注释后附上一段简要说明，解释为什么进行更改。这留下了一个良好的审计轨迹，记录了什么操作、由谁执行、何时以及为何执行。如果配置出现问题，这些注释和详细信息可以帮助你进行故障排除，并在必要时恢复到有效条目。你可以使用 rpm 命令或其他 Linux 工具（如 mc）从软件的 RPM 存档中提取一份新的配置文件副本。但请注意，提取的版本会替换当前版本并覆盖你的配置更改。

## vsftpd 默认行为

当用户进入目录时，将显示名为 .message 的文件的内容（如果该文件存在于当前目录中）。此功能在已安装的配置文件中启用，但被守护进程禁用。FTP 用户也不允许执行递归目录列表，这有助于减少带宽使用。

启用了 PASV 数据连接方法，以便让外部用户了解 FTP 服务器的 IP 地址。当在防火墙/网关后使用 FTP（该网关使用 IP 伪装）或入站数据连接被禁用时，这是一个常见问题。例如，这里展示了一个连接到 FTP 服务器（运行 ProFTPd）的过程、尝试查看目录列表以及随后需要使用 ftp 的内部 passive 命令：

```bash
$ ftp ftp.tux.org
Connected to gwyn.tux.org.
220 ProFTPD 1.2.5src1 Server (ProFTPD on ftp.tux.org) [gwyn.tux.org]
500 AUTH not understood.
KERBEROS_V4 rejected as an authentication type
Name (ftp.tux.org:gbush): gbush
331 Password required for gbush.
Password:
230 User gbush logged in.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> cd public_html
250 CWD command successful.
ftp> ls
500 Illegal PORT command.
ftp: bind: Address already in use
ftp>
ftp> pass
Passive mode on.
ftp> ls
227 Entering Passive Mode (204,86,112,12,187,89).
150 Opening ASCII data connection for file list
-rw-r--r-- 1 gbush gbush 8470 Jan 10 2000 LinuxUnleashed.gif
-rw-r--r-- 1 gbush gbush 4407 Oct 4 2001 RHut72d.gif
-rw-r--r-- 1 gbush gbush 6732 May 18 2000 SuSEUnleashed.jpg
-rw-r--r-- 1 gbush gbush 6175 Jan 10 2000 TYSUSE.gif
-rw-r--r-- 1 gbush gbush 3135 Jan 10 2000 TZones.gif
```

> **注意**：访问 http://slacksite.com/other/ftp.html 以获取有关主动和被动 FTP 模式以及防火墙阻塞服务端口对 FTP 服务器和客户端连接影响的详细讨论。

另一个默认设置是未设置特定用户登录控制，但你可以配置这些控制以拒绝一个或多个用户的访问。

匿名客户端访问的数据传输速率没有限制，但你可以通过使用 vsftpd.conf 中的 anon_max_rate 设置来设置最大速率（以字节/秒为单位）。这在访问高峰期对限制带宽使用很有用。另一个默认行为是，远程客户端在闲置活动或数据传输停滞五分钟后会被注销。你可以分别设置闲置和数据传输超时（停滞连接）。

在提供 FTP 访问时，可能对管理你的系统资源（网络带宽或内存）很重要的其他设置包括以下内容：

- dirlist_enable——切换目录列表的开启或关闭。
- dirmessage_enable——切换用户进入目录时显示消息的功能。相关设置是 ls_recurse_enable，可用于禁止递归目录列表。
- download_enable——切换下载的开启或关闭。
- max_clients——设置最大连接数的限制。
- max_per_ip——设置来自相同 IP 地址的连接数限制。

## 配置 wu-ftpd 服务器

wu-ftp 使用许多配置文件来控制其操作，包括以下内容：

- ftpaccess——包含大部分服务器配置设置
- ftconversions——包含传输期间文件转换的定义
- ftphosts——保存控制特定主机用户访问的设置

这些文件可能在 RPM 安装过程中在 /etc 目录中创建，也可能由系统管理员创建。以下部分描述了这些文件及其如何使用方法中包含的命令来配置 wu-ftpd 服务器，使其可访问所有入站请求。

> **警告**：在配置匿名 FTP 服务器时，确保采取所有安全措施以防止恶意用户获得特权级访问权限至关重要。虽然本章展示了如何配置你的 FTP 服务器以进行安全使用，但所有连接到 Internet 的计算机都是潜在攻击的目标。存在漏洞的系统可能是潜在责任的来源，特别是如果有人访问并使用它们存储专有软件的非法副本——即使是暂时的。如果系统的其余部分仍然容易受到攻击，那么配置安全的 FTP 服务器就没有什么价值。使用 Red Hat 的 *lokkit* 或 *system-config-securitylevel* 客户端在你的系统上实施防火墙。

