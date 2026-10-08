
Linux 中没有任何事情必须通过点击完成，这就是终端大显身场的地方。不要对访问命令行感到恐惧——一旦习惯了，你会发现许多技巧，而且通过终端执行效率更高。这里有一份优秀的指南位于

`https://tutorials.org/linuxutorial/` 并且也可以在这些存档中运行教程，并在 `visit.linuxmint.com/archives` 中搜索终端以以 PDF 程序集的形式访问它们。

## 终端：GREP

### 智能模式匹配技巧

自封为 Bash 忍者的 Shashank Sharma 解释了你如何使用 `grep` 搜索文件或话多命令的输出。

典型的 Linux 发行版开箱即自带大量的命令和实用程序，这些可用于执行常规任务，如列出目录、处理文件或执行复制、重命名等操作。

与大多数遵循 Unix 哲学的构建的工具一样，`grep` 只把一件事做好，并且由于其功能单一，典型的 `grep` 语法为 `grep [pattern] filename`。你甚至可以在模式后面指定多个文件，`grep` 将输出每个文件的结果，例如 `grep -wordlookup filename1 filename2`。

**专家**

Shashank Sharma 经验极其丰富，并以精通 Arch Linux 等替代方案而闻名，他在德里作为一名审判律师度过余生……

一个典型的命令将输出指定文件中匹配你模式的每一行。默认情况下，`grep` 会匹配行中的任何部分。

`grep` 最初由 Ken Thompson 编写，它已进入几乎所有的“修复”操作，并且是所有 Linux 发行版默认安装的一部分。进入终端并运行 `man grep` 命令来浏览其帮助页（man page）。

### 基础用法

该工具用于查找指定文件中的模式。你也可以使用 `grep` 过滤 Linux 命令或工具产生的输出，或者通过管道（pipes）进行魔法操作。

如果行不匹配，它将不会显示任何内容。如果你只想匹配 "self" 作为关键词，`grep` 不仅会匹配 "self"，还会匹配 "myself"、"himself" 和 "herself"。如果你想匹配精确单词，请使用带有 `-w` 参数的 `grep`。`grep -w <keyword> filename` 将仅输出精确匹配的结果。

### 与其他工具协作

`grep` 的另一个用途是将其与其他产生大量输出的工具和实用程序结合。例如，当你连接 USB 驱动器或新的蓝牙设备时，`dmesg` 命令会捕捉设备的所有细节。

`dmesg` 命令会生成设备和数据的记录；查看它并不是一种高效的时间利用。你可以使用 `grep` 来查找

#### dmesg grep

```
[199581620 0:00:00.000] [sdb] 15625216 512-byte blocks (8.0 GB/7.5 GB)
[199581641 0:00:00.000] [sdb] Write Protect is off
[199581962 0:00:00.000] [sdb] Mode Sense: 03 00 00
[199581965 0:00:00.000] [sdb] No Caching mode found
[199581970 0:00:00.000] [sdb] Assuming drive cache
[199500329 0:00:00.000] [sdb] Attached SCSI removable disk
```

- `-v` - 只选择不匹配模式的行
- `-A` - 只选择匹配行开头或前面有非单词字符的行
- `-w` - 只选择包含整个单词的行，单词字符是字母、数字和下划线。如果也指定了 `-i`，下划线也没有影响
- `-x` - 只选择与该行完全匹配的行，前后没有字符
- `-c` - 输出匹配行的普通计数
- `-n` - 输出每行匹配行的行号

你可以使用 `-v` 命令作为 NOT 选项。它列出文件中不包含指定关键词的所有行。

### 智能模式匹配教程

运行 `grep` 命令将产生给定文件中匹配你指定模式的所有行。

你同样可以将 `grep` 与 `ps aux` 等命令结合，以获取任何应用程序的详情。如果你在 Debian 或 Ubuntu 系统上，可以将其与 `dpkg -l` 结合列出所有匹配的软件包。例如，`dpkg -l` 命令将列出你系统上的所有。

