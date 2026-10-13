
使用 `redhat-config-services` 客户端或 `service` 命令来启动、停止或重启 vsftpd 服务器。不要在你的系统上同时运行两个 FTP 服务器！

> 提示
> 你可以使用 `/etc/rc.d/init.d` 目录下名为 `vsftpd` 的 shell 脚本来启动、停止、重启和查询 vsftpd 服务器。你必须拥有使用 vsftpd 脚本控制服务器的权限，但任何用户可以使用 `status` 关键字查询服务器（以查看其是否正在运行以及查看进程 ID 号），如下：
> `/etc/rc.d/init.d/vsftpd status`

### 配置非常安全 FTP 服务器

vsftpd 服务器虽然不如 Wu-FTPD 那么流行，但被 Red Hat, Inc. 用于其 FTP 服务器操作。（vsftpd 主页位于 http://vsftpd.beasts.org/）。该服务器提供了简单性、安全性和快速等功能。它已被许多站点使用，例如 ftp.debian.org、ftp.gnu.org、rpm-find.net 和 ftp.gimp.org。请注意，尽管名称如此，但“非常安全”FTP 服务器并没有启用使用加密的用户名或密码。

它的主配置文件是 `vsftpd.conf`，位于 `/etc/vsftpd` 目录下。服务器有许多功能和默认策略，但可以通过更改已安装的配置文件来覆盖这些设置。

默认情况下启用了匿名登录，但用户不允许上传文件、创建新目录或删除或重命名目录。Fedora 安装的配置文件允许本地用户（即具有登录和 shell 账户的用户）登录并访问其家目录。这种配置存在潜在的安全风险，因为用户名和密码在网络上是以未加密传输的。最佳策略是禁止用户从其用户账户访问服务器。

### 控制匿名访问

切换你的 FTP 服务器的匿名访问功能需要通过编辑 `vsftpd.conf` 文件并将文件中的相关条目更改为 YES 或 NO 来。控制服务器在匿名登录时如何工作的设置包括

```
anonymous_enable=默认情况下；请使用 NO 的设置，然后重启服务器以关闭匿名访问。
anon_mkdir_write=允许或禁止创建新目录。
anon_other_write=允许或禁止重命名文件和目录。
anon_upload_enable=控制匿名用户是否可以上传文件（取决于全局写入权限）。
anon_readable=仅允许用户下载。
```

在对配置文件进行任何更改后，请确保重启服务器。

### 其他 vsftpd 配置文件

你可以编辑 `vsftpd.conf` 来启用、禁用和配置许多功能，例如

```
/etc/vsftpd.user_list=由 user_list 和/或 user_deny 控制，此文件包含被禁用的用户名。
/etc/vsftpd.chroot_list=由 chroot 和/or local_user 控制，此文件包含允许或禁用的用户。
/etc/vsftpd.banned_emails—如果启用了 deny_email 设置，此文件包含被禁用的条目。
/etc/vsftpd.user_list=由 user_list 和/or user_deny 控制，此文件包含被禁用的用户名。
/var/log/vsftpd.log—如果启用了日志，此文件记录传输信息。
/var/log/vsftpd.log—传输信息
```

### 默认 vsftpd 行为

当用户进入目录时，会显示名为 `.message` 的文件内容（如果存在）。该功能在安装配置中启用，但被守护进程禁用。FTP 用户也不允许执行递归列表，这有助于减少带宽。

启用 PASV 数据方法是为了让用户知道 FTP 服务器的 IP 地址。当使用防火墙/网关进行 IP 转换或禁用传入连接时，这是一个常见问题。例如，以下是连接 FTP 服务器（运行 ProFTPD）、尝试查看目录以及产生的内部被动命令的结果：

```
$ ftp ftp.tux.org
Connected to gwyn.tux.org.
220 ProFTPD 1.2.51 Server (ProFTPD on ftp.tux.org) [gwyn.tux.org]
500 AUTH not understood.
KERBEROS_V4 rejected as an authentication type
Name (ftp.tux:gbush): blush
331 Password requested for blush.
Password:
230 User blush logged in.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> cd public_html
250 CWD command successful.
ftp> ls
500 Illegal PORT command.
ftp> bind: Address already in use
ftp>
ftp> pass
ftp> ls
227 Entering ASCII Mode (204,66,112,12,187,89).
150 Opening ASCII mode data connection for file list
--rw-r--r-- 1 blush 8470 Jan 10 2000 LinuxUnleashed.gif
--rw-r--r-- 1 blush 4407 Oct 4 2001 RHU72.ded-gif
--rw-r--r-- 1 blush 6732 May 18 2000 SuSEUnleashed.jpg
--rw-r--r-- 1 blush 6175 Jan 10 2000 TYSUSE.gif
--rw-r--r-- 1 blush 3135 Jan 10 2000 TZZones.gif
```

# 第 18 章 安全文件传输协议 (FTP) 服务

> 注意
> 访问 http://slacksite.com/other/ftp.html 可以查看有关主动模式和被动 FTP 模式的详细讨论，以及防火墙拦截服务端口对 FTP 服务器和客户端连接的影响。

如果为特定用户登录控制未设置其他默认设置，但你可以将这些控制配置给一个或多个用户。

匿名客户端访问的数据传输速率是无限的，但可以使用 `vsftpd.conf` 中的 `anon_max_rate` 设置设置最大速率（字节/秒）。这在访问高峰期间限制带宽可能非常有用。另一个默认设置是，远程客户端在空闲五分钟或数据传输停止后将被登出。你可以分别设置空闲和传输超时（挂起的连接）。

在提供 FTP 访问时，对于管理系统资源（网络带宽和内存）可能重要的设置包括：

```
list_enable=开启或关闭列表显示。
dmessage_enable=切换用户进入目录时显示消息的消息；相关设置是 ls_recurse_enable，它可用于禁止递归目录列表。
download_enable=开启或关闭下载功能。
max_clients=设置最大连接数限制。
max_per_ip=设置来自同一 IP 地址的连接数限制。
```
