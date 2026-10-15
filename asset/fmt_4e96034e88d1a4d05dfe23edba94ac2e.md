
要仅对文件中包含数据的行编号，请使用此命令：

```
nl file1
```

要对文件中的每一行编号（无论该行是否有数据），请使用：

```
nl -ba file1
```

预计你会将 `nl` 命令与 `pr` 和 `tac` 等命令链或管道使用以产生特定的输出。顺序很重要，因此请注意问题是要求对所有行编号还是仅非空行。

> 注意
> 
> 使用 `nl` 命令为文件行编号的一个实际示例发生在作者职业生涯早期。当时有一个庞大的编程团队，我们经常会对代码库进行打印以供团队审查。在发现如何以自动化的方式为文件的所有行以及页面正确添加行号之前，准备会议需要花费很长的时间。

在许多情况下，确定特定文件或输出的行数或单词数是非常有用的。`wc` 命令显示三种计数中的任意一种：

- `-l`—输出行数
- `-w`—输出单词数
- `-c`—输出字符（或字节）数

例如，查看系统当前有多少用户的一种极方法是使用 `wc` 统计来自 `who` 或 `w` 命令的输出行数：

```
who | wc -l
34
w | wc -l
36
```

这两个命令都在同一个系统上执行的，紧挨着，用户数量相同。

> `w` 命令有两个被 `wc` 程序计数的表头行，而 `who` 命令仅为每个用户输出一行。在用 `wc` 统计项目之前先查看输出，要小心；否则你将报告错误或表示不准确的信息。

### 制表符 (Tabs)

当输出针对屏幕进行格式化时，制表符分隔的文件可能会由于每个字段数据的长度而导致列对齐异常。`expand` 命令帮助将制表符转换为固定数量的空格。

考虑一个包含以下行的文件（行号仅供参考）：

```
1: steve      johnson
2: guillermo  villalobos
3: bo         regard
4: lawrence   aribusacus
5: marge       innovera
```

如果使用制表符分隔数据字段，第 1、3、5 行在字段 1 和 2 之间将有两个制表符，这样列就会对齐。由于第一个字段的长度，第 2 和 4 行将只有一个制表符。`expand` 将制表符转换为固定数量的空格，在大多数情况下使数据显示正确。

> 考试时要小心。你会遇到许多关于 `expand` 命令的听起来很有道理的干扰项，可能包括 `paste` 命令，它是用于在其他格式之间转换的。

# 割列 (Cutting Columns)

会有很多时候，你需要取一个包含列数据的文件（无论分隔符或分隔符是什么），并按列提取信息，或者可能重新排列列以使其更易用。虽然你在这里没有包含 `awk` 命令（处理列式数据的类型），但它们使用 `cut` 命令，该命令更适合这项任务：

```
cut -c 20-40 /etc/passwd | tail -n 5
var/spool/postfix
home/share/bash
ross brunson:/home
```

要打印每个重复行的每一个实例，请使用此命令：

`uniq -D bigpasswd`

# 正面还是反面？

`head` 命令主要用于（且默认情况下）查看给定文本文件的前 10 行。`head` 可以配置为从文件顶部开始显示特定数量的行。`-n` 参数后面要从文件开始显示的行数，用于显示比默认值更多的内容。该参数的使用方式如下：

点击此处查看代码图片

```
head -n 5 /etc/fstab
LABEL=/               ext3 defaults
1 1
none                   /dev/pts devpts gid=5,me
atime=620
0 0
none                   /proc defaults
0 0
none                   /dev/shm tmpfs defaults
0 0
/dev/hda6             swap swap defaults
0 0
```

![](img/16cd7204aa58beaaf530d67f50f15fc5_243_0.png)

`head` 命令无法显示行范围，只能从文件开始显示。

`tail` 命令与 `head` 命令完全相反：它默认显示给定文件的最后 10 行，可以配置为显示更少或更多行，但只能从文件末尾开始。它可以显示范围。这里是一个示例：

点击此处查看代码图片

```
tail -n 5 /etc/passwd
netdump:x:34:34:Network Crash Dump user:/var/crash:/bin/bash
quagga:x:92:92:quagga routing
suite:/var/run/quagga:/sbin/nologin
radvd:x:75:75:radvd user:/sbin/login
rbronson:x:500:500::/home/rbronson:/bin/bash
snuffy:x:501:501::/home/snuffy:/bin/bash
```

`tail` 命令也用于跟踪日志文件，例如 `/var/log/messages` 文件，以查看最新的系统登录尝试：

`tail -f /var/log/messages`

这将返回与此处所示类似的输出：

点击此处查看图片

```
Feb 23 21:00:01 localhost sshd(pam_unix)[29358]:nsession closed for root
Feb 23 21:00:04 localhost sshd(pam_unix)[29501]:nsession opened for root by (uid=0)
Feb 23 21:00:13 localhost sshd(pam_unix)[29501]:nsession closed for user root
Feb 23 21:00:16 localhost sshd(pam_unix)[29549]:nsession opened for root by (uid=0)
```

