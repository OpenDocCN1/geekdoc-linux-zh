
`-rw-r-- 1 root 675 2019-09-23 22:08 .profile`

每一行列出了文件权限、该家目录或目录下的文件数量、文件所有者、文件组、文件大小、创建日期和文件名。你可以看到，这里的每个文件都归 `root` 所有。`useradd` 命令将 `/etc/skel` 中的所有内容复制到新的家目录中，并将文件所有权和权限重置为新用户。

- 可能存在某些系统管理员不希望用户更改的用户；可以重置 `/home/username` 中这些文件的权限，使用户可以读取但无法写入。

- `deluser`—此命令删除用户账户（通过删除该用户的家目录及其包含的所有文件）。该命令有一个较旧版本 `userdel`，其优缺点将在稍后讨论。倾向于使用 `deluser`，因为它对要删除的内容提供了更细粒度的控制。当 `userdel` 自动删除账户和用户所有文件（例如关联的 `/home` 目录）时，`deluser` 只删除用户账户，除非你使用命令行选项告诉它执行更多操作。使用 `deluser` 时，通过这些选项你仍然可以使用 `--remove-home`、可以使用 `--remove-all-files`、可以先 `--backup` 备份用户的文件等。欲需更多信息请参阅帮助页（`man page`）。

- `passwd`—此命令更新密码管理系统使用的“身份验证令牌”。

## 提示

要锁定用户使其无法登录账户，请使用以下命令：
```
mathew@semour:-$ sudo passwd -l username
```

这会在用户的加密密码前添加一个 `!`（感叹号，也称为 bang）；反转该过程的命令使用 `-u` 选项。

- `usermod`—此命令更改多个用户属性。最常用的参数是 `-s` 更改 shell 和 `-u` 更改 UID。当用户登录或运行进程时，无法进行任何更改。

- `chsh`—此命令更改用户的默认 shell。对于 Ubuntu 而言，默认 shell 是 `/bin/bash`，称为 Bash 或 Bourne Shell。

## 添加新用户

添加用户的命令行方法非常简单，可以通过单行完成。在以下示例中，系统管理员使用 `useradd` 添加了 `heather`。（*注：原文在此处存在大量 OCR 识别重复错误，翻译已清理并保留核心逻辑*）

## 监控系统上的用户活动

监控用户活动是系统管理员职责的一部分，也是追踪系统资源使用情况的一项基本任务。`w` 命令告诉系统管理员谁登录了、登录在哪里以及正在做什么。没有人能躲过超级用户。`w` 命令后面可以跟特定的用户名，以仅显示该用户的信息。

`ac` 命令提供有关用户总连接时间的信息，以小时为单位。它访问 `/var/log/wtmp` 文件获取信息。`ac` 命令在 shell 脚本中最有用，可以生成供管理审查的操作系统使用报告。要使用 `ac` 命令，你必须从 Ubuntu 仓库安装 `ac` 软件包。

> 有趣的是，可能会发生被称为“时间扭曲”的现象，即 `wtmp` 文件中的某条目跳转到了过去，导致 `ac` 显示的用户占用时间异常。尽管这可以归因于系统时钟的一些无关因素，但系统管理员应该进行调查，因为这也可能是安全泄露的结果。

`last` 命令搜索 `/var/log/wtmp` 文件，并列出自该文件创建以来所有登录并注出的用户。`last reboot` 命令是为了让你知道自上次重启以来谁登录过。`last` 的伴侣命令是 `lastb`，它显示所有失败或无效的登录。它对于判断是合法用户遇到了问题，还是黑客正尝试访问非常有帮助。

> 你计算机上的计数系统会跟踪用户统计信息，并存储在当前的 `/var/log/wtmp` 文件。该文件由 `init` 和 `login` 进程管理。如果你想深入研究计数系统，请使用 GNU info：`info accounting`。

## 管理密码

密码是 Linux 安全不可或缺的一部分，也是用户界面可见性最高的部分。在本节中，你将学习如何为你的系统建立最小密码策略、密码存储在何处以及如何管理用户的密码。

