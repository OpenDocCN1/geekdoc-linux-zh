
# 第6章 理解 Linux 文件权限

任何系统如果缺少了某种形式的安全措施都是不完整的。必须有一种机制来保护文件免受未经授权的查看或修改。`Linux` 系统遵循 `Unix` 的文件权限方法，允许根据每个文件和目录的一组设置，赋予单个用户和组访问文件的权限。本章将讨论如何使用 `Linux` 文件安全系统，在需要共享数据时保护数据。

## 本章内容
- 理解 `Linux` 安全性
- 解码文件权限
- 组 `Linux` 组操作

## Linux 安全性

`Linux` 安全系统的核心是用户账户。每个访问 `Linux` 系统的个人都应该被分配一个唯一的用户账户。用户对系统对象的权限取决于他们登录时使用的账户。

用户权限通过用户 `ID`（通常称为 `UID`）进行跟踪，该 `ID` 在账户创建时被分配给账户。`UID` 是一个数值，对每个用户都是唯一的。然而，你并不是使用 `UID` 登录 `Linux` 系统的。相反，你应该使用登录名。登录名是一个 8 个字符或少的字母数字字符串，用户用它来登录系统（以及关联密码）。

`Linux` 系统使用特殊文件和实用程序跟踪并管理系统上的用户账户。在我们讨论文件权限之前，需要先讨论 `Linux` 如何处理用户账户。本节描述了用户账户所需的文件和实用程序，以便你可以在处理文件权限时了解如何使用它们。

### `/etc/passwd` 文件

`Linux` 系统使用一个特殊文件将登录名映射到 `UID` 值。这个文件就是 `/etc/passwd` 文件。`/etc/passwd` 文件包含了关于用户的若干信息。以下是我的 `Linux` 系统上 `/etc/passwd` 文件的样子：

```
$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:/bin:/sbin/nologin
demon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/mail:/sbin/nologin
news:x:9:9::etc/news:
uucp:x:10:14:uucp:/var/spool/uucp
operator:x:11:0:operator:/root:/sbin/nologin
games:x:12:100:games:/usr/games:/sbin/nologin
gopher:x:13:30:gopher:/var/gopher:/sbin/nologin
ftp:x:14:50:ftp:/var/ftp:/sbin/nologin
ody:x:99:99:Nobody://sbin/nologin
vcsa:x:69:69:virtual console memory owner:/dev:/sbin/nologin
mailnull:x:44:47:/var/spool/mqueue:/sbin/nologin
smsp:x:51:51:/var/spool/mqueue:/sbin/nologin
apache:x:48:48:Apache:/var/www/:/sbin/nologin
bind:x:32:32:RpcBind:/var/lib/rpcbind:/sbin/nologin
ntp:x:38:38:/etc/ntp:/sbin/nologin
scsd:x:28:28:NSCD://sbin/nologin
tcdump:x:72:72::/usr/sbin/nologin
dbus:x:81:81:System message bus:/var/sbin/nologin
avahail:x:70:70:avahail daemon:/var/cache:/sbin/nologin
hsqld:x:96:96:/var/lib/hsqldb:/sbin/nologin
sshd:x:74:74:Privilege separated SSH:/var/empty/ssh:/sbin/nologin
prucser:x:29:29:RPC Service:/var/lib/nfs:/sbin/nologin
nfobsody:x:65:65534:Anonymous NFS User:/var/lib/nfs:/sbin/nologin
haldaem:x:68:68:halda daemon:/sbin/nologin
xfs:x:43:42:Font Server:/etc/X11/fs:/sbin/nologin
dgm:x:42:42:/var/adm:/sbin/nologin
rich:x:500:500:Rich Blum:/home/rich:/bin/bash
mama:x:501:501:Mama:/home/mama:/bin/bash
katie:x:502:502:katie:/home/katie:/bin/bash
jessica:x:503:503:Jessica:/home/jessica:/bin/bash
mysql:x:27:27:MySQL Server:/var/lib/mysql:/bin/bash
$
```

`root` 用户账户是 `Linux` 系统的管理员，始终被分配 `UID 0`。如你所见，`Linux` 系统为各种功能创建了许多用户账户，但这些账户并不是实际的用户。这些被称为系统账户。系统账户是一种特殊账户，供运行在系统上的服务使用以访问系统资源。所有以后台模式运行的服务都需要以用户账户身份登录 `Linux` 系统。

在安全性成为一个大问题之前，这些服务通常直接使用 `root` 用户账户登录。不幸的是，如果未经授权的人侵入了其中一个服务，他们将立即以 `root` 用户的身份访问系统。为了防止这种情况，几乎每一个在后台运行的服务都应该在用户账户下登录。`Linux` 将 500 以下的 `UID` 留给系统账户。
