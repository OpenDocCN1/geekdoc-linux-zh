
如果强制执行 SELinux，你需要禁用对 ftp 服务的保护以确保功能正常。请使用下文所示的 `setsebool` 命令，或按照第 30 章“系统和网络安全”中的说明使用 SELinux 配置器 `system-config-selinux`。仅指定需要禁用的 Boot，保持其他不变。

使用 `getsebool` 命令进行验证：

```
# setsebool -P ftp_is_daemon=1 allow_ftpd_full_access=1 allow_ftpd_anon_write=1
allow_ftpd_use_cifs=1 allow_ftpd_use_nfs ftp_home_dir=1 ftppd_disable_trans=1
getsebool ftp_full_access -> on
getsebool allow_ftpd_use_cifs -> on
getsebool allow_ftpd_use_nfs -> on
getsebool ftp_home_dir -> on
getsebool ftppd_disable_trans -> on
getsebool ftp_is_daemon -> on
```

红帽认证技师与工程师

## 理解 vsFTP 配置

vsFTP 的主配置文件是 `/etc/vsftd/vsftpd.conf`，其中可以定义许多指令来控制 `vsftpd` 守护进程的行为。默认的未注释指令显示如下：

```bash
# grep -v ^#/etc/vsftd/vsftpd.conf
anonymous_enable=YES
local_enable=YES
write_enable=YES
local_umask=022
dirmessage_enable=YES
xferlog_enable=YES
connect_from_port-20=YES
xferlog_std_format=YES
listen=YES
pam_service_name=vsftpd
userlist_enable=YES
tcp_wrappers=YES
```

这些以及其他关键指令列于表 24-2。

| 变量 |  |
| :--- | :--- |
| anonymous_enable | YES |
| local_enable | YES |
| write_enable | YES |
| local_umask | 022 |
| dirmessage_enable | YES |
| xferlog_enable | YES |
| connect_from_port-20 | YES |
| xferlog_std_format | YES |
| listen | YES |
| pam_service_name | vsftpd |
| userlist_enable | YES |
| tcp_wrappers | YES |

## 配置匿名访问的 vsFTP 服务器

要在 `rhel02` 等系统上配置 vsFTP 服务，以便以匿名用户身份下载和上传文件，请执行以下操作：

- 1. 执行“配置 vsFTP 服务器”小节中的第 1 到 4 。
- 2. 创建一个如 `/var/ftp/incoming` 的目录用于上传文件。系统默认使用 `/var/ftp` 下载文件。

```
# cd /var/ftp && mkdir incoming
```

3. 将该目录的所有者和组更改为 `root:ftp`：

```
# chown root:ftp incoming
```

4. 更改目录权限，允许匿名用户写入该目录：

```
# chmod 730 incoming
```

- 5. 在 `vsftp.conf` 文件中，将 `anonymous_enable`、`anon_upload_enable` 和 `chown_uploads` 指令设置为 `YES`，将 `chown_username` 指令设置为 `bin`， `anon_mask` 设置为 `077`。这些指令允许匿名用户上传文件，并自动将所有权更改为用户 `bin`，权限为 `600`。

6. （或重启）vsftpd 守护进程：

```
# service vsftpd start
Starting vsftpd:                 [ OK ]
```

这就完成了匿名用户访问 vsFTP 的设置。

## 测试功能

配置好 vsFTP 服务器后，可以使用 `ftp` 或 `lftp` 等客户端程序进行测试。`lftp` 功能强大，包含比标准 `ftp` 客户端更多的特性。此外，您可以使用浏览器，在 URL 中输入系统的 IP 地址或直接输入 `localhost` 并回车。

使用 `lftp` 的步骤是指定要访问的远程机器的主名或 IP 地址。您可以从另一个 RHEL 系统执行此命令。例如，从 `rhel02` 运行 `lftp` 进入 IP 地址为 `192.168.0.201` 的 `rhel01`，用户名为 `aghori`：

```
$ lftp 192.168.0.201 -u aghori
```

当 `lftp` 通过端口 21 连接到 `rhel01` 时，`vsftpd` 守护进程开始工作，并向请求者提供输入用户名的登录提示。它会检查 TCP Wrappers 以确认远程系统是否允许访问。然后它检查 `/etc/passwd` 文件中用户的有效性，并参考 `fupers` 和 `user_list` 文件确定该用户是否被允许。它会提示用户输入密码，并查询 `/etc/shadow` 文件进行验证。如果系统和用户都通过了验证，守护进程将与 `lftp` 建立通信会话。

要以匿名用户登录进行文件传输，请按如下方式运行 `lftp` 命令，并将 `anonymous` 作为用户名，邮箱地址作为密码：

```
# $ lftp rhel01
```

在 `lftp:~` 提示符下输入以下命令可以列出可用命令：

```
lftp:~> ?
!<shell-command          (commands)
alias [<name>] [<value]]     anon
bookmark [SUBCMD]             cache [SUBCMD]
cat [-b] -file                 cd <rdir>
chmod [OPTS] mode file...      close [-a]
[recls] [opts] [path][pattern]  debug [<level>|off] -o <file>
du [<dirs>               exit <code>|bg
get [OPTS] <rfile> -o <file> glob [OPTS] <cmd> <args>
help <cmd>                   history -w file -c|-e|cnt
jobs [-v]                     kill all|<job_no>
lcd <dir>                    lftp [OPTS] <site>
ls [<args>]                 mget [OPTS] <site>
mirror [remote] [local]      mkdir <dir>
module name [args]           more <files>
mput [OPTS] <file>          mrm <files>
mv [<file>]<file>             [re]nlist [<args>
open [OPTS] <site>           pget [OPTS] <rfile> -o <lfile>
put [OPTS] <file> -o <rfile> pwd [-p]
queue [OPTS] <cmd>          quote <cmd>
repeat delay [<command]     rm [-r] [-f] <files>
rmdir [-f] <dirs>            scache [<session_no]
set [OPTS] <var> [<val>]    site <site_cmd>
source <file>user<URL> [<pass>
version                     wait [-jobno>]
zcat <files>                 zmore <files>
```

`ls`、`put` 和 `get` 命令的工作方式与在 Linux Shell 提示符中相同。`get` 用于下载和上传单个文件，而其增强版本 `mget` 和 `mput` 用于多个文件。这些命令支持通配符和制表键补全。您可以通过在命令前加上 `!` 字符，在 Linux 命令行提示符中运行这些命令。

如需退出，请在 `lftp>` 提示符下使用 `quit` 命令。

所有文件传输活动默认记录在 `/var/log/xferlog` 文件中。
