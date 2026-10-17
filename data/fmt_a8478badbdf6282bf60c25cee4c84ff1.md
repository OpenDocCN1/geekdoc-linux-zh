
`shell` 函数类似于 `shell` 脚本，因为它保存了一系列命令以便稍后执行。然而，由于 `shell` 将函数存储在计算机的主内存 (RAM) 中而不是磁盘上的文件中，`shell` 访问函数比访问脚本更快。此外，`shell` 还会对函数进行预处理（解析），使其比脚本启动得更快。最后，`shell` 在调用它的同一个 `shell` 中执行 `shell` 函数。如果你定义了太多的函数，启动子 `shell`（如运行脚本时那样）的开销可能变得不可接受。

你可以在 `~/.bash_profile` 启动文件中、使用它的脚本中，或者直接在命令行上声明 `shell` 函数。你可以使用 `unset` 内建命令删除函数。退出登录后，`shell` 不会保留函数。

### 删除同名变量和函数

> 如果你有一个 `shell` 变量和一个同名函数，使用 `unset` 会删除 `shell` 变量。如果你再次使用相同名称的 `unset`，则会删除该函数。

声明 `shell` 函数的语法如下：

```bash
[function] function-name () {
  commands
}
```

其中，单词 `function` 是可选的（并且通常被省略；它不具备可移植性），`function-name` 是你用于调用函数的名称，而 `commands` 则是函数在被调用时执行的命令列表。这些命令可以是 `shell` 脚本中包含的任何内容，包括对其他函数的调用。

左花括号 `{` 可以出现在函数名称的下一行。别名和变量在函数被读取时而不是被执行时进行展开。你可以在函数内使用 `break` 语句（见第 1005 页）来终止其执行。

你可以在单行上声明一个函数。由于右花括号必须作为单独的命令出现，当你使用此语法时，必须在右花括号前放置一个分号：

```bash
$ say_hi() { echo "hi"; }
$ say_hi
hi
```

`shell` 函数不仅作为一种简写形式很有用，还可以用来定义特殊命令。以下函数在后台启动一个名为 `process` 的进程，并将 `process` 正常显示的输出保存到 `.process.out` 中。

```bash
start_process() {
  process > .process.out 2>&1 &
}
```

下一个示例创建了一个简单的函数，显示日期、标题以及系统中已登录用户列表。此函数执行的命令与第 337 页描述的 `whoson` 脚本相同。在这个示例中，函数是从键盘输入的。大于号 (`>`) 是二级 `shell` 提示符 (`PS2`)；请勿输入它们。

```bash
$ function whoson () {
>   date
>   echo "Users Currently Logged On"
>   who
> }
$ whoson
Fri Aug  9 15:44:58 PDT 2013
Users Currently Logged On
hils    console    2013-08-08 08:59  (:0)
max     pts/4      2013-08-08 09:33  (0.0)
zach    pts/7      2013-08-08 09:23  (guava)
```

你只能在函数内部使用 `local` 内建命令。此内建命令使其参数对于调用它的函数及其子进程具有局部性。如果没有 `local`，在函数中声明的变量对调用该函数的 `shell` 是可见的（函数在其被调用的 `shell` 中运行）。以下函数演示了 `local` 的用法。

```bash
$ demo () {
>   x=4
>   local y=8
>   echo "demo: $x $y"
> }
$ demo
demo: 4 8
$ echo $x
4
$ echo $y

$
```

从键盘输入的 `demo` 函数声明了两个变量 `x` 和 `y`，并显示它们的值。变量 `x` 使用常规赋值语句声明，而 `y` 使用 `local` 声明。运行函数后，调用该函数的 `shell` 可以访问 `x`，但对 `y` 一无所知。有关函数局部变量的另一个示例，请参见第 1040 页。

`export -f` 命令将指定的函数放入环境中，使其对子进程可用。

如果你希望 `whoson` 函数无需每次登录时都手动输入即可使用，请将其定义放入 `~/.bash_profile`。然后使用 `.` (点) 命令运行 `.bash_profile`，立即使更改生效：

