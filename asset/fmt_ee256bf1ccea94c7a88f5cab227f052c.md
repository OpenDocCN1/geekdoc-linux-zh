
2367 pts/0 00:00:00 `bash`

5240 pts/0 00:00:00 _ `ps`

`$ !!`

`ps --forest`

PID TTY TIME CMD

2367 pts/0 00:00:00 `bash`

5241 pts/0 00:00:00 _ `ps`

当输入 `!!` 时，Bash 首先显示它从 shell 历史记录中回溯的命令。在显示命令后，它会被执行。

命令历史记录在隐藏的 `.bash_history` 文件中，该位于每个用户的家目录下：

```
$ pwd
/home/christine
$
$ ls .bash_history
.bash_history
$
```

请注意，在 CLI 会话期间，bash 命令历史存储在内存中。只有在退出 shell 时，它才会写入历史文件：

```
$ history
1 ps -f
2 pwd
[...]
38 exit
39 history
40 ps --forest
41 ps --forest
42 pwd
43 ls .bash_history
44 history
```

## 第一部分：Linux命令行

```
$ cat .bash_history
ps -f
pwd
[...]
ls
history
exit
$
```

注意，当运行 `history` 命令时，最后显示的命令与 `.bash_history` 文件中的最终命令并不匹配。在此期间额外发布了六条命令，这些命令没有记录在历史文件中。

你可以在不离开 shell 会话的情况下强制将命令历史记录写入 `.bash_history` 文件。为了实现这一点，请对 `history` 命令使用 `-a`：

```
$ history -a
$
$ history
  1 ps -f
  2 pwd
...
38 exit
39 history
40 ps --forest
41 ps --forest
42 pwd
43 ls .bash_history
44 history
45 cat .bash_history
46 history
47 history
```

## 使用 aliases

## 第5章：理解 Shell

```
1415519 my_script      16789592 Videos
1415015 my_script
$
```

在定义了一个别名 `alias` 值后，你可以在 shell 中随时使用它，包括在 shell 脚本中。请注意，命令别名是内置命令，别名仅对定义它的 shell 进程有效：

```
$ alias li='ls -i'
$ bash
$ li
bash: li: command not found.
$
$ exit
$ li
```

```
14366552 Desktop      1415018 NetworkManager.conf
1414976 Desktop.tar     50350618 OldDocuments
[...
1415524 my_script      1415017 test_two
1415519 my_script      16789592 Videos
1415015 my_script
$
```

> 如果需要，你可以在命令行中输入 `unalias alias-name` 来关闭别名。请记住，如果该别名不是你设置的，当你下次登录系统时它将会被重新开启。你可以修改环境文件来永久禁用别名。环境文件将在第6章介绍。

幸运的是，你可以让别名值跨子 shell。下一章将介绍如何实现，以及环境变量。

### 总结

本章讨论了复杂的交互程序 GNU Bash shell。我们涵盖了 shell 进程及其关系，包括子 shell 如何产生以及它们与父 shell 的关系。我们还探索了创建子进程的命令以及不创建的命令。

当用户登录终端时，通常会启动默认交互式 shell。系统启动的 shell 取决于用户 ID 配置。通常，它是 `/usr/bin/bash`。默认系统 shell `/usr/bin/sh` 用于系统脚本，例如启动时所需的脚本。

# 第一部分：Linux 命令行

可以使用 `bash` 命令创建子 shell 或子 shell。当使用进程列表或 `coproc` 命令时，也会创建这些 shell。在命令行中使用子 shell 可以对 CLI 进行更具创造力且高效的使用。子 shell 可以嵌套，产生孙子 shell 和曾孙子 shell。创建一个子 shell 是一个昂贵的过程，因为必须为 shell 创建一个新的环境。

最后，我们查看了两种不同类型的 shell 命令：内置命令和外部命令。外部命令会创建一个带有新环境的子进程，而内置命令不会。这导致外部命令的使用开销更大。因为不需要新环境，内置命令更高效，且不受任何环境变化的影响。

Shell、子 shell、进程和派生进程 `forked processes` 都受到环境变量的影响。这些变量如何影响以及如何在这些不同语文中被使用，将在下一章进行探讨。

## 使用 Linux 环境变量

### 本章内容
- 查看环境变量
- 创建你自己的本地变量
- 变量
- 探索默认环境变量
- 设置 PATH
- 定位环境文件
- 使用数组

环境变量有助于定义你的 shell 体验。许多程序和脚本使用环境变量来获取系统信息并存储临时数据。环境变量在 Linux 系统的许多地方被设置，了解它们的位置是有帮助的。

本章将带你进入环境变量的世界，展示它们在哪里、如何使用它们，以及如何创建你自己的变量。本章以如何使用数组作为结束。

## 探索环境变量

Bash shell 使用一种名为环境变量的特性来存储关于 shell 会话和工作环境的信息。该特性允许你向内存中存储数据，任何从 shell 运行的程序或脚本都可以轻松访问。Bash shell 中有两种类型的环境变量：
- 全局变量
- 本地变量

# 第一部分：Linux 命令行

本节描述了每种类型的环境变量并展示了如何查看它们。

> 虽然 Bash shell 使用的是一致的环境变量，但不同的发行版会添加它们自己的环境变量。你在本章看到的示例可能与你特定发行版上提供的内容略有不同。

### 查看全局环境变量

全局环境变量在 shell 会话和任何产生的子 shell 中都是可见的。本地变量仅在创建它的 shell 中可用。这一事实使得全局变量在创建子 shell 的应用程序中非常有用，因为这些程序需要父 shell 的信息。Linux 系统在你启动会话时会设置几个全局环境变量。有关此时启动了哪些更多详细信息，请参见本章后后的“定位环境变量”部分。环境变量几乎使用大写字母来区分于用户定义的变量。

要查看全局环境变量，请使用 `env` 或 `printenv` 命令：

```
$ printenv
...
USER=christine
...
PWD=/home/christine
HOME=/home/christine
...
TERM=xterm
SHELL=/bin/bash
...
HISTSIZE=1000
...
$
```

Bash shell 设置了许多全局环境变量。不仅在登录过程中设置了许多变量，你登录的方式也会影响哪些变量被设置。要显示单个环境变量的值，你可以使用 `printenv` 命令，而不是 `env` 命令：

```
$ printenv HOME
/home/christine
```

## 第6章：使用 Linux 环境变量

```
$ $HOME
$ env 'HOME': No such file or directory
$
```

你也可以使用 `echo` 命令来显示变量的值。在这种情况下，引用环境变量时，你必须在环境变量之前放置一个美元符号 `$`。

```
$ echo $HOME
/home/christine
$
```

使用美元符号配合变量名可以将该变量作为参数传递给各种命令，而不仅仅是显示其当前定义：

| Desktop | Music NetworkManager.conf |
| :--- | :--- |
| Doc.tar | OldDocuments |
| Documents | Pictures |
| Downloads | my_script |
| file | test_one |
| file_long_name | Videos |
| link_test_file | |
| really_long_name | |

正如之前所述，全局环境变量对任何进程的子 shell 都是的：

```
$ bash
$ ps -f
UID PID C STIME TTY CMD
christie+ 2770 2766 0 11:19 pts/0 00:00:00 -bash
christie+ 2981 2770 4 11:37 pts/0 00:00:00 bash
```
