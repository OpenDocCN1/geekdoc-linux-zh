
```
# apropos solaris | wc -l
54
```

太好了！

8. 现在在我们的任何系统上，我们都可以运行 apropos 命令并查找与主题 help 相关的命令：

```
$ apropos help
B::StackObj          (3pm)  - Helper module for CC backend
consolehelper        (8)   - A wrapper that helps console users run
system programs
forum                (1)   - Interactive Help for MRTG users
help [builtins]      (1)   - bash built-in commands, see bash(1)
help [faq]           (1)   - How to get help if you have problems with MRTG
LDP                  (7)   - Intro to the Linux Documentation Project, with
help, guides and documents
mibhelp              (1)   - A Table of some interesting OIDs
Pod::ParseUtils      (3pm) - helpers for POD parsing and conversion
QCharRef [qcharref]  (3qt) - Helper class for
QToolTip [qtooltip]  (3qt) - Tool tips (sometimes called balloon help)
for any widget or rectangular part of a widget
QXmlNamespaceSupport [qxmlnamespacesupport] (3qt)  - Helper class for XML
readers which want to include namespace support
smbmnt               (8)   - helper utility for mounting SMB filesystems
userhelper           (8)   - A helper interface to pam
```

这来自 Linux，你可以看到这里有许多命令。请注意，它们都在命令或描述文本中包含字母 h-e-l-p，但它们并不都必然与用户级帮助命令相关。

![](img/5ced0c78d748bd190e9027e5549a3622_47_0.png)

> 作为提醒，Unix 手册页分为八大类：1=user commands，2=system maintenance commands，3=system calls (for programmers)，4=administration files，5=miscellaneous，6=games，7=special file formats，8=administrative commands。

经常你只想查看交互式命令而不是系统维护命令，等等。一种简单的方法是使用 egrep：

```
$ apropos help | egrep '(1)'
consolehelper        (8)   - A wrapper that helps console users run
system programs
forum                (1)   - Interactive Help for MRTG users
help [builtins]      (1)   - bash built-in commands, see bash(1)
help [faq]           (1)   - How to get help if you have problems with MRTG
mibhelp              (1)   - A Table of some interesting OIDs
smbmnt               (8)   - helper utility for mounting SMB filesystems
userhelper           (8)   - A helper interface to pam
```

![](img/5ced0c78d748bd190e9027e5549a3622_47_1.png)

进一步的细微差别可能是将此输入到 sort 中，以便按顺序显示所有第 1 部分命令，然后是第 8 部分命令，但我把这个作为练习留给你！

原本只是学习如何使用 apropos 命令的简单任务迅速失控，并在我们发现并修复一些系统配置问题时漫无目的地四处游荡。这作为系统管理员的日常体验非常典型，随着你花更多时间从管理员角度学习 Unix，你会发现这一点。

## 探索 whatis 数据库

现在我们知道了如何构建 whatis 数据库，让我们花几分钟时间深入其中，看看能学到什么。只是短暂的额外岔路，我保证！

## 任务 2.2：whatis 数据库内部有什么

作为好奇的人，我们不能不做一点探索就放下数据库，所以让我们瞄一眼。

- 1. 数据库本身是一个普通文本文件，因此我们可以使用 head 来查看其内部内容：
```
# cd /var/cache/man
# file whatis
whatis: ASCII English text
# head whatis
m4topp (1) . convert Sony Mavica .411 image to PPM
a2p (1) . Awk to Perl translator
a2ps (1) . format files for printing on a PostScript
printer
ab (8) . Apache HTTP server benchmarking tool
abbrev [Text::Abbrev] (3pm) . create an abbreviation table from a list
abort (3) . cause abnormal program termination
ABORT [abort] (1) . Aborts the current transaction
abs (3) . compute the absolute value of an integer
accept (2) . accept a connection on a socket
access (2) . check user's permissions for a file
```

