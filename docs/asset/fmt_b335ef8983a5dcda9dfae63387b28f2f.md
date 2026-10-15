
```
Sub Statistics
  '此子程序显示关于'
  '文本文档的统计信息
  '定义变量来存储统计信息
  dim NumberOfChars as long, NumberOfLines as long
  dim NumberOfGraphics as integer, NumberOfTables as integer

  '检查文本文档是否活动
  IF ActiveModule.Name = 'StarWriter' THEN
    '如果不是，则弹出错误消息并退出此子程序
    MsgBox("此程序仅在文本文档可用。",0+16, "Error")
  End Sub
14 END

15 'CollectChars = ActiveWindow.GetCharCount(2)

16 NumberOfChars = ActiveWindow.GetLineCount( FALSE )

17 NumberOfLines = ActiveWindow.Graphics.Count
18 NumberOfTables = ActiveWindow.Tables.Count

20 '在消息框中显示信息

21 MsgBox( '字符数: ' & NumberOfChars &

22 '行数: ' & NumberOfLines &

23 '图形数: ' & NumberOfGraphics & chr(13) & _
24 '表格数: ' & NumberOfTables & chr(13) & _

25 +64, '此文档的统计信息'
26 End Sub
```

它应该会产生一个类似图 37.12 所示的消息框。

# 图 37

所有的编程工作——这里就是结果，一个告知你文档统计信息的消息框。

![](img/c7707891f0fd9d25e29944c84d432772_1297_0.png)

如果宏产生带有“此程序仅在文本文档可用”警告的消息框，则在运行宏时没有活动的文档文本。当你在 StarBasic IDE 中运行宏时，也会得到此错误消息。

以下是 `Statistics` 程序的详细拆解：

- 第 1 行和第 28 行是实际构建程序的代码；它们是一个告知 StarBasic “子程序在此开始/结束”的框架。`Sub` 语句、后跟的语句块以及 `End` 语句定义了一个子程序。在示例中，该子程序是一个完整的 StarBasic 程序。然而，子程序的目的是执行程序中许多功能中的某一个功能。
- 第 2 行和第 3 行描述了程序的功能。良好的做法是在子程序的开头描述该过程的功能以及它所使用的过程。每一行以单引号（’）开头的行都会被 StarBasic 解释器忽略。
- 第 6 行和第 7 行定义了存储程序收集的统计信息的四个变量。变量是存储特殊类型数据的专用位置。`NumberOfChars` 和 `NumberOfLines` 是 `long` 类型的变量，用于存储大于 32,767 的整数。`NumberOfGraphics` 和 `NumberOfTables` 是 `integer` 类型的变量，用于存储较小的数字。然而，你可以给变量命名为任何名称——例如 Fred。但是，变量名与其设计的任务相对应最好。
- 第 10 行到第 14 行是所谓的“决策块”（decision block）的一部分。如果当前活动文档不是文本文档，宏将无法运行。如果你从电子表格或 StarBasic IDE 运行宏，它将无法访问统计信息。因此，程序会抛出错误。为了防止这种情况，程序需要检查是否为 StarWriter。
- 第 20 行到第 22 行为变量赋值。
- 第 22 行到第 27 行是打开消息框对话框的一个命令的一部分。注意第 12 行也出现了一个消息框；然而，它只是一行代码。由于第二条消息需要显示这么多信息，它使用了通过下划线字符连接的五行。你可以将这样的命令写在一行中，但将很难理解。将代码分为五行更具可读性（这也是书中编写代码的唯一方式）。

## 第 37 章 熟悉 StarBasic

StarBasic 是不区分大小写的；表达式可以是小写，也可以是大写。例如，如果你调用一个变量 `NumberOfChars`，你可以输入 `numberofchars` 或 `NUMBERCHARS`，解释器都能识别它。你甚至可以用小写或大写输入 StarBasic 关键字。

StarBasic 在括号的使用或省略上也非常灵活。请仔细看下面的示例：

```
Sub Main
'以下行不需要括号：
ToShowName "Scott", "Peter"
'相同的命令仅加了括号：
ToShowName("Scott", "Peter")
```

