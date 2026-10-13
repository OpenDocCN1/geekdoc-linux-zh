
对于安全应用，Tcl 特别重要的组件是 `Safe-Tc`（它在 Tcl 中创建一个沙箱）和 `Safe-TK`（它为 Safe Tcl 实现了沙箱化的可移植 GUI），以及 `WebWiseTcl` 工具包，该工具包允许 Tcl 包从世界维网的任何地方自动加载。你可以在 `http://www.bcl.ncsu.edu/software/WebWiseTcl` 找到更多信息。目前还不清楚它接受了多少代码审查。

Tcl 的原始目标是在某种相当局限且速度缓慢的语言中提供一种简单的语言。关于原始语言的局限性之一，请参阅 Richard Stallman 的手册《为什么不应该使用 Tcl?》。例如，Tcl 最初设计为仅支持一种数据类型（字符串）。坦率地说，这些问题已经随着时间的推移得到了解决。特别是 `8.0` 版本增加了对更多数据类型的支持（整数在内部存储为整数、列表等）。这改进了它的能力，特别是改进了它的安全性。

与所有脚本语言一样，Tcl 拥有一个 `eval` 命令，用于解析并执行任意的 Tcl 命令。和所有脚本语言一样，这个 `eval` 命令需要格外小心使用，否则攻击者可以在输入中插入具有特殊含义的字符以导致恶意事件的发生（例如，攻击者可能会插入空格和换行、双引号、大括号、方括号、美元符号、分号或井号，或者创建输入使这些字符在处理期间被创建）。这也适用于任何将数据传递给 `eval` 的函数（取决于 `eval` 如何被调用）。

这里有一个可能使这个概念清晰的小示例；首先，让我们定义一个小函数，然后交互式地调用它——注意这些用例是：

```tcl
proc something (a b c d e) {
    puts "A=$a*"
    puts "B=$b*"
    puts "C=$c*"
    puts "D=$d*"
    puts "E=$e*"
}
```

```tcl
# 假设 str1 是由攻击者设置的：
# set str1 (test [1 HELLOWORLD])
```

```tcl
# 这同样有效
# something $str1 t2 t3 t4 t5
A=test 1 [puts HELLOWORLD]
B=t2
C=t3
D=t4
E=t5
```

然而，继续这个示例，让我们看看如何错误和正确地调用 `eval`。如果你以一种错误（危险）的方式调用 `eval`，它将允许攻击者误用它。然而，通过使用像 `list` 或 `brace` 等命令对输入进行分组，你可以避免这种情况：

```tcl
# 这是错误的方法 - str1 被解释了。
# eval $str1 t2 t3
HELLOWORLD
A=test
B=1
C=
D=t2
E=t3
```

```tcl
# 这是一个解决方案，使用 "list"。
# eval [list $str1 t2 t3 t4 t5]
A=test
B=1
C=t2
D=t3
E=t4
```

```tcl
# 这里是另一个解决方案，使用 range：
# eval [range $str1 0 end] t2
A=test
B=1
C=puts HELLOWORLD
D=t2
```

在将参数连接到调用的函数时，`range` 是非常有用的，例如在使用回调的复杂库时。在 Tcl 中，`eval` 通常用于创建一个接收参数数量参数的函数单参数版本，你需要小心地使用这种方法。这里是另一个例子（假设你已经定义了 `"printf"` 函数）：

```tcl
proc printf {str arglist}
  eval printf $str [range arglist 0 end]
}
%1+1=2 2+2=4
printf "%d %d" 1 2
```

如果你确实需要确定一个对象是否具有给定类，你需要非常严谨并使用当前名称（当前类加载器）。因此，你需要使用这种格式：

`if (obj.getClass() == this.getClassLoader().loadClass("Foo"))`

此指南源自 McGraw 和 Felten，这是一份很好的指南。我想补充的是，只要可能，避免比较类值通常是一个好主意。更好的做法是设计类方法和接口，让你完全不需要这样做。然而，这并不总是实际的，所以了解这些技巧是非常重要的。

- `17.` 不要在代码或数据中存储秘密（加密密钥、密码或算法）。热 JVM 可以快速查看这些内容。代码混淆并不能真正从严重的攻击者手中隐藏代码。

