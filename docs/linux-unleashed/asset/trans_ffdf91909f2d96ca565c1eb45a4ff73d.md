
设置好正确的变量后，每当您输入一个 tcsh 无法识别的命令时，它会自动检查该命令是否存在拼写错误。如果它发现可能的拼写错误，它会给出修正后的命令，并询问新的命令是否是您本意想要输入的。例如，如果您使用 all 选项设置了正确的变量，然后输入以下命令：

```
cd /usr/gmes
```

tcsh 会在命令行上显示以下提示：

```
CORRECT>cd /usr/games (y/n/e)?
```

如果您通过按 y（是）键响应此提示，tcsh 将执行修正后的命令。如果您通过按 n（否）键响应此提示，tcsh 将执行您最初输入的命令，这将导致显示一条错误消息。

如果您通过按 e（编辑）键响应此提示，tcsh 会将您输入的命令放回命令行，并允许您对其进行编辑。

## 前置命令

tcsh 支持在显示每个命令提示符之前执行命令的方式。这是通过使用一个名为 precmd 的特殊变量来实现的。如果设置了 precmd 变量，则在其显示到屏幕之前，会先执行该变量所设置的命令。例如，假设您使用以下命令设置了 precmd 变量：

```
alias precmd time
```

声明此别名后，time 命令总是在命令提示符显示到屏幕之前执行。

## 目录更改命令

tcsh 还支持目录更改命令。这些命令仅在当前目录发生变化时（通常是由于执行 cd 命令的结果）才会执行。这种类型的命令可能比前面提到的前置命令更有用，因为有时候您可能想了解刚刚进入的目录的相关信息。

此功能的支持方式与前置命令类似，不同之处在于您必须为另一个变量提供别名。用于此目的的变量是 cwdcmd。如果该变量被别名为某个命令，那么每次您更改当前工作目录时，该命令都会被执行。

此变量的一个常见用途是将当前目录显示在屏幕上。这可以通过输入以下命令来实现：

```
alias cwdcmd 'pwd'
```

每次进入新目录时，这都会显示新目录的名称。

> **警告**
>
> 您不应将 `cd` 命令放入 `cwdcmd` 中。这样做可能会导致无限循环，使您失去对 `tcsh` 的控制。

## 监控登录和注销

`tcsh` 提供了一种机制，允许您监视系统中登录或注销的任何用户。它是通过一个名为 `watch` 的 `tcsh` 变量来实现的。

`watch` 变量包含一组用户 ID 和终端编号对。这些对可以包含通配符，也可以包含单词“any”，该单词告诉 `tcsh` 匹配任何用户或终端。设置 `watch` 变量的语法如下：

```
set watch=(<user> <terminal>)
```

此命令中的 `user` 指的是 Linux 用户 ID。`terminal` 指的是 Linux 终端设备编号。

大多数人使用此功能来监视朋友登录系统。例如，如果您正等待用户名为 `jules` 的人早上来上班，您可以设置如下 `watch` 变量：

```
set watch=(jules any)
```

此命令随后会在用户 ID 为 `jules` 的人员在任何终端上登录系统时通知您。`tcsh` 默认每 10 分钟检查一次定义的监视对象。如果您希望以更高或更低的频率获取信息，您可以通过将两次检查之间等待的分钟数作为第一个参数传递给 `watch` 变量来更改此默认设置。例如，要每五分钟检查一次“jules”是否已登录，您可以使用以下 `watch` 变量：

```
set watch=(5 jules any)
```

这与第一个命令执行相同的功能，除了它每 5 分钟检查一次（而不是每 10 分钟）以查看“jules”是否已登录。在负载较重或缓慢的 Linux 系统上使用此类型的命令时要小心，因为您正在增加系统负载。如果您是出于特定目的在短时间范围内使用这些命令，那没问题，但不要让它们无休止地运行，否则您将在没有正当理由的情况下增加系统负载。

## 自定义 tcsh

在本章中，我们展示了自定义 tcsh 的许多方法。如果您只是在命令行中输入我们讨论过的命令，那么您所做的更改在每次注销系统时都会丢失。本节描述如何将这些更改存储在每次启动 tcsh 时都会执行的文件中。

> **提示**
>
> 如果您在编辑 tcsh 文件时即使犯下微小的错误，也可能导致登录时出现问题。因此，在编辑前请制作安全备份副本，并在保存新文件之前仔细验证您的每一处编辑。