```bash
$ cat ./.bash_profile
export TERM=v100
stty kill '^Au'
whoson () {
  date
  echo "Users Currently Logged On"
  who
}

$ . ./.bash_profile
```

在调用函数时，您可以指定参数。在函数内部，这些参数作为位置参数（第 1022 页）可用。以下示例展示了从键盘输入的 `arg1` 函数：

```
$ arg1 ( { echo "$1"; })
$ arg1 first_arg
first_arg
```

关于函数的另一个示例，请参阅第 332 页中的 `switch` 函数。

**可选** 以下函数允许您使用 `tcsh` 语法将变量放入环境（导出它们）。`env` 实用程序会列出所有环境变量及其值，并验证 `setenv` 是否正常工作：

```
$ cat .bash_profile
...
# setenv - keep tcsh users happy
setenv() {
    if [ $# -eq 2 ]
    then
        eval $1=$2
        export $1
    else
        echo "Usage: setenv NAME VALUE" 1>&2
    fi
}
$ . ~/.bash_profile
$ setenv TCL_LIBRARY /usr/local/lib/tcl
$ env | grep TCL_LIBRARY
TCL_LIBRARY=/usr/local/lib/tcl
```

特殊参数 `$#`（第 1027 页）取值为命令行参数的数量。此函数使用 `eval` 内建命令强制 `bash` 对命令 `$1=$2` 进行*两次*扫描。由于 `$1=$2` 以美元符号 ($) 开头，`Shell` 将整个字符串视为单个标记——一条命令。在执行变量替换后，命令名称变为 `TCL_LIBRARY=/usr/local/lib/tcl`，这会导致错误。使用 `eval` 时，第二次扫描会将字符串拆分为三个期望的标记，从而发生正确的赋值。有关 `eval` 的更多信息，请参阅第 1051 页。

## 控制 `bash`：特性与选项

本节解释如何使用命令行选项以及 `set` 和 `shopt` 内建命令来控制 `bash` 的特性和选项。`Shell` 会设置标志以指示哪些选项已启用（打开），并将 `$-` 扩展为已设置标志的列表；有关更多信息，请参阅第 1030 页。

### `bash` 命令行选项

您可以指定短命令行选项和长命令行选项。短选项由连字符后跟一个字母组成；长选项由两个连字符后跟多个字符组成。在调用 *`bash`* 的命令行中，长选项必须出现在短选项之前。表 9-12 列出了常用的一些命令行选项。

**表 9-12** *`bash`* 命令行选项

| 选项 | 说明 | 语法 |
| --- | --- | --- |
| 帮助 | 显示用法消息。 | `--help` |
| 无编辑 | 防止用户在交互式 `Shell` 中使用 `Readline` 库（第 386 页）编辑命令行。 | `--noediting` |
| 无配置文件 | 防止读取这些启动文件（第 329 页）：`/etc/profile`、`~/.bash_profile`、`~/.bash_login` 和 `~/.profile`。 | `--noProfile` |
| 无 rc | 防止读取 `~/.bashrc` 启动文件（第 331 页）。如果 `Shell` 以 `sh` 身份被调用，此选项默认开启。 | `--norc` |
| POSIX | 以 POSIX 模式运行 *`bash`*。 | `--posix` |
| 版本 | 显示 *`bash`* 的版本信息并退出。 | `--version` |
| 登录 | 使 *`bash`* 如同登录 `Shell` 一样运行。 | `-l`（小写字母 “el”） |
| `shopt` | 带有 `opt` `shopt` 选项（见下一页）运行 `Shell`。`-0`（大写字母 “O”）设置该选项；`+0` 取消设置该选项。 | `[+-]0 [opt]` |
| 选项结束 | 在命令行中，表示选项结束。后续标记被视为参数，即使它们以连字符 (-) 开头。 | `--` |

### `SHELL` 特性

