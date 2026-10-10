

根据前面的输出，“bin”组的GID为1，并且有三个用户作为成员：root、bin 和 daemon。

## 创建用户账户

你可以在 Linux 系统上使用 `useradd` 命令来创建用户账户，将用户名作为参数指定，如下所示：

```
[root@server1 ~]# useradd bobg
[root@server1 ~]# _
```

在这种情况下，所有其他信息，如 UID、shell 和主目录位置，都取自包含用户账户创建默认值的两个文件。

第一个文件 /etc/login.defs 包含设置电子邮件默认位置、密码过期信息、最小密码长度以及可用的 UID 和 GID 范围的参数。此外，它还决定在创建用户时是否自动创建主目录，以及用于在 /etc/shadow 中存储密码的密码哈希算法。

/etc/login.defs 文件的示例如下：

```
[root@server1 ~]# cat /etc/login.defs
# REQUIRED*
# Directory where mailboxes reside, _or_ name of file, relative to the
# home directory. If you _do_ define both, MAIL_DIR takes precedence.
# QMAIL_DIR is for Qmail
#
QMAIL_DIR    Maildir
MAIL_DIR     /var/spool/mail
#MAIL_FILE   .mail
# Password aging controls:
#
# PASS_MAX_DAYS       Maximum number of days a password may be used.
# PASS_MIN_DAYS       Minimum number of days allowed between password changes
# PASS_MIN_LEN        Minimum acceptable password length.
# PASS_WARN_AGE       Number of days warning given before a password expires
#
PASS_MAX_DAYS 99999
PASS_MIN_DAYS 0
PASS_MIN_LEN  5
PASS_WARN_AGE 7

#
# Min/max values for automatic uid selection in useradd
#
UID_MIN        1000
UID_MAX        60000
# System accounts
SYS_UID_MIN    201
SYS_UID_MAX    999

#
# Min/max values for automatic gid selection in groupadd
#
GID_MIN        1000
GID_MAX        60000
# System accounts
SYS_GID_MIN    201
SYS_GID_MAX    999

#
# If defined, this command is run when removing a user.
# It should remove any at/cron/print jobs etc. owned by
# the user to be removed (passed as the first argument).
#
#USERDEL_CMD     /usr/sbin/userdel_local
#
# If useradd should create home directories for users by default
# On RH systems, we do. This option is overridden with the -m flag on
# useradd command line.
#
CREATE_HOME     yes

# The permission mask is initialized to this value. If not specified,
# the permission mask will be initialized to 022.
UMASK 077
# This enables userdel to remove user groups if no members exist.
#
USERGROUPS_ENAB yes

# Use SHA512 to encrypt password.
ENCRYPT_METHOD SHA512

[root@server1 ~]# _
```

第二个文件，**/etc/default/useradd**，包含有关默认主组、主目录位置、禁用过期密码账户的默认天数、禁用用户账户的日期、使用的 shell 以及使用的骨架目录的信息。骨架目录，在大多数 Linux 系统上是 **/etc/skel**，包含在创建主目录时复制到所有新用户主目录中的文件。其中大多数文件是环境文件，如 .bash_profile 和 .bashrc。

**/etc/default/useradd** 文件的示例如下：

```
[root@server1 ~]# cat /etc/default/useradd
# useradd defaults file
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKELETON=/etc/skel
CREATE_MAIL_SPOOL=yes

[root@server1 ~]# _
```

要覆盖 **/etc/login.defs** 和 **/etc/default/useradd** 文件中用户的任何默认参数，你可以指定 `useradd` 命令的选项。例如，要创建名为 marvj 且 UID 为 762 的用户，你可以使用 `useradd` 命令的 `-u` 选项，如下例所示：

```
[root@server1 ~]# useradd -u 762 marvj
[root@server1 ~]# _
```

表 10-6 列出了 `useradd` 命令的一些常见选项及其描述。

添加用户账户后，**/etc/shadow** 文件中的密码字段包含两个 ! 字符或单个 * 字符，表明未为用户账户设置密码。要设置密码，只需输入 **passwd 命令**，在命令提示符处输入新用户账户的名称，然后在提示时提供相应的密码。为 bobg 用户设置密码的示例如下：

```
[root@server1 ~]# passwd bobg
Changing password for user bobg.
New UNIX password:
Retype new UNIX password:
passwd: all authentication tokens updated successfully.
[root@server1 ~]# _
```

