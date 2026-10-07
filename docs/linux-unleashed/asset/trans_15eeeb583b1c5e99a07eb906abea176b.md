

## Emacs 快捷键

| 命令 | 功能 |
| :--- | :--- |
| Ctrl+b | 向左移动一个字符 |
| Ctrl+d | 删除当前字符 |
| Ctrl+f | 向右移动一个字符 |
| Ctrl+g | 取消当前命令 |
| Ctrl+h | 进入 Emacs 在线帮助 |
| Ctrl+n | 移动到下一行 |
| Ctrl+p | 移动到上一行 |
| Ctrl+s | 向前搜索字符串 |
| Ctrl+v | 向前翻页（滚动一屏） |
| META+v | 向后翻页（滚动一屏） |
| Ctrl+x u | 撤销最后一次编辑 |
| Ctrl+x Ctrl+c | 退出 Emacs |
| Ctrl+x Ctrl+s | 将缓冲区保存到文件 |

## 摘要

Linux 系统有许多可用的文本编辑器。其中最受欢迎的两个是 vi（实际上它是 elvis 编辑器的别名）和 Emacs。两者都提供基本的编辑功能，如插入和删除文本、读取和写入外部文件、文本搜索以及复制和移动文本。vi 是一个全屏编辑器，具有两种模式：命令模式和文本模式。Emacs 是一个可扩展且功能强大的编辑器，具有高度的可配置性，以适应各种编辑任务（如编程、文档编写以及更改用户或系统文件）。

从这里，你可以找到相关材料阅读。若想深入了解 groff（一种文本格式化实用工具），请阅读第 17 章，“groff”。

若要了解 TeX 和 LaTeX，更灵活的文本编辑器和格式化器，请阅读第 19 章，“TeX 和 LaTeX”。

若要设置系统以使用 X 窗口系统，请阅读第 22 章，“安装和配置 XFree86”。

# 第 17 章：groff

作者：Tim Parker

### 本章内容

- 嵌入命令 320
- 控制字符外观 321
- 宏 325
- 使用 mm 326

groff 程序是 nroff 和 troff 的 GNU 版本，这两种文本格式化语言在 UNIX 系统中已使用多年。groff 系统包含 troff、nroff、eqn、tbl 以及其他 UNIX 文本格式化实用工具的版本。groff 语言主要用于将编写并以 groff/nroff 格式存储的手册页（man pages）编译成可打印或在屏幕上显示的形式。

nroff 语言的设计是为了在行式打印机上提供文本格式化，而 troff 则是为照排机（phototypesetters）开发的。这两种语言中的命令是相同的，尽管一些无法由行式打印机处理的命令会被 nroff 忽略。在大多数情况下，你不会直接使用 nroff 或 troff，而是使用宏包来访问它们。

在很大程度上，随着强大文字处理器和桌面出版软件包的发展，nroff 和 troff 已逐渐被弃用。它们目前仅剩的用途是格式化手册页，而这些手册页仍在被广泛使用。

nroff 和 troff 都有许多你永远不会用到的命令。因此，在本章中，我们将探讨使用这两种语言的 groff 版本所需的基本命令集，以及它们如何用于手册页特定的应用。如果你真的想用 groff 进行高级文本格式化，你应该找一本专门的书籍。

## 嵌入命令

groff 的一个方面可能需要适应一下，即你在文件中输入行的方式并不一定是最终输出中显示的方式。groff 系统会尽可能地将文本行合并在一起。例如，源文件

```
This is fine stuff.
It is really interesting and
could keep me busy for hours.
```

在源文件中占据三行，但经过格式化后，groff 将它们合并为如下显示：

```
This is fine stuff. It is really interesting and could keep me busy for hours.
```

并根据页面布局在必要处换行。这有一个优点，即你不必担心在源代码中让一切都看起来格式正确。然而，缺点是直到你看到输出之前，你对输出的样子没有一个准确的概念。

查看 **groff** 源文件可以发现，它全是 ASCII 字符，包含显示输出的常规文本和一组以句点开头的命令，如下所示：

```
This is a bunch of text that will be displayed.
Here is even more text.
.ps 14
```

上面的一行是一个 **groff** 命令，由行首第一列的句点标识。

大多数 **groff** 命令单独占一行，但少数命令可以嵌入在行的任何位置。这些命令通常以反斜杠开头，类似于 shell 使用反斜杠作为转义字符。一个包含嵌入命令的行示例如下：

