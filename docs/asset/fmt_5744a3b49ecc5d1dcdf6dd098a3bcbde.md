
| `/var/log/utmp*` | root | utmp | -rw-rw-r-- |
| `/var/log/wtmp*` | root | utmp | -rw-rw-r-- |
| `/var/log/xferlog` | root | root | -rw--- |
| `/var/run` | root | root | drwx-xr-x |
| `/var/run/*.pid` | root | root | -rw-r-r-- |
| `/var/spool/cron` | root | root | drwx--- |
| `/var/spool/cron/crontabs/root` | root | root | -rw--- |
| `/var/spool/mail` | root | mail | drwxwxr-x |
| `/var/spool/mail/*` | user | user | -rw-rw--- |
| `/var/tmp` | root | root | drwxrwxrwt |

> 上表列出的少数文件可能不适用于所有发行版。此外，一些文件可能存在于不同的目录中。使用 `find` 命令定位它们：`find / -type f -name filename -print 2> /dev/null`。

## /dev 中的文件

设备由 `/dev` 目录中的特殊文件表示，并且必须在这些文件上设置适当的文件权限。考虑 `/dev/hda*`，它代表 Linux 中的 IDE 磁盘。如果这些文件对全局可读，恶意用户将对磁盘上的所有数据拥有读权限！使用 `mount` 命令查找系统中已挂载驱动器关联的 `/dev` 文件。

此外，确保其他设备文件设置了适当的权限，例如 `/dev/console`、`/dev/tty/*`、`/dev/pty/*`、`/dev/audio` 和 `/dev/dsp*`。

## 磁盘分区

恶意用户可能通过消耗所有可用磁盘空间发起拒绝服务攻击。考虑以下命令：

```
[bash]$ cat /dev/zero > /tmp/zero ^C
```

上述命令将创建一个新文件 `/tmp/zero`。除非用户按 CTRL-C 中断命令，否则该文件的尺寸将持续增加。`/dev/zero` 是一个特殊的、无穷无尽的文件，其中包含零值。如果让上述命令运行一段时间，恶意用户可能会耗尽磁盘上的所有空间。由于许多正在运行的程序需要并依赖于可用的磁盘空间才能正常运行，这可能会导致不良后果。

建议将以下目录挂载到独立的分区中：

- `/boot`
- `/home`
- `/tmp`
- `/var`

此外，在挂载 `/var` 和 `/tmp` 分区时，请考虑使用 `nodev`、`nosuid` 和 `noexec` 选项。

## setuid 和 setgid 文件

检查那些设置了 setuid 和 setgid 位的文件，因为此类文件会以所有者的权限执行。由 root 或 wheel 拥有的 setuid 和 setgid 文件中的漏洞可能导致获得 root 权限。如果可能，请考虑从文件中移除 setuid 和 setgid 位。

要查找 setuid 文件，请运行

```
find / -perm -4000 -type f -print 2> /dev/null
```

要查找 setgid 文件，请运行

```
find / -perm -2000 -type f -print 2> /dev/null
```

## 实施 wheel 组

使用 wheel 组来限制对 `su` 等 setuid 程序的访问。如果该组不存在，请使用 `groupadd` 命令创建它。更改 `su` 的权限，使得只有 wheel 组中的用户才能执行它：

```
chgrp wheel `which su`
chmod u+s,o-rwx,u+rwx,g+rx `which su`
```

## SUDO

`Sudo` 是一个免费工具，允许授权用户使用 root 权限执行命令。如果多人需要执行特权操作，设置 `Sudo` 来提供特定权限是个好主意。这比共享 root 密码要好得多。`Sudo` 通常包含在大多数发行版中，但也可以在 `http://www.sudo.ws/sudo/` 获取。关于如何设置和配置 `Sudo` 的说明和示例，请参阅 `http://www.onlamp.com/pub/a/bsd/2002/08/29/Big_Scare_Daemons.html`。

### 总结

