
- “手动指定用户 ID”——通常，您不会选中此框，以便自动为新用户分配 `UID`。常规用户的新 `UID` 从 500 开始。但是，如果您想为用户分配特定的 `UID`（例如，如果您希望将 `UID` 与网络中另一台计算机上用户的 `UID` 匹配），请选择此框并在 `UID` 框中输入要使用的数字。

3. 完成后单击“确定”。新用户会被添加到 `/etc/passwd` 和 `/etc/group` 文件中。现在用户帐户可用于登录。

> **注意** 使用用户私有组（UPGs）可以有利于在几个用户之间共享文件目录。这里有一个示例：

```bash
# useradd -m projectx
# mkdir /usr/local/x
# chown root.projectx /usr/local/x
# chmod 2775 /usr/local/x
# ls -ld /usr/local/x
drwxrwx-x 2 root projectx 4096 May 12 04:31 /usr/local/x
# gpasswd -a nextuser projectx
```

在此示例中，您创建一个名为 `projectx` 的用户（带有一个名为 `projectx` 的组）。创建一个 `/usr/local/x` 目录，并使其由 `root` 用户和 `projectx` 组拥有。为组设置 `setgid` 位开启（2），为用户和组开放完整的读/写/执行权限（77），为其他人开放读和执行权限（5）。将每个您希望能够写入 `projectx` 目录的用户（将 `nextuser` 替换为您要添加的用户）添加到该组（添加）。此后，无论用户的主组是什么，用户在 `/usr/local/x` 目录中创建的任何文件都可以被 `projectx` 组中的任何人读取或修改。

### 设置用户默认值

`useradd` 命令和“用户管理器”窗口都通过读取 `/etc/login.defs` 文件来确定新帐户的默认值。您可以通过编辑该文件...

### 设置和维护用户账户

你可以使用标准文本编辑器手动编辑 `login.defs` 文件，或者通过运行带有 `-D` 选项的 `useradd` 命令来编辑。如果你选择手动编辑该文件，那么你会看到以下内容：

```text
# *REQUIRED*
# Directory where mailboxes reside, or... name of file, relative to the
# home directory. If you do define both, MAIL_DIR takes precedence.
# QMAIL_DIR is for Qmail
#
#OMAIL_DIR Maildir
MAIL_DIR /var/spool/mail
#MAIL_FILE .mail

# Password aging controls:
#
# PASS_MAX_DAYS Maximum number of days a password may be used.
# PASS_MIN_DAYS Minimum number of days allowed between password changes.
# PASS_MIN_LEN Minimum acceptable password length.
# PASS_WARN_AGE Number of days warning given before a password expires.
PASS_MAX_DAYS 99999
PASS_MIN_DAYS 0
PASS_MIN_LEN 5
PASS_WARN_AGE 7

#
# Min/max values for automatic uid selection in useradd
#
UID_MIN 500
UID_MAX 60000

#
# Min/max values for automatic gid selection in groupadd
#
GID_MIN 500
GID_MAX 60000

#
# If defined, this command is run when removing a user.
# It should remove any at/cron/print jobs etc. owned by
# the user to be removed (passed as the first argument).
#
#USERDEL_CMD /usr/sbin/userdel_local

#
# If useradd should create home directories for users by default
# On RH systems, we do. This option is overridden with the -m flag on
# useradd command line.
#CREATE_HOME         yes

# The permission mask is initialized to this value. If not specified,
# the permission mask will be initialized to 022.
UMASK                 077

# This enables usiredel to remove user groups if no members exist.
# USERGROUPS_ENAB yes

# Use MD5 or DES to encrypt password? Red Hat uses MD5 by default.
MD5_CRYPT_ENAB yes
```

空行和以井号（#）开头的注释将被忽略。其他所有行都包含关键字/值对。例如，关键字 `MAIL_DIR` 后面跟随一些空白和值 `/var/spool/mail`。这告诉 `useradd` 初始用户电子邮件邮箱将在该目录中创建。紧随其后的是允许你自定义自动分配的用户 ID 或组 ID 有效范围的行。每个关键字前面都有一个解释该关键字用途的注释段。修改默认值很简单，只需编辑与该关键字关联的值，然后保存 `login.defs` 文件即可。

如果你想查看默认值，请输入带有 `-D` 选项的 `useradd` 命令，如下所示：

```text
# useradd -D
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
CREATE_MAIL_SPOOL=yes
```

你还可以使用 `-D` 选项来更改默认值。运行带有此标志的 `useradd` 时，它不会实际创建新的用户账户。相反，它将额外提供的选项保存为 `/etc/login.defs` 中的新默认值。并非所有 `useradd` 选项都可以与 `-D` 选项结合使用。你只能使用表 10-2 中列出的五个选项。