| 选项 | 描述 |
| :--- | :--- |
| -c "description" | 在 /etc/passwd 的 GECOS 字段中为用户添加描述。 |
| -d homedir | 指定用户主目录的绝对路径名。 |
| -e expirydate | 指定禁用账户登录的日期。 |
| -f days | 指定密码过期的用户账户被禁用的天数。 |
| -g group | 指定用户账户的主组。在 Fedora Linux 中默认情况下，会创建一个与用户同名的组，并作为该用户的主组。 |
| -G group1, group2,etc. | 指定用户账户的其他所有组成员身份。 |
| -m | 指定应为用户账户创建主目录。在 Fedora Linux 中默认情况下，通过 /etc/login.defs 文件中的条目为所有用户创建主目录。然而，在许多其他 Linux 发行版中，除非指定此选项，否则不会创建主目录。 |
| -k directory | 指定在将文件复制到新主目录时使用的骨架目录。 |
| -s shell | 指定用于用户账户的 shell 的绝对路径名。 |
| -u UID | 指定用户账户的 UID。 |

**表 10-6 useradd 命令的常见选项**

![](img/c27875544958897d817484d558c208c8_479_0.png)

如果没有参数，passwd 命令更改当前用户的密码。

![](img/c27875544958897d817484d558c208c8_479_1.png)

所有用户账户在用于登录系统之前都必须设置密码。

![](img/c27875544958897d817484d558c208c8_479_2.png)

root 用户可以使用 passwd 命令设置任何用户账户的密码；然而，普通用户只能使用此命令更改自己的密码。

![](img/c27875544958897d817484d558c208c8_479_3.png)

密码应难以猜测，并包含大写字母、小写字母和特殊字符的组合，以提高系统安全性。一个好密码的示例是 C2jR1#vv。

## 修改用户账户

要在创建后修改用户账户的相关信息，你可以编辑 /etc/passwd 或 /etc/shadow 文件。然而，不建议这样做，因为这些文件中的打字错误可能会导致系统无法正常运行。相反，最好使用 **usermod 命令**，你可以用它来修改用户账户的大部分信息。例如，要将用户 bobg 的登录名称更改为 barbg，你可以使用 `usermod` 命令的 `-l` 选项：

```
[root@server1 ~]# usermod -l barbg bobg
[root@server1 ~]# _
```

表 10-7 显示了使用 usermod 命令修改用户账户的选项完整列表。

![](img/c27875544958897d817484d558c208c8_480_0.png)

> 如果已安装，可以使用 `finger` 命令查看用户信息。此信息存储在 /etc/passwd 的 GECOS 字段中。因此，用户可以使用 `chfn` 命令更改自己的 GECOS 或 finger 信息，而无需使用 usermod 命令的 `-o` 选项。

usermod 命令无法修改的唯一用户账户信息是存储在 /etc/shadow 中的密码过期信息（最小、最大、警告），前面已讨论过。要更改此信息，你可以使用适当的选项使用 `chage` 命令。例如，要指定用户 bobg 在收到新密码后必须等待 2 天才能更改密码，并指定其密码每 50 天过期一次，且在过期前 7 天给出警告，你可以使用 chage 命令的以下选项：

```
[root@server1 ~]# chage -m 2 -M 50 -w 7 bobg
[root@server1 ~]# _
```

有时需要锁定账户，即暂时阻止用户登录。要锁定账户，你可以在命令提示符处使用命令 `usermod -L username`。这会在 /etc/shadow 文件中加密密码字段的开头放置一个 ! 字符。要解锁账户，只需在命令提示符处输入 `usermod -U username`，这将移除 /etc/shadow 文件中密码字段的 ! 字符。

或者，你可以使用 `passwd -l username` 命令锁定用户账户，并使用 `passwd -u username` 命令解锁用户账户。这些命令在密码字段中放置并移除锁定字符。

| 选项 | 描述 |
| :--- | :--- |
| -c "description" | 在 /etc/passwd 的 GECOS 字段中指定用户的新描述 |
| -h homedirectory | 指定新主目录的绝对路径名 |
| -e expirydate | 指定禁用账户登录的日期 |
| -f days | 指定密码过期的用户账户被禁用的天数 |
| -g group | 指定用户账户的新主组 |
| -G group1, group2, etc. | 指定用户账户的其他所有组成员身份 |
| -l name | 指定新的登录名称 |
| -s shell | 指定用于用户账户的新 shell 的绝对路径名 |
| -u UID | 指定用户账户的新 UID |

**表 10-7 usermod 命令的常见选项**

