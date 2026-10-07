
文件中已添加了额外的名称。

## 此处文档 (Herefiles)

现在我已经解释了 `>`、` < ` 和 `>>` 的作用，而明显的问题是 `<<` 是什么，答案是它创建一个在此处文档（herefile）。

> “在此处文档，吗？”你说道。“从未听说过。它到底是什么？”

这是一个很好的问题。在此处文档允许你向 STDIN 输入大量行文本，直到遇到一个预定义的标记符，例如：

```
[ elvis@frogbog elvis $ cat ~newfile.txt << STOPHERE

> 这是一个新文件。我可以在里面放入很多文本。

>

> 如果我想这么做，我可以写上一整天天的文本。

>

> 我为什么要这么做？因为系统允许我这样做。

>

> 当然，系统允许我做各种愚蠢且毫无价值的事情。

>

> 我猜，垃圾进，垃圾出。
> STOPHERE
```

显而易见，在此处文档比简单的从 STDIN 读取要方便得多。其一，它们在每一行都提供了一个美观的提示符，使我们知道该预期得到什么。另一方面，它们避免了我们必须记住 Ctrl+D 是 Unix EOF（文件结束符）标记，即使没有在此处文档关键字，EOF 仍然会停止输入事件。2。

尽管如此，在我在第二部分讨论 shell 脚本之前，在此处文档并没有真正变得重要。这在书中讨论它们的逻辑位置。如果我不讨论它们，你仍然会好奇 `<<` 到底可能用于什么。

- 2. shell 中没有东西是万无不能的，但我们并不试图涵盖所有的 shell。我们的参考平台是 bash shell，我们在书中执行的大部分操作在 ksh 下也几乎完全相同。在这种情况下，在向在此处文档输入文本时，csh 不会提供提示符，尽管较新的 tsh 是提供的。我们将在第 6 章更详细地讨论 shell。

## 重定向 STDERR

既然我们已经使用了 `<`、`>`、`<<` 和 `>>`，那么我们如何重定向标准错误流（STDERR）呢？

遗憾的是，重定向 STDERR 的简单方法在 Bourne Shell 中不起作用，而大家都用它来编写 shell 脚本。此外，简单且逻辑上的答案是扩展现有语法使用 `>>>`，或者使用另一个符号，例如 `}`，或者与我们原始符号在视觉上相似的符号。在 Unix 上实际上有两种实现方法：简单（但不怎么实用的方法）和困难（但更有实用的方法）。

## 简单的方法

重定向 STDERR 的方法是将 STDERR 重定向到 STDOUT 的一个文件。你可以通过使用 `&` 重定向到文件来实现。假设我们正在运行 `find` 来列出系统上的所有文件，并且我们想要看到输出中的错误信息，而这些输出发送到一个文件中。可以使用命令 `find -name '*' -print > /all.txt`。输出（包括 find 的错误信息）将位于该文件中。

遗憾的是，如果我们只想重定向错误信息但保持输出显示在屏幕上，我们将遇到一些困难。要做到这一点，我们必须用“硬方法”来重定向 STDERR。

## 困难的方法

重定向 STDERR 的硬方法依赖于仅存在于某些 shell 中的功能：Bourne、Korn 和 Bash shell 都具有此功能。C Shell 和 tsh 则没有。更多细节请参阅第 6 章。现在，只需输入以下命令来查找你使用的是哪种 shell：³

```
cat /etc/passwd|grep username:cut -d : -f 7
```

将 username 替换为你自己的。该命令应该打印出一个文件和路径。如果引用的程序 csh 或 tsh，则本节不适用于你，除非你更改了 shell。如果是 sh、ksh 或 bash，则适用。⁴。无法用 csh 或 tsh 重定向特定的文件句柄这一事实，使得许多 Unix 专家认为这些 shell 是“坏掉的”。我不对此发表立场，只是说明我没有涵盖这些 shell。即使你运行这些 shell 且不愿意切换，为了理论知识，这可能仍然值得阅读。

- 3. 假设你的系统没有使用 NIS 来跟踪账户。NIS 超出了本书的范围；你可以通过输入 `ycat password` 而不是 `cat /etc/passwd` 来获取 NIS 账户列表。
- 4. 这似乎是一个很好的观点，即 Unix shell 有两个名称：“真实名称”以及运行 shell 的命令名称。Bourne Shell 也称为 sh，Korn Bourne Shell 也称为 ksh，而 tsh 就叫 tsh。

第一部分 Unix 概念

文件句柄（file handle）是文件的抽象表示。也就是说，当计算机程序需要访问一个文件时，它并不是每次都使用所访问的文件名。相反，程序创建一个命名的文件句柄。本质上，程序员说：“每当我谈到 MY_OPEN_FILE 时，我实际上是在谈论 /some/long/path/to/a/particular/file。” 这对程序员来说有许多优点：首先，他们不需要在每次读取或写入时都重命名。其次，如果文件在程序完成写入之前更改了名称或目录，需要更改的内容就更少。更重要的是，如果文件在程序运行时更改了名称或目录，或者程序之前不知道文件名，它仍然可以处理它。

