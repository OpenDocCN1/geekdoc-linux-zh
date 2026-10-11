
## 环境变量列表

| `HOSTFILE` | 当 shell 需要完成主机名时应读取的文件名 |
| `HOSTNAME` | 当前主机的名称 |
| `HOSTTYPE` | 描述 Bash shell 所运行机器的字符串 |
| `IGNOREEOF` | shell 在退出之前必须接收的连续 EOF 字符数（如果此值不存在，默认值为 1） |
| `INPUTRC` | Readline 初始化文件的名称（默认为 `.inputrc`） |
| `INSIDE_EMACS` | 仅在进程在 Emacs 编辑器 shell 缓冲区中运行时设置，可禁用行编辑（禁用行编辑还取决于 `TERM` 变量的值） |
| `LANG` | shell 的区域设置类别 |
| `LC_ALL` | 覆盖 `LANG` 变量，定义区域设置 |
| `LC_COLLATE` | 设置对排序字符串值使用的排序顺序 |
| `LC_CTYPE` | 确定文件名扩展和模式匹配中使用的字符解释 |
| `LC_MESSAGES` | 确定解释由美元符号开头的双引号字符串时使用的区域设置 |
| `LC_NUMERIC` | 确定格式化数字时使用的区域设置 |
| `LC_TIME` | 确定格式化数据和时间时使用的区域设置 |
| `LINO` | 当前正在执行的脚本中的行号 |
| `LINES` | 定义终端上可用的行数 |
| `MACHTYPE` | 以 cpu-company-system 格式定义系统类型的字符串 |
| `MAILCHECK` | shell 应检查新邮件的频率（以秒为单位）（默认为 60） |
| `MAPFILE` | 当未提供数组变量名称时，从 `mapfile` 命令读取文本的数组变量 |
| `OLDPWD` | shell 中使用的上一个工作目录 |
| `OPTERR` | 如果设置为 1，Bash shell 将显示由 `getopt` 命令生成的错误。 |
| `OSTYPE` | 定义 shell 所运行操作系统的字符串 |
| `PIPESTATUS` | 包含前台进程中退出状态值列表的变量数组 |
| `POSIXLY_CORRECT` | 如果设置，Bash 以 POSIX 模式启动。 |
| `PPID` | Bash shell 父进程的进程 ID (PID) |
| `PROMPT_COMMAND` | 如果设置，则是在显示主提示之前执行的命令 |
| `PROMPT_DIRTRIM` | 用于指示在使用 `\w` 和 `\W` 提示字符串转义时要显示多少尾部目录名称的整数（被移除的目录名称将由一组省略号替换） |
| `PS0` | 如果设置，内容将由交互式 shell 在命令输入后但在命令执行前显示。 |
| `PS3` | `select` 命令使用的提示 |
| `PS4` | 如果使用 Bash `-x` 参数，则在命令行被回显之前显示的提示 |
| `PWD` | 当前工作目录 |
| `RANDOM` | 返回 0 到 32767 之间的随机数（为此变量赋值会播种伪随机数生成器） |
| `READLINE_LINE` | 使用 `bind -x` 命令时 Readline 缓冲区的内容 |
| `READLINE_POINT` | 使用 `bind -x` 命令时 Readline 缓冲区内容插入点的位置 |
| `REPLY` | `read` 命令的默认变量 |
| `SECONDS` | shell 启动以来的秒数（赋值会重置计时器为该值） |
| `SHELL` | Bash shell 的完整路径名 |
| `SHELOPTS` | 已启用的 Bash shell 选项的冒号分隔列表 |
| `SHLVL` | 指示 shell 级别，每次启动新的 Bash shell 时递增一次 |
| `TIMEFORMAT` | 指定 shell 如何显示时间值的格式 |
| `TMOUT` | `select` 和 `read` 命令等待输入的时长（以秒为单位）的值（默认值 0 表示无限期等待） |
| `TMPDIR` | Bash shell 创建临时文件供其使用的目录名 |
| `UID` | 当前用户的真实用户数字 ID |