要设置任何默认值，请先提供 `-D` 选项；然后添加你想要设置的任何默认值。例如，要将默认主目录位置设置为 `/home/everyone`，将默认 `shell` 设置为 `/bin/tcsh`，请输入以下内容：

```text
# useradd -D -b /home/everyone -s /bin/tcsh
```

除了设置用户默认值外，管理员还可以创建默认文件，这些文件将被复制到每个用户的主目录中供其使用。这些文件可以包括登录脚本和 `shell` 配置文件，例如 `.bashrc`。以下部分将描述其中一些文件。

#### 表 10-2 `useradd` 用于更改用户默认值的选项

| 选项 | 描述 |
|---|---|
| `-b default_home` | 设置创建用户主目录的默认目录。用要使用的目录名替换 `default_home`。通常这是 `/home`。 |
| `-e default_expire_date` | 设置禁用用户账户的默认过期日期。`default_expire_date` 值应替换为 `MM/DD/YYYY` 格式的日期——例如，`10/15/2009`。 |
| `-f default_inactive` | 设置在密码过期后多少天禁用账户。用一个代表天数的数字替换 `default_inactive`。 |
| `-g default_group` | 设置新用户将加入的默认组。在 `CentOS` 中，`useradd` 创建一个与用户同名且 ID 号相同的新组，因此该值被忽略。要为某个用户设置不同的主要组，你必须在命令行上显式地使用 `-g` 选项进行设置。 |
| `-s default_shell` | 设置新用户的默认 `shell`。通常是 `/bin/bash`。用你想作为新用户的默认 `shell` 的完整路径替换 `default_shell`。 |

### 提供初始登录脚本

许多 `Linux` 应用程序（包括命令行 `shell` 本身）在启动时都会读取一个配置文件。传统做法是将这些配置文件存储在用户的主目录中。这样，每个用户都可以自定义命令行 `shell` 和其他应用的行为，而不会影响其他用户的行为。这样，可以从 `/etc/profile` 分配全局默认值，然后由用户的个人文件增强这些设置。

例如，`bash` 命令行 `shell` 在每次启动时都会查找当前用户主目录中名为 `.bashrc` 的文件。类似地，`tcsh` 命令行 `shell` 会查找用户主目录中名为 `.tcshrc` 的文件。你可能会在这里看到一个重复的主题。各种应用的启动脚本和配置文件通常以点（`.`）字符开头，并以字母 `rc`（代表“运行命令”）结尾。你可以通过将这些及其他配置文件的初始默认版本放入 `/etc/skel` 目录来提供它们。当你运行 `useradd` 命令时，这些脚本和配置文件将被复制到新用户的主目录中。

### 提供初始 `.bashrc` 和 `.bash_profile` 文件

通过为用户提供初始的 `.bashrc` 和 `.bash_profile` 文件，你为它们提供了一个起点，它们可以在此基础上进一步自定义其 `shell` 环境。此外，你可以确保文件以适当的访问权限创建，以免在用户不知情的情况下危及系统安全。

`.bash_profile` 脚本在用户每次启动新的 `bash` `shell` 时运行，并随之运行 `.bashrc` 脚本。因此，安全性是一个需要考虑的问题。`.bash_profile` 文件设置了用户最初使用的 `PATH`，因此是一个添加包含你想要用户能够运行的二进制文件目录的好地方。你还可以添加你希望自动为每个用户运行的其他启动程序。以下是 `.bash_profile` 文件的一个示例：

```text
# .bash_profile

# Get the aliases and functions
if [ -f ~/.bashrc ]; then
. ~/.bashrc
fi

# User specific environment and startup programs
PATH=$PATH:$HOME/bin
export PATH
```

`.bashrc` 文件是提供有用命令别名和命令搜索路径增量的好地方。以下是 `.bashrc` 文件的一个示例：

```text
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

这个示例 `.bashrc` 在 `/etc/bashrc` 存在时执行它，以读取任何进一步的全局 `bash` 值。接下来，该文件为 `rm`、`cp` 和 `mv` 命令创建别名，导致始终使用 `-i` 选项，除非被 `-f` 选项覆盖。这可以防止意外删除文件。

### 提供初始 `.tcshrc` 文件

以下示例 `.tcshrc` 文件基本上做了与前面 `.bashrc` 示例相同的事情。但是，这个文件（它针对 `root` 用户）还有一个额外的任务，即设置命令提示符的外观：

```text
# .tcshrc
# User specific aliases and functions

alias rm 'rm -i'
alias cp 'cp -i'
alias mv 'mv -i'

setenv PATH "$PATH:/usr/bin:/usr/local/bin"

