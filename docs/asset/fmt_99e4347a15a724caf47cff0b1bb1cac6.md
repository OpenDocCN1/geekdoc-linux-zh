
好多了！`fmt`命令有许多选项；然而，`-w`和`-s`选项是最重要的。`-w`选项告诉`fmt`行宽应为多少。如果不提供`-w`选项，`fmt`将恢复使用75个字符作为行宽。`-s`选项告诉`fmt`仅拆分行。如果你有一些较短的示例文本，默认行为是`fmt`先连接行，然后根据其内部规则拆分它们。

Previous Table of Contents Next

Products | Contact Us | About Us | Privacy | Ad Info | Home

Use of this site is subject to certain Terms & Conditions. Copyright © 1996-2000 EarthWeb Inc. All rights reserved. Reproduction whole or in part in any form or medium without express written permission of EarthWeb is prohibited.

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)

Author(s): Manuel Ricart

ISBN: 078971826x

Publication Date: 12/22/98

Search this book:

Previous Table of Contents Next

### 将文件拆分为较小文件：`split`

Check This Out:

Compression is discussed in Chapter 20, "Installing Programs and Applications," in the section "UNIX Compressed Archives: Gzip and Compress."

假设你想将一个文件复制到软盘上，但该文件即使压缩后也远大于单张磁盘的容量。你如何处理这个问题？一种方法是使用`split`命令。`split`命令的语法如下：

```
split [option] size file outfile name
```

选项有`-l`用于按行数拆分文本文件，以及`-b`用于按字节数拆分文件。选项之后指定大小。使用字节选项时，可以添加`b`表示字节、`k`表示千字节或`m`表示兆字节。`File`是你要拆分的文件名，`outfile name`是命令将用于命名所有块的基础名称。不同的文件名是通过在文件后附加扩展名生成的。

要将一个大文件拆分为1395K的块，以便每个块都能放入标准软盘：

```
[alberto@digital splitter]$ ls -l
 total 5801
 -rw-r--r-- 1 alberto alberto 5915554 Sep 20 11:51 book.zip
[alberto@digital splitter]$ split -b 1395k book.zip book.zip.
[alberto@digital splitter]$ ls -l
 total 11607
 -rw-r--r-- 1 alberto alberto 5915554 Sep 20 11:51 book.zip
 -rw-rw-r-- 1 alberto alberto 1428480 Sep 20 18:39 book.zip.aa
 -rw-rw-r-- 1 alberto alberto 1428480 Sep 20 18:39 book.zip.ab
 -rw-rw-r-- 1 alberto alberto 1428480 Sep 20 18:39 book.zip.ac
 -rw-rw-r-- 1 alberto alberto 1428480 Sep 20 18:39 book.zip.ad
 -rw-rw-r-- 1 alberto alberto 201634 Sep 20 18:39 book.zip.ae
```

没有`join`命令，因此要将文件连接成一个大文件，使用你已知的命令`cat`：

```
cat book.zip.?? > book.zip
```

文件将被串联（复制）到一个大文件中。表达式`??`匹配任意两个字符（上例中为`aa`到`ae`）。这之所以有效，是因为`shell`按字母顺序排列文件，因此`ab`有保证跟在`aa`之后。

### 通过网络访问计算机：`telnet`

`telnet`命令允许你使用`shell`登录到远程计算机。就实际用途而言，你正在远程计算机的控制台上工作，并且可以像物理上坐在该计算机键盘前一样使用任何命令。`telnet`命令非常易于使用：只需输入`telnet`后跟你想要工作的系统的主机名。这将为你提供一个登录提示，与过去几节中使用的提示大致相同。

`telnet`会话的一个问题是，有时你的键盘不会按预期工作。要修复此问题，请参阅第13章“在Shell下进行文本编辑”中关于`stty`命令的边栏讨论。

要退出`telnet`会话，输入`exit`或在提示符下按`Ctrl+D`。

### 在控制台上工作：`setfont`

如果你使用文本界面在EGA/VGA控制台上工作，你可能会想知道为什么你只能看到24行文本。好吧，有办法修复这个问题：`setfont`命令。

`setfont`命令更改控制台使用的字体大小。更改字体大小也会更改最大行宽和你可以看到的行数；因此，你选择的字体将决定你的可见工作空间。

许多字体安装在`/usr/lib/kbd/consolefonts`目录中。字体文件使用类型命名；通常，你希望选择名称以`default`开头的一个（因为字符类型会根据字体而变化）以及一个大小。标准VGA字体大小为16（高16像素），因此使用更小的字体会带来巨大差异。字体类型/大小组合也会极大地影响可读性，相同大小的不同字体在屏幕上看起来会非常不同。一些字体文件包含三种大小：8、14和16。要指定正确的大小，只需提供一个连字符(`-`)后跟大小（`setfont`在需要时会提示你）。如果你的屏幕出现混乱，只需再次输入`setfont`即可返回默认设置。

要更改字体，指定字体文件名（你不需要给出完整路径）：

```
setfont fontname
```

其中一个更受欢迎的字体，可以大大增加你的显示大小，使用以下方式选择：

```
Setfont /usr/lib/kbd/consolefonts/alt-8x8
```

尝试不同类型和大小，直到找到最适合你的可读性。

## 完全傻瓜的 Linux 使用指南

（出版社：Macmillan Computer Publishing）

作者：Manuel Ricart

ISBN：078971826x

出版日期：12/22/98

搜索本书：

### UNIX 打印入门

在这本书中，我有点忽略了告诉你如何打印文件，部分原因是如果你使用的是StarOffice、WordPerfect或Applix等文字处理器，这些程序已经知道如何打印而无需经过这些麻烦（StarOffice包含在这本书附带的CD上。）

如果你想从命令行进行UNIX文本处理（与在GUI中进行文字处理相对），有几件事你需要知道，这会影响你打印的文档的最终呈现。Linux和UNIX下的打印与Windows或Macintosh下的打印截然不同。从命令行打印涉及三个步骤：

- 1. 使用文本编辑器创建文档，并在需要时添加格式命令。这些格式命令或宏将取决于你使用的格式化程序。然而，文本标记（UNIX人喜欢称之为文本处理）的概念是相同的。
- 2. 将你的文档通过一个或多个过滤器运行（某些过滤器可能像我之前提到的`fmt`命令一样基础）；最终的过滤器通常会生成一个包含所有必要打印机控制代码以呈现文档的文件。有时，过滤器可以直接将此输出发送到打印机。
- 3. 使用名为`lpr`的程序将过滤后的文件发送到打印机。

如果你只需要打印一个纯文本文件，你必须做几件事。你使用的程序将取决于你拥有的打印机类型。通常，打印机分为两类：具有PostScript的和不具有PostScript的。

如果你的打印机具有PostScript支持，你可能会使用一个名为`enscript`的程序。如果没有，你将使用一个名为`pr`的程序。在表面上，这些程序是等效的——只是`enscript`利用了PostScript可用的功能，因此功能更多。这些程序在基本层面上允许你指定页边距、页眉和文本行的长度。

不花哨，但它们提供了生成一个相当朴素外观文档所需的基本格式化功能。

这里有一个例子。如果你想打印一个名为`intro.txt`的文本文件，你会将其发送给`pr`：

```
pr intro.txt
```

将同一文件发送到PostScript打印机将是这样做的：

```
enscript intro.txt
```
