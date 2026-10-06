
| `alert` | 表示应该立即纠正的错误，例如系统数据库损坏 |

| `emerg`, or, `panic` | 表示非常严重的系统状态，通常会广播给所有用户 |

# 管理日志文件

虽然日志文件可能包含重要信息，但它们可能会占用空间。因此，清理它们很重要。

在清理日志文件之前，最好检查权限。

你可以指定 `logrotate` 保留日志文件的数量。如果 `logrotate` 配置为只保留两个旧文件（例如 `file.1` 和 `file.2`），那么在下一个周期将删除 `file.2`。

`/etc/logrotate.conf` 文件的示例如下：

```
[root@server1 root]# cat /etc/logrotate.conf
# 详情请参 "man logrotate"
### rotate weekly
```

# 日志文件管理

## 保留 4 周的日志

`rotate 4`

## 在轮转旧文件后创建新的空日志文件

`create`

## 如果你想压缩日志文件，请取消注释

`compress`

## RPM 包将旋转信息放入此目录

`include /etc/logrotate.d`

## 没有软件包的 wtmp -- 我们在这里轮转

`/var/log/wtmp` (

   `monthly`

  `create 0664 utmp`

  `rotate 1`

)

## 系统特定的日志也可以在此配置。

在前面的输出中，任何以 `#` 字符开头的都是注释，会被忽略。其他行表示此文件以及 `/etc/logrotate.d` 中的所有其他文件都按每周进行轮转，除非另有说明。此外，保留四份旧文件（`rotate 4`）。对于 `/var/log/wtmp` 文件，这种轮转每月一次而不是每周，只保留一份旧文件，且创建的新日志文件权限为 `0664`，所有者为 `root`，组为 `utmp`。

`/etc/logrotate.conf` 文件指定了 `logrotate` 命令使用的默认参数；但日志文件的旋转信息存储在 `/etc/logrotate.d` 目录中。以 `/etc/logrotate.d/psacct` 为例：

```
[root@server1]# cat /etc/logrotate.d/psacct
### psacct RPM 的 logrotate
```

```
/var/account/pacct (
  prerate
  /usr/sbin/accton
endscript
  compress
  notifempty
  daily
  rotate 31
  create 0600 root root
)
```

# 第11章 常见管理任务

`postrotate`

`/usr/sbin/accton /var/account/pacct`

`endscript`

```
[root@server1]#
```

该文件仅显示 `/var/account/pacct` 文件应该每天轮转一次，新的日志文件由 `root` 所有，权限为 `600` (`rw-------`)，并且只有当日志文件不为空时才会进行轮转。日志文件在轮转后会被压缩，最多可以保留 `31` 份旧日志文件。此外，在每次轮转之前会运行 `/usr/sbin/accton /var/account/pacct` 程序，在轮转后会运行 `/usr/sbin/accton` 程序。

在 Linux 系统上，`logrotate` 工具通过 `/etc/cron.daily/logrotate` 自动调度为每天运行一次；但你也可以通过在命令行提示符中输入命令 `logrotate /etc/logrotate.conf` 来手动运行它。

随着时间的推移，`logrotate` 会生成多个日志文件副本，如下列表所示的 `/var/log` 目录：

```
[root@server1 log#] ls /var/log
acpid httpd pgsql secure
amanda iptraf ppp secure.1
boot.log lastlog prelink.log secure.2
boot.log.1 mail privoxy spooler
boot.log.2 maillog quagga spooler.1
boot.log.3 maillog radius spooler.2
canna maillog.2 routed squid
c mailman rpmkgps Thomas
cron.1 messages rpmkgps.1 uucp
cups messages. rpmkgps.2 vbox
dmesg messages.2 rpmkgps.3 wtmp
exim mysqld.log sa Xorg.0.log
fax mysqld.log.1 samba Xorg.0.logold
gdm news scrollkeeper.log Xorg.setup.log
[root@server1]#
```

根据输出结果，最近的事件记录在 `boot.log` 文件中，紧接着是 `boot.log.1` 文件，然后是 `boot.log.2` 文件，依此类推。

# 管理用户和组

在授予 BASH shell 之前，你必须使用有效的用户名和密码登录 Linux 系统。这个过程被称为身份验证，因为用户名和密码会针对包含所有用户帐户信息的系统数据库进行验证。通过验证的用户随后将获得对系统上文件、目录和其他资源的访问权限。

包含用户帐户信息的系统数据库通常由两个文件组成：`/etc/passwd` 和 `/etc/shadow`。每个用户通常在 `/etc/passwd` 中有一行描述该用户账户，在 `/etc/shadow` 中有一行包含加密密码和过期时间信息。