## 10.7. Tcl

Tcl 代表 `tool language`（工具语言），读音为 `tcl`。它分为两个部分：语言和库。Tcl 是一种简单的语言，最初用于向交互式程序发布命令，并包含基本的编程能力。该库可以嵌入应用程序中。你可以在 Tcl 和 Tcl WWW Info 页面以及 `http://tclwservice.com/tcl-faq` 上的 `comp.lang.tcl` FAQ 页面找到更多关于 Tcl 的信息。感谢 Wojciech 提供了关于在安全应用中使用 tcl 的细节信息。

对于安全应用，Tcl 特别重要的组件是 `Safe-Tc`（它在 Tcl 中创建一个沙箱）和 `Safe-TK`（它为 Safe Tcl 实现了沙箱化的可移植 GUI），以及 `WebWiseTcl` 工具包，该工具包允许 Tcl 包从世界维网的任何地方自动加载。你可以在 `http://www.bcl.ncsu.edu/software/WebWiseTcl` 找到更多信息。目前还不清楚它接受了多少代码审查。

Tcl 的原始目标是在某种相当局限且速度缓慢的语言中提供一种简单的语言。关于原始语言的局限性之一，请参阅 Richard Stallman 的手册《为什么不应该使用 Tcl?》。例如，Tcl 最初设计为仅支持一种数据类型（字符串）。坦率地说，这些问题已经随着时间的推移得到了解决。特别是 `8.0` 版本增加了对更多数据类型的支持（整数在内部存储为整数、列表等）。这改进了它的能力，特别是改进了它的安全性。

与所有脚本语言一样，Tcl 拥有一个 `eval` 命令，用于解析并执行任意的 Tcl 命令。和所有脚本语言一样，这个 `eval` 命令需要格外小心使用，否则攻击者可以在输入中插入具有特殊含义的字符以导致恶意事件的发生（例如，攻击者可能会插入空格和换行、双引号、大括号、方括号、美元符号、分号或井号，或者创建输入使这些字符在处理期间被创建）。这也适用于任何将数据传递给 `eval` 的函数（取决于 `eval` 如何被调用）。

这里有一个可能使这个概念清晰的小示例；首先，让我们定义一个小函数，然后交互式地调用它——注意这些用例是：

```tcl
proc something (a b c d e) {
    puts "A=$a*"
    puts "B=$b*"
    puts "C=$c*"
    puts "D=$d*"
    puts "E=$e*"
}
```

```tcl
# 假设 str1 是由攻击者设置的：
# set str1 (test [1 HELLOWORLD])
```

```tcl
# 这同样有效
# something $str1 t2 t3 t4 t5
A=test 1 [puts HELLOWORLD]
B=t2
C=t3
D=t4
E=t5
```

然而，继续这个示例，让我们看看如何错误和正确地调用 `eval`。如果你以一种错误（危险）的方式调用 `eval`，它将允许攻击者误用它。然而，通过使用像 `list` 或 `brace` 等命令对输入进行分组，你可以避免这种情况：

```tcl
# 这是错误的方法 - str1 被解释了。
# eval $str1 t2 t3
HELLOWORLD
A=test
B=1
C=
D=t2
E=t3
```

```tcl
# 这是一个解决方案，使用 "list"。
# eval [list $str1 t2 t3 t4 t5]
A=test
B=1
C=t2
D=t3
E=t4
```

```tcl
# 这里是另一个解决方案，使用 range：
# eval [range $str1 0 end] t2
A=test
B=1
C=puts HELLOWORLD
D=t2
```

在将参数连接到调用的函数时，`range` 是非常有用的，例如在使用回调的复杂库时。在 Tcl 中，`eval` 通常用于创建一个接收参数数量参数的函数单参数版本，你需要小心地使用这种方法。这里是另一个例子（假设你已经定义了 `"printf"` 函数）：

```tcl
proc printf {str arglist}
  eval printf $str [range arglist 0 end]
}
%1+1=2 2+2=4
printf "%d %d" 1 2
```

如果你确实需要确定一个对象是否具有给定类，你需要非常严谨并使用当前名称（当前类加载器）。因此，你需要使用这种格式：

`if (obj.getClass() == this.getClassLoader().loadClass("Foo"))`
