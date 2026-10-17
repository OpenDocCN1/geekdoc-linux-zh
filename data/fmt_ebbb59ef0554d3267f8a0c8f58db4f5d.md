
# 命令别名

别名（Aliases）是存储在 shell 识别的特殊变量中的命令快捷方式。或者，它可以自动应用较长命令的简写版本。当发布简单命令时，经常使用的选项。例如，当你输入 `cp` 命令时，你实际上运行的是 `cp -i` 命令的别名。

可以使用 `alias` 命令创建和查看别名。要为命令 `mount -t ext2 /dev/fd0 /mnt/floppy` 创建一个名为 `mf` 的别名并查看别名列表，你需要使用以下操作：

```
[root@localhost root]# alias mf="mount -t ext2 /dev/fd0 /mnt/floppy"
[root@localhost]# alias cp="cp -i"
alias ls -l="ls -d [a-zA-Z]* --color=tty"
alias ls-1="ls -1 --color=tty"
alias ls="ls --color=tty"
alias mf="mount -t ext2 /dev/fd0 /mnt/floppy"
alias mv="mv -i"
alias rm="rm -i"
alias which="alias /usr/bin/which --tty-only --read-alias show-do="show-tide--"
[root@localhost root]# 
```

现在，你只需要运行 `mf` 命令即可将包含文件系统的软磁盘挂载到 `/mnt/floppy` 目录，如下所示。

```
[root@localhost root]# mf
[root@localhost]# mount
/dev/hdc2 : type ext3 (rw)
none on /proc type proc (rw)
/dev/hcd1 : type ext3 (rw)
none on /dev/pts type devpts (rw,gid=5,mode=620)
none on /dev/sh type tmpfs (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
/dev/fd0 / /mnt/floppy type ext2 (rw)
[root@localhost root]# 
```

你也可以为多个命令创建别名，只要它们由元字符分隔即可。要创建一个名为 `dw` 的别名，它会运行命令后跟上 `root#` 命令，你需要执行以下操作：

```
[localhost]# alias dw="date;who"
[localhost]# alias
alias cp=cp -i
alias dw='date;who'
alias ls=ls -d [a-zA-Z]*--color=tty
alias ll=ls -l --color=tty
alias ls=ls --color=tty
alias mf="mount -t ext2 /dev/fd0 /mnt/floppy"
alias mv="mv -i"
alias rm="rm -i"
alias which="alias /usr/bin/which --tty-only --read-alias show-do="show-tide--"
[localhost]# 
```

# 环境文件

# 用户定义变量

你可以使用之前讨论过的相同方法修改现有变量的内容，从而设置自己的变量。指定变量名称（称为变量标识符），后跟等号和新内容。

当你创建新变量时，请注意变量标识符的以下特性：

- 它们可以包含字母数字（0-9, A-Z, a-z）、连字符字符（`-`）或下划线字符（`_`）。

- 它们不能与数字开头。

- 为了遵循惯例，它们通常使用大写字母（例如 `HOME`、`PATH` 等）。

要创建一个内容为 "This is a sample variable" 的变量 `MYVAR` 并显示其内容，你可以使用以下命令：

```
[root@localhost]# MYVAR="This is a sample variable"
[root@localhost]# echo $MYVAR
This is a sample variable
[root@localhost]#
```

上述命令创建了一个对当前 shell 可用的变量。然而，当前 shell 还会创建子 shell（subshells）。脚本和程序在子 shell 中运行。当前 shell 中的变量对于这些子 shell 以及在其中运行的命令是不可用的，除非该变量被导出到所有子 shell。

使用 `export` 命令，你可以确保由当前 shell 启动的所有程序都有访问该变量。

# 列出环境变量

你可以使用两个命令在 BASH shell 中列出环境变量：

- `set` 命令列出所有变量，并指示用户定义的变量

- `env` 命令列出所有导出的变量

由于 `set` 和 `env` 命令的输出通常很大，你可以将这些命令的标准输出（Standard Output）重定向到 `grep` 命令以显示某些行。

要查看 `set` 和 `env` 命令之间的差异并导出之前创建的 `MYVAR` 变量，你需要执行以下命令：

```
[root@localhost]# set | grep MYVAR
MYVAR='This is a sample variable.'
[root@localhost]# env | grep MYVAR
[root@localhost]#
[root@localhost root]# export MYVAR
[root@localhost root]# env | grep MYVAR
MYVAR=This is a sample variable.
[root@localhost root]#
```

你可以使用 `export` 命令在一个操作中创建并导出变量。要创建并导出名为 `MYVAR2` 的用户定义变量：

```
[root@localhost root]# export MYVAR2="This is another sample
variable"
[root@localhost root]# set | grep MYVAR2
MYVAR2='This is another sample variable.'
[root@localhost root]# env | grep MYVAR2
MYVAR2='This is another sample variable'
[root@localhost root]# 
```

并不是所有的环境变量都被导出了。例如，`PS1` 不需要对子 shell 可用，因此没有被导出。

# 内置命令

还有其他不被 `set` 或 `env` 命令显示的变量。变量在 shell 中执行专门的功能。

特殊变量的一个例子是 `UMASK`。它在 BASH shell 中执行特殊功能，并且必须通过 `umask` 命令设置。
