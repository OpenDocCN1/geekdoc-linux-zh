
## 第 418 页 第三部分：管理 Fedora

```bash
# QMAIL_DIR is for Qmail
#
#QMAIL_DIR Maildir
MAIL_DIR    /var/spool/mail
#MAIL_FILE .mail

# Password aging controls:
#
# PASS_MAX_DAYS Maximum number of days a password may be used.
# PASS_MIN_DAYS Minimum number of days allowed between password changes.
# PASS_MIN_LEN Minimum acceptable password length.
# PASS_WARN_AGE Number of days warning given before a password
# expires.
#
PASS_MAX_DAYS      99999
PASS_MIN_DAYS      0
PASS_MIN_LEN       5
PASS_WARN_AGE      7

#
# Min/max values for automatic uid selection in useradd
#
UID_MIN            500
UID_MAX            60000

#
# Min/max values for automatic gid selection in groupadd
#
GID_MIN            500
GID_MAX            60000

#
# If defined, this command is run when removing a user.
# It should remove any at/cron/print jobs etc. owned by
# the user to be removed (passed as the first argument).
#
#USERDEL_CMD /usr/sbin/userdel_local

#
# If useradd should create home directories for users by default.
# On RH systems, we do. This option is overridden with the -m flag on
# useradd command line.
#
CREATE_HOME yes
# The permission mask is initialized to this value. If not
# specified, the permission mask will be initialized to 022.
UMASK                    077
```

```bash
# This enables userdel to remove groups if no members exist.
#
USERGROUPS_ENAB yes

# Use MD5 or DES to encrypt password? RedHat use MD5 by default.
MD5_CRYPT_ENAB no
ENCRYPT_METHOD SHA512
```

以井号（#）开头的行将被忽略。其他所有行都包含关键字/值对。例如，关键字 **MAIL_DIR** 后面跟着一些空白字符，然后是值 `/var/spool/mail`。这告诉 `useradd` 初始用户电子邮件邮箱将在该目录中创建。接下来是允许您自定义自动分配的用户 ID 或组 ID 有效范围的行。每个关键字前面都有一个注释部分，用于解释该关键字的用途。更改默认值只需编辑与该关键字关联的值，然后保存 `login.defs` 文件即可。

可以使用 `useradd` 命令修改的默认设置存储在 `/etc/default/useradd` 文件中。以下是该文件的一个示例：

```bash
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKELE=/etc/skel
CREATE_MAIL_SPOOL=yes
```

您可以直接查看和修改该文件。或者，您可以通过输入带有 -D 选项的 `useradd` 命令来查看默认值，如下所示：

```bash
# useradd -D
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKELE=/etc/skel
CREATE_MAIL_SPOOL=yes
```

您还可以使用 -D 选项来更改默认值。当使用此标志运行时，`useradd` 不会实际创建新的用户账户；相反，它将任何额外提供的选项保存为 `/etc/default/useradd` 中的新默认值。并非所有 `useradd` 选项都可以与 -D 选项一起使用。您只能使用表 10-2 中列出的五个选项。

## 表 10-2：用于更改用户默认值的 useradd 选项

| 选项 | 描述 |
|---|---|
| `-b` `default_home` | 设置创建用户主目录的默认目录。将 `default_home` 替换为要使用的目录名称。通常是 `/home`。 |
| `-e` `default_expire_date` | 设置用户账户被禁用的默认过期日期。`default_expire_date` 值应替换为 MM/DD/YYYY 格式的日期——例如，10/15/2010。 |
| `-f` `default_inactive` | 设置密码过期后多少天账户将被禁用。将 `default_inactive` 替换为代表天数的数字。 |
| `-g` `default_group` | 设置新用户将被放入的默认组。在 Fedora 中，`useradd` 创建一个与用户同名且 ID 号相同的新组，因此此值会被忽略。若要为用户设置不同的主要组，必须在命令行上使用 `-g` 选项显式设置。 |
| `-s` `default_shell` | 设置新用户的默认 shell。通常这是 `/bin/bash`。将 `default_shell` 替换为您希望作为新用户默认 shell 的完整路径。 |

要设置任何默认值，首先提供 `-D` 选项，然后添加您想要设置的任何默认值。例如，要将默认主目录位置设置为 `/home/everyone` 并将默认 shell 设置为 `/bin/tcsh`，请键入以下内容：

```bash
# useradd -D -b /home/everyone -s /bin/tcsh
```

除了设置用户默认值外，管理员还可以创建默认文件，这些文件将被复制到每个用户的主目录中以供使用。这些文件可以包括登录脚本和 shell 配置文件（例如 `.bashrc`）。以下部分描述了这些文件的一些内容。

## 提供初始登录脚本

许多 Linux 应用程序，包括命令 shell 本身，在启动时会读取配置文件。通常这些配置文件存储在用户的主目录中。这样，每个用户都可以自定义命令 shell 和其他应用程序的行为，而不会影响其他用户的行为。通过这种方式，可以从 `/etc/profile` 分配全局默认值，然后由用户的个人文件进行自定义。

