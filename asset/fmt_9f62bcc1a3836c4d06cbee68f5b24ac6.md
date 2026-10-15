
```
# du -sk *
5888  Desktop
396760  Documents
84688  Library
0  Movies
0  Music
31648  Pictures
0  Public
32  Sites
```

注意我在这里指定了 `-k` 标志来强制使用 1KB 块（类似于 `df`，`du` 的默认值为 512 字节块）。除此之外，它与 Linux 相同。

Solaris 上的 `du` 输出以 512 字节块报告，除非像 Darwin 一样，你使用 `-k` 标志强制使用 1KB 块：

```
# du -sk *
1 bin
1689 boot
4 cdrom
372 dev
13 devices
2363 etc
10 export
0 home
8242 kernel
1 lib
8 lost+found
1 mnt
0 net
155306 opt
1771 platform
245587 proc
5777 sbin
32 tmp
25 TT_DB
3206 users
667265 usr
9268 var
0 vol
9 xfn
```

本节展示了有用的 `du` 命令，说明了如何组合 `-a`、`-s` 和 `-h` 来产生各种不同的输出。你也看到了如何通过连续的 `du` 命令来精确定位磁盘空间占用者，这预示着我们将在本小时稍后开发的 `diskhogs` shell 脚本。

### 使用 sort 简化分析

`du` 的输出非常有信息量，但扫描列表以确定四五个最大的目录是困难的，特别是当输出中包含的目录和文件越来越多时。好消息是 Unix `sort` 实用程序正是我们需要用来绕过此问题的工具。

#### Task 3.3: 将输出管道传输到 sort

为什么我们必须费力地逐页查看列表，而 Unix 工具可以轻松让我们确定最大和最小值？`sort` 是 Unix 中的一个优秀分析工具，尽管在其他 Unix 系统管理书籍中很少提到它。

+   1. 最明显的是，`sort` 对输出进行字母排序：

```
# cat names
Linda
Ashley
Gareth
Jasmine
Karma
# sort names
Ashley
Gareth
Jasmine
Karma
Linda
```

这没什么火箭科学！然而，如果 `du` 的输出被送入 `sort` 会怎样？

```
# du -s * | sort
0 gif.gif
10464 IBM
13984 Lynx
16 Exchange
196 DEMO
3092 Gator
36 Craigslist
412 bin
48 elance
4 badjoke
4 badjoke.rot13
4 browse.sh
4 buckaroo
4 getmodemdriver.sh
4 getstocks.sh
4 gettermsheet.sh
76 CBO_MAIL
84 etcpasswd
```

确实，它被排序了。但可能不是你期望的那样——它是按 ASCII 数字字符排序的！不好。

2. 这就是 `-n` 标志至关重要的地方：指定 `-n` 后，`sort` 将假定行包含数字信息并按数值排序：

```
# du -s * | sort -n
0 gif.gif
4 badjoke
4 badjoke.rot13
4 browse.sh
4 buckaroo
4 getmodemdriver.sh
4 getstocks.sh
4 gettermsheet.sh
16 Exchange
36 Craigslist
48 elance
76 CBO_MAIL
84 etcpasswd
196 DEMO
412 bin
3092 Gator
10464 IBM
13984 Lynx
```

如果我说的话，这是一个更有用的结果！

3. 我在这里想改变的唯一一点是，我希望最大的目录排在最前面，最小的排在最后。

`sort` 的顺序可以用 `-r` 标志反转，这就是需要的魔力：

```
# du -s * | sort -nr
13984 Lynx
10464 IBM
3092 Gator
412 bin
196 DEMO
84 etcpasswd
76 CBO_MAIL
48 elance
36 Craigslist
16 Exchange
4 gettermsheet.sh
4 getstocks.sh
4 getmodemdriver.sh
4 buckaroo
4 browse.sh
4 badjoke.rot13
4 badjoke
0 gif.gif
```

最后一个概念，我们就可以继续了。如果你只想查看特定目录中最大的五个文件或目录，你所需要做的就是将命令序列管道传输到 `head`：

```
# du -s * | sort -nr | head -5
13984 Lynx
10464 IBM
3092 Gator
412 bin
196 DEMO
```

这个 `sort | head` 序列在本小时稍后将证明非常有用。

Unix 的一个关键概念是理解所有命令本质上都是乐高积木，你可以以任何方式组合它们以获得你想要的确切结果。在这方面，`sort -rn` 是一个很棒的组件，随着你对系统管理了解的深入，你会一次又一次地使用它。

### 识别最大的文件

我们已经探索了 `du` 命令，撒了一些 `sort` 来增加趣味，现在是时候完成一个典型的系统管理员任务：查找系统中给定区域中最大的文件和目录。

#### Task 3.4: 查找大文件

`du` 命令提供了查找最大目录或最大文件和目录组合的能力，但它没有提供仅检查文件的方法。让我们看看如何解决这个问题。

+   1. 首先，很明显以下命令会生成我主目录中最大的五个目录的列表：

```
# du | sort -rn | head -5
28484 .
13984 ./Lynx
10464 ./IBM
6848 ./Lynx/src
3092 ./Gator
```

类似地，`/usr/share` 中以及整个文件系统（忽略可能的 `/proc` 错误）中最大的五个目录：

```
# du /usr/share | sort -rn | head -5
543584 /usr/share
200812 /usr/share/doc
53024 /usr/share/gnome
48028 /usr/share/gnome/help
31024 /usr/share/apps
# du / | sort -rn | head -5
1471213 /
1257652 /usr
543584 /usr/share
436648  /usr/lib
200812  /usr/share/doc
```

一切都很好，但如何查找和测试仅文件呢？

2. 最简单的解决方案是使用 `find` 命令。`find` 将在本书后面更详细地介绍，但现在，只需记住 `find` 让你可以快速搜索整个文件系统，并对所有匹配选择条件的文件执行你指定的操作。

对于此任务，我们希望将选择限制为所有常规文件，这将省略目录、设备驱动程序和其他不寻常的文件系统条目。这是通过 `-type f` 完成的。

此外，我们将使用 `find` 的 `-printf` 选项来产生我们想要的确切输出。对于匹配的文件。在这种情况下，我们希望文件大小以千字节为单位，以及完全限定的文件名。这使用 `printf` 格式字符串 `%k %p` 就可以惊人地轻松完成。

> 如果这一切现在看起来像希腊语一样，不要太担心。第 12 小时“管理磁盘配额”将讨论 `find` 的许多精彩功能。现在，只需在书中输入你看到的内容即可。

把这些全部放在一起，你得到的命令是

```
find . -type f -printf "%k %p\n"
```

这里的两个新增内容是 `.`，它告诉 `find` 在当前目录开始搜索，以及格式字符串中的 `\n` 序列，它在每个条目后被翻译为回车。

3. 让我们看看它在实际中的效果：

```
# find . -type f -printf "%k %p\n" | head
4 ./kde/Autostart/Autorun.desktop
4 ../kde/Autostart/.directory
4 ../emacs
4 ../.bash_logout
4 ../.bash_profile
4 ../.bashrc
4 ../.gtkrc
4 ../.screenrc
4 ../.bash_history
4 ../.badjoke
```

你可以看到 `sort` 命令将在何处发挥作用！事实上，让我们在 `head` 前加上 `sort -rn` 来识别当前目录中最大的十个文件，或如下所示：