set prompt='[%n@%m %c]# '
```

`tcsh` `shell` 不使用 `export` 命令来设置环境变量，而是使用 `setenv` 命令。在示例中，`setenv` 用于设置 `PATH` 变量。`shell` 提示符被设置为包括你的用户名（`%n`）、你的计算机名称（`%m`）和当前目录的名称（`%c`）。因此，如果你使用 `tcsh` `shell` 作为名为 `zarkov` 的计算机上的 `root` 用户，并且当前目录为 `/tmp`，你的提示符将显示如下：

```text
[root@zarkov /tmp]#
```

`.tcshrc` 文件也可以命名为 `.cshrc`。`tcsh` `shell` 实际上是 `csh` `shell` 的一个扩展版本。事实上，你可以通过 `csh` 名称调用它。当启动 `tcsh` `shell` 时，它首先在当前用户的主目录中查找 `.tcshrc` 文件。如果找不到该名称的文件，它会查找另一个名称，`.cshrc`。因此，两个名称都是合适的。

### 配置系统范围的 Shell 选项

允许每个用户具有单独可自定义的 `shell` 启动文件是一种非常灵活且有用的做法。但有时你需要比这更集中的控制。你可能有一个环境变量或其他 `shell` 设置，希望为每个用户设置，无一例外。如果你将该设置添加到每个单独的 `shell` 中，用户可以编辑该文件并将其删除。此外，如果将来必须更改该设置，你必须在每个用户的 `shell` 启动文件中更改它。

#### 配置系统范围的 Bash 选项

幸运的是，有一种更好的方法。有一些默认启动文件适用于计算机的所有用户，每个命令行 `shell` 在读取用户特定文件之前都会读取它们。对于 `bash` 命令行 `shell`，它在做任何其他事情之前都会读取 `/etc/bashrc` 文件。

**注意** 虽然你可以在 `/etc/bashrc` 文件中设置系统范围的选项，但用户可以覆盖这些设置。

#### 配置系统级 tcsh 选项

同样地，`tcsh` 外壳在处理用户主目录下的 `.cshrc` 或 `.tcshrc` 文件之前，会先读取 `/etc/csh.cshrc` 文件。以下是 `CentOS` 自带的 `/etc/csh.cshrc` 文件内容的部分列表：

```bash
# /etc/cshrc
#
# csh configuration for all shell invocations.
# by default, we want this to get set.
# Even for non-interactive, non-login shells.
umask 022

if ($?prompt) then
    if ($?tcsh) then
        set promptchars='$#'
        set prompt='[%u@%m %c]$#'
        set autolist
    else
        set prompt='\[$user@\hname -s '\]\$'
    endif
endif
```

`/etc/cshrc` 和 `/etc/bashrc` 文件会设置各种外壳环境选项。如果您想修改或添加提供给系统中每个用户的外壳环境，`/etc/bashrc` 或 `/etc/cshrc` 文件就是进行此操作的地方。

### 设置系统配置文件

分配给每个用户的一些最基本信息是从 `/etc/profile` 文件中添加的。因此，如果您想更改以下任何信息，可以从 `/etc/profile` 开始。`/etc/profile` 文件的内容仅被引入到每个用户的初始登录外壳中。以下是 `/etc/profile` 中包含的一些值：

-   `PATH` — 为 `root` 用户和所有其他用户分配默认的 `PATH`。您可能需要更改此值，以添加包含所有用户所需应用程序的本地目录路径。

-   `ulimit -S -c 0` — `ulimit` 的 `-c 0` 选项防止通常在进程崩溃时创建的 `core` 文件被创建。`-S` 使此选项成为“软”选项，因此用户可以选择启用 `core` 文件功能。

-   `Environment Variables` — 标准操作所需的外壳环境变量在此文件中被赋值。这些包括 `USER`（由 `id -un` 命令设置）、`LOGNAME`（与 `USER` 相同）、`MAIL`（设置为 `/var/spool/mail/$USER`）、`HOSTNAME`（设置为 `/bin/hostname` 命令的输出），以及 `HISTSIZE`（将外壳命令历史记录设置为 1,000 项）。

-   `INPUTRC` — 基于 `/etc/inputrc` 文件的内容，为特定情况设置键盘映射。特别是，`inputrc` 文件确保 `Linux` 控制台和各种终端窗口（`xterm` 和 `rxvt`）都能正常工作。

`/etc/profile` 文件所做的最后一件事是查看 `/etc/profile.d` 目录的内容，并引入其找到的文件。每个文件包含定义环境变量或别名的设置，这些设置会影响用户如何使用外壳。例如，`lang.sh` 和 `largs.sh` 文件标识了外语文件的位置。`vim` 文件创建别名，使得输入 `vi` 时会使用 `vim`。`which2.sh` 文件定义了 `which` 命令使用的一组选项。您可以修改 `profile.d` 文件或添加自己的文件，以为所有用户设置环境变量和别名。

### 向服务器添加用户账户

当您设置服务器时，通常希望允许人们向其上传文件，或从中下载文件或消息。然而，您可能不希望允许这些人访问整个服务器。您可以在首次创建他们的用户账户时就开始限制对这些用户的访问。