较旧的 Linux 系统将加密密码存储在 `/etc/passwd` 中，并且完全不使用 `/etc/shadow`。这被认为是一种很糟糕的安全，因为进程通常需要访问 `/etc/passwd` 中的用户信息。将加密密码存储在进程无法访问的独立文件中，可以防止进程获取所有用户帐户信息。请记住，当在安装期间提示你使用“影子密码（Shadow passwords）”时，如果没有选择此项，安装后将存在 `/etc/passwd` 文件。若要在安装后将系统转换为使用 `/etc/shadow` 存储加密密码，你可以运行 `pwconv` 命令。或者，可以使用 `pwunconv` 命令恢复到仅使用 `/etc/passwd` 文件的。

`/etc/passwd` 文件的每一行都具有以下冒号分隔的格式：

`name:UID:GECOS:homedirectory:shell`

预测输出中的名称指的是用户的名称。如果没有使用 `/etc/shadow`，密码字段包含该用户的加密密码；否则，它包含一个字符 `x` 作为存储在 `/etc/shadow` 中密码的占位符。

**用户标识符** (`UID`) 指定分配给每个用户的唯一 ID。通常，小于 `100` 的 UID 指的是守护进程登录系统时使用的用户帐户。`root` 用户的 UID 始终为 `0`。

**组标识符** (`GID`) 是用户的主要 ID。每个用户可以是多个组的成员，但这些组中只有一个是主组。用户的**主组**是作为该用户创建的任何文件或目录的组所有者的组。同样，当一个用户创建一个文件或目录时，该用户就会成为该文件和目录的所有者。

`GECOS` 提供了用户的文本描述，通常留空；该信息最初用于通用综合计算机操作系统（GECOS）。最后两个字段分别代表用户主目录的绝对路径和 shell。

一个 `/etc/passwd` 文件的示例：

```
[root@server1]# cat /etc/passwd
root:x:0:0:root:/bin/bash
bin:x:1:1:bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:0:sync:/sbin/sbin/sync
shutdown:x:6:0:shutdown:/sbin/sbin/shutdown
halt:x:7:0:halt:/sbin/sbin/halt
mail:x:8:12:mail:/var/spool/mail
news:x:9:13:news:/etc/news
uucp:x:10:14:uucp:/var/spool/uucp
operator:x:11:0:operator:/usr/games/root
games:x:12:100:games:/var/games
gopher:x:13:30:gopher:/var/gopher
ftp:x:14:50:ftp:/var/ftp
nobody:x:99:99:nobody::/sbin/nologin
rm:x:37:37:rm:/var/lib/rpm
vcs:x:69:69:vcs:/dev/sbin
nscd:x:28:28:nscd::/usr/sbin
sshd:x:74:74:sshd:Privilege-separated:/var/empty/sshd
ident:x:98:98:ident::/sbin/ident
rpc:x:32:32:rpc:/var/lib/
user:x:29:29:RPC Service:/var/lib/nfs
nfs:x:65534:65534:nfs::/var/lib/nfs
pcap:x:47:47:pcap:/var/spool/mail
mailfix:x:51:51:mailfix:/var/spool/mail
smmsp:x:53:53:smmsp:/var/spool/mail
annaanna:x:39:39:anna:/var/lib/apt
dump:x:34:34:dump:/var/backup
gdm:x:42:42:gdm:/var/run
http:x:23:23:http:/var/www
ntp:x:26:26:ntp:/var/lib/ntp
quagga:x:92:92:quagga:/var/run/quagga
radius:x:95:95:radius:/var/lib/radius
radvd:x:75:75:radvd:/var/run
xfs:x:81:81:xfs:/var/run
message:x:99:99:message:/var/log/message
getty:x:38:38:getty:/usr/sbin
xim:x:73:73:xim:/var/lib/xim
www:x:67:67:www:/var/lib/www-data
node:x:96:96:node:/nonexistent
```

*(注：由于原始文本中 `/etc/passwd` 示例内容似乎存在部分截断或重复，此处译文遵循原文逻辑进行对齐展示，但核心代码块不翻译)*

## 第11 章 常见管理任务

接收新密码后，你的密码将在 `99999` 天后过期，并在需要更改密码前七天收到警告。

当密码过期后，用户仍允许在一段时间内登录系统，之后该用户将被禁用登录。密码过期后用户账户被禁用的天数由 `/etc/shadow` 中的 `disable1` 字段表示。此外，你还可以在特定日期禁用用户登录，例如在雇合同结束时。`/etc/shadow` 中的 `disable2` 字段表示自 `1970` 年 `1` 月 `1` 日以来用户账户被禁用的天数。

显示 `/etc/shadow` 文件的示例：

