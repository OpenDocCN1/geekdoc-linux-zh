
```
$ w ; free ; df
6:02pm up 4 days, 24 min, 1 user, load average: 0.00, 0.00, 0.00
USER TTY FROM LOGIN@ IDLE JCPU PCPU WHAT
nball pts/0 shuttle.home.org 1:14pm 0.05s 0.01s w
total used free shared buffers cached
Mem: 199684 184420 6264 76 17620 142820
-/+ buffers/cache: 23980 166704
Swap: 1277156 251764
Filesystem 1-blocks Available Use% Mounted on
/dev/hda1 11788296 4478228 671148 41% /
none 95340 0 95340 0% /dev/shm
```

此示例显示了 `we`、`free` 和 `df` 命令的输出。长长的 shell 命令行可以在 shell 脚本或命令行中使用通过反斜杠字符（`\`）进行扩展。例如：

```
$ echo this is a line \
> command line and"; echo shows that multiple commands \
> may be strung out.\nthis is a long command line
shows multiple commands may be strung out.
```

这前三行是单条命令行。在这一单行中有两个 `echo` 命令实例。请注意，当你使用反斜杠作为行连续连接符时，它必须是命令行的最后一个字符（或在你的 shell 脚本中，正如你在本章后面部分看到的样）。

使用 shell 命令行的基本功能很容易，但要掌握所有功能可能很困难。整本书都致力于使用 shell、编写 shell 脚本以及使用模式匹配。接下来的章节提供了关于编写脚本的 shell 命令行的一些概述。

> 注意
> 
> 如果你计划开发 shell 脚本来扩展 `grep` 等命令的模式匹配能力，将从学习表达式中受益。使用 UNIX 和 Linux 模式匹配能力的权威指南是 Jeffrey E. Friedrich 写的《正则表达式》。

## Shell 模式匹配

命令允许你使用特殊构造的通配符字符串，这与 `grep` 等 GNU 工具的功能在某些方面更简单，即使使用可用字符的子集也可以产生构造性结果。用于模式匹配的常用字符有：

- 匹配任意字符。例如，查找当前目录中以 `.txt` 结尾的所有文件：

```
$ ls *.txt
```

- 匹配单个字符。例如，查找当前目录中以 `.dc` 结尾（0–9, a–z 或 A–Z）的文件：

```
$ ls *.dc
```

- 匹配字符范围。例如，列出目录中包含数字的文件：

```
$ ls *[0-9]
```

- 匹配如 `?` 或制表符之类的字符。例如，创建一个包含问号的文件：

```
$ touch foo?
```

注意，shell 可能不会以命令相同的方式解释某些字符或正则表达式；在 shell 脚本中混合通配符和表达式会导致问题。

## 重定向输入和输出

你可以在命令行上创建、覆盖和将数据追加到文件中，这种过程称为输入和输出重定向。shell 识别该过程的几个字符，如 `>` 或 `>>`。在本示例中，`ls` 命令的输出被重定向创建一个名为 `textfiles.listing` 的文件：

```
$ ls *.txt >textfiles.listing
```

谨慎使用输出重定向，因为可能会覆盖现有文件。例如，指定不同的目录但使用相同的文件将覆盖 `textfiles.listing`：

```
$ ls /usr/doc/mutt-1.4/*.txt >textfiles.listing
```

幸运的是，大多数 shell 足够智能，你可能在做蠢事。在这里，shell 警告命令正尝试将输出重定向到目录：

```
$ mkdir foo
$ ls >foo
```

可以通过追加 (`>>`) 运算符将输出追加到文件而不覆盖现有内容。在本示例中，目录列表追加到 `textfiles.listing` 的末尾：

```
$ ls /usr/doc/mutt-1.4/*.txt >>textfiles.listing
```

你可以使用 `<` 通过输入重定向将数据输入命令：

```
$ cat < textfiles.listing
```

你可以使用 shell 运算符指定命令行的结束：

```
$ cat >simple_script <<DONE
> echo "this is a simple script"
> DONE
$ cat simple_script
echo "this is a simple script"
```

在此示例中，shell 将接收你输入的 `cat` 命令，直到识别出 `DONE` 模式。输出文件 `simple_script` 被保存并验证了其内容。这种技术可以用于脚本，根据各种命令的输出创建内容并定义输入结束符或分隔符。

## 管道数据

许多 Linux 命令可以在单个连接的命令行中协同工作，将数据从一种形式转换为另一种。这种将 Linux 命令连接在一起的方法被称为使用或创建管道。管道在命令行上通过竖线运算符 (`|`) 创建。例如，可以使用管道从单命令行执行复杂的任务，如下：

```
$ find /d2 -name '*.txt' -print | xargs cat | \
  tr ' ' '\n' | sort | uniq >output.txt
```

此示例获取 `find` 命令的输出通过 `xargs` 为 `cat` 命令提供 `/d2` 下的所有文本文件。所有匹配文件的内容随后通过 `tr` 命令，将数据流中的每个空格改为换行符。对单词流进行排序，并使用 `uniq` 命令删除相同的相邻行。输出（原始单词列表）保存在文件 `output.txt` 中。

> 注意
> 
> 你将在书中找到使用管道和其他 shell 运算符的示例。例如，参见第 10 章“管理文件系统”中的“fdisk”部分，查看如何将系统分区发送到文件或打印机。查看第 11 章“用户帮助与辅助功能”中的“tar”部分，查看如何在执行增量备份时使用管道，或保存系统上更改的文件目录。

## 编写、创建和执行 Shell 脚本的基础

为什么要编写和使用 shell 脚本？shell 脚本可以节省你的时间和输入量，特别是当你每天都例行使用相同的命令行时。虽然你也可以使用历史功能（在运行 `bash` 时按向上或向下键，或使用 `history` 命令），但 shell 脚本可以通过命令行参数替换和内置帮助增加灵活性。

虽然 shell 脚本的执行速度不会比 C 等编程语言的程序快，但 shell 程序的体积比编译后的程序小，而且除了 shell 本或系统中已安装的命令外，不需要任何额外的库支持。创建和测试 shell 脚本的过程通常比开发等效的 C 命令更简单快速。

> 许多 Red Hat Linux 命令实际上都是 shell 脚本，互联网上还有许多其他 shell 脚本示例——快速搜索就能找到来自 Linux 用户和开发者的大量教程和脚本。例如，从控制台启动 X 会话的 `start` 命令就是红帽用户每天使用的 shell 脚本。可以使用 `fax` 命令发送事实，这是一个你可以自定义的 shell 脚本，可以包含你的姓名、电话号码和其他信息。要学习更多关于使用 bash 脚本的知识，请参阅本章末尾“引用”部分列出的《高级 Bash 脚本指南》。你还会发现《Sams24小时自学编程》是一本学习更多如何使用 shell 构建命令的有用指南。

当你学习编写和执行 shell 脚本时，从简单但实用的任务脚本开始。从短示例开始，随着经验和知识的积累扩展脚本。大量使用注释（以 `#` 号开头的行）来记录脚本的每个方面。包含作者信息和脚本概述作为额外帮助，以及创建日期或版本号。使用 `vi` 等文本编辑器编写 shell 脚本，因为它不会自动换行。换行可能会破坏脚本语法并导致问题。如果你使用 `pico` 编辑器，请包含 `-w` 标志以禁用换行。

## 使用 bash 创建并执行简单的 Shell 程序

在本节中，你将学习如何编写一个简单的 shell 脚本，以便每次登录时设置若干别名（命令同义词）（参见第 19 章“使用别名转发电子邮件”）。你不需要每次登录时都输入所有别名，可以使用 `vi` 等文本编辑器将它们放入一个文件中，然后执行该文件。通常，这些更改保存在 `/etc` 目录下的系统级 shell 配置文件中，使更改对所有用户生效；或者保存在家目录下的 `.bashrc`、`.cshrc`（如果你使用 `tsh`）或 `.bash_profile` 文件中。

以下是为此目的创建的 `myenv` 示例 shell 脚本（用于 `bash`）：

```
#!/bin/sh
alias l11='ls -1'
alias ldir='ls -AF'
alias copy='cp'
```
