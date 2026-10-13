
```text
# *REQUIRED*
# Directory where mailboxes reside, _or_ name of file, relative
# to the home directory. If you _do_ define both, MAIL_DIR
# takes precedence.
# QMAIL_DIR is for Qmail
#
#QMAIL_DIR Maildir
MAIL_DIR /var/spool/mail
#MAIL_FILE .mail

# Password aging controls:
#
# PASS_MAX_DAYS Maximum number of days a password may be used.
# PASS_MIN_DAYS Minimum number of days allowed between password changes.
# PASS_MIN_LEN   Minimum acceptable password length.
# PASS_WARN_AGE Number of days warning given before a password
# expires.
#
PASS_MAX_DAYS		99999
PASS_MIN_DAYS		0
PASS_MIN_LEN		5
PASS_WARN_AGE		7

#
# Min/max values for automatic uid selection in useradd
#
UID_MIN			500
UID_MAX			60000

#
# Min/max values for automatic gid selection in groupadd
#
GID_MIN			500
GID_MAX			60000

#
# If defined, this command is run when removing a user.
# It should remove any at/cron/print jobs etc. owned by
# the user to be removed (passed as the first argument).
#
#USERDEL_CMD /usr/sbin/userdel_local

#
# If useradd should create home directories for users by
# default. On RH systems, we do. This option is ORed with on
# the -m flag useradd command line.
#
CREATE_HOME yes
```

`useradd` 命令会忽略空行和以井号（`#`）开头的注释。所有其他行都包含关键字/值对。例如，第一个非注释行是关键字 `MAIL_DIR`，后跟一些空白和值 `/var/spool/mail`。这告诉 `useradd` 初始用户电子邮件信箱应在该目录中创建。随后是其他关键字/值对，它们允许你自定义自动分配的用户 ID 号或组 ID 号的有效范围。每个关键字之前都有一个解释该关键字用途的注释部分。更改默认值很简单，只需编辑与该关键字关联的值，然后保存 `login.defs` 文件即可。

如果你想要查看默认值，请按照以下方式输入带有 `-D` 选项的 `useradd` 命令：

```text
# useradd -D
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKELE=/etc/skel
```

你也可以使用 `-D` 选项来更改默认值。当以此标志运行时，`useradd` 不会实际创建新的用户账户；相反，它将额外提供的选项保存为 `/etc/login.defs` 中的新默认值。并非所有 `useradd` 选项都可以与 `-D` 选项结合使用。你只能使用表 11-2 中列出的五个选项。

### 表 11-2：用于更改用户默认值的 useradd 选项

| 选项 | 描述 |
| :--- | :--- |
| `-b` `default_home` | 设置创建用户家目录的默认目录。用要使用的目录名替换 `default_home`。通常这是 `/home`。 |
| `-e` `default_expire_date` | 设置用户账户被禁用的默认过期日期。`default_expire_date` 值应替换为 MM/DD/YYYY 形式的日期——例如，10/15/2001。 |
| `-f` `default_inactive` | 设置密码过期后多少天禁用账户。用代表天数的数字替换 `default_inactive`。 |
| `-g` `default_group` | 设置新用户将被放置的默认组。通常 `useradd` 会创建一个与用户同名且 ID 号相同的新组。用要使用的组名替换 `default_group`。 |
| `-s` `default_shell` | 设置新用户的默认 shell。通常这是 `/bin/sh`。用你希望作为新用户默认 shell 的完整路径替换 `default_shell`。 |

要设置任何默认值，首先提供 `-D` 选项；然后添加你想要设置的任何默认值。例如，要将默认家目录位置设置为 `/home/everyone`，将默认 shell 设置为 `/bin/tcsh`，请输入以下内容：

```text
# useradd -D -b /home/everyone -s /bin/tcsh
```

## 提供初始登录脚本

除了设置用户默认值外，管理员还可以创建默认文件，这些文件会被复制到每个用户的 home 目录中以供使用。这些文件可以包括登录脚本和 shell 配置文件（例如 `.bashrc`）。以下章节将介绍其中的一些文件。

许多 Red Hat Linux 应用程序（包括命令 shell 本身）在启动时都会读取一个配置文件。传统上，这些配置文件存储在用户的 home 目录中。这样，每个用户都可以自定义命令 shell 和其他应用程序的行为，而不会影响其他用户的行为。通过这种方式，可以从 `/etc/profile` 分配全局默认设置，然后用户可以通过其个人文件增强或覆盖这些设置。

例如，`bash` 命令 shell 在每次启动时都会查找当前用户 home 目录中名为 `.bashrc` 的文件。同样，`tcsh` 命令 shell 会查找用户 home 目录中名为 `.tcshrc` 的文件。您可能会注意到一个重复出现的主题。各种应用程序的启动脚本和配置文件通常以点号（`.`）字符开头，并以字母 `rc` 结尾。您可以通过将这些文件及其他配置文件的初始默认版本放置在 `/etc/skel` 目录中来提供这些文件。当您运行 `useradd` 命令时，这些脚本和配置文件会被复制到新用户的 home 目录中。

### 提供初始 .bashrc 文件

通过向用户提供初始的 `.bashrc` 文件，您为他们提供了一个起点，他们可以在此基础上进一步自定义其 shell 环境。此外，您可以确保该文件以适当的访问权限创建，从而不损害系统安全。

毕竟，`.bashrc` 脚本在每次用户启动新的 `bash` shell 时都会运行。因此，安全性是一个关注点。它也是提供有用的命令别名和命令搜索路径补充的好地方。让我们来看一个例子：

```bash
# .bashrc
# User specific aliases and functions
alias rm='rm -i'
alias cp='cp -i'
alias mv='mv -i'

if [ -f /etc/bashrc ]; then
	. /etc/bashrc
fi

PATH=$PATH:/usr/bin:/usr/local/bin
export PATH
```

这个示例 `.bashrc` 文件为 `rm`、`cp` 和 `mv` 命令创建别名，导致始终使用 `-i` 选项（除非用 `-f` 选项覆盖）。这可以防止意外删除文件。接下来，如果 `/etc/bashrc` 存在，该文件会执行它以读取更多全局 bash 值。该文件还设置了搜索路径。

### 提供初始 .tcshrc 文件

下面的 `.tcshrc` 文件示例基本上执行与前一个 `.bashrc` 示例相同的功能。但是，该文件（针对 root 用户）还有一个额外的任务：设置命令提示符的外观：

```csh
# .tcshrc

# User specific aliases and functions

alias rm `rm -i`
alias cp `cp -i`
alias mv `mv -i`

setenv PATH "$PATH:/usr/bin:/usr/local/bin"

set prompt='[%n@%m %c]# '
```