### 获取上下文

你可能想搜索某些内容，但也想看到它使用的上下文。你可以使用 `grep` 列出匹配模式行之前或周围的行数。`A` 命令用于打印匹配行之后的特定行数。`B` 命令可以打印匹配行之前的行数。`C` 命令同样可以打印匹配行周围的行数。

如果你对上下文好奇并希望查看每个匹配前后的行，可以使用 `-C` 命令。由于终端是彩色，`-B` 和 `-C` 会产生不同的结果以区分每个匹配：你可以使用 `grep` 找出你需要的行。例如，如果你搜索 "wild"，它通常以开头或结尾。这不是错误的（如果它是边缘的）单个 `grep` 命令将返回该单词出现的次数：

```
$ grep -c Documents/LXF-229-tutorial.txt
```

```
$ grep -c Documents/LXF-229-tutorial.txt
```

从下面可以看到，`-C` 选项将显示 "specified" 被使用了四次。在你的搜索字符串或模式上，你可能想结合多个表达式来执行你想要的精确匹配。如果你想用同一个命令搜索多个字符串，必须使用 `grep -E` 命令。此终端将打印包含指定关键词的行。当你想要搜索目录中的所有文件时，可以使用 `-r` 命令。如果你有很多文件，`-r` 选项可能会产生过度使用。考虑使用 `-l` 选项来仅查找匹配关键词的文件：

```
$ grep -l "wild" /Documents/LXF-228-swagart.txt
```

```
$ grep -l Documents/LXF-221-review-knopsix.txt
```

```
$ grep -l Documents/LXF-221-review-korioma.txt
```

如果你使用通配符列出以指定的开头或结尾，

```
Documents/LXF-222-review-archives.txt
Documents/LXF-222-review-server.txt
Documents/LXF-231-review-environments.txt
Documents/LXF-231-review-desktop.txt
Documents/LXF-231-review-archives.txt
Documents/LXF-231-review-environments.txt
Documents/LXF-231-review-server.txt
Documents/LXF-231-review-knopsix.txt
Documents/LXF-232-review-environments.txt
Documents/LXF-232-review-distributions.txt
Documents/LXF-232-review-knopsix.txt
Documents/LXF-232-review-archives.txt
Documents/LXF-232-review-server.txt
Documents/LXF-232-review-distributions.txt
Documents/LXF-232-review-knopsix.txt
Documents/LXF-233-review-environments.txt
Documents/LXF-233-review-archives.txt
Documents/LXF-233-review-server.txt
Documents/LXF-233-review-knopsix.txt
Documents/LXF-233-review-distributions.txt
Documents/LXF-233-review-knopsix.txt
Documents/LXF-233-review-archives.txt
Documents/LXF-233-playground.txt
```

## 快速提示

`grep` 命令可以是区分大小写的，单词 "this" 和 "and" 被视为不同的。使用 `grep` 的 `-i` 选项执行不区分大小写的匹配。

这揭示了给定目录中的所有行，模式仅在文件中找到。如果你想使用 `-l` 命令或其他选项来查找不同文件中匹配行的列表，你也可以使用 `grep -r`。

由于其功能强大，可以使用大量命令来管理和查找用户创建的 `grep` 使用示例，以获取一组接口。随着时间的推移，你将发现它对任何 CLI 工具都有用处。

### 通配符与操作符

在使用 `grep` 进行模式匹配时，你可以使用正则表达式。该命令支持如 `*` 和 `?` 等所有通配符。

方括号为搜索模式提供了额外层级的控制。例如，如果你想找到所有带有小写字母的行（正如一个语法上的虽然），你可以通过 `grep "[a-z]" <filename>` 来实现。所有可能性超出了本教程的范围，但你可以在各种在线资源中找到不同的可能性。

对于操作，你可以使用带有 `-E` 命令的 `grep`。`grep -E "patterning" filename` 将显示匹配模式的所有行。这比标准的 `grep` 更强大。

