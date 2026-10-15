
```
quagga:x:92:92:Quagga routing suite:/var/run/quagga:/sbin/nologin

radvx:x:75:75:radvx:/usr/sbin/nologin

radius:x:95:95:radius user:/bin/false

ldap:x:55:55:LDAP User:/var/lib/ldap:/bin/false

mysql:x:27:27:MySQL Server:/var/lib/mysql:/bin/bash

postgres:x:26:26:PostgreSQL Server:/var/lib/postgresql:/bin/bash

fax:x:78:78::/var/spool/fax:/sbin/nologin

ups:x:57:57:UPS Tools:/var/lib/ups:/bin/false

privoxy:x:73:73::/etc/privoxy:/sbin/nologin

tomcat:x:53:53::/var/lib/tomcat:/sbin/nologin

cyrus:x:67:67:Cyrus IMAP Server:/var/lib/imap:/bin/bash

exim:x:93:93::/var/exim:/sbin/nologin

user:x:500:500:sample user:/home/user/bash
```

虽然每个用户必须在 `/etc/passwd` 文件中列出一个主组，但每个用户可以是多个组的成员。所有组及其成员都列在 `/etc/group` 文件中。`/etc/group` 文件具有以下冒号分隔的字段：

`name:password:GID:members`

第一个字段是组名，后面是组密码。

> 密码字段通常包含一个 `x`，因为组密码很少使用。如果你需要使用本章稍后讨论的 `newgrp` 命令更改主组身份，则需要指定密码。这些密码使用 `gpasswd` 命令设置，并可以存储在 `/etc/shadow` 文件中以增加安全性。更多信息请参阅 `gshadow` 手册或 info 页面。

# 管理用户和组 495

`GID` 代表该组的唯一组 ID，而 `members` 字段表示组成员列表。接下来是一个 `/etc/group` 文件的示例：

```
[root@server1 ~]# cat /etc/group
root:x:0:root
bin:x:1:root, bin, daemon
demon:x:2:root, bin, admin
sys:x:3:root, bin, admin
adm:x:4:root, adm, daemon
tty:x:5:
disk:x:6:root
lp:x:7:daemon, lp
mem:x:8:
kmem:x:9:
wheel:x:10:root
mail:x:12:mail, postfix, exim
news:x:13:news
uucp:x:14:uucp
man:x:15:
games:x:20:
gopher:x:30:
dip:x:40:
ftp:x:50:
lock:x:54:
nobody:x:99:
users:x:100:
rpm:x:97:
floppy:x:19:
vcsa:x:69:
utmp:x:22:
slocate:x:21:
nscd:x:28:
sshd:x:74:
ident:x:98:
rpc:x:32:
rpcuser:x:29
nfsnobody:x:65534
pcap:x:77:
mailnull:x:47
smmsp:x:51
apache:x:48
squid:x:23
webalizer:x:67
dbus:x:81
xfs:x:43:
named:x:25:
tp:x:38
gdm:x:42:
htt:x:101:
npvm:x:24:
canna:x:39:
wnn:x:49:
dovecot:x:97:
postdrop:x:90:
postfix:x:89:
mailman:x:41:
ettdump:x:34:
quaggavt:x:102:
quagga:x:92:
radvd:x:75:
radius:x:95:
ldap:x:55:
mysql:x:27:
postgresql:x:26:
fax:x:78:
nut:x:57:
privoxy:x:73:
tomcat:x:53:
exim:x:93:
user:x:500:
[root@server1 root]# _
```

从上述输出可以看出，“bin”组的 `GID` 为 1，有三个用户成员：`root`、`bin` 和 `daemon`。

## 创建用户账户

你可以使用 `useradd` 命令在 Linux 系统上创建用户账户，并将用户名作为参数，如下所示：

```
[root@server1 root]# useradd bobg
[root@server1 root]# _
```

在这种情况下，所有其他信息（如 `UID`、`shell` 和家目录位置）都取自包含用户账户创建默认值的两个文件。

第一个文件 `/etc/login.defs` 包含参数，用于设置电子邮件的默认位置、密码过期信息、最小密码长度、可用的 `UID` 和 `GID` 范围，以及指定默认创建家目录的位置。

接下来的示例展示了一个采样的 `/etc/login.defs` 文件：

```
[root@server1 root]# cat /etc/login.defs
* REQUIRED*
# 邮件邮箱所在的目录，或相对于家
# 目录的文件名。如果你同时定义了两者，则 MAIL_DIR 优先级更高。
# QMAIL_DIR 用于 Qmail
#QMAIL_DIR      Maildir
MAIL_DIR /var/spool/mail
#MAIL_FILE .mail
# 密码年龄控制：
# PASS_MAX_DAYS 密码可以使用的最大天数。
# PASS_MIN_DAYS 密码更改之间允许的最小天数。
# PASS_MIN_LEN 最小接受的密码长度。
# PASS_WARN_AGE 密码过期前的警告天数。
# PASS_MAX_DAYS 99999
# PASS_MIN_DAYS 0
# PASS_MIN_LEN 5
# PASS_WARN_AGE 7
# useradd 中自动选择 uid 的最小/最大值
# UID_MIN 500
UID_MAX 60000
# groupadd 中自动选择 gid 的最小/最大值
# GID_MIN 500
GID_MAX 60000
# 如果定义了，在删除用户时运行此命令。
# 它应该移除被删除用户（作为第一个参数传递）
# 拥有的 at/cron/打印作业等。
#$USERDEL_CMD /usr/sbin/userdel_local
# 如果 RH 系统上 useradd 默认为用户创建家目录
# 我们是这样做的。此选项与 useradd 命令行上的 -m 标志是“或”的关系。
# CREATE_HOME yes
[root@server1 root]#
```

第二个文件 `/etc/default/useradd` 包含有关默认主组、家目录位置、禁用过期账户的默认天数、账户禁用的日期、使用的 `shell` 以及骨架（skeleton）目录的信息。大多数 Linux 系统的骨架目录是 `/etc/skel`，包含要复制到新用户家目录的文件，如 `.bash_profile` 和 `.bashrc`。

要覆盖 `/etc/login.defs` 和 `/etc/default/useradd` 文件中的任何参数，可以在创建用户账户时为 `useradd` 指定选项。例如，要创建一个 `UID` 为 1002 的名为 `maryj` 的用户，可以使用 `useradd` 命令的 `-u` 选项，如下所示：

```
[server1 ~]# useradd -u 1002 maryj
[server1 ~]# _
```