当结合使用这两个命令时，可以实现非常有趣的事情。例如，假设你想查看一个 50 行文件的第 31 到 40 行。记住，任一命令都无法显示范围，但通过将它们结合起来，你可以使用以下命令显示 `50linefile` 中某个范围的行：

点击此处查看图片

```
head -n 40 50linefile | tail
31
32 Both software and hardware watchdog drivers are available in
1
33 kernel. If you are using the software watchdog, you probably
also want
34 to use "panic=60" as a boot argument as well.
35
36 The wdt card cannot be safely probed for. Instead you need to pass
37 wdt=ioaddr,irq as a boot parameter - eg "wdt=0x240,11".
38
39 The SA1100 watchdog module can be configured with the
"sa1100-"
40 commandline argument which specifies timeout value in seconds.
```

考试中请留意 `head` 和 `tail` 命令——特别是用于跟踪日志文件最新内容的 `-f`。

# 切分文件

`split` 命令用于将大量记录拆分成多个包含特定数据量的独立文件。

`split` 命令的选项包括（`#` 字符表示前缀字符的数量）：

- `-a #`—使用指定长度的字符（默认为 xaa）。
- `-b`—输出文件包含指定字节数的数据。
- `-c`—输出文件包含指定行数的字节数据。
- `-l`—输出文件包含指定行数的数据。

`#` 值可以是 b（即 512 字节）、k（即 1024 字节）或 m（即 1024 千字节）。例如，如果你需要将一个 8.8MB 的文本文件拆分成 1.44MB 的块，可以使用此命令：

点击此处查看代码图片

```
split -b1440000 bigtextfile.txt
ls -l
-rw-r--- 1 root 1440000 Feb 23 09:25 xaa
-rw-r--- 1 root 1440000 Feb 23 09:25 xab
-rw-r--- 1 root 1440000 Feb 23 09:25 xac
-rw-r--- 1 root 1440000 Feb 23 09:25 xad
-rw-r--- 1 root 1440000 Feb 23 09:25 xae
-rw-r--- 1 root 1440000 Feb 23 09:25 xaf
-rw-r--- 1 root 1440000 Feb 23 09:25 xag
```

> 注意
> 
> 在考试时，预计将具有已知行数的文件拆分成多个文件，能够确定文件的默认名称，并知道 `split` 命令生成了多少个文件。

# 反向 cat

在某些情况下，你希望反向或倒序显示文件，这时 `tac` 命令派上了用场。你可以这样使用它：

```
cat file1
```

这将产生类似以下的输出：

点击此处查看图片

```
1 Watchdog Timer Interfaces For The Linux
2 Alan Cox <xorguk.ukuu.org>
3
4
5 Linux Driver And Development
```

在该文件使用 `tac` 会产生：

```
tac file1
```

这将产生类似以下的输出：

点击此处查看图片

```
5 Linux Driver And Development
4 Alan Cox <xorguk.ukuu.org>
2
1 Watchdog Timer Interfaces For The Linux
```

# 安全查看二进制文件

许多管理员意外使用 `cat` 将文件内容发送到屏幕，结果显然包含了机器码或语言。通常你可以输入 `clear` 让屏幕恢复，然后必须使用 `cat` 的工具查看该文件的内容。

![](img/16cd7204aa58beaaf530d67f50f15fc5_246_0.png)

你通常会 `od` 命令安全地查看二进制或非 ASCII 文件；否则显示可能会乱码，系统将尝试解释二进制文件中的控制代码。`od` 可以以不同的方法显示文件，包括：

- `-a`—命名
- `-o`—八进制
- `-d`—十六进制
- `-f`—浮点

这些格式大多数用于日常使用，只有十六进制格式非常感兴趣。

> 注意
> 
> 注意如何查看二进制文件。`od` 命令是这种查看唯一可能。如果在意外查看二进制文件后控制出现问题，使用 `reset` 命令。它会重新初始化终端使其再次可读。另一个选项是 `strings` 命令，它可以显示二进制文件中包含的文本而不是弄乱屏幕。

# 格式化命令

![](img/16cd7204aa58beaaf530d67f50f15fc5_247_0.png)

`pr` 和 `fmt` 命令用于文本流或文件的打印换行和格式化，并且经常配合使用，为特定目的正确格式化文本，无论是同行评审还是喜欢阅读代码的经理。

> 注意
> 
> 我们之前使用了以下 `50linefile`，它已经被 `nl` 命令标记了编号，所以如果你在尝试这样做但没有名为 `50linefile` 的文件或者你的文件没有编号，请返回完成执行此操作的之前的示例。

`pr` 命令用于源代码和其他文本文件的打印格式化。它在每个格式化后的文件顶部添加日期和时间块、文件名（如果存在）以及页码，如下所示：

```
pr 50linefile
```

这将产生与此处所示类似的输出：

点击此处查看代码图片

```
2112-02-23 21:19
50linefile
Page 1
```

# Linux Watchdog Timer Interfaces

操作系统

2

3

4

5

Alan Cox <alan@lxorguk.ukuu.org.uk>

Custom Linux Driver And Program Development

`pr` 命令可以显示列数据，调整列以适应每页数量，如下：

点击此处查看代码图片