大多数编程语言使用名称作为文件句柄，而 Unix shell 使用数字。名称可能很方便，虽然冗长，但要确定命令行的哪部分是文件句柄、哪部分不是，要困难得多。数字让这部分变得简单。

所有的重定向实际上都是通过编号的文件句柄（也称为描述符）完成的；大多数重定向命令都隐含一个默认描述符。通用格式简单就是重定向命令左侧的文件描述符。STDIN 是 0，STDOUT 是 1，STDERR 是 2。当我们重定向命令 `command < outfile.txt` 时，我们实际上是在运行 `cat 0 outfile.txt`。同样，当我们运行 `ls > whatever` 时，我们实际上是在做 `ls 1 > whatever`。

如果我们之前的之前的 `find` 示例中想将 STDERR 重定向到一个文件，我们应该使用 `find / -name '*' -print 2 errors.txt`。这会将正常输出打印到控制台，同时将错误发送到 errors.txt。

这使得能够在将错误发送到 errors.txt 的同时获取控制台的正常输出。

## 练习题

- 1. 使用重定向创建一个名为 something.txt 的文件。里面 什么什么？
- 2. 使用管道显示 something.txt 的内容。
- 3. 使用管道将输出重定向到 something.txt。
- 4. 使用管道从 something.txt 重定向输入。
- 5. 使用管道将错误重定向到 something.txt。something.txt 的内容是什么？
- 6. 使用在此处文档创建一个名为 something.txt 的文件，内容如下：

# 重定向与管道 第 3 章

## 管道

管道是 Unix 的核心所在。我知道重定向和管道是 Unix 的核心，但有效使用管道定义了 Unix。虽然其他系统在重定向方面还尚可，但只有 Unix 在管道方面做得很好。

# 常用过滤器

现在你已经有了一个工具箱，让我们用一些基础工具填充它吧！这一部分将介绍 Unix 工具箱中的锤子、螺丝刀和扳手——那些你每天都会使用的工具。虽然还有钻床和圆锯，但在学习那些工具之前，你需要先学习基础知识。

# 分页器 (Pagers)

大多数用户尝试的第一个过滤器是将 `cat` 接入 `more`，这是一个简单的程序，它在每次滚动文本后停止并等待用户按键。如果你正在读取一个长文本文件，`more` 是你的朋友。只需试一下，输入 `cat /usr/dict/words | more`。（当你看腻了一长字母列表时，只需按 Ctrl+C 即可退出 `more`。）如果你的系统没有 `/usr/dict/words`，请尝试查看 `/etc/services` 或系统上的其他长文件。

在使用过 `more` 之后，尝试 `less`（如果你的系统上安装了的话）。如果你不确定安装了哪一个，只需尝试这些命令看看它们是否有效。如果没有安装 `less`，你会收到错误信息，且不会发生任何故障；你无法看到尝试查看的文件。`less` 允许你向后移动也可以向前移动；如果你的终端配置正确，PageUp 和 PageDown 键可以让你一次滚动一页文本。因为 `less` 在到达文件末尾不会退出，你需要按 `q` 退出。（与大多数程序不同，Ctrl+C 不会退出 `less`。）和 `more` 一样，只需 `cat /etc/syslog.conf | less` 来查看一个你不关心的长文件。

`more` 和 `less` 是过滤器的一类特殊子类，被称为分页器，因为它们允许用户翻页文本。然而，大多数过滤器都会以某种方式转换通过它们的文本。

# 头部与尾部 (Heads and Tails)

`head` 和 `tail` 通过只显示文件的部分来转换文本。`head` 显示文件的顶部部分，而 `tail` 显示文件的底部部分：

```
$ elvis@frog elvis $ cat tao.txt|head -2
```

老子
庄子

```
$ elvis@frog elvis $ cat tao.txt|head -4
```

> 你还记得我们在第一章讨论文档时提到的老朋友 `more` 和 `less` 管道。它们不仅是 `more` 和 `less` 管道，还可以直接接受文件名作为参数并显示该文件。许多 Unix 命令在某些方面都是灵活的。如果你不在命令行中给它提供文件名，`cat` 也可以用作过滤器。仔细想想，你实际上这样做这样做；当你把文件重定向到 `cat` 的时候。

老子
庄子
孔子
孟子

```
$ elvis@frogbog elvis $ cat tao.txt|tail -2
```

孟子
王弼

```
$ elvis@frogbog elvis $ cat tao.txt|tail -4
```

庄子
孔子
孟子
王弼

默认情况下，`head` 和 `tail` 各打印十行。在这些命令的某些版本中，你可以指定行以外的测量，但计数是最常见的。

