
你可以用以下命令将此文档全部改为大写：

```
# cat LICENSE | tr a-z A-Z
```

```
...
1. YOU MAY MAKE AND GIVE AWAY VERBATIM COPIES OF THE SOURCE FORM OF THE STANDARD VERSION OF THIS PACKAGE WITHOUT RESTRICTION, PROVIDED THAT YOU DUPLICATE ALL OF THE ORIGINAL COPYRIGHT NOTICES AND ASSOCIATED DISCLAIMERS.
2. YOU MAY APPLY BUG FIXES, PORTABILITY FIXES AND OTHER MODIFICATIONS DERIVED FROM THE PUBLIC DOMAIN OR FROM THE COPYRIGHT HOLDER. A PACKAGE MODIFIED IN SUCH A WAY SHALL STILL BE CONSIDERED THE STANDARD VERSION.
...
```

文档已通过 cat 命令以管道方式传输到 tr 命令，指定要将从 a 到 z 的小写字母集合转换为大写字母，或 A 到 Z。tr 命令也可以用于转换单个字符。例如，注意在示例文本中，每个数字和句点后面使用了两个空格。你可以通过使用 -s，或 squeeze，命令行选项来用单个字符替换字符的多次出现：

```
# cat LICENSE | tr -s ' '
```

```
...
1. You may make and give away verbatim copies of the source form of the Standard Version of this Package without restriction, provided that you duplicate all of the original copyright notices and associated disclaimers.
...
```

正如你所见，两个空格已被替换为一个空格。tr 命令还可以将输入过滤到其他命令，例如 cut，以便快速生成自定义报告。例如，如果你不需要 ls 命令的 -l，或 long，格式列表中的所有信息，而只想要输出的某些列，你可以通过几个管道过滤列表来获取你想要的任何列：

```
# ls -l
```

```
...
-rw-r--r-- 1 root root 1898 Jan 29 1998 ANNOUNCE
-rw-r--r-- 1 root root 28796 Jul 23 18:13 CHANGES
-rw-r--r-- 1 root root 68500 Mar 16 1997 HOWTO
-rw-r--r-- 1 root root 5040 May 1 1997 LICENSE
-rw-r--r-- 1 root root 850 Dec 14 1997 LSM
-rw-r--r-- 1 root root 11535 May 1 1997 README
...
```

信息量很大，但如果你只想要每个文件的权限、大小和名称，可以使用以下命令快速生成自定义列表：

```
# ls -l | tr -s " " | cut -d" " -f1,8,9  *
...
-rw-r--r-- 1998 ANNOUNCE
-rw-r--r-- 18:13 CHANGES
-rw-r--r-- 1997 HOWTO
-rw-r--r-- 1997 LICENSE
-rw-r--r-- 1997 LSM
-rw-r--r-- 1997 README
...
```

列表现在只显示原始列表的第一、第八和第九列，因为 tr 命令将多个空格压缩成单个空格。输出通过 cut 命令传输，使用 -d 选项指定字段分隔符（在本例中为空格）。请注意，虽然第一列和第二列看起来不错，但第三列有点参差不齐。如果这仍然不是你想要的，可以剪切不同的字段或再次使用 tr 命令将空格分隔符替换为制表符来清理它：

```
# ls -l | tr -s " " | cut -d" " -f1,5,9 | tr " " '\t'
...
-rw-r--r-- 1898 ANNOUNCE
-rw-r--r-- 28796 CHANGES
-rw-r--r-- 68500 HOWTO
-rw-r--r-- 5040 LICENSE
-rw-r--r-- 850 LSM
-rw-r--r-- 11535 README
...
```

列表现在显示每个文件的权限、文件大小和名称。你可以使用这些过滤器来更改文档中的文本，但流编辑器，例如 sed 命令，提供从命令行编辑文本的更强大的方法。例如，示例许可证文档使用短语 this Package 来描述软件包。如果你是新游戏 Nano-Warrior 的软件开发人员，并且需要节省编写版权许可的时间，可以轻松快速地将 this Package 的所有出现更改为 Nano-Warrior，而无需使用文本编辑器：

```
# cat LICENSE | sed 's/this Package/Nano-Warrior(TM)/g'
...
1. You may make and give away verbatim copies of the source form of the Standard Version of Nano-Warrior(TM) without restriction, provided that you duplicate all of the original copyright notices and associated disclaimers.
...
```

