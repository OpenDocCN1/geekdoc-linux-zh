
## 使用星号和问号大显身手

你有另一种避免输入长文件名的办法。（毕竟，让用户少做工作正是我们使用计算机的原因，不是吗？）

这个特定的技巧涉及使用星号 (*) 和问号 (?)。这些特殊字符是通配符，因为它们可以匹配文本行中的零个或多个字符。

如果你熟悉 MS-DOS，你可能使用过诸如 COPY *.* A: 这样的命令来将当前目录中的所有文件复制到 A: 驱动器。bash 在文件名中接受类似的通配符。正如你所预期的那样，bash 提供的通配符选项比 MS-DOS 命令解释器多得多。当然，新电脑（尤其是笔记本电脑，特别是上网本）已经不再有 A 和 B 驱动器了，这剥夺了整整一代人尝试将大文件复制到软盘上的乐趣！

你可以在 bash 中使用三种类型的通配符：

- **星号 (*)**：匹配文件名中的零个或多个字符。星号表示目录中的所有文件。
- **问号 (?)**：匹配任意单个字符。如果你输入 **test?**，bash 会匹配以 test 开头的任意五个字符的文本。
- **方括号中的字符集合**：匹配该集合中的任意单个字符。例如，字符串 `[aB]` 仅匹配名为 a 或 B 的文件。而字符串 `[aB]*` 则匹配以 a 或 B 开头的任何文件名。

通配符在你想要对许多文件执行操作时非常方便。例如，要将 /media/cdrom 目录中的所有文件复制到当前目录，请输入以下内容：

```
cp /media/cdrom/* .
```

bash 会用 /media/cdrom 目录中所有文件的名称替换通配符 *。命令末尾的句点代表当前目录。

你可以将星号与其他文件名部分一起使用，以选择更具体的组文件。假设你想使用 grep 命令在 /usr/include 目录中符合以下条件的所有文件中搜索文本 typedef struct：

- 文件名以 s 开头。
- 文件名以 .h 结尾。

通配符规范 s*.h 表示符合这些条件的所有文件名。因此，你可以使用以下命令执行搜索：

```
grep "typedef struct" /usr/include/s*.h
```

该字符串包含一个空格，你希望 grep 命令找到它，因此你必须用引号将该字符串括起来。这样，bash 就不会尝试将该文本中的每个单词解释为单独的命令行参数。

问号 (?) 匹配单个字符。假设当前目录中有四个文件：image1.pcx、image2.pcx、image3.pcx 和 image4.pcx。要将这些文件复制到 /personal/calendar 目录，请使用以下命令：

```
cp image?.pcx /personal/calendar
```

bash 用任意单个字符替换单个问号，并将四个文件复制到 /personal/calendar。

第三种通配符格式 — [ ... ] — 匹配方括号中特定字符集合中的单个字符。你可能希望将此格式与其他通配符结合使用，以将匹配的文件名缩小到更小的集合。要查看 /etc/X11/xdm 目录中以 x 或 X 开头的所有文件名列表，请输入以下命令：

```
ls /etc/X11/xdm/[xX]*
```

## 重复先前输入的命令

为了让你重复长命令变得容易，bash 将最多 500 个旧命令存储为命令历史记录的一部分（旧命令列表）。要查看命令历史记录，请输入 history。bash 会显示旧命令的编号列表，包括你在以前登录期间输入的命令。

如果命令列表太长，你可以限制要查看的旧命令数量。要仅查看最近的 10 个命令，请输入此命令：

```
history 10
```

要重复 `history` 命令显示的列表中的某个命令，请输入感叹号 (!) ，后跟该命令的编号。例如，要重复命令号 3，请输入 `!3`。

你可以在不知道其命令编号的情况下重复命令。假设你几分钟前输入了 `more /usr/lib/X11/xdm/xdm-config`，现在你想再次查看该文件。要重复之前的 `more` 命令，请输入以下内容：

```
!more
```

