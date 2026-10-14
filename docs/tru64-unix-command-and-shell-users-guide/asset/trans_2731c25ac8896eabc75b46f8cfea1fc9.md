

现在在你的示例文件上再试一次替换。按如下方式使用 $（转到最后一行）、o（创建新行）、yy（ yank ）和 p（粘贴）命令向文件中添加三行新文本：

```
:$ Return
o
Some new text with a misspelling. Escape
yy
p
p
p
```

你现在应该有四行新文本，都包含拼写错误的单词 misspelling。

要修复拼写错误，输入以下其中一个命令：

```
:1,$s/misepelling/misspelling/ Return
```

或

```
:5,8s/misepelling/misspelling/ Return
```

在第一个示例中，地址 1,$ 表示替换应从第一行（1）开始，到文件的最后一行（$）结束。在第二个示例中，5,8 表示替换应从第五行开始，到第八行结束。在任何一种情况下你都不需要使用 g 操作符，因为每个行上只需要更改一次。

## A.3.2 写入整个文件或文件的一部分

:wq 命令是 ex 命令中的一个特殊命令，用于写入整个文件。它结合了写命令 w 和退出命令 q 的功能。quit 命令唯一可以接受的参数是感叹号（!）。它强制会话退出，即使退出会导致对文件的更改丢失。

w 命令也可以接受地址和文件名参数，这让你可以将文本的一部分保存到另一个文件。例如，要将文本的前三行保存到新文件 my.new.file，请使用以下命令：

```
:1,3w my.new.file Return
```

```
"my.new.file" [New file] 3 lines, 130 characters
```

## A.3.3 删除一段文本

ex 中删除命令是 d，就像在 vi 中一样。要从当前行删除到文件末尾，请使用以下命令：

```
: ., $d Return
```

## A.3.4 自定义你的环境

ex 编辑器提供了两种自定义你的 vi 环境的机制。你可以使用 :set 命令设置环境变量，并使用 :map 命令将键序列映射到 vi 命令键。

环境变量要么通过将它们设为选项或布尔变量的非选项来设置，要么通过将它们设为 option=value 来设置。完整的环境变量集在 ex(1) 参考页中有描述。表 A-5 列出了一些常见变量。

### Table A-5: Selected vi Environment Variables

| Variable | Description |
|---|---|
| errorbells | 指定当出现错误时，响铃声响起。这是默认设置。 |
| ignorecase | 指定在执行搜索时，应忽略字符的大小写。默认变量设置是 noignorecase。 |
| number | 指定在左边界显示行号。默认变量设置是 nonumber。 |
| showmatch | 指定当你输入匹配的括号或大括号时，光标会移动到匹配字符然后返回。默认变量设置是 noshowmatch。 |
| tabstop | 指定制表符之间的空格量。默认设置是 tabstop=8。 |

### Table A–5: Selected vi Environment Variables (cont.)

| Variable | Description |
|---|---|
| `wrapscan` | 指定搜索应在文件开头或结尾处换行。默认变量设置是 wrapscan。 |
| `wrapmargin` | 在距屏幕右侧指定数量字符处创建自动右边界。每当光标到达指定的右边界时，就会生成自动换行，并且你正在输入的单词会被带到下一行。默认设置是 `wrapmargin=0`。你应该将 wrapmargin 变量设置为你舒适的值。否则，vi 将使用默认值 0。使用默认值意味着当光标到达屏幕末尾时它会跳到下一行；然而，你键入的单词的部分可能在单独的行上。 |

要显示示例文件的行号，输入以下命令：

```
:set number  Return
```

要移除行号，输入以下命令：

```
:set nonumber  Return
```

:map 命令将单个 vi 命令键设置为 vi 命令序列。:map 命令的语法如下：

```
:map key sequence  Return
```

此命令序列会替换该键的任何现有命令。命令序列应与你想要映射的击键相同，只是诸如 Return 键、Escape 键和用 Ctrl 键修改的键等特殊键必须先用 Ctrl-V 加引号。因为 q 和 v 键没有关联的命令，所以它们是很好的映射键。

例如，要映射一个插入文本行到你的文本中，该行内容为 "This space held for new text"，你可以使用以下命令：

```
:map q oThis space held for new text  Ctrl/V  Escape  Return
```

注意使用 Ctrl/V 来引用 Escape 字符。

