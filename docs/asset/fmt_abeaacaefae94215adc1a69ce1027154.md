
## Perl：初学者指南

## 注意

文件的句柄也可以是一个重新赋值的变量，其中包含你想让文件句柄呈现的字符串。

从上一个示例中，你可以看到文件成功打开，并且执行了正确的语句来告知你。
在我们继续之前，我们需要向你介绍两个在处理文件和目录时可能非常有用的函数：`die` 和 `warn` 函数。这些函数可以通过使用逻辑或运算符 `||` 或任何其他判断类型的语句来与其他语句结合使用。如果逻辑运算符左侧的操作没有返回真值，就会执行 `die` 或 `warn` 函数。这些函数中的每一个都为你提供了显示某些错误信息的选项。`warn` 函数只需输出你请求显示的错误信息。让我们通过另一个编程示例来看这两个函数的用法：

这行代码将尝试打开 "example.txt" 文件。如果无法打开该文件，将执行 `die` 函数并终止程序。

```perl
#!/usr/bin/perl

print "This program will open an example file \n"

print "This is an example of the die and warn functions being used with the \
|| operator \n"

open (EXAMPLE
```

这行代码将尝试打开 "example.txt" 文件。如果无法打开该文件，将执行 `die` 函数并终止程序。

```perl
#!/usr/bin/perl

print "This program will open an example file \n"

print "This is an example of the die and warn functions being used with the \
|| operator \n"

open (EXAMPLE
```

## 第 6 模块：文件与目录的操作 193

该语句返回真。正如此，你可以使用语句（例如 `if` 语句）来判断操作是否成功。让我们来看一个打开文件的简短编程示例。

## 注意

标准做法是在完成对文件的工作后关闭它。在这个示例中，我们不会关闭文件，因为我们还没有介绍关闭操作。

![](img/2070407c4a70134aab89572f10d21e60_216_0.png)

上一个编程示例（在当前工作目录中打开文件）的输出如插图所示。

## 第 6 模块：文件与目录的操作 194

## 195

## 196 | Perl：初学者指南

现在你已经知道了如何打开文件，你可以以三种模式打开它们：读、写和追加。默认情况下，所有文件以读模式打开，这允许你读取文件内容而不对其更改。

你可以打开文件的另一种模式是写模式，这对用户来说是危险的。当你以写模式打开文件时，所有内容都会被破坏。你删除的内容将被对该文件的写入所取代。我们将在本模块稍后部分介绍如何写入文件。如果你想以写模式打开文件，需要在文件名和路径前加上一个大于符号 `>`。以下是打开文件的 `>` ：

```
Open (EXAMPLE, "D:/Perl/book/test.txt");
```

一旦 `example.txt` 以写模式打开，它的内容将被移除，除非向文件写入任何内容，否则它将包含零字节。写模式适用于你每次都重写文件内容的情况。

另一种打开文件的模式是追加模式，它允许向文件中添加内容而不破坏当前内容。当你使用追加模式时，你无法读取文件的现有内容。要以这种模式打开文件，你需要在文件名和路径前加上两个大于符号 `>>`。它在程序中看起来如下：

```
Open (EXAMPLE, "D:\Perl\book\test.txt");
```

追加模式适用于你需要向文件添加内容无需读取当前内容的情况。如果你想以读写模式打开文件且不想损坏文件内容，可以在文件名和路径前加上一个加号 `+` 和一个小于符号 `<`。这个字符序列 `+<` 表示文件已以读写模式打开。

现在你已经知道了如何打开文件，你需要学习如何关闭文件。记住，文件句柄是整个过程中文件的引用

## 模块 6：文件与目录的操作 197

它在程序中的生命。要关闭文件，你必须使用此文件句柄。以下是 `close` 语句的语法：

`close (file handle);`

该语句自俗易懂。一旦你完成对打开的文件的操作，应该始终使用此语句关闭文件。包含以下程序，以作为 `close` 语句使用的示例：

```perl
#!/usr/bin/perl

print "This program will open an example file \n"

print "This is an example of the die and warn functions used with the || operator \n";

open(EXAMPLE, "example.txt") || die("Could not open example.txt \n");

close(0);
```

使用 `close` 语句关闭 `example.txt` 的示例

我们对打开和关闭文件的讨论到此结束。你应该能够熟练执行这些语句。现在，让我们进入下一节，介绍在文件打开后你可以对其进行的一些操作。

# 1分钟演练

- 如果你想在每次打开文件时重写内容，应该以什么模式打开文件？什么字符代表这种模式的使用？
- 文件打开后，始终使用什么来引用它？

## 读取和写入文件

本模块的上一节教了你如何打开和关闭文件。现在你已经掌握了这些信息，让我们讨论对文件进行读取和写入。我们从一些

- 写入模式， `>`
- 句柄

## 198 Perl：初学者指南

更简单的文件操作方法，并用一些高级概念结束本节。你知道打开文件时使用的默认模式是读取模式（Read mode）。这种模式允许你读取文件内容。与此，标准输入文件是 `STDIN`，这意味着如果你不使用文件句柄指定特定的文件进行读取，用户输入将作为信息源。与 `STDIN` 一样，文件句柄和从该打开文件中读取的输入行可以保存到程序中的变量中。让我们来看一个程序，它将打开文件并使用指定的句句柄从该文件中读取第一行信息。

## 注意

记住，行尾是由回车符标记的。

| 这一行代码将读取文件中的所有内容，直到遇到第一个回车符，并将所有信息保存为变量中的字符串 |

```perl
#!/usr/bin/perl

print "This program will open an example file \n"

open(EXAMPLE, "D:\Perlbook\test\example.txt") || die("Could not open example.txt: $!");

$text = <EXAMPLE>;

print "The first line of text read from the file is \n \n$text\n";
```

这一行代码简单地输出了 `$text` 变量的内容

上一个从文件中读取信息的编程示例的输出如插图所示

![](img/2070407c4a70134aab89572f10d21e60_221_0.png)

## 模块 6：文件与目录的操作

上一个示例演示了如何从文件中读取的一行信息。如果你想显示文件中所有的行信息，你必须将赋值语句放在循环中，每次循环都检查是否有另一行文本需要读取。以下程序是读取和显示整个文件的一种方法：

这一行使用文件句柄 "EXAMPLE" 打开

这一行使用文件句柄从文件中读取第一行信息

```perl
#!/usr/bin/perl

print "This program will read an entire file \n \n";

open (EXAMPLE, "D:\perl\book\test\example.txt") || die("Could not open example.txt\n");

$text = <EXAMPLE>;

while ($text) {

    print "$text\n";

    $text = <EXAMPLE>;

}
```

这是我们用于检查文件中其他信息的 `while` 语句

这是另一个与第 5 行完全相同的赋值语句，但该语句会在每次 `while` 语句满足条件时执行

我们需要打印 `$text` 的内容，它将包含第一次通过循环赋值的第一行信息

接下来的插图显示了上一个从文件读取并输出所有信息的编程示例的输出：

```text
C:\Perl\book>figure6.code.pl

This program will read an entire file

The first line from example.txt

The second line from example.txt

The third line from example.txt

C:\Perl\book>
```
