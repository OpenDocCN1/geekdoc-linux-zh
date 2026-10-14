
`aspell` will see the contents of the HTML tags as misspelled. This problem can be overcome by including the `-H` (HTML) checking-mode option, like this:

```
[me@linuxbox ~]$ aspell -H check foo.txt
```

which will result in this:

```
<html>
    <head>
        <title>Misspelled HTML file</title>
    </head>
    <body>
        <p>The quick brown fox jimped over the lazy dog.</p>
    </body>
</html>

1) Mi spelled      6) Misapplied
2) Mi-spelled      7) Miscalled
3) Misspelled      8) Respelled
4) Dispelled       9) Misspell
5) Spelled         0) Misled
i) Ignore          I) Ignore all
r) Replace         R) Replace all
a) Add             l) Add Lower
b) Abort           x) Exit
? 
```

The HTML is ignored and only the non-markup portions of the file are checked. In this mode, the contents of HTML tags are ignored and not checked for spelling. However, the contents of ALT tags, which benefit from checking, are checked in this mode.

> Note: By default, `aspell` will ignore URLs and email addresses in text. This behavior can be overridden with command line options. It is also possible to specify which markup tags are checked and skipped. See the `aspell` man page for details.

## Summing Up

In this chapter, we have looked at a few of the many command line tools that operate on text. In the next chapter, we will look at several more. Admittedly, it may not seem immediately obvious how or why you might use some of these tools on a day-to-day basis, though we have tried to show some semi-practical examples of their use. We will find in later chapters that these tools form the basis of a tool set that is used to solve a host of practical problems. This will be particularly true when we get into shell scripting, where these tools will really show their worth.

## Further Reading

The GNU Project website contains many online guides to the tools discussed in this chapter.

- From the Coreutils package:

  - http://www.gnu.org/software/coreutils/manual/coreutils.html#Output-of-entire-files

  - http://www.gnu.org/software/coreutils/manual/coreutils.html#Operating-on-sorted-files

  - http://www.gnu.org/software/coreutils/manual/coreutils.html#Operating-on-fields

  - http://www.gnu.org/software/coreutils/manual/coreutils.html#Operating-on-characters

- From the Diffutils package:

  - http://www.gnu.org/software/diffutils/manual/html_mono/diff.html

- `sed`:

  - http://www.gnu.org/software/sed/manual/sed.html

- `aspell`:

  - http://aspell.net/man-html/index.html

- There are many other online resources for `sed`, in particular:

  - http://www.grymoire.com/Unix/Sed.html

  - http://sed.sourceforge.net/sed1line.txt

- Also try googling “`sed` one liners”, “`sed` cheat sheets”

## 21 – 格式化输出

在本章中，我们继续探讨与文本相关的工具，重点关注用于格式化文本输出的程序，而不是改变文本本身。这些工具通常用于为最终打印做准备，这将在下一章中介绍。本章将介绍的程序包括：

- `nl` – 给行编号

- `fold` – 将每行换行到指定长度

- `fmt` – 一个简单的文本格式化程序

- `pr` – 为打印准备文本

- `printf` – 格式化并打印数据

- `groff` – 一个文档格式化系统

## 简单的格式化工具

我们先来看一些简单的格式化工具。这些大多是单一用途的程序，在功能上有点不成熟，但可以用于小型任务，以及作为管道和脚本的一部分。

## `nl` – 给行编号

`nl` 程序是一个相当古老的工具，用于执行一个简单的任务：给行编号。在最简单的使用中，它类似于 `cat -n`：

```
[me@linuxbox ~]$ nl distros.txt | head
     1   SUSE      10.2   12/07/2006
     2   Fedora    10     11/25/2008
     3   SUSE      11.0   06/19/2008
     4   Ubuntu    8.04   04/24/2008
     5   Fedora    8      11/08/2007
     6   SUSE      10.3   10/04/2007
     7   Ubuntu    6.10   10/26/2006
```

| 行号 | 发行版 | 版本 | 日期 |
| --- | --- | --- | --- |
| 8 | Fedora | 7 | 05/31/2007 |
| 9 | Ubuntu | 7.10 | 10/18/2007 |
| 10 | Ubuntu | 7.04 | 04/19/2007 |

像 `cat` 一样，`nl` 可以接受命令行参数中的多个文件，或标准输入。然而，`nl` 有许多选项，并支持一种原始的标记形式，以允许更复杂的编号方式。

`nl` 支持一种称为“逻辑页”的概念来进行编号。这允许 `nl` 在编号时重置（重新开始）数字序列。使用选项，可以将起始编号设置为特定值，并在一定程度上设置其格式。逻辑页进一步细分为页眉、正文和页脚。在这些各部分中，行编号可以重置和/或分配不同的样式。如果 `nl` 被赋予多个文件，它会将它们视为单个文本流。文本流中的各部分由添加到文本中的一些看起来很奇怪的标记指示：

### 表 21-1：`nl` 标记

| 标记 | 含义 |
| --- | --- |
| `\:\:\:\:` | 逻辑页页眉的开始 |
| `\:\:\:` | 逻辑页正文的开始 |
| `\:` | 逻辑页页脚的开始 |

上述每个标记元素必须单独占一行。处理完标记元素后，`nl` 会将其从文本流中删除。

以下是 `nl` 的常用选项：

### 表 21-2：常见的 `nl` 选项

| 选项 | 含义 |
| --- | --- |
