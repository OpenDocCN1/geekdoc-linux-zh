
`login.defs` 文件包含新账户的默认设置。你可以通过编辑文件来修改这些默认设置。这里是可以更改的常用设置：

# 第 11 章：设置与支持用户 477

作为 `/etc/login.defs` 中的新默认值。并不是所有的 `useradd` 选项都可以与 `-D` 选项配合使用。你可以使用表 11-2 中列出的五个选项。

## 表 11-2：更改用户默认值的 useradd 选项

| 选项 | 描述 |
| --- | --- |
| `-b default_home` | 设置创建家目录的默认目录。将 `default_home` 替换为要使用的目录。这通常是 `/home/`。 |
| `-e default_expire_date` | 设置用户账户禁用的默认过期日期。默认的 `expire_date` 值应替换为 `MM/DD/YYYY` 格式的日期——例如 `10/15/2008`。 |
| `-f default_inactive` | 设置密码过期后账户被禁用前的天数。将 `default_inactive` 替换为代表天数的数字。 |
| `-g default_group` | 设置新用户所属的默认组。在 Fedora 中，`useradd` 会创建一个与用户具有相同名称和 ID 的新组，因此此值会被忽略。要为用户设置默认主组，你必须在命令行上使用 `-g` 选项显式设置。 |
| `-s default_shell` | 设置新用户的默认 shell。这通常是 `/bin/bash`。将 `default_shell` 替换为新用户所需的 shell 完整路径。 |

若要设置任何默认值，请先给出 `-D` 选项；然后添加你想要设置的任何默认值。例如，要将默认家目录位置设置为 `/home/everyone` 并将默认 shell 设置为 `/bin/tcsh`，输入以下命令：

```bash
# useradd -D -b /home/everyone -s /bin/tcsh
```

除了设置用户账户，管理员还可以创建默认文件并将其复制到每个用户的家目录中供使用。这些文件包括登录脚本和 shell 配置文件（如 `.bashrc`）。后续章节描述了其中一些文件。

## 提供初始登录脚本

许多 Linux 应用（包括命令 shell 本身）在启动时都会读取配置文件。传统的做法是将这些配置文件存储在用户的家目录中。这样，每个用户都可以自定义命令 shell 和其他应用程序的行为，而不影响其他用户。通过这种方式，可以从 `/etc/profile` 分配全局默认值，然后用户的个人文件会对这些设置进行增强。

例如，`bash` 命令 shell 每当启动时都会在当前用户的家目录查找名为 `.bashrc` 的文件。同样，`tcsh` 命令 shell 也会用户的家目录查找名为 `.bashrc` 的文件。你可能会在这里发现一个重复的主题：各种应用程序的启动脚本和配置文件通常以点（`.`）开头并以字母 `rc`（代表 run commands，运行命令）结尾。你可以通过将这些及其他配置文件放在 `/etc/skel` 目录中，来提供它们的初始默认版本。当你运行 `useradd` 命令时，这些脚本和配置文件会被复制到新用户的家目录中。

## 提供初始 .bashrc 和 .bash_profile 文件

通过为用户提供初始的 `.bashrc` 和 `.bash_profile` 文件，你为他们提供了一个起点，让他们可以从这里自定义自己的 shell 环境。此外，你可以确保这些文件以适当的访问权限创建，以防在用户不知情的情况下损害系统安全。

`.bash_profile` 脚本在用户每次启动新的 `bash` shell 时运行，并随后运行 `.bashrc` 脚本。安全性是一个考虑因素。`.bash_profile` 文件设置了用户使用的原始 `PATH`，因此它是在你位置添加包含你希望用户运行的二进制文件的目录的好地方。你还可以添加其他启动程序供每个用户自动运行。这里是一个 `.bash_profile` 文件的示例。

```bash
# .bash_profile

# 获取别名和函数
if [ -f ~/.bashrc ]; then
    source ~/.bashrc
fi

# 用户特定环境和启动程序

PATH=$HOME/bin
export PATH
```

`.bashrc` 文件是提供实用的命令别名和命令搜索路径补充的好地方。这里是一个 `.bashrc` 文件的示例：

```bash
# 源全局定义
if [ -f /etc/bashrc ]; then
    source /etc/bashrc
fi
# 用户特定别名和函数
alias rm='rm -i'
alias cp='cp -i'
alias mv='mv -i'
```

此示例 `.bashrc` 执行 `/etc/bashrc`（如果存在）以读取任何进一步的全局值。接下来，该文件为 `rm`、`cp` 和 `mv` 命令创建了别名，导致始终使用 `-i` 选项（除非被 `-f` 选项覆盖）。这可以防止误删文件。

## 提供初始 .tcshrc 文件

以下示例 `.tcshrc` 文件的功能与之前的 `.bashrc` 示例基本相同。然而，此文件（针对 root 用户）还有一个额外任务是设置命令提示符的外：

```bash
# .tcshrc

# 用户特定别名和函数

alias rm 'rm -i'
alias cp 'cp -i'
alias mv 'mv -i'

setenv PATH=$PATH:/usr/bin:/usr/local/bin

set prompt='$[%n@%m %# '
```

`tcsh` 不使用 `export` 命令来设置环境变量，而是使用 `setenv` 命令。在示例中，使用 `setenv` 来设置 `PATH`。提示符被设置为包含用户名 (`%n`)、计算机名 (`%m`) 和当前目录 (`%c`)。因此，如果你使用 `tcsh`，提示符将显示为：`[user@host dir]`。

`/etc/cshrc` 和 `/etc/bashrc` 文件设置了各种 shell 选项。如果你想修改或添加提供给每个用户的 shell 环境，`/etc/bashrc` 或 `/etc/cshrc` 文件是操作的地方。

全局 shell 选项在这些配置文件中设置。

## 第三部分：管理 Fedora 和 RHEL

同样，`tcsh` 在用户家目录之前读取 `/etc/cshrc` 文件。以下是 `/etc/csh` 内容的部分列表：
