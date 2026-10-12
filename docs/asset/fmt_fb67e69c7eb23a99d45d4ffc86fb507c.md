
```bash
export PATH USER LOGNAME MAIL HISTSIZE INPUTRC
for i in /etc/profile.d/*.sh; do
    if [ -r "$i" ]; then
        $i
    fi
done

unset
unset pathmunge
```

## 配置 BASH Shell：`.bashrc`

`.bashrc` 文件是一个在每次进入 `BASH` shell 或生成 shell 时都会执行的配置文件。如果 `.bashrc` 是你的 shell 登录 shell，那么在登录时，`.bashrc` 会与你的 `.bash_login` 文件一起执行。如果 `BASH` shell 从另一个 shell 启动，`.bashrc` 文件将自动执行，其中包含的变量和别名定义将被定义。如果你进入不同类型的 shell，将执行该 shell 的配置文件。例如，如果你输入 `tcsh` 命令，将执行 `tcsh` 配置文件而不是 `.bashrc`。

# `.bashrc` Bash 脚本

`.bashrc` shell 配置文件实际上在每次生成 `BASH` shell 时都会执行，例如当你运行一个脚本时。换句话说，每当创建一个子壳（subshell）时，`.bashrc` 文件就会执行。这具有导出你在 `.bashrc` 初始化文件中定义的任何本地变量或别名的效果。`.bashrc` 通常包含别名定义以及用于开启 shell 特性的任何特性变量。别名和特性变量在 shell 内部局部定义。但 `.bashrc` 文件在每个 shell 中都定义它们。出于这个原因，`.bashrc` 通常持有你为每个 shell 定义的别名为选项。在本示例中，用户的标准 `.bashrc` 包含了对 shell `/etc/bashrc` 文件的执行。作为添加自定义别名和选项的示例，添加了 `rm`、`cp` 和 `mv` 命令的别名，以及 shell 的 `noclobber` 和 `ignoretty` 选项。对于 root 用户的 `.bashrc`，`rm`、`cp` 和 `mv` 别名已经包含在 root 的 `.bashrc` 中。

```bash
.bashrc
## 源全局定义
if [ -f /etc/bashrc ];
then
. /etc/bashrc
fi
set -o ignoretty
set -o noclobber
alias rm='-i'
alias mv='-i'
alias cp='-i'
```

你可以向你的 `.bashrc` 文件中添加任何你自己的命令或定义。如果你对 `.bashrc` 做了更改，并希望这些更改在当前会话中生效，你需要使用 `.` 或 `source` 命令重新执行该文件。

.bashrc

系统级 `/etc/bashrc` Bash 脚本与 `/etc/profile.d` 目录

Linux 系统使用一个为所有用户执行的系统级 `bashrc` 文件。该文件包含了所有用户每次进入 `BASH` shell 时需要的全局别名和特性。它位于 `/etc` 目录下的 `/etc/bashrc`。用户位于家目录下的 `.bashrc` 文件包含了执行系统 `.bashrc` 文件的命令。在之前的 `.bashrc` 示例中，`/etc/bashrc` 命令执行的就是这一操作。目前，`/etc/bashrc` 文件设置了默认提示符，一个用于终端窗口，另一个用于屏幕界面。随后使用位于 `/etc/profile.d` 目录下的配置文件设置了其他几个别名和变量。如果 shell 不是用户的登录 shell，这些将由 `/etc/bashrc` 执行。

# Bash Shell 退出文件：`.bash_logout`

`.bash_logout` 文件也是一个配置文件，但它是在用户注销时执行的。它的设计是为了在你注销时执行任何你操作。而不是变量定义，`.bash_logout` 文件通常包含形成某种关机程序的命令——即你在注销前总是想要执行的操作。一个常见的退出命令是清除屏幕然后发出一条告别信息。

与 `.bash_profile` 一样，你可以将自己的 shell 命令添加到 `.bash_logout` 中。事实上，`.bash_logout` 文件在你账户首次创建时并不会自动设置的。

# 第5章：Shell 配置

