
. adobe

```
# &
```

插入在任何其他命令后的 `&` shell 操作符告诉计算机在后台运行该命令。通过将作业置于后台，用户可以继续使用 shell。

```
# |
```

`|`（管道）shell 操作符用于在独立的程序之间，将一个命令的输出“管道”到另一个命令。这种操作是 Linux 的主要优势之一，shell 可以通过简单程序构建复杂的命令。例如，您可以将 `cat` 命令的输出通过到 `sort` 命令以对文件内容进行排序：

```
cat list.txt | sort
```

```
# >
```

`>`（标准输出）shell 操作符将程序的输出发送到文件或设备。使用此操作符时要小心：它会覆盖现有文件！要将目录列表保存到文本文件，请像这样使用 `>`：

```
ls > dir.txt
```

注意，如果 `dir.txt` 文件存在，它将被擦除并用新内容覆盖。此外，由于 Linux 版本的工作非常像 UNIX，您可以将内容发送到设备：

```
cat welcome.au > /dev/audio
```

这通过将文件直接发送到音频设备来播放声音。

```
# <
```

`<`（标准输入）shell 操作符用于从文件或其他设备输入内容。例如，您可以使用该运算符配合 `sort` 命令对文件进行排序并保存结果：

```
sort < unsorted.txt > sorted.txt
```

```
# >>
```

`>>`（追加）shell 操作符不会替换指定的文件，而是将程序的输出追加到指定文件的后面。这可以用于构建日志文件：

```
cat newfile.txt >> oldfile.txt
```

`newfile.txt` 的内容不会覆盖 `oldfile.txt`，而是追加到其末尾。

```
# <<
```

`<<`（在此）shell 操作符用于告诉程序何时到达输入结束。例如，为了将 shell 作为文本编辑器，告诉 shell 在使用 `end` 单词时停止接受输入：

```
document.txt << end
```

这是一行文本。
在您输入单词 `end` 后，shell 将您的文本保存到 `document.txt` 文件中，因为您已经告诉 shell `end` 单词终止了输入。

# adduser

由 root 或其他具有权限的用户使用的 `adduser` 命令创建一个新用户。`adduser` 命令后面要创建的帐户名称：

```
adduser dplitts
```

# alias

`alias` 命令用于为命令创建别名或替代名称。通常，这些别名是实际命令的缩写。在以下示例中，用户（可能是一个 DOS 用户）为目录列表添加了 `dir` 的别名：

```
alias dir=ls
```

# 常用 Linux 命令与实用程序
附录 B

输入 `alias` 会列出你当前所有的别名。此类列表可能如下：

```bash
svr01:/home/dpitts$ alias
alias d='dir'
alias dir='/bin/ls --options --format=vertical'
alias ls='/bin/ls --options'
alias vs='dir'
alias vdir='/bin/ls --options --format=long'
```

# apropos <parameter>

`apropos` 的字面意思是“适当”或“关于（其他）”。后面跟随参数时，它会在手册页（man pages）中搜索包含该参数的条，对所有手册页进行关键词搜索。这等同于 `man -k <parameter>` 命令。

# ash

`ash` 是一个简单的 shell，功能与 `sh`（或 Bourne shell）相似。`ash` shell 通过 `/bin` 目录下的符号链接 `bsh` 运行。

# at

`at` 在指定时间运行程序。你可以使用 `at` 命令在命令行或文件中指定一个时间来调度任务作业运行。

# atq

`atq` 用于列出等待作业队列。`atq` 命令打印 `at` 命令的等待作业事件列表（通常位于 `/var/spool/at` 目录下）。

# atrm

`atrm` 用于删除指定的作业。`atrm` 命令删除 `at` 队列中等待的一个或多个作业。用户或 root 可以使用 `atrm` 命令删除待处理的事件（被停止的 at 命令）。

# banner

`banner` 向标准输出打印大型、高质量的横幅。如果省略消息，`banner` 会提示并从标准输入读取一行。例如，输入 `$ banner hi` 来创建如下的横幅。

