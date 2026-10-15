
```perl
#! /usr/bin/tclsh

if ($argc != 2) exit

set magiclength [index argv 0]
set myfilename [index argv 1]

set infile [open "$myfile"]
while ![eof $infile] {
  gets $infile line
  if [string length line] == $magiclength]
    puts $line

close $infile
```

然而，如果你运行它，你会发现它通常什么都不返回。然而，有时它可能会返回*所有*行，无论长度如何。你能发现错误吗？如果你是一个资深的 Tcl 程序员，这个错误可能很容易找到，尽管你可能想通过调试器运行脚本看看发生了什么。

列表 11.11 显示了一个用于测试的 *fl.dat* 版本。

# **列表 11.11** *fl.dat—脚本的数据文件*

```
1234567890
1111111111
1234567890
222222222222221
```

遗憾的是，Tcl 本身没有自己的调试器。（Scriptics 公司正在计划发布 TclPro 开发环境，它将包含一个可视化调试器。）然而，免费可用且广泛应用的 Expect 程序使用 Tcl 作为其脚本语言，包含一个你可以用于 Tcl 脚本的调试器。

### 提示

要确保你的系统中安装了 Expect，在 shell 提示符输入 `which expect`。如果没有安装 Expect，请通过你的首选浏览器访问 `http://expect.nist.gov` 获取更多信息。

要调试 `fl.tcl`，使用 `-D` 参数配合值 `1` 调用 Expect：

```
% expect -D 1 fl.tcl.dat
1: if ($argc != 2) exit
dbg1.0>
```

你可以看到，Expect 调试器显示 `dbg1.0>` 提示符。在这里，“1.0”中的第一个1 显示的是栈深度，第二个1 只是当前会话历史中的命令编号。你还会注意到脚本中的第一个命令（`if` 命令）出现在提示符上方。这就是当你要求 Expect 执行命令时，Expect 下一个执行的命令。

### 注意

栈在程序内部执行函数时，存储从调用者传递给被调用者的临时信息。每当一个函数调用另一个函数，然后该函数再调用另一个时，栈就会变深。当函数结束并将控制返回给调用者时，栈就会变浅。

```
dbg1.0> s
1: index $argv 0
dbg1.1>
```

调试器执行了 `if` 语句，发现表达式为假后，移动到下一行。继续单步执行直到提示符变为 `dbg1.3`。

