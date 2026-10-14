

NOTES: 此正则表达式仍会输出仅包含制表符的行。

## METHOD #3

要从输出中删除所有空行，以及仅包含制表符或空格字符组合的行，请使用 grep 并以 "^[[:space:]]." 作为要搜索的正则表达式。它使用特殊的预定义 "[:space:]" 正则表达式类，可匹配任何类型的空格字符，包括制表符。

⇒ 要仅输出文件 term-paper 中包含不止空格或制表符字符的行，请键入：

```
$ grep '^[[:space:]].' term-paper RET
```

## METHOD #4

如果文件是双倍行距，其中所有偶数行都是空白，则可以使用 sed 并使用 "n;d" 表达式从输出中删除这些行。

⇒ 要仅输出文件 term-paper 的奇数行，请键入：

```
$ sed 'n;d' term-paper RET
```

## 13.1.3 Double-Spacing Text

要双倍行距文本，在原始文本的每行之间插入一行空白行，请使用带有 -d 选项的 pr 工具。默认情况下，pr 会分页文本，并在每页顶部加上当前日期、时间和页码的页眉；使用 -t 选项可省略此页眉。

⇒ 以下是两种使用方法。

- 要对文件 term-paper 进行双倍行距并将输出写入文件 term-paper.print，请键入：
  $ pr -d -t term-paper > term-paper.print RET

- 要对文件 term-paper 进行双倍行距并将输出直接发送到打印机进行打印，请键入：
  $ pr -d -t term-paper | lpr RET

NOTES: pr（"print"）工具是文本预格式化工具，常用于分页和以其他方式准备文本文件以便打印；有关此工具使用的更多讨论，请参阅 Recipe 13.3 [Paginating Text]，第 312 页。

## 13.1.4 Triple-Spacing Text

要三倍行距文本，在原始文本的每行之间插入两行空白行，请使用带有 "G;G" 表达式的 sed。

⇒ 要对文件 term-paper 进行三倍行距并将输出写入文件 term-paper.print，请键入：
$ sed 'G;G' term-paper > term-paper.print [RET]

"G" 表达式会在 sed 输出的每一行后附加一行空白行；使用 ";" 你可以指定要附加的空白行数（但你必须引用此命令，因为分号 (;) 对 shell 有意义——请参阅 Recipe 3.1.3 [Quoting Reserved Characters]，第 56 页）。你可以使用多个 "G" 字符来输出具有双倍或三倍以上行距的文本。

⇒ 要对文件 term-paper 进行四倍行距，并将输出写入文件 term-paper.print，请键入：
$ sed 'G;G;G' term-paper > term-paper.print [RET]

NOTES: SED 的说明见 Recipe 10.5 [Editing Streams of Text]，第 255 页。

## 13.1.5 Adding Line Breaks to Text

有时文件在每行末尾没有换行符（这在文件在操作系统之间转换时很常见）。要为没有换行符的文件添加换行符，请使用文本格式化程序 fmt。它输出按指定宽度排列的文本；如果未指定宽度，则格式化文本的宽度为每行 75 个字符。

⇒ 要输出文件 term-paper，使行长不超过 75 个字符，请键入：
$ fmt term-paper [RET]

使用 -w 选项指定最大行宽，以字符为单位。

⇒ 要输出文件 term-paper，使行长不超过 80 个字符，请键入：
$ fmt -w 80 term-paper [RET]

## 13.1.6 Adding Margins to Text

为文本提供更大的左边界在你想打印一份副本并打孔以用于三孔活页夹时尤其好。

要输出具有更大左边界的文本文件，请使用 pr 并将文件名作为参数；给出 -t 选项（以禁用页眉和页脚），并作为 -o 选项的参数给出偏移文本的空格数。将空格数添加到页面宽度（默认值为 72）并将此新宽度指定为 -w 选项的参数。

⇒ 以下是两种使用方法。

- 要将文件 list2 中每八个前导空格字符转换为制表符，并将输出写入 list，请键入：
  $ unexpand -t 8 list2 > list [RET]
- 要将文件 list2 中所有八个空格字符出现的位置转换为制表符，并将输出写入标准输出，请键入：
  $ unexpand -a list2 [RET]

要指定要转换为制表符的空格数，请将该数字作为 -t 选项的参数给出。

⇒ 要将 list2 中的每个前导空格字符转换为制表符，并将输出写入标准输出，请键入：
  $ unexpand -t 1 list2 [RET]

NOTES: 你也可以使用带有 -x 选项的 col 将其输入中的所有制表符转换为空格。

## 13.1.8 Removing or Replacing Newline Characters

换行符，由许多命令表示为 "\n" 反斜杠转义序列，是终止每一行的字符。使用 tr 来删除它或将其替换为其他内容。

要删除换行符，请使用 -d 选项并给出要删除的引号集中的换行符。

⇒ 要从文件 many 中的文本中删除任何换行符，然后将其写入文件 single，请键入：
  $ tr -d '\n' < many > single [RET]

要将换行符替换为其他字符，请使用 tr，将换行符作为第一个引号集，将要替换它的字符作为第二个。

⇒ 要从文件 many 中的文本中将任何换行符替换为换页符，然后将输出发送到打印机，请键入：
  $ tr '\n' '\f' < many | lpr [RET]

## 13.1.9 Removing Carriage Return Characters

在 Linux 中，与所有类 Unix 系统一样，文本文件中的行仅以换行符结束，表示为 "\n"（因此当你按下 [RET] 键时，就是这个字符