## 系统密码策略

有效的密码策略是良好的系统管理计划的基础部分。该策略应涵盖以下内容：

- 允许和禁止的密码
- 强制更改密码的频率
- 丢失或忘记密码的检索或替换
- 此类用户的密码处理

## 密码文件

密码文件是 `/etc/passwd`，它是系统上所有用户的数据库文件。每行的格式如下：

```
username:uid:gid:gecos:homedir:shell
```

除了 `gecos` 字段外，其他字段都是自解释的。该字段用于关于用户的杂杂信息，例如用户的姓名、地点、办公室和家庭电话号码以及简短文本消息。出于安全和隐私考虑，该字段很少使用，但系统管理员应该意识到它的存在，因为 `gecos` 字段被传统的 UNIX 程序用作 `finger` 和 `mail`。因此，它使用逗号作为分隔符；你可以通过 `chfn`（更改 finger）命令更改 `gecos` 字段。

注意，`/etc/passwd` 文件中的所有字段都用冒号分隔。如果某个字段没有可用信息，则该字段为空，但冒号仍然保留。

如果密码字段中出现星号 `*`，则该用户不允许登录。为什么会有这个功能？该功能的建立是为了可以方便地禁用和（可能）恢复用户，而无需重新创建。传统的 UNIX 完成此任务的方法是让系统管理员手动编辑此文件。Ubuntu 通过本章前面提到的 `password -1` 命令提供了一种更优雅的方法。

服务作为伪用户运行，通常具有 root 权限。这些是之前提到的系统用户或逻辑用户。出于安全考虑，你不希望这些账户可供普通登录，因此为它们分配了 `/sbin/nologin` 或 `/bin/false` 作为其 shell，从而禁止这些账户登录。

`/etc/passwd` 列表显示了以下内容（为了简练进行了缩减）：

```
mathew@seymour:~ $ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:2:2:bin:/bin/sh
sys:x:3:3:sys:/dev/sh
games:x:5:60:games:/usr/bin/sh
man:x:6:12:man:/var/cache:/bin/sh
mail:x:8:8:mail:/bin/sh
news:x:9:9:news:/var/spool:/bin/sh
uucp:x:10:10:uucp:/var/spool/uucp:/bin/sh
www-data:x:33:33:www-data:/var/www:/bin/sh
gnats:x:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/bin/sh
nbody:x:65534:65534:nobody/nonexistent:/bin/sh
messagebus:x:102:106:/var/run/:bin/file
avahi:x:105:111:Avahi mDNS daemon,:,:/var/run/avahi-daemon:/bin/file
couchdb:x:106:113:CouchDB Administrator,,,:/var/lib/couchdb:/bin/bash
haldaemon:x:107:114:Hardware abstraction layer,,,:/var/run/hald:/bin/file
kernoos:x:109:65534:Kernel Ops,,:/bin/file
gdm:x:112:119:Gnome Display Manager:/var/lib/gdm/bin/bash
mathew:x:1000:1000:Matthew,,,/home/mathew/sh:/usr/sbin/sshd/nologin
sshd:x:114:65534::/var/run/:bin/file
ntp:x:115:122::/home/ntp:/bin/file
pulse:x:111:127:PulseAudio,,,/var/run/pulse:/bin/file
```

注意，某些密码字段显示密码，其他则包含 `X`。这是因为它们是影子密码（shadow passwords），是 Linux 的有用增强。

## 密码

将密码保存在 `/etc/passwd` 中被认为存在安全风险，因为任何具有读取权限的人都可以创建该程序并获取密码。为了避免这种情况，使用了影子密码，使得 `/etc/passwd` 的密码字段中只显示 `X`；真实的密码保留在 `/etc/shadow` 中，该文件只有系统管理员（以及 PAM，可插认证模块）可以读取；参见“PAM 详解”侧边栏。

必须使用传统密码和登录程序的特殊版本才能启用影子密码。影子在安装期间会自动启用。检查以下 `/etc/passwd` 伴侣 `/etc/shadow` 的缩略列表：

