
```
[root@server1 root]# cat /etc/login.defs
# "REQUIRED"
# Directory where mailboxes reside, or name of file, relative to the
# home directory. If you_do_ define both, MAIL_DIR takes precedence.
#       OMAIL_DIR is for Qmail
#
#OMAIL_DIR        Maildir
MAIL_DIR           /var/spool/mail
#MAIL_FILE        .mail


# Password aging controls:
#
#	PASS_MAX_DAYS	Maximum number of days a password may be used.
#	PASS_MIN_DAYS	Minimum number of days allowed between password
#				changes.
#	PASS_MIN_LEN	Minimum acceptable password length.
#	PASS_WARN_AGE	Number of days warning given before a password
#				expires.
#
PASS_MAX_DAYS		99999
PASS_MIN_DAYS		0
PASS_MIN_LEN		5
PASS_WARN_AGE		7


#
#	Min/max values for automatic uid selection in useradd
#
UID_MIN			500
UID_MAX			60000


#
#	Min/max values for automatic gid selection in groupadd
#
GID_MIN			500
GID_MAX			60000


#
#	If defined, this command is run when removing a user.
#	It should remove any at/cron/print jobs etc. owned by
#	the user to be removed (passed as the first argument).
#
#USERDEL_CMD		/usr/sbin/userdel_local
```

第二个文件`/etc/default/useradd`包含关于默认主组、主目录位置、禁用密码过期账户的默认天数、禁用用户账户的日期、使用的Shell以及使用的骨架目录的信息。大多数Linux系统上的`skeleton directory（骨架目录）`是`/etc/skel`，其中包含在创建主目录时复制到所有新用户主目录中的文件。这些文件大多是环境文件，例如`.bash_profile`和`.bashrc`。

`/etc/default/useradd`文件的一个示例显示在以下输出中：

```
[root@server1 root]# cat /etc/default/useradd
# useradd defaults file
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKELETON=/etc/skel
[root@server1 root]#
```

若要覆盖`/etc/login.defs`和`/etc/default/useradd`中用户的任何默认参数，可以在创建用户账户时为`useradd`命令指定选项。例如，要创建一个`UID`为`762`的用户`mary`，可以使用`useradd`命令的`-u`选项，如以下示例所示：

```
[root@server1 root]# useradd -u 762 mary
[root@server1 root]#
```

表 11-6 列出了`useradd`命令的一些常用选项及其描述。

| 选项 | 描述 |
| :--- | :--- |
| `-c "description"` | 在`/etc/passwd`的`GECOS`字段中为用户添加描述。 |
| `-d home/directory` | 指定用户主目录的绝对路径名。 |
| `-e expiry/date` | 指定禁止账户登录的日期。 |
| `-f days` | 指定密码过期的用户账户在禁用前的天数。 |
| `-g group` | 指定用户账户的主组。在`Red Hat Fedora Linux`中，默认情况下会创建一个与用户同名的组，并将其作为该用户的主组。 |
| `-G group1, group2,etc.` | 指定用户账户的其他所有组成员身份。 |
| `-m` | 指定应为用户账户创建主目录。在`Red Hat Fedora Linux`中，默认情况下通过`/etc/login.defs`文件中的条目为所有用户创建主目录。 |
| `-k directory` | 指定在将文件复制到新主目录时使用的骨架目录。 |
| `-s shell` | 指定用户账户使用的`Shell`的绝对路径名。 |
| `-u UID` | 指定用户账户的`UID`。 |

添加用户账户后，`/etc/shadow`文件中的密码字段包含两个`!`字符，表示未为用户账户设置密码。要设置密码，只需输入`passwd`命令，在命令提示符处输入新用户账户的名称，然后在提示时提供适当的密码。为`bob`用户设置密码的示例如下：

```
[root@server1 root]# passwd bobg
Changing password for user bobg.
New UNIX password:
Retype new UNIX password:
passwd: all authentication tokens updated successfully.
[root@server1 root]#
```

**注意**

如果没有参数，`passwd`命令会更改当前用户的密码。

所有用户账户在登录系统之前必须设置密码。

`root`用户可以使用`passwd`命令为任何用户账户设置密码；但是，普通用户只能使用此命令更改其密码。

#### 修改用户账户

要在创建后修改用户账户的相关信息，你可以编辑`/etc/passwd`或`/etc/shadow`文件；但这并不是推荐的做法，因为这些文件中的拼写错误可能会导致系统无法正常工作。`usermod`命令可用于修改有关用户账户的大多数信息。例如，要将用户`bob`的登录名称更改为`barb`，可以使用`usermod`命令的`-l`选项：

```
[root@server1 root]# usermod -l barb bobg
[root@server1 root]#
```

表 11-7 列出了使用`usermod`命令修改用户账户的完整选项列表。

**表 11-7 usermod 命令的常用选项**

| 选项 | 描述 |
| :--- | :--- |
| `-c "description"` | 在`/etc/passwd`的`GECOS`字段中指定用户的新描述 |
| `-d homedirectory` | 指定新主目录的绝对路径名 |
| `-e expirydate` | 指定禁止账户登录的日期 |
| `-f days` | 指定密码过期的用户账户在禁用前的天数 |
| `-g group` | 指定用户账户的新主组 |
| `-G group1, group2, etc.` | 指定用户账户的其他所有组成员身份 |
| `-l name` | 指定新的登录名称 |
| `-s shell` | 指定用户账户使用的新`Shell`的绝对路径名 |
| `-u UID` | 指定用户账户的新`UID` |

#### 管理用户账户

`usermod`命令唯一无法修改的用户账户信息是存储在`/etc/shadow`中的密码过期信息（最小值、最大值、警告天数），这在前面已经讨论过。若要更改此信息，您可以使用带有适当选项的`chage`命令。例如，要指定用户`bob`在获得新密码后必须等待`2`天才能更改密码，同时指定其密码每`50`天过期一次，并在过期前`7`天发出警告，您可以使用`chage`命令的以下选项：

```
[root@server1 root]# chage -m 2 -M 50 -W 7 bob
[root@server1 root]#
```

在某些情况下，可能需要临时禁止用户登录，这通常被称为锁定账户。要锁定账户，您可以在命令提示符下使用命令`usermod -L username`。这会在`/etc/shadow`文件中的加密密码字段开头放置一个`!`字符。要解锁账户，只需在命令提示符下输入`usermod -U username`，这会移除`/etc/shadow`文件中密码字段中的`!`字符。
