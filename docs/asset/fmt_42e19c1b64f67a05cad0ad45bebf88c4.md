
```
$ sed '3ia\n> is an inserted line.' data6
This is line number 1.
This is line number 2.
This is an inserted line.
This is line number 3.
This is line number 4.
$
```

这是一个在数据流的 3 之后追加新行的示例：

```
$ sed '3a\n> is an inserted line.' data6
This is line number 1.
This is line number 2.
This is line number 3.
This is an inserted line.
This is line number 4.
$
```

这使用的过程与插入命令相同；如果你有一个多行数据流，并且想在数据流的末尾追加新行文本，只需使用我们的新朋友美元符号，它代表最后一行数据：

```
$ sed '$a\n> This is a new line of text.' data6
```

437

# 第三部分 高级 Shell 脚本

This is line number 1.

This is line number 2.

This is line number 3.

This is line number 4.

This is a new line of text.

如果你想在数据流的开头添加新行，原理是相同的。

在第一行之前插入一个新行。

要插入或追加多行文本，你必须在每一行新文本后使用反斜杠，直到达到你想要插入或追加文本的最后一行：

```
$ sed 'li|
> This is one line of new text.\n> This is another line of new text.' data6
This is one line of new text.
This is another line of new text.
This is line number 1.
This is line number 2.
This is line number 3.
This is line number 4.
$
```

这两个指定的行都将添加到数据流中。

# 修改行

更改命令允许你修改整行的内容。它与插入和追加命令的方法相同，即必须单独指定新行：

```
$ sed '3c\n> This is a changed line.'
This is line number 1.
This is line number 2.
This is a changed line.
This is line number 4.
$
```

在这个例子中，`sed` 编辑器修改了第 3 行。你也可以使用文本作为地址：

```
$ sed '/number 3/\n> This is a changed line.'
This is line number 1.
This is line number 2.
This is a changed line.
This is line number 4.
$
```

# 引入 sed 和 awk 16

文本模式命令将更改数据流中匹配的任何行文本。

```
$ sed '/number/1c\
> This is a changed line.' data7
This is a changed line.
This is line number 2.
This is line number 3.
This is line number 4.
This is a changed line.
This is yet another line.
This is the last line in the file.
$
```

你可以在更改命令中使用地址范围，但结果可能不是你预期的：

```
$ sed '2,3c\
> This is a new line of text.' data6
This is line number 1.
This is a new line of text.
This is line number 4.
$
```

而不是修改这两行，`sed` 编辑器使用单行文本来替换这两行。

# 转换命令

转换命令 `y` 是 `sed` 编辑器唯一操作单个字符的。转换命令使用的格式为：

```
[address]/inchars/outchars/
```

转换命令对 `inchars` 和 `outchars` 的值执行一对一映射。`inchars` 中的第一个字符转换为 `outchars` 中的第一个字符。`inchars` 中的第二个字符转换为 `outchars` 中的第二个字符。这种映射持续到指定字符的长度。如果 `inchars` 和 `outchars` 的长度不相同，`sed` 编辑器将产生错误消息。

使用转换命令的简单示例是：

```
$ sed 'y/123/789/'
This is line number 7.
This is line number 8.
This is line number 9.
This is line number 4.
This is line number 7 again.
This is yet another line.
This is the last line in the file.
$
```

439

## 高级 Shell 脚本

从输出可以看出，`inchars` 模式中指定的每个字符实例都被 `outchars` 模式中相同位置的字符所替换了。

`transform` 命令是一个全局命令，也就是说，它会自动对行中找到的任何字符进行转换，而不忽略其出现的次数：

```
$ echo "This 1 is a test of 1 try." | sed 'y/123/456/'
This 4 is a test of 4 try.
$
```

编辑器转换了文本行中匹配的字符 1 的两个实例。你无法将转换限制为该字符的特定出现次数。

## 重新回顾打印

“替换选项（Substitution Options）”部分展示了如何使用替换命令配合 `p` 标志来显示编辑器修改过的行。还有这三个命令也可以用于从数据流中打印信息：

- 小写 `p` 命令用于打印文本行
- 等号 `=` 命令用于打印行号
- `l` 命令用于列出一行

接下来的章节将查看 `sed` 编辑器中这三个打印命令的每一个。

## 打印行

与替换命令中的 `p` 标志类似，`p` 命令在 `sed` 编辑器输出中打印一行。单独使用它并没什么大不起的：

```
$ echo "this is a test" | sed 'p'
this is a test
this is a test
$
```

它所做的只是打印你已经知道那里存在的数据。打印命令 `print` 最常见的用法是打印包含来自文本模式的匹配文本的行：

```
$ sed -n '/number 3/p' data6
This is line number 3.
$
```

通过在命令行使用 `-n` 选项，你可以抑制所有其他行，只打印包含匹配文本模式的行。

你也可以将此作为快速打印数据流中部分行的的方法：

```
$ sed -n '2,3p' data6
This is line number 2.
```

这里是第 3 行。

$ 

## 介绍 sed 和 gawk

`print` 命令的另一个用途是当你需要在行被修改之前查看它，例如使用替换或更改命令时。你可以创建一个脚本在行更改之前显示它：

```
$ sed -n '/3/l
p
s/line/test/p
' data6
This is line number 3.
This is test line number 3.
$
```

此 `sed` 编辑器搜索包含数字 3 的行，然后执行两个命令。首先，脚本使用 `p` 命令打印行的原始版本，然后它使用 `s` 命令替换文本，并带有 `p` 标志打印结果文本。输出显示了原始行文本和新行文本。

## 打印行号

等号命令 `=` 显示数据流中当前行的行号。行号是由数据流中的换行符决定的。每当数据流中出现换行符时，`sed` 编辑器就认为它结束了一行文本。

等号命令的基本用法并不太令人兴奋：

```
$ sed '=' datal
1
The quick brown fox jumps over the lazy dog.
2
The quick brown fox jumps over the lazy dog.
3
The quick brown fox jumps over the lazy dog.
4
The quick brown fox jumps over the lazy dog.
$
```

`sed` 编辑器在实际的文本行之前打印行号。如果你在数据流中搜索特定的文本模式，等号命令就会派上用场：

```
$ sed -n '/number 4/l
=
p
' data6
4
This is line number 4.
$
```

## 第三部分 高级 Shell 脚本
