

⇒ 这里有两种使用方法。

- 要输出文件 `placement-list` 的末尾部分，从第三行开始，输入：
  `$ tail +3 placement-list [RET]`
- 要输出文件 `placement-list` 的末尾部分，从第100个字符开始，输入：
  `$ tail -c +100 placement-list [RET]`

有时持续查看文件的末尾是有用的；这对于“增长中”的文件很有用，即正在被另一个进程写入的文件。要持续查看此类文件的末尾，请使用带有 `-f`（“跟随”）选项的 `tail`。输入 `CTRL-C` 以停止查看文件。

⇒ 要跟随文件 `access_log` 的末尾，输入：

  `$ tail -f access_log [RET]`

注意：你也可以使用 `less` 实现相同的结果；为此，在浏览文本时输入 `F`（参见 Recipe 9.1 [Perusing Text]，第 211 页）。

## 9.2.4 显示文本的中间部分

有几种方法可以只输出文本的中间部分。

### METHOD #1

要输出文件的某一行，使用 `sed`（参见 Recipe 10.5 [Editing Streams of Text]，第 255 页）。将要输出的行号后跟 `!d` 作为 `sed` 的引号参数；将要输出的文件名作为第二个参数给出。

⇒ 要输出文件 `placement-list` 的第 47 行，输入：

  `$ sed '47!d' placement-list [RET]`

要输出多于一行的区域，请给出起始和结束行号，用逗号分隔。

⇒ 要输出文件 `placement-list` 的第 47 到 108 行，输入：

  `$ sed '47,108!d' placement-list [RET]`

### METHOD #2

要输出某些文本的中间部分，你也可以在管道上组合多个 `head` 或 `tail` 命令（参见 Recipe 3.2.4 [Redirecting Output to Another Command’s Input]，第 69 页）。

⇒ 这里有一些使用方法。

- 要输出文件 `placement-list` 中的第10行，输入：
  `$ head placement-list | tail -1 [RET]`
- 要输出文件 `placement-list` 末尾的第五和第四行，输入：
  `$ tail -5 placement-list | head -2 [RET]`
- 要输出 `placement-list` 中的第500个字符，输入：
  `$ head -c500 placement-list | tail -c1 [RET]`
- 要输出文件 `placement-list` 第五行上的第一个字符，输入：
  `$ head -5 placement-list | tail -1 | head -c1 [RET]`

在前面的示例中，使用了三个命令：文件 `placement-list` 的前五行被传递给 `tail`，它输出输出中的最后一行（文件中的第五行）；然后，最后一个 `head` 命令输出该最后一行中的第一个字符，从而达到所需结果。

## 9.2.5 显示字符串之间的文本

使用 `sed` 选择字符串之间的文本行，并输出仅该文本段，或除该段之外的所有文本行。字符串可以是单词甚至正则表达式（参见 Recipe 14.3 [Matching Patterns of Text]，第 335 页）。

使用 `-n` 选项运行 `sed`，后跟 `'/first/,/last/p'` 以仅输出字符串 `first` 和 `last` 之间的文本，包含两者。这对于输出文本文件中的某一章或某一节很有用，当你知道用于开始各节的文本时。

⇒ 要输出文件 `book-draft` 中从“Chapter 3”到“Chapter 4”的所有文本，输入：

```
$ sed -n '/Chapter 3/,/Chapter 4/p' book-draft [RET]
```

要输出除两个模式之间的所有文本行之外的内容，请省略 `-n` 选项。

⇒ 要输出文件 `book-draft` 的所有文本，除了位于文本“Chapter 3”和“Chapter 4”之间的部分，输入：

```
$ sed '/Chapter 3/,/Chapter 4/d' book-draft [RET]
```

注意：有关 SED 的更多信息，请参见 Recipe 10.5 [Editing Streams of Text]，第 255 页。

## 9.2.6 显示文本的字面字符

有工具可以显示字面字符——文本格式化的方式，使你能够清晰且无歧义地看到每个字符及其在文件中的位置。以下方法展示了如何使用这些工具。

### METHOD #1

使用 `od`，即“八进制转储”工具，并带 `-c` 选项来显示某些文本中的 ASCII 字符。这会将字符每行分组 16 个，用空格分隔，并在可能的情况下为控制字符提供反斜杠转义。左侧显示一列，包含该行中第一个字符的偏移量（文件中的字节数）。使用 `-A` 选项并给出 `d` 作为参数，以十进制而不是默认的八进制输出这些数字。

⇒ 这里有一些使用方法。

- 要以每行 16 个字符分组显示文件 `details` 中的字面字符，并以偏移号作为每行前缀，输入：
  `$ od -Ad -c details [RET]`
- 要输出文件 `details` 的最后一行中的字面字符，输入：
  `$ tail -1 details | od -Ad -c [RET]`

### METHOD #2

你可以用 `hexdump` 获得与 `od` 相同的效果。使用 `-c` 选项，它会将文件中的每个字节显示为其代表的字符。与方法 #1 相同，每行显示 16 个输入字符，用空格分隔，并在左侧写入一列显示文件的偏移值，不同之处在于此处偏移以十六进制给出。

⇒ 要以每行 16 个字符分组显示文件 `exam` 中的字面字符，并以十六进制偏移号作为每行前缀，输入：

```
$ hexdump -c exam [RET]
```

## 9.2.7 显示文本的十六进制值

所有文本字符都以磁盘上的数值形式存储（参见 Recipe 9.3.7 [Viewing a Character Set]，第 228 页）。有时你可能想显示文本字符的值，而不是这些值所代表的字符。这对于检查包含非打印字符的文本文件的字面内容，或显示构成二进制文件的字面字符很有用。

