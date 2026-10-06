
在前面的输出中，任何 `#` 字符都表示注释并被忽略。其他行表示此文件中包含的日志文件以及 `/etc/logrotate.d` 目录中的所有文件（`include /etc/logrotate.d`）除非另有指定，否则每周轮转一次。此外，保留四份旧日志文件（`rotate 4`）。对于文件 `/var/log/wtmp`，轮转是每月一次而非每周，仅保留一份旧日志文件，且创建的新日志文件权限为 `"0664"`（`rw-r--`），所有者为 `"root"`，组为 `"utmp"`。

`/etc/logrotate.conf` 文件指定了 `logrotate` 命令使用的默认参数；关于日志文件的大多数轮转信息存储在 `/etc/logrotate.d` 目录中。以文件 `/etc/logrotate.d/psacct` 为例：

```bash
compress
notifempty
daily
rotate 31
create 0600 root
poststate
    /usr/sbin/accton /var/account/account
endscript
}
```

该文件仅指示 `/var/account/psacct` 文件应该被轮转，新的日志文件权限为 `"0664"`（`rw-r--`），所有者为 `"root"`，组为 `"utmp"`。在大多数 Linux 系统中，`logrotate` 实用程序通过 `/etc/shadow` 自动进行调度。随着时间的推移，`logrotate` 会生成每个文件的多个副本，如下所示：

```
[root@server1]# ls -d /var/log
acanna
amanda
boot
cron
cups
dmesg
exim
log.1
log.2
log.3
log.4
mail
messages
oldlog
pacct
secure
samba
wtmp
```

# 管理用户和组

你使用有效的用户名和密码登录 Linux 系统，在授予 Bash Shell 之前。此过程被称为身份验证，因为用户名和密码会对包含用户信息的系统数据库进行验证。通过验证的用户随后根据其用户账户访问文件、目录和其他资源。

包含信息的系统数据库通常由两个文件组成：`etc/passwd` 和 `/etc/shadow`。每个用户在 `/etc/passwd` 中有一行描述，在 `/etc/shadow` 中有一行包含加密密码和过期信息。

旧系统将加密密码存储在 `/etc/passwd` 文件中，完全不使用 `/etc/shadow` 文件。这被认为安全性较低，因为进程通常需要 `/etc/passwd` 中的用户信息。将加密密码存储在单独的文件中可以防止获取所有账户信息。记得在安装期间会提示使用“影子密码”；如果未选择此项，安装后将存在 `/etc/passwd`。要在安装后将系统转换为使用 `/etc/shadow` 文件存储加密密码，可以使用 `pwpasswd` 命令。或者，可以使用 `pwpasswd` 命令恢复到仅使用 `/etc/passwd` 文件。

`etc/passwd` 的每行具有以下列分隔格式：

`name:password:UID:GID:GECOS:homedirectory:shell`

上述输出中的名称指的是用户名。如果未使用 `/etc/shadow`，密码字段包含用户的加密密码；否则，它包含一个 `x` 字符作为 `/etc/shadow` 中密码的占位符。

用户标识符 (`UID`) 指定了分配给每个用户的唯一用户 ID。通常，小于 `100` 的 `UID` 指守护进程登录系统时使用的用户账户。`root` 用户的 `UID` 始终为零。

## 管理用户和组

组标识符 (`GID`) 是用户的主要组 ID。每个用户可以是多个组的成员，但这些组中只有一个可以作为主组。用户的主组是该用户创建的任何文件或目录的所有者所在的组。同样，当用户创建一个文件或目录时，该用户就会成为该文件或目录的所有者。

`GECOS` 代表用户的文本描述，通常留空；此信息最初用于通用电气综合操作系统 (`GECOS`)。最后最后两个字段代表用户主目录的绝对路径和 shell（外壳）路径。

下面显示了一个 `/etc/passwd` 文件的示例：

