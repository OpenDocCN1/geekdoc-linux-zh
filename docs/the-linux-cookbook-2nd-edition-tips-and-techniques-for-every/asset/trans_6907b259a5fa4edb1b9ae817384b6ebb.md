

stream and replace it with some other pattern in the output stream is “s/searchpattern/replacepattern/g”; to filter the output of a command, you can quote this command as an argument to sed and put it on a pipeline.

⇒ 要输出当前月份的日历，并将所有“1”字符替换为“1”字符，输入：

```
$ cal | sed 's/1/1/g' [RET]
```

此示例使用 cal 显示日历（参见 Recipe 27.3.1 [Displaying a Calendar], page 539）。cal 的输出由 sed 编辑，然后发送到标准输出。

你也可以通过将某个 filespec 作为第二个参数给出，使用 sed 编辑文件的内容；文件的內容会连同指定的编辑更改一起发送到标准输出，而原始文件不会被更改。

⇒ 以下是两种使用方法。

- 要输出文件 remarks 的内容，将其中“quite pleased;”的每个实例替换为“absolutely delighted,”，输入（全部在一行上）：
  
  `$ sed 's/quite pleased/absolutely delighted/g' remarks` [RET]

- 要输出当前目录中所有文件名以 remarks 结尾的文件的内容，将其中“surprised”和“nearly shocked”的每个实例替换为“utterly astounded,”，输入（全部在一行上）：
  
  `$ sed 's/surprised\|nearly shocked/utterly astounded/g' *remarks` [RET]

**NOTES:** 有关 sed 的更多信息，请参阅附录 D [References for Further Interest], page 731。

## 10.6 串联文本

cat 工具之所以得名，是因为它会将提供给它的所有文本串联起来，并将合并后的结果输出到标准输出。可以把它看作是将一段文本链接到另一段文本的方式；你可以创建任意长度的链条。这对于将文本文件串联成新文件非常有用。

例如，假设你有两个文件，early 和 later。文件 early 看起来像 Figure 10-3，而文件 later 看起来像 Figure 10-4。

### Figure 10-3. The early file.

```
This Side of Paradise
The Beautiful and Damned
```

### Figure 10-4. The later file.

```
The Great Gatsby
Tender Is the Night
The Love of the Last Tycoon
```

⇒ 要将这些文件串联到一个新文件 novels 中，输入：
$ cat early later > novels [RET]

此命令将标准输出重定向到一个新文件 novels，其内容将看起来像 Figure 10-5。文件 early 和 later 未被更改。

### Figure 10-5. The novels file.

```
This Side of Paradise
The Beautiful and Damned
The Great Gatsby
Tender Is the Night
The Love of the Last Tycoon
```

如果你改为运行 cat later early > novels，则文件会以相反的顺序串联，从 later 开始；因此文件 novels 将看起来像 Figure 10-6。

### Figure 10-6. The novels file reversed.

```
The Great Gatsby
Tender Is the Night
The Love of the Last Tycoon
This Side of Paradise
The Beautiful and Damned
```

以下各节提供了串联文本的其他配方。

NOTES: 你也可以使用 cat 串联非文本文件，但它最流行的用法是与文本文件一起使用。另一种以自动化方式串联文本文件的方法是使用文件包含——参见 Recipe 10.7 [Including Text from Other Files], page 261。

一个类似的工具，zcat，可用于压缩文件的内容。

### 10.6.1 写入文件中的文本

有时，调用文本编辑器来完成特定任务太麻烦了——你只想用两行内容创建一个文本文件，或者只想向文本文件追加一行。有很好的方法可以在没有文本编辑器的情况下完成这类微编辑工作。

要不使用文本编辑器写入文本文件，请将 cat 的标准输出重定向到要写入的文件。然后你可以输入文本，在单独的一行上输入 CTRL-D 以结束文件。这在你想快速创建一个小型文本文件时很有用，仅此而已；通常，你会在文本编辑器中打开或创建文本文件，如本章前几节所述。

⇒ 要创建一个包含一些文本的文件 novels，输入：

```
$ cat > novels RET
This Side of Paradise RET
The Beautiful and Damned RET
The Great Gatsby RET
Tender Is the Night RET
CTRL-D
$
```

在此示例中，文本文件 novels 被创建并包含四行文本（带 CTRL-D 的最后一行永远不会成为文件的一部分）。

在没有编辑器的情况下输入文本有时可以应付，但如果你犯了错误，几乎没有补救办法——你可以输入 CTRL-U 来删除当前行，并输入 CTRL-C 来中止整个操作，根本不将文本写入文件，但就这些了。

### 10.6.2 向文件追加文本

要不打开文件在文本编辑器中向文本文件添加文本，请使用 cat 和追加操作符 >>。 （使用 > 则会覆盖文件。）

⇒ 要在文件 novels 底部添加一行文本，输入：

```
$ cat >> novels RET
The Love of the Last Tycoon RET
CTRL-D
```
