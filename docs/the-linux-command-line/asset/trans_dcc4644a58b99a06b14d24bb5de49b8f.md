

大括号展开可以嵌套：

```
[me@linuxbox ~]$ echo a{A{1,2},B{3,4}}b
aA1b aA2b aB3b aB4b
```

那这有什么用呢？最常见的应用是创建文件或目录列表。例如，如果我们是摄影师，拥有大量想要按年份和月份整理的图片，我们首先可能会创建一系列以数字“年-月”格式命名的目录。这样，目录名就会按时间顺序排序。我们可以手动输入完整的目录列表，但这工作量很大而且容易出错。相反，我们可以这样做：

```
[me@linuxbox ~]$ mkdir Pics
[me@linuxbox ~]$ cd Pics
[me@linuxbox Pics]$ mkdir {2007..2009}-{0{1..9},10..12}
[me@linuxbox Pics]$ ls
2007-01  2007-07  2008-01  2008-07  2009-01  2009-07
2007-02  2007-08  2008-02  2008-08  2009-02  2009-08
2007-03  2007-09  2008-03  2008-09  2009-03  2009-09
2007-04  2007-10  2008-04  2008-10  2009-04  2009-10
2007-05  2007-11  2008-05  2008-11  2009-05  2009-11
2007-06  2007-12  2008-06  2008-12  2009-06  2009-12
```

挺 slick 的！

## 参数扩展

我们在本章中只会简要涉及参数扩展，但稍后会深入讲解。它在 shell 脚本中比直接在命令行上更有用。其许多功能都与系统能够存储小块数据并为每块数据命名有关。许多这样的块，更准确地称为变量，可供你查看。例如，名为“USER”的变量包含你的用户名。要调用参数扩展并显示 USER 的内容，你可以这样做：

```
[me@linuxbox ~]$ echo $USER
me
```

要查看可用变量的列表，可以尝试：

```
[me@linuxbox ~]$ printenv | less
```

你可能已经注意到，对于其他类型的扩展，如果你输入错误，扩展将不会发生，echo 命令只会简单地显示输入错误的模式。对于参数扩展，如果你拼错了变量名，扩展仍然会发生，但会得到一个空字符串：

```
[me@linuxbox ~]$ echo $SUER
[me@linuxbox ~]$
```

## 命令替换

命令替换允许我们将命令的输出用作扩展：

```
[me@linuxbox ~]$ echo $(ls)
Desktop Documents ls-output.txt Music Pictures Public Templates Videos
```

我最喜欢的一个大概是这样的：

```
[me@linuxbox ~]$ ls -l $(which cp)
-rwxr-xr-x 1 root root 71516 2007-12-05 08:58 /bin/cp
```

这里我们将 which cp 的结果作为参数传递给 ls 命令，从而在不知道其完整路径名的情况下获取 cp 程序的列表。我们并不局限于简单的命令。整个管道也可以使用（仅显示部分输出）：

```
[me@linuxbox ~]$ file $(ls /usr/bin/* | grep zip)
/usr/bin/bunzip2: symbolic link to `bzip2'
/usr/bin/bzip2: ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.9, stripped
/usr/bin/bzip2recover: ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.9, stripped
/usr/bin/funzip:      ELF 32-bit LSB executable, Intel 80386,
version 1 (SYSV), dynamically linked (uses shared libs), for
GNU/Linux 2.6.9, stripped
/usr/bin/gpg-zip:     Bourne shell script text executable
/usr/bin/gunzip:      symbolic link to '../.. /bin/gunzip'
/usr/bin/gzip:        symbolic link to '../.. /bin/gzip'
/usr/bin/mzip:        symbolic link to 'mtools'
```

在这个例子中，管道的结果成为了 file 命令的参数列表。

在旧的 shell 程序中，命令替换有一种替代语法，在 bash 中也支持。它使用反引号而不是美元符号和括号：

```
[me@linuxbox ~]$ ls -l `which cp`
-rwxr-xr-x 1 root root 71516 2007-12-05 08:58 /bin/cp
```

## 引号

现在我们已经看到了 shell 可以执行扩展的多种方式，是时候学习如何控制它了。例如：

```
[me@linuxbox ~]$ echo this is a    test
this is a test
```

或：

```
[me@linuxbox ~]$ echo The total is $100.00
The total is 00.00
```

在第一个例子中，shell 的词分割移除了 echo 命令参数列表中的多余空白。在第二个例子中，参数扩展将空字符串替换为“$1”的值，因为它是一个未定义的变量。shell 提供了一种称为引用的机制来有选择地抑制不需要的扩展。

### 双引号

我们要看的第一种引用是双引号。如果你将文本放在双引号内，shell 使用的所有特殊字符都会失去其特殊含义，并且是