```
[server1 root]# /etc/passwd
root:x:0:0:root:/bin/bash
bin:x:1:bin:/sbin/nologin
daemon:x:2:daemon:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/lpd:/sbin/nologin
sys:x:5:0:sync:/bin/sync
shndown:x:6:0:shutdown:/sbin/shutdown
halt:x:7:0:/sbin/halt
mail:x:8:12:mail:/var/mail:/sbin/nologin
news:x:9:13:news:/etc/news
uucp:x:10:uucp:/var/uucp:/sbin/nologin
operator:x:11:0:operator:/sbin/nologin
games:x:12:100:games/user:/sbin/nologin
gopher:x:13:30:gopher:/var/gopher:/sbin/nologin
ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
body:x:99:99:Nobody:::/sbin/nologin
rm:x:37:37::/var/lib/rm:/sbin/nologin
vscsa:x:69:69:virtual console memory owner:/dev:/sbin/nologin
nscd:x:28:NSCD Daemon::/sbin/nologin
ssh:x:74:77:Privilege-separated /var/empty/sshd:/sbin/nologin
rpc:x:32:Portmapper RPC user::/sbin/nologin
rpcuser:x:29:29:RPC User:/var/nfs:/sbin/nologin
nfsnobody:x:65534:65534:Anonymous NFS User:/var/nfs:/nfs:/sbin/nologin
ncap:x:77:77::/var/archive:/sbin/nologin
mailnull:x:47:47::/var/pool/mqueue:/sbin/nologin
smsmp:x:51:51::/var/pool/mqueue:/sbin/nologin
apache:x:48:48:/var/www:/sbin/nologin
squid:x:23:23::/var/pool:/sbin/nologin
webalizer:x:67:67:Webalizer:/var/www/usage:/sbin/nologin
dbus:x:81:System message bus::/sbin/nologin
xfs:x:43:43:X Font Server:/etc/xifs:/sbin/nologin
named:x:25:25:Named:/var/named:/sbin/nologin
tp:x:38:38::/etc/ntp:/sbin/nologin
gdm:x:42:42::/gdm:/sbin/nologin
ttt:x:100:101:IIIMF Http:/usr/lib/im:/sbin/nologin
pvm:x:24:24::/user/share/pmv3:/bin/bash
canna:x:39:39:Canna Service:/var/lib/canna:/sbin/nologin
wn:x:49:49:W System Account:home/wn:/sbin/nologin
decovec:x:97:97:decotec:/usr/lib/decovec:/sbin/nologin
postfix:x:89:89::/var/postfix:/sbin/nologin
mail:x:41:41:GNU List Manager:/var/mail:/sbin/nologin
amanda:x:33:36:Amanda user:/var/amanda:/bin/bash
netnum:x:34:34:Network User:/var/crash:/bin/bash
quagga:x:92:92:Quagga routes:/var/run/quagga:/sbin/nologin
radvd:x:77:75:radvd:/usr/sbin/nologin
radius:x:95:95:radius:/usr/bin/false
ldap:x:55:LDAP User:/var/lib/ldap:/false
mysql:x:27:27:MySQL Server:/var/lib/mysql:/bin/bash
postgresql:x:26:26:PostgreSQL Server:/var/lib/postgresql:/bin/bash
fax:x:78:78:mtty:/var/spool:/sbin/nologin
ut:x:57:57:Network UFS:/var/ups:/false
privoxy:x:73::/etc/privoxy:/sbin/nologin
tomcat:x:53:53:Tomcat Server:/var/lib/tomcat:/sbin/nologin
cyrus:x:76:72:Cyrus IMAP Server:/var/lib/imap:/bin/bash
ex:x:93:93:/var/spool:/sbin/nologin
user1:x:500:500:sample user:/home/user1:/bash
```

一个 `/etc/shadow` 文件的示例如下：

```
[root@server1#]# cat /etc/shadow
root:$!iPy5h9X$LNBfOk.MyG61R.F::12617:0:999997:::
bin::*12617:0:999997:::daemon::*12617:0:999997:::
adm::*12617:0:999997:::
lp::*12617:0:999997:::
sync::*12617:0:999997:::
shutdown::*12617:0:999997:::
halt::*12617:0:999997:::
mail::*12617:0:999997:::
news::*12617:0:999997:::
uucp::*12617:0:999997:::
operator::*12617:0:999997:::
games::*12617:0:999997:::
gopher::*12617:0:999997:::
ft::*12617:0:999997:::
nobody::*12617:0:999997:::
rpm::*12617:0:999997:::
vcssa::*12617:0:999997:::
nscd::*12617:0:999997:::
ssh::*12617:0:999997:::
ident::*12617:0:999997:::
rpc::*12617:0:999997:::
rpcuser::*12617:0:999997:::
nfsnobody::*12617:0:999997:::
ncap::*12617:0:999997:::
mailnull::*12617:0:999997:::
```

492 第11章 常见管理任务

```
gdm:x:42:42::/gdm:/sbin/nologin
ttt:x:100:101:IIIMF Http:/usr/lib/im:/sbin/nologin
pvm:x:24:24::/user/share/pmv3:/bin/bash
canna:x:39:39:Canna Service:/var/lib/canna:/sbin/nologin
wn:x:49:49:W System Account:home/wn:/sbin/nologin
decovec:x:97:97:decotec:/usr/lib/decovec:/sbin/nologin
postfix:x:89:89::/var/postfix:/sbin/nologin
mail:x:41:41:GNU List Manager:/var/mail:/sbin/nologin
amanda:x:33:36:Amanda user:/var/amanda:/bin/bash
netnum:x:34:34:Network User:/var/crash:/bin/bash
quagga:x:92:92:Quagga routes:/var/run/quagga:/sbin/nologin
radvd:x:77:75:radvd:/usr/sbin/nologin
radius:x:95:95:radius:/usr/bin/false
ldap:x:55:LDAP User:/var/lib/ldap:/false
mysql:x:27:27:MySQL Server:/var/lib/mysql:/bin/bash
postgresql:x:26:26:PostgreSQL Server:/var/lib/postgresql:/bin/bash
fax:x:78:78:mtty:/var/spool:/sbin/nologin
ut:x:57:57:Network UFS:/var/ups:/false
privoxy:x:73::/etc/privoxy:/sbin/nologin
tomcat:x:53:53:Tomcat Server:/var/lib/tomcat:/sbin/nologin
cyrus:x:76:72:Cyrus IMAP Server:/var/lib/imap:/bin/bash
ex:x:93:93:/var/spool:/sbin/nologin
user1:x:500:500:sample user:/home/user1:/bash
```

管理用户和组

组标识符 (`GID`) 是用户的主要组 ID。每个用户可以是多个组的成员，但这些组中只有一个可以作为主组。用户的主组是该用户创建的任何文件或目录的所有者所在的组。同样，当用户创建一个文件或目录时，该用户就会成为该文件或目录的所有者。

`GECOS` 代表用户的文本描述，通常留空；此信息最初用于通用电气综合操作系统 (`GECOS`)。最后两个字段代表用户主目录的绝对路径和 shell 路径。

一个 `/etc/passwd` 文件的示例如下：
