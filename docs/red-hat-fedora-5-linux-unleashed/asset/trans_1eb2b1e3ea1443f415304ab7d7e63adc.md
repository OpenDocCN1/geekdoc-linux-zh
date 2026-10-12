

该文件显示了所有失败或异常的登录记录。它对于判断是合法用户遇到了问题还是黑客正在尝试访问非常有用。

> **注意**
>
> 计算机上的记账系统会跟踪用户使用统计信息，并保存在当前 `sar`-ing 写入文件中。该文件由 `last` 和 `login` 进程管理。如果你想要探索记账系统的详细信息，请使用 GNU info 系统：`info accounting`。

## 管理密码

密码是 Linux 安全性的一个组成部分，也是用户最容易看到的部分。在本节中，你将学习如何为你的系统建立最小密码策略，密码存储在哪里，以及如何为用户管理密码。

### 系统密码策略

有效的密码策略是良好系统管理计划的基本组成部分。策略应涵盖：

- 允许和禁止的密码
- 强制更改密码的频率
- 丢失或忘记密码的检索或替换
- 用户的密码处理方式

### 密码文件

密码文件是 `/etc/passwd`，它是系统中所有用户的数据库文件。每一行的格式如下：

`username:password:uid:gid:gecos:homeDir:shell`

除了 `gecos` 字段外，其他字段的含义都很明确。`gecos` 字段用于存储关于用户的杂项信息，例如用户的姓名、办公室位置、办公和家庭电话号码，以及可能的简短文本消息。出于安全和隐私原因，如今很少使用此字段，但系统管理员应了解其存在，因为传统 UNIX 程序（如 `finger` 和 `mail`）会使用该 `gecos` 字段。因此，它通常被称为 *finger 信息字段*。该字段中的数据将以逗号分隔；可以使用 `chfn`（更改 finger）命令修改 `gecos` 字段。

请注意，在 `/etc/passwd` 文件中，所有字段之间都用冒号分隔。如果某个字段没有可用信息，则该字段为空，但所有冒号仍保留。

如果密码字段中出现星号，则该用户将不被允许登录。为什么会有这种功能？这样可以在不需要重新创建账户的情况下，轻松禁用（并可能稍后重新启用）用户。系统管理员手动编辑此字段，这是实现此任务的传统 UNIX 方式。Fedora 通过前面提到的 `passwd -l` 命令提供了改进的功能。

若干服务以伪用户身份运行，通常具有 root 权限。这些就是前面提到的系统用户或逻辑用户。出于安全原因，你不希望这些账户可用于常规登录，因此它们的 shell 被指定为 `/sbin/nologin`，这将禁止这些“用户”进行任何登录。

列出 `/etc/passwd` 的内容如下：

```
# cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
news:x:9:13:news:/etc/news:
uucp:x:10:14:uucp:/var/spool/uucp:/sbin/nologin
operator:x:11:0:operator:/root:/sbin/nologin
games:x:12:100:games:/usr/games:/sbin/nologin
gopher:x:13:30:gopher:/var/gopher:/sbin/nologin
ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
nobody:x:99:99:Nobody:/:/sbin/nologin
dbus:x:81:81:System message bus:/:/sbin/nologin
vcsa:x:69:69:virtual console memory owner:/dev:/sbin/nologin
nscd:x:28:28:NSCD Daemon:/:/sbin/nologin
rpm:x:37:37:/:/var/lib/rpm:/sbin/nologin
haldaemon:x:68:68:HAL daemon:/:/sbin/nologin
netdump:x:34:34:Network Crash Dump user:/var/crash:/bin/bash
sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologin
rpc:x:32:32:Portmapper RPC user:/:/sbin/nologin
rpcuser:x:29:29:RPC Service User:/var/lib/nfs:/sbin/nologin
nfsnobody:x:65534:65534:Anonymous NFS User:/var/lib/nfs:/sbin/nologin
mailnull:x:47:47:/:/var/spool/mqueue:/sbin/nologin
smmsp:x:51:51:/:/var/spool/mqueue:/sbin/nologin
pcap:x:77:77:/:/var/arpwatch:/sbin/nologin
apache:x:48:48:Apache:/var/www:/sbin/nologin
xfs:x:43:43:X Font Server:/etc/X11/fs:/sbin/nologin
ntp:x:38:38:/:/etc/ntp:/sbin/nologin
gdm:x:42:42:/:/var/gdm:/sbin/nologin
named:x:25:25:Named:/var/named
dovecot:x:97:97:dovecot:/usr/libexec/dovecot:/sbin/nologin
postfix:x:89:89::/var/spool/postfix:/sbin/nologin
andrew:x:500:500:Andrew Hudson:/home/andrew:/bin/bash
```

