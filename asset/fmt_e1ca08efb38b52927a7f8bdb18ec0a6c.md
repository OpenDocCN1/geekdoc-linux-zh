
```
1  set -o vi
2  set -o noclobber
3  set -o ignoreeof
4  alias rm='rm -i'
   alias cp='cp -i'
   alias mv='mv -i'
5  stty erase ^H
   # Source global definitions
6  if [ -f /etc/bashrc ]; then
       . /etc/bashrc
   fi
7  case "$-" in
       *i*) echo This is an interactive bash shell
           ;;
       *)  echo This shell is noninteractive
           ;;
   esac
10 history control=ignoredups
11 function cd { builtin cd $1; echo $PWD; }
```

# 解释

- 1. `set` 命令配合 `-o` 开关可以打开或关闭特殊的内置选项。参见“`set -o` 选项”第 763 页。如果开关是 `-o`，即减号，则选项被打开；如果是加号，则选项被关闭。`vi` 选项允许交互式命令行编辑。例如，`set -o vi` 打开交互式命令行编辑，而 `set +o vi` 则关闭它。参见第 764 页表 13.1。
- 2. `noclobber` 选项被打开，这会阻止用户在使用重定向时覆盖文件；例如，`sort filex > filex`。参见“标准 I/O 和重定向”第 844 页。
- 3. 退出 shell 时，通常可以输入 `^D`（Ctrl-D）。设置了 `ignoreeof` 后，必须输入 `exit`。
- 4. `rm` 的别名 `rm -i` 使 `rm` 成为交互式（`-i`），即在实际删除文件之前会询问用户是否可以删除文件。`cp` 命令的别名 `cp -i` 使复制操作成为交互式。
- 5. `stty` 命令用于将终端退格键设置为擦除。`^H` 表示退格键。
- 6. 如果存在名为 `/etc/bashrc` 的文件，则对其进行 `source`。
- 7. 如果 shell 是交互式的，特殊变量 `$-` 将包含 `i`。如果不是，你可能正在运行脚本。`case` 命令会评估 `$-`。
- 8. 如果 `$-` 返回的值匹配 `*i*`（即包含 `i` 的任意字符串），则 shell 打印 `This is an interactive bash shell`。
- 9 否则，shell 打印 `This shell is noninteractive`。如果你启动脚本或在提示符下启动新 shell，你将能够判断你的 shell 是否是交互式的。它仅用于让你测试对“交互式”和“非交互式” shell 术语的理解。
- 10 `history_control` 设置用于控制命令在历史文件中的保存方式。此行读作：如果命令已存在于历史文件中，则不要保存；即忽略重复项。
- 11 这是一个用户定义的函数。当用户更改目录时，会打印当前工作目录 `PWD`。函数名为 `cd`，其定义中包含 `cd` 命令。特殊内置命令 `builtin` 在函数定义中位于 `cd` 命令之前，以防止函数进入无限递归；即无限调用自身。

`/etc/bashrc` 文件。系统范围的函数和别名可以在 `/etc/bashrc` 文件中设置。主提示符通常在此处设置。

## 示例 13.7

```
(Sample /etc/bashrc)

# Systemwide functions and aliases
# Environment stuff goes in /etc/profile

# For some unknown reason bash refuses to inherit
# PS1 in some circumstances that I can’t figure out.
# Putting PS1 here ensures that it gets loaded every time.

1 PS1="[\u@\h \W]\$ "
2 alias which="type -path"
```

# 解释

1 系统范围的函数和别名在此设置。主要的 bash 提示符被设置为用户名（`\u`）、`@` 符号、主机名（`\h`）、当前工作目录的基名，以及美元符号。参见第 769 页表 13.2。此提示符将出现在所有交互式 shell 中。
2 别名，即命令的昵称，通常在用户的 `.bashrc` 文件中设置。该别名已预设，并在 bash 启动时可用。你在想知道程序在磁盘上的位置时使用它；即它位于哪个目录中（例如，`which ls` 将打印 `/bin/ls`）。

