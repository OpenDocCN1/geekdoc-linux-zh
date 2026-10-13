
```
$nntp->datasend('Newsgroups: news.announce\n');

$nntp->datasend('Subject: FAQ - Frequently Asked Questions\n');

$nntp->datasend('From: ADMIN <root@arcbowen.com>\n');

$nntp->datasend('\n\n');

# for each line in the post array, send it

for (@post)

{

    $nntp->datasend($_);

} # End for

$nntp->quit;
```

## 单行脚本

Perl 擅长的其中一种形式是单行脚本（`one-liner`）。人们会花很大的功夫将任务减少到一行 Perl 代码。Perl 有一种不太公平的声誉，即难以阅读。事实是，你可以在任何语言中编写难以阅读的代码。Perl 允许用多种方法完成某事，这自然而然地导致人们试图寻找最晦涩的方式来完成事情。

以兰达尔·施瓦茨（Randal Schwartz）的名字命名，*施瓦茨变换*（Schwartzian transform）是一种根据不明显标准对数组进行排序的方法。排序函数按字母顺序对数组进行排序，这很直观。那么，如果你想按第三个单词对字符串数组进行字母排序呢？也许你想要更实用的东西，例如按文件大小对文件列表进行排序？施瓦茨变换会创建一个新列表，其中包含你希望用于排序的信息，并引用原始列表。然后，你排序新列表，并以此来确定原始列表应采用的顺序。这里有一个简单的例子，按长度对字符串列表进行排序：

```perl
@sorted_by_length =
    map { $_->[0] }        # 提取原始列表
    sort { $a->[1] <=> $b->[1] }  # 按转换后的值排序
    map { [$_, length($_)] }      # 映射为包含元素长度的列表
    @list;
```

由于每个运算符都作用于其紧邻右侧的内容，因此从右向左阅读（或者像这里那样从上到下阅读）会很有帮助。

首先作用于列表的是 `map` 运算符。它将列表转换为一个哈希，其中键是列表元素，值是各元素的长度。这是你放入代码以执行排序所需转换的地方。

下一个运算符是 `sort` 函数，它按值对列表进行排序。最后，哈希通过提取其键被重新转换回数组。现在数组已处于所需的顺序。

## 命令行处理

Perl 在解析各种程序的输出方面表现出色。这是许多人使用 `awk` 和 `sed` 等工具完成的任务。Perl 为你提供了更大的词汇量来执行这些任务。以下示例非常简单，但说明了你如何使用 Perl 截取部分输出并对其进行处理。在示例中，Perl 用于仅列出大于 10KB 的文件：

```bash
$ ls -la | perl -nae 'print "@F[0] is @F[4]\n"  if @F[4] > 10000;'
```