例如，`bash` 命令 shell 在启动时会在当前用户的主目录中查找名为 `.bashrc` 的文件。类似地，`tcsh` 命令 shell 会在用户的主目录中查找名为 `.cshrc` 的文件。您可能在这里看到了一个重复的主题。各种应用程序的启动脚本和配置文件通常以点（`.`）字符开头，并以字母 `rc` 结尾（代表 `run commands`，即运行命令）。您可以通过将这些文件以及其他配置文件的初始默认版本放在 `/etc/skel` 目录中，来提供这些配置文件的初始默认版本。

当您运行 `useradd` 命令时，这些脚本和配置文件将被复制到新用户的主目录中。

## 提供初始 `.bashrc` 和 `.bash_profile` 文件

通过向用户提供初始的 `.bashrc` 和 `.bash_profile` 文件，您为他们提供了一个起点，他们可以在此基础上进一步自定义他们的 shell 环境。此外，您可以确保文件以适当的访问权限创建，以免在用户不知情的情况下损害系统安全性。

`.bash_profile` 脚本在用户每次启动新的 `bash` shell 时运行，并反过来运行 `.bashrc` 脚本。因此，安全性是一个关注点。`.bash_profile` 文件设置了用户最初使用的 `PATH`，因此它是添加包含您希望用户能够在您的位置运行的二进制文件目录的好地方。您还可以添加您希望为每个用户自动运行的其他启动程序。以下是 `.bash_profile` 文件的一个示例：

```bash
# .bash_profile

# Get the aliases and functions
if [ -f -/.bashrc ]; then
    . -/.bashrc
fi

# User specific environment and startup programs
PATH=$PATH:$HOME/bin
export PATH
```

`.bashrc` 文件是提供有用的命令别名和命令搜索路径添加的好地方。以下是 `.bashrc` 文件的一个示例：

```bash
# .bashrc

# Source global definitions
if [ -f /etc/bashrc ]; then
    . /etc/bashrc
fi
# User specific aliases and functions
alias rm='rm -i'
alias cp='cp -i'
alias mv='mv -i'
```

这个示例 `.bashrc` 文件执行 `/etc/bashrc`（如果存在）以读取任何额外的全局 `bash` 值。接下来，该文件为 `rm`、`cp` 和 `mv` 命令创建别名，这些别名导致始终使用 `-i` 选项（除非被 `-f` 选项覆盖）。这防止了文件被意外删除。

### 提供初始 .tcshrc 文件

以下示例 `.tcshrc` 文件基本上与前面的 `.bashrc` 示例做着相同的事情。但是，该文件（适用于 root 用户）还有一个额外的任务，即设置命令提示符的外观：

```bash
# .tcshrc

# User specific aliases and functions

alias rm 'rm -i'
alias cp 'cp -i'
alias mv 'mv -i'

setenv PATH "$PATH:/usr/bin:/usr/local/bin"

set prompt='[\$n@\$m \$c]# '
```

在 `tcsh` shell 中，不使用 `export` 命令来设置环境变量，而是使用 `setenv` 命令。在示例中，使用 `setenv` 来设置 `PATH` 变量。将 shell 提示符设置为包括您的用户名（`$n`）、您的计算机名称（`$m`）以及当前目录的名称（`$c`）。因此，如果您在名为 `maple` 的计算机上以 root 用户身份使用 `tcsh` shell，并且当前目录为 `/tmp`，您的提示符将显示如下：

```bash
[root@maple /tmp]#
```

`.tcshrc` 文件也可以命名为 `.cshrc`。`tcsh` shell 实际上是 `csh` shell 的扩展版本（事实上，您可以使用 `csh` 名称调用它）。当启动 `tcsh` shell 时，它首先在当前用户的主目录中查找 `.tcshrc` 文件。如果找不到该名称的文件，它会查找另一个名称 `.cshrc`。因此，这两个名称都是合适的。

## 配置系统范围的 shell 选项

为每个用户允许单独自定义的 shell 启动文件是一种非常灵活且有用的做法。但有时您需要比那更集中的控制。您可能有一个环境变量或其他 shell 设置，您希望为每个用户设置，无一例外。如果您将该设置添加到每个单独的 shell 中，用户就有能力编辑该文件并删除它。此外，如果该设置将来需要更改，您必须在每个用户的 shell 启动文件中更改它。

### 配置系统范围的 bash 选项

幸运的是，有一种更好的方法。存在适用于计算机所有用户的默认启动文件，每个命令 shell 在读取用户特定文件之前都会读取这些文件。在 `bash` 命令 shell 的情况下，它在执行任何其他操作之前都会读取 `/etc/bashrc` 文件。

> **注意：** 虽然您可以在 `/etc/bashrc` 文件中放入系统范围的选项，但用户可以覆盖这些设置。