你可能会注意到，当使用 `set` 命令时，并非所有默认环境变量都会显示出来。当未使用时，默认环境变量不需要包含值。

### 注意

> 默认环境变量是否在系统中使用有时取决于正在运行的 Bash shell 版本。例如，`EPOCHREALTIME` 仅在 Bash shell 版本 5 及以上版本中可用。你可以通过在 CLI 中输入 `bash --version` 并按 Enter 键来查看你的 Bash shell 版本号。

### 设置 PATH 环境变量

当你在 shell CLI 中输入外部命令（参见第 5 章，“理解 Shell”）时，shell 必须搜索系统以找到程序。`PATH` 环境变量定义了它查找命令和程序的目录。在这个 Ubuntu Linux 系统中，`PATH` 环境变量看起来是这样的：

```bash
$ echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
$
```

`PATH` 中的目录由冒号分隔。这表明有九个目录，shell 在其中查找命令和程序。

如果命令或程序的位置未包含在 `PATH` 变量中，shell 在没有绝对目录引用的情况下无法找到它。如果 shell 无法找到命令或程序，它会产生一条错误消息：

```bash
$ myprog
myprog: command not found
$
```

问题是，有时应用程序会将它们的可执行程序放在不在 `PATH` 环境变量中的目录里。诀窍是确保你的 `PATH` 环境变量包含你的应用程序所在的所有目录。

> **注意**
>
> 一些脚本构建者在 Bash shell 脚本的第一行使用 *env* 命令（在**第 11 章**，“基本脚本构建”中介绍），如下所示：`#!/usr/bin/env bash`。这种方法的优点是 *env* 实用程序在 `$PATH` 目录中搜索 *bash* shell 程序，使脚本更具可移植性到其他 Linux 发行版。

你可以将新的搜索目录添加到现有的 `PATH` 环境变量中，而不必从头开始重建它。`PATH` 中列出的各个目录由冒号分隔。你所要做的只是引用原始的 `PATH` 值，添加一个冒号 `:`，并使用绝对目录引用输入新目录。在 CentOS Linux 系统中，它看起来是这样的：

```bash
$ ls /home/christine/Scripts/
myprog
```

```
$ echo $PATH
/home/christine/.local/bin:/home/christine/bin:/usr/local/bin:
$
$ PATH=$PATH:/home/christine/Scripts
$
$ myprog
5 的阶乘是 120
$
```

通过将目录添加到 `PATH` 环境变量中，你现在可以在虚拟目录结构的任何位置执行你的程序：

```
$ cd /etc
$ myprog
5 的阶乘是 120
$
```

> **提示**
>
> 如果你希望你的程序位置对子 shell 可用，请务必导出你修改后的 `PATH` 环境变量。

对 `PATH` 变量的更改仅持续到你退出系统或系统重启为止。这些更改不是持久的。在下一节中，你将看到如何使环境变量的更改永久化。

### 定位系统环境变量

Linux 系统使用环境变量来实现许多功能。你现在已经知道如何修改系统环境变量以及创建自己的变量。关键在于这些环境变量如何被持久化。

当你登录 Linux 系统启动 Bash shell 时，默认情况下 Bash 会检查几个文件中的命令。这些文件称为启动文件或环境文件。Bash 处理哪些启动文件取决于你启动 Bash shell 的方式。启动 Bash shell 有三种方式：

- 作为登录时的默认登录 shell
- 作为通过生成子 shell 启动的交互式 shell
- 作为运行脚本的非交互式 shell

以下部分描述了 Bash shell 在每种启动方法中执行的启动文件。

#### 理解登录 shell 流程

当你登录 Linux 系统时，Bash shell 作为*登录 shell* 启动。登录 shell 通常查找五个不同的启动文件来处理命令：

- `/etc/profile`
- `$HOME/.bash_profile`
- `$HOME/.bashrc`
- `$HOME/.bash_login`
- `$HOME/.profile`

`/etc/profile` 文件是系统中 Bash shell 的主要默认启动文件。系统上的所有用户在登录时都会执行此启动文件。

> **注意**