您可以通过打开和关闭特性来控制 `Bourne Again Shell` 的行为。不同的方法开启和关闭不同的特性：*`set`* 内建命令控制一组特性，而 *`shopt`* 内建命令控制另一组特性。您还可以从用于调用 *`bash`* 的命令行控制许多特性。

**特性、选项、变量、属性？**

> **提示** 为了避免术语混淆，本书将您可以控制的各种 `Shell` 行为称为特性。*`bash info`* 页面将它们称为“选项”和“控制可选 `Shell` 行为的变量值”。在某些地方，您可能会看到它们被称为*属性*。

## `set +o`：开关 `Shell` 特性

`set` 内建命令在与 `-o` 或 `+o` 选项一起使用时，可以启用、禁用和列出某些 `bash` 特性。例如，以下命令开启了 `noclobber` 特性（第 156 页）：

```
$ set -o noclobber
```

您可以通过执行以下命令来关闭此特性（默认状态）：

```
$ set +o noclobber
```

不带选项的命令 `set -o` 会列出 `set` 控制的每个特性，随后显示其状态（开启或关闭）。不带选项的命令 `set +o` 以您可以用作 `Shell` 输入的形式列出相同的特性。表 9-13 列出了 `bash` 特性。此表未列出 `-i` 选项，因为您无法设置它。当 `Shell` 作为交互式 `Shell` 被调用时，`Shell` 会设置此选项。有关 `set` 其他用途的讨论，请参阅第 1024 页。

## `shopt`：开关 `Shell` 特性

`shopt`（`Shell` 选项）内建命令可以启用、禁用和列出控制 `Shell` 行为的某些 `bash` 特性。例如，以下命令导致 `bash` 在扩展模糊文件引用时包含以点 (.) 开头的文件名（`-s` 代表 `set`）：

```
$ shopt -s dotglob
```

您可以通过执行以下命令来关闭此特性（默认状态）（`-u` 代表 `unset`）：

```
$ shopt -u dotglob
```

如果您将特性名称作为 `shopt` 的唯一参数，`Shell` 会显示该特性的设置状态：

```
$ shopt dotglob
          dotglob off
```

如果不带任何选项或参数，`shopt` 会列出其控制的特性及其状态。不带参数的命令 `shopt -s` 列出由 `shopt` 控制且已设置或开启的特性。命令 `shopt -u` 列出未设置或关闭的特性。表 9-13 列出了 `bash` 特性。

## 使用 `shopt` 设置 `set +o` 特性

> **提示** 您可以使用 `shopt` 来设置/取消设置通常由 `set +o` 控制的特性。使用常规的 `shopt` 语法，使用 `-s` 或 `-u` 并包含 `-o` 选项。例如，以下命令开启了 `noclobber` 特性：

```
$ shopt -o -s noclobber
```

## 表 9-13 `bash` 特性

| 特性 | 描述 | 语法 | 替代语法 |
|---|---|---|---|
| `allexport` | 执行此命令后，自动将您创建或修改的所有变量和函数放入环境中（导出）（默认关闭）。 | `set -o allexport` | `set -a` |
| `braceexpand` | 导致 *`bash`* 执行花括号扩展（默认开启；第 405 页）。 | `set -o braceexpand` | `set -B` |
| `cdspell` | 纠正用作 *`cd`* 参数的目录名称中的轻微拼写错误（默认关闭）。 | `shopt -S cdspell` | |
| `cmdhist` | 将多行命令的所有行保存在同一历史记录条目中，必要时添加分号（默认开启）。 | `shopt -S cmdhist` | |
| `dotglob` | 导致 `Shell` 特殊字符（通配符；第 165 页）在模糊文件引用中匹配文件名中的前导点。默认情况下，特殊字符不匹配前导点：因为没有任何模式匹配它们，所以必须始终显式指定文件名 `.` 和 `..`（默认关闭）。 | `shopt -S dotglob` | |
| `emacs` | 指定命令行编辑的 *`emacs`* 编辑模式（默认开启；第 387 页）。 | `set -o emacs` | |
| `errexit` | 导致 *`bash`* 在管道（第 158 页）失败时退出，管道可以是简单命令（第 147 页；不是控制结构）（默认关闭）。 | `set -o errexit` | `set -e` |
| `execfail` | 导致 `Shell` 脚本在找不到 *`exec`* 给定参数指定的文件时继续运行。默认情况下，当 *`exec`* 找不到给定参数指定的文件时，脚本会终止（默认关闭）。 | `shopt -S execfail` | |
| `expand_aliases` | 导致别名（第 392 页）被扩展（默认在交互式 `Shell` 中开启，在非交互式 `Shell` 中关闭）。 | `shopt -S expand_aliases` | |
| `hashall` | 导致 *`bash`* 记住使用 *`PATH`*（第 359 页）找到的命令所在位置（默认开启）。 | `set -o hashall` | `set -h` |