![](img/fbfff30e42d507bc7531108a281d6cf4_1162_0.png)

# bash

`bash` 是 GNU Bourne Again Shell。作为 Red Hat Linux 的默认 shell，`bash` 具有许多功能，如命令行编辑、内置帮助和命令历史。`bash` shell 通过 `/bin` 目录下的符号链接 `sh` 运行。

# batch

`batch` 命令根据负载平均运行作业。该程序用于在计算机达到特定的负载平均值时运行事件，该平均值由 `/proc/loadavg` 文件中的实时值确定。`batch` 还有其他选项；详情请阅读 `at` 命令手册页。

# bc

`bc` 是一种计算器语言，是一个用于计算器程序和工具的解释器和语言。你可以使用这个解释器和语言编写自定义计算器。

# bg

`bg` 命令用于强制让挂起的进程在后台运行。假设你以前台启动了一个命令（没有在命令后使用 `&`），并意识到它需要花费时间，但你仍然需要你的 shell。你可以使用 `Ctrl+Z` 将当前进程挂起。然后，你可以让它保持挂起状态——就像你给电话公司打电话一样——或者输入 `bg` 让该进程在后台运行，并释放你的 shell 以允许执行其他命令。

# bind

`bind` 命令用于 `pdsh`，允许用户更改按键组合的行为以用于命令行编辑。许多人会将上、下、左、右键绑定，使其工作方式与在 Bourne Again Shell `bsh` 中保持一致。该命令的语法如下：

```
bind <key sequence> <command>
```

以下示例是 `bind` 命令，用于创建向上和向下滚动历史列表，以及沿命令行向左右移动的绑定关系：

```bash
bind ^[[=prefix-2
bind ^XA=up-history
bind ^XB=down-history
bind ^XC=forward-char
bind ^XD=backward-char
```

# cat

`cat` 并不是在调用你喜爱的猫；相反，它会将（通常是）文件的内容滚动到屏幕上。如果该文件恰好是二进制文件，`cat` 就会吐出一个毛线球并在屏幕上显示给你。通常，这也是一个嘈杂的过程。`cat` 命令实际上是在滚动文件的字符，而终端正在尽一切努力解释并显示文件中的数据。这种解释可能包括用于创建铃信号的字符，声音就源于此。正如你可能猜测的那样，`cat` 命令需要需要显示对象，其格式如下：

```bash
cat <filename>
```

![](img/fbfff30e42d507bc7531108a281d6cf4_1164_0.png)

# cd

`cd` 代表切换目录（change directory）。你会发现这个命令极其有用。该命令的三种典型用法是：

- `cd ..`：向目录树向上移动一级。
- `cd -`：从当前任何位置移动到主目录。这等同于单独执行 `cd`。
- `cd directory name`：切换到特定目录。这可以是相对于你当前位置的目录，也可以通过在目录名前加上正斜杠（`/`）来基于根目录。

这些示例可以组合使用。例如，假设你处于 `/home/dsp1234` 目录并想进入 `tng4321` 的主账户。你可以执行以下命令向上移动一级目录，然后再向下。

# chown

此命令用于更改与文件或目录权限关联的用户 ID（所有者）。文件的所有者（当然，也包括 root 用户）有权更改与文件关联的用户。命令的格式简单如下：

```
chown <new user id> <file>
```

# chroot

`chroot` 命令使文件系统的 `/` 目录（称为根目录）变为文件系统中 `/` 以外的其他目录。例如，在处理 Internet 服务器时，你可以将根目录设置为等于 `/usr/ftp`。这样，任何使用 FTP 登录的人（FTP 默认进入根目录）实际上将进入 `usr/ftp`。这可以保护你的目录结构其余部分不被匿名游客看到，被修改。为了进入 `/etc`，ftp 程序将尝试将用户放入根目录，然后进入该根目录下的 `etc` 目录。由于根目录是 `/usr/ftp`，ftp 程序实际上会将用户置于 `/usr/ftp/etc` 目录（假设该目录存在）。

该命令的语法如下：

```
chroot <original filesystem location> <new filesystem location>
```