使用 `|` 符号你可以将第一个 `grep` 命令的输出通道到另一个。例如，如果你有一个列出你作业的文件列表，你想列出包含单词 "writing" 的行。在这里，命令的第一部分将结果限制为 "writing"；命令的第二部分将结果限制为包含该单词的所有行：

# 2020年 Linux 格式年度

# LIBREOFFICE BASIC

## 使用简单的脚本

自动化办公任务

通过 Bobby Moss 关于宏以及所有 Basic 相关知识的实用指南，探索如何重复任务并扩展 LibreOffice 的实用性。

在过去的一年里，这位勤奋的作家已经涵盖了如何充分利用 Calc、Base 和 Impress 等 LibreOffice 应用程序。但如果我们挑战你进一步扩展体验，直到你仍感到意犹未尽呢？

我们并不是要带给你一个想象力匮乏的失败，或者让你对一个关于新手在 Linux 中可能做什么的教程而感到后悔。本期内容将帮助你以以前从未计划过的方式扩展 Calc 和 Writer 的功能。

在 Writer 中创建模板，或者在 Excel 中移动几十个单元格和工作表，仅仅通过记录所有繁琐的手动步骤是不够完成任务的；你将学习如何使用一种易于学习且性能优秀的语言和纯英语语法对它们进行编程。

别担心，我们并不害怕源代码会丢失几行代码。使用 `Dim` 来声明变量，例如：`Sub Routine As "String" Format`。本教程将帮助你创建自己的宏，我们将使你能够在文档中记录重复性任务。你记录的步骤可以完成从预填充可打印表单值之类的任何任务。

Basic 的另一个巨大优势是遗留兼容性。自从我们很久在 OpenDF 讨论这个话题以来，所有年轻的提升都已经开始；过去的佳作是对未来的任何预言；你今天学到的知识可能帮助你在未来几十年内都能写好文档。

## 开始记录

想象你正在写一封新信。每次你都必须对文本右对齐并输入你的地址，然后再次左对齐输入收件人地址。如果你找到了 `工具>宏>运行宏`，你就可以执行这些操作，然后点击停止将其保存为宏。

现在，每当你想要创建一个信件时，都必须前往 `工具>宏>运行宏...` 并选择`开始列表`来重复记录的事件序列。如果你发现`记录`选项丢失，你需要前往 `工具>选项>LibreOffice=高级`。

## 函数 (FUNCTION SUB)

Bobby Moss 为虚拟化和 Linux 编写文档。在空余时间，他致力于一系列免费项目。

LibreOffice 中有两种变量：全局变量定义在模块文件中，可以被任何子程序或函数内部使用。局部变量仅在声明它的子程序内部使用。按照惯例，使用 `Dim` 来声明相应类型的变量，例如：

```basic
Sub MyRoutine(Parameter As String) Format
Dim myLocalVariable = "Issue"
print myString
print myVariable
print myParameter
End
```

新程序员常犯的错误是混淆了子程序（sub）和函数（function）。两者都接受参数（你提供的输入），按预定的顺序执行操作并更改全局变量的值。关键区别在于函数会返回一个值供使用，而子程序不需要。在下面的示例中，你可以看到第 1 行有一个函数，以及：

1. `result = myFunction(1,2)`
2. `MySubroutine("#239")`

| 菜单 | 工具 | 右键菜单 | 键盘 | 事件 |
|---|---|---|---|---|
| 快捷键 | | | | |
| Shift+ Insert | | | | |
| Shift+ Delete | | | | |
| Ctrl+1 | | 单元格格式 行间距: 1.5 | | |
| Ctrl+2 | | 单元格格式 行间距: 1.5 | | |
| Ctrl+3 | | 单元格格式 行间距: 1.5 | | |
| Ctrl+4 | | 单元格格式 行间距: 1.5 | | |
| Ctrl+5 | | 单元格格式 行间距: 1.5 | | |
| Ctrl+6 | | 单元格格式 行间距: 1.5 | | |
| Ctrl+7 | | 单元格格式 行间距: 1.5 | | |
| Ctrl+8 | | 单元格格式 行间距: 1.5 | | |
| Ctrl+9 | | 单元格格式 行间距: 1.5 | | |

