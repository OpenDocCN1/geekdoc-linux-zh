
# 第12章 分析文本

Emacs 在回显缓冲区（echo buffer）中输出当前缓冲区的每页行数。例如，如果输出为`Page has 351 lines (69 + 282)`，这意味着页面包含 351 行，光标位于第 70 行——该行之前有 69 行，之后有 283 行。

## 12.2 为文本创建词表

*词表*（concordance）是文本中所有单词及其上下文的索引。使用一些 bash 工具：`tr`、`sort` 和 `uniq`，可以轻松创建文本中所有单词的字母顺序列表及其频率统计。

- 输出文件`naked_lunch`的词频列表，输入：

```
$ tr ' ' < naked_lunch | sort | uniq -c RET
```

> 命令`translate`将所有空格字符转换为换行符，每个单词占一行输出文本；然后按字母顺序进行排序，并输出给`uniq`，后者只输出*唯一*单词（即非重复行），而`-c`选项会在每行前标上其*计数*（该单词在文本中出现的次数）。

要获取词频统计——即文本中所有*不同*单词的总数——只需将词频列表的输出管道传递给带有`-l`选项的`wc`。这会统计输入的所有行，在本例中即每行一个唯一单词的列表。

- 输出文本文件`naked_lunch`中唯一单词的计数，输入：

```
$ tr ' ' ' ' RET | sort | uniq -c | wc -l RET
> naked_lunch sort | uniq -c | wc -l RET
```

## 12.3 文本相关性

以下方案展示了如何分析给定文本与其他文本（无论是关键词还是整个文本文件）的相关性。

你可以使用`diff`系列工具来分析文本之间的差异；这些工具特别适合比较同一个文件的不同版本（参见方案 8.4 [比较文件]，第 101 页）。

### 12.3.1 按相关性排序文本

Debian: `rel`
WWW: http://www.johncon.com/

使用`rel`分析文本文件与给定关键词集的相关性。它输出与给定关键词相关的文件名，并按相关性顺序排序；如果文件不符合标准，则不会在相关性列表中输出。

`rel`接受一个关键词选项来搜索引号；你可以通过括号组合多个关键词，并在它们之间使用以下任何运算符来构建布尔表达式：

| 运算符 | 说明 |
| --- | --- |
| \| | 逻辑“或”。 |
| & | 逻辑“与”。 |
| ! | 逻辑“非”。 |

提供要排序的文件名作为参数。

- 按关键词`saving`和`profit`的相关性对`report.a`、`report.b`和`report.c`排序，输入：
  `$ rel "(saving & profit)" report.a report.b report.c RET`

提供目录树名称以分析该目录树中的所有文件。

- 输出`/mail`目录下包含`invitation`或`request`的文件列表，按相关性顺序排序，输入：
  `$ rel "(invitation & request)" "/mail" RET`

- 输出`/mail`目录下包含`invitation`但不包含`wedding`的文件列表，按相关性顺序排序，输入：
  `$ rel "(invitation & party)" "/mail" RET`

### 12.3.2 在 Emacs 中列出相关文件

Debian: `remembrance-agent`
WWW: http://www.media.mit/~rhodes/RA/

Remembrance Agent（记忆代理）的目的是分析你在 Emacs 会话中输入的文本，并在后台寻找相似的行。

## 12.4 在文本中寻找异位词

Debian: `an`

异位词（anagram）是指由完全相同的字母组成的单词或短语，例如`stop`和`tops`。
使用`an`寻找异位词；它将结果输出到标准输出，输入：

- 输出`lake`的所有异位词：
  `$ an lake`

- 输出`lakes and oceans`的所有异位词，输入：
  `$ an 'lakes and oceans' RET`

- 输出包含给定字符串的异位词，使用`-c`选项指定该字符串：
  `$ an -c seas 'lakes and oceans'`

要打印生成的单词，使用`-w`选项：
  `$ an -w seas RET`

## 12.5 在文本中寻找回文

回文（palindrome）是指正反读都相同的单词，例如`Mom`、`madam.`和`nun`。

要在文件中查找回文，请使用这个简单的 Perl 单行命令，并将`file`替换为要检查的文件：

```
perl -ln 'print if reverse' file
```
