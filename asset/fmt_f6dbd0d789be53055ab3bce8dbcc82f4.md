
| `-n` | `--line-number` | Prefix each matching line with the number of the line within the file. |
| `-h` | `--no-filename` | For multifile searches, suppress the output of filenames. |

To more fully explore `grep`, let’s create some text files to search.

```
[me@linuxbox ~]$ ls /bin > dirlist-bin.txt
[me@linuxbox ~]$ ls /usr/bin > dirlist-usr-bin.txt
[me@linuxbox ~]$ ls /sbin > dirlist-sbin.txt
[me@linuxbox ~]$ ls /usr/sbin > dirlist-usr-sbin.txt
[me@linuxbox ~]$ ls dirlist*.txt
dirlist-bin.txt  dirlist-sbin.txt  dirlist-usr-sbin.txt
dirlist-usr-bin.txt
```

We can perform a simple search of our list of files like this:

```
[me@linuxbox ~]$ grep bzip dirlist*.txt
dirlist-bin.txt:bzip2
```

```
dirlist-bin.txt:bzip2recover
```

In this example, `grep` searches all the listed files for the string `bzip` and finds two matches, both in the file `dirlist-bin.txt`. If we were interested only in the list of files that contained matches rather than the matches themselves, we could specify the `-l` option.

```
[me@linuxbox ~]$ grep -l bzip dirlist*.txt
dirlist-bin.txt
```

Conversely, if we wanted to see only a list of the files that did not contain a match, we could do this:

```
[me@linuxbox ~]$ grep -L bzip dirlist*.txt
dirlist-sbin.txt
dirlist-usr-bin.txt
dirlist-usr-sbin.txt
```

## Metacharacters and Literals

While it might not seem apparent, our `grep` searches have been using regular expressions all along, albeit very simple ones. The regular expression `bzip` is taken to mean that a match will occur only if the line in the file contains at least four characters and that somewhere in the line the characters `b`, `z`, `i`, and `p` are found in that order, with no other characters in between. The characters in the string `bzip` are all literal characters, in that they match themselves. In addition to literals, regular expressions may also include metacharacters that are used to specify more complex matches. Regular expression metacharacters consist of the following:

```
^ $ . [ ] { } - ? * + ( ) | \
```

All other characters are considered literals, though the backslash character is used in a few cases to create metasequences, as well as allowing the metacharacters to be escaped and treated as literals instead of being interpreted as metacharacters.

### NOTE

正如我们所见，许多正则表达式元字符也是在展开时对 shell 具有意义的字符。当我们在命令行上传递包含元字符的正则表达式时，必须将其用引号括起来，以防止 shell 尝试展开它们。

## The Any Character

我们要看的第一个元字符是点 `(.)` 或句点字符，用于匹配任意字符。如果我们将其包含在正则表达式中，它将匹配该字符位置中的任意字符。以下是一个示例：

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

我们搜索了文件中与正则表达式 `.zip` 匹配的任意行。关于结果，有几件有趣的事情需要注意。请注意，`zip` 程序未被找到。这是因为我们在正则表达式中包含点元字符，使所需匹配的长度增加到四个字符，而名称 `zip` 仅包含三个字符，因此不匹配。此外，如果我们的列表中包含任何文件扩展名为 `.zip` 的文件，它们也会被匹配，因为文件扩展名中的句点字符也会被“任意字符”匹配。

## Anchors

插入号 (`^`) 和美元符号 (`$`) 在正则表达式中被视为 *锚点*。这意味着它们仅在正则表达式出现在行首 (`^`) 或行尾 (`$`) 时才导致匹配发生。

```
[me@linuxbox ~]$ grep -h '^zip' dirlist*.txt
zip
zipcloak
zipgrep
zipinfo
zipnote
zipsplit
[me@linuxbox ~]$ grep -h 'zip$' dirlist*.txt
gunzip
gzip
funzip
gpg-zip
preunzip
prezip
unzip
zip
[me@linuxbox ~]$ grep -h '^zip$' dirlist*.txt
zip
```

在这里，我们搜索文件列表中位于行首、行尾以及同时位于行首和行尾的字符串 `zip`（即单独一行）。请注意，正则表达式 `^$`（开头和结尾之间没有任何内容）将匹配空白行。

## A CROSSWORD PUZZLE HELPER

即使我们目前对正则表达式的了解有限，我们也可以做一些有用的事情。

我妻子喜欢填字游戏，她有时会请我帮忙解答某个问题。比如，“第三个字母是 `j`、最后一个字母是 `r` 的五字母单词是什么意思……？” 这类问题让我思考。

你知道你的 Linux 系统包含一个词典吗？确实如此。查看 `/usr/share/dict` 目录，你可能会找到一个或多个词典。那里的词典文件只是按字母顺序排列的长单词列表，每行一个单词。在我的系统上，`words` 文件包含略多于 98,500 个单词。要找到上面填字游戏问题的可能答案，我们可以这样做：

```
[me@linuxbox ~]$ grep -i '^..j.r$' /usr/share/dict/words
Major
major
```

使用此正则表达式，我们可以找到词典文件中所有长度为五个字母、第三个位置为 `j`、最后一个位置为 `r` 的单词。

## Bracket Expressions and Character Classes

除了在正则表达式的给定位置匹配任意字符外，我们还可以通过使用括号表达式来匹配来自指定字符集的单个字符。使用括号表达式，我们可以指定一组字符（包括否则会被解释为元字符的字符）以进行匹配。在此示例中，使用一个包含两个字符的集合，我们匹配包含字符串 `bzip` 或 `gzip` 的任意行：

```
[me@linuxbox ~]$ grep -h '[bg]zip' dirlist*.txt
bzip2
bzip2recover
gzip
```

一个集合可以包含任意数量的字符，并且元字符在放在括号内时会失去其特殊含义。然而，在括号表达式中使用元字符并具有不同含义的情况有两种。第一种是插入号 (`^`)，它用于