有趣吧？这让我得出结论，apropos 是 grep -i 的同义词，果然，grep -i help whatis 产生的结果与我们之前看到的完全相同。试试看！

- 2. 更有趣的是，我们现在可以提取数据库的不同部分，并查看每个部分有多少命令。

为此，我想在开始的括号处分割行，然后再次在结束的括号处分割，只保留其中的值。这可以通过

两次调用 cut 来完成，第一次指定打开括号作为分隔符，第二次指定关闭括号。第一次调用的效果如下：

```
# cut -d\( -f2 < whatis | head -5
1) - convert Sony Mavica .411 image to PPM
1) - Awk to Perl translator
1) - format files for printing on a PostScript printer
8) - Apache HTTP server benchmarking tool
3pm) - create an abbreviation table from a list
```

而第二个，添加到管道中间：

```
# cut -d\( -f2 < whatis | cut -d\) -f1 | head -5
1
1
1
8
3pm
```

现在，最后，只需调用 sort 对它们全部排序，并使用 -c 标志调用 uniq 以获得最终的输出计数：

```
# cut -d\( -f2 < whatis | cut -d\) -f1 | sort | uniq -c
14
1405 1
6 1m
39 1ss1
254 2
8272 3
400 3pm
335 3qt
657 3ss1
77 3t
61 3thr
3603 3x
36 4
146 5
1 5s1
3 6
67 7
1 7ss1
380 8
67 1
446 n
1 Paranoia release III
1 xnmap
```

这就是答案。忽略那些奇特的条目（例如 Paranoia release III），你可以看到在 Linux 系统上，第 1 部分有 1,405 个命令，第 8 部分有 380 个命令，系统程序员使用的不同命令和函数超过 13,000 个。难怪编程 Unix 系统并不容易！

![](img/5ced0c78d748bd190e9027e5549a3622_49_0.png)

![](img/5ced0c78d748bd190e9027e5549a3622_50_0.png)

> 有趣的是，在 Solaris 中只有 1,324 个第 1 部分命令，总共 6,689 个命令，而在 Darwin 上的 whatis.db 文件中记录的第 1 部分命令仅有 478 个，总共 2,068 个命令，数量更少。

本节不仅很好地展示了如何组合 Unix 命令以产生有用的结果，也展示了你如何很容易分心。即使作者有时也很难避免到处探查并了解更多关于系统的信息！

## 查找命令

apropos 命令提供了一种非常有用的方法，可以根据单行命令摘要浏览 man 命令，但探索 Unix 系统上可用命令还有其他方法。最值得注意的是 which，它会搜索你的路径并告诉你给定命令名称要执行的文件是什么，而 locate 则是快速尝试将模式与系统上所有文件名列表进行匹配的一种方法。

然而，后者实际上是功能强大的通用 find 命令的特殊用途变体，我们将在本书后面更详细地介绍它。

## 任务 2.3：你正在运行哪个命令？

在 Unix 中调试任何问题的第一步是确保你的 PATH 正确，然后确保你认为正在运行的命令版本就是被调用的版本。

所有命令 shell 都会构建所谓的命令哈希表，这是一个快速搜索的列表，其中包含位于 PATH 环境变量指定的每个目录中的文件名。如果出现冲突（例如，两个目录具有相同的文件名），则 PATH 中更早引用的目录获胜。

![](img/5ced0c78d748bd190e9027e5549a3622_50_1.png)

> 早期 PATH 匹配覆盖后期 PATH 条目的特性正是 PATH 设置为 PATH=.:other stuff 之类的方式如此危险的原因：如果你在某个目录中存在 ls 的伪造版本，你可能会在不知情的情况下执行它。为什么这很危险？因为伪造的 ls 可能做一些狡猾的事情，比如制作 shell 的秘密副本，然后 chmod 它使其对你的账户具有 setuid 权限。黑客在稍后某个时间出现，每当她想冒充你时，她只需运行该 shell 即可。这就是所谓的特洛伊木马攻击。
