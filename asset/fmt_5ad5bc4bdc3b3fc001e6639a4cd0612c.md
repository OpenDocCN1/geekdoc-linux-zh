
当给定一个不带 `=value` 或 `value` 字段的别名列表时，`alias` 内置命令会响应显示每个已定义别名的值。如果某个别名未定义，`alias` 内置命令会报告错误：

```
$ alias ll l ls zap wx
alias ll='ls -l'
alias l='ls -ltr'
alias ls='ls -F'
alias zap='rm -i'
bash: alias: wx: not found
```

你可以通过在别名命令前加反斜杠（`\`）来避免别名替换：

```
$ \ls
Test_Emacs XTerm.ad     flute.ps    maptax.icn
Tiger      fixtax.icn   floor       testdir
```

由于用别名值替换别名名称不会改变命令行的其余部分，因此参数仍然会被接收该命令的程序接收：

```
$ ll fl*
-rw-r--r-- 1 alex group     641 Apr  1 2008 fixtax.icn
-rw-r--r-- 1 alex group   30015 Mar  1 2007 flute.ps
-rw-r-xr-x 1 alex group     485 Oct 21 08:03 floor*
```

你可以使用 `unalias` 内置命令移除别名。当移除 `zap` 别名后，它不再通过 `alias` 内置命令显示，后续使用会导致错误消息：

```
$ unalias zap
$ alias
alias ll='ls -l'
alias l='ls -ltr'
alias ls='ls -F'
$ zap maptax.icn
bash: zap: command not found
```

## 函数

`shell` 函数类似于 `shell` 脚本，因为它存储一系列命令以便稍后执行。然而，由于 `shell` 将函数存储在计算机的主内存（`RAM`）中，而不是磁盘上的文件中，`shell` 访问它的速度比访问脚本更快。`shell` 还会对函数进行预编译（解析），使其启动速度比脚本快。最后，`shell` 在调用它的同一 `shell` 中执行 `shell` 函数。如果你定义了太多函数，启动子 `shell`（如运行脚本时）的开销可能会变得无法接受。

你可以在 `~/.bash_profile` 启动文件中、使用它的脚本中，或直接从命令行声明 `shell` 函数。你可以使用 `unset` 内置命令移除函数。一旦注销，`shell` 不会保留函数。

### 移除变量和函数

> **提示** 如果你有一个 `shell` 变量和一个同名的函数，使用 `unset` 会移除 `shell` 变量。如果你再次使用相同名称调用 `unset`，它会移除函数。

声明 `shell` 函数的语法是

```
[function] function-name ()
{
commands
}
```

其中 `function` 这个词是可选的，`function-name` 是你用于调用函数的名称，`commands` 组成当调用函数时执行的命令列表。`commands` 可以是 `shell` 脚本中包含的任何内容，包括对其他函数的调用。

第一个花括号 `{` 可以出现在与函数名称相同的行上。别名和变量在函数被读取时展开，而不是在执行时展开。你可以在函数内使用 `break` 语句（第 910 页）来终止其执行。

`shell` 函数作为简写很有用，也可以用于定义特殊命令。以下函数在后台启动名为 `process` 的进程，并将 `process` 通常显示的输出保存在 `.process.out` 中：

```
start_process() {
process > .process.out 2>&1 &
}
```

下一个示例展示了如何创建一个简单的函数，显示日期、标题以及正在使用系统的人员列表。此函数执行与第 287 页描述的 `whoson` 脚本相同的命令。在此示例中，函数是通过键盘输入的。大于号（`>>`）是二级 `shell` 提示符（`PS2`）；请勿输入它们。

```
$ function whoson ()
> {
> date
> echo "Users Currently Logged On"
> who
> }

$ whoson
Thu Aug  7 15:44:58 PDT 2008
Users Currently Logged On
hls    console       Aug  6 08:59  (:0)
alex   pts/4         Aug  6 09:33  (0.0)
jenny  pts/7         Aug  6 09:23  (bravo.example.com)
```

### 启动文件中的函数

如果您希望始终可以使用 `whoson` 函数，而无需每次登录时手动输入，请将它的定义放入 `~/.bash_profile` 中。然后使用 `.` (点) 命令运行 `~/.bash_profile`，以立即使更改生效：

```bash
$ cat ~/.bash_profile
export TERM=vT100
stty kill '^u'
whoson ()
{
    date
    echo "Users Currently Logged On"
    who
}
$ . ~/.bash_profile
```

在调用函数时，您可以指定参数。在函数内部，这些参数可作为位置参数使用（见第 930 页）。以下示例展示了从键盘输入 `arg1` 函数。

```bash
$ arg1 () {
> echo "$1"
> }

$ arg1 first_arg
first_arg
```

请参阅第 283 页的 `switch ()` 函数作为函数的另一个示例。第 927 页的“函数”部分讨论了在函数内使用局部变量和全局变量。

#### 可选

以下函数允许您使用 `tcsh` 语法导出变量。`env` 内置命令列出所有环境变量及其值，并验证 `setenv` 是否正常工作：

```bash
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

`Eval`

特殊参数 `$#`（第 931 页）取命令行参数的数量值。此函数使用 `eval` 内置命令强制 `bash` 对命令 `$1=$2` 进行两次扫描。因为 `$1=$2` 以美元符号 (`$`) 开头，`shell` 将整个字符串视为单个标记——一个命令。在执行变量替换后，命令名称变为 `TCL_LIBRARY=/usr/local/lib/tcl`，这将导致错误。使用 `eval` 后，第二次扫描将字符串分割为所需的三个标记，并执行正确的赋值。

# 控制 BASH 功能和选项

本节介绍如何使用命令行选项以及 `set` 和 `shopt` 内置命令来控制 `bash` 的功能和选项。

## 命令行选项

有两种类型的命令行选项：短选项和长选项。短选项由连字符后跟一个字母组成；长选项由两个连字符后跟多个字符组成。在调用 `bash` 的命令行上，长选项必须出现在短选项之前。表 9-12 列出了一些常用的命令行选项。

**表 9-12** **命令行选项**

| 选项 | 说明 | 语法 |
| :--- | :--- | :--- |
| Help | 显示用法消息。 | `--help` |
| No edit | 防止用户在使用 `Readline` 库（第 326 页）在交互式 `shell` 中编辑命令行。 | `--noediting` |
| No profile | 防止读取这些启动文件（第 281 页）：`/etc/profile`, `~/.bash_profile`, `~/.bash_login`, 和 `~/.profile`。 | `--norc` |
| No rc | 防止读取 `~/.bashrc` 启动文件（第 281 页）。如果 `shell` 作为 `sh` 调用，此选项默认开启。 | `--norc` |
| POSIX | 在 `POSIX` 模式下运行 `bash`。 | `--posix` |
| Version | 显示 `bash` 版本信息并退出。 | `--version` |
| Login | 使 `bash` 像登录 `shell` 一样运行。 | `-l` (小写 "1") |
| shopt | 以 `shopt` 选项（第 339 页）运行 `shell`。`-O` (大写 "O") 设置选项；`+O` 取消设置选项。 | `±O [apf]` |
| End of options | 在命令行上，表示选项结束。后续的标记被视为参数，即使它们以连字符 (`-`) 开头。 | `--` |

## Shell 功能
