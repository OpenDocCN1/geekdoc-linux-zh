
当运行 `ls` 命令时，注意不同类型的文件通常用不同的颜色表示；然而，表示某些类型文件的特定颜色可能会根据终端或发行版的不同而异。因此，不要使用颜色来判断文件类型。

提示

## 查看文件和目录

Windows 使用 `dir` 命令列出文件和目录；为了方便 Windows 用户学习 Linux，Linux 中也有一个 `dir` 命令，它仅仅是 `ls` 命令的指针或快捷方式。

> 注意

回想上一章，你可以使用开关参数来改变命令的行为。要查看文件和目录列表，请对 `ls` 命令使用 `-F` 开关：

```
[root@server1 root]# pwd
/root
[root@server1 root]# ls -F
current@ myprogram* project project12 project2 project4
Desktop/ myscript* project1 project13 project3 project5
[root@server1 root]#_
```

`ls -F` 命令在每个文件名末尾添加一个字符来指示文件类型。在前面的输出中，注意文件名 Desktop、myprogram 和 myscript 后面添加了特殊字符。`@` 符号表示链接文件，`*` 符号表示可执行文件，`/` 表示子目录，`=` 字符表示套接字，`|` 表示管道。所有其他文件类型末尾都没有添加特殊字符，可能是文本文件、二进制数据文件或设备文件。

以大写字母开头命名目录是一种惯例，正如前面输出中 Desktop 目录中的字母 D 一样。这确保了目录会列在 `ls` 输出的开头，并让你在运行不带指定文件类型的 `ls` 命令时，能够快速确定哪些名称是指目录。

> 注意

虽然 `ls -F` 命令是一种以易读格式获取文件类型信息的快速方法，但你需要获取关于每个文件的更详细信息。可以使用 `ls -1` 命令为特定目录中的每个文件提供详细列表。

# 第 4 章 探索 Linux 文件系统

```
-rw-r--  1 root root    99 Apr  7 10:01 project4
-rw-r--  1 root root   108 Apr  7 10:01 project5
[root@server1]# 
```

上一个示例中列出的每个文件从左到右列出了八部分信息：

- 1. 一个文件类型字符

    - `d` 字符表示目录。
    - `l` 字符表示符号链接文件（在第 5 章“Linux 文件系统管理”中讨论）。
    - `b` 或 `c` 字符表示特殊设备文件（在第 6 章讨论）。
    - `n` 字符表示命名管道。
    - `s` 表示套接字。
    - 该字符表示所有其他文件类型（文本文件、二进制数据文件）。

- 2. 文件权限列表（也称为文件的模式）
- 3. 硬链接计数（在第 5 章讨论）
- 4. 文件所有者（在第 5 章讨论）
- 5. 文件组所有者（在第 5 章讨论）
- 6. 文件大小
- 7. 文件的最后修改时间
- 8. 文件名（某些文件是其他文件的快捷方式或指针，用箭头 `->` 指示，如前面输出中名为“current”的文件；这些是符号链接，将在第 5 章中讨论）。

对于上一个示例中名为 `project` 的文件，你可以看到该文件是一个普通文件，因为它的详细列表以 `-` 字符开头，文件权限为 `rw-r--r--`，硬链接计数为 1，所有者为 `root`，组所有者为 `root`，大小为 99 字节，修改时间为 4 月 7 日 10:01，文件名为 `project`。（注意：此处 OCR 文本略有混乱，已根据提供的代码块进行重构）。

## 查看文件和目录

表 4-2 ls 命令的常用选项

| 选项 | 说明 |
| --- | --- |
| -a | 列出所有文件名 |
| --all | 列出大多数文件名（排除 . 和 .. 特殊文件） |
| --almost-all | 以列格式显示文件名 |
| -C | 不带颜色列出文件名 |
| --color=n | 列出目录名称而非内容 |
| -d | 不排序列出所有文件名 |
| --directory | 按文件类型分类列文件名 |
| -F |  |
| --full-time | 以长格式列出文件名并显示修改时间 |
| -l | 以长格式列出文件名 |
| -lh | 以长格式列出文件名并带有易读（人类读）的文件大小 |
| -1 --human-readable | 以长格式列出文件名，但省略组信息 |
| --no-group |  |
| -O | 反序列出文件名 |
| -r |  |
| --reverse | 列出指定目录及所有子目录中的文件名 |
| -R |  |
| --recursive -s | 列出文件名及其以千字节（KB）计算的大小 |
| -S | 按文件大小排序列出文件名 |
| -t | 按修改时间排序列出文件名 |
| -U | 不排序列出文件名 |
| -x | 以行而非列列出文件名 |

