
注意，在红帽 Linux 中，`ls` 命令的输出是有颜色区分的，帮助你区分文件、目录和其他类型的数据。目录显示为蓝色。

`ls` 命令为你提供了两行输出。你看到的每个名称都在你 Linux 系统的根目录下。使用相同的命令列出 `usr` 目录的内容：

```
[@workstation20]$ ls /usr
bin etc include lib libec sbin src X11R6
dict games kerberos lib64 local share tmp
[@workstation20]$
```

注意，`ls` 命令的参数以正斜杠（`/`）开头，并包含一个或多个用额外的斜杠分隔的单词。在 Linux 命令行引用文件或目录的特定位置时，你从根目录（`/`）开始，提供一种导航所需文件或目录的路线图，并在沿途每一步使用额外的斜杠进行分隔。

为了练习，再列出另一个目录的内容：

```
[@workstation20]$ ls /usr/X11R6
bin include LessTif lib man share
[@workstation20]$
```

# Linux 是大小敏感的

遇到困难了吗？如果你一直忠实地尝试却遇到“Command not found”（找不到命令）或“No such file or directory”（无此类文件或目录），请检查你在输入这些命令时没有使用大写字母。Linux 与大多数 Unix 类操作系统一样，是大小敏感的。这意味着对于 Linux 来说，`ls` 与 `LS`；同样，`x11r6` 也不是 `X11R6`。

# 在控制台导航 Linux

在这些命令中，你列出了根目录的内容、根目录下名为 `usr` 的目录，以及 `usr` 目录下名为 `X11R6` 的目录。`usr` 目录位于根目录内部。你在每次情况下为 `ls` 命令提供的路线图被称为“路径”（path）。表 4.1 列出了路径的更多示例及解释。

表 4.1 Linux 路径示例

| 路径 | 解释 |
| --- | --- |
| `/` | 指代根目录 |
| `/usr/X11R6/lib` | 指代根目录下 usr 目录下的 X11R6 目录中的 lib 目录 |
| `/usr/lib/xmms/Input` | 指代根目录下 lib 目录下的 xmms 目录中的 Input 目录 |

熟悉路径的概念非常重要，因为许多 Linux 命令都期望你提供路径作为参数——`ls` 就是一个显而易见的例子。

## 家目录

你已经学习了 Linux 中的一个特殊目录——根目录，它包含了所有其他目录和文件。现在是时候学习第二个特殊目录了，称为家目录（home directory）。当 Linux 用户创建并保存文件、接收电子邮件、在平板式扫描仪上扫描图像或执行任何其他任务时，用户需要存储在硬盘上的任何数据通常都会存储在用户家目录的某个某个文件中。

Linux 系统上的每个账户都有一个家目录，通常以账户名命名并位于 `/home`。如果你以 `jack` 登录，你的家目录位于 `/home/jack`。你登录时产生的所有文件和创建的任何目录通常包含在 `/home/jack` 中。如果你注销后另一个用户 `jill` 登录，她在登录后创建的任何文件通常存储在 `/home/jill`。

通过这种方式，Linux 允许创建许多用户账户，同时保持用户文件相互隔离。这种组织系统还确保了文件系统的整洁，因为用户创建的大多数日常文件都存储在由用户拥有的一个位置。

# 有更快的回家路

大多数 Shell 都识别波浪号字符（`~`）为代表家目录的特殊快捷方式。

# 当前工作目录

此时，你的当前工作目录就是你的家目录——位于 `/home` 中属于你账户的目录。当你登录时，Shell 总是假设你想让当前目录成为家目录，除非你显式更改它。要更改工作目录，请使用 `cd` 命令并将所需的当前目录作为参数。现在尝试将你的当前目录更改为根目录：

```
[@workstation20]$ cd /
[@workstation20]$
```

注意命令提示符已经改变以反映你新的工作目录。你也可以使用 `pwd` 查看更改是否已生效：

```
[@workstation20]$ pwd
/
[@workstation20]$
```

现在，使用不带参数的 `ls` 命令显示的是根目录的内容，而不是你家目录的内容：

```
[@workstation20]$ ls
bin dev home lib misc opt root tmp var
boot etc initrd lost+found proc sbin usr
[@workstation20]$
```

尝试将 `/usr/X11R6` 设置为当前工作目录，使用 `pwd` 验证更改，然后使用不带参数的 `ls` 列出目录内容：

```
[@workstation20]$ cd /usr/X11R6
[@workstation20 $X11R6]$ pwd
/usr/X11R6
[@workstation20 $X11R6]$ ls
bin include LessTif lib man share
[@workstation20 $X11R6]$
```

由于家目录对于命令行命令行使用 Linux 至关重要，你可以通过输入不带参数的 `cd` 命令快速返回此处：

```
[@workstation20 X11R6]$ cd
[@workstation20 you]$ pwd
/home/you
[@workstation20 you]$
```

# 两个名称，一个概念

你可能会遇到“当前目录”（present working directory）而不是“当前工作目录”（current working directory）；这两个术语含义完全相同。

![](img/efbfd8c0b79408e6b4551c9993acdb3c_118_0.png)

## 操作文件和目录

现在你已经回到了主目录，假设你想要为之前创建的名为 `empty.txt` 的文件创建一个副本。你可以使用 `cp` 命令来实现，提供两个参数——首先是源（原始）文件名，然后是目标（新）文件名：

```
[@workstation20]$ cp empty.txt notfull.txt
[@workstation20]$ ls
empty.txt notfull.txt
[@workstation20]$
```

现在你的主目录下有两个文件：`empty.txt` 和 `notfull.txt`。但是，假设你不希望 `empty.txt` 留在主目录中，而是想将该文件放在一个名为 `empties` 的自定义目录中。要创建一个目录，请使用 `mkdir` 命令，并将你想创建的目录名称作为参数：

```
[@workstation20]$ mkdir empties
[@workstation20]$ ls
empties notfull.txt
[@workstation20]$
```

你现在创建了一个名为 `empties` 的目录（`ls` 会用蓝色显示它以表示这是一个目录），并可以将 `empty.txt` 移动其中。Linux 文件使用 `mv` 命令，它接受要移动的文件名作为参数，并将目标目录作为最后一个参数。完成后，你可以使用熟悉的 `ls` 命令来验证 `mv` 的效果：

```
[@workstation20]$ mv empty.txt empties
[@workstation20]$ ls
empties notfull.txt
[@workstation20]$
```

注意，你刚刚输入的命令中的路径参数并不是以斜杠字符开头的。这些命令给出的是相对路径，我们将在下一节中讨论。

## 使用相对路径

在你刚刚输入的一系列命令中，你只给 `ls` 传递了一个目录名 `empties` 作为参数，而不是一个以斜杠开头的完整路径。一个没有指向根目录地图的目录就是相对路径，之所以这样命名是因为它不是从根目录 (`/`) 开始的，而是指定

该参数相对于你当前的工作目录。Linux 足够聪明，可以注意到提供给 `ls` 的路径并不是从根目录开始的；因此，它会将你提供的路径添加到你的当前工作目录中（当前工作目录总是以斜杠开头）。在这种情况下，`/home/you`（当前工作目录）加上 `emptyfiles`（给 `ls` 的参数）导致 `/home/you/emptyfiles` 的内容显示在控制台上，从而省去了你手动输入长路径的麻烦。

为了更多地练习相对路径，尝试再创建一个目录。这次在你的主目录下通过在之前创建的 `emptyfiles` 目录内部创建一个名为 "deeper" 的目录。记住，你的当前工作目录仍然是主目录；你可以使用 `pwd` 来验证这一点：
