
3. 有两种不同的方法可以让 UNIX 匹配包含 `not` 和 `cold` 单词的所有行：一种是使用 `grep` 和管道。请展示这两种方法。

4. 在各种 `grep` 命令中使用 `-v` 标志，并显示匹配以下行所需的命令和模式：

```
不包含 cabana
不包含 jazz 或 funk
不包含 jazz, funk, disco, blues 或 ska。
```

5. 结合使用 `ts -l`、`cat -n` 和 `grep` 来找到你系统中 `/etc` 目录下第 11 个或第 24 个文件的名称。

6. 有两种方法可以查找包含 jazz、funk、disco、blues 和 ska 其中任何一个单词的行。请展示这两种方法。

4. 下面命令的作用是什么？

```
sed "s/:*/ /;/" /etc/passwd | head
```

7. 这一个命令的作用又什么？

```
sed "s/^$/ /" < testme
```

# 下一小时预览

在接下来的一小时里，你将学习一些更高级的管道命令以及极其强大的过滤器 `awk`。

# 第 10 小时

# 强过滤器与文件重定向

在这一小时中，你将戴上编程的帽子，学习两个可以无限自定义并用于各种任务的强大命令。其中第一个是 `awk`，它可以让你提取特定列的信息，在文本流经时对其修改，甚至交换文件中信息列的顺序。

另一个是 `tee` 程序，它允许你保存在管道中传输的数据副本。

# 本小时学习目标

在这一小时中，你将学习：

- 如何使用万变且奇妙的 `awk` 命令
- 如何使用 `tee` 重新路由管道

从上一小时（你学习了 `grep` 命令）开始，你正在学习可能需要花费数月才能掌握的命令。在本小时处理的命令之一 `awk` 甚至有专门为它编写的著作，如果你能想象出那种事的话。我这样做是为了设定背景：这是一个复杂且非常强大的命令。由于需要，你只需要学习这些命令中较简单的功能，但不要担心。

最后，如果没有一两个与管道相关的命令，水管比喻又算什么呢？UNIX 正是一个拥有各种奇怪命令名称的系统。所说的命令就是 `tee`。

## 任务 10.1：万变且奇妙的 awk 命令

尽管 `sed` 命令对管道编辑任务大有所帮助，但要获得真正的力量，你需要调用 `awk` 程序。`awk` 程序是一个用于分析和处理包含单词的文本文件的编程工具包。它是 UNIX 中最有用的通用过滤器之一。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_197_0.png)

> 当然，你可能奇怪 `awk` 的名字从哪里来。最初的猜测是它指的是其尴尬的语法（awkward），但并不完全准确。这个名字源于作者的姓氏：Aho、Weinberg 和 Kernighan。

等一下

与 `sed` 类似，`awk` 可以直接接受命令作为参数。你也可以将程序写入文件并让 `awk` 读取该文件以获取指令。使用该程序的通用方法是 `awk { commands }`。`awk` 有两个可能的标志：`-f file` 指定应从文件而不是命令行读取指令；`-Fc` 表示程序应该将字母 `c` 视为信息字段之间的分隔符（例如一个或多个空格或制表符），而不是默认的空白符（例如一个或多个空格或制表符）。

动作

- 要学习的第一个 `awk` 命令在我看来也是最通用的：`print` 命令。在不带任何参数的情况下，它逐行打印文件中的内容：

```
% who | awk '{ print }'
root      console Nov  9 07:31
yuenca    ttyAo  Nov 27 17:39
timyx4    ttyAp Nov 27 17:22
wifey     ttyAx Nov 27 17:16
tobster   ttyAz Nov 27 17:59
taylor    ttyqh Nov 27 17:43
```

一行输入被拆分为特定的字段，每个字段被分配一个唯一的标识符。字段一是 `$1`，字段二是 `$2`，依此类推：

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_197_1.png)

# 强过滤器与文件重定向

```
% who | awk '{ print $1 }'
root
yuenca
wifey
tobster
taylor
```

好消息是，你也可以通过双引号指定打印的任何其他信息：

```
% who | awk '{ print " $1 "}'
root is terminal line console
yuenca is terminal line ttyAo
linyx4 is terminal line ttyAp
wifey is terminal line ttyAx
taylor is terminal line ttygh
```

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_198_0.png)

