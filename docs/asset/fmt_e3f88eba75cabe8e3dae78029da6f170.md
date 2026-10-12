
要查看 `set` 和 `env` 命令之间的区别，并导出前面创建的 `MYVAR` 变量，可以执行以下命令：

```
[root@server1 root]# set | grep MYVAR
MYVAR="This is a sample variable."
[root@server1 root]# env | grep MYVAR
[root@server1 root]# _
[root@server1 root]# export MYVAR
[root@server1 root]# env | grep MYVAR
MYVAR=This is a sample variable.
[root@server1 root]# _
```

并非所有环境变量都被导出；`PS1` 变量就是一个示例，它不需要对子 shell 可用，因此未被导出。但是，导出用户定义变量是一种良好的做法，因为它们很可能被在子 shell 中运行的进程使用。结果，要创建并导出名为 `MYVAR2` 的用户定义变量，可以单独使用 `export` 命令，如下所示：

```
[root@server1 root]# export MYVAR2="This is another sample variable"
[root@server1 root]# set | grep MYVAR2
MYVAR2=$'This is another sample variable.'
__MYVAR2
[root@server1 root]# env | grep MYVAR2
MYVAR2=This is another sample variable.
[root@server1 root]# _
```

### 其他变量

其他变量不会由 `set` 或 `env` 命令显示；这些变量在 shell 中执行专门功能。

前文提到的 `UMASK` 变量是一个特殊变量的示例，它在 `BASH` shell 中执行特殊功能，必须通过 `umask` 命令进行设置。另外回想一下，当你输入 `cp` 命令时，实际上是运行了 `cp -i` 命令的别名。别名是存储在特殊变量中的命令快捷方式，可以使用 `alias` 命令创建和查看。要创建指向命令 `mount -t ext2 /dev/fd0 /mnt/floppy` 的别名为 `mf` 并查看它，可以使用以下命令：

```
[root@server1 root]# alias
[root@server1 root]# alias
    alias cp='cp -i'
    alias l.='ls -d .* --color=ty'
    alias ll='ls -1 --color=ty'
    alias ls='ls --color=ty'
    alias mc='. /usr/share/mc/bin/mc-wrapper.sh'
    alias mf='mount -t ext2 /dev/fd0 /mnt/floppy'
    alias mv='mv -i'
    alias rm='rm -i'
    alias vi='vim'
    alias which='alias | /usr/bin/which --tty-only --read-alias --show-dot --show-tilde'
[root@server1 root]# _
```

现在，你只需运行 `mf` 命令即可将包含 `ext2` 文件系统的软盘设备挂载到 `/mnt/floppy` 目录，如下所示：

```
[root@server1 root]# mf
[root@server1 root]# mount
    /dev/hdc2 on / type ext3 (rw)
    none on /proc type proc (rw)
    none on /sys type sysfs (rw)
    /dev/hdc1 on /boot type ext3 (rw)
    none on /dev/pts type devpts (rw,gid=5,mode=620)
    none on /dev/shm type tmpfs (rw)
    none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
    /dev/fd0 on /mnt/floppy type ext2 (rw)
[root@server1 root]# _
```

你也可以为多个命令创建别名，前提是它们由第 2 章“准备安装 Linux”中介绍的 `;` 元字符分隔。要创建并测试一个名为 `dw` 的别名，该别名先运行 `date` 命令然后运行 `who` 命令，可以执行以下操作：

```
[root@server1 root]# alias dw="date;who"
[root@server1 root]# alias
alias cp='cp -i'
alias dw='date;who'
alias l.='ls -d .* --color=tty'
alias ll='ls -l --color=tty'
alias ls='ls --color=tty'
alias mc='. /usr/share/mc/bin/mc-wrapper.sh'
alias mf='mount -t ext2 /dev/fd0 /mnt/floppy'
alias mv='mv -i'
alias rm='rm -i'
alias vi='vim'
alias which='alias | /usr/bin/which --tty-only --read-alias --show-dot --show-tilde'
[root@server1 root]# dw
Sun Jun 5 10:25:45 EDT 2005
  root     pts/0    Jun 1 08:44 (3.0.0.2)
  root     pts/1    Jun 1 11:54 (:0)
[root@server1 root]#
```

> **注意**
>
> 使用唯一的别名名称很重要，因为 shell 在搜索可执行文件之前会先搜索别名；如果你创建一个名为 `who` 的别名，该别名将取代文件系统上的 `who` 命令被使用。

### 环境文件

回想一下，变量存储在内存中。当用户退出 `BASH` shell 时，存储在内存中的所有变量都会随 shell 本身一起销毁。为了确保变量随时可被 shell 访问，你必须将变量放入一个文件中，该文件在每次用户登录并启动 `BASH` shell 时都会执行。这些文件称为**环境文件**。一些常见的 `BASH` shell 环境文件及其执行顺序如下：

1. `/etc/profile`
2. `~/.bash_profile`
3. `~/.bash_login`
4. `~/.profile`

`/etc/profile` 文件在系统上所有用户登录后立即执行，并设置大多数环境变量，如 `HOME` 和 `PATH`。在 `/etc/profile` 执行完毕后，用户的主目录将被搜索以查找隐藏的环境文件 `.bash_profile`、`.bash_login` 和 `.profile`。如果这些文件存在，则执行找到的第一个文件；因此，通常只使用这些文件中的一个。这些隐藏的环境文件允许用户设置自定义变量，独立于系统中其他用户使用的 `BASH` shell；由于执行顺序的原因，在这些文件中分配给变量的值将覆盖 `/etc/profile` 中设置的值。

要向这些文件中的任何一个添加变量，您只需添加一行与命令行中使用的命令格式相同的行。要将前面使用过的 `MYVAR2` 变量添加到 `.bash_profile` 文件中，只需使用 `vi` 等文本编辑器编辑该文件，并将该行 `export MYVAR2="This is another sample variable"` 添加到文件中。

变量并不是可以输入到环境文件中的唯一类型的信息；任何可以在命令行上执行的命令也可以放入任何环境文件中。如果您希望将 `UMASK` 设置为 `077`，在每次登录后显示日期，并创建一个别名，您可以将以下行添加到主目录中的某个隐藏环境文件中：

```
umask 077
date
alias dw="date;who"
```

还存在一种特殊的环境文件，它总是在搜索其他隐藏环境文件之前执行，并在用户登录后启动任何新的 `BASH` shell 时执行；此文件位于当前用户的主目录中，名为 `.bashrc`（`BASH` 运行时配置）。

此外，您可能希望在退出 shell 时执行清理任务；为此，只需将这些清理命令添加到主目录中的 `.bash_logout` 文件即可。

### Shell 脚本
