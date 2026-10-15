
随着你添加了更多版本，拥有一个描述每个版本的列表可能会有所帮助。`log`命令将打印RCS文件中所有版本的摘要，让你大致了解每个版本的内容。每个摘要都有一个包含头，包含日期和时间；创建它的用户；版本的序列号；以及插入、删除或未更改的行数。随后会打印该版本的注释。这些信息将让你清晰地了解程序从一个版本到下一个版本是如何进展和变化的。

```
$ rlog main.c
RCS file: RCS/main.c,v
Working file: main.c
head: 1.2
branch:
locks: strict
access list:
symbolic names:
keyword substitution: kv
total revisions: 2; selected revisions: 2
description:
Calculation program

revision 1.2
date: 1999/11/07 22:52:41; author: root; state:
Exp; lines: -0
Added prompt

revision 1.1
date: 1999/11/07 22:50:20; author: root; state:
Exp:
Initial revision
```

| 选项 | 说明 |
| - | - |
| `-rversion` | 输出关于特定版本的信息。 |
| `-ddate` | 输出在特定日期创建的版本的信息。（日期格式为`yy/mm/dd`和`hh:mm:ss`。除年份外，所有部分均为可选。） |

## 版本控制系统：RCS 237

| 选项 | 说明 |
| - | - |
| `-d<date>` | 输出早于指定日期的信息。 |
| `-t<date>` | 输出晚于指定日期的信息。 |

## 检索和删除特定的 RCS 版本

你可以使用`ci`命令的`-r`选项来为新版本指定自己的编号。你输入附加在`-r`选项后的版本号。在下一个示例中，用户使用`-r`选项指定了一个新的版本号。

```
$ ci -r3 main.c
RCS/main.c,v <-- main.c
new revision: 3.1; previous revision: 1.2
enter log message, terminated with single '.
or end of file:
>> A new version Number
>> .
done
```

你使用`co`命令配合`-l`选项来检索文件的特定版本。然而，使用`ci`提交该编辑后的版本会创建一个分支版本。你所做的更改将保存在你所检索的版本的分支中。原始版本保持不变。在下一个示例中，`-r`选项检索了版本`1.1`，然后`ci`创建了一个新分支版本`1.1.1`。

```
$ co -l -r1.1 main.c
RCS/main.c,v --> main.c
revision 1.1 (locked)
done
```

```
$ ci main.c
RCS/main.c,v <-- main.c
new revision: 1.1.1.1; previous revision: 1.1
enter log message, terminated with single '.
or end of file:
>> A new branch
>> .
done
```

## 238 版本控制系统：RCS

然后你可以使用`log`查看给定文件的所有版本和分支列表。

```
$ rlog main.c
RCS file: RCS/main.c,v
Working file: main.c
head: 3.1
branch:
locks: strict
access list:
symbolic names:
keyword substitution: kv
total revisions: 4 selected revisions:
description:
Calculation program
-----------------
revision 3.1
date: 1999/11/07 23:15:23; author: root;
state: Exp; lines: +1 -1
A new version Number
-------------------
revision 1.2
date: 1999/11/07 22:52:41; author: root;
state: Exp; lines: +1 -0
added prompt
-----------------
revision 1.1
date: 1999/11/07 22:50:20; author: root;
state: Exp;
branches: 1.1.1;
Initial revision
-------------------
revision 1.1.1.1
date: 1999/11/07 23:01:57; author: root;
state: Exp; lines: +1 -1
A new branch
====================================
```

你可以使用`rcs`命令配合`-o`选项从RCS文件中删除一个版本。在下一个示例中，删除了版本`3.1`。

```
$ rcs -o3.1 main.c
```

## 版本控制系统：RCS 239

## RCS 文件的 make 后缀规则

在本章之前描述的`make`工具具有若干个管理RCS文件的标准后缀规则。`make`假设一个RCS文件对应一个源代码文件并包含该源代码，例如`.c`。

# 应用程序在线手册：man

## 应用程序在线手册：man

当你为Linux开发一个程序时，你可能需要对其进行文档记录。如果这是一个由几个程序员同时开发的大型应用程序，那么文档可能变得至关重要。文档通常以描述程序不同命令和功能的手册的形式存在。很多时候，应用程序会被拆分成独立的程序。对于用户和程序开发者来说，能够检索并显示应用程序手册的相应章节是非常有帮助。这种在线手册让所有用户和开发者都能立即访问文档。`man`命令提供了访问Linux命令在线手册的接口，你也可以使用`man`命令管理你自己的在线应用程序。你可以使用特殊的`man`文本处理宏来创建`man`文档。然后，你可以指示`man`命令读取这些文档。

今天`groff`最常用的用途之一就是创建在线手册文档。你在Linux系统上找到的在线手册实际上是一个`groff`文档。你使用一组被称为`man`的宏来创建你自己的在线手册条目。如果你创建了一个新命令并想对其进行文档记录，可以为它创建一个手册文档，并使用`man`命令读取该文档。

当你使用文档名调用`man`命令时，`man`命令会使用`groff`来格式化文档并显示它。你创建的实际文档是一个带有相应`man`宏的未格式化文本文件。`man`宏与`ms`宏非常相似。你实际上可以使用带有`-man`选项的`groff`命令直接格式化并显示文档。在下一个示例中，两个命令都显示`ls`命令的手册。

```
$ ls
$ groff -man /usr/man/man1/ls | more
```

## man 文档文件

你可以使用任何标准文本编辑器创建一个`man`文档文件。你给文本文件命名的就是所涉及的命令或主题名称，并带有章节号作为扩展名。关于`who`命令的文档将名为`who.1`。在此描述的示例中，该文档是关于`bookrec`命令的，章节号为`1`。它的名字是`bookrec.1`。章节号将在下一节“man目录”中讨论。

一个`man`文档由多个章节组成，顶部有一个运行标题。章节可以命名为你喜欢的任何名称。按照惯例，Linux命令的`man`文档组织为几个预定义的章节，例如`NAME`（名称）、`SYNOPSIS`（概要）和`DESCRIPTION`（描述）。不过，你可以自由创建任意数量的章节，并赋予你喜欢的名称。你创建的实际文档是一个带有相应`man`宏的未格式化文本文件。手册文档至少需要两个不同的宏：`.TH`和`.SH`提供一个运行标题，它将显示在文档每页的顶部以及文档的章节号。你为每个章节标题使用`SH`命令。你可以根据需要添加其他宏，例如用于段落格式化的`.PP`宏，或用于缩进段落的`.IP`宏。

你在文档的行开头输入`man`宏，前面有一个点。你在宏之后的几几行中输入的任何文本都将由该宏进行格式化。某些宏（如`.SH`和`.TH`）会接收参数，直到遇到另一个宏。你在与`.SH`宏相同的同一行中在宏之后输入参数。与`.SH`宏相同的同一行是章节名称的正文。然后是章节的正文。章节正文通过一系列短行输入。这些行以后会被`man`格式化为对齐的段落。在下一个示例中，用户输入了一个`.SH`宏，随其后的是章节名`DESCRIPTION`。在接下来的行中，用户输入了章节的文本。

```
.SH DESCRIPTION

mylistopst 提供了显示购物列表的替代方法。
```
