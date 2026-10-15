

```
. /etc/bashrc
fi
set -o ignoreeof
set -o noclobber
alias rm='rm -i'
alias mv='mv -i'
alias cp='cp -i'
```

你可以向自己的 .bashrc 文件中添加任何命令或自定义定义。如果你修改了 .bashrc 并希望在当前登录会话中生效，则需要使用 `.` 或 `source` 命令重新执行该文件。

```
$ .bashrc
```

## System /etc/.bashrc BASH Script

Linux 系统通常包含一个对所有用户执行的系统 .bashrc 文件。它可能包含所有用户在进入 BASH shell 时所需的一定的全局别名和功能。该文件位于 /etc 目录下，/etc/.bashrc。用户自己的 .bashrc 文件位于主目录中，其中包含执行此系统 .bashrc 文件的命令。前面 .bashrc 示例中的 ./etc/bashrc 命令正是如此。

## The BASH Shell Logout File: .bash_logout

.bash_logout 文件也是一个配置文件，在用户注销时执行。它旨在执行你在每次注销时希望完成的操作。与其说是变量定义，.bash_logout 文件通常包含形成一种关闭程序的 shell 命令——在注销前你始终希望执行的操作。一个常见的注销命令是清除屏幕然后发出告别信息。

与 .bash_profile 一样，你可以向 .bash_logout 添加自己的 shell 命令。事实上，当你的账户首次创建时，.bash_logout 文件并不会自动为你设置。你需要使用 Vi 或 Emacs 编辑器自行创建它。然后你可以添加告别信息或其他操作。在下一个示例中，用户在 .bash_logout 文件中有 clear 和 echo 命令。当用户注销时，clear 命令清除屏幕，然后 echo 命令显示信息 "Good-bye for now."

```
.bash_logout
# ~/ .bash_logout
clear
echo "Good-bye for now"
```

## Initialization and Configuration Files

每种类型的 shell 都有其自己的初始化和配置文件集。Bash shell 配置文件之前已讨论过。TCSH shell 使用 .login、.tcshrc、.logout 文件代替 .bash_profile、.bashrc 和 .bash_logout。Z shell 有多个初始化文件：.zshenv、.zlogin、.zprofile、.zshrc 和 .zlogout。见表 9-2 的列表。查阅每个 shell 的手册页以了解它们的通常配置方式。当你安装一个 shell 时，这些文件的默认版本会自动放置在用户的 home 目录中。除了 TCSH shell 外，所有 shell 在变量定义和赋值值的语法上都基本相同，TCSH 使用略有不同的语法，其手册页中有描述。

## TABLE 9-2
Shell Configuration Files

| BASH Shell | Function |
|---|---|
| .bash_profile | Login initialization file |
| .bashrc | BASH shell configuration file |
| .bash_logout | Logout file |
| .bash_history | History file |
| /etc/profile | System login initialization file |
| /etc/bashrc | System BASH shell configuration file |
| /etc/profile.d | Directory for specialized BASH shell configuration files |
| TC SH Shell |  |
| .login | Login initialization file |
| .tcshrc | TC SH shell configuration file |
| .logout | Logout file |
| Z Shell |  |
| .zshenv | Shell login file (first read) |
| .zprofile | Login initialization file |
| .zlogin | Shell login file |
| .zshrc | Z shell configuration file |
| .zlogout | Logout file |
| PDKSH Shell |  |
| .profile | Login initialization file |
| .kshrc | PDKSH shell configuration file |

## Configuration Directories and Files

应用程序经常在用户的主目录中安装配置文件，其中包含特定的配置信息，以使应用程序适应该特定用户的需求。这可能采用以句点开头的单个配置文件形式，也可能是包含多个配置文件的目录。目录名也将以句点开头。例如，Mozilla 在用户的主目录中安装名为 .mozilla 的目录，其中包含配置文件。另一方面，Mail 应用程序使用单个名为 .mailrc 的文件来保存用户设置的别名和功能设置。大多数单个配置文件以字母 rc 结尾。FTP 使用名为 .netrc 的文件。大多数新闻阅读器使用名为 .newsrc 的文件。配置文件中的条目通常由应用程序设置，尽管你通常可以通过编辑文件直接添加条目。应用程序有一组自己的特殊变量，你可以为其定义和赋值。你可以使用 ls -a 命令列出主目录中的配置文件。