```
pr --columns=2 50linefile
2004-02-23
21:02 50linefile
```

| 1 Watchdog Timer Inte | 26 and some Berkshire |

| cards. T 2 | 27 internal temperature |

| 3 Alan Cox <a | 28 giving the temperature. 4 29 |

| 5 Custom Linux D | 30 The third interface logs ke |

`fmt` 命令用于格式化文本文件，但它限于限于折长行以适应较小的页面或 `pr` 设置的列。

之前的 `pr` 列示例会截断列数据，导致页面数据丢失。可以通过混合命令来修复，如下所示：

点击此处查看代码图片

```
[root]@local host]# fmt -35 50linefile | pr --column=2
2004-02-23 21:49 50linefile
```

| 1 Watchdog temperature. 29 30 The third | Timer Interfaces For The interface logs kernel messages |

| Linux Operating System 2 on additional alert events. |

| 3 Alan Cox 31 32 Both software and |

## 翻译文件

`tr` 命令用于更改文件或流中的字符，而不是整个单词或短语——那是 `sed` 要做的工作。

例如，如果你有一个文件，包含了书中示例中的许多命令，但由于某些命令因为编辑器将行首字母大写了而无法运行，你可以使用以下命令将文件中的大写字母转换为小写字母：

点击此处查看代码图片

```
tr 'A-Z' 'a-z' < commands.txt
```

`tr` 命令无法自己读取输入，也不接受文件作为参数。这虽然不公平，但我们说 `tr` 命令没有 `cat` 智能，因为 `cat` 可以自己读取输入。因此，在这种情况下在使用 `tr` 时，`<` 运算符是强制性的；否则命令将无法工作。

可以使用以下命令实现相同的结果：

点击此处查看代码图片

```
tr [:upper:] [:lower:] < commands.txt
```

> 注意
> 
> 记住 `tr` 无法自己读取输入，也不接受文件作为参数，因此需要 `<` 重定向符号来将文件发送到命令。任何其他操作都是错误的命令并会产生语法错误。

## He sed, She sed

`sed` 命令（或称为流编辑器）用于处理并对文本流执行操作，例如文本文件中的行。`sed` 强大得惊人，换句话说，它可能很难使用。

关于 `sed` 工作原理的一个很好的类比是：想象你的文本文件是一根从房间一侧延伸到另一侧的长字符串。在这根字符串上，你可以放置一些特殊的转换珠子并让它们沿着字符串向下滑动，让它们在沿字符串或文件行滑动时执行特定的转换。`sed` 的妙之处在于，你可以堆叠这些珠子，或者让它们排在其他珠子后面，通过单个命令或一组命令实现对文本文件几乎近乎魔法般的转换。

## 核心主题

`sed` 最常用的操作之一是搜索和替换文本，包括单词和完整的短语。而 `tr` 仅对单个字符/数字进行操作，`sed` 则能够胜任复杂的功能，包括每行多次操作。

`sed` 使用以下语法执行命令：

点击此处查看代码图片

```
sed -option action/regexp/replacement/flag filename
```

与其费结于解释输入某些选项后会发生什么，不如来看看当我们使用这些选项时 `sed` 做了什么。正确使用 `sed` 包括能够，额，“复用”其他系统管理员的 `sed` 命令。

要替换给定文件中每行的第一个实例 `bob` 为 `BOB`，请使用此命令：

```
sed s/bob/BOB/ file1
```

要替换给定文件中每行中所有的 `bob` 为 `BOB`，请使用此命令：

```
sed s/bob/BOB/g file1
```

`sed` 允许对给定流的行进行多次操作，所有操作都会在处理下一行之前完成。

要对给定文件的每行、每个实例搜索并替换 `bob` 为 `BOB`，然后搜索 `BOB` 并将其替换为 `snuffy`，请使用以下：

点击此处查看代码图片

```
sed 's/bob/BOB/g ; s/bob/snuffy/g' file1
```

分号字符的使用类似于 bash 运行多个相互独立命令的能力。然而，这整个操作——从第一个单引号（''）到最后一个引号——都是在 `sed` 内部执行，而不是作为 bash 的一部分。

当 `sed` 用于多个命令时，你可以使用分号来分隔命令，或使用多个 `-e` 实例来执行多个命令：

点击此处查看代码图片

```
sed -e s/bob/BOB/g -e s/BOB/snuffy/g file1
```

在考试中，以及当你需要在模式中使用空格使用 `sed` 时，请将模式/程序用单引号括起来，例如：

点击此处查看代码图片

```
sed 's/is not/is too/g' file1
```

这可以防止你因为字符串中的空格而导致语法错误。早晚，你会厌倦了为 `sed` 输入相同的操作，并想要使用脚本或某些自动执行重复任务的方法。`sed` 能够使用包含一组过程的简单脚本文件。这里显示了 `sed` 脚本文件中一组过程的示例：

```
s/bob/BOB/g
s/BOB/snuffy/g
```

该脚本文件以以下方式使用：

点击此处查看代码图片

```
sed -f scriptfile targetfile
```

在单个流上可以执行许多个过程，整组过程会在每个后续行上依次执行。