> 你不能使用单引号来包围打印参数，因为这会与单引号冲突。现在回到 `/etc/passwd` 看看 `awk` 如何帮助你理解内容：

```
% grep taylor /etc/passwd | awk -F: '{ print $7 }'
login shell is /bin/bash
mtaylor is /local/bin
taylor is /bin/bash
taylorm is /bin/bash
```

3. 在我处理这些示例时，出现了一个有趣的案例：使用了多少种不同的登录壳（login shells）以及哪最流行。在系统中，你可能需要写一个程序来解决这个问题；使用 `awk` 和其他工具，UNIX 提供了：

```
% awk -F:'print $7' /etc/passwd | sort | uniq -c
2365 /bin/csh
84 /bin/bash
21 /bin/sh
353 /local/bin/tcsh
45 /local/lib
```

# 第 10 小时

然后让我找出哪些出现的次数最多，这在你的系统中也是如此。4. 在密码文件中，请注意到名字都是“名-姓”的格式。也就是说，我的账户是 Dave Taylor。你可能需要生成一个用户报告，但你希望按姓对它们排序。你可以使用 `awk` 做到，首先去掉那些讨厌的逗号：

```
% grep taylor /etc/passwd | awk -F: '{ print $5 }'
James Taylor,
Mary Taylor,
Dave Taylor,
Robert Taylor,
Melanie Taylor,
Dave Taylor,
```

这生成了用户列表。现在我将使用 `sed` 去掉那些逗号并使用 `awk` 反转名字顺序：

```
% grep taylor /etc/passwd | awk -F: '{print $5}' | sed 's/,//g'
| awk '{print $2","$1}'
Taylor, James
Taylor, Mary
Taylor, Dave
Taylor, Robert
Taylor, Melanie
Taylor, Dave
```

如果我将此命令的输出交给 `sort`，名字将按照所需的顺序列出：

```
% grep taylor /etc/passwd | awk -F: '{print $5}' | sed 's/,//g'
| awk '{print $2","$1}' | sort
Taylor, Dave
Taylor, Dave
Taylor, James
Taylor, Mary
Taylor, Melanie
```

这非常顺滑。它还说明了如何逐步构建所需的结果。5. 如果用户想让 `/bin/sh`——Bour shell——作为其默认 shell，最后一个字段可以留空：

```
joe::45:555:Joe-Bob Billiard,...:/home/joe:/bin/sh:/bin/sh
```

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_199_0.png)

这可能是个问题，因为空白字段会混淆 `awk` 程序；`awk` 只在统计字段。好消息是每行都有关联的字段数量，称为 `NF` 变量。使用美元符号，它表示一行中有多少字段：对于 `/etc/passwd`，之前的命令方法应该是：

```
% awk -F: '{print NF}'
```

6. 与 `NF` 类似的是 `NR`，它记录显示的记录数。这里有一种给文件编号的方法：

```
% ls -l | awk "%$0"
1: total 229
2: drwx- 2 taylor Nov 21 10:30 Archives/
3: drwx- 2 taylor Nov 16 16:55 Infolorld/
4: drwx- 2 taylor Nov 27 18:02 Mail/
5: drwx- 2 taylor Oct 6 09:36 News/
6: drwx- 2 taylor Nov 21 12:39 OLU/
7: drwx- 2 taylor Oct 15 21:48
8: -rw-rw-1 taylor 12556 Nov 16 09:49 keyline.pie
9: -rw-rw-1 taylor 11503 Nov 27 18:05 randy
10: drwx- 2 taylor Oct 13 10:45 src/
11: drwx- 2 taylor Nov 6 22:20 temp/
12: -rw-rw-1 taylor 0 Nov 27 18:22 testme
```

在这里你可以看到，行的零 字段是整整行。这非常有用：

```
% who | awk "{print \$0}"
ttyAb: limxy4 ttyAb Nov 27 16:22
ttyAt: ltbei ttyAt Nov 27 18:21
ttyAu: woodsoon ttyAu Nov 27 18:19
ttyAv: morning ttyAv Nov 27 18:19
ttyAw: hawk ttyAw Nov 27 18:12
ttyAx: wifey ttyAx Nov 27 17:16
ttyAz: wiwatr ttyAz Nov 27 18:22
ttyAA: chong ttyAA Nov 27 13:56
ttyAB: isidahax ttyAB Nov 27 18:20
```
