
```bash
JAZZ=/usr/local/jazz
export JAZZ

ulimit -c 1000000
if [ `id -gn` = `id -un` -a `id -u` -gt 14 ]; then
    umask 002
else
    umask 022
fi

USER=`id -un`
MAIL="/var/spool/mail/$USER"

HOSTNAME=`/bin/hostname`
HISTSIZE=1000
HISTFILESIZE=1000
export PATH PS1 HISTNAME HISTSIZE HISTFILESIZE USER LOGNAME MAIL

for i in /etc/profile.d/*.sh ; do
    if [ -x $i ]; then
        . $i
    fi
done
```

请注意，环境变量（例如系统 `umask`）、路径、主机名和历史记录大小是如何被识别的。有关环境变量的更多信息，请参阅第 5 章。

要对用户的环境进行系统范围的更改，请在此文件中进行更改。例如，您可能希望将目录添加到路径中或更改默认系统提示符。若要阻止 `bash` 执行 `profile` 文件中的命令，请使用 `--no-profile` 选项。

如果用户希望某些默认变量有所不同，可以将启动文件放在用户的主目录中。将 `/etc/profile` 文件复制到用户主目录中的 `*.profile`，并将新文件的所有权更改为用户。现在，用户可以更改任何启动参数（例如她的提示符），并且这些更改仅适用于该用户。

当您创建新用户时，位于 `/etc/profile` 文件中的默认值会被读取并执行，以创建用户的环境。接下来，shell 在用户的主目录中查找 `.bash_profile`、`.bash_login` 和 `.profile` 文件。

如果找到其中一个或多个文件，它们将按列出的顺序读取并执行。如果同一环境变量在所有这些文件中都被设置，则该变量将被设置为最后读取的值。因此，如果您希望将路径更改为与 `/etc/profile` 文件中定义的系统路径不同的值，您可以在主目录中的 `.profile` 文件中进行此更改。由于此文件是最后读取的文件，因此它所设置的任何值都将应用于该用户的环境。第 5 章更详细地讨论了环境变量。当退出交互式登录 shell 时，如果 `/home/<username>/.bash_logout` 存在，`bash` 将读取并执行其中的命令。

当 `bash` shell 启动一个非登录的交互式 shell 时（例如，在命令提示符下输入 `bash`），它会读取并执行 `/etc/bashrc` 文件中的命令。此文件也可以在 `profile` 文件内部调用。一个 `bashrc` 文件的示例如下：

```bash
###### /etc/bashrc

###### System wide functions and aliases
###### Environment stuff goes in /etc/profile

###### For some unknown reason bash refuses to inherit
###### PS1 in some circumstances that I can't figure out.
###### Putting PS1 here ensures that it gets loaded every time.
PS1="${USER}|${PWD}> "
alias lsa="ls -aF --color | more"
alias lsl="ls -l --color | more"
alias rm="rm -i"
alias cp="cp -i"
alias mv="mv -i"
alias cl="clear"
alias dira="dir --color | more"
alias dl="dir -aF --color | more"
```

当启动 `bash` 作为交互式非登录 shell 时，您可以使用 `--norc` 选项来抑制此行为。您还可以使用 `--rcfile <filename>` 选项指定读取另一个文件而不是 `bashrc`，这将导致 `bash` 执行指定文件中的命令。

当 `bash` 作为非交互式 shell 调用时（例如运行 shell 脚本时），它会查找环境变量 `BASH_ENV`。此变量可以除 `bashrc` 文件外要执行的其他文件的名称。设置此变量时需要包含完整路径以及文件名。

可以使用名称 `sh` 而不是 `bash` 来调用 Bash。以此种方式调用 `bash` 时，`bash` 会检查 `ENV` 变量的值以确定要执行的文件。以此种方式调用 `bash` 时，不会处理其他启动文件。

确保新用户在其主目录中接收这些文件副本的一种简单方法是创建适当的文件并将它们保存到 `/etc/skel`。每当你使用 `useradd` 命令创建新用户时，这些文件会被复制到新用户目录中，并适当设置权限。

