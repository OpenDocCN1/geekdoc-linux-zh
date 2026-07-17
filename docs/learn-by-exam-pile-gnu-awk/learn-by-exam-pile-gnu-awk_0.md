# 通过题库学习：GNU AWK




1. 封面
2. 目录

# 前言

在涉及到命令行文本处理时，从抽象的角度来看，有三大支柱：用于过滤的 `grep`、用于替换的 `sed` 以及用于字段处理的 `awk`。这些工具也具有一些重叠的功能，例如，这三者都具备强大的过滤能力。

与 `grep` 和 `sed` 不同，`awk` 是一门完整的编程语言。然而，本书旨在展示如何从命令行组合成 `awk` 单行命令（one-liners），而不是编写程序文件。

本书极度依赖示例来逐一介绍 `awk` 的选项和功能。建议你手动输入每个示例并进行实验。理解示例输入字符串的本质以及产生的输出至关重要。类比一下，这就像学习骑自行车或开车——无论你读了多少相关书籍或听了多少解释，你都需要大量的练习并推导出自己的结论。如果你觉得复制粘贴更适合你，可以在 [GitHub 上按章节获取代码片段](https://github.com/learnbyexample/learn_gnuawk/tree/master/code_snippets)。

## 前提条件

* 拥有命令行和 `bash` shell 的工作经验，应熟悉文件重定向、命令管道等概念。
* 熟悉编程概念，如变量、打印、函数、控制结构、数组等。
* 了解 `grep` 和 `sed` 的基础将有助于理解 `awk` 的相似功能。

如果你是命令行世界的新手，在开始本书之前，请先查看我整理的 [Linux CLI 和 Shell 脚本](https://learnbyexample.github.io/curated_resources/linux_cli_scripting.html) 资源。

我的 [命令行文本处理](https://github.com/learnbyexample/Command-line-text-processing) 仓库包含关于 `GNU awk` 的章节，该章节经过编辑和重构，形成了本书。

## 规范

* 此处展示的示例已在 `GNU bash` shell 和 `GNU awk 5.1.0` 上经过测试，并包含了早期版本不支持的功能。
* 所示的代码片段是从 `bash` shell 复制粘贴并为了演示目的修改过的。某些命令前带有注释，以提供背景和解释。为了提高可读性增加了空行；速度对比中仅显示 `real` 时间；对于 `wget` 等命令则跳过了输出。
* 除非另有说明，所有示例和解释均针对 `ASCII` 字符。
* 除非特别指定，`awk` 指 `GNU awk`，`grep` 指 `GNU grep`，以此此类推。
* 本书中提供了外部链接以供进一步阅读。不需要立即访问。它们经过了仔细挑选，会对你有帮助，尤其是在重读时。
* [learn_gnuawk 仓库](https://github.com/learnbyexample/learn_gnuawk) 包含了示例、练习以及与书籍相关的全部代码片段和文件。如果你不熟悉 `git` 命令，请点击网页上的 `Code` 按钮获取文件。

## 致谢

* [GNU awk documentation](https://www.gnu.org/software/gawk/manual/) — 手册和示例。
* [stackoverflow](https://stackoverflow.com/) 和 [unix.stackexchange](https://unix.stackexchange.com/) —— 获取关于 `bash`、`awk` 和其他命令问题的答案。
* [tex.stackexchange](https://tex.stackexchange.com/) —— 获取关于 [pandoc](https://github.com/jgm/pandoc/) 和 `tex` 相关问题的帮助。
* [LibreOffice Draw](https://www.libreoffice.org/discover/draw/) —— 封面图片。
* [pngquant](https://pngquant.org/) 和 [svgcleaner](https://github.com/RazrFalcon/svgcleaner) 用于优化图像。
* [softwareengineering.stackexchange](https://softwareengineering.stackexchange.com/questions/39/whats-your-favourite-quote-about-programming) 和 [skolakoda](https://skolakoda.org/programming-quotes) 用于编程格言。
* 由 [Amada44](https://commons.wikimedia.org/wiki/User:Amada44) 提供的公有领域 [Warning](https://commons.wikimedia.org/wiki/File:Warning_icon.svg) 和 [信息](https://commons.wikimedia.org/wiki/File:Info_icon_002.svg) 图标。
* [arifmahmudrana](https://github.com/arifmahmudrana) 指出了一个歧义的解释。

特别感谢我所有的朋友和在线伙伴提供的帮助、支持和鼓励，特别是在这些艰难的时刻。

## 反馈与错误

如果你能告诉我你对这本书的感受，我将不胜感激，这将有助于本书以及我未来的尝试。此外，如果你发现任何错误或错别字，请尽管告知。

问题管理器：[`github.com/learnbyexample/learn_gnuawk/issues`](https://github.com/learnbyexample/learn_gnuawk/issues)

电子邮箱：learnlearnbyexample.net@gmail.com

Twitter：[`twitter.com/learn_byexample`](https://twitter.com/learn_byexample)

## 作者信息

Sundeep Agarwal 是一位自由培训师、作者和导师。他之前的经历包括在 Analog Devices 工作了 5 年多。你可以找到他的其他作品，主要是书籍 [命令行基础](https://www.packt.com/product/command-line-fundamentals/p36444)。他还担任过 [命令行基础](https://www.packt.com/product/command-line-fundamentals/p36444) 的技术评审员。

## 许可证

本作品采用 [Creative Commons 署名-非商业-相同共享 4.0 ](https://creativecommons.org/licenses/by-sa/4.0/) 许可。代码片段可在 `https://github.com/learnbyexample/` 获取。

## 书籍版本

查看 [Version_changes.md](https://github.com/learnbyexample/learn_gnuawk) 以跟踪更改。

# 安装与文档

`awk` 命令名称源于它的开发者——Alfred V. Aho、Peter J. Weinberger 和 Brian W. Kernighan。多年来，它被各种开发者不断适配和修改。详情请参见 [gawk 手册: History](https://www.gnu.org/software/gawk/manual.html#History)。本章将展示如何安装或升级 `awk`，随后是与文档相关的详细信息。

## 安装

如果你在类 Unix 系统上，你可能已经安装了某个版本的 `awk`。本书主要针对 `GNU awk`。由于不同实现之间存在语法和功能的差异，请确保按照此处演示的内容进行。要安装更新或特定版本，请访问 [gnu: software gawk](https://www.gnu.org/software/gawk/)。

```
## 使用一个目录，例如 ~/Downloads/awk_install 然后执行以下步骤
$ wget https://ftp.gnu.org/gnu/gawk/gawk-5.1.0.tar.xz
$ tar -Jxf gawk-5.1.0.tar.xz
$ cd gawk-5.1.0/
$ ./configure
$ make
$ sudo make install

$ type -a awk
awk is /usr/local/bin/awk
awk is /usr/bin/awk
$ awk --version | head -n1
GNU Awk 5.1.0, API: 3.0
```




> ![info](img/file0.svg) 请参阅 [gawk 手册：安装](https://www.gnu.org/software/gawk/manual/html_node/Installation.html) 获取高级选项以及在其他平台上安装 `awk` 的说明。

## 文档

知道哪里找到文档总是一个好主意。从命令行，你可以使用 `man awk` 查看简短手册，使用 `info awk` 查看完整文档。[在线 GNU awk 手册](https://www.gnu.org/software/gawk/manual/) 拥有更好的阅读界面，并提供最完整的文档、示例以及关于其他 `awk` 版本、POSIX 标准等信息。

以下是 `man awk` 的一个片段：

```
[](#cb2-1)$ man awk
[](#cb2-2)GAWK(1)                        Utility Commands                        GAWK(1) 
[](#cb2-3) 
[](#cb2-4)NAME
[](#cb2-5)       gawk - pattern scanning and processing language
[](#cb2-6)
[](#cb2-7)SYNOPSIS
[](#cb2-8)       gawk [ POSIX or GNU style options ] -f program-file [ -- ] file ...
[](#cb2-9)       gawk [ POSIX or GNU style options ] [ -- ] program-text file ...
[](#cb2-10)
[](#cb2-11)DESCRIPTION
[](#cb2-12)       Gawk  is  the  GNU Project's implementation of the AWK programming lan‐
[](#cb2-13) guage.  It conforms to the definition of  the  language  in  the  POSIX
[](#cb2-14) 1003.1  Standard.   This version in turn is based on the description in
[](#cb2-15) The AWK Programming Language, by Aho, Kernighan, and Weinberger.   Gawk
[](#cb2-16) provides  the additional features found in the current version of Brian
[](#cb2-17) Kernighan's awk and numerous GNU-specific extensions.
```

## 选项概述

若要快速概述所有可用选项，请在命令行使用 `awk --help`。

```
[](#cb3-1)$ awk --help
[](#cb3-2)Usage: awk [POSIX or GNU style options] -f progfile [--] file ...
[](#cb3-3)Usage: awk [POSIX or GNU style options] [--] 'program' file ...
[](#cb3-4)POSIX options:                  GNU long options: (standard)
[](#cb3-5)    -f progfile                 --file=progfile
[](#cb3-6)    -F fs                       --field-separator=fs
[](#cb3-7)    -v var=val                  --assign=var=val
[](#cb3-8)Short options:                  GNU long options: (extensions)
[](#cb3-9)    -b                          --characters-as-bytes
[](#cb3-10)    -c                          --traditional
[](#cb3-11)    -C                          --copyright
[](#cb3-12)    -d[file]                    --dump-variables[=file]
[](#cb3-13)    -D[file]                    --debug[=file]
[](#cb3-14)    -e 'program-text'           --source='program-text'
[](#cb3-15)    -E file                     --exec=file
[](#cb3-16)    -g                          --gen-pot
[](#cb3-17)    -h                          --help
[](#cb3-18)    -i includefile              --include=includefile
[](#cb3-19)    -l library                  --load=library
[](#cb3-20)    -L[fatal|invalid|no-ext]    --lint[=fatal|invalid|no-ext]
[](#cb3-21)    -M                          --bignum
[](#cb3-22)    -N                          --use-lc-numeric
[](#cb3-23)    -n                          --non-decimal-data
[](#cb3-24)    -o[file]                    --pretty-print[=file]
[](#cb3-25)    -O                          --optimize
[](#cb3-26)    -p[file]                    --profile[=file]
[](#cb3-27)    -P                          --posix
[](#cb3-28)    -r                          --re-interval
[](#cb3-29)    -s                          --no-optimize
[](#cb3-30)    -S                          --sandbox
[](#cb3-31)    -t                          --lint-old
[](#cb3-32)    -V                          --version
```

# awk 介绍

本章将概述 `awk` 语法并提供一些示例，展示你可以使用 `awk` 解决什么类型的问题。这些功能将在后面的章节中深入介绍，但不要跳过本章。

## 过滤

`awk` 提供了类似于 `grep` 和 `sed` 支持的过滤功能，以及它自身的一些巧妙功能。与许多命令行工具一样，`awk` 可以从 `stdin` 和文件接受输入。

```
[](#cb4-1)$ # sample stdin data
[](#cb4-2) # sample stdin data
```




`sub` 和 `gsub` 函数的第一个参数是用于匹配输入内容的正则表达式。第二个参数是替换字符串。字符串字面量在双引号内指定。在上面的示例中，`sub` 和 `gsub` 被用在块内部，因为它们并不是设计用于条件表达式的。块后面的 `1` 被视为条件表达式，因为它是在块外部使用的。你也可以使用下面展示的变体来获得相同的结果。

*   `awk '{sub(/:/, "-")} 1'` 等同于 `awk '{sub(/:/, "-"); print $0}'`
*   你也可以用 `print` 代替 `print $0`，因为 `$0` 是默认字符串。

> ![info](img/file0.svg) 你可能可能会奇怪，既然已经可以用 `awk` 实现相同的结果，为什么还要使用或学习 `grep` 和 `sed`呢？这取决于你尝试解决的问题。对于简单的行过滤，`grep` 会比 `sed` 或 `awk` 更快，因为 `grep` 针对此类情况进行了优化。同样，对于替换场景，`sed` 会比 `awk` 快。此外，并不是所有功能都能在这些工具之间轻松转换。例如，用 `sed` 或 `awk` 编写 `grep -o` 需要更多的代码步骤。只有 `grep` 提供递归搜索。诸此类推。另请参见 [unix.stackexchange: When to use grep, sed, awk, perl, etc.](https://unix.stackexchange.com/q/303044/109046)。

## 字段处理

如前所述，`awk` 主要用于基于字段的处理。考虑下面所示的示例输入文件，字段由单个空格字符分隔。

> ![info](img/file0.svg) [learn_gnuawk 仓库](https://github.com/learnbyexample/learn_gnuawk/tree/master/example_files) 包含了示例中使用的所有文件。

```
[](#cb8-1)$ cat table.txt
[](#cb8-2)brown bread mat hair 42
[](#cb8-3)blue cake mug shirt -7
[](#cb8-4)yellow banana window shoes 3.14
```

这里是一些基于特定字段而非整行的示例。默认情况下，`awk` 根据空格分割输入行，字段内容可以通过 `$N` 访问，其中 `N` 是所需的字段编号。特殊变量 `NF` 会更新为每行输入的字段总数。虽然还有更多细节需要介绍，但目前这些足够继续操作了。

```
[](#cb9-1)$ # 打印每个输入行的第二个字段
[](#cb9-2)$ awk '{print $2}' table.txt
[](#cb9-3)bread
[](#cb9-4)cake
[](#cb9-5)banana
[](#cb9-6)
[](#cb9-7)$ # 仅当最后一个字段为负数时打印这些行
[](#cb9-8)$ # 记住默认操作是打印 $0 的内容
[](#cb9-9)$ awk '$NF<0' table.txt
[](#cb9-10)blue cake mug shirt -7
[](#cb9-11)
[](#cb9-12)$ # 仅针对第一个字段将 'b' 改为 'B'
[](#cb9-13)$ awk '{gsub(/b/, "B", $1)} 1' table.txt
[](#cb9-14)Brown bread mat hair 42
[](#cb9-15)Blue cake mug shirt -7
[](#cb9-16)yellow banana window shoes 3.14
```

## awk 一行命令结构

之前章节中的示例使用了几种不同的方法来构建典型的 `awk` 一行命令。如果你还没有掌握语法，这个通用结构可能会有所帮助：

`awk 'cond1{action1} cond2{action2} ... condN{actionN}'`

如果未提供条件，则始终会执行动作（action）。在块内部，你可以提供多个用分号隔开的语句。如果未提供动作，那么当条件求值为 `true` 时，默认会打印 `$0` 变量的内容。当不存在动作时，你可以使用分号来结束一个条件并开始另一个 `condX{actionX}` 片段。

注意，多个块只是语法上的糖。。它有助于在大多数一行命令中避免显式地使用 `if` 控制结构。下面的代码段展示了使用和不使用 `if` 结构时的等效代码。

```
[](#cb10-1)$ awk '{
[](#cb10-2) if($NF < 0){
[](#cb10-3) print $0
[](#cb10-4) }
[](#cb10-5) }' table.txt
[](#cb10-6)blue cake mug shirt -7
[](#cb10-7)
[](#cb10-8)$ awk '$NF<0' table.txt
[](#cb10-9)blue cake mug shirt -7
```

当你需要在读取输入之前执行某些操作时可以使用 `BEGIN{}` 块，在处理所有输入之后执行某些操作时可以使用 `END{}` 块。

```
[](#cb11-1)$ seq 2 | awk 'BEGIN{print "---"} 1; END{print "%%%"}'
[](#cb11-2)---
[](#cb11-3)1
[](#cb11-4)%%%
```

后续章节会有更多类型。请参见 [awk 手册：运算符](https://www.gnu.org/software/gawk/manual/gawk.html#Operators) 了解细节。请参见 [awk 手册：字符串与数字](https://www.gnu.org/software/gawk/manual/gawk.html#Values-Conditions) 了解更多。

## 字符串与数字

到目前为止示例使用了字符串和数字。如提到的，`awk` 会尝试将字符串转换为数字。字符串字面量在双引号内。数字可以是整数或浮点数。允许科学计数法。请参见 [awk 手册：字符串与数字](https://www.gnu.org/software/gawk/manual/gawk.html#Strings-and-Numbers) 了解细节。

```
[](#cb12-1)$ # 等于：awk 'BEGIN{print "hi"}'
[](#cb12-2)hi
[](#cb12-3)
```

你也可以将这些保存在变量中以后使用。

```
[](#cb13-1)$ # 使用：awk 'BEGIN{a=5}'
[](#cb13-2)5
[](#cb13-3)
```

如果使用了未初始变量，它将作为空字符串。

```
[](#cb14-1)$ # 示例：awk 'BEGIN{s1="con"; s2="cat"; print s1 s2}'
[](#cb14-2)concat
[](#cb14-3)
```

如果字符串以有效数字开头，它将表现为 `0`。

```
[](#cb15-1)$ # 等于：awk 'BEGIN{sum=0}'
[](#cb15-2)0
[](#cb15-3)
```

## 数组

`awk` 中的数组是关联的，这意味着它们键值对。键可以是数字或字符串，但数字内部会被转换为字符串。它们也可以是多维的。在后续相关章节会有大量的数组示例。请参见 [gawk 手册：数组](https://www.gnu.org/software/gawk/manual/gawk.html#Arrays) 了解完整的细节和注意事项。

```
[](#cb16-1)$ # 分配数组并根据字符串键访问元素
[](#cb16-2)$ awk 'BEGIN{student["id"] = 101; student["name"] = "Joe";
[](#cb16-3) print student["name"]}'
[](#cb16-4)Joe
[](#cb16-5)
[](#cb16-6)$ # 检查键是否存在
[](#cb16-7)$ awk 'BEGIN{student["id"] = 101; student["name"] = "Joe";
[](#cb16-8) if("id" in student) print "Key found"}'
[](#cb16-9)Key found
```




在我刚开始接触 Linux 命令行时，我被 `sed` 和 `awk` 的示例吓住了，甚至没有尝试过学习它们。希望这个更温和的介绍对你有所帮助，并且各种语法魔法已经得到了充分解释。尝试对给定的示例进行实验，例如将字段编号更改为除使用的数字以外数字。保持好奇，例如如果字段编号是负数或浮点数会发生什么。阅读手册。多练习。

下一章专门介绍正则表达式。本章介绍的功能将用于示例中，因此在继续之前，请确保你已经熟悉 `awk` 的语法。而且，请解决下一节中的练习题。

## 练习

> ![info](img/file0.svg) 练习相关文件从 [learn_gnuawk repo 的 exercises 文件夹](https://github.com/learnbyexample/learn_gnuawk/tree/master/exercises) 获取。所有练习也已汇总在 [Exercises.md](https://github.com/learnbyexample/learn_gnuawk/blob/master/exercises/Exercises.md) 一处。解决方案请参阅 [Exercise_solutions.md](https://github.com/learnbyexample/learn_gnuawk/blob/master/exercises/Exercise_solutions.md)。

**a)** 对于输入文件 `addr.txt`，显示所有包含 `is` 的行。

```
[](#cb16-1)$ cat addr.txt
[](#cb16-2)Hello World
[](#cb16-3)How are you
[](#cb16-4)This game is good
[](#cb16-5)Today is sunny
[](#cb16-6)12345
[](#cb16-7)You are funny
[](#cb16-8)
[](#cb16-9)$ awk ##### add your solution here
[](#cb16-10)This game is good
[](#cb16-11)Today is sunny
```

**b)** 对于输入文件 `addr.txt`，显示不包含 `y` 的行的第一个字段。此文件空格空格字段分隔符。

```
[](#cb17-1)$ awk ##### add your solution here
[](#cb17-2)Hello
[](#cb17-3)This
[](#cb17-4)12345
```

**c)** 对于输入文件 `addr.txt`，显示所有包含不超过 2 个字段的行。

```
[](#cb18-1)$ awk ##### add your solution here
[](#cb18-2)Hello World
[](#cb18-3)12345
```

**d)** 对于输入文件 `addr.txt`，显示第二个字段中包含 `is` 的行。

```
[](#cb19-1)$ awk ##### add your solution here
[](#cb19-2)Today is sunny
```

**e)** 对于输入文件 `addr.txt` 的每一行，将 `o` 的第一次出现处替换为 `0`。

```
[](#cb20-1)$ awk ##### add your solution here
[](#cb20-2)Hell0 World
[](#cb20-3)H0w are you
[](#cb20-4)This game is g0od
[](#cb20-5)T0day is sunny
[](#cb20-6)12345
[](#cb20-7)Y0u are funny
```

**f)** 对于输入文件 `table.txt`，计算并显示每行最后一个字段中数字的乘积。此文件空格字段分隔符。

```
[](#cb21-1)$ cat table.txt
[](#cb21-2)brown bread mat hair 42
[](#cb21-3)blue cake mug shirt -7
[](#cb21-4)yellow banana window shoes 3.14
[](#cb21-5)
[](#cb21-6)$ awk ##### add your solution here
[](#cb21-7)-923.16
```

**g)** 在给定的 `stdin` 数据的所有输入行末尾附加 `.`。

```
[](#cb22-1)$ printf 'last\nappend\nstop\nttail\n' | awk ##### add your solution here
[](#cb22-2)last.
[](#cb22-3)append.
[](#cb22-4)stop.
[](#cb22-5)tail.
```

## 正则表达式

正则表达式是一种用于文本处理的多功能工具。它可以帮助精确定义匹配标准。为了学习和理解，可以将正则表达式视为一种专门用于文本处理的微型编程语言。正则表达式的某些部分可以保存以备后用，类似于变量和函数。有方法执行 AND（与）、OR（或）、NOT（非）条件，以及简洁定义重复的特征以避免手动复制等。

这里是一些常见用例：

*   清理字符串以确保符合一组已知的规则。例如，检查给定字符串是否符合密码规则。
*   在抽象层上过滤或提取部分，如字母、数字、标点符号等。
*   限定的字符串替换。例如，在字符串的开头或结尾，根据周围文本仅替换整个单词等。

本章将涵盖 `awk` 中实现的正则表达式。`awk` 的大多数正则表达式语法与 `grep -E` Find 的扩展正则表达式 (ERE) 相似。

> ![info](img/file0.svg) 练习相关文件从 [learn_gnuawk repo 的 exercises 文件夹](https://github.com/learnbyexample/learn_gnuawk/tree/master/exercises) 获取。所有练习也已汇总在 [Exercises.md](https://github.com/learnbyexample/learn_gnuawk/blob/master/exercises/Exercises.md) 一处。解决方案请参阅 [Exercise_solutions.md](https://github.com/learnbyexample/learn_gnuawk/blob/master/exercises/Exercise_solutions.md)。

### 语法与变量

如前章所示，`string /regexp/` 检查字符串是否满足正则表达式。`string !~ /regexp/` 反转条件。你也可以将正则表达式保存在变量中。

```
r = "ed"
if ($0 ~ r) { print "found" }
```

### 字符串锚点

在之前的示例中，`awk` 在任何地方匹配。除非另有说明，否则转义字符。这些具有特殊含义的字符被称为元字符。

有两个字符串锚点：

*   `^` 元字符将匹配限制在字符串的开头。
*   `$` 元字符将匹配限制在字符串的结尾。

```
[](#cb24-1)$ cat addr.txt
[](#cb24-2)Hello World
[](#cb24-3)How are you
[](#cb24-4)This game is good
[](#cb24-5)Today is sunny
[](#cb24-6)12345
[](#cb24-7)You are funny
[](#cb24-8)
[](#cb24-9)$ awk ##### add your solution here
[](#cb24-10)This game is good
[](#cb24-11)Today is sunny
```




使用 `\<` 表示单词起始锚点，使用 `\>` 表示单词结束锚点。作为替代方案，你可以使用 `\y` 同时表示单词的起始和结束锚点。

> ![info](img/file0.svg) 通常 `\b` 用于表示单词锚点（例如在 `grep`、`sed`、`perl` 等中），但在 `awk` 中，转义序列 `\b` 指的是退格字符。

```
cat word_anchors.txt
sub par
spar
apparent effort
two spare computers
cart part tart mart
$ # 以 'par' 开头的单词
$ awk '/\<par/' word_anchors.txt
sub par
cart part tart mart
$ # 以 'par' 结尾的单词
$ awk '/par\>/' word_anchors.txt
sub par
spar
$ # 仅匹配整个单词 'par'
$ # 注意只有替换成功的行会被打印
$ # 因为 sub/gsub 的返回值是替换的次数
$ awk 'gsub(/\<par\>/, "***")' word_anchors.txt
sub ***
```

> ![warning](img/file1.svg) 另参 单词边界差异 。

`\y` 也有反向操作。`\B` 匹配单词锚点匹配以外的位置。

```
# 如果 'par' 被单词字符包围，则匹配它
$ awk '/\Bpar\B/' word_anchors.txt
apparent effort
two spare computers
$ # 匹配 'par' 但不是作为单词起始
$ awk '/\Bpar/' word_anchors.txt
spar
apparent effort
two spare computers
$ # 匹配 'par' 但不是作为单词结束
$ awk '/par\B/' word_anchors.txt
apparent effort
two spare computers
cart part tart mart
```

这是一个将单词边界本身作为模式使用的示例。它也清晰地展示了 `\y` 和 `\B` 的相反功能。

```
echo 'copper' | awk '{gsub(/\y/, ":")} 1'
:copper:
$ echo 'copper' | awk '{gsub(/\B/, ":")} 1'
c:o:p:p:e:r
```

> ![warning](img/file1.svg) 否定逻辑在许多文本处理场景中非常有用。但请谨慎使用，否则你可能会匹配到你无意的内容。

## 组合条件

在查看下一个正则表达式特性之前，最好注意，有时使用逻辑运算符比用正则表达式完成所有工作更易于阅读和维护。

```
# 字符串以 'b' 开头但不包含 'at'
$ awk '/^b/ && !/at/' table.txt
blue cake mug shirt -7
$ # 如果第一个字段包含 'low' 或者最后一个字段小于 0
$ awk '$1 ~ /low/ || $NF<0' table.txt
blue cake mug shirt -7
yellow banana window shoes 3.14
```

## 分支 (Alternation)

很多时候，你想要搜索多个术语。在条件表达式中，你可以使用逻辑运算符组合多个条件。在正则表达式中，元字符 `|` 类似于逻辑或。如果由 `|` 分隔的表达式中有任何一个满足条件，正则表达式将匹配。这些表达式也可以拥有自己独立的锚点。

分支 类似于在两个正则表达式之间使用 `||` 运算符。使用单个正则表达式有助于编写更简洁的代码，且在需要替换时无法使用 `||`。

```
# 匹配整个单词 'par' 或以 's' 结尾的字符串
## 等同于：awk '/\<par\>/ || /s$/
$ awk '/\<par\>|s$/' word_anchors.txt
sub par
two spare computers
$ 将 'cat' 或 'dog' 或 'fox' 替换为 '--'
$ echo 'cats dog parrot foxed' | awk '{gsub(/cat|dog|fox/, "--")} 1'
```

使用分支时存在一些复杂的情况。如果它用于过滤行，则没有歧义。但对于替换等用例，取决于几个因素。例如，你想替换 `are` 或 `spared` —— 哪一个获得优先级？是更大的单词 `spared`，还是它内部的子字符串 `are`，或者基于其他什么？在输入中最早匹配的分支获得优先级。

```
## 注意这里使用了 'sub'，所以第一个匹配的项会被替换
$ echo 'cats dog parrot foxed' | awk '{sub(/bee|parrot/, "--")} 1'
cats dog parrot foxed
$ echo 'cats dog parrot foxed' | awk '{sub(/parrot|at/, "--")} 1'
```

在匹配从相同位置开始的情况下，对于 `spar` 和 `spared`，最长部分获得优先级。与其他正则表达式实现不同，分支的从左到右优先级仅在匹配长度相同时才起作用。请参 最长匹配获胜 和 反引用 以了解更多示例。

```
echo 'spared party parent' | awk '{sub(/spa|spared/, "--")} 1'
party parent
$ echo 'spared party parent' | awk '{sub(/spared|spa/, "--")} 1'
party parent
## 其他实现如 'perl' 具有从左到右的优先级
$ echo 'spared party parent' | perl -pe 's/spa|spared/'
```

## 分组

通常，正则表达式之间有一些共同点。可能是共同字符，也可能是锚点之类的限定符。在这种情况下，你可以使用一对元字符对它们进行分组。类似于数学中的 `a(b+c)`d`，在正则表达式中得到 `a(b|c)d`。

```
### 无分组
$ printf 'red\nreform\nread\narrest\n' | awk '/reform|rest/'
reform
### 有分组
$ printf 'red\nreform\nread\narrest\n' | awk '/re(form|st)/'
arrest
### 无分组
$ printf 'sub par\nspare\npart time\n' | awk '/\<par>|\<part>/'
sub par
part time
### 提取共同锚点
$ printf 'sub par\nspare\npart time\n' | awk '/\<par|t)>\'
sub par
part time
# 也提取共同字符
# 你以后将学习一种更好的技术，而不是使用空分支
$ awk '/\<par(|t)>\'
sub par
part time
```

## 匹配元字符

你已经看到了一些有助于组合正则表达式的元字符和转义序列。要字面匹配这些元字符（即移除它们的特殊含义），在这些字符前加上 `\` 字符。要表示字面量 `\` 字符，请使用 `\\`。

与 `grep` 和 `sed` 不同，字符串锚点必须始终转义才能字面匹配，因为 `awk` 中没有 BRE 模式。当它们不在惯常的位置时，它们不会失去其特殊含义。

```
### awk '/b²/' 将不起作用，即使 ^ 没有被作锚点
### 如果使用 BRE 语法，b² 对于 grep 和 sed 都是有效的
$ echo 'a² + b² - C*3' | awk '/b\²/'
a² + b² - C*3
### 注意 ')' 不需要转义
$ echo '(a*b) + c' | awk '{gsub(/\(|)/, "")} 1'
a*b + c
$ echo '\learn\by\example' | awk '{gsub(/\\/, "/")} 1'
/learn/by/example
```

> ![info](img/file0.svg) 反引用 将在替换部分讨论如何处理元字符。

## 使用字符串字面量作为正则





`sub` 和 `gsub` 函数的第一个参数也可以是字符串，`awk` 会处理将其转换为正则表达式。这有几个优点。例如，如果你在搜索模式中有许多 `/` 字符，那么使用字符串而不是正则表达式可能会更简单。

```
[](#cb35-1)$ p='/home/learnbyexample/reports'
[](#cb35-2)$ echo "$p" | awk '{sub(/\/home\/learnbyexample\//, "~/")} 1'
[](#cb35-3)~/reports
[](#cb35-4)$ echo "$p" | awk '{sub("/home/learnbyexample/", "~/")} 1'
[](#cb35-5)~/reports
[](#cb35-6)
[](#cb35-7)$ # 使用行匹配而非替换的示例
[](#cb35-8)$ printf '/foo/bar/1\n/foo/baz/1\n' | awk '/\/foo\/bar\//'
[](#cb35-9)/foo/bar/1
[](#cb35-10)$ printf '/foo/bar/1\n/foo/baz/1\n' | awk '$0 ~ "/foo/bar/"'
[](#cb35-11)/foo/bar/1
```

在上面的示例中，直接提供了字符串字面量。但也可以使用任何其他表达式或变量，相关的示例将在本章的稍后部分显示。不总是使用字符串作为第一个参数的原因是 `\` 字符的特殊含义会产生冲突。例如：

```
[](#cb36-1)$ awk 'gsub("\<par\>", "X")' word_anchors.txt
[](#cb36-2)awk: cmd. line:1: warning: escape sequence `\<' treated as plain `<`
[](#cb36-3)awk: cmd. line:1: warning: escape sequence `\>` treated as plain `>`
[](#cb36-4)
[](#cb36-5)$ # 你需要用 \\ 来表示 \
[](#cb36-6)$ awk 'gsub("\\<par\\>", "X")' word_anchors.txt
[](#cb36-7)sub X
[](#cb36-8)$ # 使用正则表达式字面量更易读
[](#cb36-9)$ awk 'gsub(/\<par\>/, "X")' word_anchors.txt
[](#cb36-10)sub X
[](#cb36-11)
[](#cb36-12)$ # 另一个示例
[](#cb36-13)$ echo '\learn\by\example' | awk '{gsub("\\\\", "/")} 1'
[](#cb36-14)/learn/by/example
[](#cb36-15)$ echo '\learn\by\example' | awk '{gsub(/\\/, "/")} 1'
[](#cb36-16)/learn/by/example
```

> ![info](img/file0.svg) 查看 [gawk 手册：详细细节](https://www.gnu.org/software/gawk/manual/gawk.html#Gory-Details) 获取比你需要的更多的信息。

## 点元字符 `.`

点元字符用作占位符来匹配任何字符（包括换行符）。稍后你将学习如何为有限字符集定义自定义的占位符。

```
[](#cb37-1)$ # 以 'c' 开始以 't' 结尾的 3 字符序列
[](#cb37-2)$ echo 'tac tin cot abc:tyz excited' | awk '{gsub(/c.t/, "-")} 1'
[](#cb37-3)ta-in - ab-yz ex-ed
[](#cb37-4)
[](#cb37-5)$ # 任意字符后跟 3 再跟任意字符
[](#cb37-6)$ printf '4\t35x\n' | awk '{gsub(/.3./, "")} 1'
[](#cb37-7)4x
[](#cb37-8)
[](#cb37-9)$ # 'c' 后跟任意字符再跟 'x'
[](#cb37-10)$ awk 'BEGIN{s="abc\nxyz"; sub(/c.x/, " ", s); print s}'
[](#cb37-11)ab yz
```

## 量化符

作为类比，或（alternation）提供了逻辑或（OR）。结合点元字符 `.` 和量化符（如果需要还有或）为执行逻辑与（AND）铺了道路。例如，检查字符串是否匹配两个之间带有任意字符的模式。量化符可以应用于字符和分组。除了指定精确数量和边界范围外，它们还可以匹配无边界的变化数量。

首先是 `?` 元字符，它将字符或分组量化为匹配 `0` 次或 `1` 次。这有助于定义可选模式，并在某些情况下与分组相比可以构建出更简洁的模式。

```
[](#cb38-1)$ # 等同于：awk '{gsub(/\<(fe.d|fed)\>/, "X")} 1'
[](#cb38-2)$ echo 'fed fold fe:d feeder' | awk '{gsub(/\<fe.?d\>/, "X")} 1'
[](#cb38-3)X fold X feeder
[](#cb38-4)
[](#cb38-5)$ # 等同于：awk '/<par(|t)>'
[](#cb38-6)$ printf 'sub par\nare\npart' | awk '/<part>/'
[](#cb38-7)sub par
[](#cb38-8)$ # 等同于：awk '{gsub(/part|parrot/, "X")} 1'
[](#cb38-9)$ echo 'par part' | awk '{gsub(/par(ro)?t/, "X")} 1'
[](#cb38-10)par X
[](#cb38-11)$ # 等同于：awk '{gsub(/part|parent/, "X")} 1'
[](#cb38-12)$ echo 'par part' | awk '{gsub(/par(en|ro)?t/, "X")} 1'
[](#cb38-13)par X
[](#cb38-14)$ # 替换
[](#cb38-15)
[](#cb38-16)$ echo 'blah bar' | awk '{gsub(/<?, "<")}'
[](#cb38-19)
```

`*` 元字符将字符或分组量化为匹配 `0` 次或更多。没有上界，细节稍后讨论。

```
[](#cb39-1)$ # 'f' 后跟 0 次或多次 'e'
[](#cb39-2)$ echo 'fd fod:d' | awk '{gsub(/fe*/, "X")} 1'
[](#cb39-3)X fod:d
[](#cb39-4)
[](#cb39-5)$ # 'f' 后跟 0 次或多次 'e'
[](#cb39-6)$ echo '311111111251142' | awk '{gsub(/1*2/, "-")} 1'
```
注：此处为示例。

`+` 元字符将字符或分组量化为匹配 `1` 次或更多。与 `*` 量化符类似，没有上界。

```
[](#cb40-1)$ # 'f' 后跟 1 次或多次 'e'
[](#cb40-2)$ echo 'fd fod:d' | awk '{gsub(/fe+d/, "X")} 1'
[](#cb40-3)X fod:d
[](#cb40-4)$ # 'f' 后跟 1 次或多次 'e' 或 'o' 或 ':' 后跟 'd'
[](#cb40-5)$ echo 'fd fod:d' | awk '{gsub(/f(e|o|)+d/, "X")} 1'
[](#cb40-6)fd X X
[](#cb40-8)$ # 'f' 后跟 1 次或多次 '1' 然后是可选的 '4' 最后是 '2'
[](#cb40-9)$ echo '311111111251142' | awk '{gsub(/1+?2/, "-")} 1'
```

你可以使用 `{}` 元字符指定整数范围，包括有边界和无边界的。使用此量化符有四种方式，如下所示：

| 模式 | 描述 |
| --- | --- |
| `{m,n}` | 匹配 `m` 到 `n` 次 |
| `{m,}` | 至少匹配 `m` 次 |
| `{,n}` | 最多匹配 `n` 次（包括 `0` 次） |
| `{n}` | 精确匹配 `n` 次 |

```
[](#cb41-1)$ # 注意 {} 内部不允许空格
[](#cb41-2)$ echo 'ac abc abbc abbbc abbbbbbc' | awk '{gsub(/ab{1,4}c/, "X")} 1'
[](#cb41-3)ac X X X abbbbbbc
[](#cb41-4)
[](#cb41-5)$ echo 'ac abc abbc abbbc abbbbbbc' | awk '{gsub(/ab{3,,}c/, "X")} 1'
[](#cb41-6)ac abc abbc X X
[](#cb41-7)
[](#cb41-8)$ echo 'ac abc abbc abbbc abbbbbbc' | awk '{gsub(/ab{,2}c/, "X")} 1'
[](#cb41-9)X X X abbbbbbbbc
[](#cb41-10)
[](#cb41-11)$ echo 'ac abc abbc abbbc abbbbbbc' | awk '{gsub(/ab{3}c/, "X")} 1'
[](#cb41-12)ac abc abbc X abbbbbbc
```

> ![info](img/file0.svg) `{}` 元字符必须转义才能匹配其字面量。与 `()` 元字符类似，单独转义 `{` 即可。

接下来是如何使用点元字符和量化符构建条件逻辑与。

```
[](#cb42-1)$ # 匹配 'Error' 后跟零或多个字符，再跟 'valid'
[](#cb42-2)$ echo 'Error: not a valid input' | awk '/Error.*valid/'
[](#cb42-3)Error: not a valid input
```

为了允许任意顺序匹配，你还需要引入或（alternation）。但是，对于超过 3 个模式的情况，组合将变得难以编写和维护。

```
[](#cb43-1)$ # 'cat' 后跟 'dog' 或 'dog' 后跟 'cat'
[](#cb43-2)$ echo 'two cats and a dog' | awk '{gsub(/cat.*dog|dog.*cat/, "pets")} 1'
[](#cb43-3)two pets
[](#cb43-4)$ echo 'two dogs and a cat' | awk '{gsub(/cat.*dog|dog.*cat/, "pets")} 1'
[](#cb43-5)two pets
```

## 最长匹配获胜

你已经看到一个或的示例，当两个备选方案从相同位置开始时，会选择最长的匹配部分。例如 `spar|spared` 将导致选择 `spared` 而不是 `spar`。当从相同起始位置有两个或多个匹配可能时，情况同样适用。例如，如果匹配的字符串是 `foot`，`f.?o` 将匹配 `foo` 而不是 `fo`。





```
[](#cb44-1)$ # 在 'foo' 和 'fo' 之间最长匹配获胜
[](#cb44-2)$ echo 'foot' | awk '{sub(/f.?o/, "X")} 1'
[](#cb44-3)Xt
[](#cb44-4)$ # 这里将匹配所有内容
[](#cb44-5)$ echo 'car bat cod map scat dot abacus' | awk '{sub(/.*/, "X")} 1'
[](#cb44-6)X
[](#cb44-7)
[](#cb44-8)$ # 当 (1|2|3)+ 只匹配到 '1233' 时，会发生最长匹配
[](#cb44-9)$ # 这样 '12baz' 也能匹配
[](#cb44-10)$ echo 'foo123312baz' | awk '{sub(/o(1|2|3)+(12baz)?/, "X")} 1'
[](#cb44-11)foX
[](#cb44-12)$ # 在 'perl' 等其他实现中，情况并非如此
[](#cb44-13)$ # 量化尽可能匹配，但优先级是从左到右
[](#cb44-14)$ echo 'foo123312baz' | perl -pe 's/o(1|2|3)+(12baz)?/X/'
[](#cb44-15)foXbaz
```

在确定最长匹配时，还会考虑整个正则表达式的匹配。这就是 `Error.*valid` 示例能够工作的原理。如果 `.*` 消耗了 `Error` 之后的所有字符，那么就没有更多的字符可以尝试匹配 `valid` 了。因此，在匹配 `.*` 的数量字符中，将选择满足整个正则表达式的最长部分。类似于 `a.*b` 的表达式将从输入字符串中的第一个 `a` 匹配到最后一个 `b`。在其他实现（如 `perl`）中，这是通过一个名为“回溯”（backtracking）的过程实现的。这两种方法各有优劣，并且在某些情况下，正则表达式会导致指数级的时间消耗。

```
[](#cb45-1)$ # 从行首到行末最后一个 'm'
[](#cb45-2)$ echo 'car bat cod map scat dot abacus' | awk '{sub(/.*m/, "-")} 1'
[](#cb45-3)-ap scat dot abacus
[](#cb45-4)
[](#cb45-5)$ # 从行内第一个 'b' 到行末最后一个 't'
[](#cb45-6)$ echo 'car bat cod map scat dot abacus' | awk '{sub(/b.*t/, "-")} 1'
[](#cb45-7)car - abacus
[](#cb45-8)
[](#cb45-9)$ # 从行内第一个 'b' 到行末最后一个 'at'
[](#cb45-10)$ echo 'car bat cod map scat dot abacus' | awk '{sub(/b.*at/, "-")} 1'
[](#cb45-11)car - dot abacus
[](#cb45-12)
[](#cb45-13)$ # 这里 'm*' 将匹配 0 次 'm'，因为这产生了最长匹配
[](#cb45-14)$ echo 'car bat cod map scat dot abacus' | awk '{sub(/a.*m*/, "-")} 1'
[](#cb45-15)c-
```

## 字符类

为了为的字符集创建自定义占位符，可以将它们封装在 `[]` 元字符内部。这类似于在分组内部使用单字符交替，但增加了灵活性和功能。字符类有它们自己的元字符版本，并为常见用例提供了特殊的预定义集合。量化也适用于字符类。

```
[](#cb46-1)$ # 等同于：awk '/cot|cut/' 和 awk '/c(o|u)t/'
[](#cb46-2)$ printf 'cute\ncat\ncot\ncoat\ncost\nscuttle\n' | awk '/c[ou]t/'
[](#cb46-3)cute
[](#cb46-4)cot
[](#cb46-5)scuttle
[](#cb46-6)
[](#cb46-7)$ # 等同于：awk '/.(a|e|o)+t/'
[](#cb46-8)$ printf 'meeting\ncute\nboat\nat\nfoot\n' | awk '/.[aeo]+t/'
[](#cb46-9)meeting
[](#cb46-10)boat
[](#cb46-11)foot
[](#cb46-12)
[](#cb46-13)$ # 等同于：awk '{gsub(/\<(s|o|t)(o|n)\>/, "X")} 1'
[](#cb46-14)$ echo 'no so in to do on' | awk '{gsub(/\<[sot][on]\>/, "X")} 1'
[](#cb46-15)no X in X do X
[](#cb46-16)
[](#cb46-17)$ # 由字母 'o' 和 'n' 组成的字符串，长度至少为 2
[](#cb46-18)$ # /usr/share/dict/words 包含字典单词，每行一个单词
[](#cb46-19)$ awk '/^[on]{2,}$/' /usr/share/dict/words
[](#cb46-20)no
[](#cb46-21)non
[](#cb46-22)noon
[](#cb46-23)on
```

字符类有它们自己的元字符来简洁地定义集合。字符类外的 `^`、`$` 等元字符没有特殊含义，或者在字符类内部的含义完全不同。

首先，`-` 元字符有助于定义字符范围，而不是逐个指定它们。

```
[](#cb47-1)$ # 等同于：awk '{gsub(/[0123456789]+, "-")} 1'
[](#cb47-2)$ echo 'Sample123string42with77numbers' | awk '{gsub(/[0-9]+, "-")} 1'
[](#cb47-3)Sample-string-numbers
[](#cb47-4)$ # 由小写字母和数字组成的单词
[](#cb47-5)$ echo 'coat food12 best' | awk '{gsub(/[a-z0-9]+, "X")} 1'
[](#cb47-6)X
[](#cb47-7)$ # 由小写字母 'p' 到 'z' 组成的单词
[](#cb47-8)$ echo 'road post' | awk '{gsub(/[p-z][a-z]*, "X")} 1'
[](#cb47-9)X
```

字符类也可以用于构建数值范围。然而，很容易漏掉边界情况，且某些范围的设计非常复杂。参见[正则表达式：范围](https://www.regular-expressions.info/ranges.html)。

```
[](#cb48-1)$ # 10 到 29 之间的数字
[](#cb48-2)$ echo '23 54 34' | awk '{gsub(/[12][0-9], "X")} 1'
[](#cb48-3)X
[](#cb48-4)
[](#cb48-5)$ # 带有前零的 >= 100 的数字
[](#cb48-6)$ echo '0501 12 26 9823' | awk '{gsub(/0*[0-9]{3,}, "X")} 1'
[](#cb48-7)X
```

下一个元字符是 `^`，它必须作为第一个字符类指定。它否定该集合，因此除指定的字符以外的所有字符都会匹配。小心处理否定逻辑，可能会得到超出结果。

```
[](#cb49-1)$ # 替换所有非数字
[](#cb49-2)$ echo 'Sample123string42with77numbers' | awk '{gsub(/[⁰-9]+, "-")} 1'
[](#cb49-3)-123-
[](#cb49-4)$ # 根据分隔符删除两列
[](#cb49-5)$ echo 'foo:123:baz' | awk '{sub(/(::){2}$/, "") 1'
[](#cb49-6)foo:123
[](#cb49-7)$ # 被唯一字符围的字符序列
[](#cb49-8)$ echo 'I like "mango" and "guava"' | awk '{gsub(/""]+, "X")} 1'
[](#cb49-9)I like X
[](#cb49-10)$ # 有时正向定义集合比否定更简单
[](#cb49-11)$ # 等同于：awk '/^aeiou]*$/'
[](#cb49-12)$ printf 'try\nfun\ngly\npity\n' | awk '!/[aeiou]/'
[](#cb49-13)try
[](#cb49-14)
```

常用的字符集有预定义的转义序列：

- `\w` 匹配所有`单词`字符 `[a-zA-Z0-9_]`（回顾单词描述）
- `\W` 匹配所有非单词字符（回顾之前的对立性，如 `\y` 和 `\B`）
- `\s` 匹配所有`空白`字符：制表符、换行符、垂直制表符、分页、回车和空格
- `\S` 匹配所有非空白字符

```
[](#cb50-1)$ # 匹配所有非单词字符
[](#cb50-2)$ echo 'load;err_msg--ant,r2..not' | awk '{gsub(/\W+/, "-")} 1'
[](#cb50-3)load-err_msg-ant-r2-not
[](#cb50-4)
[](#cb50-5)$ # 将所有空白序列替换为单个空格
[](#cb50-6)$ printf 'hi  \v\f  there.\thave   \ra nice\t\tday\n' | awk '{gsub(/\s+/, " ")} 1'
[](#cb50-7)hi there. have a nice day
```

这些转义序列*不能*在字符类内部使用。

```
[](#cb51-1)$ # \w 在字符类中将简单匹配 w
[](#cb51-2)$ echo 'w=y\x+3' | awk '{gsub(/[\w=], "") 1'
[](#cb51-3)y\x+3
```

> ![warning](img/file1.svg) `awk` 不支持 `\d` 和 `\D`，这些在其他实现中用作所有数字和非数字的快捷方式。

**命名字符集**由封装在 `[:` 和 `:]` 之间的名称定义，必须在字符类 `[]` 内使用，并根据需要与其他字符一起使用。

| 命名集合 | 描述 |
| --- | --- |
| `[:digit:]` | `[0-9]` |
| `[:lower:]` | `[a-z]` |
| `[:upper:]` | `[A-Z]` |
| `[:alpha:]` | `[a-zA-Z]` |
| `[:alnum:]` | `[0-9a-zA-Z]` |
| `[:xdigit:]` | `[0-9a-fA-F]` |
| `[:cntrl:]` | 控制字符 - 前 32 个 ASCII 字符和第 127 个(DEL) |
| `[:punct:]` | 所有标点符号 |
| `[:graph:]` | `[:alnum:]` 和 `[:punct:]` |
| `[:print:]` | `[:alnum:]`、`[:punct:]` 和空格 |
| `[:blank:]` | 空格和制表符字符 |





| `[:space:]` | 空白字符，等同于 `\s` |

```
[](#cb52-1)$ s='err_msg xerox ant m_2 P2 load1 eel'
[](#cb52-2)$ echo "$s" | awk '{gsub(/\<[[:lower:]]+\>/, "X")} 1'
[](#cb52-3)err_msg X X m_2 P2 load1 X
[](#cb52-4)
[](#cb52-5)$ echo "$s" | awk '{gsub(/\<[[:lower_]+]+\>/, "X")} 1'
[](#cb52-6)X X X m_2 P2 load1 X
[](#cb52-7)
[](#cb52-8)$ echo "$s" | awk '{gsub(/\<[[:alnum:]]+\>/, "X")} 1'
[](#cb52-9)err_msg X X m_2 X X X
[](#cb52-10)
[](#cb52-11)$ echo ',pie tie#ink-eat_42' | awk '{gsub(/[^[:punct:]]+/, "")} 1'
[](#cb52-12),#-_
```

为了字面量匹配字符类元字符，需要特定的放置位置。或者，可以通过在前面加上 `\` 来进行转义，以避免记忆不同的规则。由于 `\` 在字符类内部是特殊字符，请使用 `\\` 来表示其字面量。

```
[](#cb53-1)$ # - 应该是 [] 内的第一个或最后一个字符
[](#cb53-2)$ echo 'ab-cd gh-c 12-423' | awk '{gsub(/[a-z-]{2,}/, "X")} 1'
[](#cb53-3)X X 12-423
[](#cb53-4)$ # 或使用 \ 进行转义
[](#cb53-5)$ echo 'ab-cd gh-c 12-423' | awk '{gsub(/[a-z\-0-9]{2,}/, "X")} 1'
[](#cb53-6)X X X
[](#cb53-7)
[](#cb53-8)$ # ] 应该是 [] 内的第一个字符
[](#cb53-9)$ printf 'int a[5]\nfoo\n1+1=2\n' | awk '/[=]]/'
[](#cb53-10)$ printf 'int a[5]\nfoo\n1+1=2\n' | awk '//=]/'
[](#cb53-11)int a[5]
[](#cb53-12)1+1=2
[](#cb53-13)
[](#cb53-14)$ # 若要匹配 ，可以在字符集中的任何位置使用 [
[$ # [][] 会同时匹配 [ 和 ]
[](#cb53-16)$ printf 'int a[5]\nfoo\n1+1=2\n' | awk '/[][]/'
[](#cb53-17)int a[5]
[](#cb53-18)
[](#cb53-19)$ # ^ 不应该是 [] 内的第一个字符
[](#cb53-20)$ echo 'f*(a^b) - 3*(a+b)/(a-b)' | awk '{gsub(/a[+^]b/, "c")} 1'
[](#cb53-21)f*(c) - 3*(c)/(a-b)
```

> ![warning](img/file1.svg) 像 `[.` 或 `[:` 这样的组合不能共同表示两个独立的字符，因为它们在 `[]` 中有特殊含义。更多详情请参阅 [gawk 手册：Using Bracket Expressions](https://www.gnu.org/software/gawk/manual/gawk.html#Bracket-Expressions)。

```
[](#cb54-1)$ echo 'int a[5]' | awk '/[x[.y]/'
[](#cb54-2)awk: cmd. line:1: error: Unmatched [, [^, [:, [., or [=: /[x[.y]/
[](#cb54-3)$ echo 'int a[5]' | awk '/[x[y.]/'
[](#cb54-4)int a[5]
```

## 转义序列

某些 ASCII 字符如制表符 `\t`、回车 `\r`、换行符 `\n` 等都有表示它们的转义序列。此外，任何字符都可以使用八进制 `\NNN` 或十六进制 `\xNN` 格式的 ASCII 值来表示。与字符类转义序列（如 `\w`）不同，这些可以在字符类内部。

```
[](#cb55-1)$ # 使用 \t 表示制表符字符
[](#cb55-2)$ printf 'foo\tbar\tbaz\n' | awk '{gsub(/\t/, " ")} 1'
[](#cb55-3)foo bar baz
[](#cb55-4)
[](#cb55-5)$ # 这些转义序列在字符类内同样有效
[](#cb55-6)$ printf 'a\t\r\fb\vc\n' | awk '{gsub(/[\t\v\f\r]+/, ":")} 1'
[](#cb55-7)a:b:c
[](#cb55-8)
[](#cb55-9)$ # 表示单引号
[](#cb55-10)$ # 使用 \047 八进制格式
[](#cb55-11)$ echo "universe: '42'" | awk '{gsub(/\x27/, "")} 1'
[](#cb55-12)universe: 42
```

> ![info](img/file0.svg) 如果通过 ASCII 值指定元字符，仍视为元字符。未定义的序列将导致警告。

```
[](#cb56-1)$ # \x5e 是 ^ 字符，作为字符串锚点
[](#cb56-2)$ printf 'cute\ncot\cat\n' | awk '/\xeco/'
[](#cb56-3)cot
[](#cb56-4)coat
[](#cb56-5)$ # & 代表整个匹配部分
[](#cb56-7)$ echo 'hello world' | awk '{sub(*/, "[&]")} 1'
[](#cb56-8)hello world
[](#cb56-9)$ # \x26 是 & 字符
[](#cb56-10)$ echo 'hello world' | awk '{sub(*/, "\x26]")} 1'
[](#cb56-11)hello world
[](#cb56-12)$ echo 'read' | awk '{sub(/a/, ".")} 1'
[](#cb56-13)awk: line:1: escape sequence `.` 被视为普通字符
[](#cb56-14)re.d
```

> ![info](img/file0.svg) 参阅 [gawk 手册：Escape Sequences](https://www.gnu.org/software/gawk/manual/html#Escape-Sequences)。

## 替换特定次数

替换函数 `gensub`，可以替代 `sub` 和 `gsub`。在语法上，`gensub` 需要三个参数。第三个参数用于指定是替换所有出现还是通过数字指定特定次数。另一个区别是 `gensub` 返回一个字符串值，而不是修改输入。

```
[](#cb57-1)$ # 等于 sed 's/:/-/'
[](#cb57-2)$ # 仅替换第二个 ':' 为 '-'
[](#cb57-3)$ # 注意 gensub 的输出在这里被传递
[](#cb57-4)$ echo 'foo:123:bar:baz' | awk '{print gensub(/:/, "-", 2)}'
[](#cb57-5)foo:123-baz
[](#cb57-6)$ # 等于 sed -E 's/[^:]+/X/3'
[](#cb57-8)$ # 仅替换第三字段为 'X'
[](#cb57-9)$ echo 'foo:123:bar:baz' | awk '{print gensub(/[^:]/, "X", 3)}'
10)foo:123:X:baz
```

`gensub` 函数的第四个参数允许你指定执行替换的输入字符串或变量。默认值为 `$0`，如之前的示例所示。

```
[](#cb58-1)$ # 仅针对第四字段替换元音为 'X'
[](#cb58-2)$ # 等于 awk '{gsub(/[aeiou]/, "X", $4)}'
[](#cb58-3)$ echo '1 good 2 apples' | awk '{$4 = gensub(/[aeiou]/, "X", "g", $4)} 1'
4)1 good 2 Xs
```

## 反引用

分组元字符 `()` 也称为捕获组。它们像变量一样，`()` 捕获的字符串可以通过反引用 `\N` ，其中 `N` 是你想要的捕获组。正则表达式中最左边的 `(` 是 `\1`，下一个是 `\2`，依此类直到 `\9`。作为特殊情况，由于 `\` 在引号内是特殊字符，你必须使用 `"\\1"` 来表示 `\1`。

> ![info](img/file0.svg) `\N` 形式的反引用只能用于 `gensub` 函数。`&` 可以用于 `sub`、`gsub` 和 `gensub` 函数。

```
[](#cb59-1)$ # 将 \\ 减少为单个 \，如果它是单个 \
[](#cb59-2)$ s='\[\] and \\w and \[a-zA-Z0-9\_\]'
[](#cb59-3)$ echo "$s" | awk '{print gensub(/(\\?)\/, "\\1", "g")}'
[](#cb59-4)[] and \w and [a-zA-Z0-9_]
[](#cb59-5)
[](#cb59-6)$ # 将第一列的值复制为最后一列
[](#cb59-7)$ echo 'one,2,3.14,42' | awk '{print gensub(/^,]+).*/ "\\1", 1)}'
8)one,2,3.14,42
[](#cb59-9)
[](#cb59-10)$ # 在字符串开头和结尾添加内容
[](#cb59-11)$ # 因为使用了 '&'，不需要 gensub
[](#cb59-12)$ echo 'hello world' | awk '{sub(*/, "Hi. &. Have a day")} 1'
13)Hi. hello world. Have a day
[](#cb59-14)
[](#cb59-15)$ # 这里 {N} 指的是最后一个但第 N 个出现
[](#cb59-16)$ s='456:foo:123:bar:789:baz'
[](#cb59-17)$ echo "$s" | awk '{print gensub(/(.*):((.*:){2})/, "\\1[]\\2", 1)}'
18)456:foo:123[]bar:789:baz
```

> ![warning](img/file1.svg) 参阅 [unix.stackexchange: 为什么这个 sed 命令没有替换倒数三个 "and"?](https://unix.stackexchange.com/q/579889/109046) 关于在 `(){N})` 通用情况下使用单词边界的错误。

> ![warning](img/file1.svg) 与 `grep` 或 `sed` 或 `perl` 等其他正则表达式实现不同，反引用不能用于 awk 的搜索部分。另参阅 [unix.stackexchange: backreference in awk](https://unix.stackexchange.com/q/361427/109046)。

如果量词应用于在 `()` 元字符内部分组的模式，你需要一个外部 `()` 组来捕获匹配部分。某些正则表达式引擎提供了非捕获组来处理此类情况。在 `awk` 中，你必须绕过额外的捕获组。





```
[](#cb60-1)$ # 注意替换部分中使用的数字
[](#cb60-2)$ s='one,2,3.14,42'
[](#cb60-3)$ echo "$s" | awk '{$0=gensub(/^(([^,]+,){2})([^,]+)/, "\\1", 1)} 1'
[](#cb60-4)one,2,,42
```

这是一个当匹配部分的长度相同时，交替顺序变得重要的示例。目标是删除所有单词，除非它们以 `g` 或 `p` 开头且包含 `y`。

```
[](#cb61-1)$ s='tryst,fun,glyph,pity,why,group'
[](#cb61-2)
[](#cb61-3)$ # 因为 \w+ 在这里优先级更高，所有单词都会被删除
[](#cb61-4)$ echo "$s" | awk '{print gensub(/\<\w+\>|(\<[gp]\w*y\w*\>)/, "\\1", "g")}'
[](#cb61-5),,,,,
[](#cb61-6)
[](#cb61-7)$ # 这里捕获组的优先级更高，因此匹配组的单词会被保留
[](#cb61-8)$ echo "$s" | awk '{print gensub(/(\<[gp]\w*y\w*\>)|\<\w+\>/, "\\1", "g")}'
[](#cb61-9),,glyph,pity,,
```

由于 `\` 和 `&` 在替换部分的双引号内是特殊字符，请分别使用 `\\` 和 `\\&` 来进行字面表示。

```
[](#cb62-1)$ echo 'foo and bar' | awk '{sub(/and/, "[&]")} 1'
[](#cb62-2)foo [and] bar
[](#cb62-3)$ echo 'foo and bar' | awk '{sub(/and/, "[\\&]")} 1'
[](#cb62-4)foo [&] bar
[](#cb62-5)
[](#cb62-6)$ echo 'foo and bar' | awk '{sub(/and/, "\\")} 1'
[](#cb62-7)foo \ bar
```

## 不区分大小写的匹配

与 `sed` 或 `perl` 不同，`awk` 中的正则表达式并不支持使用标志（flags）来改变某些行为。例如，没有标志可以强制正则表达式在匹配时忽略大小写。

特殊变量 `IGNORECASE` 用于控制大小写敏感性，默认值为 `0`。通过将其更改为其他值（在条件表达式中表示 `true`），你可以进行不区分大小写的匹配。`-v` 命令行选项允许你在读取输入之前分配变量。`BEGIN` 块也经常用于更改此类设置。

```
[](#cb63-1)$ printf 'Cat\ncOnCaT\nscatter\ncot\n' | awk -v IGNORECASE=1 '/cat/'
[](#cb63-2)Cat
[](#cb63-3)cOnCaT
[](#cb63-4)scatter
[](#cb63-5)
[](#cb63-6)$ # 对于足够小的字符串，也可以使用字符类
[](#cb63-7)$ printf 'Cat\ncOnCaT\nscatter\ncot\n' | awk '{gsub(/[cC][aA][tT]/, "dog")} 1'
[](#cb63-8)dog
[](#cb63-9)cOndog
[](#cb63-10)sdogter
[](#cb63-11)cot
```

另一种方法是使用内置字符串函数 `tolower` 先将输入转换为小小写。

```
[](#cb64-1)$ printf 'Cat\ncOnCaT\nscatter\ncot\n' | awk 'tolower($0) ~ /cat/'
[](#cb64-2)Cat
[](#cb64-3)cOnCaT
[](#cb64-4)scatter
```

## 动态正则表达式

如之前所示，你可以使用字符串字面量而不是正则表达式来指定要匹配的模式。这意味着你可以使用任何表达式或变量。如果你需要根据某些条件计算正则表达式，或者从外部获取模式（例如用户输入），这种方法非常有帮助。

`-v` 命令行选项对于获取用户输入非常方便，例如从 `bash` 变量获取。

```
[](#cb65-1)$ r='cat.*dog|dog.*cat'
[](#cb65-2)$ echo 'two cats and a dog' | awk -v ip="$r" '{gsub(ip, "pets")} 1'
[](#cb65-3)two pets
[](#cb65-4)
[](#cb65-5)$ awk -v s='ow' '$0 ~ s' table.txt
[](#cb65-6)brown bread mat hair 42
[](#cb65-7)yellow banana window shoes 3.14
[](#cb65-8)
[](#cb65-9)$ # 你必须确保使用 \\ 而不是 \
[](#cb65-10)$ r='\\<[12][0-9]\\>'
[](#cb65-11)$ echo '23 154 12 26 34' | awk -v ip="$r" '{gsub(ip, "X")} 1'
[](#cb65-12)X 154 34
```

> ![info](img/file0.svg) 查看 使用 shell 变量 以避免使用 `\`。

有时你需要获取输入并将其视为字面量而不是正则表达式。在这种情况下，你需要在使用替换之前转义元字符。对于替换部分，只需要转义 `\` 和 `&` 字符。

```
[](#cb66-1)$ awk -v s='(a.b)' '{BEGIN{gsub(//, "\\&", s); print s}'
[](#cb66-2)a.b
[](#cb66-3)
[](#cb66-4)$ echo 'f*(a^b)' | awk -v s='(a^b)' '{gsub(//, "\\&", s); gsub(s, "c")} 1'
[](#cb66-5)fc
[](#cb66-6)fc
[](#cb66-7)$ # 字面匹配给定输入，但仅位于字符串结尾
```

> ![info](img/file0.svg) 如果你需要匹配而不是替换，可以使用 `index` 函数。查看 index。

## 总结

正则表达式是你会在命令行和编程语言中遇到的特性。它是一个多功能强大的文本处理工具。虽然 `awk` 中的功能与编程语言中的要少少，但对于你需要的命令行用法已经足够了。掌握正则表达式的语法和功能需要大量时间，因此我鼓励你多加练习。由于其灵活性，也可以将其视为一种微型编程语言。

## 练习

a)** 对于给输入，打印所有以 `den` 开头或 `ly` 结尾的行。

```
[](#cb67-1)$ lines='lovely\ndent\nlonely\nfly away\nent\n'
[](#cb67-2)$ printf '%b' "$lines" | awk ##### add your solution
[](#cb67-3)lovely
[](#cb67-4) lonely
[](#cb67-5)dent
```

b)** 替换所有的 `word`，除非它位于单词边界。注意这些练习中的 `word` 与正则表达式中定义的含义相同。

```
[](#cb68-1)$ echo 'hiword niceword1 bad cool_worda' | awk ##### add your solution
[](#cb68-2)hi nice1 bad cool_worda
```

c)** 在以 `s` 开头并任意顺序包含 `e` 和 `t` 的单词周围添加 `[]`。

```
[](#cb69-1)$ words='sequoia subtle tests site'
[](#cb69-2)$ echo "$words" | awk ##### add your solution
[](#cb69-3)sequoia [subtle] exhibit [sets] [site]
```

d)** 将以 `a` 或 `r` 结尾的单词后的空格字符替换为换行符。

```
[](#cb70-1)$ echo 'area not a _a roar 22' | awk ##### add your solution
[](#cb70-2)area
[](#cb70-3)not a
[](#cb70-4)_a roar
[](#cb70-5)took 22
```

e)** 对于给定的输入，将所有的 `[4]*` 替换为 `2`。

```
[](#cb71-1)$ echo '2.3/[4]*6 5.3-[4]*9' | awk ##### add your solution
[](#cb71-2)2.3/26 foo 5.3-29
```

f)** `awk '/\<a-z[a-z]\>'` 等于 `awk '/\<[a-z][on]{2}[a-z]\>'`。真还是假？下面的示例输入可能有助于理解差异（如果有的话）。

```
[](#cb72-1)$ printf 'known\nmood\nknow\npony\ninns\n'
[](#cb72-2)known
[](#cb72-3)mood
[](#cb72-4)know
[](#cb72-5)pony
[](#cb72-6)inns
```

g)** 打印所有以 `hand` 开头并以 `s`、`y`、`le` 或没有后续字符结尾的行。例如，`handed` 虽然以 `hand` 开头但不应该打印。

```
[](#cb73-1)$ lines='handed\nhand\nhandy\nunhand\nhands\nhand\n'
[](#cbcb73-2)$ printf '%b' "$lines" | awk ##### add your solution
[](#cb73-3)hand
[](#cb73-4)handy
[](#cb73-5)hands
[](#cb73-6)handle
```

h)** 对于给定的输入，将 `42//5` 或 `42/5` 替换为 `8`。

```
[](#cb74-1)$ echo 'a+42//5-c pressure*3+42/5-14256' | awk ##### add your solution
[](#cb74-2)a+8-c pressure*3+8-14256
```

i)** 对于给定的量词，使用 `{m,n}` 表示的等效形式是什么？

*   `?` 等于

*   `*` 等于

*   `+` 等于

j)** 真还是假？`(a*|b*)` 等于 `(a|b)*`。

k)** 对于给定的输入，构造两个不同的正则表达式以获得所示的输出。





```
[](#cb75-1)$ # delete from '(' till next ')'
[](#cb75-2)$ echo 'a/b(division) + c%d() - (a#(b)2(' | awk ##### add your solution here
[](#cb75-3)a/b + c%d - 2(
[](#cb75-4)
[](#cb75-5)$ # delete from '(' till next ')' but not if there is '(' in between
[](#cb75-6)$ echo 'a/b(division) + c%d() - (a#(b)2(' | awk ##### add your solution here
[](#cb75-7)a/b + c%d - (a#2(
```

l) 对于输入文件 `anchors.txt`，将 `markdown` 锚点转换为对应的 `hyperlinks`。

```
[](#cb76-1)$ cat anchors.txt
[](#cb76-2)# <a name="regular-expressions"></a>Regular Expressions
[](#cb76-3)## <a name="subexpression-calls"></a>Subexpression calls
[](#cb76-4)
[](#cb76-5)$ awk ##### add your solution here
[](#cb76-6)Regular Expressions
[](#cb76-7)Subexpression calls
```

m) 显示满足以下 `both` 条件的所有行：

* `professor` 不区分大小写匹配
* `quip` 或 `this` 区分大小写匹配

输入是一个从互联网下载的文件，如下所示。

```
[](#cb77-1)$ wget https://www.gutenberg.org/files/345/345.txt -O dracula.txt
[](#cb77-2)
[](#cb77-3)$ awk ##### add your solution here
[](#cb77-4)equipment of a professor of the healing craft. When we were shown in,
[](#cb77-5)should be. I could see that the Professor had carried out in this room,
[](#cb77-6)"Not up to this moment, Professor," she said impulsively, "but up to
[](#cb77-7)and sprang at us. But by this time the Professor had gained his feet,
[](#cb77-8)this time the Professor had to ask her questions, and to ask them pretty
```

n) 给定的字符串字段由 `,` 分隔，且字段值不为空。将第三字段替换为 `42`。

```
[](#cb78-1)$ echo 'lion,ant,road,neon' | awk ##### add your solution here
[](#cb78-2)lion,ant,42,neon
[](#cb78-3)
[](#cb78-4)$ echo '_;3%,.,=-=,:' | awk ##### add your solution here
[](#cb78-5)_;3%,.,42,:
```

o) 对于给定字符串，将倒数第三个 `so` 替换为 `X`。只打印被替换改变的行。

```
[](#cb79-1)$ printf 'so and so also sow and soup' | awk ##### add your solution here
[](#cb79-2)so and X also sow and soup
[](#cb79-3
[](#cb79-4)$ printf 'sososososososo\nso and so\n' | awk ##### add your solution here
[](#cb79-5)sososoXsososo
```

p) 将所有完整单词用 `()` 包围。此外，如果完整单词是 `imp` 或 `ant`，则删除它们。你能用一次替换完成吗？

```
[](#cb80-1)$ words='tiger imp goat eagle ant important'
[](#cb80-2)$ echo "$words" | awk ##### add your solution here
[](#cb80-3)(tiger) () (goat) (eagle) () (important)
```

# 字段分隔符

现在你已经熟悉了 `awk` 语法和正则表达式，本章将深入探讨字段处理。你将学习如何设置输入输出字段分隔符、如何使用正则表达式定义字段以及如何处理固定长度字段。

## 默认字段分隔

如之前所示，`awk` 自动将输入拆分为字段，可以使用 `$N` 访问，其中 `N` 是所需的字段编号。你也可以传递表达式而不是数字字面量来指定所需的字段。

```
[](#cb81-1)$ cat table.txt
[](#cb81-2)brown bread mat hair 42
[](#cb81-3)blue cake mug shirt -7
[](#cb81-4)yellow banana window shoes 3.14
[](#cb81-5)
[](#cb81-6)$ # 如果第一个字段以 'b' 开头，则打印第四字段
[](#cb81-7)$ awk '$1 ~ /^b/{print $4}' table.txt
[](#cb81-8)hair
[](#cb81-9)shirt
[](#cb81-10)$ # 打印存储在变量 'f' 中的字段
[](#cb81-11)$ awk -v f=3 '{print $f}'
[](#cb81-12)mat
[](#cb81-13)mug
[](#cb81-14)window
```

`NF` 特殊变量将给出一个每行的字段数。当你不知道输入中有多少字段且需要从末尾指定字段编号时，这非常有用。

```
[](#cb82-1)$ # 打印每行的最后一个字段
[](#cb82-2)$ awk '{print $NF}' table.txt
[](#cb82-3)42
[](#cb82-4)-7
[](#cb82-5)3.14
[](#cb82-6)$ # 打印倒数第二个字段
[](#cb82-7)$ awk '{print $NF-1}' table.txt
[](#cb82-8)hair
[](#cb82-9)shoes
[](#cb82-10)$ # 别忘记括号！
[](#cb82-11)$ awk '{print $NF-1}'
[](#cb82-12)14
```

默认情况下，`awk` 不仅按空格拆分输入，还会根据一个或多个空格、制表符或换行符进行拆分。此外，输入开头或结尾的这三种字符会被修剪，不作为内容的一部分。包含换行符的输入将包含在记录分隔符中。

```
[](#cb83-1)$ echo 'a   b   c' | awk '{print NF}'
[](#cb83-2)3
[](#cb83-3)$ # 注意领先空格不是字段内容
[](#cb83-4)$ echo 'a   b   c' | awk '{print $1}'
[](#cb83-5)a
[](#cb83-6)$ # 注意尾随空格不是字段内容
[](#cb83-7)$ echo 'a   b   c' | awk '{print $NF}'
[](#cb83-8)c.
[](#cb83-9)$ # 这里包含制表符的另一个示例
[](#cb83-10)$ printf 'one \t two\tthree' | awk '{print NF}'
[](#cb83-11)3
[](#cb83-12)$ printf 'one \t\tthree' | awk '{print $2}'
[](#cb83-13)two.
```

> ![warning](img/file.svg) 当传递表达式作为字段时，浮点结果是可以接受的。小数部分会被忽略。然而，由于精度限制，可能会导致舍入。

```
[](#cb84-1)$ awk 'BEGIN{printf "%.16f\n", 2.999999999999999}'
[](#cb84-2)2.9999999999999991
[](#cb84-3)$ awk 'BEGIN{printf "%.16f\n", 2.999999999999999}'
[](#cb84-4)3.0000000000000000
[](#cb84-5)
[](#cb84-6)$ # 相当于：awk '{print $2}' table.txt
[](#cb84-7)$ awk '{print $2.999999999999999}' table.txt
[](#cb84-8)bread
[](#cb84-9)cake
[](#cb84-10)banana
[](#cb84-11)$ # 相当于：awk '{print $3}' table.txt
[](#cb84-12)$ awk '{print $2.999999999999999}' table.txt
[](#cb84-13)mat
[](#cb84-14)mug
[](#cb84-15)window

## 输入字段分隔符

更改默认字段分隔符常用的方法是使用 `-F` 命令行选项。传递给选项的值将被视为字符串字面量，然后转换为正则表达式。这里是一些没有任何特殊正则表达式的示例。

```
[](#cb85-1)$ # 使用 ':' 作为输入字段分隔符
[](#cb85-2)$ echo 'goal:amazing:whistle:kwality' | awk -F: '{print $1}'
[](#cb85-3)goal
[](#cb85-4)$ echo 'goal:amazing:whistle:kwality' | awk -F: '{print $NF}'
[](#cb85-5)kwality
[](#cb85-6)
[](#cb85-7)$ # 使用引号避免与 shell 特殊字符冲突
[](#cb85-8)$ echo 'one;two;three;four' | awk -F';' '{print $3}'
[](#cb85-9)three
[](#cb85-10)
[](#cb85-11)$ # 第一个和最后一个字段将为空字符串
[](#cb85-12)$ echo '=a=b=c=' | awk -F= '{print $1 "[" $NF ""]}'
[](#cb85-13)[]
```

你也可以直接设置特殊变量 `FS` 来更改输入字段分隔符。这可以通过命令行使用 `-v` 选项，或在代码块内完成。

```
[](#cb86-1)$ echo 'goal:amazing:whistle:kwality' | awk -v FS=: '{print $2}'
[](#cb86-2)amazing
[](#cb86-3)
[](#cb86-4)$ # 字段分隔符也可以是多个字符
[](#cb86-5)$ echo '1e4SPT2k6SPT3a5SPT4z0' | awk 'BEGIN{FS="SPT"} {print $3}'
[](#cb86-6)3a5
```

如果你希望将输入拆分为单个字符，请使用空字符串作为字段分隔符。

```
[](#cb87-1)$ # 注意 -F 和 '' 之间的空格是强制的
[](#cb87-2)$ echo 'apple' | awk -F '' '{print $1}'
[](#cb87-3)a
[](#cb87-4)$ echo 'apple' | awk -v FS= '{print $NF}'
[](#cb87-5)e
[](#cb87-6)
[](#cb87-7)$ # 根据区域设置，你也可以处理多字节字符
[](#cb87-8)$ echo 'αλεπού' | awk -v FS= '{print $3}'
[](#cb87-9)ε
```





这里是一些使用基于正则表达式的字段分隔符的示例。传递给 `-F` 或 `FS` 的值被视为字符串，然后转换为正则表达式。因此，你需要使用 `\\` 而不是 `\` 来表示反斜符字符。好消息是，对于同时也是正则表达式元字符的单字符，它们将作为字面字符处理，你不需要对它们进行转义。

```
[](#cb88-1)$ echo 'Sample123string42with777numbers' | awk -F'[0-9]+' '{print $2}'
[](#cb88-2)string
[](#cb88-3)$ echo 'Sample123string42with777numbers' | awk -F'[a-zA-Z]+' '{print $2}'
[](#cb88-4)123
[](#cb88-5)
[](#cb88-6)$ # 注意这里使用 \\W 来表示 \W
[](#cb88-7)$ echo 'load;err_msg--\ant,r2..not' | awk -F'\\W+' '{print $3}'
[](#cb88-8)ant
[](#cb88-9)
[](#cb88-10)$ # 等于：awk -F'\\.' '{print $2}'
[](#cb88-11)$ echo 'hi.bye.hello' | awk -F. '{print $2}'
[](#cb88-12)bye
[](#cb88-13)
[](#cb88-14)$ # 统计每行输入的元音数量
[](#cb88-15)$ printf 'cool\nnice car\n' | awk -F'[aeiou]' '{print NF-1}'
[](#cb88-16)2
[](#cb88-17)3
```

> ![warning](img/file1.svg) `FS` 的默认值是单个空格字符。因此，如果你将输入字段分隔符设置为单个空格，那么它将与你在上一节中讨论默认拆分方式相同。如果你想覆盖这一行为，可以在字符类内部使用空格。

```
[](#cb89-1)$ # 等于：awk '{print NF}'
[](#cb89-2)$ echo '   a   b   c   ' | awk -F' ' '{print NF}'
[](#cb89-3)3
[](#cb89-4)$ # 这里有 12 个空格字符，因此有 13 个字段
[](#cb89-5)$ echo '   a   b   c   ' | awk -F'[ ]' '{print NF}'
[](#cb89-6)13
```

> ![warning](img/file1.svg) 如果设置了 `IGNORECASE`，它也会影响字段分割。但字段分隔符为单个字符的情况除外，可以使用字符类来规避此问题。

```
[](#cb90-1)$ echo 'RECONSTRUCTED' | awk -F'[aeiou]+' -v IGNORECASE=1 '{print $1}'
[](#cb90-2)R
[](#cb90-3)
[](#cb90-4)$ # 当 FS 为单个字符时
[](#cb90-5)$ echo 'RECONSTRUCTED' | awk -F'e' -v IGNORECASE=1 '{print $1}'
[](#cb90-6)RECONSTRUCTED
[](#cb90-7)$ echo 'RECONSTRUCTED' | awk -F'[e]' -v IGNORECASE=1 '{print $1}'
[](#cb90-8)R
```

## 输出字段分隔符

`OFS` 特殊变量控制输出字段分隔符。`OFS` 用于传递给 `print` 函数的多个参数之间的字符串。当由于更改字段内容而需要重构 `$0` 时，也会使用它。`OFS` 的默认值是单个空格字符，就像 `FS` 一样。不过没有命令行选项，你必须直接修改 `OFS`。

```
[](#cb91-1)$ # 打印第一和第三字段，OFS 用于连接这些值
[](#cb91-2)$ # 注意使用逗号来分隔 print 参数
[](#cb91-3)$ awk '{print $1, $3}' table.txt
[](#cb91-4)brown mat
[](#cb91-5)blue mug
[](#cb91-6)yellow window
[](#cb91-7)
[](#cb91-8)$ # 相同的 FS 和 OFS
[](#cb91-9)$ echo 'goal:amazing:whistle:kwality' | awk -F: -v OFS=: '{print $2, $NF}'
[](#cb91-10)amazing:kwality
[](#cb91-11)$ echo 'goal:amazing:whistle:kwality' | awk 'BEGIN{FS=OFS=":"} {print $2, $NF}'
[](#cb91-12)amazing:kwality
[](#cb91-13)
[](#cb91-14)$ # FS 和 OFS 的值不同
[](#cb91-15)$ echo 'goal:amazing:whistle:kwality' | awk -F: -v OFS=- '{print $2, $NF}'
[](#cb91-16)amazing-kwality
```

这里是更改字段内容后打印 `$0` 的示例。

```
[](#cb92-1)$ echo 'goal:amazing:whistle:kwality' | awk -F: -v OFS=: '{$2 = 42}'
[](#cb92-2)goal:42:whistle:kwality
[](#cb92-3)$ echo 'goal:amazing:whistle:kwality' | awk -F: -v OFS=, '{$2 = 42}'
[](#cb92-4)goal,42,whistle,kwality
[](#cb92-5)
[](#cb92-6)$ # 记得开头/结尾的空格在默认 FS 下会被修剪
[](#cb92-7)$ echo '   a   b   c   ' | awk '{$NF = "last"}'
[](#cb92-8)a last
```

有时你想用新的 `OFS` 打印 `$0` 的内容，但并不想更改字段内容。在这种情况下，你可以将字段值赋值给自己，以强制重构 `$0`。

```
[](#cb93-1)$ # 没有变化，因为没有触发重构
[](#cb93-2)$ echo 'Sample123string42with777numbers' | awk -F'[0-9]+' -v OFS=, '{$1}'
[](#cb93-3)string
[](#cb93-4)$ # 将字段赋值给自身
[](#cb93-5)$ echo 'Sample123string42with777numbers' | awk -F'[0-9]+' -v OFS=, '{$1=$1}'
[](#cb93-6)string42with777numbers
```

## 操作 NF

`NF` 值也会重构 `$0`。

```
[](#cb94-1)$ # 减少字段
[](#cb94-2)$ echo 'goal:amazing:whistle:kwality' | awk -F: -v OFS=: '{NF--}'
[](#cb94-3)goal:amazing
[](#cb94-4)$ # 增加字段
[](#cb94-5)$ echo echo 'goal:amazing:whistle:kwality' | awk -F: -v OFS=: '{NF++}'
[](#cb94-6)goal:amazing:whistle:kwality:
```

`FS` 允许定义输入分隔符。相比之下，`FPAT`（字段模式）允许定义字段由什么组成。

```
[](#cb95-1)$ s='Sample123string42with777numbers'
[](#cb95-2)$ # 定义连续数字为字段
[](#cb95-3)$ echo "$s" | awk -v FPAT='[0-9]+' '{print $1}'
[](#cb95-4)2
[](#cb95-5)$ # 定义连续字母为字段
[](#cb95-6)$ echo "$s" | awk -v FPAT='[a-zA-Z]+' -v OFS=, '{$1}'
[](#cb95-7)string
```

`FPAT` 通常用于包含分隔符字符的 `csv` 输入。例如，当字段包含嵌入的逗号时。

```
[](#cb96-1)$ s='eagle,"42",frog'
[](#cb96-2)$ # 仅使用逗号作为分隔符是不够的
[](#cb96-3)$ echo "$s" | awk -F, '{print $2}'
[](#cb96-4)"42
```

对于这种简单的 `csv` 输入，`FPAT` 帮助定义以双引号开头结尾或包含非逗号字符的字段。

```
[](#cb97-1)$ s='eagle,,frog'
[](#cb97-2)$ # 使用 * 代替 + 以允许空字段
[](#cb97-3)$ echo "$s" | awk -v FPAT='"[^"]*"|[^,]*' '{print $2}'
[](#cb97-4),
```

> ![warning](img/file1.svg) 以上方法并不适用于所有的 `csv` 文件，例如当字段包含转义引号、换行符等时。此类情况请参考 [stackoverflow: 如何使用 awk 高效地解析 CSV?](https://stackoverflow.com/q/4542053/408252)。你也可以使用 Perl、Python、Ruby 等语言，它们自带标准的 `csv` 解析库，或者可以轻松访问第三方解决方案。还有专门的命令行工具，如 [xsv](https://github.com/BurntSushi/xsv)。

> ![info](img/file1.svg) 如果设置了 `IGNORECASE`，它会影响字段匹配。与 `FS` 不同，单字符模式没有不同的行为。

```
[](#cb98-1)$ # 统计输入字符串中 'e' 的数量
[](#cb98-2)$ echo 'Read Eat Sleep' | awk -v FPAT='e' '{print NF}'
[](#cb98-3)3
[](#cb98-4)$ echo 'Read Eat Sleep' | awk -v IGNORECASE=1 -v FPAT='e' '{print NF}'
[](#cb98-5)4
[](#cb98-6)$ echo 'Read Eat Sleep' | awk -v IGNORECASE=1 -v FPAT='[e]' '{print NF}'
[](#cb98-7)4
```

## FIELDWIDTHS

`FIELDWIDTHS` 是另一个允许定义字段内容的特性。正如名称所示，你必须指定每个字段的字符数。这种方法适用于处理固定宽文件输入，特别是当它们可能包含空字段时。





```
$ cat items.txt
apple   fig banana
50      10  200

# 这里分配了字段宽度，
# 额外的空格被放置在每个字段的末尾
awk -v FIELDWIDTHS='8 4 6' '{print $2}' items.txt
fig 
10 
# 注意字段内容也将包含空格
awk -v FIELDWIDTHS='8 4 6' '{print "[" $2 "]"}' items.txt
[fig ]
[10  ]
```

你可以选择性地在字段宽度前加上一个数字，表示要忽略的字符数。

```
# 第一个字段是 5 个字符
# 然后忽略前 3 个字符，第二个字段留 3 个字符
# 然后忽略 1 个字符，第三个字段留 6 个字符
awk -v FIELDWIDTHS='5 3:3 1:6' '{print "[" $1 "]"}' items.txt
[apple]
[50   ]
awk -v FIELDWIDTHS='5 3:3 1:6' '{print "[" $2 "]"}' items.txt
[fig]
[10 ]
```

如果输入行的长度超过了指定的总宽度，多出的字符将被直接忽略。如果你想访问这些字符，可以使用 `*` 来表示最后一个字段。请参阅 [gawk 手册：FIELDWIDTHS](https://www.gnu.org/software/gawk/manual/gawk.html#Fields-with-fixed-data) 以了解更多特殊边界情况。

```
awk -v FIELDWIDTHS='5 *' '{print "[" $1 "]"}' items.txt
[apple]
[50   ]

awk -v FIELDWIDTHS='5 *' '{print "[" $2 "]"}' items.txt
[   fig banana]
[   10  200]
```

## 总结

字段字段操作是 `awk` 最受欢迎的功能。本章讨论了将输入拆分为字段并对其处理的各种方法。在接后的章节中，还将讨论更多关于字段的示例。我强烈建议也阅读 [gawk 手册：Fields](https://www.gnu.org/software/gawk/manual/gawk.html#Fields) 以获取更多关于字段处理的详细信息。

下一章将讨论使用记录分隔符和相关特殊变量各种方法。

## 练习

**a)** 从每行输入中仅提取 `()` 或 `)(` 之间的内容。假设 `()` 字符每行只出现一次。

```
$ cat brackets.txt
foo blah blah(ice) 123xyz$
(almond-pista) choco
yo )yoyo( yo

$ awk ##### 在此处添加你的解决方案
ice
almond-pista
yoyo
```

**b)** 对于输入文件 `scores.csv`，按所示格式提取 `Name` 和 `Physics` 字段。

```
$ cat scores.csv
Name,Maths,Physics,Chemistry
Blue,67,46,99
Lin,78,83,80
Er,56,79,92
Cy,97,98,95
Ort,68,72,66
Ith,100,100,100

$ awk ##### 在此处添加你的解决方案
Name:Physics
Blue:46
Lin:83
Er:79
Cy:98
Ort:72
Ith:100
```

**c)** 对于输入文件 `scores.csv`，显示数学科目得分高于 `70` 的人员姓名。

```
$ awk ##### 在此处添加你的解决方案
Lin
Cy
Ith
```

**d)** 显示给定输入中单词字符的数量。这里的单词定义与正则表达式相同。你能构造一个使用 `gsub` 的解决方案，以及一个不使用替换替换的解决方案吗？

```
$ echo 'hi there' | awk ##### 在此处添加你的解决方案
7
$ echo 'u-no;co_12:as' | awk ##### 在此处添加你的解决方案
12
```

**e)** 构造一个同时适用于给定输入和相应输出的解决方案。解决方案不应使用替换函数或字符串拼接。

```
$ echo '1 grape" and "mango" and "guava"' | awk ##### 在此处添加你的解决方案
"grape","guava"
$ echo 'a 1""c-2""d') | awk ##### 在此处添加你的解决方案
"a 1","c-2"
```

**f)** 构造一个同时适用于给定输入和相应输出的解决方案。解决方案不应使用替换函数。你能在不显式使用 `print` 的情况下完成吗？

```
$ echo 'hi,bye,there,was,to' | awk ##### 在此处添加你的解决方案
hi,bye,to
$ echo '1,2,3,4,5' | awk ##### 在此处添加你的解决方案
1,2,5
```

**g)** 转换给输入文件 `fw.txt` 以得到所示输出。如果字段为空（即只包含空格字符），则将其替换为 `NA`。

```
$ cat fw.txt
1.3  rs   90  0.134563
3.8           6
5.2  ye       8.2387
4.2  kt   32  45.1

$ awk ##### 在此处添加你的解决方案
1.3,rs,0.134563
3.8,NA,6
5.2,ye,8.2387
4.2,kt,45.1
```

**h)** 显示每行输入中的第三和第五个字符，如下所示。

```
$ printf 'restore\ncricket' | awk ##### 在此处添加你的解决方案
sto
ik
```

# 记录分隔符

到为止，你已经看到 `awk` 如何根据 `\n` 换行符自动拆分输入。正如你可以使用 `FS` 控制这些行进一步拆分为字段一样，`awk` 提供了一种方法来控制什么构成一个行。在 `awk` 术语中，“记录（record）”一词用于描述放入 `$0` 变量的内容。类似于 `OFS`，你可以控制在 `print` 函数末尾添加的字符串。本章还将讨论如何使用与记录（行）号相关的特殊变量。

## 输入记录分隔符

`RS` 特殊变量用于控制如何将输入内容拆分为记录。默认是 `\n` 换行符，如之前的章节所示。特殊变量 `NR` 用来跟踪当前记录号。

```
# 将输入记录分隔符改为逗号
# 注意第二个记录的内容，换行只是另一个字符
printf 'this,is\na,sample' | awk -v RS=, '{print NR ")", $0}'
1) this
2) is
3) a
4) sample
```

记得默认 `FS` 将根据空格、制表符和换行符拆分输入记录。现在你已经看到 `RS` 可以是换行符以外的内容，这里有一个示例展示了默认记录拆分的完整效果。

```
$ s='   a\t\tb:1000\n\n\n\n123 7777:x  y \n \n z  '
printf '%b' "$s" | awk -v RS=: -v OFS=, '{$1=$1} 1'
a,b
1000
7777
z
```

与 `FS` 类似，`RS` 的值被视为字符串字面量并转换为正则表达式。现在，考虑一个具有多个字符 `RS` 但不需要正则表达式元字符的示例。

```
$ cat report.log
blah blah Error: second record starts
something went wrong
some more details Error: third record
details about what went wrong

# 使用 'Error:' 作为输入记录分隔符
# 打印所有包含 'something' 的记录
awk -v RS='Error:' '/something/' report.log
 second record starts
something went wrong
some more details 
```

> ![warning](img/file1.svg) 如果设置了 `IGNORECASE`，它也会影响记录分离。记录分隔符是单个字符时，可以通过使用字符类来绕过。





```bash
awk -v IGNORECASE=1 -v RS='error:' 'NR==1' report.log
blah blah 
# when RS is a single character
awk -v IGNORECASE=1 -v RS='e' 'NR==1' report.log
blah blah Error: s
awk -v IGNORECASE=1 -v RS='[e]' 'NR==1' report.log
blah blah 
```

> ![warning](img/file1.svg) 文本文件的默认换行符在不同平台之间有所不同。例如，从网上下载的文本或源自 Windows 系统的文件通常以回车符和换行符结尾。因此，对于此类文件，你可能需要使用 `RS='\r\n'`。有关详细的讨论和解决方法，请参阅 [stackoverflow: Why does my tool overwrite itself and how do I fix it?](https://stackoverflow.com/q/45772525/4082052)。

## 输出记录分隔符 (Output record separator)

特殊变量 `ORS` 用于输出记录分隔符。`ORS` 是在每次调用 `print` 函数时添加到末尾的字符串。`ORS` 的默认值是一个换行符，这与 `RS` 相同。

```bash
# 将 NUL 记录分隔符改为点和换行符
printf 'foo\0bar\0' | awk -v RS='\0' -v ORS='.\n' '1'
foo.
bar.

cat msg.txt
Hello there.
It will rain to-
day. Have a safe
and pleasant jou-
rney.
# 此处 ORS 为空字符串
awk -v RS='-\n' -v ORS= '1' msg.txt
Hello there.
It will rain today. Have a safe
and pleasant journey.
```

> ![info](img/file0.svg) 注意 `$0` 变量是在移除由 `RS` 匹配的尾部字符后赋值的。因此，你无法直接用 `sub` 等函数操作这些字符。对于不自动剥离记录分隔符的工具（如 `perl`），之前的示例可以通过 `perl -pe 's/-\n//' msg.txt` 来解决。

很多时候，你需要根据输入记录的内容或其他条件来更改 `ORS`。三元运算符 `cond ? expr1 : expr2` 经常用于此类场景。下面的示例假设输入是均匀整除的，如果不是这种情况，你必须添加更多逻辑。

```bash
# 在这里也可以 RS 代替 "\n"
seq 6 | awk '{ORS = NR%3 ? "-" : "\n"} 1'
1-2-3
4-5-6
```

> ![info](img/file0.svg) 如果输入的最后一行没有以输入记录分隔符结束，那么在使用 `print` 时，它可能会被加到输出中，因为 `ORS` 会被追加在末尾。

```bash
# 此处输入的最后一行没有以换行符结束
# 但在使用 'print' 时会通过 ORS 被添加
printf '1\n2' | awk '1; END{print 3}'
1
2
3
```

## 正则 RS 和 RT (Regexp RS and RT)

如前所述，传递给 `RS` 的值被视为字符串字量量然后转换为正则表达式。这里是一些示例。

```bash
# 将输入记录分隔符设置为一个或多个数字字符
# 打印包含 'i' 和 't' 的记录
printf 'Sample123string42with777numbers' | awk -v RS='[0-9]+' '/i/ && /t/'
string
with

# 类似于 FS，传递给 RS 的值是字符串字面量
# 然后被转换为正则表达式，因此这里需要用 \\ 而不是 \
printf 'load;err_msg--ant,r2..not' | awk -v RS='\\W+' '/an/'
ant
```

> ![info](img/file0.svg) 如果 `RS` 从输入开始处匹配，则第一条记录将为空。然而，如果 `RS` 匹配到输入文件的最后一个字符，则最后一条不会有空记录。这与 `FS` 在匹配到最后一个字符时的行为不同。

```bash
# 第一条记录为空，最后一条记录为换行符
# 将 'echo' 改为 'printf' 查看变化
echo '123string42with777' | awk -v RS='[0-9]+' '{print NR $0}'
1 [string]
2 [with]
3 [4]
printf '123string42with777' | awk -v FS='[0-9]+' '{print NF}'
4
printf '123string42with777' | awk -v RS='[0-9]+' 'END{print NR}'
3
```

特殊变量 `RT` 包含了由 `RS` 匹配的文本。该变量会在每个输入记录处更新。

```bash
# 打印记录号和该记录的 RT 值
# 最后一条记录 RT 为空，因为它以数字结尾
echo 'Sample123string42with777' | awk -v RS='[0-9]+' '{print NR, RT}'
1 123
2 42
3 777
4 
```

## 段落模式 (Paragraph mode)

作为一个特殊情况，当 `RS` 设置为空字符串时，一个或多个连续的空行被用作记录分隔符。考虑以下示例：

```bash
cat programming_quotes.txt
Debugging is twice as hard as writing the code in the first place.
Therefore, if you write the code as cleverly as possible, you are,
by definition, not smart enough to debug it by Brian W. Kernighan
Some people, when confronted with a problem, think - I know, I will
use regular expressions. Now they have two problems by Jamie Zawinski
A language that does not affect the way you think about programming,
is not worth knowing by Alan Perlis
There are 2 hard problems in computer science: cache invalidation,
naming things, and off-by-1 errors by Leon Bambrick
```

这是一个按段落处理输入的示例。

```bash
# 打印包含 'you' 的段落
# 注意最后一条记录后有一个空行
awk -v RS= -v ORS='\n' '/you/' programming_quotes.txt
Debugging is twice as hard as writing the code in the first place.
Therefore, if you write the code as cleverly as possible, you are,
by definition, not smart enough to debug it by Brian W. Kernighan

A language that does not affect the way you think about programming,
is not worth knowing by Alan Perlis
```

在处理自定义记录分隔符时，最后的空行是一个常见问题。你可以处理输出以移除它，或者添加逻辑来避免额外的行。这里是针对上述示例的一种解决方法。

```bash
# 此处 ORS 保持为默认换行符
# 未初始化的变量 's' 在第一次匹配时为空
# 之后 's' 将提供空行分隔
awk -v RS= '/you/{print s $0; s="\n"}' programming_quotes.txt
Debugging is twice as hard as writing the code in the first place.
Therefore, if you write the code as cleverly as possible, you are,
by definition, not smart enough to debug it by Brian W. Kernighan

A language that does not affect the way you think about programming,
is not worth knowing by Alan Perlis
```

段落模式不等同于使用 `RS='\n\n+'`，因为当 `RS` 为空时 `awk` 会执行更多操作。详细信息请参阅 [gawk manual: multiline records](https://www.gnu.org/software/gawk/manual/html_node/Multiple-Line.html#Multiple-Line)。重要的要点在文中引用并用示例说明。

> 然而，`RS = ""` 和 `RS = "\n\n+"` 之间存在重要的区别。在第一情况下，输入数据文件开头的换行符会被忽略





```bash
s='\n\n\na\nb\n\n12\n34\n\nhi\nhello\n'
# 段落模式
printf '%b' "$s" | awk -v RS= -v ORS='\n---\n' 'NR<=2'
a
b
---
12
34
---

# RS 为 '\n\n+'而不是段落模式
printf '%b' "$s" | awk -v RS='\n\n+' -v ORS='\n---\n' 'NR<=2'

---
a
b
---
```

> 如果一个文件在最后一条记录后没有额外的空行，则记录末尾的换行会被移除。在第二种情况下，不会进行这种特殊处理。

```bash
s='\n\n\na\nb\n\n12\n34\n\nhi\nhello\n'
# 段落模式
printf '%b' "$s" | awk -v RS= -v ORS='\n---\n' 'END{print}'
hi
hello
---
# RS 为 '\n\n+'而不是段落模式
printf '%b' "$s" | awk -v RS='\n\n+' -v ORS='\n---\n' 'END{print}'
hi
hello

---
```

> 当 RS 设置为空字符串且 FS 设置为单个字符时，换行符始终充当字段分隔符。这是在由 FS 产生的任何字段分隔符之外的。当 FS 为空字符串（""""）或正则表达式时，RS 的这一特殊功能不适用。它适用于默认的单空格字段分隔符：`FS = " "`

```bash
s='a:b\nc:d\n\n1\n2\n3'
# 段落模式下 FS 为单个字符
printf '%b' "$s" | awk -F: -v RS= -v ORS='\n---\n' '{$1=$1} 1'
a b c d
---
1 2 3
---
# 段落模式下 FS 为正则表达式
printf '%b' "$s" | awk -F':+' -v RS= -v ORS='\n---\n' '{$1=$1} 1'
a b
c d
---
1
2
3
---
# 段落模式下 FS 为单字符且 RS 为 '\n\n+'
printf '%b' "$s" | awk -F: -v RS='\n\n+' -v ORS='\n---\n' '{$1=$1} 1'
a b
c d
---
1
2
3
---
```

## NR 对比 FNR

有两个与记录数相关的特殊变量。你之前在章节中已经见过 `NR`，但这里有更多例子。

```bash
# 等同于: head -n2
seq 5 | awk 'NR<=2'
1
2
# 等同于: tail -n1
awk 'END{print}' table.txt
banana window shoes 3.14
# 仅修改第二行的第一个字段
awk 'NR==2{$1="green"} 1' table.txt
bread mat hair 42
cake mug shirt -7
banana window shoes 3.14
```

为止为止所有带有 `NR` 的示例都是单文件输入。如果是多个文件输入，你可以在 `NR` 和第二个变量 `FNR` 之间进行选择。区别在于 `NR` 包含目前为止读取的总记录数，而 `FNR` 仅包含当前处理文件的记录数。这里有一些展示它们如何运作的示例。之后你会看到更多例子。

```bash
awk -v OFS='\t' 'BEGIN{print "NR", "FNR"} {print NR, FNR, $0}' report.txt
NR FNR
1 blah Error: second starts
2 something went wrong
3 some more details: third record
4 details about what went wrong
5 bread mat hair 42
6 blue cake shirt -7
7 banana window shoes 3.14
# 等同于: head -q -n1
awk 'FNR==1' report.txt
blah Error: second starts
bread mat hair 42
```

> ![info](img/file0.svg) 对于大输入文件，使用 `exit` 避免不必要的记录处理。

```bash
seq 3542 462352 | awk 'NR==2452{print; exit}'
5993
seq 3542 462352 | awk 'NR==250; NR==2452{print; exit}'
3791
5993
# 这里是一个示例耗时
time seq 3542 462352 | awk 'NR==2452{print; exit}' > f1
real 0m.004s
time seq 3542 462352 | awk 'NR==2452' > f2
real 0m.395s
```

## 总结

本章向你展示了如何更改输入内容拆分为记录的方式，以及在使用 `print` 时如何设置追加字符串。段落模式对于处理由空行分隔的多行记录非常有用。你还学习了两个与记录数相关的特殊变量以及它们的使用场景。

到目前，你已经使用 `awk` 来处理文件内容而不修改源文件。下一章将讨论如何将更改写回原始输入文件。

## 练习

a) 输入文件 `jumbled.txt` 由由各种分隔符分隔的单词组成。显示所有包含 `an` 或 `at` 或 `in` 或 `it` 的单词，每行一个。

```bash
cat jumbled.txt
overcoats;furrowing-typeface%pewter##hobby
wavering:concession/woof\retailer
joint[]seer{intuition}titanic
awk ##### 在此处添加你的解决方案
overcoats
furrowing
wavering
joint
intuition
titanic
```

b) 使用 `awk` 模拟 `paste -sd,`。

```bash
# 此命令用逗号 ',' 字符连接所有输入行
paste -sd, addr.txt
Hello World,are you,This game is good,Today is sunny,12345,You funny
# 确保行尾没有逗号
# 并且确保行尾有换行符
awk ##### 在此处添加你的解决方案
Hello World,are you,This game is good,Today is sunny,12345,You funny
# 如果输入中只有一行，再次确保没有尾随逗号
printf 'foo' | paste -sd,
awk ##### 在此处添加你的解决方案
foo
```

c) 对于输入文件 `scores.csv`，添加另一列 `GP`，该值基于 `100` 分计算，给 `Maths` 占比 50%，给 `Physics` 和 `Chemistry` 各占比 25%。

```bash
awk ##### 在此处添加你的解决方案
Name,Maths,Physics,Chemistry,GP
Blue,67,46,99,69
Lin,78,83,80,79
Er,56,79,92,70
Cy,97,98,95,96
Ort,68,72,66
```

d) 对于输入文件 `sample.txt`，提取所有包含 `do` 且恰好行的段

```bash
cat sample.txt
Hello World

Good day
How are you

Just do-it
Believe it

Today is sunny
Not a bit funny
No doubt you like it too

Much about nothing
He he he

# 注意输出末尾没有额外的空行
awk ##### 在此处添加你的解决方案
Just do-it
Believe it

Much about nothing
He he he
```

e) 对于输入文件 `sample.txt`，使用 `.` 和空格字符作为分隔符将所有段落合并为单行。并在每个段落末尾添加一个最终的 `.`。





```
[](#cb134-1)$ # 注意输出末尾没有额外的空行
[](#cb134-2)$ awk ##### 在此处添加你的解决方案
[](#cb134-3)Hello World.
[](#cb134-4)
[](#cb134-5)你好。你今天好吗。
[](#cb134-6)
[](#cb134-7)尽管去做吧。相信你能做到。
[](#cb134-8)
[](#cb134-9)今天天气晴朗。一点也不搞笑。无疑你也喜欢它。
[](#cb134-10)
[](#cb134-11)一场空欢。嘿嘿。
```

### f) 各种输入/输出分隔符可以动态更改，并在下次输入/输出操作期间生效。对于输入文件 `mixed_fs.txt`，仅保留每行前两个字段。前两行的字段分隔符应为空格，其余行使用逗号 `,`。

```
[](#cb135-1)$ cat mixed_fs.txt
[](#cb135-2)rose lily jasmine tulip
[](#cb135-3)pink blue white yellow
[](#cb135-4)car,mat,ball,basket
[](#cb135-5)green,brown,black,purple
[](#cb135-6)
[](#cb135-7)$ awk ##### 在此处添加你的解决方案
[](#cb135-8)rose lily
[](#cb135-9)pink blue
[](#cb135-10)car,mat
[](#cb135-11)green,brown
```

### g) 对于输入文件 `table.txt`，获取所示输出。所有输出都包含行号作为解决方案的一部分。

```
[](#cb136-1)$ #打印第二行以外的内容
[](#cb136-2)$ awk ##### 在此处添加你的解决方案
[](#cb136-3)brown bread mat hair 42
[](#cb136-4)yellow banana window shoes 3.14
[](#cb136-5)
[](#cb136-6)$ # 打印包含 'air' 或 'win' 的行的行号
[](#cb136-7)$ awk ##### 在此处添加你的解决方案
[](#cb136-8)1
[](#cb136-9)3
[](#cb136-10)
[](#cb136-11)$ # 计算除第二行外最后一列数字的和
[](#cb136-12)$ awk ##### 在此处添加你的解决方案
[](#cb136-13)45.14
```

### h) 每五行一组，打印第二和第四行。

```
[](#cb137-1)$ seq 15 | awk ##### 在此处添加你的解决方案
[](#cb137-2)2
[](#cb137-3)4
[](#cb137-4)7
[](#cb137-5)9
[](#cb137-6)12
[](#cb137-7)14
```

### i) 对于输入文件 `odd.txt`，将所有起始和结束字符相同的整个单词用 `{}` 包围。这是一个为了让你练习使用 `RT` 而设计的练习题。在现实世界中，你可以使用 `sed -E 's/\b(\w|(\w)\w*\2)\b/{&}/g' odd.txt` 来解决这个问题。

```
[](#cb138-1)$ cat odd.txt
[](#cb138-2)-oreo-not:a _a2_ roar<=>took%22
[](#cb138-3)RoaR to wow-
[](#cb138-4)
[](#cb138-5)$ awk ##### 在此处添加你的解决方案
[](#cb138-6)-{oreo}-not:{a} {_a2_} {roar}<=>took%{22}
[](#cb138-7){RoaR} to {wow}-
```

# 原地文件编辑

在目前为止的示例中，`awk` 的输出显示在终端上。本章将讨论如何使用 `-i` 命令行选项将更改写回输入文件本身。该选项可以配置为在不创建原始内容备份的情况下对输入文件进行更改。

## 不使用备份

`-i` 选项允许你加载库（详情请 [gawk 手册: -i 选项](https://www.gnu.org/software/gawk/manual/gawk.html#index-_002di-option)）。`inplace` 库随 `awk` 安装默认提供。使用 `-i inplace` 表示 `awk` 应该修改原始输入。请谨慎使用此选项，最好在测试代码按预期工作之后。

```
[](#cb139-1)$ cat greet.txt
[](#cb139-2)Hi there
[](#cb139-3)Have a nice day
[](#cb139-4)Good bye
[](#cb139-5)
[](#cb139-6)$ # 为行号添加前缀
[](#cb139-7)$ awk -i inplace '{print NR ". " $0}' greet.txt
[](#cb139-8)$ cat greet.txt
[](#cb139-9)1. Hi there
[](#cb139-10)2. Have a nice day
[](#cb139-11)3. Good bye
```

多个输入文件会被分别处理，更改会被写回各自对应的文件。

```
[](#cb140-1)$ cat f1.txt
[](#cb140-2)I ate 3 apples
[](#cb140-3)$ cat f2.txt
[](#cb140-4)I bought two balls and 3 bats
[](#cb140-5)
[](#cb140-6)$ awk -i inplace '{gsub(/\<3\>/, "three")} 1' f1.txt f2.txt
[](#cb140-7)$ cat f1.txt
[](#cb140-8)I ate three apples
[](#cb140-9)$ cat f2.txt
[](#cb140-10)I bought two balls and three bats
```

## 使用备份

可以通过设置特殊变量 `inplace::suffix` 来提供备份扩展名。例如，如果输入文件是 `ip.txt` 并使用了 `inplace::suffix`，则备份文件将命名为 `ip.txt.orig`。





```bash
## 现有的环境变量
$ # 此处的输出针对我的机器，你的机器会有所不同
$ awk 'BEGIN{print ENVIRON["HOME"]}'
/home/learnbyexample
$ awk 'BEGIN{print ENVIRON["SHELL"]}'
/bin/bash

$ # 与 awk 命令一起定义
$ # 注意变量放置在 awk 之前
$ word='hello' awk 'BEGIN{print ENVIRON["word"]}'
hello
```

`ENVIRON` 是规避 `awk` 对转义序列解释的一种良好方法。这对于固定字符串匹配特别有用，示例参见 索引 章节。

```bash
$ s='hi\nbye'

# 通过 -v 选项传递时
$ awk -v ip="$s" 'BEGIN{print ip}'
hi
bye

# 作为环境变量传递时
$ ip="$s" awk 'BEGIN{print ENVIRON["ip"]}'
hi\nbye
```

这里另一个将正则表达式传递给 `awk` 命令的示例。

```bash
# 通过 -v 选项传递时
$ r='\Bpar\B'
$ awk -v rgx="$r" '$0 ~ rgx' word_anchors.txt
awk: warning: 转义序列 `\B` 被视为普通字符 `B`
$ r='\\Bpar\\B'
$ awk -v rgx="$r" '$0 ~ rgx' word_anchors.txt
apparent effort
two spare computers

# 作为环境变量传递时
$ r='\Bpar\B'
$ rgx="$r" awk '$0 ~ ENVIRON["rgx"]' word_anchors.txt
apparent effort
two spare computers
```

## 总结

本章简单回顾了 `-v` 命令行选项，并引入了 `ENVIRON` 特殊数组。当 `awk` 命令作为 shell 脚本的一部分时，这些工具特别有用。关于数组的更多内容将在后续章节中讨论。

下一章将涵盖控制结构。

## 练习

**a)** 使用变量 `s` 的内容显示输入文件 `sample.txt` 中的所有匹配行。假设 `s` 变量不包含任何正则表达式元字符，并构造一个仅匹配完整单词的解决方案。

```bash
$ s='do'
##### 在此处添加你的解决方案
Just do-it
```

**b)** 将输入文件 `addr.txt` 中所有出现的 `o` 替换为变量 `s` 的字面内容。假设 `s` 变量包含正则表达式元字符。

```bash
$ s='\&/'
##### 在此处添加你的解决方案
Hell\&/ W\&/rld
H\&/w are y\&/u
This game is g\&/\&/d
T\&/day is sunny
12345
Y\&/u are funny
```

# 控制结构

你已经见过各种需要条件表达式示例。本章将回顾 `if-else` 控制结构以及三元运算符。然后你将看到一些带有显式循环的示例（记得 `awk` 已经在遍历输入记录了）。随后是控制循环流的关键字。大部分语法与 `C` 语言非常相似。

## if-else

通常，当你需要使用 `if` 控制结构时，在 `awk` 单行命令中使用 `condX{actionX}` 格式即可。但有时，你可能需要在此类动作块内部进行额外的条件检查。或者，你可能在循环内部需要它。语法为 `if(cond){action}`，如果只需要一条语句，大括号是可选的。`if` 后面可以可选跟随多个 `else if` 条件和一个最终的 `else` 条件。这些也可以根据需要进行嵌套。

```bash
# 打印所有以 'b' 开头的行
$ # 此外，如果最后一列大于 0，则打印一些信息
$ awk '/^b/{print; if($NF>0) print "------"}' table.txt
brown mat hair 42
------
blue cake shirt -7
$ 与上述相同，还包含了 'else'
$ awk '/^b/{print; if($NF>0) print "------"; else print "=="}' table.txt
brown mat hair 42
------
blue cake shirt -7
```

三元运算符通常减少了对单个 `if-else` 情况的需求。

```bash
$ 等同于：awk '{if(NR%3) ORS="-" else ORS=RS}'
$ seq 6 | awk '{ORS = NR%3 ? "-" : RS}'
1-2-3-4-56
# 注意，在这种情况下 print 的括号是必要的
$ awk '/^b/{print; print($NF>0 ? "------" : "=="}' table.txt
brown mat hair 42
------
blue cake shirt -7
======
```

> ![info] 另请 [stackoverflow: 查找列的最小值和最大值](https://stackoverflow.com/a/297842)。

> ![info] 另请 [gawk 手册: switch](https://www.gnu.org/software/gawk/manual.html#Switch-Statement)。

## 循环

当你处理数组时，`for` 循环非常方便。处理输入字段也是如此，因为 `$N` 语法允许传递表达式 own 固定值。

```bash
$ awk 'BEGIN{for(i=2; i<7; i+=2) print i}'
2
4
6
# 遍历每个字段
$ awk -v OFS=, '{for(i=1; i<=NF; i++) if($i ~ /^[bm]/) $i="["i"]"}' 1' table.txt
[brown],mat,hair,42
[blue],cake,shirt,-7
```

这里有一个遍历动态构造数组的示例。

```bash
$ cat marks.txt
Dept    Name    Marks
ECE     Raj     53
EEE     Joel    72
CSE     Surya   81
EEE     Tia     59
ECE     Om      92
CSE     Amy     67
# 每个部门的平均分
$ awk 'NR>1{d[$1]+=$3; c[$1]++} END{for(k in d) print k, d[k]/c[k]}' marks.txt
ECE 72.3333
EEE 63.5
CSE 74
```

你可以使用 `break` 和 `continue` 来改变循环的正常流。`break` 会立即退出当前循环而不处理剩余语句。`continue` 会跳过循环中的剩余语句并开始下一次迭代。

```bash
$ awk -v OFS=, '{for(i=1; i<=NF; i++) if($i ~ /b/){NF=i; break}} 1' table.txt
brown
blue
yellow,banana
```

> ![info] 另请 [stackoverflow: 从列表中查找缺失的数字](https://stackoverflow.com/q/38491676/408205)。

`awk` 也支持 `while` 和 `do-while` 循环机制。

```bash
$ awk 'BEGIN{i=6; while(i>0){print i; i-=2}}'
6
4
2
# 递归替换
$ echo 'titillate' | awk '{while(gsub(/til/, "")) print}'
tilate
ate
$ echo 'titillate' | awk '{do{print} while(gsub(/til/, ""))}'
titillate
tilate
ate
```

## next

`next` 类似于 `continue` 语句，但它作用于遍历输入记录的循环。它不影响 `BEGIN` 或 `END` 块，因为它们在循环之外。执行 `next` 时，其余语句将被跳过，并获取下一个输入记录进行处理。

```bash
$ awk '/\<par/{print "%% " $0; next} {print /s/ ? "X" : "Y"}' word_anchors.txt
%% sub par
X
Y
X
%% cart part tart mart
```

你将在后续章节中看到更多 `next` 的示例。

## exit





```
$ seq 3542 4623452 | awk 'NR==2452{print; exit}'
5993
$ echo $?
0

$ awk '/^br/{print "Invalid input"; exit 1}' table.txt
Invalid input
$ echo $?
1

# 剩余待处理的文件也会被跳过
$ awk 'FNR==2{print; exit}' table.txt greeting.txt
blue cake mug shirt -7
```

如果在 `BEGIN` 或普通块中使用 `exit`，则 `END` 块中的任何代码仍会被执行。有关更多细节和边界情况，请参见 [gawk 手册：exit](https://www.gnu.org/software/gawk/manual/gawk.html#Exit-Statement)。

```
$ # 首先执行第一个 print
$ # 看到 exit 后，剩余的 BEGIN 和普通块将被跳过
$ # 随后执行 END 中的代码
$ awk 'BEGIN{print "hi"; exit; print "hello"}
 /^b/;
END{print "bye"}' table.txt
hi
bye
```

## 总结

本章涵盖了 `awk` 提供的一些控制流结构。对于熟悉编程语言的人来说，这些特性使得 `awk` 比 `sed` 更灵活且易用。

下一章将讨论一些内置函数。

## 练习

**a)** 输入文件 `nums.txt` 包含单列数字。将正数更改为负数，反之亦然。你可以在仅使用 `sub` 函数且不显式使用 `if-else` 或三元运算符的情况下完成吗？

```
$ cat nums.txt
42
-2
10101
-3.14
-75

$ awk ##### 在此处添加你的解决方案
-42
2
-10101
3.14
75
```

**b)** 对于输入文件 `table.txt`，将字段分隔符从空格改为 `,` 字符。此外，任何不包含数字字符的字段都应该用双引号括起来。

```
$ awk ##### 在此处添加你的解决方案
"brown","bread","mat","hair",42
"blue","cake","mug","shirt",-7
"yellow","banana","window","shoes",3.14
```

**c)** 对于文件 `secrets.txt` 的每行输入，删除每个字段最后一个字符以外的所有字符。假设空格作为输入字段分隔符。

```
$ cat secrets.txt
stag area row tick
deaf chi rate tall glad
Bi tac toe - 42

$ awk ##### 在此处添加你的解决方案
gawk
field
ice-2
```

**d)** 模拟如下所示的 `sed` 命令 `q` 和 `Q`。

```
$ # sed '/are/q' sample.txt 将打印到（并包含）包含 'are' 的行
$ awk ##### 在此处添加你的解决方案
Hello World

Good day
How are you

$ # sed '/are/Q' sample.txt 将打印到（但不包含）包含 'are' 的行
$ awk ##### 在此处添加你的解决方案解决方案
Hello World

Good day
```

**e)** 对于输入文件 `addr.txt`：

*   如果行包含 `e`
    *   删除所有 `e` 的出现情况
    *   用 `{}` 括起所有连续重复的字符
    *   假设输入不会有两个以上的连续重复
*   如果行不包含 `e` 但包含 `u`
    *   用 `[]` 括起行中所有的小写元音

```
$ awk ##### 在此处添加你的解决方案
Hello World
How you
This is godunny
12345
You funny
```

## 内置函数

你已经详细看到了一些内置函数，如 `sub`、`gsub` 和 `gensub`。本章将讨论许多单行命令中常用的内置函数。你还将看到更多关于数组的示例。访问 [gawk 手册：函数](https://www.gnu.org/software/gawk/manual/gawk.html#Functions) 获取有关所有内置函数的细节以及如何定义你自己的函数。

### length

`length` 函数返回给定字符串的字符数。默认情况下，它作用于 `$0` 变量，并将数字参数转换为字符串。

```
$ awk 'BEGIN{print length("road"); print length(12346)}'
4
6
# 记录分隔符不是 $0 的一部分
# 所以，行结束符在这里不会被计数
$ printf 'fox\ntiger\n' | awk '{print length()}'
3
5

$ awk 'length($1)' table.txt
bread mat hair 42
blue cake shirt -7
```

如果你需要字节数而不是字符数，请使用 `-b` 选项。区域设置（Locale）也可能起作用。

```
$ echo 'αλε' | awk '{print length()}'
6
$ echo 'αλε' | awk -b '{print length()}'
12
$ echo 'αλε' | LC_ALL=C awk '{print length()}'
12
```

### 数组排序

默认情况下，使用 `for(key in array)` 遍历数组会以随机顺序给你的元素。通过给 `PROCINFO["sorted_in"]` 设置一个特殊值，你可以控制你想要检索元素的顺序。参见 [gawk 手册：使用预定义的数组顺序](https://www.gnu.org/software/gawk/manual/gawk.html#Controlling-Scanning) 获取其他选项和细节。

```
$ 默认情况下，数组按随机顺序遍历
$ awk 'BEGIN{a["z"]=1; a["x"]=12; a["b"]=42; for(i in a) print i, a[i]}'
x 12
z 1
b 42

# 索引（即键）按字符串升序排序
$ awk 'BEGIN{PROCINFO["sorted_in"] = "@ind_str_asc";
a["z"]=1; a["x"]=12; a["b"]=42; for(i in a) print i, a[i]}'
b 42
x 12
z 1

# 值按数字升序排序
$ awk 'BEGIN{PROCINFO["sorted_in"] = "@val_num_asc";
a["z"]=1; a["x"]=12; a["b"]=42; for(i in a) print i, a[i]}'
z 1
x 12
b 42
```

这是一个根据第二列（视为字符串）升序排序输入行的示例。

```
$ awk 'BEGIN{PROCINFO["sorted_in"] = "@ind_str_asc"}
{a[$2]=$0} END{for(k in a) print a[k]}' table.txt
yellow banana window shoes 3.14
brown bread mat hair 42
blue cake mug shirt -7
```

### split

`split` 函数提供了与使用 `FS` 进行记录分割相同的功能。当你由于某些原因需要数组形式的结果时非常有用，例如为了使用数组排序功能。或者当你需要进一步拆分字段内容时。`split` 四个参数，后两个是可选的。

*   第一个参数是要拆分的字符串
*   第二个参数是用于保存结果的数组变量
*   第三个参数是分隔符，默认值为 `FS`

`split` 函数的返回值是字段数，类似于 `NF` 变量。数组从 `1` 开始索引，第一个元素为 `1`，第二个元素为 `2`，依此类推。如果数组已经有了值，它会被新值覆盖。





```bash
# 等于： awk '{print $2}'
printf '     one \t two\t\t\tthree  ' | awk '{split($0, a); print a[2]}'
two

# 同时使用 FS 和 split 的示例
s='Joe,1996-10-25,64,78'
echo "$s" | awk -F, '{split($2, d, "-"); print $1 " was born in " d[1]}'
Joe was born in 1996

# 根据分割最后一个字段将单行转换为多行
s='air,water,12:42:3'
echo "$s" | awk -F, '{n=split($NF, a, ":");
for(i=1; i<=n; i++) print $1, $2, a[i]}'
air water 12
air water 42
air water 3
```

与 `FS` 类似，你可以使用正则表达式作为分隔符。

```bash
s='Sample123string42with777numbers'
echo "$s" | awk '{split($0, s, /[0-9]+/); print s[2], s[4]}'
string numbers
```

第四个参数提供了 `FS` 分割不具备的功能。它允许你将由分隔符匹配到的部分保存到数组中。引用 [gawk 手册：split()](https://www.gnu.org/software/gawk/manual/gawk.html#index-split_0028_0029-function)：

> 如果 `fieldsep` 是单个空格，则任何前面的空白字符将进入 `seps[0]`，任何结尾的空白字符将进入 `seps[n]`，其中 `n` 是 `split()` 的返回值（即数组中的元素个数）。

```bash
s='Sample123string42with777numbers'
echo "$s" | awk '{n=split($0, s, /[0-9]+/, seps);
for(i=1; i<n; i++) print seps[i]}'
123
42
777
```

这里是一个示例，其中 `split` 仅用于根据空分隔符初始化数组。与 `$N` 语法（允许产生浮点数的表达式）不同，数组索引必须是整数。因此，在下面的示例中使用了 `int` 函数将浮点结果转换为整数。

```bash
cat marks.txt
Dept    Name    Marks
ECE     Raj     53
ECE     Joel    72
EEE     Moi     68
CSE     Surya   81
EEE     Tia     59
ECE     Om      92
CSE     Amy     67

# 根据第 3 列的标记添加新的等级列
awk 'BEGIN{OFS="\t"; split("DCBAS", g, //)}
{$(NF+1) = NR==1 ? "Grade" : g[int($NF/10)-4]} 1' marks.txt
Dept    Name    Marks   Grade
ECE     Raj     53      D
ECE     Joel    72      B
EEE     Moi     68      C
CSE     Surya   81      A
EEE     Tia     59      D
ECE     Om      92      S
CSE     Amy     67      C
```

## patsplit

`patsplit` 函数将为你提供由 `FPAT` 提供的特性。参数顺序和可选参数与 `split` 函数相同，以 `FPAT` 为默认分隔符。返回值是从分割中获得的字段数量。

```bash
s='eagle,"fox,42",bee,frog'
echo "$s" | awk '{patsplit($0, a, /"[^"]*"|[^,]*/); print a[2]}'
"fox,42"
```

## substr

`substr` 函数允许根据索引从给定字符串提取指定数量的字符。参数顺序为：

* 第一个参数是输入字符串
* 第二个参数是起始位置
* 第三个参数是要提取的字符数

索引从 `1` 开始。如果未指定第三个参数，默认提取直到输入字符串末尾的所有字符。如果第二个参数大于字符串长度，或者第三个参数小于等于 `0`，则返回空字符串。如果指定的数字小于 1，则第二个参数将使用 `1`。

```bash
echo 'abcdefghij' | awk '{print substr($0, 1, 5)}'
abcde
echo 'abcdefghij' | awk '{print substr($0, 4, 3)}'
def
echo 'abcdefghij' | awk '{print substr($0, 6)}'
fgh
echo 'abcdefghij' | awk -v OFS=: '{print substr($0, 2, 3), substr($0, 6)}'
bcd:fgh
```

如果只需要输入中的几个字符，也可以使用 `FS`。

```bash
echo 'abcdefghij' | awk -v FS= '{print $3}'
c
echo 'abcdefghij' | awk -v FS= '{print $5}'
e
```

## match

`match` 函数用于提取被正则表达式匹配的输入字符串部分。获取匹配部分有两种方法：

* 通过使用 `substr` 函数配合特殊变量 `RSTART` 和 `RLENGTH`
* 给 `match` 传递第三个参数，以便结果从数组中可用

`match` 的第一个参数是输入字符串，第二个是正则表达式。如果匹配失败，`RSTART` 将得到 `0`。

```bash
s='051234 154 9823'
# 逗号分隔的示例
echo 's,42,123' | awk '{match($0, /,[0-9]+/); print substr($0, RSTART, RLENGTH)}'
,42
,123
# 使用数组获取结果
echo 's,42,123' | awk '{match($0, /,[0-9]+/, a); print a[2]}'
42
```





请记住 `-v` 选项是由 `awk` 的字符串处理规则解析的。因此，如果你需要传递一个字面量而不想陷入反斜杠地狱，请使用 `ENVIRON` 而不是 `-v` 选项。

```
[](#cb180-1)$ echo 'a\b\c\d' | awk -v s='a\b' 'index($0, s)'
[](#cb180-2)$ echo 'a\b\c\d' | awk -v s='a\\b' 'index($0, s)'
[](#cb180-3)a\b\c\d
[](#cb180-4)$ echo 'a\b\c\d' | s='a\b' awk 'index($0, ENVIRON["s"])'
[](#cb180-5)a\b\c\d
```

## system

可以使用 `system` 函数执行外部命令。除非在调用命令时进行了重定向，否则外部命令生成的任何输出将像往一样输出到 `stdout`。

```
[](#cb181-1)$ awk 'BEGIN{system("echo Hello World")}'
[](#cb181-2)Hello World
[](#cb181-3)
[](#cb181-4)$ wc table.txt
[](#cb181-5) 3 15 79 table.txt
[](#cb181-6)$ awk 'BEGIN{system("wc table.txt")}'
[](#cb181-7) 3 15 79 table.txt
[](#cb181-8)
[](#cb181-9)$ awk 'BEGIN{system("seq 10 | paste -sd, > out.txt")}'
[](#cb181-10)$ cat out.txt
[](#cb181-11)1,2,3,4,5,6,7,8,9,10
[](#cb181-12)
[](#cb181-13)$ cat t2.txt
[](#cb181-14)I bought two balls and 3 bats
[](#cb181-15)$ echo 'f1,t2,f3' | awk -F, '{system("cat " $2 ".txt")}'
[](#cb181-16)I bought two balls and 3 bats
```

`system` 的返回值取决于所执行命令的 `exit` 状态。详情请参阅 [gawk manual：输入/输出函数](https://www.gnu.org/software/gawk/manual/html_node/I_002fO-Functions.html)。

```
[](#cb182-1)$ ls xyz.txt
[](#cb182-2)ls: cannot access 'xyz.txt': No such file or directory
[](#cb182-3)$ echo $?
[](#cb182-4)2
[](#cb182-5)
[](#cb182-6)$ awk 'BEGIN{s=system("ls xyz.txt"); print "Exit status: " s}'
[](#cb182-7)ls: cannot access 'xyz.txt': No such file or directory
[](#cb182-8)Exit status: 2
```

## printf and sprintf

当你需要在打印之前格式化数据时，`printf` 函数比 `print` 函数更好。另一个区别是 `OFS` 和 `ORS` 不影响 `printf` 函数。这些特性与 `C` 语言和 shell 内置命令中的特性相似。

```
[](#cb183-1)$ # OFMT 控制 print 函数显示数字的格式化
[](#cb183-2)$ awk 'BEGIN{print OFMT}'
[](#cb183-3)%.6g
[](#cb183-4)$ awk 'BEGIN{sum = 3.1428 + 100; print sum}'
[](#cb183-5)103.143
[](#cb183-6)$ awk 'BEGIN{OFMT="%.5f"; sum = 3.1428 + 100; print sum}'
[](#cb183-7)103.14280
[](#cb183-8)
[](#cb183-9)$ # 使用 printf 函数
[](#cb183-10)$ # 注意使用 \n，因为不像 print，它不会追加 ORS
[](#cb183-11)$ awk 'BEGIN{sum = 3.1428 + 10; printf "%f\n", sum}'
[](#cb183-12)13.142800
[](#cb183-13)$ awk 'BEGIN{sum = 3.1428 + 10; printf "%.3f\n", sum}'
[](#cb183-14)13.143
```

这里是更多浮点数的格式化选项。

```
[](#cb184-1)$ # 总长度为 10，需要时用空格填充
[](#cb184-2)$ # 在这里使用 [ 和 ] 是为了可视化目的-
[](#cb184-3)$ awk 'BEGIN{pi = 3.14159; printf "[%10.3f]\n", pi}'
[](#cb184-4)[     3.142]
[](#cb184-5)$ awk 'BEGIN{pi = 3.14159; printf "[%-10.3f]\n", pi}'
[](#cb184-6)[3.142     ]
[](#cb184-7)
[](#cb184-8)$ # 零填充
[](#cb184-9)$ awk 'BEGIN{pi = 3.14159; printf "%010.3f\n", pi}'
[](#cb184-10)000003.142
[](#cb184-11)
[](#cb184-12)$ # 科学计数法
[](#cb184-13)$ awk 'BEGIN{pi = 3.14159; printf "%e\n", pi}'
[](#cb184-14)3.141590e+00
```

是整数的格式化选项。

```
[](#cb185-1)$ # 注意没有四舍五入
[](#cb185-2)$ awk 'BEGIN{printf "%d\n", 1.99}'
[](#cb185-3)1
[](#cb185-4)
# 确保整数始终带符号
[](#cb185-5)$ awk 'BEGIN{printf "%+d\n", 100}'
[](#cb185-6)+100
[](#cb185-7)$ awk 'BEGIN{printf "%+d\n", -100}'
[](#cb185-8)-100
```

是字符串的一些格式化选项。

```
[](#cb186-1)$ # 前缀剩余宽度
[](#cb186-2)$ awk 'BEGIN{printf "|10s|\n", "mango"}'
[](#cb186-3)|     mango|
[](#cb186-4)$ # 后缀剩余宽度
[](#cb186-5)$ awk 'BEGIN{printf "|%-10s|\n", "mango"}'
[](#cb186-6)|mango     |
[](#cb186-7) # 截断
[](#cb186-8)$ awk '{printf "%.4s\n", $0}'
[](#cb186-9)brow
[](#cb186-10)blue
```

你也可以 `N$` 格式引用参数，其中 `N` 是位置数字。这种方法的优点是你可以重复使用参数。你不能将这种格式与普通方式混合。

```
[](#cb187-1)$ awk 'BEGIN{printf "%1$d + %2$d = %3$d\n", 3, 4, 15}'
[](#cb187-2)3 + 4 = 15
[](#cb187-3)$ # 如果不需要前缀
[](#cb187-4)$ awk 'BEGIN{printf "hex=%1$x\noct=%1$o\ndec=%1$d\n", 15}'
[](#cb187-5)hex=f
oct(#cb187-6)oct=17
[](#cb187-7)dec=15
```

你可以通过在格式字符串中指定 `*` 而不是数字来传递变量。

```
[](#cb188-1)$ # 等于：awk 'BEGIN{pi = 3.14159; printf "%10.3f\n", pi}'
[](#cb188-2)$ awk 'BEGIN{d=10; p=3; pi = 3.14159; printf "%0.*f\n", d, pi}'
[](#cb188-3)000003.142
```

> > 直接向 `printf` 传递变量而不使用格式说明可能会根据变量的内容导致错误。

```
[](#cb189-1)$ awk 'BEGIN{s="solve: % x = 1"; printf s}'
[](#cb189-2)awk: line:1: not enough arguments to satisfy format
[](#cb189-3)    `solve: % x = 1'
[](#cb189-4) ^ ran out for this
```

因此，良好的习惯是始终配合适当格式使用变量，而不是将其传递给 `printf`。

```
[](#cb190-1)$ awk 'BEGIN{s="solve: % x = 1"; printf "%s\n", s}'
[](#cb190-2)solve: % x = 1
```

如果格式说明符内部必须使用字面量 `%`，请使用 `%%`。这类似于在正则表达式中使用 `\` 来表示字面量 `\` `。

```
[](#cb191-1)$ awk 'BEGIN{printf "n%%d gives the remainder\n"}'
[](#cb191-2)n%d gives the remainder
```

要将格式化结果保存到变量中而不是打印，请使用 `sprintf` 函数。与 `printf` 不同，使用 `sprintf` 函数时始终需要括号。

```
[](#cb192-1)$ awk 'BEGIN{pi = 3.14159; s = sprintf("%10.3f", pi); print s}'
[](#cb192-2)000003.142
```

 重定向 print 输出

`print` 和 `printf` 函数的结果可以重定向到外部命令或文件，而不是 `stdout`。这没什么特别的，你也可以在 `awk` 命令中正常执行。用例出现在只需要重定向特定部分或者在同一个 `awk` 命令中需要多个重定向时。这里有一些重定向到多个文件的示例。

```
[](#cb193-1)$ seq 6 | awk 'NR%2{print > "odd.txt"; next} {print > "even.txt"}'
[](#cb193-2)$ cat odd.txt
[](#cb193-3)1
[](#cb193-4)3
[](#cb193-5)5
[](#cb193-6)$ cat even.txt
[](#cb193-7)2
[](#cb193-8)4
[](#cb193-9)6
[](#cb193-11)$ # 动态创建文件名
[](#cb193-12)$ awk -v OFS='\t' 'NR>1{print $2, $3 > $1".txt"}' marks.txt
[](#cb193-13)$ # 其中一个部门的输出
[](#cb193-14)$ cat ECE.txt
[](#cb193-15)Raj     53
[](#cb193-16)Joel    72
[](#cb193-17)Om      92
```





```bash
awk '{print $2 | "sort | paste -sd,"}' table.txt
banana,bread,cake

# 在写入文件之前对输出排序
awk -v OFS='\t' 'NR>1{print $2, $3 | "sort > "$1".txt"}' marks.txt
# 输出一个部门的内容
cat ECE.txt
Joel    72
Om      92
Raj     53
```

> ![info](img/file0.svg) 请参考 [gawk manual: 重定向 print 和 printf 的输出](https://www.gnu.org/software/gawk/manual/gawk.html#Redirection) 以了解更多关于重定向和操作符的信息。如果有太多的重定向，请查看 [gawk manual: 关闭输入和输出重定向](https://www.gnu.org/software/gawk/manual/gawk.html#Close-Files-And-Pipes)。

## 总结

本章介绍了 `awk` 提供的的一些内置函数。请检查手册以获取更多函数，例如数学和时间相关的函数。

下一章将介绍与处理作为输入传递给 `awk` 的多个文件相关的特性。

## 练习

> ![info](img/file0.svg) 练习还将包含在本章未讨论的函数和特性。参考 [gawk manual: 函数](https://www.gnu.org/software/gawk/manual/gawk.html#Functions) 详情。

**a)** 针对输入文件 `scores.csv`，根据 `Physics` 值降序对行进行排序。表头应作为第一行保留。

```bash
awk ##### 在此处添加你的解决方案
Name,Maths,Physics,Chemistry
Ith,100,100,100
Cy,97,98,95
Lin,78,83,80
Er,56,79,92
Ort,68,72,66
Blue,67,46,99
```

**b)** 针对输入文件 `nums3.txt`，计算数字的平方根并以两种不同的格式显示。首先小数点后保留四位，然后使用科学计数法并同样保留四位小数。假设输入只有单列正数。

```bash
awk ##### 在此处添加你的解决方案
1.7720
64.8151
27.8747
568.3414

awk ##### 在此处添加你的解决方案
1.7720e+00
6.4815e+01
2.7875e+01
5.6834e+02
```

**c)** 将给定的输入字符串转换为所示相应的输出。假设空格为字段分隔符。从第二个字段中删除第二个 `:` 以及其随后的数字。通过将最后一个字段乘以从第二个字段中删除的数字来修改该最后一个字段。这些数字可以是正/负整数或浮点数（包括科学计数法）。

```bash
echo 'go x:12:-425 og 6.2' | awk ##### 在此处添加你的解决方案
go x:12 og -2635

echo 'rx zwt:3.64:12.89e2 ljg 5' | awk ##### 在此处添加你的解决方案
rx zwt:3.64 ljg 6445
```

**d)** 将给定的输入字符串转换为所示相应的输出。假设空格为字段分隔符。将第二个字段替换为嵌入其中的两个数字之和。这些数字可以是正/负整数或浮点数（但不是科学计数法）。

```bash
echo 'f2:z3 kt//-42\\3.14//tw 5y6' | awk ##### 在此处添加你的解决方案
f2:z3 -38.86 5y6

echo 't5:x7 qr;wq<=>+10{-8764.124}yb u9' | awk ##### 在此处添加你的解决方案
t5:x7 -8754.12 u9
```

**e)** 针对给定的输入字符串，提取从 shell 变量 `s` 指定匹配位置开始到行尾的行部分。如果没有匹配，则不打印该行。`s` 的内容应进行字面匹配。

```bash
s='(a^b)'
echo '3*f + (a^b) - 45' | ##### 在此处添加你的解决方案
(a^b) - 45

s='\&/'
# 此输入不应输出
echo 'f\&z\&2.14' | ##### 在此处添加你的解决方案
# 但这个有一个匹配
echo 'f\&z\&2.14' | ##### 在此处添加你的解决方案
\&2.14
```

**f)** 提取所有以 `-` 开头并以 `:` 或 `;` 结尾的正整数，并换行显示所有此类匹配项。

```bash
s='42 foo-5; baz3; x-83, y-20:-34'
echo "$s" | awk 在此处添加你的解决方案
5
20
34
```

**g)** 针对输入文件 `scores.csv`，计算每个 `Name` 三个分数的平均分。平均分大于等于 `80` 的保存到 `pass.csv`，其余保存到 `fail.csv`。格式为 `Name` 和平均分（保留两位小数），用表符分隔。

```bash
awk ##### 在此处添加你的解决方案
cat fail.csv
Blue    70.67
Er      75.67
Ort     68.67
cat pass.csv
Lin     80.33
Cy      96.67
th     100.00
```

**h)** 针对输入文件 `files.txt`，将以空格开头的行替换为该行命令的输出。

```bash
cat files.txt
sed -n '2p' addr.txt
wc -w sample.txt
awk '{print $1}' table.txt
awk 在此处添加你的解决方案
How are you
31 sample.txt
brown
blue
yellow
```

**i)** 针对输入文件 `fw.txt`，用科学计数法格式化最后一列数字，保留两位小数。

```bash
awk 在此处添加你的解决方案
1.3e+01
3.8e+00
5.2e+00
4.2e+01
```

**j)** 针对输入文件 `addr.txt`，显示所有包含 `e` 或 `u` 但不同时两者的行。

> ![info](img/file0.svg) 提示 — [gawk manual: 位操作](https://www.gnu.org/software/gawk/manual/gawk.html#Bitwise-Functions)。

```bash
awk 在此处添加你的解决方案
Hello World
This game is good
Today is sunny
```





> ![warning](img/file1.svg) `nextfile` 不能在 `BEGIN`、`END` 或 `ENDFILE` 块中使用。更多信息请参见 [gawk manual: nextfile](https://www.gnu.org/software/gawk/manual/gawk.html#Nextfile-Statement)，以及它如何影响 `ENDFILE` 等特殊情况。

## ARGC 和 ARGV

特殊变量 `ARGC` 包含给 `awk` 命令的参数总数，包括 `awk` 本身作为一个参数。特殊数组 `ARGV` 包含了参数本身。

```
[](#cb208-1)$ # 注意这里的索引从 '0' 开始
[](#cb208-2)$ awk 'BEGIN{for(i=0; i<ARGC; i++) print ARGV[i]}' f[1-3].txt greeting.txt
[](#cb208-3)awk
[](#cb208-4)f1.txt
[](#cb208-5)f2.txt
[](#cb208-6)f3.txt
[](#cb208-7)greeting.txt
```

类似于操作 `NF` 和修改 `$N` 字段内容，你可以更改 `ARGC` 和 `ARGV` 的值来控制如何处理这些参数。

然而，并非所有参数都是文件名。如果在通常提供文件参数的地方，`awk` 允许在不使用 `-v` 选项的情况下为变量赋值。例如：

```
[](#cb209-1)$ awk 'BEGIN{for(i=0; i<ARGC; i++) print ARGV[i]}' table.txt n=5 greeting.txt
[](#cb209-2)awk
[](#cb209-3)table.txt
[](#cb209-4)n=5
[](#cb209-5)greeting.txt
```

在上面的示例中，在 `awk` 处理完 `table.txt` 文件后，变量 `n` 将获得值 `5`。这里是一个在两个文件之间更改 `FS` 的示例。

```
[](#cb210-1)$ cat table.txt
[](#cb210-2)brown bread mat hair 42
[](#cb210-3)blue cake mug shirt -7
[](#cb210-4)yellow banana window shoes 3.14
[](#cb210-5)$ cat books.csv
[](#cb210-6)Harry Potter,Mistborn,To Kill a Mocking Bird
[](#cb210-7)Matilda,Castle Hangnail,Jane Eyre
[](#cb210-8)
[](#cb210-9)$ # 对于 table.txt，FS 将为默认值
[](#cb210-10)$ # 对于 books.csv，FS 将为逗号
[](#cb210-11)$ # 两个文件的 OFS 均为逗号
[](#cb210-12)$ awk -v OFS=, 'NF=2' table.txt FS=, books.csv
[](#cb210-13)brown,bread
[](#cb210-14)blue,cake
[](#cb210-15)yellow,banana
[](#cb210-16)Harry Potter,Mistborn
[](#cb210-17)Matilda,Castle Hangnail
```

> ![info](img/file0.svg) 参考 [stackoverflow: extract positions 2-7 from a fasta sequence](https://stackoverflow.com/a/64427745/4082052) 获取关于在处理的文件之间更改字段/记录分隔符的实际示例。

## 总结

本章介绍了几个对于处理多个文件输入非常有用的特殊块和变量。这些内容将在后续章节的示例中出现。

下一章将讨论需要根据多个输入记录做决策的用例。

## 练习

**a)** 打印输入文件 `table.txt`、`scores.csv` 和 `fw.txt` 前两行的最后一个字段。这些文件的字段分隔符分别是空格、逗号和固定宽度。为了让输出更具信息量，请像下面的输出所示打印文件名和分隔符。假设输入文件至少有两行。

```
[](#cb211-1)$ awk ##### 在此处添加你的解决方案
[](#cb211-2)>table.txt<
[](#cb211-3)42
[](#cb211-4)-7
[](#cb211-5)----------
[](#cb211-6)>scores.csv<
[](#cb211-7)Chemistry
[](#cb211-8)99
[](#cb211-9)----------
[](#cb211-10)>fw.txt<
[](#cb211-11)0.134563
[](#cb211-12)6
[](#cb211-13)----------
```

**b)** 对于给定的输入文件列表，显示第三字段中包含 `at` 或 `fun` 的文件名。假设空格为字段分隔符。

```
[](#cb212-1)$ awk ##### 在此处添加你的解决方案 sample.txt secrets.txt addr.txt table.txt
[](#cb212-2)secrets.txt
[](#cb212-4)table.txt
```

## 处理多个记录

通常，你你需要将记录分组以便作为一个单元进行处理。例如，你可能想要处理所有属于同一个用户的行。

## 处理连续记录

有时你不仅想要匹配的记录，还需要相对于匹配项的记录。例如，这可能是为了查看被匹配函数开处的注释。





```
[](#cb215-1)$ # 等同于: grep --no-group-separator -A1 'blue'
[](#cb215-2)$ # 输出匹配行以及其随后的行
[](#cb215-3)$ awk '/blue/{n=2} n && n--' context.txt
[](#cb215-4)blue
[](#cb215-5)    toy
[](#cb215-6)light blue
[](#cb215-7)    flower
[](#cb215-8)
[](#cb215-9)$ # 重叠示例，n 在达到 0 之前就会被重新赋值
[](#cb215-10)$ awk '/toy|flower/{n=2} n && n--{print NR, $0}' context.txt
[](#cb215-11)2     toy
[](#cb215-12)3     flower
[](#cb215-13)4     sand stone
[](#cb215-14)6     flower
[](#cb215-15)7     sky
[](#cb215-16)
[](#cb215-17)$ # 不允许重叠情况重新赋值计数器
[](#cb215-18)$ awk '!n && /toy|flower/{n=2} n && n--{print NR, $0}' context.txt
[](#cb215-19)2     toy
[](#cb215-20)3     flower
[](#cb215-21)6     flower
[](#cb215-22)7     sky
```

一旦你理解了上面的示例，本节中的其余示例应该更容易理解了。它们都是上面使用的逻辑的变体，并经过重新排列以解决所讨论的用例。

### 案例 2：匹配后打印 `n` 条记录。这与之前的情况类似，不同之处是匹配的记录不打印。

```
[](#cb216-1)$ # 在匹配行后打印 1 行
[](#cb216-2)$ # 对于重叠情况，n 在达到 0 之前会被重新赋值
[](#cb216-3)$ awk 'n && n--; /language/{n=1}' context.txt
[](#cb216-4)    english
[](#cb216-5)    python
[](#cb216-6)
[](#cb216-7)$ # 在匹配行后打印 2 行
[](#cb216-8)$ # 不允许重叠情况重新赋值计数器
[](#cb216-9)$ awk '!n && /toy|flower/{n=2; next} n && n--' context.txt
[](#cb216-10)    flower
[](#cb216-11)    sand stone
[](#cb216-12)    sky
[](#cb216-13)    water
```

### 案例 3：这里是如何打印匹配记录后的第 `n` 条记录。

```
[](#cb217-1)$ # 仅打印匹配行后找到第 2 行
[](#cb217-2)$ # 数组为每条记录保存匹配结果
[](#cb217-3)$ # 不依赖计数器，因此适用于重叠情况
[](#cb217-4)$ awk -v n=2 'a[NR-n]; /toy|flower/{a[NR]=1}' context.txt
[](#cb217-5)    sand stone
[](#cb217-6)light blue
[](#cb217-7)    water
[](#cb217-8)
[](#cb217-9)$ # 仅打印匹配行后找到第 3 行
[](#cb217-10)$ # n && !--n 只有在 --n 产生 0 时才为真
[](#cb217-11)$ # 重叠情况将不起，因为 n 在变为 0 之前会被重新赋值
[](#cb217-12)$ awk 'n && !--n; /language/{n=3}' context.txt
[](#cb217-13)    spanish
[](#cb217-14)    ruby
```

### 案例 4：匹配前打印 `n` 条记录。是否打印匹配本身留作练习。由于文件是正向读取的，且问题描述是在匹配记录之前打印内容，因此不会发生像之前示例那样的叠加情况。

```
[](#cb218-1)$ # 使用 i>0 是因为 NR 从 1 开始
[](#cb218-2)$ awk -v n=2 '/toy|flower/{for(i=NR-n; i<NR; i++) if(i>0) print a[i]}
[](#cb218-3) {a[NR]=$0}' context.txt
[](#cb218-4)blue
[](#cb218-5)blue
[](#cb218-6)    toy
[](#cb218-7)    sand stone
[](#cb218-8)light blue
```

### 案例 5：匹配记录之前的第 `n` 条记录。

```
[](#cb219-1)$ # 如果计数足够小，你可以将它们保存在变量中
[](#cb219-2)$ # 打印匹配行之前的第 2 行
[](#cb219-3)$ # NR>2 是因为前 2 条记录不应被考虑
[](#cb219-4)$ awk 'NR>2 && /toy|flower/{print p2} p2=p1; p1=$0' context.txt
[](#cb219-5)blue
[](#cb219-6)    sand stone
light blue
[]8)$ 否则，使用数组保存之前的记录
[](#cb219-9)$ awk -v n=4 'NR>n && /age/{print a[NR-n]} a[NR]=$0' context.txt
english
```

## 由不同标记边界的记录

此部分涵盖输入文件始终包含交替出现的起始和结束模式的情况。例如，两个起始模式之间没有结束模式，反之亦然。这些组内部也可以出现零或多条记录。下方示例文件将用于说明。为了简单，假设起始模式由 `start` 标记，结束模式由 `end` 标记。它们赋予了数字以便可视化输入和输出之间的转换。

```
[](#cb220-1)$ cat.txt
[](#cb220-2)mango
[](#cb220-3)icecream
[](#cb220-4)--start 1--
[](#cb220-5)1234
[](#cb220-6)6789
[](#cb220-7)end 1
[](#cb220-8)how are you
[](#cb220-9)have a nice day
[](#cb220-10)--start 2--
[](#cb220-11)a
[](#cb220-12)b
[](#cb220-13)c
[](#cb220-14)end 2
[](#cb220-15)par,far,tar
```

### 案例 1：根据不同标记处理所有记录组，包括匹配本身。为了简单，下面的命令将打印所有此类记录。

```
[](#cb221-1)$ awk '/start/{f=1} f; /end/{f=0}' uniform.txt
[](#cb221-2)--start 1--
[](#cb221-3)1234
[](#cb221-4)6789
[](#cb221-5)end 1
[](#cb221-6)--start 2--
[](#cb221-7)a
[](#cb221-8)b
[](#cb221-9)c
[](#cb221-10)end 2
```

![info](img/file0.svg) 类似于 `sed -n '/start/,/end/p'` 你也可以使用 `awk '/start/,/end/'` 但状态机格式更适用于后续的各种情况。

### 案例 2：处理所有记录组，但排除匹配本身。

```
[](#cb222-1)$ awk '/end/{f=0} f{print "*", $0} /start/{f=1}' uniform.txt
[](#cb222-2)* 1234
[](#cb222-3)* 6789
[](#cb222-4)* a
[](#cb222-5)* b
[](#cb222-6)* c
```

### 案例 3-4：处理所有记录组，但排除任意一个标记。

```
[](#cb223-1)$ awk '/start/{f=1} /end/{f=0} f' uniform.txt
[](#cb223-2)--start 1--
[](#cb223-3)1234
[](#cb223-4)6789
[](#cb223-5)--start 2--
[](#cb223-6)a
[](#cb223-7)b
[](#cb223-8)c
[](#cb223-9)
[](#cb223-10)$ awk 'f; /start/{f=1} /end/{f=0}' uniform.txt
[](#cb223-11)1234
[](#cb223-12)6789
[](#cb223-13)end 1
[](#cb223-14)a
[](#cb223-15)b
[](#cb223-16)c
[](#cb223-17)end 2
```

接下来的四个案例仅通过在上面的案例中使用 `!f` 代替 `f` 得到。

### 案例 5：处理所有输入记录，但标记边界的记录组。

```
[](#cb224-1)$ awk '/start/{f=1} !f{print $0 "."} /end/{f=0}' uniform.txt
[](#cb224-2)mango.
[](#cb224-3)icecream.
[](#cb224-4)how are you.
[](#cb224-5)have a nice day.
[](#cb224-6)par,far,mar,tar.
```

### 案例 6：处理所有输入记录，但排除标记之间的组。

```
[](#cb225-1)$ awk '/end/{f=0} !f; /start/{f=1}' uniform.txt
[](#cb225-2)mango
[](#cb225-3)icecream
[](#cb225-4)--start 1--
[](#cb225-5)end 1
[](#cb225-6)how are you
[](#cb225-7)have a nice day
[](#cb225-8)--start 2--
[](#cb225-9)end 2
[](#cb225-10)par,far,mar,tar
```





```
[](#cb227-1)$ awk '/start/{f=1} f; /end/{exit}' uniform.txt
[](#cb227-2)--start 1--
[](#cb227-3)1234
[](#cb227-4)6789
[](#cb227-5)`end 1`
[](#cb227-6)
[](#cb227-7)$ # 根据需要使用上一节讨论过的其他技巧
[](#cb227-8)$ awk '/end/{exit} f; /start/{f=1}' uniform.txt
[](#cb227-9)1234
[](#cb227-10)6789
```

单独获取最后一个块需要多得的工作，除非你恰好知道输入文件中有多少个块。

```
[](#cb228-1)$ # 按行反转输入，改变比较顺序，再次反转
[](#cb228-2)$ # 如果 RS 必须是换行符以外的字符则无法使用
[](#cb228-3)$ tac uniform.txt | awk '/end/{f=1} f; /start/{exit}' | tac
[](#cb228-4)--start 2--
[](#cb228-5)a
[](#cb228-6)b
[](#cb228-7)c
[](#cb228-8)`end 2`
[](#cb228-9)
[](#cb228-10)$ # 或者，将块保存在缓冲区中并单独打印最后一个
[](#cb228-11)$ awk '/start/{f=1; b=$0; next} f{b=b ORS $0} /end/{f=0}
[](#cb228-12) END{print b}' uniform.txt
[](#cb228-13)--start 2--
[](#cb228-14)a
[](#cb228-15)b
[](#cb228-16)c
[](#cb228-17)`end 2`
```

### 仅第 `n` 个块

```
[](#cb229-1)$ # 也可以使用： awk -v n=2 '/4/{c++} c==n{print; if(/6/) exit}'
[](#cb229-2)$ seq 30 | awk -v n=2 '/4/{c++} c==n; /6/ && c==n{exit}'
[](#cb229-3)14
[](#cb229-4)15
[](#cb229-5)16
```

### 所有于第 `n` 个块的块

```
[](#cb230-1)$ seq 30 | awk -v n=1 '/4/{f=1; c++} f && c>n; /6/{f=0}'
[](#cb230-2)14
[](#cb230-3)15
[](#cb230-4)16
[](#cb230-5)24
[](#cb230-6)25
[](#cb230-7)26
```

### 排除第 `n` 个块

```
[](#cb231-1)$ seq 30 | awk -v n=2 '/4/{f=1; c++} f && c!=n; /6/{f=0}'
[](#cb231-2)4
[](#cb231-3)5
[](#cb231-4)6
[](#cb231-5)24
[](#cb231-6)25
[](#cb231-7)26
```

### 仅当标记之间的记录匹配额外条件的所有块

```
[](#cb232-1)$ # 这里的额外条件是内容为 '15' 的记录
[](#cb232-2)$ seq 30 | awk '/4/{f=1; buf=$0; m=0; next}
[](#cb232-3) f{buf=buf ORS $0}
[](#cb232-4) /6/{f=0; if(m) print buf}
[](#cb232-5) $0=="15"{m=1}'
[](#cb232-6)14
[](#cb232-7)15
```

## 损坏的块

有时候，标记顺序可能是随机且混合的。在这种情况下，为了处理它们之间没有其他标记的块，缓冲区方法再次变得有用。

```
[](#cb233-1)$ cat broken.txt
[](#cb233-2)qqqqqqqqqqqq
[](#cb233-3)error 1
[](#cb233-4)hi
[](#cb233-5)error 2
[](#cb233-6)1234
[](#cb233-7)6789
[](#cb233-8)state 1
[](#cb233-9)bye
[](#cb233-10)state 2
[](#cb233-11)error 3
[](#cb233-12)xyz
[](#cb233-13)error 4
[](#cb233-14)abcd
[](#cb233-15)state 3
[](#cb233-16)zzzzzzzzzz
[](#cb233-17)$ awk '/error/{f=1; buf=$0; next}
[](#cb233-18) f{buf=buf ORS $0}
[](#cb233-19) /state/{if(f) print buf; f=0}' broken.txt
[](#cb233-20)error 2
[](#cb233-21)1234
[](#cb233-22)6789
[](#cb233-23)state 1
[](#cb233-24)error 4
[](#cb233-25)abcd
[](#cb233-26)state 3
```

## 总结

本章涵盖了处理多个记录的各种示例。状态机在推此类此类解决方案方面起着重要作用。了解各种情况也关关，否则适用于一个输入的解决方案在另一个输入上可能会失败。

下一章将讨论根据另一个文件的内容处理文件的情况。

## 练习

**a)** 对于输入文件 `sample.txt`，如果上一行为空且之前的行包含 `you`，则打印包含 `do` 的匹配行。

```
[](#cb234-1)$ awk [在此处添加你的解决方案]
[](#cb234-2)Just do-it
```
```
``` nothing
```

**b)** 对于输入文件 `sample.txt`，分别为搜索词 `do` 和 `not` 打印第二行。不区分大小写地匹配这些词。

```
[](#cb235-1)$ awk [在此处添加你的解决方案]
[](#cb235-2)No doubt you it too
```
``` nothing
```

**c)** 对于输入文件 `sample.txt`，打印匹配的行 `are` 或 `bit` 以及它们周围的 `n` 行。`n` 的值通过 `-v` 选项传递给 `awk` 命令。

```
[](#cb236-1)$ awk -v n=1 [在此处添加你的解决方案]
[](#cb236-2)Good day
[](#cb236-3)How are you
[](#cb236-4)
[](#cb236-5)Today is sunny
[](#cb236-6)Not a bit funny
[](#cb236-7)No doubt you like it too
[](#cb236-8)
# 注意在这种情况下第一行和最后一行是空的
[](#cb236-9)$ awk -v n=2 [在此处添加你的解决方案]
[](#cb236-10)
[](#cb236-11)Good day
[](#cb236-12)How are you
[](#cb236-13)
[](#cb236-14)Just do-it
[](#cb236-15)
[](#cb236-16)Today is sunny
[](#cb236-17)Not a bit funny
[](#cb236-18)No doubt you like it too
```

**d)** 对于输入文件 `broken.txt`，打印标记 `top` 和 `bottom` 之间的所有行。下面显示的第一个 `awk` 命令不起作用，因为如果没有找到第二个标记，它将一直匹配到文件结束。假设输入文件在没有出现 `bottom` 标记的情况下没有两个 `top` 标记，反之亦然。

```
[](#cb237-1)$ cat broken.txt
[](#cb237-2)top
[](#cb237-3)3.14
[](#cb237-4)bottom
[](#cb237-5)
[](#cb237-6)top
[](#cb237-7)123456789
[](#cb237-8)bottom
[](#cb237-9)top
[](#cb237-10)Hi there
[](#cb237-11)Have a nice day
[](#cb237-12)Good bye
[](#cb237-13)$
# 错误输出
[](#cb237-14)$ awk '/bottom/{f=0} f; /top/{f=1}' broken.txt
[](#cb237-15)3.14
[](#cb237-16)123456789
[](#cb237-17)Hi there
[](#cb237-18)Have a nice day
[](#cb237-19)Good bye
[](#cb237-20)$
# 预期输出
[](#cb237-21)$ [在此处添加你的解决方案]
[](#cb237-22)3.14
```

**e)** 对于输入文件 `concat.txt`，从以 `###` 开始的行提取直到包含下一个这样的行。要提取的块通过 `-v` 传递的变量 `n` 指定。

```
[](#cb238-1)$ cat concat.txt
[](#cb238-2)### addr
[](#cb238-3)How are you
[](#cb238-4)This game
[](#cb238-5)Today is sunny
[](#cb238-6)### broken.txt
[](#cb238-7)top
[](#cb238-8)123456789
[](#cb238-9)bottom
[](#cb238-10)### sample.txt
[](#cb238-11)Just do-it
[](#cb238-12)Believe it
[](#cb238-13)### mixed_fs.txt
[](#cb238-14)pink blue yellow
[](#cb238-15)car,mat,ball,basket
[](#cb238-16)$ awk -v n=2 [在此处添加你的解决方案]
[](#cb238-17)### broken.txt
[](#cb238-18)top
[](#cb238-19)123456789
[](#cb238-20)bottom
[](#cb238-21)$ awk -v n=4 [在此处添加你的解决方案]
[](#cb238-22)### mixed_fs.txt
```

**f)** 对于输入文件 `ruby.md`，将所有出现的 `ruby`（不区分大小写）替换为 `Ruby`。但是，不要替换 ``` ```ruby ``` 和 ``` ```` 行之间的任何匹配项（这些标记中的 ruby 也不应该被替换）。

```
[](#cb239-1)$ awk [在此处添加你的解决方案] ruby.md > out.md
[](#cb239-2)$ diff -sq out.md expected.md
```





```
下方解决方案中使用的 `key` 特性：

*   对于两个输入文件，仅当正在处理第一个文件时 `NR==FNR` 才会为 `true`
*   `next` 将跳过剩余代码并获取下一个记录
*   `a[$0]` 本身是一个有效语句。它会在数组 `a` 中创建一个以 `$0` 为键的未初始化元素（假设该键尚不存在）
*   `$0 in a` 检查给定字符串（此处为 `$0`）是否存在作为数组 `a` 的键
```

### 常见行示例

```
# 等同于：`grep -Fxf color_list1.txt color_list2.txt`

awk 'NR==FNR{a[$0]; next} $0 in a' color_list1.txt color_list2.txt
```
浅蓝色

黄色

# color_list2.txt 中存在但 color_list1.txt 中不存在的行

```
# 等同于：`grep -vFxf color_list1.txt color_list2.txt`

awk 'NR==FNR{a[$0]; next} !($0 in a)' color_list1.txt color_list2.txt
```
黑色

深绿色

# 反转输入文件的顺序可以得到

```
# color_list1.txt 中存在但 color_list2.txt 中不存在的行

awk 'NR==FNR{a[$0]; next} !($0 in a)' color_list2.txt color_list1.txt
```
青蓝色

绿色

> ![warning](img/file1.svg) 注意，如果第一个文件为空，`NR==FNR` 逻辑将失效。

## 比较字段

在上一节中，你学习了如何比较两个文件之间的记录完整内容。本节将重点于只比较特定的字段。下面的示例文件将作为本节示例中两个输入文件之一。

```
cat marks.txt

Dept    Name    Marks
ECE     Raj     53
ECE     Joel    72
EEE     Moi     68
CSE     Surya   81
EEE     Tia     59
ECE     Om      92
CSE     Amy     67
```

首先，这里有一个单字段比较。问题描述是：如果第一个字段匹配 `dept.txt` 文件中列出的任何部门，则获取 `marks.txt` 中的所有记录。

```
cat dept.txt

CSE
ECE

# 注意先使用 dept.txt 来构建数组键

awk 'NR==FNR{a[$1]; next} $1 in a' dept.txt marks.txt

ECE     Raj     53
ECE     Joel    72
CSE     Surya   81
ECE     Om      92
CSE     Amy     67

# 如果也需要表头

awk 'NR==FNR{a[$1]; next} FNR==1 || $1 in a' dept.txt marks.txt

Dept    Name    Marks
ECE     Raj     53
ECE     Joel    72
CSE     Surya   81
ECE     Om      92
CSE     Amy     67
```

对于多字段比较，你需要构建一个健健的键。简单连接字段值可能会导致误匹配。例如，字段值 `abc` 和 `123` 会错误地匹配 `ab` 和 `c123`。为了避免这种情况，你可以在字段值之间引入一些字符串，例如 `"_"`（如果你确定字段本身不会包含该字符）或 `FS`（更安全的选项）。你也可以允许 `awk` 帮你处理。如果你在字段值之间使用 `,` 符号（而不是字符串 `","`），则会插入特殊变量 `SUBSEP` 的值。`SUBSEP` 的默认值是非打印字符 `\034`，该字符通常不作为文本的一部分。

```
cat dept_name.txt

EEE Moi
CSE Amy
ECE Raj

# 使用 SUBSEP 作为字段值之间的分隔符
# 注意键上使用了括号

awk 'NR==FNR{a[$1,$2]; next} ($1,$2) in a' dept_name.txt marks.txt

ECE     Raj     53
EEE     Moi     68
CSE     Amy     67
```

在这个例中，其中一个字段被用于数值比较。

```
cat dept_mark.txt

ECE 70
EEE 65
CSE 80

# 匹配 dept_mark.txt 中指定的部门和最低分数

awk 'NR==FNR{d[$1]=$2; next} $1 in d[$1]' dept_mark.txt marks.txt

ECE     Joel    72
EEE     Moi     68
CSE     Surya   81
ECE     Om      92
```

这是一个添加新字段的示例。

```
cat role.txt

Raj class_rep
Amy sports_rep
Tia placement_rep

awk -v OFS='\t' 'NR==FNR{r[$1]=$2; next} $(NF+1) = FNR==1 ? "Role" : r[$2]} 1' role.txt marks.txt

Dept    Name    Marks   Role
ECE     Raj     53      class_rep
ECE     Joel    72
EEE     Moi     68
CSE     Surya   81
EEE     Tia     59      placement_rep
ECE     Om      92
CSE     Amy     67      sports_rep
```

## getline

顾名其实，`getline` 函数允许你按需从文件中读取行。当你需要基于行号进行操作时非常有用。以下示例展示了如何用另一个文件的 `n` 行替换某个文件的 `m` 行。`getline` 有许多语法变体，此处读取的行保存在变量中。

```
# 此处未显示返回值，但理想情况下应该这样做

awk -v m=3 -v n=2 'BEGIN{while(n-- > 0) getline s < "greeting.txt"} FNR==m{$0=s} 1' table.txt

brown bread mat hair 42
blue cake mug shirt -7
Have a nice day
```

这是一个同时处理两个文件的示例。在这种情况下也使用了 getline 的返回值。如果成功读取行，它将返回 `1`；如果没有更多输入（到达文件末尾），则返回 `0`；如果发生错误，则返回 `-1`。特殊变量 `ERRNO` 将包含有关问题的详细信息。

```
# 如果 table.txt 中对应行的最后一列是正数
# 则打印 greeting.txt 中的行

awk -v file='table.txt' '(getline line < file)==1{n=split(line, a); if(a[n]>0) print}' greeting.txt

Hi there
Good bye
```

如果传递作为 `awk` 命令参数的文件无法打开，你将得到错误。例如：

```
awk '{print $2}' xyz.txt
awk: fatal: cannot open file 'xyz.txt' for reading (No such file or directory)
```

建议在使用 `getline` 时始终检查返回值，或者也许可以使用之前节的技术完全避免使用 `getline`。

```
# xyz.txt 不存在，但输出没有显示发生错误

awk '{getline line < "xyz.txt"; print $NF, line}' table.txt

42 
-7 
3.14 

awk -v file='xyz.txt' '{ e=(getline line < file); if(e<0){print file ": " ERRNO; exit} print $NF, line }' table.txt

xyz.txt: No such file or directory
```




> ![info](img/file0.svg) 查看 [gawk 手册：getline](https://www.gnu.org/software/gawk/manual/gawk.html#Getline) 获取详情，特别是关于边界情况和错误。另另 [awk.freeshell:getline 注意](https://awk.freeshell.org/AllAboutGetline)。

## 总结

本章讨论了需要比较两个文件内容的几种情况。`NR==FNR` 技巧对于此类情况非常有用。`getline` 函数对于基于行号的比较很有帮助。

下一章将讨论如何处理重复内容。

## 练习

**a)** 使用 `match_words.txt` 文件的内容显示 `jumbled.txt` 和 `sample.txt` 中的匹配行。匹配标准是：这些文件中行的第二个单词应匹配 `match_words.txt` 文件中行的第三个单词。

```
[](#cb251-1)$ cat match_words.txt
[](#cb251-2)%whole(Hello)--{doubt}==ado==
[](#cb251-3)just,\joint*,concession<=nice
[](#cb251-4)
[](#cb251-5)$ # 'concession' 是 'match_words.txt' 中的第三个单词之一
[](#cb251-6)$ # 也是 'jumbled.txt' 中的第二个单词
[](#cb251-7)$ awk ##### 在此处添加你的解决方案
[](#cb251-8)wavering:concession/woof\retailer
[](#cb251-9)No doubt you like it too
```

**b)** 如所示，将 `secrets.txt` 的内容与通过 `-v` 选项传递的文件内容交错排列。

```
[](#cb252-1)$ awk -v f='table.txt' ##### 在此处添加你的解决方案
[](#cb252-2)stag area row tick
[](#cb252-3)brown bread mat hair 42
[](#cb252-4)---
[](#cb252-5)deaf chi rate tall glad
[](#cb252-6)blue cake mug shirt -7
[](#cb252-7)---
[](#cb252-8)Bi tac toe - 42
[](#cb252-9)yellow banana window shoes 3.14
[](#cb252-10)---
```

**c)** 文件 `search_terms.txt` 每行包含一个搜索字符串（这些字符串不包含正则元字符）。构造一个 `awk` 命令，读取该文件并显示在所有其他文件参数中找到的术语（忽略大小大小）。注意，这些术语应匹配行的任何部分，而不仅仅是整个单词。

```
[](#cb253-1)$ cat search_terms.txt
[](#cb253-2)hello
[](#cb253-3)row
[](#cb253-4)you
[](#cb253-5)is
[](#cb253-6)at
[](#cb253-7)
[](#cb253-8)$ awk ##### 在此处添加你的解决方案
[](#cb253-9)##file list## search_terms.txt jumbled.txt mixed_fs.txt secrets.txt table.txt
[](#cb253-10)at
[](#cb253-11)row
[](#cb253-12)$ awk ##### 在此处添加你的解决方案
[](#cb253-13)##file list## search_terms.txt addr.txt sample.txt
[](#cb253-14)is
[](#cb253-15)you
[](#cb253-16)hello
```

# 处理重复项

通常，你需要从输入文件中消除重复项。这可以基于整行内容，也可以基于某些字段。这些问题通常通过 `sort` 和 `uniq` 命令解决。使用 `awk` 的优势包括：基于正则表达式的字段和记录分隔符、输入不需要排序，并且由于它是一门编程语言，通常更具活性。

## 整行重复

`awk '!a[$0]++'` 是最著名的 `awk` 单行命令之一。它在保留输入顺序的同时消除了基于行的重复项。接下来的示例展示了它的用法，并说明了其逻辑的工作原理。

```
[](#cb254-1)$ cat purchases.txt
[](#cb254-2)coffee
[](#cb254-3)tea
[](#cb254-4)washing powder
[](#cb254-5)coffee
[](#cb254-6)toothpaste
[](#cb254-7)tea
[](#cb254-8)soap
[](#cb254-9)tea
[](#cb254-10)
[](#cb254-11)$ awk '{print +a[$0] "\t" $0; a[$0]++}' purchases.txt
[](#cb254-12)0       coffee
[](#cb254-13)0       tea
[](#cb254-14)0       washing powder
[](#cb254-15)1       coffee
[](#cb254-16)0       toothpaste
[](#cb254-17)1       tea
[](#cb254-18)0       soap
[](#cb254-19)2       tea
[](#cb254-20)
[](#cb254-21)$ # 只有第一列为零的条目会被保留
[](#cb254-22)$ awk '!a[$0]++' purchases.txt
[](#cb254-23)coffee
[](#cb254-24)tea
[](#cb254-25)washing powder
[](#cb254-26)toothpaste
[](#cb254-27)soap
```

## 列重复

对于单字段比较，删除基于字段的重复非常简单。只需在设置相应的字段分隔符后，将 `$0` 更改所需的字段编号即可。

```
[](#cb255-1)$ cat duplicates.txt
[](#cb255-2)brown,toy,bread,42
[](#cb255-3)dark red,ruby,rose,111
[](#cb255-4)blue,ruby,water,333
[](#cb255-5)dark red,ruby,rose,111
[](#cb255-6)blue,ruby,water,333
```




# 2 个苹果

加油

```bash
$ awk ##### 在此处添加你的解决方案
```

去就吧

加油

---

## 2 个苹果和 5 个芒果

加油！

2 个苹果

### b) 针对输入文件 `lines.txt`，仅保留每行的第一个副本。假设空格作为字段分隔符，每行有两个字段。在比较行内容时不考虑字段的顺序。例如，`hehe haha` 和 `haha hehe`将被视为重复项。

```bash
cat twos.txt
hehe haha
door floor
haha hehe
6;8 3-4
true blue
hehe bebe
floor door
3-4 6;8
tru eblue
haha hehe

$ awk ##### 在此处添加你的解决方案
hehe haha
door floor
6;8 3-4
true blue
hehe bebe
tru eblue
```

### c) 针对输入文件 `twos.txt`，创建一个包含所有唯一行的文件 `uniq.txt` 以及一个包含所有重复行的文件 `dupl.txt`。假设空格作为字段分隔符，每行有两个字段。在比较行内容时不考虑字段的顺序。例如，`hehe haha` 和 `haha hehe`将被视为重复项。

```bash
awk ##### 在此处添加你的解决方案

$ cat uniq.txt
true blue
hehe bebe
tru eblue

$ cat dupl.txt
hehe haha
door floor
haha hehe
6;8 3-4
floor door
3-4 6;8
haha hehe
```

# awk 脚本

## -f 选项

`-f` 命令行选项允许你通过文件传递 `awk` 代码，而不是将所有代码写在命令行中。这里是之前看到的一个单行命令转换为多行脚本的形式。注意，不再需要用 `;` 来分隔命令，换行符也可以。

```bash
$ cat buf.awk
/error/{
    f = 1
    buf = $0
    next
}

f{
    buf = buf ORS $0
}

/state/{
    if(f)
        print buf
    f = 0
}

$ awk -f buf.awk broken.txt
error 2
1234
6789
state 1
error 4
abcd
state 3
```

另一个优势是可以自由使用单引号。

```bash
$ echo 'cue us on this example' | awk -v q="'" '{gsub(/\w+/, q "&" q)} 1'
'cue' 'us' 'on' 'this' 'example'

# 上面的解决方案写成脚本更简单
$ cat quotes.awk
{
    gsub(/\w+/, "'&'")
}

1

$ echo 'cue us on this example' | awk -f quotes.awk
'cue' 'us' 'on' 'this' 'example'
```

## -o 选项

如果代码已经在命令行上测试过，可以添加 `-o` 选项来获取美化输出的版本。输出文件名可以通过 `-o` 选项传递，否则默认将使用 `awkprof.out`。

```bash
# 在测试过单行命令后添加 -o
$ # 输入文件名和 -v 将被简单忽略
$ awk -o -v OFS='\t' 'NR==FNR{a[$0]=$1;next}if(!($0 in a))print $0}' lines.txt
```





```bash
# 静默失败，由于字符串到数字的转换，$word 变成了 $0
awk -v word="cake" '$2==$word' table.txt
# 当变量使用正确时可以工作
awk -v word="cake" '$2==word' table.txt
blue cake mug shirt -7
# 在这里 'field' 被替换为 '2'，因此打印 $2
awk -v field=2 '{print $field}' table.txt
bread
cake
banana
```

## Dos 风格行结束

如前所述，行结束在不同平台之间有所不同。在 Windows 上，行结束通常是回车符和换行符的组合，被称为 `dos style` 行结束。由于 `GNU awk` 允许多字符的 `RS`，因此处理起来很容易。请参考 [stackoverflow: 为什么我的工具输出会覆盖自身，我该如何修复它？](https://stackoverflow.com/q/45772525/4082052) 获取详细讨论和各种缓解方法。

```bash
# unix 风格行结束没有问题
printf 'mat dog\n123 789\n' | awk '{print $2, $1}'
dog mat
789 123
# dos 风格行结束会导致麻烦
printf 'mat dog\r\n123 789\r\n' | awk '{print $2, $1}'
 mat
123
printf 'mat dog\r\n123 789\r\n' | awk '{sub(/$/, ".")} 1'
.at dog
.23 789
# 如果你想用同一个命令同时处理 unix 和 dos 风格，请使用 \r?\n
# 注意 ORS 仍然仅为换行符
printf 'mat dog\r\n123 789\r\n' | awk -v RS='\r\n' '{print $2, $1}'
dog mat
789 123
printf 'mat dog\r\n123 789\r\n' | awk -v RS='\r\n' '{sub(/$/, ".")} 1'
mat dog.
123 789.
```

## 当字符串包含换行符时 ^ 和 $ 的行为

在某些正则表达式实现中，`^` 匹配行首，`$` 匹配行尾（以换行符作为行分隔符）。在 `awk` 中，这些锚点始终匹配整个字符串的开头和整个字符串的结尾。当 `RS` 不是换行符时，或者你有一个包含换行符的字符串值时，这种情况就会发生作用。

```bash
# 'apple\n' 不匹配，因为有换行符
printf 'apple\n,mustard,grape,\nmango' | awk -v RS=, '/e$/'
grape
# '\nmango' 不匹配，因为有换行符
printf 'apple\n,mustard,grape,\nmango' | awk -v RS=, '/^m/'
mustard
```

## 单词边界差异

单词边界 `\y` 同时匹配单词位置的开始和结束。而，`\<` 和 `\>` 分别精确匹配单词位置的开始和结束。这导致你必须根据所需的结果选择这些单词边界中的某一个。以 `I have 12, he has 2!` 作为样本文本，如下图所示，图中用竖线标记了单词边界。最后一个字符 `!` 没有单词结束边界，因为它不是单词字符。

![word boundary](img/file2.png)

```bash
# \y 同时匹配单词边界的开始和结束
# 这里的第一次匹配使用了 'I' 和 'have' 的起始边界
echo 'I have 12, he has 2!' | awk '{gsub(/\y..\y/, "[&]")} 1'
[I ]have [12][,he] has [2]!
# \< 和 \> 只匹配单词的开头结束边界
echo 'I have 12, he has 2!' | awk '{gsub(/\<..\>/, "[&]")} 1'
I have [12], [he] has 2
```

这里是另一个示例展示了两种单词边界之间的差异。

```bash
# 在单词的开始/结束添加某些内容
echo 'hi_42 12b' | awk '{gsub(/\y/, ":")} 1'
hi:42:12b:
# 只在单词开头添加某些内容
echo 'hi_42 12b' | awk '{gsub(/\</, ":")} 1'
:hi_42 12b
# 只在单词结束添加某些内容
echo 'hi_42 12b' | awk '{gsub(/\>/, ":")} 1'
hi_42:12b
```

## 依赖默认值

未初始化的变量是有用的，但有时当你将单个文件转换为多个文件时，它们的转换并不理想。你必须找出哪些变量在处理每个文件开始时需要重置。

```bash
# 步骤 1 - 适用于单文件
awk '{sum += $NF} END{print sum}' table.txt
38.14
# 步骤 2 - 准备代码适用于多个文件
awk '{sum += $NF} ENDFILE{print FILENAME ":" sum}' table.txt
table.txt:38.14
# 步骤 3 - 使用多个文件输入检查
# 哎，sum 的默认数值值 '0' 仅作用一次
awk '{sum += $NF} ENDFILE{print FILENAME ":" sum}' table.txt
table.txt:38.14
marks.txt:50.14
# 步骤 4 - 正确初始化变量
awk '{sum += $NF} ENDFILE{print FILENAME ":" sum; sum=0}' table.txt
table.txt:38.14
marks.txt:42
```

## 替换部分的代码

替换函数的替换部分接受任何表达式，并在需要时转换为字符串。如果正则表达式没有匹配输入字符串，但表达式可以更改变量的值（例如增减运算符）会怎样？好吧，表达式仍然会被执行，这可能不是你想要的。

```bash
# 第二行没有匹配，但 'c' 仍然被修改了
awk '{sub(/^(br|ye)/, ++c ") &")} 1' table.txt
1) brown bread mat hair 42
blue cake mug shirt -7
3) 
# 在应用替换之前检查匹配行
# 这有助于简化替换的正则表达式
# 或者，你可以将正则表达式保存在变量中以避免重复
awk '/^(br|ye)/{sub(/^/, ++c ") ")} 1' table.txt
1) brown bread mat hair 42
blue cake mug shirt -7
2) yellow window shoes 3.14
```

此外，表达式每个函数调用执行一次，而不是每次匹配执行一次。

```bash
# 第一行有两个匹配，但 'c' 只被修改一次
awk '{gsub(/\<b/, ++c ") &")} 1' table.txt
1) brown 1) bread mat hair 42
2) blue cake mug shirt -7
yellow banana3) 3.14
```

## 强制字符串上下文

连接空字符串以强制进行字符串比较。





```bash
# 为了清晰起见，第一个参数使用了括号
# 字段在这里作为数字进行比较
echo '5 5.0' | awk '{print ($1==$2 ? "same" : "different"), "number"}'
same number

# 字段在这里作为字符串进行比较
echo '5 5.0' | awk '{print ($1""==$2 ? "same" : "different"), "string"}'
different string
```

## 负数 NF

操作 `NF` 有时会导致负值。幸运的是，`awk` 会抛出错误而不是像未初始化变量那样运行。

```bash
# 字段数量不同的文件
cat varying.txt
parrot
good cool awesome
blue sky
12 34 56 78 90

# 删除最后两个字段
awk '{NF -= 2} 1' varying.txt
awk: cmd. line:1: (FILENAME=varying.txt FNR=1) fatal: NF set to negative value

# 添加条件来检查字段数量
# 假设字段少于 3 的行应该被保留
awk 'NF>2{NF -= 2} 1' varying.txt
parrot
good
blue sky
12 34 56
```

这里是另一个示例，需要访问倒数第三字段。

```bash
awk '{print $(NF-2)}' varying.txt
awk: cmd. line:1: (FILENAME=varying.txt FNR=1) fatal: attempt to access field -1

# 仅当至少有 3 个字段时打印
awk 'NF>2{print $(NF-2)}' varying.txt
good
56
```

## 更快的执行

将区域设置（locale）更改为 ASCII（假设当前区域不是 ASCII 且输入文件仅包含 ASCII 字符）可以显著提高速度。使用 `mawk` 是另一种加速执行的方法，只要你没有使用 `GNU awk` 的特定功能。在其他功能差异中，`mawk` 不支持 `{}` 形式的量符，详情请参见 [unix.stackexchange: 如何在 mawk 中指定正则量符？](https://unix.stackexchange.com/q/506119/109046)。另请参阅 [wikipedia: awk 版本与实现](https://en.wikipedia.org/wiki/AWK_programming_language#Versions_and_implementations)。

```bash
# 显示的时间为多次运行的最优结果
# 速度收益将取决于计算资源、输入等
# /usr/share/dict/words 包含字典词汇，每行一个
time awk '/^([a-d][r-z]){3}$/' /usr/share/dict/words > f1
real    0m0.029s

time LC_ALL=C awk '/^([a-d][r-z]){3}$/' /usr/share/dict/words > f2
real    0m0.022s

time mawk '/^[a-d][r-z][a-d][r-z][a-d][r-z]$/' /usr/share/dict/words > f3
real    0m0.009s

# 检查结果是否相同
diff -s f1 f2
Files f1 and f2 are identical
diff -s f2 f3
Files f2 and f3 are identical
# 清理临时文件
rm f1
```

这里是另一个示例。

```bash
# 统计恰好 3 个小写的 'a'
time awk -F'a' 'NF==4{cnt++} END{print cnt}' /usr/share/dict/words
real    0m0.034s

time LC_ALL=C awk -F'a' 'NF==4{cnt++} END{print cnt}' /usr/share/dict/words
real    0m0.023s

time mawk -F'a' 'NF==4{cnt++} END{print cnt}' /usr/share/dict/words
real    0m0.014s
```

## 扩展阅读

- `man awk`、`info awk` 以及 [在线手册](https://www.gnu.org/software/gawk/manual.html)
- 关于 `awk` 各种实现的信息
    - [awk FAQ](http://www.faqs.org/lang/faq/) — 极好的资源，最后修改于 2002 年
    - [grymoire: awk 教程](https://grymoire.com/Unix/Awk.html) — 涵盖了不同 `awk` 版本的信息
    - [awk/nawk 速查表](https://catonmat.net/ftp/awk.cheat.txt)
- stackoverflow/stackexchange 上的问答是很好的学习材料，适合练习
    - [stackexchange 上的 awk 问答](https://unix.stackexchange.com/questions/awk?sort=votes&15)
    - [stackoverflow 上的 awk 问答](https://stackoverflow.com/questions/awk?sort=15)
- 学习正则表达式（包含 POSIX 以外的信息）
    - [regular-expressions](https://www.regular-expressions.info/) — 教程与工具
    - [rexegg](https://rexegg.com/) — 技巧及更多
    - [stackoverflow: 这个正则表达式是什么意思？](https://stackoverflow.com/q/22937618)
    - [在线正则测试器和调试器](https://regex101.com/) — 不完全适用于命令行工具，但大多数 POSIX 语法均适用
- [我关于 CLI 文本处理的仓库](https://github.com/learnbyexample/Command-line-processing)
- 相关工具
    - [GNU datamash](https://www.gnu.org/software/datamash/)
    - [bioawk](https://github.com/lh3/bioawk)
    - [frawk](https://github.com/ezros/frawk) — 基于 Rust 的高效 awk
    - [hawk](https://github.com/gelisam/hawk/blob/README.md) — 基于 Haskell
    - [miller](https://github.com/johnkerl/miller) — 类 awk/sed/join，用于表格化数据
        - 关于此类工具的 [讨论](https://newsycombinator.com/item=100672)
- 杂项
    - [stackexchange: 什么时候用 grep, sed, awk, perl](https://unix.stackexchange.com/q/303044)
    - [awk-libs](https://github.com/e36freak/awk-libs) — 许多实用函数
    - [awkaster](https://github.com/TheMozg/awk-raycaster) — 完全用 awk 编写的伪 3D 游戏
    - [awk](https://awk.js/) — 浏览器在线编辑器
- ASCII 参考与区域设置使用
    - [ASCII 代码表](https://ascii.cl/)
    - [archlinux wiki: locale](https://wiki.archlinux.org/index.php/locale)
    - [shellhacks: 定义区域设置与语言](https://www.shellhacks.com/linux-define-locale-language/)
- 本书未涵盖主题示例
    - [stackexchange: rand/srand](https://unix.stackexchange.com/q/372816)
    - [stackexchange: strftime](https://unix.stackexchange.com/q/224969)
    - [stackoverflow: 任意精度整数扩展](https://stackoverflow.com/q/46904447)
    - [stackoverflow: 识别十六进制](https://stackoverflow.com/q/3683110)
    - [stackexchange: sprintf 和文件关闭](https://unix.stackexchange.com/q/223727)
    - [stackexchange: 自定义函数与数组传递](https://unix.stackexchange.com/q/72469)
    - [stackexchange: 根据表头中的字段数量重命名 CSV 文件](https://unix.stackexchange.com/q/408742)