```
mathew@seymour:-$ sudo cat /etc/shadow
root::14547:0:99997:
daemon::14544:0:99997:
bin::14544:0:99997:
sys::14544:0:99997:
games::14544:0:99997:
man::14544:0:99997:
mail::14544:0:99997:
www-data::14544:0:99997:
circ::14544:0:99997:
body::14544:0:99997:
lib::14544:0:99997:
syslog::14544:0:99997:
messagebus::14544:0:99997:
kernoos::14544:0:99997:
gdm::14544:0:99997:
sshd::14547:0:99997:
ntp::14548:0:99997:
usbmux::14724:0:99997:
pulse::14725:0:99997:
```

字段由冒号分隔，内容为：

- 用户的登录名。
- 用户的加密密码。
- 上次更改发生的日期，以自 1970 年 1 月 1 日以来的天数计算。此日期在 UNIX 圈中被称为纪元（epoch）。只是让你知道一下，纪元以来的第十亿秒发生在 2001 年 9 月；那是 UNIX 版本的千年问题（Y2K）——和现实中的千年问题一样，什么都没有发生。
- 密码更改后可以再次更改的天数（防止更改密码后立即改回旧密码——一种危险的安全做法）。
- 必须更改密码的天数。这可以用于强制更改系统管理员已知的新发出的密码。
- 密码过期前警告用户即将过期的天数。
- 密码过期后禁用账户的天数（出于安全考虑）。
- 与密码更改日期类似，但它是自 1970 年 1 月 1 日以来账户被禁用的天数。
- 最后一个字段是“保留”字段，目前未分配任何用途。

注意，Ubuntu 默认禁用了密码过期日期和警告。这些功能在家庭系统中并不常用，通常在小型办公室也不常用。如果存在密码过期策略，则是系统管理员的责任来建立并执行。

`/etc/shadow` 文件的权限应设置为普通用户不可读不可写：权限应为 `600`。

## PAM 详解

可插认证模块（PAM）是一个处理计算机上认证任务的库系统。它使用四种管理组：账户管理、身份验证、密码管理和会话管理。这允许系统管理员选择哪些特定的应用程序验证用户。Ubuntu 已预安装并配置了所有必要的 PAM 文件。

Ubuntu 中的配置文件位于 `/etc/pam.d`。这些文件以其所控制的服务命名，格式如下：

```
type control module-path module-arguments
```

## 第 11 章 管理用户

`type` 字段对应相应的管理组。`control` 字段告诉 PAM 如果身份验证失败时该做什么。最后两项通常处理所使用的 PAM 模块及其所需的任何参数。使用 PAM 的程序通常会带有适用于 `/etc/pam.d` 目录的相应条目。为了获得更高的安全性，系统管理员可以修改默认条目。配置错误可能会导致不可预测的结果，因此在修改配置文件之前请进行备份。Ubuntu 提供的默认适用于家庭和小型办公室用户。

这里显示了一个具有前述格式化条目的 PAM 配置示例。以下是 `/etc/pam.d/gdm` 的内容：

```
#PAM-1.0
auth requisite        pam_nlogin.so
auth required        pam_env.so readenv=1
auth required        pam_env.so readenv=1 envfile=/etc/default/locale
auth sufficient      pam_success_if user group nopasswdlogin
@include common-auth
auth optional        pam_gnome_keyring.so
@include common-account
session [success=ok ignore module_unknown=ignore default=bad]
pam_selinux.so open
session required      pam_limits.so
@include common-session
session [success=ok ignore module_unknown=ignore default=bad]
pam_selinux.so close
session optional      pam_gnome_keyring.so so_auto
@include common-password
```

有趣的是，PAM 文档指出你并不真的需要（或想要）了解关于 PAM 的很多就能有效地使用它。

你可能需要 PAM 系统管理员指南。你可以在 `kernel.org/pub/linux/doc/html/Linux-PAM/Linux-PAM_SAG.html` 找到它。

## 为用户管理密码安全