通常，你想重复上一个输入的命令，也许稍作修改。例如，你可能已使用 `ls -l` 命令显示目录的内容。要重复该命令，请输入两个感叹号，如下所示：

```
!!
```

有时，你想重复上一个命令但为其添加额外的参数。假设 `ls -l` 显示的文件太多。重复该命令，但将输出通过管道传输到 `more` 命令，如下所示：

```
!! | more
```

`bash` 用上一个命令替换两个感叹号，并将该命令附加 `| more`。

![](img/322157d1fa7d965f05bcd68ed0ffc36b_108_0.png)

这是召回以前命令的最简单方法：按向上箭头键。`bash` 会一直向后浏览你输入的命令历史记录。要在命令历史记录中向前移动，请按向下箭头键。

## 发现和使用 Linux 命令

你在 shell 提示符下输入 Linux 命令。通过 *Linux 命令*，我的意思是 `bash` shell 理解的一些命令以及随 Linux 提供的命令行实用程序。在本节中，我介绍 Linux 命令的几个主要类别。

我无法在本章中涵盖每一个 Linux 命令，但我想通过向你展示常见的 Linux 命令，让你感受到命令的广度。表 3-2 按类别列出了常见的 Linux 命令。在开始记忆任何 Linux 命令之前，请浏览此表。

## 表 3-2 基本 Linux 命令

| Command Name | Action |
|---|---|
| **Finding help and abbreviations** |  |
| apropos | Finds online manual pages for a specified keyword. |
| info | Displays online help information about a specified command. |
| man | Displays online help information. |
| whatis | Searches for complete words only and finds the online manual pages. |
| alias | Defines an abbreviation for a long command. |
| type | Shows the type and location of a command. |
| unalias | Deletes an abbreviation defined with alias. |
| **Managing files and directories** |  |
| cd | Changes the current directory. |
| chmod | Changes file permissions. |
| chown | Changes the file owner and group. |
| cp | Copies files. |
| ln | Creates symbolic links to files and directories. |
| ls | Displays the contents of a directory. |
| mkdir | Creates a directory. |
| mv | Renames a file and moves the file from one directory to another. |
| rm | Deletes files. |
| rmdir | Deletes directories. |
| pwd | Displays the current directory. |
| touch | Updates a file's time stamp. |
| **Finding files** |  |
| find | Finds files based on specified criteria, such as name and size. |
| locate | Finds files by using a periodically updated filename database. (The database is created by the updatedb program.) |

(continued)

## 表 3-2（续）

| Command Name | Action |
|---|---|
| whereis | Finds files based in the typical directories where *executable* (also known as *binary*) files are located. |
| which | Finds files in the directories listed in the PATH environment variable. |
| Processing files |  |
| cat | Displays a file in standard output (can be used to concatenate several files into one big file). |
| cut | Extracts specified sections from each line of text in a file. |
| dd | Copies blocks of data from one file to another (used to copy data from devices). |
| diff | Compares two text files and finds any differences. |
| expand | Converts all tabs to spaces. |
| file | Displays the type of data in a file. |
| fold | Wraps each line of text to fit a specified width. |
| grep | Searches for regular expressions in a text file. |
| less | Displays a text file one page at a time. (Go backward by pressing **b**.) |
| lpr | Prints files. |
| more | Displays a text file one page at a time. (Goes forward only). |
| nl | Numbers all nonblank lines in a text file and prints the lines to standard output. |
| paste | Concatenates corresponding lines from several files. |
| patch | Updates a text file by using the differences between the original and revised copies of the file. |
| sed | Copies a file to standard output while applying specified editing commands. |
| sort | Sorts lines in a text file. |
| split | Breaks up a file into several smaller files with specified sizes. |
| tac | Reverses a file (last line first and so on). |
| tail | Displays the last few lines of a file. |
| tr | Substitutes one group of characters for another throughout a file. |
| uniq | Eliminates duplicate lines from a text file. |

