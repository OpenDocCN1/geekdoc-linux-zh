
```
[root@server1 ~]# echo $PATH
/usr/lib/qt-3.3:/usr/kerberos/sbin:/usr/kerberos/bin:
/usr/lib/cache:/usr/local/sbin:/usr/local/bin:/bin:/sbin:
/usr/bin:/root/bin
[root@server1 ~]#
```

在示例中，如果用户在命令行输入了 `ls` 并按回车，`shell` 会注意到路径中缺少 `/`，并开始在 `/usr/lib/qt-3.3/bin` 目录中搜索文件，然后是 `/kerberos/sbin` 目录、`/usr/lib/cache` 目录、`/usr/local/sbin` 目录、`/usr/local/bin` 目录、`/sbin` 目录，最后在 `PATH` 变量中寻找可执行文件。如果在任何目录中未找到 `ls`，`shell` 将返回错误信息，如下所示拼写错误的命令所示：

```
[root@server1 ~]# ls
Command not found.
[root@server1 ~]#
```

```
[root@server1 ~]# pwd
/root
[root@server1 ~]# ls -F
Desktop/myprogram*
[root@server1 ~]# myprogram
Command not found.
[root@server1 ~]# /root/myprogram
This is a sample program.
[root@server1 ~]# ./myprogram
This is a sample program.
[root@server1 ~]# cp myprogram /bin
This is a sample program.
[root@server1 ~]#
```

## 第 7 章 使用 BASH Shell

在前面的输出中，将 `myprogram` 可执行文件复制到 `/bin` 目录后，用户只需输入其名称即可执行它，因为 `/bin` 目录已列在 `PATH` 变量中。

表 7-3 提供了在大多数 BASH shell 中使用的环境变量列表。

### 用户定义变量

你可以使用之前讨论的相同方法设置自己的变量，以更改现有环境变量的内容。为此，你只需在等号（`=`）之前指定变量名称（称为变量标识符）和新内容。

| 变量 | 描述 |
| --- | --- |
| BASH | BASH shell 的完整路径 |
| BASH_VERSION | 当前 BASH shell 的版本 |
| DISPLAY | 用于将 X Windows 的输出重定向到另一台计算机或设备的变量 |
| ENV | BASH 配置文件的位置（通常为 `~/.bashrc`） |
| EID | 当前用户的有效 UID（ID） |
| HISTFILE | 用于存储 BASH shell 中之前输入的命令的文件（通常为 `~/.bash_history`） |
| HISTSIZE | 可以存储在 `HISTFILE` 中供下次登录使用的之前输入的命令数量；通常为 1,000 条命令 |
| HISTSIZE | 在当前登录会话期间存储在内存中的之前输入的命令数量；通常为 1,000 条命令 |
| HOME | 当前用户主目录的绝对路径 |
| HOSTNAME | Linux 系统的主机名 |
| LOGNAME | 登录 shell 时用户的用户名 |
| MAIL | 邮件箱文件的位置（存储电子邮件的地方） |
| OTYPE | 当前操作系统 |
| PATH | 在缺少包含 `/` 字符的绝对或相对路径时，搜索可执行文件的目录 |
| PS1 | 当前 shell 提示符 |
| PWD | 当前工作目录 |
| RANDOM | 访问时产生随机数的变量 |
| SHELL | 当前 shell 的绝对路径 |
| TERM | 用于确定终端设置的变量；在较新的 Linux 系统上通常设置为 "linux" 或 "xterm"，在较旧的 Linux 系统上设置为 "console" |
| TERMCAP | 用于在使用 TERCAP 数据库（`/etc/termcap`）的旧系统上确定终端设置的变量 |

表 7-3 常用 BASH 环境变量

## Shell 变量 313

创建新变量时，注意以下变量标识符的特征很重要：

- 它们可以包含字母数字（0–9, A-Z, a-z）、连字符 `–`（dash）或下划线 `_`（underscore）字符。
- 它们不能以数字开头。
- 按照惯例，通常使用大写（例如 `HOME`、`PATH` 等）。

要创建一个内容为 "This is a sample variable" 的变量 `MYVAR` 并显示其内容，可以使用以下命令：

```
[root@server1]# MYVAR="This is a sample variable"
[root@server1]# echo MYVAR
This is a sample variable
[root@server1]#
```

前面的命令创建了一个当前 `shell` 可用的变量。由 `shell` 运行的大多数命令都在当前 `shell` 创建的独立子 `shell`（`subshell`）中。在当前 `shell` 中创建的任何变量对这些子 `shell` 及其内部运行的命令都是不可见的。如果你创建一个在 C 程序中作为数据库使用的变量...

（注：提供的 OCR 文本在后几页包含大量碎片化/重复的部分。根据逻辑流和标准 `shell` 文档：）

前面的命令创建了一个当前 `shell` 可用的变量。由 `shell` 运行的大多数命令都在当前 `shell` 创建的独立子 `shell`（`subshell`）中。在当前 `shell` 中创建的任何变量对这些子 `shell` 及其内部运行的命令都是不可见的。

[第 340-341 页的剩余文本包含源高度重复且损坏的 OCR 伪迹。我已处理了上述连贯段落。]

你也可以创建别名（`alias`），只要它们由第 2 章引入的 `shell` 元字符 `;` 分隔。要创建一个名为 `dw` 的别名，其运行 `date` 命令后紧跟 `who` 命令，你可以执行以下操作：

```
[root@server1] # alias dw="date;who"
[root@server1] # alias
alias cp='cp -i'
alias dw='date;who'
alias ls='ls -d *' --color=auto'
alias lls='ls -l --color=auto'
alias ls='ls --color=auto'
alias mv='mount -t ext2 /dev/fd0 /mnt/floppy'
alias mv='mv -i'
alias rm='rm -i'
alias which='alias | /usr/bin/*--read-aliases --show-dot --show-tty' #$ dw
[root@server1] #
```

| 2010年8月20日 周五 08:32:14 EDT | | |
|---|---|
| user tty | 2010-08-20 07:47 (:0) |
| root pts/0 | 2010-08-20 07:45 (10.0.1.2) 在文件系统中。 |

使用唯一的别名名称非常重要，因为 `shell` 在执行文件之前会先搜索别名。如果你创建一个名为 `who` 的别名，那么该别名将取代文件系统上的对应命令。

# 环境文件

回想变量存储在内存中。当用户退出 BASH shell 时，内存中存储的所有变量都会随着 `shell` 一起销毁。为了确保变量始终可以被 `shell` 访问，你必须将变量放在文件中，该会在每次用户登录并启动 BASH shell 时都会执行。这些文件被称为环境文件。下面列出了常见的 BASH 环境文件及其执行顺序：

```
~/.bashrc
~/etc/profile
~/.bash_profile
~/.bash_login
~/.profile
```

`~/.bashrc` (BASH 运行时配置) 文件通常用于设置必须在每个 BASH shell 中存在的别名和变量。它在系统所有用户登录后、以及在登录后创建新的 BASH shell 时立即执行。

其他环境文件仅在 `~/.bashrc` 文件执行后才会执行。`/etc/profile` 文件在系统所有用户登录后始终执行，并设置大多数环境变量，如 `HOME` 和 `PATH`。在 `/etc/profile` 执行完成后，

![](img/bafa5678973f896b93838a140b8f7840_342_0.png)

![](img/bafa5678973f896b93838a140b8f7840_342_1.png)
