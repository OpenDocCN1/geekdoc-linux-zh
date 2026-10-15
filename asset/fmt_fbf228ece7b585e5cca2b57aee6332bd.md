
`sub { my $a; sub f { $a } }`

在 `f` 创建时，它无法捕获 `$a` 的当前值，因为匿名子程序尚未创建。相反，以下情况不会产生警告，因为匿名子程序已经创建且处于活动状态：

```
sub { my $a; eval 'sub f { $a }'->(); }
```

第二种情况是由 `eval` 访问已超出作用域的变量引起的，例如：

```
sub f { my $a; sub { eval '$a' } f()(); }
```

在这里，当 `eval` 中的 `'$a'` 编译时，`f()` 并没有正在执行，因此它的 `'$a'` 不可捕获。

变量 `"%s"` 未导入 `%s`
`(M misc)` 在 `"use strict"` 生效的情况下，你引用了一个你显然认为是从另一个模块导入的全局变量，但该模块导出了同名的其他内容（通常是子程序）。通常意味着你在变量前面写了错误的字符。

正则 `m/%s%` 中未实现变长后向断言
`(F)` 后向断言（Lookbehind）仅允许用于编译时固定且已知的子表达式。对于正向后向断言，你可以使用 `\K` 正则构造来实现等效功能。在 perl 中使用 `"(?<=pattern)\K"`。有些不明显的 Unicode 规则 `/i` 可以匹配，你可能并不知道。例如，字符串 `ss` 可以匹配 LATIN SMALL LETTER SHARP。还有其他 ASCII 字符序列可以匹配单个字符，如 LATIN SMALL FF 匹配 `/i`。从 Perl v16 开始，如果你只使用 ASCII 匹配，那么 `/aa` 修饰符将排除这些不明显的匹配，从而消除此信息。你也可以使用 `re qw()` 对范围内编译的所有正则表达式应用 `/aa`。

`%s` 变量 `%s` 匹配 `%s`
`(W misc)` 在当前作用域或语句中声明了 `"my,"our" 或 "state"`，有效地消除了对之前实例的访问。这几乎总是类型错误。注意，之前的变量将一直存在到作用域结束或闭包引用被销毁。

变量语法
`(A)` 你写了一个元操作符，后面跟着看起来像二进制操作符的内容，但它也可以被解释为项或元操作符。例如，如果你知道 `rand` 函数的默认参数为 `1.0`，而你写了

`rand + 5;`

你可能认为你写的是和 `rand() + 5` 相同，但实际上你得到的是
`rand(+5);`

所以使用括号明确你的真实含义。

变量 `"%s"` 将不会共享
`(W closure)` 一个内部（嵌套）子程序引用了变量。当匿名子程序创建时，它们会自动重绑定到当前作用域。这个问题通常可以通过将内部匿名化（使用 `{}` 语法）解决。

`when` 是实验性的
`(S experimental::smartmatch)` 依赖于 `smartmatch`，它是实验性的。此外，它有几个可能立即不可见的特殊情况，其行为可能会在未来的任何 perl 版本中更改或删除。请参见 `perlyn` 中 `"Experimental Details on get and when"` 的解释。

`%s` 中的宽字符
`(S utf8)` Perl 在不预料的情况下遇到了一个宽字符（>255）。此警告默认针对 I/O（如 `print`）。消除此警告最简单的方法是直接为输出添加 `utf8` 层，例如 `binmode STDOUT, :utf8`。另一种关闭警告的方法是使用 `no warnings 'utf8';`；这通常更接近

作弊。通常情况下，你应该显式地为文件句柄指定编码，请参阅 `perfunc` 中的 `open` 和 `"binmode"`。
在 `%s` 中遇到宽字符 `(U+%X)`