请注意，所有密码字段均未显示密码，而是包含一个 x，因为它们是影子密码（shadow passwords），这是 Linux 的一项有用的安全增强功能，将在下一节中讨论。

### 影子密码

在 `/etc/passwd` 中保留任何密码都被视为安全风险，因为任何具有读取权限的人都可以在该文件上运行破解程序，轻松获取密码。为了避免这种风险，使用了影子密码，使得 `/etc/passwd` 的密码字段中只出现 x；真实密码保存在 `/etc/shadow` 中，这是一个只有系统管理员和 PAM（可插拔认证模块认证管理器）可读的文件（有关 PAM 的解释，请参阅“PAM 详解”边栏）。

必须使用传统密码和登录程序的特别版本来启用影子密码。在 Fedora 系统上，影子密码在操作系统安装阶段会自动启用。

让我们查看 `/etc/passwd` 的影子伴随文件，即 `/etc/shadow` 文件列表：

```
# cat /etc/shadow
root:*:13121:0:99999:7:::
daemon:*:13121:0:99999:7:::
bin:*:13121:0:99999:7:::
sys:*:13121:0:99999:7:::
sync:*:13121:0:99999:7:::
games:*:13121:0:99999:7:::
man:*:13121:0:99999:7:::
lp:*:13121:0:99999:7:::
mail:*:13121:0:99999:7:::
news:*:13121:0:99999:7:::
uucp:*:13121:0:99999:7:::
proxy:*:13121:0:99999:7:::
ww-data:*:13121:0:99999:7:::
backup:*:13121:0:99999:7:::
list:*:13121:0:99999:7:::
irc:*:13121:0:99999:7:::
gnats:*:13121:0:99999:7:::
nobody:*:13121:0:99999:7:::
dhcp:l1:13121:0:99999:7:::
syslog:l1:13121:0:99999:7:::
Klog:l1:13121:0:99999:7:::
andrew:$1$z/9LTBHLs0mT70dYK.KJL7rwB1M0s11:13121:0:99999:7:::
cupsys:l1:13121:0:99999:7:::
fetchmail:l1:13121:0:99999:7:::
messagebus:l1:13121:0:99999:7:::
hal::1:13121:0:99999:7:::
saned::1:13121:0:99999:7:::
gdm:1:13121:0:99999:7:::
lpip::1:13121:0:99999:7:::
```

字段由冒号分隔，按顺序如下：

- 用户的登录名。
- 用户的加密密码。
- 自 1970 年 1 月 1 日以来密码最后更改的天数。这个日期在 UNIX 圈子中被称为纪元（epoch）。顺便告诉你，自纪元以来的第十亿秒发生在 2001 年 9 月；那是 UNIX 版本的 Y2K 问题——当时并没有发生什么大事。
- 密码可以被更改前的天数（防止更改密码后立即改回旧密码——这是一种危险的安全做法）。
- 必须更改密码的天数。这可以设置为强制更改系统管理员已知的新发行密码。
- 密码过期前用户收到警告的天数。
- 密码过期后账户被禁用的天数（出于安全考虑）。
- 自 1970 年 1 月 1 日以来账户被禁用的天数。
- 最后一个字段是“保留”字段，目前未分配任何用途。

请注意，在 Fedora 中，密码过期日期和警告默认是禁用的。家庭系统不使用这些功能，小办公室通常也不使用。建立和强制执行密码过期策略是系统管理员的责任。

`/etc/shadow` 文件的权限应设置为普通用户不可写或不可读：权限应为 600。

### PAM 详解

可插拔认证模块（PAM）是一套处理计算机上认证任务的库。它使用四个管理组：账户管理、认证管理、密码管理和会话管理。这使得系统管理员可以选择单个应用程序如何认证用户。Fedora 已为你预装并预配置了所有必要的 PAM 文件。

Fedora 中的配置文件位于 `/etc/pam.d`。这些文件以其控制的服务命名，格式如下：

```
type control module-path module-arguments
```

type 字段是该规则对应的管理组。control 字段告诉 PAM 在认证失败时该怎么做。最后两项涉及使用的 PAM 模块及其所需的任何参数。使用 PAM 的程序通常打包带有 `/etc/pam.d` 目录的适当条目。为了实现更高的安全性，系统管理员可以修改默认条目。配置错误可能导致不可预测的结果，因此备份

