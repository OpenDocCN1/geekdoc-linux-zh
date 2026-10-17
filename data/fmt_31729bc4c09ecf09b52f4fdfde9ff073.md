
从前面的输出可以看出，“bin”组的 GID 为 1，有三个用户成员：root、bin、daemon。同样，`wheel`组的 GID 为 10，用户为成员。

> 注意
> `wheel`组是一个特殊组，为其成员提供了运行`su`和`sudo`命令的能力；因此，在 Linux 安装期间创建的第一个用户会被添加到`wheel`组，以便使用`sudo`命令设置 root 密码。包括 Ubuntu 在某些 Linux 发行版使用`sudo`组代替`wheel`组。
> 你还可以使用`getent`命令查看系统数据库（etc/passwd、/etc/shadow、/etc/group和/etc/gshadow）中的条目；例如，`getent shadow`将显示影子数据库（etc/shadow）中的条目。

## 创建用户账户

你可以使用`useradd`命令在 Linux 系统上创建用户账户，并将用户名作为参数，如下：

```
[root@server1 ~]# useradd bobg

[root@server1 ~]#
```

在这种情况下，其他信息（如 UID、shell 和家目录位置）从两个包含账户创建默认值的文件中获取。第一个文件`/etc/login.defs`包含了设置默认邮件位置、密码过期信息、密码长度以及允许使用的 UID/GID 范围的参数。此外，它还决定了创建用户时是否会自动创建家目录，以及用于在`/etc/shadow`中存储密码的密码哈希算法。
`/etc/login.defs`的示例所示：

```
# QMAIL_DIR 用于 Qmail
#
# QMAIL_DIR 邮件池目录
MAIL_DIR /var/spool/mail
#MAIL_FILE .mail

# 密码有效期控制：
#
# PASS_MAX_DAYS 密码使用的最大天数。
# PASS_MIN_DAYS 更改之间允许的最小天数。
# PASS_MIN_LEN 密码最小接受长度。
# PASS_WARN_AGE 密码过期前的警告天数。

PASS_MAX_DAYS 99999
PASS_MIN_DAYS 0
PASS_MIN_LEN 5
PASS_WARN_AGE 7

#
# useradd 中自动选择 uid 的最小/最大值
#
UID_MIN 1000
UID_MAX 60000
# 系统账户
SYS_UID_MIN 201
SYS_UID_MAX 999

#
# groupadd 中自动选择 gid 的最小/最大值
#
GID_MIN 100
GID_MAX 60000
# 系统账户
SYS_GID_MIN 201
SYS_GID_MAX 999

# 如果定义了，在删除用户时将运行此命令。
# 它应该删除由被删除用户（作为第一个参数传递）拥有的
#任何 at/cron/打印任务等
# USERDEL_CMD /usr/sbin/userdel_local

# useradd 是否应该默认为用户创建主目录
# 在 RH 系统上，是这样的。此选项可以通过 useradd 命令行上的 -m 标志覆盖。

CREATE_HOME yes

# 权限掩码初始化为此值。如果未指定，
# 权限掩码将初始化为 022。
UMASK 077

# 这允许 userdel 在没有成员存在时删除用户组。
USERGROUPS_ENAB yes

# 使用 SHA512 加密密码。
ENCRYPT_METHOD SHA512
```

第二个文件`/etc/default/useradd`包含有关默认主组、主目录位置、带有密码的账户禁用的默认天数、禁用用户账户的日期、使用的 shell 以及使用的骨架目录（在 Linux 系统上为`/etc/skel`）的信息。它包含复制到新用户主目录的文件。这些文件中大多数是环境文件，例如`.bash_profile`和`.bashrc`。

示例的`/etc/default/useradd`文件如面输出所示：

```bash
[root@server1 ~]# cat /etc/default/useradd

# useradd defaults file

GROUP=100

HOME=

INACTIVE=-1

EXPIRE=

SHELL=/bin/bash

SKEL=/etc/skel

CREATE_MAIL_SPOOL=yes
```

