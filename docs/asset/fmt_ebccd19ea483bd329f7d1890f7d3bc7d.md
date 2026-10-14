
```
[me@linuxbox ~]$ echo {01..15}
01 02 03 04 05 06 07 08 09 10 11 12 13 14 15
[me@linuxbox ~]$ echo {001..15}
001 002 003 004 005 006 007 008 009 010 011 012 013 014 015
```

以下是字母范围的反向顺序：

```
[me@linuxbox ~]$ echo {Z..A}
Z Y X W V U T S R Q P O N M L K J I H G F E D C B A
```

大括号展开可以嵌套。

```
[me@linuxbox ~]$ echo a{A{1,2},B{3,4}}b
aA1b aA2b aB3b aB4b
```

那么，这有什么用呢？最常见的应用是创建要创建的文件或目录列表。例如，如果我们是摄影师，拥有大量想要按年份和月份组织的图像，我们首先要做的事情可能是创建一系列以数字“年-月”格式命名的目录。这样，目录名就会按时间顺序排序。我们可以输入完整的目录列表，但这工作量很大，而且容易出错。相反，我们可以这样做：

```
[me@linuxbox ~]$ mkdir Photos
[me@linuxbox ~]$ cd Photos
[me@linuxbox Photos]$ mkdir {2007..2009}-{01..12}
[me@linuxbox Photos]$ ls
2007-01  2007-07  2008-01  2008-07  2009-01  2009-07
2007-02  2007-08  2008-02  2008-08  2009-02  2009-08
2007-03  2007-09  2008-03  2008-09  2009-03  2009-09
2007-04  2007-10  2008-04  2008-10  2009-04  2009-10
2007-05  2007-11  2008-05  2008-11  2009-05  2009-11
2007-06  2007-12  2008-06  2008-12  2009-06  2009-12
```

相当 slick！

### 参数展开

我们将在本章中仅简要介绍参数展开，但稍后会对其进行广泛介绍。它在 `shell` 脚本中比直接在命令行上更有用。其许多功能与系统存储小块数据并为每个块命名 的能力有关。许多这样的块，更正确地称为变量，可供你检查。例如，名为 `USER` 的变量包含你的用户名。要调用参数展开并显示 `USER` 的内容，你可以这样做：

```
[me@linuxbox ~]$ echo $USER
me
```

要查看可用变量的列表，请尝试以下操作：

```
[me@linuxbox ~]$ printenv | less
```

你可能已经注意到，对于其他类型的展开，如果你输入错误的模式，展开将不会发生，并且 `echo` `command` 将只显示拼写错误的模式。使用参数扩展，如果你拼写错误变量名，扩展仍然会进行，但结果会是一个空字符串。

```
[me@linuxbox ~]$ echo $SUER
[me@linuxbox ~]$
```

### 命令替换

命令替换允许我们将命令的输出用作扩展。

```
[me@linuxbox ~]$ echo $(ls)
Desktop Documents ls-output.txt Music Pictures Public Templates Videos
```

我最喜欢的一种用法是这样的：

```
[me@linuxbox ~]$ ls -l $(which cp)
-rwxr-xr-x 1 root root 71516 2007-12-05 08:58 /bin/cp
```

这里我们将 `which cp` 的结果作为参数传递给 `ls` 命令，从而在不知道其完整路径名的情况下获取 `cp` 程序的列表。我们并不局限于简单的命令。整个管道也可以使用（此处仅显示部分输出）。

```
[me@linuxbox ~]$ file $(ls -d /usr/bin/* | grep zip)
/usr/bin/bunzip2:     symbolic link to `bzip2'
/usr/bin/bzip2:      ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.9, stripped
/usr/bin/bzip2recover: ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.9, stripped
/usr/bin/funzip:      ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.9, stripped
/usr/bin/gpg-zip:     Bourne shell script text executable
/usr/bin/gunzip:      symbolic link to `../../bin/gunzip'
/usr/bin/gzip:        symbolic link to `../../bin/gzip'
/usr/bin/mzip:        symbolic link to `mtools'
```

在这个例子中，管道的结果成为了 `file` 命令的参数列表。

在旧的 `shell` 程序中，命令替换还有一种备用的语法，在 `bash` 中也支持。它使用反引号代替美元符号和括号。

```
[me@linuxbox ~]$ ls -l `which cp`
-rwxr-xr-x 1 root root 71516 2007-12-05 08:58 /bin/cp
```

### 引号

现在我们已经看到了 `shell` 可以执行扩展的多种方式，是时候学习如何控制它了。例如：

```
[me@linuxbox ~]$ echo this is a    test
this is a test
```

或者这个：

```
[me@linuxbox ~]$ echo The total is $100.00
The total is 00.00
```

在第一个例子中，`shell` 的词分割移除了 `echo` 命令参数列表中的多余空白。在第二个例子中，参数扩展将 `$1` 的值替换为空字符串，因为它是一个未定义的变量。`shell` 提供了一种称为引用的机制来有选择地抑制不需要的扩展。

#### 双引号

我们要看的第一种引用是双引号。如果我们将文本放在双引号内，`shell` 使用的所有特殊字符都会失去其特殊含义并被视为普通字符。例外是 `$`（美元符号）、`\`（反斜杠）和 `` ` ``（反引号）。这意味着词分割、路径名扩展、波浪号扩展和大括号扩展会被抑制；然而，参数扩展、算术扩展和命令替换仍然会执行。使用双引号，我们可以处理包含嵌入空格的文件名。假设我们不幸遇到了一个名为 `two words.txt` 的文件。如果我们在命令行上尝试使用它，词分割会将其视为两个独立的参数而不是期望的单个参数。

```
[me@linuxbox ~]$ ls -l two words.txt
ls: cannot access two: No such file or directory
ls: cannot access words.txt: No such file or directory
```

通过使用双引号，我们停止了词分割并得到了期望的结果；此外，我们甚至可以修复损坏。

```
[me@linuxbox ~]$ ls -l "two words.txt"
-rw-rw-r-- 1 me me 18 2018-02-20 13:03 two words.txt
[me@linuxbox ~]$ mv "two words.txt" two_words.txt
```

好了！现在我们不必再一直输入那些讨厌的双引号了。

记住，参数扩展、算术扩展和命令替换在双引号内仍然会进行。

```
[me@linuxbox ~]$ echo "$USER $((2+2)) $(cal)"
me 4 February 2020
Su Mo Tu We Th Fr Sa
          1
2  3  4  5  6  7  8
9 10 11 12 13 14 15
16 17 18 19 20 21 22
23 24 25 26 27 28 29
```

我们应该花点时间来看一下双引号对命令替换的影响。首先让我们更深入地了解一下词分割的工作原理。在我们之前的例子中，我们看到了词分割如何似乎移除了我们文本中的多余空格。