```
'在下面这一行中，SumArgs 命令必须使用括号。
'否则，StarBasic 不知道哪些参数属于
'Msgbox 和 SumArgs
MsgBox SumArgs(10, 20)
'注意，我们使用 MsgBox 运行时函数时没有使用括号！
 End
```

```
Sub ShowName(Lastname as string, FirstName as string)
MsgBox FirstName & " " & Lastname, 64, "Your Name here"
 End Sub
```

```
Function SumArgs(a as integer, b as integer) as integer
SumArgs = a + b
 End Function
```

注意，`SumArgs` 的参数 `a` 和 `b` 是在括号内的。如果你想将函数的结果赋值给变量，使用括号是必不可少的。为了避免差异，请始终为参数加上括号。

### 我必须处理这些对象吗？

前面的章节包含了大量对 StarOffice 对象的引用。到这里，你可能在好奇对象到底是什么，是否真的需要在 StarBasic 中了解它们。接下来的章节将解释什么是 StarOffice 对象。

### 什么是 StarOffice 对象？

StarOffice 的所有函数和属性都通过对象层次结构表示。使用鼠标格式化的常用方法是选择 Format，然后会出现对话框。然而，如果你想在 StarBasic 程序中打开相同的对话框，可以使用以下命令：

```
ActiveWindow.Font.Dialog()
```

因此，`Dialog()` 方法属于 `Font` 对象，而 `Font` 是 `ActiveWindow` 的属性。`ActiveWindow` 是引用当前活动窗口的对象。

## 从零开始 STARBASIC 编程

查看文本的属性。以下命令为选中的文本添加下划线：

```
ActiveWindow.Font.Underline = 1
```

点击对象栏中的 Underline 按钮也可以为选中的部分添加下划线。然而，区别在于，无论是否已下划，该命令都会更改 `ActiveWindow.Font` 的值。

正如你所看到的，通过名称访问方法或对象属性。方法和属性之间用点隔开。回顾已经分析过的示例是有趣的，它们充满了 StarOffice 对象。如果它们听起来仍然像乱码，不要慌。熟悉 StarOffice 中的对象并不困难，你不需要学习所有的名称。重要的是熟悉它们的结构。

对象是 StarBasic 程序与 StarOffice 之间的通信手段。如果你想自动处理文本或在电子表格中进行自动计算，你需要的内容都由 StarOffice 对象表示。所有属性——颜色、字体甚至值——都是 StarOffice 对象的属性。你的程序将包含 StarOffice 对象的方法和属性。你可以使用以下代码通过宏关闭 StarOffice：

```
Sub CloseOffice
Application.Quit()
End Sub
```

StarOffice 对象加载了不同的函数和属性。主要的困难在于不知道从哪里开始。在大多数情况下，使用宏记录器查找应用程序的方法和属性是最容易的。它会生成对所用模块和已更改属性的完整引用。即使它们对你的任务没有帮助，你至少有了一个 StarBasic 系统搜索的起点。

查找程序的 StarOffice 对象的三个主要途径如下：

- 将你想要的操作手动录制临时宏，并检查其代码。
- 在 StarBasic 帮助系统中查找对象。鉴于帮助系统的结构和内容有点复杂，下一节将介绍其用法。
- 从他人处获取代码。这并不是“窃取”，互联网上的人称之为开源。查看其他程序。StarOffice 本身带有一些示例。此外，你可以检查 Gimmicks 库并在帮助系统中找到大量代码段。

再次，你不需要记忆大量的对象。只需学习 StarBasic 的编程结构、语句和表达式即可。该结构与微软的 VBA 兼容（你在 Word 97 和 Excel 97 中使用的）。遗憾的是（尽管有此原因），StarOffice 的对象层次结构并不相当于 Microsoft Office。如果你用过 Word 和 StarWriter，显然程序是不同的！因为它们有不同的使用范式，因此具有不同的函数和属性，从而有不同的对象。

成为一名 StarBasic 程序员通常意味着你熟悉结构。然而，帮助系统并不最方便；熟悉它可能是一个挑战。