![](img/8dd1e68596303df43cb8ccf3197e8e53_194_0.png)

> 如果您选择创建启动文件并手动将其复制到用户的主目录中，请确保将用户设置为这些文件的所有者，并适当设置组所有权。未能做到这一点可能导致用户无法登录或环境变量设置不当。

### 摘要

管理用户和组是管理员工作的重要组成部分。所有用户账户都包含在 `/etc/passwd` 文件中。每个用户在单行中定义，字段包括：

- 用户名
- 密码
- 用户 ID
- 组 ID
- 注释
- 主目录
- 登录命令

这些字段中的每一个（可以为空）都是必需的。

您可以通过编辑 `/etc/passwd` 文件或使用 `useradd` 命令来创建用户。其他用于管理用户的命令是 `usermod` 和 `userdel`。

`su` 命令用于伪装成另一个用户。如果您是以 `root` 身份运行，发出 `su` 命令伪装成用户时，您不需要提供密码。然而，如果您是一般用户，则需要提供正确的密码才能使命令成功完成。

组定义在 `/etc/group` 文件中。每个组列在单独的一行中。可以通过编辑 `/etc/group` 文件或运行 `groupadd`、`groupmod`、`groupdel` 或 `gpasswd` 命令来管理组。

系统在不同情况下会读取多个不同的配置文件。交互式登录 shell 的默认文件是 `/etc/bash_profile`、`/etc/bash_login` 和 `/etc/profile`。这些文件可以复制到用户的主目录中，以便进行仅适用于该用户的更改。

其他配置文件包括 `.bash_logout` 和 `/etc/bashrc`。影响 shell 行为的两个环境变量是 `BASH_ENV` 和 `ENV`。

- 组名
- 密码
- 组 ID
- 成员

通过为用户和组使用 shadow 密码可以实现额外的安全性。

### 问答

1. 在检查系统上的各个文件时，你查看了 `/etc/passwd` 文件的内容。每一行代表什么？
   A. `/etc/passwd` 文件的每一行都包含一个用户账户的信息。该行中包含的字段（按顺序）为：用户名、密码、UID、GID、注释、主目录以及登录命令。

2. 如何一次性更改多个用户的密码？
   A. 可以通过给 `chpasswd` 提供文件名作为参数来更改多个用户的密码。该文件每行包含一个用户名/密码组合。用户名和密码必须用冒号分隔。

3. 你正在通过编辑 `/etc/passwd` 文件来创建新用户，但你没有每个用户的全名。你应该怎么做？
   A. 通常，你会将用户的全名放在注释字段中。如果你不知道正在创建的某个新账户的名字，可以将其留空。但是，请确保该字段中有冒号作为占位符。

4. 你的老板告诉你在你管理的系统上实施影子密码（shadow passwords）。你该怎么做？
   A. 你只需要运行 `pwconv` 命令即可。这将读取 `/etc/passwd` 文件，将所有密码字段更改为 `x`，并创建一个包含新加密密码的 `/etc/shadow` 文件。确保该文件仅 `root` 用户可读。

5. 你计划使用 `useradd` 命令创建新账户，但首先你想了解默认操作是什么。你如何找到这一点？
   A. 要查看 `useradd` 命令将使用的系统默认值，只需在命令提示符下输入 `useradd -D`。它将显示已设置为系统默认值的各项数值。

6. 你需要将工资记录的访问权限限制为仅三个人。最好的方法是什么？
   A. 你想做的第一件事是创建一个新组，并让这三人成为成员。接下来，设置工资记录上的适当访问权限，使得只有该组的成员才有权限访问它们。

7. 你希望每个新用户都有自己的 `.profile` 文件。确保实现这一点的最佳方法是什么？
   A. 你可以将该文件复制到每个新用户的主目录中，然后设置适当的权限。然而，一种更简单的方法是让 `useradd` 命令复制该文件并设置权限。只需将 `.profile` 文件复制到 `/etc/skel`，并在创建新用户账户使用 `useradd` 命令时使用 `-m` 选项。