```
This \fBline\fR has two embedded \fIgrot\fR commands.
```

尽管有时你会想使用嵌入命令，但使用的大多数命令将是单独占一行，以句点开头的。

## 控制字符外观

**groff** 语言有一些命令用于控制字符在打印或显示时的外观。这些包括改变字符的大小和行距，以及控制字体。

### 大小和行距

字符大小和行距在屏幕显示文本时通常没什么用，除非你使用的是点阵终端。但它们用于打印文档。你可以使用 .ps（磅值）命令来改变文本的大小：

```
This is the default 10-point size.
.ps 14
This is now in fourteen-point size.
.ps 20
This is a point size of twenty.
.ps 6
And this is a really small point size of six.
```

> **注意**
> 一点（point）是 1/72 英寸，因此 36 磅的字符高度为半英寸。最常用的 12 磅字符高度为 1/6 英寸。不同版本的 groff 支持不同的磅值，但大多数版本支持 6、7、8、9、10、11、12、14、16、20、24、28 和 36 磅。如果你设置了一个不支持的值，它会向上舍入到下一个较高的值（最大为 36）。默认的磅值为 10。如果你在不带参数的情况下使用 .ps 命令，groff 会恢复之前的值。

在句子中，可以使用行内嵌入命令 \s 后跟磅值来改变磅值。例如：

```
This is in 10-point, while \s20this is in twenty,\s10 and back to 10 again.
```

\s 命令后面必须跟一个合法的磅值。特殊命令 \s0 会使 groff 恢复之前的值。也支持相对变化，因此你可以嵌入诸如 \s+2 和 \s-2 的命令，但只能指定一位数字（因此你不能改变超过 9 磅）。

*行距*是行之间的垂直间距。垂直间距不随磅值绑定，因此需要手动调整。一般规则是，使用比磅值大约 20% 的垂直间距。默认垂直间距为 11。

行距由 .vs（垂直间距）命令控制。在下一个示例中，我们改变磅值和垂直间距，以便字符能清晰打印而不重叠：

```
This is in normal 10-point, 11 vertical space size.
.ps 12
.vs 14
This is in 12-point with 14 vertical spacing.
```

如果你在不带参数的情况下使用 .vs 命令，groff 会恢复之前的值。

如果你想出于某种原因强制间距，例如分隔文本部分，请使用 .sp（空格）命令。不带参数使用时，.sp 给出一个空行。它也可以接受 i（英寸）和 p（磅）作为参数：

```
This is default 10-point 11 vertical spaced text.
.sp
We have a blank line above this because of the command.
.sp 3.5i
This is three and a half inches below the previous line.
```

你可以在大多数 groff 命令中使用分数，如本例所示。

### 字体

更改字体需要 .ft（字体类型）命令。在 troff 的早期，只支持四种字体：罗马体、罗马粗体、罗马斜体以及一组特殊字符。其他字体必须在照排机上特别加载。因此，groff 默认使用罗马体。

要切换到罗马粗体，使用命令 .ft B，而 .ft I 则令人毫无意外地切换到罗马斜体。要返回正常的罗马字体，使用命令 .ft R，尽管在大多数系统上，单独使用 .ft 就足够了：

```
This is in normal Roman font.
.ft B
This is bold.
.ft I
This is italic.
.ft
This is back to normal Roman font.
```

你也可以使用行内嵌入命令切换字体，使用 \f 后跟 I 或 B，使用 R 切换回正常字体：

```
This is normal, \fBbold\fR and \fIitalics\fR.
```

由于大多数系统打印机不支持下划线，带下划线的文本被转换为斜体。下划线命令 .ux 会将接下来的 x 行文本设为斜体。

由于我们现在要比仅仅罗马体多得多可用的字体，我们必须能在 groff 中更改字体。更改字体的命令是 .fp（物理安装的字体），它还需要一个数字来指示字体在照排机中安装的位置（这是老式的东西了，不是吗？）。例如，如果 Helvetica 字体安装在字体位置 3，我们通过字体字母 H 来引用它，那么命令

```
.fp 3 H
```

将指示照排机切换到字体位置 3 的 Helvetica。groff 仍然保留这些旧式命令。

### 缩进和行长度

在 groff 中，行长度默认设置为 6.5 英寸。要覆盖此值，使用 .ll（行长度）命令并指示单位的参数。例如，命令

```
.ll 7i
```