## ~/.profile 文件。

`.profile` 文件是一个用户定义的初始化文件。它位于用户的主目录中，并在以 `sh`（Bourne shell）运行时登录时 `source` 一次。因为该文件由 Bourne shell 使用，所以不应包含任何 bash 特定的设置。如果运行 bash，且 bash 找不到之前列出的其他初始化文件，则会运行 `.profile`。它允许用户自定义和修改其 shell 环境。环境和终端设置通常放在此处，如果要启动窗口应用程序或数据库应用程序，则在此处启动。

## 示例 13.8

```
(Sample .profile)
# A login initialization file sourced when running as sh or the #.bash_profile or
# .bash_login are not found.

1 TERM=xterm
2 HOSTNAME=`uname -n`
3 EDITOR=/bin/vi
4 PATH=/bin:/usr/ucb:/usr/bin:/usr/local:/etc:/bin:/usr/bin:.
5 PS1="HOSTNAME $ > "
6 export TERM HOSTNAME EDITOR PATH PS1
7 stty erase ^h
8 go () { cd $1; PS1=`pwd`; PS1=`basename $PS1`; }
9 trap 'HOME/ logout' EXIT
10 clear
```

# 解释

- 1. `TERM` 变量被赋值为终端类型 `xterm`。
- 2. 因为 `uname -n` 命令被反引号括起来，shell 会执行命令替换；即命令的输出（主机名）将被赋给变量 `HOSTNAME`。
- 3. `EDITOR` 变量被赋值为 `/bin/vi`。`mail` 和 `history` 等程序在定义编辑器时现在可以使用此变量。
- 4. `PATH` 变量被赋值为 shell 为查找 UNIX/Linux 程序而按顺序搜索的目录条目。例如，如果你输入 `ls`，shell 将在 `PATH` 中搜索，直到在其中一个列出的目录中找到该程序。如果从未找到该程序，shell 会通知你。
- 5. 主提示符被赋值为 `HOSTNAME`，即机器名，以及 `$` 和 `>` 符号。
- 6. 列出的所有变量都被导出。它们将被从此 shell 启动的子进程所知。
- 7. `stty` 命令设置终端选项。`Erase` 键被设置为 `^H`，因此当你按下退格键时，光标前输入的字母将被擦除。

# 说明（续）

8 定义了一个名为 `go` 的函数。该函数的目的是接受一个参数（目录名），然后 `cd` 到该目录，并将主提示符设置为当前工作目录。`basename` 命令会移除路径中除最后一项之外的所有部分。提示符将显示当前目录。
9 `trap` 命令是一个信号处理命令。当你退出 shell（即注销）时，`.logout` 文件将被执行。`.logout` 文件是一个用户自定义文件，其中包含将在注销前执行的命令，这些命令用于清理临时文件、记录注销时间等。
10 `clear` 命令用于清屏。

## ~/.bash_logout 文件。

当用户注销（退出登录 shell）时，如果存在名为 `~/.bash_logout` 的文件，它将被引用（`source`）。该文件通常包含清理临时文件、截断历史文件、记录注销时间以及执行其他维护任务的命令。

## 防止启动文件被执行的选项。

如果 bash 以 `--noprofile` 选项调用（例如 `bash --noprofile`），则 `/etc/profile`、`~/.bash_profile`、`~/.bash_login` 或 `~/.profile` 启动文件将不会被引用。如果以 `-p` 选项调用（例如 `bash -p`），bash 将不会读取用户的 `~/.profile` 文件。如果 bash 以 `sh`（Bourne shell）方式调用，它会尽可能模仿 Bourne shell 的行为。对于登录 shell，它只会按顺序尝试引用 `/etc/profile` 和 `~/.profile`。仍可使用 `-noprofile` 选项来禁用此行为。如果 shell 以 `sh` 方式调用，它不会尝试引用任何其他启动文件。

## .inputrc 文件。