tcsh 有两个重要的初始化文件。第一个称为登录文件。当首次登录到 Linux 时，此文件中的命令会执行。默认登录文件的内容如下：

```
if ($?prompt) then
#this means that the shell is interactive
umask 022
set cdpsh = ( /usr/spool )
set notify
set history = 100
set histfile = .history
# The savehist variable is set to tell tcsh to
# save the history list to the history file on
# logout. The value of 25 means that tcsh will
# save the last 25 commands to the history file.
set savehist = 25
setenv OPENWINHOME /usr/openwin
setenv MANPATH /usr/local/man:/usr/man/preformat:/usr/man:/usr/X11/man:/usr/openwin/man
setenv MINICOM "-c on"
setenv HOSTNAME "`cat /etc/HOSTNAME`"
set path = ( $path /usr/X11/bin /usr/andrew/bin $OPENWINHOME/bin /usr/games .)
end
# I had problems with the Backspace key installed by 'tset,' but you might
# want to try it anyway, instead of the `setenv term...` below it.
# eval `tset -sQ "$term"`
# setenv term console
if ! $?TERM setenv TERM console
set prompt = "%m:%~-%# "
alias ls 'ls -F'
if ( { tty --silent } ) then >& /dev/null
 echo "";fortune;echo ""
endif
```

这个名为 `csh.login` 的文件可以在 `/etc` 目录中找到。如果您想要更改 `csh.login` 中的任何设置，请将其复制到您的主目录，并在那里进行您想要的更改。

`tcsh` 使用的另一个文件是 `cshrc`。此文件中的命令在每次运行 `tcsh` 程序的副本时都会执行。通常出现在此文件中的命令类型示例包括别名和变量声明。这个名为 `csh.cshrc` 的文件也包含在 `/etc` 目录中。如果您想要对此文件进行修改，请将其复制到您的主目录并在那里进行修改。

首次登录到 Linux 时，`tcsh` 先执行 `/etc/csh.cshrc` 文件，然后执行 `/etc/csh.login` 文件。接着它检查您的主目录，查看您是否拥有 `csh.cshrc` 文件的个人副本。此文件可以命名为 `.tcshrc` 或 `.cshrc`。如果您的主目录中有这些文件之一，`tcsh` 接下来会执行它。

然后 `tcsh` 检查您是否在主目录中拥有自己的 `csh.login` 文件副本。此文件必须命名为 `.login`。如果您的主目录中有一个 `.login` 文件，它将接下来被执行。

每当您在登录系统后启动另一个 `tcsh` 副本时，它会执行 `/etc/csh.cshrc` 文件中的命令，然后检查您的主目录，查看那里是否有一个 `.tcshrc` 或 `.cshrc` 文件。

## tcsh 命令摘要

以下是一些最实用的 `tcsh` 命令：

- `alias`：用于设置和显示别名，即用户可设置的命令昵称。
- `bg`：后台命令。强制已挂起的进程在后台继续运行。
- `bindkey`：允许用户更改与按键序列相关的编辑操作。
- `cd`：将当前工作目录更改为指定的目录。
- `exit`：终止 shell。
- `fg`：前台命令。强制已挂起的进程在前台继续运行。
- `history`：允许用户显示和修改历史列表和历史文件的内容。
- `kill`：终止另一个进程。
- `logout`：终止登录 shell。
- `set`：用于设置 tcsh 变量的值。
- `source`：读取并执行文件的内容。此命令在第 14 章中有更详细的讨论。
- `unalias`：用于移除使用 alias 命令定义的别名。

## tcsh 变量

以下是一些最实用的 tcsh 变量：

- `autocorrect`：如果已设置，tcsh 会自动尝试更正命令行拼写错误。
- `histfile`：用于存储命令历史的文件名称。
- `history`：历史列表的大小。
- `home`：用户的主目录。
- `path`：tcsh 在查找可执行程序时使用的搜索路径。
- `prompt`：显示在命令行的第一级提示符。
- `prompt2`：当 for、foreach 或 while 循环期待输入时显示的第二级提示符。
- `prompt3`：当 tcsh 尝试更正命令中的拼写错误时显示的第三级提示符。
- `savehist`：如果您希望 tcsh 在注销时保存历史列表，则此变量必须设置为您想要保存的历史命令数量。
- `watch`：包含要监视登录和注销的用户终端对列表。

![](img/e8e6b47ac20475e23d48b4c476f5d891_296_0.png)