你需要自己使用 `Vi` 或 `Emacs` 编辑器创建它。然后你可以添加一条告别信息或其他操作。在接的示例中，用户在 `.bash_logout` 文件中有一个 `clear` 命令和一个 `echo` 命令。当用户注销时，`clear` 命令清除屏幕，然后 `echo` 命令显示信息“再见”。

```bash
.bash_logout
# ~/.bash_logout
clear
echo "Good-bye now"
```

# TCSH Shell 配置

`TCSH` shell 本质上是增加了功能的 `C` shell 版本。配置操作执行的任务相似但语法略有不同。系统变量使用 `TCSH` 赋值运算符赋值，且初始化和配置文件名称不同。

# TCS/C 别名

你使用 `alias` 命令为命令创建另一个名称。别名就像它所代表的命令宏。别名并没有从上替换命令的名字；它只是提供了另一个名称。

别名命令以关键字 `alias` 开始，后面是命令的新名称，然后是别引用的命令。在下一个示例中，`ls` 命令被别名为 `list`。`list` 变成了 `ls` 命令的另一个名称。

```bash
> alias list ls
> ls
mydata intro
> list
mydata intro
>
```

当你带有选项作为别名时，你也应该将命令和选项包含在单引号内。带有空格的别名命令需要引号。在下一个示例中，带有 `-1` 选项的 `ls` 被赋予别名 `long`：

```bash
> alias longl 'ls -1'
> ls -1
--rw-r--r-- 1 chris we 207 Feb 20 11:55 mydata
> longl
--rw-r--r-- 1 chris we 207 Feb 20 11:55 mydata
```

你可以将命令的名字作为别名。对于 `rm`、`cp` 和 `mv` 命令，应该始终使用 `-i` 选项以确保现有文件不被覆盖。而不是在每次使用这些命令之一时都小心地使用 `-i` 选项。

通过这些命令，你可以将命令名别命名为包含选项。在接下来的示例中，`rm`、`cp` 和 `mv` 命令被别命名为包含 `-i` 选项。

```
> alias rm '-i'
> alias mv '-i'
> alias cp '-i'
```

`alias` 命令本身可以提供所有生效的别名及其对应的命令列表。

可以使用 `unalias` 命令删除别名。

```
alias
ls ls -s
list ls
rm rm -i
unalias ls
```

## TCSH/C Shell 特性变量：Shell 特性

`TCSH` 具有若干功能，允许你控制不同 shell 操作的工作方式。`TCSH` Shell 特性包括 `PDKSH` Shell 中的功能，例如 `noclobber` 选项，用于防止重定向覆盖文件。最常用的功能包括 `echo`、`noclobber`、`ignoreof` 和 `noglob`。`TCSH` 特性通过定义与特性相关的变量来开启或关闭。每个功能都有一个变量名称，例如，通过定义 `noclobber` 变量来开启 `noclobber` 功能。使用 `set` 命令定义变量，使用 `unset` 命令取消定义。要开启 `noclobber` 功能，请执行命令 `set noclobber`；要关闭它，请执行命令 `unset noclobber`。

```
> set feature-variable
> unset feature-variable
```

这些变量有时也被称为开关（toggles），因为它们被用于开启和关闭功能。

### `echo`

设置 `echo` 可以启用在执行命令前显示命令的功能。执行 `set echo` 开启 `echo`，执行 `unset echo` 则将其关闭。

### `ignoreof`

设置 `ignoreof` 可以启用防止用户通过 `CTRL-D` 退出用户 shell 的功能。它旨在防止意外注销。当此功能关闭时，你可以按 `CTRL-D` 退出。然而，`CTRL-D` 也用于直接将用户输入到标准输入。它经常用于 `Mail` 程序或如 `cat` 等实用程序。在这种情况下，你很容易输入一个额外的 `CTRL-D` 并意外注销。使用 `ignoreof` 功能可以防止此类注销。当它开启时，你必须使用 `logout` 命令显式退出：

```
$ set ignoreof
$ CTRL-D
Use logout to logout
$
```

### `noclobber`