## 表 9-13 `bash` 特性（续）

| 特性 | 描述 | 语法 | 替代语法 |
| :-- | :-- | :-- | :-- |
| `histappend` | 使 `bash` 在 `shell` 退出时将历史列表追加到由 `HISTFILE` 指定的文件中（第 377 页）（默认关闭 [`bash` 会覆盖此文件]）。 | `shopt` -s histappend | |
| `histexpand` | 开启历史机制（默认使用感叹号；第 381 页）。关闭此功能以禁用历史扩展（默认开启）。 | `set` -o histexpand | `set` -H |
| `history` | 启用命令历史记录（默认开启；第 376 页）。 | `set` -o history | |
| `huponexit` | 指定 `bash` 在交互式登录 `shell` 退出时向所有作业发送 `SIGHUP` 信号（默认 **关闭**）。 | `shopt` -s huponexit | |
| `ignoreeof` | 指定 `bash` 必须接收十个 `EOF` 字符才能退出。适用于嘈杂的拨号线路（默认关闭）。 | `set` -o ignoreeof | |
| `monitor` | 启用作业控制（默认开启；第 346 页）。 | `set` -o monitor | `set` -m |
| `nocaseglob` | 使模糊文件引用（第 165 页）在不区分大小写的情况下匹配文件名（默认关闭）。 | `shopt` -s nocaseglob | |
| `noclobber` | 帮助防止覆盖文件（默认关闭；第 156 页）。 | `set` -o noclobber | `set` -C |
| `noglob` | 禁用路径名扩展（默认关闭；第 165 页）。 | `set` -o noglob | `set` -f |
| `notify` | 在启用作业控制（第 346 页）的情况下，立即报告后台作业的终止状态（默认关闭：`bash` 仅在下一个提示符显示前显示状态）。 | `set` -o notify | `set` -b |
| `nounset` | 当 `shell` 试图扩展一个未设置的变量时显示错误；`bash` 会从脚本中退出，但不会从交互式 `shell` 中退出（默认关闭：`bash` 为未设置的变量替换空值）。 | `set` -o nounset | `set` -u |
| `nullglob` | 使 `bash` 为未匹配文件名的模糊文件引用（第 165 页）替换空字符串（默认关闭；`bash` 原样传递这些文件引用）。 | `shopt` -s nullglob | |
| `pipefail` | 将管道线的退出状态设置为该管道中最后一个（最右侧）失败的简单命令（返回非零退出状态）的退出状态；如果没有命令失败，退出状态设置为零（默认关闭）。`bash` 将管道线的退出状态设置为管道中最后一个命令的退出状态。 | `set` -o pipefail` | |
| `posix` | 在 POSIX 模式下运行 `bash`（默认关闭）。 | `set` -o posix` | |
| `verbose` | 在 `bash` 读取命令行后、扩展之前显示每一行命令（默认关闭）。另见 `xtrace`。 | `set` -o verbose` | `set` -v |
| `vi` | 指定 `vi` 编辑模式用于命令行编辑（默认关闭；第 386 页）。 | `set` -o vi` | |
| `xpg_echo` | 使 `echo` 内建命令无需 `-e` 选项即可展开反斜杠转义序列（默认关闭；第 1009 页）。 | `shopt` -s xpg_echo` | |