理解并强制执行正确的文件权限至关重要。除了由 `bin` 和 `sys` 等系统账户拥有的文件外，还必须定期审计对所有人可读和可写的文件。`umask` 值应设置为尽可能严格。重要的配置文件也必须经过审计，以确保权限正确。必须为 `/tmp` 和 `/var` 等目录创建磁盘分区，以防范拒绝服务攻击。在可能的情况下，应使用 wheel 组来限制对 setuid 程序等可执行文件的访问。使用 `Sudo` 允许用户以超级用户权限执行文件也是个好主意。这比共享 root 密码要好得多。

# 第 9 章

# 日志记录与补丁

本章内容：

- 日志记录
- 补丁
- 总结

本章描述了系统事件日志记录的最常见方法；接下来的部分涵盖了具体的日志文件及其包含的信息。每个系统管理员理解不同事件及其记录位置都很重要。没有这些信息，系统管理员将无法得知主机上正在发生哪些事件和活动。

除了日志记录，另一个重要问题是软件更新。每天都会公布软件漏洞及其利用代码。通常，这些漏洞由软件供应商以补丁或软件更新的形式进行修复。本章提供了获取此类软件补丁的资源。

## 日志记录

本节描述了具体的日志文件及其包含的信息。此外，还讨论了 `/var` 上的磁盘空间和日志轮转等问题。作为管理员，请务必理解本节中呈现的信息，以便检测异常的系统活动和行为。

### 日志文件

以下是一些常见的日志文件以及通常记录到其中的信息。定期浏览这些文件是个好主意。

> 根据你的 Unix 或 Linux 发行版，某些日志文件可能位于不同的目录中。如果你找不到这些文件，请使用 `find` 命令定位它们：`find /var -name filename -print 2> /dev/null`。

#### /var/audit

大多数 Solaris 发行版都附带了 BSM（Basic Security Module，基本安全模块），这是一个记录用户操作详情的实用程序。由于 BSM 在系统调用级别进行审计，可能会生成巨大的日志文件。

要启用 BSM，请切换到 runlevel 1：

```
init 1
```

接下来，运行 `bsmonv`：

```
cd /etc/security ; ./bsmonv
```

配置 `/etc/security/audit_control` 以选择要记录的事件。请参阅 `http://www.securityfocus.com/infocus/1362` 获取详细说明。更改配置后需要重启才能生效。

#### /var/adm/loginlog

在五次未成功的登录尝试后，后续的所有尝试都会记录到此文件中。每个日志事件包含登录名、tty 信息和时间。仅当此文件存在时才会记录到该文件。因此，如果该文件不存在，请使用 `touch` 命令创建它。确保此文件仅 root 可读。

#### /var/adm/sulog

`su` 命令用于登录到另一个用户的账户。例如，用户 `joe` 可能会使用 `su` 登录到 `jack` 的账户：

```
[joe's_bash]$ su - jack
Password: jackspassword
[jack's_bash]$
```

类似地，用户也可以使用 `su` 命令以 root 身份登录：

```
[joe's_bash]$ su -
Password: rootpassword
[root's_bash]#
```

记录所有 `su` 尝试非常重要。这样做有助于检测恶意本地用户的暴力破解密码猜测尝试。编辑 `/etc/default/su` 并确保 `SULLOG` 的值指向 `/var/adm/sulog`。你也可以通过将 `SYSLOG` 的值设置为 `yes` 来启用 `syslogd` 日志记录。

#### /var/log/cron

`cron` 守护进程将此文件记录信息。编辑 `/etc/syslog.conf` 并确保存在以下行：

```
cron.*    /var/log/cron
```

#### /var/log/maillog

此文件包含主机邮件服务器记录的信息。关于发出和接收电子邮件的详细信息以及相应的错误消息都会记录到该文件。编辑 `/etc/syslog.conf` 并确保存在以下行：

```
mail.*    /var/log/maillog
```

#### /var/log/messages

此文件包含由 `syslogd` 记录的信息性消息。要启用记录到该文件，`/etc/syslog.conf` 中必须存在类似下面的行：

```
*.info;mail.none;authpriv.none;cron.none /var/log/messages
```

#### /var/log/secure
