
[magagne@testsys tmp]$] `ls -l`

total 0

--r--r--r-- 1 mgagne mgagne  0 Nov 5 12:58

```
## setuid 位

除了那三个权限位（读、写、执行）之外，还有另一个非常重要的位：`s` 位，根据它的位置，有时被称为 `setuid`。

这个特殊位背后的原理如下：有时你希望一个程序在运行时就像你是以另一个用户的身份登录一样。例如，你可能希望某个程序以 `root` 用户身份运行。这将是一个你希望非管理员用户运行的程序，但（出于某种原因），该程序需要读取或写入仅属于 `root` 的文件。`sendmail` 程序就是一个完美的例子。该程序需要访问特权函数来完成工作，但你又希望普通（非 `root`）用户也能发送邮件。

`setuid` 位是执行位的变体。为了让假设的程序 `ftl_travel` 可以被任何人执行但具有 `root` 权限，你按照如下方式更改其权限：

```
chmod u+s ftl_travel
```

下一步，正如你可能猜到的那样，是结合完整权限和 `setuid` 位。首先考虑，将 `setuid` 位和 `setgid` 位视为另一组三元权限。就像你可以将 `r`、`w` 和 `x` 引用为 4、2 和 1 一样，你可以将 `setuid` 引用为 4，`setgid` 引用为 2，而其他的你不需要担心。

所以，用一个复杂的例子，让我们让该命令对所有者具有读、写和执行权限，对组具有读和执行权限，对其他任何人没有权限。但是，对于那些具有执行权限的人，你希望将其设置为 `setuid`。你也可以用符号或数字方式来表示。

```
chmod u=rwxs,g=rx,o= ftl_travel
chmod 4755 ftl_travel
```

前面的数字 4 代表 `setuid` 位。如果你想让程序设置为 `setgid`，可以将其更改为 2。是的，如果你想让可执行文件同时保持所有者的权限和组的权限，你只需要将 4 和 2 相加得到 6。结果的权限集如下：

```
chmod 6750 ftl_travel
```

更改 `setuid` 位（或 `setgid` 位）并不严格为非 `root` 用户提供管理访问权限。这可以是任何情况。你可能有一个仅在一个用户 ID 下运行的数据库包，或者你可能希望所有用户都像是特定组的一部分一样访问某个程序。你必须决定。

> 注意：你不能对 脚本使用 `setuid` 或 `setgid` 位（尽管有 `perl` 钩子可以做到）。出于安全原因，这是不起作用的。如果你需要以自身以外的权限集执行，你必须编写一个短小的 C 程序来封装你的脚本，然后允许程序而不是脚本拥有 `setuid`（或 `setgid`）权限。

这里的教训是，将某些设置为 `setuid` 会立即引发安全问题。明确你为什么要采取这种方法并考虑风险。

## 文件属性

（注：原文此部分包含大量 OCR 错误和重复，此处已根据逻辑提取并清理了内容。）

# 第 10 章 与 Shell 合而为一

从根目录开始，通过以下命令递归地列出磁盘上的系统上的每一个文件：

```
find / -print
```

虽然这可能很有趣，而且你可能想将其重定向到文件中以备后参考，但它的用处有限。搜索某些内容可能更有意义。例如，查找你磁盘上所有的 JPEG 类型的图像文件。因为你知道图像以 `.jpg` 扩展名结尾，你可以利用这一点进行搜索。

```
find / -name "*.jpg"
```

取决于你系统的性能，这可能需要一些时间，而且你很可能会收到很多“拒绝访问”（Permission Denied）的提示（特别是当你遍历一个名为 `/proc/` 的目录时）。如果你是以 `root` 用户以外的用户运行此命令，你可能会收到大量的“拒绝访问”信息。此时，`find` 的用处应该开始显现出来，因为散落在磁盘各个部分的大量图像从磁盘空间来看确实是不积成多。你可以尝试使用 `.avi` 或 `.mpg` 扩展名来查找视频片段，这些文件通常非常大。

如果你想做的是定位旧文件，特别是那些在过去 12 个月内未被修改（使用 `-mtime` 参数）或未访问（使用 `-atime` 参数）的文件。`-o` 标志是这个公式中的“或”。

```bash
# find /data/Marcel -size +1024 \
(-mtime +365 -o -atime +365 \) -ls
```

这里介绍的技巧值得注意。括号前面的反斜杠是转义字符，它们的作用是确保 `shell` 不以你不想要的方式来解释它们——例如第二行中的左右括号。第一行末尾也有一个反斜杠。这是为了表示换行，因为整个命令无法整齐地放在本页的一行内。如果你完全按照所示输入而不带任何反斜杠，它将无法工作；然而，第二行中的反斜杠是至关重要的。前面的命令还搜索了大于 500KB 的文件。这就是 `-size +1024` 的含义，因为 1024 指的是 512 字节块。命令末尾的 `-ls` 告诉系统对任何符合我搜索标准的文件进行详细列出。

## 转向 Linux 办公桌面

在本章的早期，你已经学习了 `setuid` 和 `setgid` 文件。留意这些文件所在的位置并确定它们对于维护你系统安全的重要性非常重要。这里有一个命令可以检查你文件的权限（使用 `-perm` 选项）并报告它所发现的内容。

```bash
find / -type f -perm -4000 -o -perm -2000 -ls
```

你可能想将此输出重定向到一个文件中，稍后你可以查阅并决定采取什么行动。现在，看另一个示例，帮助你发现你正在查看的是什么类型的文件。你的 Linux 系统还有另一个名为 `file` 的命令，它可以提供关于文件及其种类的有用信息，无论它们是可执行文件、文本文件还是电影片段。以下是 `file` 命令报告的我家目录下一些文件的示例。

```bash
$ file $HOME/*
code.layout: ASCII text
cron.txt: data
dainbox: International language text
dainbox.gz: gzip compressed data, deflated,
filename, last modified: Sat Oct 7 13:21:14 2000, os: Unix
definition.htm: HTML document text
gatekeeper.1: troff or preprocessor input text
gatekeeper.man: English text
gatekeeper.pl: perl commands text
hilarious.mpg: MPEG video stream data
```

下一步是修改 `find` 命令并添加 `-exec` 子句，这样我就可以获取 `find` 找到的内容的 `file` 命令输出。

```bash
# find /data/Marcel -size +1024 \
-mtime 365 -o -atime 365 -ls -exec file {} \;
```

`-exec file` 之后的大大括号意味着生成的文件列表应该传递给 `-exec` 选项之后的任何命令（换句话说，是你将执行的命令）。末尾的反斜杠加分号是命令有效所必需。如你所见，`find` 非常强大。学会利用这种力量可以让你的管理工作变得简单得多。你将在书中书中多次遇到 `find`。

## 使用 grep

`grep` 是什么意思？全局正则表达式解析器（Global regular expression parser）——但这个缩写定义只是许多定义之一。如果你听到有人称它为“大吞练习程序”，也不要感到惊讶。基本上，`grep` 的目的是让你轻松地在文本文件中找到字符串。这是它的基本格式：

```
grep pattern file(s)
```

例如，假设你想找出你的 `/etc/passwd` 文件中是否有一个名为 `natika` 的用户。问题是该文件有 500 行。

```bash
[root@testsys /root]# grep natika /etc/passwd
natika:x:504:504:Natika the Cat:/home/natika:/bin/bash
```

有时你只是想知道文件中是否存在某段文本，但你不知道是哪个文件。在 `grep` 中使用 `-l` 选项可以让你只列出文件名，而不是行（`grep` 的默认行为）。

```bash
[root@testsys /root]# grep -l natika /etc/passwd
/etc/passwd
```
