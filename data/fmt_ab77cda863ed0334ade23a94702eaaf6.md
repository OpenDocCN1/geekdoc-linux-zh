
```
[root@localhost root]# mf
[root@localhost root]# mount
/dev/hdc2 on / type ext3 (rw)
none on /proc type proc (rw)
/dev/hdc1 on /dev type ext3 (rw)
none on /dev/pts type devpts (rw,gid=5,mode=620)
none on /dev/shm type tmpfs (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
/dev/fd0 on /mnt/floppy type ext2 (rw)
[root@localhost root]# _
```

# 第 8 章 使用 BASH Shell

你也可以为多个由冒号 `:` 元字符分隔的命令创建别名。要创建并测试一个名为 `dw` 的别名，它运行 `date` 命令后运行另一个命令，你可以执行以下操作：

```
[root@localhost root]# alias dw="date;who"
[root@localhost root]# alias
alias cp=cp -i
alias dw=date;who
alias 1.=ls -d [a-zA-Z]* --color=tty
alias 1l=ls -l --color=tty
alias ls=ls -t --color=tty
alias mf=mount -t ext2 /dev/fd0 /mnt/floppy
alias rm=mv -i
alias which=alias | /usr/bin/which --tty-only --read-alias --show-dot --show-tilde
[root@localhost]# dw
root Sun 2 10:25:45 EDT 2003
pts/0 Jun 1 08:44 (3.0.0.2)
root pts/1 Jun 1 11:54 (:)
[root@localhost]# _
```

使用唯一的别名是非常重要的，因为 shell 在搜索可执行文件之前会先搜索别名；如果你创建一个名为 `who` 的别名，那么系统将使用该别名而不是文件系统上的命令。

# 环境文件

记住，变量存储在内存中。当你退出 BASH shell 时，所有存储在内存中的变量都会随着 shell 本身被销毁。因此，为了确保变量始终供 shell 访问，你必须将变量放在每次登录并启动 BASH shell 时执行的文件中。这些文件被称为环境文件。一些常见的 BASH shell 环境文件及其执行顺序如下：

- `/etc/profile`
- `~/.bash_profile`
- `~/.bash_login`
- `~/.profile`

`/etc/profile` 文件在系统所有用户登录后立即执行，并设置了大多数环境变量，如 `HOME` 和 `PATH`。在 `/etc/profile` 执行完成后，系统会在用户的家目录中查找隐藏的环境文件 `.bash_profile`、`.bash_login` 和 `.profile`。如果这些文件存在，则会执行找到的一个；因此，通常只使用这些文件中的一个。这些隐藏的环境文件允许你设置自定义的变量，且独立于系统中其他用户所使用的 BASH shell；分配给这些文件中变量的任何值……

要设置一个跨越会话持续的变量，你可以使用 `export` 命令。例如：

```bash
export MYVAR="some value"
```

`.bashrc` 文件是另一个常见的环境文件，每次启动新的 BASH shell 时都会执行。这是放置你经常使用的别名和函数的好地方。你可以向 `.bashrc` 文件中添加你自己的别名。例如：

```bash
alias ll='ls -la'
alias grep='grep --color'
```

`.profile` 文件用于登录 shell。它与 `.bash_profile` 类似，但它被非 BASH shell 使用。

环境文件的执行顺序非常重要。

| 文件 | 用途 |
| :--- | :--- |
| `/etc/profile` | 所有用户的全局环境 |
| `~/.bash_profile` | BASH 登录 shell 的用户特定环境 |
| `~/.bash_login` | 其他登录 shell 的用户特定环境 |
| `~/.profile` | 所有登录 shell 的用户特定环境 |
| `~/.bashrc` | 非登录 BASH shell 的用户特定环境 |

通过了解这些文件，你可以根据需求定制你的 BASH 环境。

# Shell 脚本 381

登录系统的用户包括：

```
root pts/0 Jun 1 08:44 (3.0.0.2)
```

`/` 目录的内容为：

```
bin/ dev/home/ lib/ misc/ opt/root/ tftpboot/ usr/
boot/ etc/ initrd/ last-found/ mnt/ proc/ sbin/ tmp/ var/
```

```
[root@localhost root]# #
```

# 转义序列

在上一个例中，我们使用 `echo` 命令来处理显示在屏幕上的数据。`echo` 命令还支持几种特殊符号——转义序列，只要为 `echo` 命令指定 `-e` 选项，就可以使用它们来进一步控制显示在终端屏幕上的文本。这些 `echo` 转义序列列表见表 8-4。

**表 8-4 常见的 echo 转义序列**

| 转义序列 | 说明 |
| --- | --- |
| `\nnn` | 插入一个由三位八进制数 (ooo) 表示的 ASCII 字符 |
| `\\` | 反斜杠 |
| `\a` | ASCII 蜂鸣 |
| `\b` | 退格 |
| `\c` | 防止命令后出现换行 |
| `\f` | 换页 |
| `\n` | 换行 |
| `\r` | 回车 |
| `\t` | 水平制表 |
| `\v` | 垂直制表 |

表 8-4 中列出的转义序列可进一步处理之前使用的 `myscript` shell 脚本，如下所示：

```
[root@localhost root]# cat myscript
!/bin/bash
echo -e "Today's date is: \c"
date
echo -e "\nThe people logged into the system include:"
who
echo -e "\nThe contents of the / directory are:"
ls -F /
[root@localhost root]# ./myscript
Today's date is: Sat Jun 1 09:13:31 EDT 2003
```

# 第 8 章 使用 BASH Shell 环境

登录系统的用户包括：

```
root pts/0 Jun 1 08:44 (3.0.0.2)
```

`/` 目录的内容为：

```
bin/ dev/ home lib/ misc/ opt/ root/ tftpboot/ usr/
boot/ etc/ initrd/ lost-found/ mnt/ proc/ sbin/ tmp/ var/
```

```
[root@localhost]#
```

注意上方内容，当执行 `myscript` 时，转义序列防止了输出 `Today's date is:` 结尾出现换行符。同样，换行符 (`\n`) 被插入到显示 `The people logged into the system include:` 和 `The contents of the / directory are:` 之前，以清除命令输出前的空行。这消除了早期使用 `echo ""` 命令的需求。

# 读取标准输入

shell 脚本有时需要来自执行程序的用户的输入；这些输入可以存储在变量中供以后使用。`read` 命令从标准输入获取用户输入，并将其放在 `read` 命令参数指定的变量中。在输入读入变量后，就可以使用该变量的内容，如下 shell 脚本所示：

```
[root@localhost root]# cat newscript
!/bin/bash
echo "What is your name? --\c"
read USERNAME
echo "$USERNAME"
[root@localhost root]# chmod +x newscript
[root@localhost root]# ./newscript
What is your name? -- Fred
Hello Fred
[root@localhost]#
```

注意上方内容，向用户提问的命令输出以 `-- >` 结尾以模拟屏幕上的箭头提示符，并使用 `\c` 转义序列将光标置于提示符之后。这是 Linux 管理员在编写 shell 脚本时的常用做法。

## 决策构造

决策构造是 shell 脚本中最常用的构造类型；它们根据程序中的命令是否成功完成，或者根据用户对程序提出的问题做出的决定来改变程序的流。这在图 8-4 和图 8-5 中所示。

# Shell 脚本 383
