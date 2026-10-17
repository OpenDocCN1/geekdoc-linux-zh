
图 7.3 显示了我们刚刚讨论的所有命令生成的输出。

图 7.3
在纯文本编辑器中使用选择命令，你可以使用 LaTeX 为打印文档添加结构。

在 LaTeX 中插入强调文本非常简单，特别是在像这里这样的段落中间，这个段落是为了你的阅读体验设计的。
我昨天打了足球¹。

这是居中的文本。

女士们、先生们，睁开你们眼睛。我不会再次警告你们了，比赛就要开始了！如果现在不出发，你们将错过发令！

1. 这是第一个编号项目。

2. 这是第二个编号项目。

3. 这是第三个编号项目。

• 这是一个无编号的符号项目。
• 这是一个另一个无编号的符号项目。

> ¹足球是一项接触运动，应该只由具备适当装备的合格人员进行。

# 插入特殊字符

从事出版行业的人对这些非常熟悉。为了说明这些字符的使用，请考虑以下行：
我去了商店——书店，我在那里……

# 表 7.5 常用字符

| 命令 | 描述 |
|---|---|
| `\dots` | 插入正确间隔的省略号 |
| `--` | 插入连接折号 (en dash) |
| `---` | 插入破折号 (em dash) |
| `\` | 插入左引号 |
| `''` | 插入右引号 |

# 整合一切

使用你刚刚学会命令，你可以通过 emacs 或 vi 等编辑器从文本生成专业级的打印文档。列表 7.2 使用多个命令的 文档

```
\documentclass[letter,paper,12pt]{book}

\title{我的小说}

\author{郭晓}

\begin{document}

\pagestyle{headings}

\maketitle

\chapter{开始我的小说}

我从\emph{这里}开始我的小说。遗憾的是，这只有两段。尽管如此，它将是一部精彩的小说，因为它展示了 LaTeX 的格式化过程。

\chapter{结束我的小说}

我的小说现在有两个章节（第三章正在创作中）。第二章只是一个神秘的购物清单

\begin{itemize}

\item 条纹红袜子

\item 一个绿色橡胶脸盆

\item 《时间》杂志的最后一期

\end{itemize}

也许有一天，这个购物清单中的所有物品都会得到解释。但我想我们将那份悬念留给续集。

\end{document}
```

- 使用 `\documentclass` 命令创建一个信纸大小、12 点字号的新文档。
- 使用 `\maketitle` 命令输出一个包含标题和作者信息的精美标题页。
- 使用 `\tableofcontents` 命令输出目录。
- 使用 `\chapter` 命令开启“开始我的小说”和“结束我的小说”。
- 使用 `\begin{itemize}` 和 `\end{itemize}` 命令创建一个符号列表，并用 `\item` 标记每个项目。

# 170

# 第 7 小

图 7.4
我们最后一个令人印象目的示例文档，使用 LaTeX 文本格式器创建并发送到打印机。

![](img/486a8c2356942c74dbc4de3c2f5d0f4e_196_0.png)

## 关于 LaTeX 的更多信息

在这个简要介绍中，你只接触了 LaTeX 及其能力的一角。要学习更多关于 LaTeX 或在正式项目中使用 LaTeX，你应该考虑更深入的文档。

这些在线文档资源是一个很好的起点：

- * http://www.giss.nasa.gov/latex/ 包含一个由 Sheldon Green 编写的关于使用 LaTeX 格式器的超文本指南。
- * http://www.maths.tcd.ie/~dwilkins/LaTeXPrimer/Index.html 包含由 David R. Wilkins 编写的关于使用 LaTeX 格式器的超文本入门。
- 一名为《The Not So Short Introduction to LaTeX 2e》的优秀可打印指南可以以便携文档 (.pdf) 格式从 http://people.ee.ethz.ch/~etiker/lshort/lshort.pdf 下载。
- 各种类型的参考材料可以在 http://www.latex-project.org 这个综合网站上找到。

## 使用二进制计算器执行数学任务

数学和计算是任何包含计算机系统的办公常见的生产力工作。许多办公室使用图形化表格程序，例如 Microsoft Excel 或 Corel Quattro Pro。

正如你可能预测的那样，Linux 命令行让你能够使用一种更原始但也更强大的计算形式。尽管它是一个强大的执行者，但你只需要少量的训练就可以使用名为 bc 的 Linux 二进制计算器。

## 启动 bc 并执行基础计算

要启动 `bc`，在命令行输入它且不带参数。如果你进入了 `bc` 命令模式：

```bash
$ bc

1.06

Copyright 1991-1994, 1997, 2000 Free Software Foundation, Inc.

This is free software with ABSOLUTELY NO WARRANTY.

For details type 'warranty'.
```

`bc` 没有提示符，但尽管如此，`bc` 仍在耐心地等待你的指令。要执行基础计算，只需正常输入即可。例如，通过输入数字和必要的加号运算符来加几个数字，然后按回车键：

```bash
216 + 45 + 36
297
```

注意 `bc` 会立即打印结果。你可以通过输入你预期的输入字符来使用其他数学运算符。使用括号来指定操作顺序，如本例所示，它指定了 20 + 20 为第一次计算：

```bash
( 1200 / ( 20 + 20 ) * 6
180
```

再次，答案被立即计算并显示。使用小数点来表示分数部分，如在本例中：

```bash
10.44 * 3.623
37.824
```

你可以在任何时候通过在空行上输入特殊命令 `quit` 来退出 `bc`：

```bash
quit
[@workstation20 you]$
```

这种快速、轻松且具有任意精度（任意数量的小位数）执行此类小规模计算的能力，使得二进制计算器极其有用。

## 使用变量

有时，记住计算结果或存储数字以备后用很有帮助。这在 `bc` 中也可以做到。为了让 `bc` 输出你想要使用的计算结果或数字，你可以将值或计算表达式的结果赋值给：

```bash
a=10.1
b=6.3
c=a*b
c
63.6
```

在这里，你将值 10.1 赋值给变量 `a`，将值 6.3 赋值给变量 `b`，将 `a` 乘以 `b` 的结果赋值给变量 `c`。然后通过输入变量名来显示 `c` 的内容。

除法的结果可能会计算到任意精度水平而不得出结论。使用特殊变量 `scale` 来确定除法时计算的小位数：

```bash
scale=10
3/7
.4285714285
```

使用这些示例所示的变量和运算符，你可以轻松准确地执行相当长且复杂的系列计算。

## 使用 bc 自动化计算

假设你经常重复执行一系列计算。与其每次都使用新数字反复在 `bc` 中输入这些计算，你不如编写脚本在 `bc` 中自动执行这些类型的计算。这里有一个示例：

1. 使用 `vi` 或 `em` 创建一个名为 `addtree.bc` 的文件，其中包含以下文本：
   - "Number to add? ; y=read()"
   - "Adding 3 to ; y"
   - "produces ; y+3"
   - `quit`

2. 现在，从命令行调用 `bc` 并提供 `addtree.bc` 作为参数。

## 无需鼠标的操作

3. 当 `bc` 提示输入数字时，输入一个数字并按回车。

你输入的这个数字的值将被 `bc` 存储在变量 `y` 中，并对其加数字 3。然后显示结果：

```bash
[@workstation20]$ bc addthree.bc
b 1.06
Copyright 1991-1994, 1997, 1998, 2000 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type 'warranty'.
Number to add? 5
Adding 3 to 5
produces 8
[@workstation20]$
```
