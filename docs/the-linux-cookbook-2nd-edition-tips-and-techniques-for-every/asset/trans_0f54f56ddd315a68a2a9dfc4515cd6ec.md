

在本例中，只有包含单词“CD”的行会被打印；包含“CDROM”或“anecdote”等单词的行不会被打印，除非它们包含单词“CD。”²

> ² 然而，单词“CD-ROM”会被视为匹配；grep 将连字符视为单词分隔符，因此会把“CD-ROM”看作两个单词。

## 14.2 搜索文本中的短语

要搜索文本中的短语，请用引号将其括起来。

- ⇒ 要输出文件 catalog 中包含单词“Compact Disc”的行，请输入：
  $ grep 'Compact Disc' catalog [RET]

前面的示例会输出文件 catalog 中包含确切字符串“Compact Disc”的所有行；然而，它不会匹配包含“compact disc”或搜索模式中字母大小写有任何变化的行。使用 -i 选项可指定不区分大小写地进行匹配。

- ⇒ 要输出文件 catalog 中包含字符串“compact disc”的行，而不考虑字母的大小写，请输入：
  $ grep -i 'compact disc' catalog [RET]

该命令会输出文件 catalog 中包含“compact disc”模式的任何变体形式的行，包括“Compact Disc”、“COMPACT DISC”和“comPact dISC”。

需要注意的是，grep 只匹配出现在单行上的模式，因此在前面的示例中，如果 catalog 中的一行以单词“compact”结尾，而下一行以“disc”开头，则该命令不会匹配这两行。grep 有一种方法可以绕过这个问题（参见配方 14.4.3 [忽略间距查找短语]，第 343 页），Emacs 中也有一种方法可以做到（参见配方 14.9.2 [在 Emacs 中搜索短语]，第 353 页）。

搜索字符串中可以包含制表符以及空格字符。要在引号字符串中输入制表符，先输入 [CTRL]-(V)，然后输入 [TAB]（参见配方 3.1.2 [输入控制字符]，第 55 页）。

- ⇒ 要输出 screenplay 中仅在直接前面有制表符时才包含文本“In the beginning”的行，请输入：
  $ grep '[CTRL]-(V)[TAB]In the beginning' screenplay [RET]

某些特殊字符具有保留含义，若要搜索它们，必须以特殊方式指定，如下一配方所述。

句点字符 (.) 就是此类字符之一。尽管如此，当仅搜索字符串时，你可以使用 -F 选项指定给出的模式是一个固定字符串，其中完全不包含特殊字符。

fgrep 等同于带 -F 选项的 grep。它是分配用于执行特殊用途的 grep 的两种变体之一（另一种将在下面讨论）。

- ⇒ 以下是两种使用方法。
  - 要不区分大小写地在文件 screenplay 中搜索短语“the end.”，请输入：
    $ grep -F 'the end.' screenplay RET
  - 要不区分大小写地在文件 screenplay 中搜索短语“the end.”，请输入：
    $ fgrep 'the end.' screenplay RET

前面两个示例的结果是相同的。

要搜索包含双引号字符的字符串，请使用单引号将其括起来，反之亦然。当你要搜索的文本同时包含两种引号字符时，不要对字符串加引号，而是用反斜杠字符（\）为字符串中的每个引号和空格字符加上前缀。

- ⇒ 以下是一些使用方法。
  - 要输出文件 screenplay 中包含字符串 `"Frankly, Scarlett," he said,` 的所有行，请输入：
    $ grep '"Frankly, Scarlett," he said,' screenplay RET
  - 要输出文件 screenplay 中包含字符串“I don’t give,” 的所有行，请输入：
    $ grep "I don’t give" screenplay RET
  - 要输出文件 screenplay 中包含字符串“Don’t say “Goodbye”；” 的所有行，请输入：
    $ grep Don\'t\ say\ \"Goodbye\" screenplay RET

## 14.3 匹配文本模式

除了单词和短语搜索之外，你还可以使用 grep 查找复杂的文本模式。称为正则表达式（或简称为“regexps”），它是一个指定要匹配的模式集的文本字符串。正则表达式是 UNIX 世界中的一个基本概念，也是用计算机搜索文本的最强大的方式。

从技术上讲，前几配方中描述的单词或短语模式是正则表达式——只是非常简单的正则表达式。它们指定给定的单词或短语作为要匹配的模式集。