# 通配符元字符

在上一节中，你看到元字符 `*` 用于指示或“匹配”当前目录下的所有文件，这就像通配符在卡牌游戏中匹配某些卡牌一样。因此，`*` 元字符被称为通配符元字符。这些字符可以简化在命令行上指定多一个文件名的命令，正如你之前使用 `file` 命令时看到的那样。这些元字符由 shell 解析，并可以用于大多数常见的 Linux 文件系统命令，包括已经提到的几个命令（ls、file 和 ed）。这些元字符匹配文件名的某些部分或整个文件名本身。表 4–2 显示了通配符元字符列表及其说明。

## 表 4-3 通配符元字符

| 元字符 | 说明 |
| --- | --- |
| * | 匹配文件名中的 0 个或多个字符 |
| ? | 匹配文件名中的 1 个字符 |
| [aegh] | 匹配文件名中的 1 个字符——只要该字符是 a、e、g 或 h |
| [a-e] | 匹配文件名中的 1 个字符——只要该字符是 a、b、c 或 e |
| ![la-e] | 匹配文件名中的 1 个字符——只要该字符不是 a、b、c、d 或 e |

可以使用 ls 命令来演示通配符。下面显示了使用通配符缩小 `ls` 命令输出列表的示例。

```
[root@server1]## ls
current myprogram project project12 project2 project4
Desktop myscript project1 project13 project3 project5
[root@server1]## ls*
project1 project12 project13 project2 project3
project4 project5
[root@server1]## ls?
project1 project2 project3 project4 project5
[root@server1]## ls??
project12 project13
[root@server1]## ls project[135]
project1 project3 project5
[root@server1]## ls[!135]
project2 project4
```

# 显示文本文件的内容

到目前，本章讨论了用于导航 Linux 目录结构和文件类型的命令；通常需要显示这些文件的内容。到目前为止，用户显示的最常见类型是文本文件。这些文件通常很小，包含配置信息或指令（称为 shell 脚本），也可以包含其他形式的文本，例如电子邮件。要在终端屏幕上查看整个文本文件（也称为连接），你可以使用 `cat` 命令。以下是使用 `cat` 命令显示电子邮件（在虚构的 project4 中）内容的示例：

```
[root@server1]## ls
current myprogram project project12 project2 project4
Desktop myscript project1 project13 project3 project5
[root@server1]## cat project4
Hi there, I hope this day finds you well.
```

# 显示文本文件的内容

遗憾的是，今年我们在阿冈昆比公园度假时没能去你们的餐厅坐——我特别想看到餐厅里 Highland Inn 的模型和火车站模型。

我一直在阅读关于阿冈昆比公园的历史，但无论在哪里都找不到关于 Highland Inn 最初位于 Cache 湖何处的描述。

如果不麻烦的话，能否请告诉我，这样我就不必等到明年拜访你们的小木屋了？

此致，

Mackenzie Elizabeth

你可以通过向 `cat` 命令传递 `-n` 选项，除了内容外还可以显示文件中每一行的行号。在下面的示例中，显示了 project文件的行数：

```
[root]@server1 root]# cat -n project4
1 Hi there, I hope this day finds you well.
2 Unfortunately we were not able to make it to your dining room this year while vacationing in Algonquin Park - I
3 especially wished to see the model of the Highland
4 Inn and the train station in the dining room.
5 I have been reading on the history of Algonquin Park but
6 where no could I find a description of where the Highland
7 Inn was originally located on Cache lake.
8 If it is no trouble, could you kindly let me know such
9 that I need not wait until next year when I visit your lodge?
10 Regards,
11 Mackenzie Elizabeth
```

在某些情况下，你可能想反序显示文本文件的内容，这对于那些由系统服务持续追加的文件很有用。这些文件被称为日志文件，最新的条目位于底部。要反序显示文件，请使用 `tac` 命令（tac 是 cat 的反过来），如下 project4 所示：

```
[root]@1 root]# tac project4
Mackenzie Elizabeth
Regards
```

如果显示的文件很大，你想查看它的前几行，请使用 `head`。该命令将文件的前 10 行（包括空行）显示在终端屏幕上，也可以带有指定不同行数的数值选项。下面显示了使用 `head` 命令查看 project4 文件顶部的示例：

```
[root]@server1 root]# head project4
Hi there, I hope this day finds you well.
```

遗憾的是，今年我们在阿冈昆比公园度假时没能去你们的餐厅坐——我特别想看到餐厅里 Highland Inn 的模型和火车站模型。

我一直在阅读关于阿冈昆比公园的历史，但无论在哪里都找不到关于 Highland Inn 最初位于 Cache 湖何处的描述。