选择合适的用户密码始终是一个权衡的过程。作为密码的密码（不要笑，这在现实世界中经常被使用，并导致了灾难性的后果）太容易通过简单的单词或数字组合被猜中了（例如，街道地址的数字或出生日期）。你会惊讶于有多少人能轻易地猜出如 `123456`、`ileyou`、`Qerty` 或 `abc123` 这样的密码。

相比之下，像 `2a56"F$(84u&^#Hiu44Ik%$($EJD$` 这样的密码无疑会给入侵者（或审计员）带来巨大的困难。然而，这个密码太难以记忆了，以至于密码所有可能会将密码写在贴在显示器上的便利贴上。

## 为普通用户授予系统管理员权限

系统管理员拥有控制权，通过 `/etc/shadow` 文件中的设置，但通常必须更改密码。超级用户可以使用文本编辑器或 `change` 命令来更改设置。（详情请参见 `shadow` 和 `change` 的 man 页。）

## 批量更改密码

在大型系统中，可能会出现大量用户及其密码需要进行某些处理的情况。超级用户可以使用 `chmodpass` 命令批量更改密码，该命令接受每行一个“用户名/密码”对的形式作为输入：

```
mathew@seymour:-~ sudo chmodpass username:password
```

可以通过将用户名和密码对的列表重定向到命令来批量更改密码。可以根据第 10 章“命令行大师课”中收集到的信息构建一个合适的 shell 脚本。

然而，Ubuntu 提供了提供了 `newusers` 命令从文本文件批量添加用户。该命令还允许将用户添加到组，并为用户添加新目录。

## 为普通用户授予系统管理员权限

有时，用户可能需要像 root 用户一样运行某个命令。他们通常不需要这些权力，但用户在特殊场合可能会需要——例如，临时访问某些设备或为了测试目的运行命令。

以 root 权限运行命令有两种方法。第一方法在你是超级用户账户（已启用的 root 账户）和普通用户的所有者时有用；第二方法在你不是普通用户但没有权限访问所有超级用户功能时有用。（这可能发生在具有高级和初级管理员以及普通用户的大型多用户网络中。）让我们来看每种。

## 使用 su 命令临时更改用户身份

第一个场景要求存在 root 账户，而 Ubuntu 系统默认未启用该账户。然而，有时这样做是有意义的。考虑到本章的范围，为了讨论，本节中的场景和细节假设我们正在这些特殊情况之一操作，并且已经启用 root 账户。

如果你以超级用户的身份可以访问已启用的 root 账户，但以普通用户的身份登录以执行非管理任务，并且发现需要做某些只有超级用户才能做的事情怎么办？`su` 命令可为此。

注意

一个常见的误解是认为 `su` 命令是 super user 的缩写；它实际上只是代表 substitute user（替换用户）。`su` 和 `su -` 之间有一个重要的区别。在前一种情况下，你变成了 [user] 但保留了自己的环境变量（如路径）。在后者中，你继承了该用户的环境。当你使用 `su` 变成超级用户 root 时这种差异最为明显。如果不加上 `-`，你就不会继承包含 `/bin` 或 `/sbin` 的路径变量，因此当你仅仅 `su` 到 root 时，必须始终输入命令的完整路径。

## 为普通用户授予系统管理员权限

...

root，但你保留了你的普通用户环境。这可以通过在更改前后使用 `printenv` 命令进行验证。注意工作目录（你可以执行 `pwd`）没有改变。通过执行以下命令，你变成了 root 并继承 root 的环境：

```
mathew@seymour:-~ su
```

通过执行以下命令，你变成了该用户并继承环境（记住：继承环境来自于命令中的连字符；省略它，你就会保留“旧”环境）。要变成另一个用户，请在命令行上指定不同的用户名：

```
mathew@seymour:-~ su other_user
```

离开某个身份返回你的常规身份时，请使用 `exit` 命令。例如，当作为普通用户登录时

```
mathew@seymour:-~ root
```

系统提示输入密码：

```
Password:
```

输入正确的密码后，会出现 root 用户的提示符：

```
root-#
```
