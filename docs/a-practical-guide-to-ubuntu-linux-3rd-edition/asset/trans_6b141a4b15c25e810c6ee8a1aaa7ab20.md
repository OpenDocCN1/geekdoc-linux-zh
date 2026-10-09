
与其调用者相同的 shell 中运行。如果你定义了过多的函数，启动子 shell（如运行脚本时）的开销可能会变得不可接受。你可以在 `~/.bash_profile` 启动文件中、使用函数的脚本中，或者直接从命令行声明一个 shell 函数。你可以使用 `unset` 内建命令移除函数。注销后，shell 不会保留函数。

## 移除变量和函数

**提示** 如果你有一个 shell 变量和一个函数具有相同的名称，使用 `unset` 会移除 shell 变量。如果你再次使用 `unset` 处理相同的名称，它将移除该函数。

声明 shell 函数的语法如下

```
[function] function-name ()
{
    commands
}
```

其中 `function` 是可选的，`function-name` 是你用来调用函数的名称，而 `commands` 构成了函数在调用时执行的命令列表。`commands` 可以是 shell 脚本中包含的任何内容，包括对其他函数的调用。

左花括号（{）可以出现在与函数名称相同的行上。别名和变量在读取函数时进行展开，而不是在执行时。你可以在函数内使用 `break` 语句（第 976 页）来终止其执行。

Shell 函数不仅可作为简写使用，还可用于定义特殊命令。以下函数在后台启动名为 `process` 的过程，并将 `process` 通常显示的输出保存至 `.process.out`：

```
start_process() {
    process > .process.out 2>&1 &
}
```

下一个示例创建一个简单的函数，该函数显示日期、标题以及当前登录在系统中的人员列表。此函数运行与第 300 页描述的 `whoson` 脚本相同的命令。在此示例中，函数是通过键盘输入的。大于号（> ）是次要 shell 提示符（PS2）；请勿输入它们。

```
$ function whoson ()
> {
>    date
>    echo "Users Currently Logged On"
>    who
> }
$ whoson
Mon Aug  9 15:44:58 PDT 2010
Users Currently Logged On
hls       console       2010-08-08 08:59    (:0)
max       pts/4         2010-08-08 09:33    (0.0)
zach      pts/7         2010-08-08 09:23    (bravo.example.com)
```

![](img/2344fc4a798f29dca9e8b5ed7288171a_401_0.png)

如果你希望 whoson 函数始终可用，而无需每次登录时都输入它，请将其定义放入 ~/.bash_profile 中。然后使用 .（点）命令运行 .bash_profile 以立即使更改生效：

```
$ cat ~/.bash_profile
export TERM=vt100
stty kill '^\\u'
whoson() 
{
date
    echo "Users Currently Logged On"
who
}
$ . ~/.bash_profile
```

在调用函数时可以指定参数。在函数内部，这些参数可作为位置参数（第 996 页）使用。以下示例展示了从键盘输入的 arg1 函数：

```
$ arg1() {
> echo "$1"
> }

$ arg1 first_arg
first_arg
```

请参阅第 296 页的 function switch () 以了解函数的另一个示例。“第 993 页的函数”讨论了函数内部局部和全局变量的使用。

![](img/2344fc4a798f29dca9e8b5ed7288171a_401_1.png)

以下函数允许你使用 tcsh 语法导出变量。env 内建命令列出所有环境变量及其值，并验证 setenv 是否正常工作：

```
$ cat .bash_profile
...
# setenv - keep tcsh users happy
function setenv()
{
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

![](img/2344fc4a798f29dca9e8b5ed7288171a_401_2.png)

特殊参数 $# （第 997 页）取值为命令行参数的数量。此函数使用 eval 内建命令强制 bash 两次扫描命令 $1=$2。由于 $1=$2 以美元符号（$）开头，shell 将整个字符串视为单个标记——即一条命令。执行变量替换后，命令名称变为 `TCL_LIBRARY=/usr/local/lib/tcl`，这会导致错误。使用 `eval`，第二次扫描将字符串拆分为三个所需的标记，从而进行正确的赋值。

## 控制 bash：功能与选项

本节解释如何使用命令行选项以及 `set` 和 `shopt` 内建命令来控制 `bash` 的功能和选项。

## 命令行选项

有两种类型的命令行选项：短选项和长选项。短选项由连字符后跟一个字母组成；长选项由两个连字符后跟多个字符组成。在调用 `bash` 的命令行中，长选项必须出现在短选项之前。表 9-12 列出了一些常用的命令行选项。

**表 9-12 命令行选项**

| **选项** | **说明** | **语法** |
| :--- | :--- | :--- |
| 帮助 | 显示使用信息。 | `--help` |
| 无编辑 | 防止用户在交互式 shell 中使用 Readline 库（第 340 页）编辑命令行。 | `--noediting` |
| 无 profile | 阻止读取这些启动文件（第 293 页）：`/etc/profile`、`~/.bash_profile`、`~/.bash_login` 和 `~/.profile`。 | `--noprofile` |
| 无 rc | 阻止读取 `~/.bashrc` 启动文件（第 294 页）。如果 shell 作为 `sh` 调用，则默认启用此选项。 | `--norc` |
| POSIX | 以 POSIX 模式运行 `bash`。 | `--posix` |
| 版本 | 显示 `bash` 版本信息并退出。 | `--version` |
| 登录 | 使 `bash` 如同登录 shell 一样运行。 | `-l` （小写 "l"） |
| shopt | 带有 _opt_ _shopt_ 选项（下一页）运行 shell。`-O` （大写 "O"）设置选项；`+O` 取消设置该选项。 | `[±]O` [_opt_] |
| 选项结束 | 在命令行上，指示选项结束。后续标记将被视为参数，即使它们以连字符（-）开头。 | `--` |

## shell 功能

你可以通过开启和关闭功能来控制 Borne Again Shell 的行为。不同的功能使用不同的方法来开启或关闭。`set` 内建命令控制一组功能，而 `shopt` 内建命令控制另一组功能。你还可以从用于调用 bash 的命令行控制许多功能。

## 功能、选项、变量？

**提示** 为了避免术语混淆，本书将你可以控制的各种 shell 行为称为*功能*。*bash* info 页面将它们称为“选项”和“控制可选 shell 行为的变量值”。

## set ±o：开启和关闭 shell 功能

`set` 内建命令在使用 `-o` 或 `+o` 选项时，可以启用、禁用和列出某些 `bash` 功能。例如，以下命令开启 `noclobber` 功能（第 248 页）：

```
$ set -o noclobber
```

你可以通过输入以下命令来关闭此功能（默认值）：

```
$ set +o noclobber
```

不带选项的命令 `set -o` 会列出由 `set` 控制的每个功能及其状态（开启或关闭）。不带选项的命令 `set +o` 会以你可以用作 shell 输入的形式列出相同的功能。表 9-13（下一页）列出了 `bash` 功能。

## shopt：开启和关闭 shell 功能

`shopt`（shell 选项）内建命令可以启用、禁用和列出某些控制 shell 行为的 `bash` 功能。例如，以下命令使 `bash` 在扩展模糊文件引用时包含以点（.）开头的文件名（`-s` 代表 `set`）：

```
$ shopt -s dotglob
```

你可以通过输入以下命令来关闭此功能（默认值）（`-u` 代表 `unset`）：

```
$ shopt -u dotglob
```

如果你将功能名称作为 `shopt` 的唯一参数输入，shell 将显示该功能的设置状态：

```
$ shopt dotglob
dotglob             off
```

不带任何选项或参数的命令 `shopt` 会列出由 `shopt` 控制的功能及其状态。不带参数的命令 `shopt -s` 会列出由 `shopt` 控制且已设置或开启的功能。命令 `shopt -u` 会列出未设置或关闭的功能。表 9-13（下一页）列出了 `bash` 功能。

## 使用 shopt 设置 set ±o 功能

**提示** 你可以使用 `shopt` 来设置/取消设置其他由 `set ±o` 控制的功能。使用标准的 `shopt` 语法配合 `-s` 或 `-u`，并包含 `-o` 选项。例如，以下命令开启 `noclobber` 功能：

```
$ shopt -o -s noclobber
```

