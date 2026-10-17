
(A220 15 D1 T4) TEMP (`C:\WINDOWS\TEMP`)

当然，通常需要遍历数组的每个元素并处理每个值。为了方便，Tcl 提供了常用的 `array names` 命令，它返回数组中所有索引的列表。你可以将 `array names` 与 `foreach` 命令结合使用，“遍历”数组的每个元素，如下：

```tcl
foreach x [array names env] [
  puts "$x"
  # do something interesting with $env($x) here, if you
]
```

## 使用语句 (Using Statements)

现在你已经对 Tcl 替换和分组这些基本概念有了初步了解，并理解了 Tcl 变量，让我们来看看基础 Tcl 语句的构造。Tcl 的语法确实非常简单；每个 Tcl 命令都是系列字符串，以 Tcl 命令名或过程名开头。

这种方法与你在 Perl、shell 语言以及像 C 这样的语言中会看到的内容略有不同。例如，在下面这样的 Perl 结构中，大括号是 `if` 命令正确语法的一部分，如果 Perl 编译器无法在预期的位置找到正确的标点符号，它将返回错误（请记住 Perl 并不是一种特别挑剔的语言）。

```perl
$variable {
  `pwd`
}
```

在 Tcl 中，大括号不是 `if` 命令不可或缺的一部分，如果 Tcl 解释器没有看到大括号，它不会返回错误。相反，Tcl 期望在 `if` 命令之后看到两个单词，紧跟着一个换行符或分号。例如，以下内容是一个完全有效（尽管不一定有用）的 Tcl 命令：

```tcl
% if $variable pwd
```