# sort 和 uniq (排序与去重)

另一个非常流行的过滤器是 `sort`，它只需按字母顺序对传递它的文件进行排序。有了 `head` 和 `tail`，关于 `sort` 无好说的，我就运行几个简单的演示：

- `$ elvis@frogbog elvis $ cat tao.txt|sort`
```
庄子
孔子
老子
孟子
王弼
```
- `$ elvis@frogbog elvis $ cat west.txt|sort`
```
亚里士多德
笛卡尔
赫拉克利特
克尔凯郭
帕斯卡
柏拉图
普鲁图丁
萨特
苏格拉
```
- `$ elvis@frogbog elvis $ cat west.txt.west.txt|sort`
```
亚里士多德
庄子
笛卡尔
赫拉克利特
克尔凯郭
孔子
老子
# Unix 概念
- 孟子
帕斯卡
柏拉图
普鲁图丁
萨特
苏格拉
王弼
亚里士多德
庄子
笛卡尔
赫拉克利特
克尔凯郭
孔子
老子
孟子
帕斯卡
柏拉图
普鲁图丁
萨特
苏格拉
王弼
```
$ elvis@frogbob elvis $ cat west.txt tao.txt|sort

如你所见，`sort` 接收通过 STDIN 接收的所有输入，并将排序后的数据发送到 STDOUT。它有一个特殊的数值模式，可以通过 `-n` 选项访问。使用此开关，行开头的文本是一个数字，数字按数值排序。这似乎是多余的，但让我们来看个例子：

```
[ jon@frogbob jon $ cat some-stuff.txt
```

99 Dead Baboons

99 Red Balloons

101 Dalmatians

16 Candles

24 Hours

9 Lords a Leaping

```
$ [ jon@frogbob jon $ cat some-stuff.txt|sort -n
```

9 Lords a Leaping

16 Candles

24 Hours

99 Dead Baboons

99 Red Balloons

101 Dalmatians

但如果没有 `-n` 开关会发生什么？我们也试一下那个：

```
[ jon@frogbob jon $ cat some-stuff.txt|sort
```
101 Dalmatians
16 Candles
24 Hours

# 重定向与管道 第 3 章

99 Dead Baboons

99 Red Balloons

9 Lords a Leaping

当我们按数量排序时，这几乎不是我们预想的：不是按数值排序，这个列表是按字母顺序排序的。（记住，数字在字母之前。）另一个用途相当有限的相关工具是 `uniq`，它当重复行在文件中连续出现时剔除重复行。例如：

```
$ jon@frogbog jon $ cat other-stuff.txt
```

One

Two

One

Two

Three

One

```
$ jon@frogbog jon $ cat other-stuff.txt|uniq
```
One
Two
One
Two
Three
One
```

这在接 `sort` 之后非常有用：

```
$ jon@frogbog jon $ cat other-stuff.txt | sort | uniq
```

One

Three

Two

## wc

到目前为止，我最喜欢的过滤器是 `wc`，它只需报告文件中包含多少个字符、单词和行。

```
$ jon@frogbog jon $ cat some-stuff.txt | wc
```
16 85
```

```
$ jon@frogbog jon $ cat some-stuff.txt | wc -c
```
85

## 将过滤器组合成更长的管道

`wc` 特别适用于统计任何每记录一条存储的内容，例如 `ps` 命令的输出：

```
$ jon@frogbog jon $ cat some-stuff.txt | wc -w
```
16
```

```
$ jon@frogbog jon $ cat some-stuff.txt | wc -l
```
6

显然，精确数字取决于你的系统以及你运行命令时的用途。现在这个系统上运行着多少进程？单个过滤器本身可能是自己，但过滤器在相互组合以产生特定效果时最有用。

## grep

如果我想找到我的 shell，使用我之前提到的命令，我首先必须找到我的账户。为此，我们通过 `/etc/passwd` 管道到 `grep`，这是一个高级搜索程序。默认返回所有匹配命令行提供的正则表达式的行。

我们将在第 5 章讨论正则表达式，但目前我们只需要知道可以使用正则表达式查找文本，并且某些字符具有特殊含义。在之前的例子中，如果我想找到我的账户，管道的这部分读作 `grep "jon"`：

cut 默认以冒号分隔。我们想指定只显示第七个字段，因此我们加上 `-f 7`。

```
cat /etc/passwd | grep "jon" | cut -d : -f 7
```

`/etc/passwd` 中的第一个字段是用户名。第二个是密码，x 是该字段中显示的唯一内容。第三是该账户的 UID，第四是主 GID。第五个字段，它包含了人类可读的用户名。在某些系统中，这还可以包含电话号码、办公室等。第六个是用户的主目录，最后我们有用户的默认 shell。

在我的系统上，这样的行如下：

```
jon:x:500:/home/jon:/bin/bash

elvis:x:501:100:/home/elvis:/bin/bash
```