- `(W)` 在单字节区域语言（即非 UTF-8 区域）中，遇到了一个多字节字符。Perl 将该字符视为指定的 Unicode 码点（code point）。将非 UTF-8 区域与 Unicode 结合是危险的。几乎可以确定，某些字符会有两种不同的表示方式。例如，在 ISO 8859-7（希腊语）区域中，码点 `0xC3` 代表大写希腊字母 Gamma。但 `0xC3` 也是如此。这将导致比较变得不可靠。

你可能需要弄清楚这个多字节字符是如何与你的单字节区域混合在一起的（或者你可能认为你使用的是 UTF-8 区域，但 Perl 并不这么认为）。

在 `[]`-长度内不允许使用 `"%c"`

- `(F)` `(un)pack` 模板中的计数可以被 `[TEMPLATE]` 替换，仅当 TEMPLATE 与从模板区域可以确定的相同打包字节数相匹配时。如果它包含任何代码 `@`、`/`、`u`、`w` 或 `*`-长度，则这样做是不可能的。请重新设计模板。

`write(on)` 已关闭文件句柄 `%s`

- `(W)` 你正在写入的文件句柄在之前的某个时候已经关闭。请检查你的控制流。

`%s` `"\xX"` 映射到 Unicode

- `(S utf8)` 在读取不同的编码时，Perl 尝试将所有内容映射为 Unicode 字符。你读取的字节在此编码中是不合法的。例如，`utf8 "\xE4"` 不映射到 Unicode，如果你尝试在 UTF-8 中编码为 `a-diaeresis Latin-1`。

字符 `'X'` 超出字符串范围

- `(F)` 你有一个 `(un)pack` 模板，它在被 `(un)pack` 的字符串开始位置之前指定了一个相对位置。请参阅 `perfunc` 中的 `"pack"`。

`unpack` 中的 `'x'` 超出字符串范围

- `(F)` 你有一个 `pack` 模板，它在被解包的字符串结束位置之后指定了一个相对位置。请请参阅 `perfunc` 中的 `"pack"`。

你在内核中禁用了 SET-ID 脚本！

- `(F)` 你可能永远不会开启它，因为你可能没有内核的源码，而且你的供应商可能根本不在乎你想要。最好的方法是在你的脚本外封装一个 `setuid` C 包装器。

你需要引用 `"%s"`，

- `(W 语法)` 你分配了一个已声明同名的子程序，这意味着 Perl 5 在执行赋值时将尝试调用该子程序，这可能不是你想要的。（如果这正是你想要的，请加上 `&` 符号）

你的随机数不是随机的

- `(F)` 在初始化哈希表的随机数种子时，Perl 无法从你的系统中获取任何随机性。这通常表示发生了非常严重的错误（Something Very Wrong）。

正则表达式中长度为零的 `\N{}`；在 `m/%s/` 中标记为 `<— HERE`

- `(F)` 命名的 Unicode 字符转义符 `(\n{...})` 可能会返回长度为零的序列。此类转义符被用于扩展字符类，即 `(?<`，是不被允许的。请检查是否使用了正确的转义符，以及正确的处理器是否在作用范围内。`<— HERE` 显示了在正则表达式中发现问题。

## 另请
`warnings`, `diagnostics`.

## PERLDOC

### 名称 (NAME)
`perldoc` - 以 Pod 格式查找 Perl 文档。

### 概要 (SYNOPSIS)
`perldoc [-h] [-D] [-t] [-m] [-F] [-i] [-T] [-r] [-d destination_file] [-o formatname] [-M formatterClassName] [-w option:value] [-X] [-L language_code]` 页面|模块名|程序名|URL

示例：

```
perldoc -f BuiltinFunction

perldoc -it BuiltinFunction

perldoc -q BuiltinFunction

perldoc -v BuiltinFunction

perldoc -a BuiltinFunction

perldoc -
```
实际上：

```
perldoc -f BuiltinFunction

perldoc -it BuiltinFunction

perldoc -q FAQ

perldoc -v PerlVariable

perldoc -a PerlAPI
```
