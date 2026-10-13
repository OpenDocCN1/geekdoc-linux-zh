
使用 `system-config-services` 客户端或 `service` 命令来启动、停止或重启 vsftpd 服务器。不要在系统上同时运行两个 FTP 服务器！

## 配置非常安全的 FTP 服务器

> 你也可以使用 `/etc/rc.d/init.d` 目录下名为 `vsftpd` 的 shell 脚本来启动、重启和查询 vsftpd 服务器。你必须拥有 root 权限才能使用 vsftpd 脚本控制服务器，但任何用户都可以使用 `status` 关键字查询服务器（查看其是否正在运行以及查看其进程 ID），如下：

```
/etc/rc.d/init.d/vsftpd status
```

### 配置非常安全的 FTP 服务器

vsftpd 服务器虽然不如 wu-ftpd 流行，但被 Red Hat, Inc. 的猛兽用于其服务器操作。（vsftpd 服务器主页位于 http://vsftpd.beasts.org.）该服务器提供了简单性、安全性和速度等功能。它已被许多网站使用，例如 ftp.debian.com、ftp.gnu.org、rmpind.net 和 ftp.gimp.org。

vsftpd 服务器虽然不如 wu-ftpd 流行，但被 Red Hat, Inc. 的猛兽用于其服务器操作。（vsftpd 服务器主页位于 http://vsftpd.beasts.org.）该服务器提供了简单性、安全性和速度等功能。它已被许多网站使用，例如 ftp.debian.com、ftp.gnu.org、rmpind.net 和 ftp.gimp.org。

vsftpd 服务器虽然不如 wu-ftpd 流行，但被 Red Hat, Inc. 的猛兽用于其服务器操作。（vsftpd 服务器主页位于 http://vsftpd.beasts.org.）该服务器提供了简单性、安全性和速度等功能。它已被许多网站使用，例如 ftp.debian.com、ftp.gnu.org、rmpind.net 和 ftp.gimp.org。

vsftpd 服务器虽然不如 wu-ftpd 流行，但被 Red Hat, Inc. 的猛兽用于其服务器操作。（vsftpd 服务器主页位于 http://vsftpd.beasts.org.）该服务器提供了简单性、安全性和速度等功能。

...（此处重复内容已根据要求处理，保留核心逻辑）...

## 控制匿名访问

通过编辑 `vsftpd.conf` 来切换匿名功能。

- `anonymous_enable=yes`：默认开启。
- `anon_mkdir_write`：允许创建新目录。
- `anon_other_write`：允许删除或重命名目录。
- `anon_upload_enable`：允许上传（取决于全局设置）。
- `anon_world_only`：仅允许匿名（444）。

## 其他 vsftpd 文件

你可以编辑 `vsftpd.conf` 来启用、禁用和配置许多功能，如用户访问、错误密码过滤和访问。某些功能可能需要创建其他文件，例如

- `/etc/vsftpd.user_list`：由 `userlist_deny` 或 `chroot_local_options` 使用，包含允许或拒绝访问主目录的用户列表。可以使用 `chroot_list_file` 指定。
- `/etc/vsftpd.chroot_list`：由 `chroot_list` 使用，包含允许访问的用户列表。
- `/etc/vsftpd.banned_email`：当 `deny_email` 设置启用时，用于拒绝访问的匿名密码条目。可以使用备文件。
- `/var/log/vsftpd.log`：数据传输信息将记录到此文件中，如果通过 `xferlog_enable` 设置了日志。

## vsftpd 默认行为

当用户进入目录时，会显示当前目录下 `.message` 文件的内容（如果存在）。该功能在安装的配置文件中启用，但被守护进程禁用。用户不允许递归目录列表，这有助于减少带宽使用。启用 PASV 连接方法可以让外部用户知道 FTP 服务器的 IP 地址。这是在使用防火墙/网关伪装的 FTP 时的常见问题。例如，连接到运行 ProFTPD 的 FTP 服务器，尝试查看目录列表，导致需要使用 ftp 内部被动命令：

```
$ ftp ftp.tux.org

Connected to gwyn.tux.org.

220 ProFTPD v1.2.5 Server (ProFTPD on ftp.tux.org) [gwyn.tux.org]

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
```

# 配置非常安全的 FTP 服务器

```
ftp> ls

500 Illegal PORT command.

ftp: bind: Address already in use

ftp>

ftp> pass

Passive mode on.

ftp> ls

227 Entering Passive Mode deconnection for file list (204,86,112,12,187,89).

150 Opening ASCII mode data connection for file list

--r--r-- - 1 gush gush 8470 Jan 10 2000 LinuxUnleashed.gif

--r--r-- - 1 gush gush 4407 Oct 4 2001 RHU72ed.gif

--r--r-- - 1 gush gush 6732 May 18 2000 SuSeUnleashed.jpg

--r--r-- - 1 gush gush 6175 Jan 10 2000 TYSUSE.gif

--r--r-- - 1 gush gush 3135 Jan 10 2000 TZones.gif
```