sed s，或 substitute，命令用于搜索第一个字符串的所有实例，并由于 g，或 global，命令而将每个实例替换为第二个。原始文本文件未被更改，你可以通过重定向输出来保存新版本。

sed 命令也设计为使用编辑脚本工作。要对文件进行大量常规更改，请创建编辑脚本并使用脚本编辑文件。使用 sed 命令的 -f，或 script file，命令行选项来使用脚本：

```
# sed -f myscript.sed < form.ltr >output.ltr
```

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_353_0.png)

> 你的 OpenLinux 发行版中包含的文本过滤器太多，无法在此小时内讨论；请参阅本节开头附近列出的过滤器命令的手册页。你可能还想尝试 wc，或 word count，程序，它报告文本文档中的字符、单词和行数。

## 检查你的文档拼写

文档中拼写错误的单词可能会很尴尬，尤其是当其他人阅读你的文本时。正确的拼写是写作和文字处理的重要组成部分。就像语法错误会导致编程错误一样，拼写错误会导致沟通不畅、失去潜在工作或客户，或主管的尊重。

幸运的是，你的 Linux 发行版附带了 ispell 拼写检查器，因此你不必遭受拼写错误的尴尬！本节向你展示如何更正文档并修复拼写错误。

### 使用 ispell 命令校正文档

ispell 命令位于 /usr/bin 目录下，是一个交互式拼写程序，你可以单独使用或与文本编辑器一起使用来更正拼写错误。你的 Linux 发行版中包含的几个编辑器，例如 emacs 和 pico，都已设置好自动使用此程序进行拼写检查，但单独使用 ispell 很简单。例如，要检查文件 myfile.txt 的拼写，请使用以下命令：

```
# ispell myfile.txt
```

ispell 程序加载文本，然后在上下文中显示第一个找到的错误，以及一个或多个建议的替换，如以下示例所示：

```
MERCHANTABILITY          File: LICENSE

WARRANTIES, INCLUDING, WITHOUT LIMITATION, THE IMPLIED WARRANTIES OF
MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE.

? : MERCHANTIBILITY
[SP] <number> R)epl A)ccept I)nsert L)ookup U)ncap Q)uit e(X)it or ?
? for help
```

通过输入 0，建议的替换词的编号，或 R，可以通过重新输入该词来替换该词，从而更正拼写。

使用 L，lookup 命令，查找其他单词，该命令搜索位于 /usr/dict 目录下的系统词典，称为 words。如果你使用 I，或 insert 命令，ispell 会在你的主目录中创建一个个人词典，使用 .ispell_english 作为文件名。

你也可以在 ispell 命令行上指定多个文档：

```
# ispell *.txt
```

此命令行会导致 ispell 加载每个以 .txt 结尾的文件进行拼写检查。如果你更喜欢将 ispell 用作更传统的 UNIX spell 命令，该命令读取文档然后打印出疑似单词的列表，请在命令行上使用 -l，或 list，选项：

```
# ispell -l < LICENSE
```

```
...
Julianne
Haugh
uunet
UU
MERCHANTABILITY
...
```

请注意，< 重定向运算符被使用，因为在 -l 模式下，ispell 命令充当拼写过滤器，检查输入文本流与其词典（位于 /usr/lib/ispell 目录下）是否匹配。你可以将此列表重定向到文件或在命令行上使用 -f 选项：

```
# ispell -l -f errors -a <LICENSE
```

这会将所有拼写错误的单词发送到名为 errors 的文件。ispell 程序有 15 个不同的命令行选项。使用 -L 选项更改上下文，或在疑似错误之前和之后显示的文本量。-b 选项创建原始文档的备份文件，如果你不小心输入了错误的更正，这是一个好主意（这是你版本 ispell 的默认值）。

ispell 包包含另外九个程序，你可以使用它们来构建自己的词典或将个人词典中的单词列表添加到 ispell 词典中。有关这些程序的详细信息，请参阅 ispell 手册页。有关构建自己的词典的详细信息，请阅读位于 /usr/man/man5 目录下的 ispell 手册页。你可以使用以下命令执行此操作：

```
# man 5 ispell
```

ispell 的文档位于其两个手册页和 /usr/doc/ispell 目录下。