` 标签中似乎不完整（在到第 11 章总结之后就中断了），我仅针对您提供的显示部分进行了翻译。如果您有完整的文本，请重新提供。以下是针对您提供内容的翻译：

# 调试工具

在过程的任何时候，我们都可以执行任何喜欢的命令，就就像在 `tcsh` 提示符中输入命令一样。让我们确保 `magiclength` 已经从命令行正确读取：

```
1: lindex $argv 1
dbg1.3> set magiclength
10
dbg1.4>
```

现在，让我们跳过另外两个步骤，确保文件名已经正确读取：

```
dbg1.4> s
1: lindex $argv 1
dbg1.5> s
1: open "$filename"
dbg1.6> set filename
fl1.tcl
```

到目前为止，一切看起来正常。现在是时候遍历数据文件并读取文本行了：

```
dbg1.10> s
2: eof $infile
dbg2.11> s
2: gets $infile line
dbg2.12> s
2: if [[string length line]] -- ...
dbg2.13> s
3: string length line
dbg3.14> s
2: eof $infile
dbg2.15>
```

此时，我们应该预期脚本打印出文本文件的第一行——当然，前提是第一行的长度为 10 个字符，且 10 是我们在调用调试器时传递给 `fl` 的参数。

因为我们预期在这里能得到一些结果，但没有看到任何输出，我们应该仔细检查这一行。啊！我忘记在嵌入字符串长度的变量行中使用变量替换了：函数：`if` 语句应该读取为：

```
if [[string length $line]] == $magiclength] {
  puts $line
}
```

# 第 11 章 / 调试概念

就因为少了一个美元符号，脚本失败了——解释器在评估的是字面量字符串 "line" 的长度，而不是名为 "line" 的变量的值。（替换是 Tcl 的本质！）为了测试我们的理论，让我们重新启动调试器，并将 `magiclength` 的值改为四，看看解释器是否会产生匹配：

Tcl 的 `exit` 函数会停止调试器。

```
% expect -D 1 fl1.tcl 10 fl1.dat
1: if ($argc == 2) exit
dbg1.0> s
1: index argv 0
dbg1.1> s
1: index argv 0
dbg1.2> s
1: index argv 1
dbg1.3> set magiclength
10
dbg1.4> set magiclength 4
4
dbg1.5> s
1: index argv 1
dbg1.6> s
1: open "$myfilename"
dbg1.7> s
1: open "$myfilename"
dbg1.8> s
1: while { ! [ eof $infile ] } (
    gets $infile line
    if { [ string length ... ] ...
dbg1.9> s
    1: eof $infile
dbg1.10> s
2: index $infile line
dbg2.11> s
2: if [ [string length line] == ...
    puts $line
}
dbg2.12> s
2: string length line
dbg2.13> s
3: puts $line
dbg3.14> s
1234567890        <- 输入行已显示！
1: eof $infile
dbg3.15>
```

## 总结

好了，这确实解决了问题。我们可以退出调试器并对源代码进行相应的修改。

表 11.3 总结了 Expect 的调试命令。

# 表 11.3 Expect 调试命令

| 等级代码 | 说明 |
|---|---|
| s | 进入过程 |
| n | 跳过过程 |
| r | 从过程返回 |
| b | 断点 |
| c | 继续 |
| w | 显示堆栈 |
| u | 作用域向上移动 |
| d | 作用域向下移动 |
| h | 帮助 |
| \r> | 重复上一个调试命令 |

## 总结

本章概述了在创建脚本时可能会遇到的的许多类型的错误。我听过的程序员中，没有谁能写出超过几行的完美脚本。只需记住，当你自己犯错时，你并不孤单。

调试通常有两个阶段。第一阶段涉及修复你在输入代码时引入程序的任何语法错误或拼写错误。例如，在 Perl 中，你可能没有在行末尾添加分号，或者你可能使用了 **else** 而不是 **elsif**。每种编程语言都有其独特的易错拼写错误。

有时，拼写错误直到脚本开始运行才会暴露。这些错误被称为运行时错误。运行时错误包括经典的除以零错误和使用错误的变量名，例如使用 `shipping-Books` 而不是 `Shipping_Books`。

在相对容易修复语法错误之后，是第二阶段——发现并修复逻辑错误。在 Bash 中，你可以使用 `set -u` 和 `set +x` 命令来开启未绑定变量标记和展开命令显示。我还建议在运行任何潜在危险的命令之前，使用 `echo` 命令来验证命令行变量扩展。

Perl 有三种捕捉 Bug 的主要技术：`-w` 命令行选项、`strict` 模块和 `print` 语句。`-w` 告诉 Perl 寻找某些危险情况，例如只使用一次的变量。`strict` 模块做了几件事，最重要的是它要求你在在使用所有变量之前声明它们。最后一种技术 `print` 语句在所有计算机语言中无处不在。只需在代码的策略位置放置 `print` 语句，显示状态消息和重要变量的值。

Tcl 没有 Perl 那种开启额外警告消息的能力，但用于显示变量和监控程序进的 `puts` 函数非常有帮助。

Perl 的交互式调试器非常有用，尽管我觉得大多数 Perl 程序员并没有充分使用它。它的许多命令以及交互式显示变量、调用函数和更改变量值的能力，使其在创建复杂的脚本时非常有价值。

Tcl/Expect 的结合产生了一个类似于 Perl 的交互式调试器。你可以用它单步执行脚本、显示变量并更改变量的值。

第 12 章“自定义工具”让你有机会使用所有这些调试技术。

## 更好的 find 命令