```
[server1 root]# cat /etc/shadow
root:$!IPy5n0F69FX9nFKz.Gm6IR.R/:12617:0:999997::
bin::12617:0:999997::
demon::12617:0:999997::
adm::12617:0:999997::
lp::12617:0:999997::
sync::12617:0:999997::
shutdown::12617:0:999997::
halt::12617:0:999997::
mail::12617:0:999997::
news::12617:0:999997::
uucp::12617:0:999997::
operator::12617:0:999997::
games::12617:0:999997::
gopher::12617:0:999997::
ft::12617:0:999997::
nobody::12617:0:999997::
rm::12617:0:999997::
vcsa::12617:0:999997::
scd::12617:0:999997::
sshd::12617:0:999997::
ident::12617:0:999997::
rpc::12617:0:999997::
rpcuser::12617:0:999997::
fsnobody::12617:0:999997::
pcap::12617:0:999997::
mailn::12617:0:999997::
nsmssp::12617:0:999997::
apache::12617:0:999997::
squid::12617:0:999997::
webalizer::12617:0:999997::
dbus::12617:0:999997::
xfs::12617:0:999997::
```

密码字段通常包含一个 `x`，因为组密码很少被使用。如果使用，你需要指定一个密码来使用本章后讨论的 `newgroup` 命令更改你的组成员身份。这些密码使用 `gpasswd` 命令设置，并可以存储在 `/etc/gshadow` 文件中增加安全性。请参阅 `gpasswd` 手册或 info 页面获取更多信息。

`GID` 代表组的唯一 ID，`members` 字段表示组成员列表。接下来是一个 `/etc/group` 文件示例：

```
[root@server1]# cat /etc/group
root:x:0:root
bin:x:1:daemon
daemon:x:2:root,daemon
sys:x:3:root,daemon
adm:x:4:root,daemon
tty:x:5:
disk:x:6:root
lp:x:7:daemon,lp
mem:x:8:
kmem:x:9:
wheel:x:10:root
mail:x:12:mail,postfix
news:x:13:news
uucp:x:14:uuc,nut
man:x:15:
games:x:20:
gopher:x:30:
dip:x:40:
ftp:x:50:
lock:x:54:
nobody:x:99:
users:x:100:
rpm:x:37:
floppy:x:19:
vcsa:x:69:
utmp:x:22:
slocate:x:21:
sshd:x:74:
ident:x:98:
rpc:x:32:
rpcuser:x:29:
fsnobody:x:6534:
pcap:x:77:
mailn:x:47:
smmsp:x:1:
apache:x:48:
nsquid:x:23:
webalizer:x:67:
dbus:x:81:
xfs:x:43:
named:x:25:
tp:x:38:
gdm:x:101:
htt:x:24:
anna:x:39:
dovecot:x:97:
postdrop:x:90:
postfix:x:89:
netdump:x:34:
quavat:x:102:
agga:x:92:
radvd:x:75:
radiusd:x:95:
ldap:x:55:
mysql:x:27:
postgres:x:26:
fax:x:78:
privoxy:x:73:
tomcat:x:53:
user:x:500:
```

从前面的输出可以看出，“bin”组的 GID 为 `1`，成员为 `root`、`bin` 和 `daemon`。

## 创建账户

你可以使用 `useradd` 命令在 Linux 系统上创建账户，并指定用户名作为参数，如下所示：

在这种情况下，UID、shell 和家目录等所有信息均来自两个包含默认值的文件。第一个文件 `/etc/login.defs` 包含了设置邮件默认位置、密码过期、最小密码长度、可用的 UIDs 和 GIDs 范围以及默认创建家目录的参数。

示例 `/etc/login.defs` 文件所示：

```
[root@server1]# cat /etc/login.defs
# REQUIRED
# 邮箱所在的目录，相对于家目录的文件名。
# 如果两个都定义，MAIL_DIR 优先级更高。
# QMAIL_DIR      Maildir
MAIL_DIR       /var/spool/mail
#MAIL_FILE      .mail

# 密码有效期:
#   PASS_MAX_DAYS密码可以使用天数。
#   PASS_MIN_DAYS更改之间的最小天数。
#   PASS_MIN_LEN 可接受的密码长度。
#   PASS_WARN_AGE密码过期前的警告天数。

PASS_MAX_DAYS   99999
PASS_MIN_DAYS  0
PASS_MIN_LEN    5
PASS_WARN_AGE   7

#
# useradd 自动选择 uid 的最小/最大值
#   UID_MIN        500
#   UID_MAX        60000

#
# groupadd 自动选择 gid 的最小/最大值
#   GID_MIN        500
#   GID_MAX        60000

#
# 如果定义，在删除用户时运行此命令。
# 它应该删除被删除用户的任何 cron/打印作业（作为第一个参数）。
#
USERDEL_CMD    /usr/sbin/userdel

#
# 如果 RH 系统上 useradd 默认为用户创建家目录
# 我们这样做。此选项与 useradd 命令行的 -m 标志或。
#
CREATE_HOME      yes
```

```
[root@server1 root]#
```