```
[root]@server1 root]# head -3 project4
Hi there, I hope this day finds you well.
```

正如该命令显示文本文件的开头一样，`tail` 命令可以用于显示文本文件的结尾。默认情况下，`tail` 命令显示文件的最后 10 行，但也可以带有指定在终端屏幕显示行数的数值选项，如下面的 project4 文件示例所示：

```
[root]@server1 root]# tail project4
```

## 显示文本文件的内容 139

此致，

Mackenzie Elizabeth

[root@server1 #]# tail -2 project4

此致，

Mackenzie Elizabeth

[root@server1 #]#_

`tail` 命令还接受另一个选项，用于指定从终端屏幕开始显示文本的行数。例如，要从文本文件的第 10 行开始显示直到文件末尾，只需对 `tail` 命令使用 `+10` 选项即可，如下所示：

```
[root@server1 root]# tail +10 project4
Inn was originally located in Cache lake.
```

如果不麻烦的话，能否请你告诉我我不需要等到明年去拜访您的旅馆时了，

此致，

Mackenzie Elizabeth

[root@server1 #]#_

虽然某些文本文件可以完整显示在终端屏幕上，但你可能会遇到大到无法完全显示的文件。在这种情况下，`cat` 命令按顺序将整个文件内容显示在终端屏幕上，由于屏幕空间不足，文件的顶部将无法显示。因此，使用 `more` 或 `less` 命令按页显示文本文件是很有用的。

`more` 命令的名字源于 UNIX 系统上使用的 `pg` 命令。

该命令在终端屏幕上从文件开始逐页显示文件；按下空格键或回车键进入下一页，依此类推。

`more` 命令的功能比 `pg` 多，因为当你按下空格键时，它会显示文本文件的整页，但按下回车键时仅显示文本文件的一行。这样，你就可以按页或按行浏览文本文件的内容。

虚构的项目 `project5` 是莎士比亚悲剧《麦克白》节节，它太大，无法使用 `cat` 命令在终端屏幕上完整显示。使用 `more` 命令得到的输出结果如下：

```
[root@server1 #]# project5
Go bid thy mistress, when my drink is ready,
Strike upon the bell. Get thee to bed.
is this a dagger which I see before me,
The handle toward my hand? Come, let me clutch thee.
i have thee not, and yet I see thee still.
Art thou not, fatal vision, sensible
to feeling as to sight? or thou but
Dagger of the mind, a false creation,
Proceeding from the heat-oppressed brain?
```

# 第 4 章 探索 Linux 文件系统

I see thee yet, in form as palpable

As this now I drew.

Thou marshall'st me the way that I was going;

And such an instrument I was to use.

Mine eyes are the fools o' the other senses,

Or else all the rest; I see thee still,

On thy blade and dudgeon gout of blood,

Which was not before. There's no such thing:

It is the bloody business that informs

Thus mine eyes. Now o'er the one halfworld

Nature seems dead and wicked dreams abuse

The curtain'd slip; witchcraft celebrates

Pale Hec's offerings, and with'der murder,

Alarum'd by his sentinel, the wolf,

----(71%)

注意前述输出，`more` 命令在显示第一页时不会返回返回 shell 提示符。相反，`more` 命令会在终端屏幕底部显示一个提示符，指示屏幕上显示的内容占文件总大小的百分比。在前面的示例中，显示了 `project5` 文件的 71%。在此提示符处，你可以按空格键翻一页，或按回车键翻下一行。此外，`more` 命令允许在此提示符处进行其他用户交互。在提示符处按 `h` 字符将显示如下输出所示的帮助屏幕，按 `q` 字符将完全退出 `more` 命令，而不查看文件的剩余部分。

----(71%)

大多数命令可选前带一个整数参数 `k`。

默认值在括号中。星号 (*) 表示参数变为新的默认值。

```
<space>                              显示下 k 行文本 [当前
screen size]                           显示下 k 行文本 [当前
z screen size]*
<return>                          显示下 k 行文本 [1]*
d or ctrl-l*                      滚动 k 行 [当前大小，
ially 11)
q or Q <interrupt>               退出 more 向前跳过 k 行文本 [1]
f                               向前跳过全屏文本 [1]
b or ctrl-B                       向后跳过全屏文本 [1]
'                               跳转到上一次搜索的位置
=                              显示当前行号
/<regular expression>           搜索正则表达式的第 k 次出现[1]
搜索上一个 r.e. 的第 k 次出现 [1]
!<cmd> or :!<cmd>             在子壳中执行 <cmd>
```

## 显示文本文件的内容 141
