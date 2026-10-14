

包含标准输出匹配的行。

到目前为止，我们一直使用 grep 进行固定字符串搜索，如下所示：

```
[me@linuxbox ~]$ ls /usr/bin | grep zip
```

这将列出 /usr/bin 目录中文件名包含子字符串“zip”的所有文件。

grep 程序以这种方式接受选项和参数：

```
grep [options] regex [file...]
```

其中 regex 是一个正则表达式。

以下是常用的 grep 选项列表：

Table20-1: grep Options

| Option | Description |
| --- | --- |
| -i | 忽略大小写。不区分大小写字符。也可指定 --ignore-case。 |
| -v | 反转匹配。正常情况下，grep 打印包含匹配的行。此选项会使 grep 打印所有不包含匹配的行。也可指定 --invert-match。 |
| -c | 打印匹配数（如果同时指定了 -v 选项，则为不匹配数）而不是行本身。也可指定 --count。 |
| -l | 打印包含匹配的每个文件的文件名，而不是行本身。也可指定 --files-with-matches。 |
| -L | 类似 -l 选项，但只打印不包含匹配的文件名。也可指定 --files-without-match。 |
| -n | 在每个匹配行前加上该行在文件中的行号。也可指定 --line-number。 |
| -h | 对于多文件搜索，抑制文件名输出。也可指定 --no-filename。 |

为了更全面地探索 grep，让我们创建一些用于搜索的文本文件：

```
[me@linuxbox ~]$ ls /bin > dirlist-bin.txt
[me@linuxbox ~]$ ls /usr/bin > dirlist-usr-bin.txt
[me@linuxbox ~]$ ls /sbin > dirlist-sbin.txt
[me@linuxbox ~]$ ls /usr/sbin > dirlist-usr-sbin.txt
[me@linuxbox ~]$ ls dirlist*.txt
dirlist-bin.txt    dirlist-sbin.txt    dirlist-usr-sbin.txt
dirlist-usr-bin.txt
```

我们可以像这样对文件列表执行简单搜索：

```
[me@linuxbox ~]$ grep bzip dirlist*.txt
dirlist-bin.txt:bzip2
dirlist-bin.txt:bzip2recover
```

在此示例中，grep 在所有列出的文件中搜索字符串 bzip，并在文件 dirlist-bin.txt 中找到了两个匹配项。如果我们只对包含匹配项的文件列表感兴趣，而不是匹配项本身，可以指定 -l 选项：

```
[me@linuxbox ~]$ grep -l bzip dirlist*.txt
dirlist-bin.txt
```

相反，如果我们只想查看不包含匹配项的文件列表，可以这样做：

```
[me@linuxbox ~]$ grep -L bzip dirlist*.txt
dirlist-sbin.txt
dirlist-usr-bin.txt
dirlist-usr-sbin.txt
```

## Metacharacters And Literals

虽然可能并不明显，但我们的 grep 搜索一直在使用正则表达式，只不过是非常简单的。正则表达式“bzip”意味着只有当文件中的行至少包含四个字符，并且在某处按顺序包含字符“b”、“z”、“i”和“p”，且中间没有其他字符时，才会发生匹配。字符串“bzip”中的字符都是字面字符，因为它们匹配自身。除了字面字符外，正则表达式还可能

包含用于指定更复杂匹配的 *metacharacters*。正则表达式元字符包括以下内容：

^ $ . [ ] { } - ? * + ( ) | \

所有其他字符都被视为字面字符，尽管反斜杠字符在某些情况下用于创建 *meta sequences*，以及允许元字符被转义并作为字面字符处理而不是被解释为元字符。

> **Note:** 正如我们所见，许多正则表达式元字符也是在 shell 执行展开时具有含义的字符。当我们在命令行上传递包含元字符的正则表达式时，必须将其用引号括起来，以防止 shell 尝试展开它们。

## The Any Character

我们要看的第一个元字符是点或句点字符，用于匹配任意字符。如果在正则表达式中包含它，它将匹配该字符位置的任何字符。以下是示例：

```
[me@linuxbox ~]$ grep -h '.zip' dirlist*.txt
bunzip2
bzip2
bzip2recover
gunzip
gzip
funzip
gpg-zip
preunzip
prezip
prezip-bin
unzip
unzipsfx
```

我们搜索了文件中与正则表达式“.zip”匹配的任意行。结果有几个有趣的地方需要注意。注意程序 zip 并未被找到。这是因为在正则表达式中包含点元字符使所需匹配的长度增加到四个字符，而名称“zip”仅包含三个字符，因此不匹配。此外，如果我们的列表中存在任何包含文件扩展名 .zip 的文件，它们也会被匹配，因为文件扩展名中的句点字符也被视为“任意字符”。

