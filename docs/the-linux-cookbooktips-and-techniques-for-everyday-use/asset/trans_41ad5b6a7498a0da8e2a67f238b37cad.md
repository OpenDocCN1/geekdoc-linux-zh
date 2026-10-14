

此命令在小说文件开头插入两行文本，该文件即本节前面示例中使用过的文件。此文件现在将包含以下内容：

```
The Novels of F. Scott Fitzgerald
--------------------------------
This Side of Paradise
The Beautiful and Damned
The Great Gatsby
Tender Is the Night
The Last Tycoon
```

## 11.7 包含文本文件

```
@sf(Debian): `m4'
```

文件包含是指可以通过在另一个文件中的特定位置指定文件名，就将一个文件的内容包含到另一个文件中的某个位置。

如果您想要或需要频繁地重新排列文档的各个部分或章节，如果您需要以多种排列方式保存文档，或者如果您有一些文本段落经常需要在多个文档中插入，那么这种方法就很有用。对于这些情况，您可以将每个部分保存在单独的文件中，并创建一个包含文件，其中包含各个部分的文件名，按您希望生成该文件的顺序排列。

要在文本文件中包含一个文件，请在单独的一行中指定要包含的文件，如下所示：

```
include(`file')
```

当您处理此文件以进行包含时，包含 `include'` 语句的那一行将被文件 file 的内容替换（其路径相对于包含文件的当前目录）。

使用 m4 工具，即 GNU 宏处理器，来处理包含文件。它以包含文件的名称作为参数，并将包含结果输出到标准输出。您可以使用重定向将输出重定向到文件。

例如，假设文件 `soups` 包含以下文本：

```
Clam Chowder
Lobster Bisque
Vegetable
```

假设文件 `sandwiches` 包含以下文本：

```
BLT
```

最后，假设文件 `menu` 包含以下文本：

```
Ham on Rye
Roast Beef
```

```
Diner Menu For Today

Soups
-----

include(soups)

Sandwiches
------------

include(sandwiches)
```

- 要处理该文件并写入文件 `monday.txt`，请输入：

```
$ m4 menu > monday.txt
```

此命令写入一个新文件 `monday.txt`，其内容如下所示：

```
Diner Menu For Today

Soups
-----

Clam Chowder
Lobster Bisque
Vegetable

Sandwiches
------------

BLT
Ham on Rye
Roast Beef
```

*注意：* 您可以编写多个包含文件来使用您的文件——而且文件本身也可以有自己的包含文件。

这只是 m4 的一个相当简单的用法；它可以做更多的事情，包括运行命令、操作文本和运行自定义宏。有关此工具的更多信息，请参阅 Info 文件 `m4.info`，节点 `Top`。

## The Linux Cookbook: Tips and Techniques for Everyday Use:

[ < ] [ > ]   [ << ] [ Up ] [ >> ]   [Top] [Contents] [Index] [ ? ]

## 12. Grammar and Reference

在基于 Linux 的系统上进行写作和编辑的工具和资源包括拼写检查器、词典和参考文件。本章展示了使用它们的方法。

- 12.1 Spelling
- 12.2 Dictionaries
- 12.3 Checking Grammar
- 12.4 Word Lists and Reference Files

拼写检查。
语法工具。
词表和参考文件。

### 12.1 Spelling

在 Linux 上有几种拼写检查文本和文件的方法；以下配方展示了如何查找特定单词的正确拼写以及如何执行批处理、交互式和基于 Emacs 的拼写检查。

系统词典文件 `/usr/dict/words` 只是一个词表（尽管非常庞大），按字母顺序排序，每行包含一个单词。与大小写无关而正确的单词以小写字母列出，而依赖某种形式的 capitalization 才能正确的单词（如专有名词）则以该形式出现。所有 Linux 拼写工具都使用此文本文件来检查拼写；如果某个单词未出现在词典文件中，则被视为拼写错误。

> 注意：没有任何计算机化拼写检查工具会在您一开始就使用错误的词时纠正您的写作——例如，如果您写了 `there` 而本意是 `their`，计算机是不会捕捉到的（至少目前不会！）。

- 12.1.1 Finding the Correct Spelling of a Word
- 12.1.2 Listing the Misspellings in a Text
- 12.1.3 Keeping a Spelling Word List
- 12.1.4 Interactive Spell Checking
- 12.1.5 Spell Checking in Emacs

拼写检查一个单词。
拼写检查一个文件。
保留个人词典。
交互式拼写检查。
在 Emacs 中拼写检查。