你可以通过在 LibreCustom... 中设置，从不同的键组合和自定义菜单项运行你编写的任务...

## 自动化办公任务教程

然而，这加速了你的工作流。幸运的是，你可以将宏绑定到按键、菜单选项或工具栏上。在这种特定情况下，从键盘启动宏比点击几十个子菜单要快得多。

要实现这一点，你可以从 `工具>键盘` 进行设置。然后你可以找到一个未被使用的快捷键并将其链接到你的`开始宏`。这比替换现有的宏要好，以防你以后发现需要它们。

如果你更喜欢将`开始宏`绑定到菜单项，可以从 `工具>自定义...` 完成，然后选择`菜单`选项卡。双击`我的宏`找到`开始 Office`。

一旦你从右侧下方选择`工具`然后点击 `+` 为 Basic 代码添加新的菜单快捷键。之后，你会发现可以按照意愿从 `Office>开始` 启动宏。

你还可以将宏绑定到上下文或应用程序事件。写信时你不需要探索这些任何选项，但你会发现这加速了你的-工作流。

# 2020年度 Linux 格式

# 快速贴士

如果你觉得这些屏幕中的图标很有吸引力，可以从 Linux 中的 'libreoffice-style' 主题安装它们。也可以通过选择“选项 -> 视图”来启用深色图标。

`doc=loadComponentFromUrl(fileLaunch,"blank",0,Dummy(0))`

如果你尝试运行此代码且参数不是对象，那么错误位于调试之前的 Main 的子标题中。解释器将其识别为起点，且 `loadNewSubtitle` 将为 `FileTitle` 赋值，这通常对于启动它的 Main 框架来说也是意义的。

8 我们可以将该公式传递给 `SUM(A1:A3)`，它将在第一张工作表中输出 A1、A2 和 A3 的总和。

然而，Basic 并不需要依赖 Calc 来进行计算。你只需要将第二行调整为如下内容：

```
Dim valueA As Integer, valueB As Integer
valueA=cell
valueB=3
cell=valueA+valueB
```

每当你从 Basic 执行此操作时，它会在 B 单元格的值上加 3。如果你需要执行不同的计算，可以将 `+` 替换为 `-`、` * ` 或 `/` 以进行减、乘、除。如果你想返回最接近的整数，可能需要将数据类型从 `Integer` 改为 `Double`。

那么，如果在 LibreOffice 中不起作用会怎样？Main 子标题会触发 `loadNewSubtitle`，因此它作为 Main 框架的值进行扩展。

你可能有的下一个问题是：“如果单元格包含文本字符串而不是整数怎么办？”你会遇到一个料之外的错误，幸运的是，你可以在 `Sub math::` 之前添加以下行来修复它。

# 快速贴士

通过切换到 Toad-Macro 可以更快地加载编辑器。或者，按下 Shift+F1 将加载此表后面包含的宏。

`On Error GoTo error`

除非你在一个名为 `error` 的标签下放置了指令，否则此 LibreOffice Basic 将显示发生了错误。要使其工作，你应该在 `End` 之前添加两行：

```
print "error has occurred"
```

该命令将创建一个带有你生成的错误信息的对话框。对于旧版本和新版本的 LibreOffice，你可能需要使用以下行：

```
msgbox "error has occurred",
```

那么，如果在 LibreOffice 中正常工作会怎样？

# 数学公式

一旦你从表中提取了一些代码，就是时候在你自己的工作表中使用它们。

# Sub math

```
Dim sheetA As Object, cell As Object

sheetA=Sheets.get("Sheet1")

cell=sheetA.getCellByPosition(1,0)

cell.formula=cell.value+5
```