## 第 10 章 常见管理任务

要覆盖`/etc/login.defs`和`/etc/default`文件中对用户的任何默认参数，您可以在创建用户账户时为`useradd`命令指定选项。例如，要创建一个 UID 为 762 的用户 maryj，你可以对`useradd`命令使用`-u`选项，如下例所示：

```bash
[root@server1 ~]# useradd -u 762 maryj
```

表 10-6 出了出了`useradd`命令可用的某些常用选项及其描述。

### 表 10-6 useradd 命令的常用选项

| 选项 | 描述 |
|---|---|
| -c "description" | 为`/etc/passwd`中的 GECO 字段为用户添加描述 |
| -d homedirectory | 指定用户主目录的绝对路径 |
| -e expiredate | 指定禁用该账户登录的日期 |
| -f days | 指定密码过期的用户账户被禁用前的天数 |
| -g group | 指定用户账户的主组；在大多数 Linux 发行版中，会创建一个同名的组，并通过`/etc/login.defs`文件中的`USERGROUPS_ENABLE`条目将其设为用户的主组 |
| -G group1,group2,etc. | 指定用户账户的所有组成员身份 |
| -m | 指定为用户账户创建主目录；在大多数 Linux 发行版中，通过`/etc/login.defs`中的`CREATE_HOME`条目默认为所有用户创建主目录 |
| -k directory | 指定在复制文件到新主目录时使用的骨架目录 |
| -s shell | 指定用于用户账户的 shell 的绝对路径 |
| -u UID | 指定用户账户的 UID |

在添加用户账户后，`/etc/shadow`文件中的密码字段包含两个字符或一个星号`*`，表示未为该用户账户设置密码。要设置密码，请输入`passwd`命令，在命令行提示符输入新用户账户的名称，然后提供密码。

表 10-7 显示了用于`usermod`命令修改用户账户的选项完整列表。

### 表 10-7 usermod 命令的常用选项

| 选项 | 描述 |
|---|---|
| -c "description" | 为`/etc/passwd`中的 GECO 字段为用户添加描述 |
| -d homedirectory | 指定用户主目录的绝对路径 |
| -e expiredate | 指定禁用该账户登录的日期 |
| -f days | 指定密码过期的用户账户被禁用前的天数 |
| -g group | 指定用户账户的主组 |
| -G group1,group2,etc. | 指定用户账户的所有组成员身份 |
| -l | 锁定用户账户 |
| -U | 解锁用户账户 |
| -s shell | 指定用于用户账户的 shell 的绝对路径 |
| -u UID | 指定用户账户的 UID |

要删除用户账户，您使用`userdel`命令并指定用户名作为参数。这将从`/etc/passwd`和`/etc/shadow`文件中删除对应用户账户的条目。此外，您可以指定`-r`选项来删除用户的主目录及其所有内容。

当用户账户被删除时，以前由该用户拥有的文件变为代表该用户 UID 的数字所有。任何未来具有相同 UID 的账户将成为这些文件的所有者。

```bash
[root@server1 ~]# userdel -r bobg
```

## 第 10 章 常见管理任务

```
-rw-r--r-- 1 1002 1002 124 Jul 17 15:37 .bashrc

-rw-r--r-- 1 1002 1002 5542 Jul 17 15:37 .canna

-rw-r--r-- 1 1002 1002 820 Jul 17 15:37 .emacs

-rw-r--r-- 1 1002 1002 118 Jul 17 15:37 .gtkrc

-rw-r--r-- 3 1002 1002 4096 Jul 17 15:37 .kde

drwxr-xr-x 2 1002 1002 4096 Jul 17 15:37 .xacs

-rw-r--r-- 1 1002 1002 3511 Jul 17 15:37 .zshrc

[root@server1 ~]#
```
