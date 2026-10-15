
# The vi history

The vi editor is a text editor which is supported by most of the UNIX operating systems.

```

The vi history

UNIX operating systems.

```

The vi history

UNIX operating systems.

The vi editor is a text editor

```

使用光标移动键，将光标放在第一行的任意字符上。

按`[P]`；vi 将被删除的行放在当前行上方。

```

The vi editor is a text editor which is supported by most of the

The vi history

UNIX operating systems.

The vi editor is a text editor supported by most of the

```

被删除的文本仍留在临时缓冲区中，你可以将它的副本移动到文件的不同位置。

### 6.2.2 复制行：`[y][y]` 和 `[p]` 或 `[P]`

使用`yank`（复制）和`put`运算符，你可以将文本从文件的部分复制到另一个部分。

- 按`[y][y]`；vi 将当前行复制到临时缓冲区中。
- 使用光标移动键将光标放在第一行。
- 按`[p]`；vi 将临时缓冲区的内容复制到当前行下方。

```

The vi history

The vi editor is a text editor which is supported by most of the

Unix operating systems.

```

```
The vi history.
The vi editor is a text editor which is supported by most of the
The vi editor is a text editor which is supported by most of the
UNIX operating systems.
```

- 使用光标移动键将光标移动到最后一行。
- 按`[P]`；vi 将临时缓冲区的内容复制到当前行上方。

```
The vi history
The vi editor is a text editor which is supported by most of the
The vi editor is a text editor which is supported by most of the
The vi editor is a text editor which is supported by most of the
UNIX operating systems.
```

复制的文本将留在临时缓冲区中，直到下一次删除或复制操作，你可以将此缓冲区的内容复制到文件的任何地方，并根据需要重复多次。

## vi 运算符的作用范围

在第 4 章中，你学习了基本的 vi 命令；然而，许多 vi 命令作用于文本块。文本块可以是一个字符、一个单词、一行、句子或其他指定的字符集合。使用带有范围（scope）键的 vi 命令可以让你对编辑任务有更强的控制力。这类命令的格式可以表示为：

```
command = operator + scope
```

没有特定的范围键来表示整行。为了将整行作为命令的范围，你需要双击光标编辑器的按键。例如，`[d][d]` 删除一行，`[y][y]` 复制一行。表 6-2 总结了与命令组合使用的一些常用范围键。以下示例演示了范围的使用。要遵循这些示例，请从`myfirst`文件开始。在该文件上使用`delete`、`yank`和`change`运算符。

## 使用范围键使用删除运算符

从光标位置到行尾删除文本：表 6–2 一些范围键。

| 范围 | 操作 |
| :--- | :--- |
| `$` | 从光标位置到行的末尾。 |
| `0` (零) | 从光标之前的位置到行的开头。 |
| `e` | 从光标位置到单词的末尾。 |
| `b` | 从光标之前的字符到单词的开头。 |

按`[d][$]`；vi 删除光标位置到行尾的文本，并将光标移动到此处。

```

The vi history

The vi editor is a text editor which is supported by most of the UNIX operating systems.

```

可以使用`[u]`或`[U]`撤销最近的更改。

```

The vi history

UNIX operating systems.

```

要从光标位置到行开头删除文本，按`[d][0]`；vi 删除文本并将光标留在`m`上。

```

The vi history

The vi editor is a text editor which is supported by most of the UNIX operating systems.

```

删除光标位置后的一个单词，按`[d][w]`；vi 删除该单词及其后的空格，并将光标移动到字母`o`。

## 无边界 UNIX：一种入门方法

```

The vi history

The vi editor is a text editor which is supported by most of the

UNIX operating systems.

```

```

The vi history

UNIX operating systems.

```

要删除光标位置后的多个单词（例如，三个单词），按`[d][d][w]`；vi 删除三个单词（most, of, the）及其后的空格，并将光标移动到单词`by`之后的空格。

```

The vi history

The vi editor is a text editor which is supported by most of the

UNIX operating systems.

```

```

The vi history

of the the.

```
